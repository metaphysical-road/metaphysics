[TOC]

# metaphysics

玄学，架构师玄学之路

## 1 中间件高频问题域

### 1.1 RocketMq 问题域

- [Rocketmq如何保证消息不丢失](systemstability/Rocketmq如何保证消息不丢失.md)
- [Rocketmq 生产端 为什么没有使用缓存并合并批量发送](systemstability/Rocketmq生产端为什么没有是用缓存并合并批量发送.md)
- [Rocketmq具备哪些特性指标](systemstability/Rocketmq具备哪些特性指标.md)

### 1.2 分布式链路追踪(全链路追踪)问题域

- [分布式链路追踪如何选型](https://mp.weixin.qq.com/s?__biz=MzU1NzY1ODAyNQ==&mid=2247483735&idx=1&sn=a68724d3c6feab9b8e61ccd1f579c4ba&chksm=fc333b91cb44b2873028e442a3ab1408b9c2d015f511d5f8f132d524fb8b5544456b09508993&token=644040893&lang=zh_CN#rd)
- [全链路监控落地方案](https://mp.weixin.qq.com/s?__biz=MzU1NzY1ODAyNQ==&mid=2247483724&idx=1&sn=ab9d60c9e01e6d290aa173442a4a783e&chksm=fc333b8acb44b29c26ddbd2b995725cebfe5903c7bd7b9cd869b53280cc1c466ede2837f23e6&token=644040893&lang=zh_CN#rd)

### 1.3 分布式缓存-redis问题域

- [Redis为什么是单线程模型](redis/Redis为什么是单线程模型.md)
- [什么是缓存穿透? 怎么解决?](redis/什么是缓存穿透以及怎么解决.md)
- [什么是缓存雪崩？ 怎么解决？](redis/什么是缓存雪崩以及怎么解决.md)
- [缓存的更新策略有几种？分别有什么注意事项？](redis/缓存的更新策略有几种以及分别有什么注意事项.md)
- [redis会阻塞吗，什么业务场景下会阻塞？](redis/Redis什么业务场景下会阻塞.md)
- [redis的业务场景](redis/Redis的业务场景.md)
- [Redis怎么实现分布式锁](redis/Redis怎么实现分布式锁.md)

### 1.4 分库分表问题域

#### [1.4.1 什么是分库分表？](databasesharding/什么是分库分表.md)

##### [1.4.1.1 数据库存储的演进阶段](databasesharding/数据库存储的演进阶段.md)

##### [1.4.1.2 分库分表的业务场景案例分析](databasesharding/分库分表的业务场景案例分析.md)

#### 1.4.2 分库分表的解决方案

客户端分片、代理分片和支持事务的分布式数据库

##### [1.4.2.1 客户端分片](databasesharding/客户端分片.md)

[1.4.2.2 代理分片](databasesharding/代理分片.md)

[1.4.2.3 支持事务的分布式数据库](databasesharding/支持事务的分布式数据库.md)

### 1.5 定时任务问题域

### 1.6 RPC框架问题域

- RPC框架如何选型
- RPC框架如何保障CAP(高可用性)

## 2 Spring全家桶问题域

### 2.1 Spring

#### [2.1.1 AOP](spring/AOP.md)

#### [2.1.2 IOC](spring/IOC.md)

#### [2.1.3 Spring Bean 注入是如何解决循环依赖](spring/SpringBean注入是如何解决循环依赖.md)

#### [2.1.4 Spring 事务失效问题](spring/Spring事务失效问题.md)

#### 2.1.5 谈谈对 Spring IoC 的理解？

​    IoC Inverse of Control 反转控制的概念。将之前程序中需要手动创建对象的操作，交由 Spring 框架来实现，创建对象的操作被反转到了 Spring 框架。对象的生命周期由 Spring 来管理，直接从 Spring 那里去获取一个对象。

#### 2.1.6 谈谈对 Spring DI 的理解？

​    DI Dependency Injection 依赖注入。Spring 框架创建 Bean 对象时，动态的将依赖对象注入到 Bean 组件中，实现依赖对象的注入。

#### 2.1.7 BeanFactory 接口和 ApplicationContext 接口不同点是什么？

- ApplicationContext 接口继承 BeanFactory 接口，Spring 核心工厂是 BeanFactory，BeanFactory 采取延迟加载，第一次 getBean 时才会初始化 Bean，ApplicationContext 是会在加载配置文件时初始化 Bean。

- ApplicationContext 是对 BeanFactory 扩展，它可以进行国际化处理、事件传递和 Bean 自动装配以及各种不同应用层的 Context 实现。

开 发 中 基 本 都 在 使 用 ApplicationContext，Web 项 目 使 用 WebApplicationContext ，很少用到 BeanFactory。

#### 2.1.8 请介绍你熟悉的 Spring 核心类，并说明有什么作用？

- BeanFactory：产生一个新的实例，可以实现单例模式
- BeanWrapper：提供统一的 get 及 set 方法
- ApplicationContext：提供框架的实现，包括 BeanFactory 的所有功能。

#### [2.1.9 Spring实现事务原理](spring/Spring实现事务原理.md)

#### 2.1.10 解释下AOP

​    AOP（Aspect-Oriented Programming）是一种程序设计类型，它通过分离横切关注点来增加程序的模块化。AOP 在不修改现有代码的情况下对现有代码添加功能，这个是 AOP 最重要的能力。

#### [2.1.11 请详细介绍一下 Spring MVC 的流程？](spring/请详细介绍一下SpringMVC的流程?)

#### [2.1.12 请介绍一下设计模式在 Spring 框架中的使用？](spring/请介绍一下设计模式在Spring框架中的使用?.md)

#### [2.1.13 解释 Spring 支持的几种 Bean 的作用域](spring/解释Spring支持的几种Bean的作用域.md)

#### 2.1.14 你可以在 Spring 中注入一个 null 和一个空字符串吗？

可以

#### [2.1.15 Spring 的生命周期？](spring/Spring的生命周期?)

#### [2.1.16 Spring 如何处理线程并发问题？](spring/Spring如何处理线程并发问题?.md)

#### [2.1.17 为什么说 Spring 是一个容器？](spring/为什么说Spring是一个容器?.md)

Spring 容器是整个 Spring 框架的核心，通常我们说的 Spring 容器就是 Bean 工厂，Bean 工厂负责创建和初始化 Bean、装配 Bean 并且管理应用程序中的 bean.spring 中提供了两个核心接口——BeanFactory 和 ApplicationContext，ApplicationContext 是 BeanFactory 子接口，它提供了比 BeanFactory 更完善的功能。

#### [2.1.18 Spring 框架中的单例 Beans 是线程安全的吗？](spring/Spring框架中的单例Beans是线程安全的吗?.md)

#### [2.1.19 Spring 框架中有哪些不同类型的事件？](spring/Spring框架中有哪些不同类型的事件?.md)

#### 2.1.20 如何给 Spring 容器提供配置元数据?

- XML 配置文件
- 基于注解的配置
- 基于 Java 的配置

#### 2.1.21 Spring MVC 的控制器是不是单例模式,如果是,有什么问题,怎么解决？

是单例模式，所以在多线程访问的时候有线程安全问题，不要用同步，会影响性能的，解决方案是在控制器里面不能写字段。

## 3 系统高可用建设方法论

undo

## 4 系统高性能建设方法论

undo

## 5 系统高并发建设方法论