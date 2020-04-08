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

#### [2.1.3 Spring Bean 注入是如何解决循环依赖](spring/Spring Bean 注入是如何解决循环依赖.md)

#### [2.1.4 Spring 事务失效问题](spring/Spring 事务失效问题.md)

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

#### 2.1.11 请详细介绍一下 Spring MVC 的流程？

- 用户发送请求至前端控制器 DispatcherServlet
- DispatcherServlet 收到请求调用 HandlerMapping 处理器映射器。
- 处理器映射器根据请求 url 找到具体的处理器，生成处理器对象及处理器拦截器（如果有则生成）可以一并返回给 DispatcherServlet。
- DispatcherServlet 通过 HandlerAdapter 处理器适配器调用处理器
- 执行处理器（Controller，也叫后端控制器）。
- Controller 执行完成返回 ModelAndView。
- HandlerAdapter 将 controller 执行结果 ModelAndView 返回给 DispatcherServlet。
- DispatcherServlet 将 ModelAndView 传给 View Reslover 视图解析器。
- View Reslover 解析后返回具体 View。
- DispatcherServlet 对 View 进行渲染视图（即将模型数据填充至视图中）。
- DispatcherServlet 响应用户。

#### 2.1.12 请介绍一下设计模式在 Spring 框架中的使用？

- 工厂模式：BeanFactory 就是简单工厂模式的体现，用来创建对象的实例。
- 单例模式：Bean 默认为单例模式。
- 代理模式：Spring 的 AOP 功能用到了 JDK 的动态代理和 CGLIB 字节码生成技术。
- 模板方法：用来解决代码重复的问题。比如：RestTemplate, JmsTemplate, JpaTemplate。
- 观察者模式：定义对象键一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都会得到通知被制动更新，如 Spring 中 listener 的实现：ApplicationListener。

#### 2.1.13 解释 Spring 支持的几种 Bean 的作用域

Spring 框架支持以下五种 Bean 的作用域：

- singleton：Bean 在每个 Spring IoC 容器中只有一个实例。
- prototype：一个 Bean 的定义可以有多个实例。
- request：每次 http 请求都会创建一个 Bean，该作用域仅在基于 Web 的 Spring ApplicationContext 情形下有效。
- session：在一个 HTTP Session 中，一个 Bean 定义对应一个实例。该作用域仅在基于 Web 的 Spring ApplicationContext 情形下有效。
- global-session：在一个全局的 HTTP Session 中，一个 Bean 定义对应一个实例。该作用域仅在基于 Web 的 Spring ApplicationContext 情形下有效。

缺省的 Spring Bean 的作用域是 Singleton。

#### 2.1.14 你可以在 Spring 中注入一个 null 和一个空字符串吗？

可以

#### 2.1.15 Spring 的生命周期？

- instantiate Bean 对象实例化
- populate properties 封装属性
- 如果 Bean 实现 BeanNameAware 执行 setBeanName
- 如果 Bean 实现 BeanFactoryAware 或者 ApplicationContextAware 设置工厂 setBeanFactory 或者上下文对象 setApplicationContext
- 如果存在类实现 BeanPostProcessor（后处理 Bean） ，执行 postProcessBeforeInitialization，BeanPostProcessor 接口提供钩子函数，用来动态扩展修改 Bean。（程序自动调用后处理 Bean）
- 如果 Bean 实现 InitializingBean 执行 afterPropertiesSet
- 调用 `<bean init-method="init">` 指定初始化方法 init
- 如果存在类实现 BeanPostProcessor（处理 Bean），执行postProcessAfterInitialization
- 执行业务处理
- 如果 Bean 实现 DisposableBean 执行 destroy
- 调用 `<bean destroy-method="customerDestroy">` 指定销毁方法 customerDestroy

#### 2.1.16 Spring 如何处理线程并发问题？

Spring 使用 ThreadLocal 解决线程安全问题。

