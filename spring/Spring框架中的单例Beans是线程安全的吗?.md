# Spring 框架中的单例 Beans 是线程安全的吗？

Spring 框架并没有对单例 Bean 进行任何多线程的封装处理。关于单例 Bean 的线程安全和并发问题需要开发者自行去搞定。但实际上，大部分的 Spring Bean 并没有可变的状态(比如 Service 类和 DAO 类)，所以在某种程度上说 Spring 的单例 Bean 是线程安全的。如果你的 Bean 有多种状态的话（比如 View Model 对象），就需要自行保证线程安全。最浅显的解决办法就是将多态 Bean 的作用域由“singleton”变更为“prototype”。