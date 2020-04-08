# Spring Bean 注入是如何解决循环依赖

## 1 什么是循环依赖，有啥问题？

循环依赖就是 N 个类中循环嵌套引用，这样会导致内存溢出。循环依赖主要分两种：

- 构造器循环依赖
- setter 循环依赖                  

## 2 如何解决循环依赖

- 使用优先级注解  @Lazy
- 使用条件注解  @ConditionalOnClass  @AutoConfigureAfter @ConditionalOnMissingBean