我们知道在一般情况下，只有无状态的 Bean 才可以在多线程环境下共享，在 Spring 中，绝大部分 Bean 都可以声明为 singleton 作用域。就是因为 Spring 对一些 Bean （如 RequestContextHolder、TransactionSynchronizationManager、LocaleContextHolder 等）中非线程安全状态采用 ThreadLocal 进行处理，让它们也成为线程安全的状态，因为有状态的 Bean 就可以在多线程中共享了。

ThreadLocal 和线程同步机制都是为了解决多线程中相同变量的访问冲突问题。在同步机制中，通过对象的锁机制保证同一时间只有一个线程访问变量。这时该变量是多个线程共享的，使用同步机制要求程序慎密地分析什么时候对变量进行读写，什么时候需要锁定某个对象，什么时候释放对象锁等繁杂的问题，程序设计和编写难度相对较大。而 ThreadLocal 则从另一个角度来解决多线程的并发访问。 ThreadLocal 会为每一个线程提供一个独立的变量副本，从而隔离了多个线程对数据的访问冲突。因为每一个线程都拥有自己的变量副本，从而也就没有必要对该变量进行同步了。 ThreadLocal 提供了线程安全的共享对象，在编写多线程代码时，可以把不安全的变量封装进 ThreadLocal。

由于 ThreadLocal 中可以持有任何类型的对象，低版本 JDK 所提供的 get() 返回的是 Object 对象，需要强制类型转换。但 JDK 5.0 通过泛型很好的解决了这个问题，在一定程度地简化 ThreadLocal 的使用。概括起来说，对于多线程资源共享的问题，同步机制采用了“以时间换空间”的方式，而 ThreadLocal 采用了“以空间换时间”的方式。前者仅提供一份变量，让不同的线程排队访问，而后者为每一个线程都提供了一份变量，因此可以同时访问而互不影响。

#### 2.1.17 为什么说 Spring 是一个容器？

Spring 容器是整个 Spring 框架的核心，通常我们说的 Spring 容器就是 Bean 工厂，Bean 工厂负责创建和初始化 Bean、装配 Bean 并且管理应用程序中的 bean.spring 中提供了两个核心接口——BeanFactory 和 ApplicationContext，ApplicationContext 是 BeanFactory 子接口，它提供了比 BeanFactory 更完善的功能。

#### 2.1.18 Spring 框架中的单例 Beans 是线程安全的么？

Spring 框架并没有对单例 Bean 进行任何多线程的封装处理。关于单例 Bean 的线程安全和并发问题需要开发者自行去搞定。但实际上，大部分的 Spring Bean 并没有可变的状态(比如 Service 类和 DAO 类)，所以在某种程度上说 Spring 的单例 Bean 是线程安全的。如果你的 Bean 有多种状态的话（比如 View Model 对象），就需要自行保证线程安全。最浅显的解决办法就是将多态 Bean 的作用域由“singleton”变更为“prototype”。

#### 2.1.19 Spring 框架中有哪些不同类型的事件？

Spring 提供了以下 5 种标准的事件：

- 上下文更新事件（ ContextRefreshedEvent ）：在调用 ConfigurableApplicationContext 接口中的 refresh() 方法时被触发。
- 上下文开始事件（ ContextStartedEvent ）：当容器调用 ConfigurableApplicationContext的Start() 方法开始/重新开始容器时触发该事件。
- 上下文停止事件（ ContextStoppedEvent ）：当容器调用 ConfigurableApplicationContext的Stop() 方法停止容器时触发该事件。
- 上下文关闭事件（ ContextClosedEvent ）：当 ApplicationContext 被关闭时触发该事件。容器被关闭时，其管理的所有单例 Bean 都被销毁。
- 请求处理事件（ RequestHandledEvent ）：在 Web 应用中，当一个 HTTP 请求（ request ）结束触发该事件。 如果一个 Bean 实现了 ApplicationListener 接口，当一个 ApplicationEvent 被发布以后，Bean 会自动被通知。

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