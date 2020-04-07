# Rocketmq如何保证消息不丢失

消息可以丢失的业务场景：生产阶段、存储阶段、消费阶段

- **Producer** 新建消息，然后通过网络将消息投递给 **MQ Broker**
- 消息将会存储在 **Broker** 端磁盘中
- **Consumer** 将会从 **Broker** 拉取消息

## 1 生产阶段

### 1.1 生产阶段状态机

- **SEND_OK** 消息发送成功。确保消息能够发送成功，但是需要配合**Broker**端存储模式：同步**Master**服务器和同步刷盘，即开启**SYNC_MASTER**和**SYNC_FLUSH**
- **FLUSH_DISK_TIMEOUT** 消息发送成功，但是**Broker**端刷盘超时。此时消息已经进入**Broker**端内存队列，如果**Broker**端宕机，消息才会丢失。消息存储端可以配置刷盘策略和刷盘超时时间，如果配置为**SYNC_FLUSH**(默认为异步刷盘)，当**Broker**未在同步刷盘时间(**5s**)完成刷盘，返回状态机-**FLUSH_DISK_TIMEOUT**
- **FLUSH_SLAVE_TIMEOUT** 消息发送成功，但是**Broker-Master**同步到**Slave**时超时。消息已经在**Broker**端的内存队列中，只有Broker端宕机才会消息才会丢失。如果**Broker**服务器端角色是同步**Master**，即**SYNC_MASTER**(默认是**ASYNC_MASTER**),并且从**Broker**服务器，未在同步刷盘时间(默认为**5秒**)内完成与主服务器的同步，则返回**FLUSH_SLAVE_TIMEOUT**状态-数据同步到**Slave**服务器超时
- **SLAVE_NOT_AVAILABLE** 消息发送成功，但此时**Slave**不可用。如果**Broker**服务器的角色是同步**Master**，即**SYNC_MASTER**(默认是**ASYNC_MASTER**),但是没有配置**Slave Broker**服务器，则返回**SLAVE_NOT_AVAILABLE** 状态-无**Slave**服务器可用

```java
package org.apache.rocketmq.client.producer;

public enum SendStatus {
    SEND_OK,
    FLUSH_DISK_TIMEOUT,
    FLUSH_SLAVE_TIMEOUT,
    SLAVE_NOT_AVAILABLE,
}
```

## 2 存储阶段

- **同步刷盘**   保证 **Broker** 端不丢消息，保证消息的可靠性(**flushDiskType = SYNC_FLUSH** )
- **HA高可用性**   为了保证可用性，**Broker** 通常采用一主（**master**）多从（**slave**）部署方式。为了保证消息不丢失，消息还需要复制到 **slave** 节点。默认方式下，消息写入 **master** 成功，就可以返回确认响应给生产者，接着消息将会异步复制到 **slave** 节点。

### 2.1 存储阶段状态机

```java
public enum GetMessageStatus {

    FOUND,

    NO_MATCHED_MESSAGE,

    MESSAGE_WAS_REMOVING,

    OFFSET_FOUND_NULL,

    OFFSET_OVERFLOW_BADLY,

    OFFSET_OVERFLOW_ONE,

    OFFSET_TOO_SMALL,

    NO_MATCHED_LOGIC_QUEUE,

    NO_MESSAGE_IN_QUEUE,
}
```



## 3 消费阶段

​    消费者从 **broker** 拉取消息，然后执行相应的业务逻辑。一旦执行成功，将会返回 `ConsumeConcurrentlyStatus.CONSUME_SUCCESS` 状态给 **Broker**。如果 **Broker** 未收到消费确认响应或收到其他状态，消费者下次还会再次拉取到该条消息，进行重试。这样的方式有效避免了消费者消费过程发生异常，或者消息在网络传输中丢失的情况。

**消费阶段两种模式状态机**：并行和顺序

```java
public enum ConsumeConcurrentlyStatus {
    /**
     * Success consumption
     */
    CONSUME_SUCCESS,
    /**
     * Failure consumption,later try to consume
     */
    RECONSUME_LATER;
}
public enum ConsumeOrderlyStatus {
    /**
     * Success consumption
     */
    SUCCESS,
    /**
     * Rollback consumption(only for binlog consumption)
     */
    @Deprecated
    ROLLBACK,
    /**
     * Commit offset(only for binlog consumption)
     */
    @Deprecated
    COMMIT,
    /**
     * Suspend current queue a moment
     */
    SUSPEND_CURRENT_QUEUE_A_MOMENT;
}
```

