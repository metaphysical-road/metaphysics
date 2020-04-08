# 请介绍一下设计模式在Spring框架中的使用?

- 工厂模式：BeanFactory 就是简单工厂模式的体现，用来创建对象的实例。
- 单例模式：Bean 默认为单例模式。
- 代理模式：Spring 的 AOP 功能用到了 JDK 的动态代理和 CGLIB 字节码生成技术。
- 模板方法：用来解决代码重复的问题。比如：RestTemplate, JmsTemplate, JpaTemplate。
- 观察者模式：定义对象键一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都会得到通知被制动更新，如 Spring 中 listener 的实现：ApplicationListener。