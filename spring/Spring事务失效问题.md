# Spring 事务失效问题

- MySQL 使用的是 MyISAM 引擎，而 MyISAM 是不支持事务的。需要支持使用可以使用 InnoDB 引擎

- 如果使用了 Spring MVC ，`context:component-scan` 重复扫描问题可能会引起事务失败。

- @Transactional 注解开启配置放到 DispatcherServlet 的配置里了。

- @Transactional 注解只能应用到 public 可见度的方法上。 在其他可见类型上声明，事务会失效。

- 在接口上使用 @Transactional 注解，只能当你设置了基于接口的代理时它才生效。所以如果强制使用了 CGLIB，那么事务就会失效

- @Transactional 同一个类中无事务方法 a() 内部调用有事务方法 b()，那么此时事务不生效。

  这是由于 Spring 的事务实现是通过 AOP 来实现的。此时，当这个有注解的方法 b() 被调用的时候，实际上是由代理类来调用的，代理类在调用之前就会启动 transaction。然而，如果这个有注解的方法是被同一个类中的其他方法 a() 调用的，那么该方法的调用并没有通过代理类，而是直接通过原来的那个 bean，所以就不会启动 transaction