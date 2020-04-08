# Mybatis安全性问题

- SQL注入
- 线程安全问题

## 1 SQL注入

- 通过#{}防止SQL注入，${}不能防止sql注入
- \#{}：相当于JDBC中的PreparedStatement ${}：是输出变量的值
- 简单说，**#**{}是经过**预编译的**，是**安全的**；**$**{}是未经过预编译的，仅仅是取变量的值，是非安全的，存在SQL注入。

MyBatis是如何做到**SQL****预编译**的呢？其实在框架底层，是JDBC中的**PreparedStatement**类在起作用，PreparedStatement是我们很熟悉的Statement的子类，它的对象包含了**编译好的****SQL****语句**。这种**“准备好”的方式**不仅能提高**安全性**，而且在多次执行**同一个****SQL**时，能够提高**效率**。**原因**是SQL已编译好，再次执行时无需再编译。

## 2 线程安全

- **SqlSessionManager** 线程安全

- **SqlSessionTemplate** 线程安全

  通过维护单例的DefaultSqlSession保证线程安全

  Mybatis一级缓存失效

- **DefaultSqlSession** 线程不安全