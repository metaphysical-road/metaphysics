# 解释Spring支持的几种Bean的作用域

Spring 框架支持以下五种 Bean 的作用域：

- singleton：Bean 在每个 Spring IoC 容器中只有一个实例。
- prototype：一个 Bean 的定义可以有多个实例。
- request：每次 http 请求都会创建一个 Bean，该作用域仅在基于 Web 的 Spring ApplicationContext 情形下有效。
- session：在一个 HTTP Session 中，一个 Bean 定义对应一个实例。该作用域仅在基于 Web 的 Spring ApplicationContext 情形下有效。
- global-session：在一个全局的 HTTP Session 中，一个 Bean 定义对应一个实例。该作用域仅在基于 Web 的 Spring ApplicationContext 情形下有效。

缺省的 Spring Bean 的作用域是 Singleton。