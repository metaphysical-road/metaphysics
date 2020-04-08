# BeanFactory接口和ApplicationContext接口不同点是什么

- ApplicationContext 接口继承 BeanFactory 接口，Spring 核心工厂是 BeanFactory，BeanFactory 采取延迟加载，第一次 getBean 时才会初始化 Bean，ApplicationContext 是会在加载配置文件时初始化 Bean。
- ApplicationContext 是对 BeanFactory 扩展，它可以进行国际化处理、事件传递和 Bean 自动装配以及各种不同应用层的 Context 实现。

开 发 中 基 本 都 在 使 用 ApplicationContext，Web 项 目 使 用 WebApplicationContext ，很少用到 BeanFactory。