# Mybatis如何分页

- 逻辑分页

- 物理分页

## 逻辑分页

​    Mybatis 使用 RowBounds 对象进行分页，它是针对 ResultSet 结果集执行的内存分页，而非物理分页。可以在 sql 内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。

   分页插件的基本原理是使用 Mybatis 提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的 sql，然后重写 sql，根 据 dialect 方言，添加对应的物理分页语句和物理分页参数。

## 物理分页

- PageHelper

  ThreadLocal+重载Mybatis拦截器

  https://github.com/pagehelper/Mybatis-PageHelper

