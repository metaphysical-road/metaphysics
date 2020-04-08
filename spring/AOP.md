# AOP

## 1 AOP 重要概念

- Aspect（切面） Aspect 就是对我们横切关注点的抽象和描述，定义了需要对哪些方法或者是类、字段进行拦截和操作。
- Joinpoint（连接点） 简单点来说就是被拦截的方法或者是字段，通常都是方法。
- Pointcut（切入点） Pointcut 就是对连接点的描述和定义，比如我们定义的正则式切入点，Spring AOP 通过 Pointcut 获取到我们需要拦截的方法。
- Advice（通知） Advice 对被拦截方法执行前后（包括异常）需要执行的一些操作。

## 2 AOP 不等于动态代理

​    看到 AOP 大家往往想到动态代理，因为动态代理是实现 AOP 最常见、最常用的方式之一。但是 AOP 不等于动态代理。

​    运行期的代理，通过修改源码或者是字节码的注入方式也可以实现 AOP ，AspectJ 、 Javassist 等一些框架就是通过字节码注入方式实现的 AOP 。还有在编译期间通过代码的植入方式也可以实现 AOP，如 javax.annotation.processing.Processor 编译期间运行的处理器，在编译期间植入代码实现 AOP。

## 3 原理

- 反射
- 动态代理
- 字节码技术

## 4 动态代理

- JDK动态代理

  必须实现 InvocationHandler接口，然后通过Proxy.newProxyInstance(Classloader)获取对象

- CGLIB动态代理

  - [x] SpringBoot集成SpringAOP默认使用CGLIB动态代理
  - [x] 使用 CGLIB 动态代理，被代理类**不需要强制实现接口**。CGLIB 不能对声明为 final 的方法进行代理，因为 CGLIB **原理是动态生成被代理类的子类**。