# 为什么说 Spring 是一个容器？

Spring 容器是整个 Spring 框架的核心，通常我们说的 Spring 容器就是 Bean 工厂，Bean 工厂负责创建和初始化 Bean、装配 Bean 并且管理应用程序中的 bean.spring 中提供了两个核心接口——BeanFactory 和 ApplicationContext，ApplicationContext 是 BeanFactory 子接口，它提供了比 BeanFactory 更完善的功能。