# Spring框架中有哪些不同类型的事件?

Spring 提供了以下 5 种标准的事件：

- 上下文更新事件（ ContextRefreshedEvent ）：在调用 ConfigurableApplicationContext 接口中的 refresh() 方法时被触发。
- 上下文开始事件（ ContextStartedEvent ）：当容器调用 ConfigurableApplicationContext的Start() 方法开始/重新开始容器时触发该事件。
- 上下文停止事件（ ContextStoppedEvent ）：当容器调用 ConfigurableApplicationContext的Stop() 方法停止容器时触发该事件。
- 上下文关闭事件（ ContextClosedEvent ）：当 ApplicationContext 被关闭时触发该事件。容器被关闭时，其管理的所有单例 Bean 都被销毁。
- 请求处理事件（ RequestHandledEvent ）：在 Web 应用中，当一个 HTTP 请求（ request ）结束触发该事件。 如果一个 Bean 实现了 ApplicationListener 接口，当一个 ApplicationEvent 被发布以后，Bean 会自动被通知。