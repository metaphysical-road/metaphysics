# Rocketmq如何保证消息不丢失

消息可以丢失的业务场景：生产阶段、存储阶段、消费阶段

- Producer 新建消息，然后通过网络将消息投递给 MQ Broker
- 消息将会存储在 Broker 端磁盘中
- Consumer 将会从 Broker 拉取消息

## 1 生产阶段

### 1.1 生产阶段状态机

- **SEND_OK** 消息发送成功。确保消息能够发送成功，但是需要配合**Broker**端存储模式：同步**Master**服务器和同步刷盘，即开启**SYNC_MASTER**和**SYNC_FLUSH**
- **FLUSH_DISK_TIMEOUT** 消息发送成功，但是**Broker**端刷盘超时。此时消息已经进入**Broker**端内存队列，如果**Broker**端宕机，消息才会丢失。消息存储端可以配置刷盘策略和刷盘超时时间，如果配置为**SYNC_FLUSH**(默认为异步刷盘)，当**Broker**未在同步刷盘时间(**5s**)完成刷盘，返回状态机-**FLUSH_DISK_TIMEOUT**

```java
package org.apache.rocketmq.client.producer;

public enum SendStatus {
    SEND_OK,
    FLUSH_DISK_TIMEOUT,
    FLUSH_SLAVE_TIMEOUT,
    SLAVE_NOT_AVAILABLE,
}
```

## 2 生产阶段

## 3 消费阶段