# Spring 的生命周期？

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