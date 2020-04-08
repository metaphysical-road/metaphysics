# Spring实现事务原理

事务是数据库操作的最小工作单元，是作为单个逻辑工作单元执行的一系列操作；这些操作作为一个整体一起向系统提交，要么都执行、要么都不执行；事务是一组不可再分割的操作集合（工作逻辑单元）。

事务特性：ACID

1. 原子性：事务不可分割
2. 一致性：事务执行的前后，数据完整性保持一致
3. 隔离性：一个事务执行的时候，不应该受到其他事务的打扰
4. 持久性：一旦结束，数据就永久的保存到数据库

Spring 中有自己的事务管理机制，使用 TransactionMananger 进行管理，可以通过 Spring 的注入来完成此功能。提供了以下几个事务处理的类：

1. TransactionDefinition：事务属性定义，定义了事务传播行为 类型（ 7 种），事务隔离类型（ 5 种），超时设置等。
2. TranscationStatus：代表了当前的事务，可以提交、回滚。
3. PlatformTransactionManager：这个是 Spring 提供的用于管理事务的基础接口。通过这个接口，Spring 可以为如 JDBC、Hibernate 等提供了对应的事务管理器，具体的实现就是各个平台来实现。

事务定义样例：

```java
TransactionDefinition td = new TransactionDefinition();  
TransactionStatus ts = transactionManager.getTransaction(td);  
try{  
    //do sth  
    transactionManager.commit(ts);  
}catch(Exception e){  
    transactionManager.rollback(ts);  
}  
```

Spring 事务管理实现方式有两种：编程式事务管理和声明式事务。

**1. 编程式事务**

使用 TransactionTemplate 或使用底层的 PlatformTransactionManager，显式的方式调用 beginTransaction() 开启事务、commit() 提交事务、rollback() 回滚事务，编写代码形式来声明事务。

**2. 声明式事务**

底层是建立在 Spring AOP 的基础上，在方式执行前后进行拦截，并在目标方法开始执行前创建新事务或加入一个已存在事务，最后在目标方法执行完后根据情况提交或者回滚事务。

声明式事务的优点：不需要编程，减少了代码的耦合，在配置文件中配置并在目标方法上添加 @Transactional注解来实现。