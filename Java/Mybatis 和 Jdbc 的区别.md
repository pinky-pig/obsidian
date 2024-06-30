
# jdbc

首先，jdbc 是一种规范，就是 java database connection ，一个术语。
然后再说我们使用的 jdbc 操作数据库，因为在pom.xml引入了一个 jdbc 的包，所以其实这里的 jdbc 就是这个依赖包。

这里的 jdbc 操作数据库，很灵活，想怎么在代码里写sql就怎么写，想怎么用就怎么用。

```java
List<Map<String, Object>> getDogList(){  
    String sql = "select * from dog";  
    List<Map<String, Object>> result = jdbcTemplate.queryForList(sql);  
    return result;  
}
```

用完将结果返回给了result，这个结果的类型是自己随便定义的 List<Map<String, Object>> 。所以很灵活。

# Mybatis

再说 mybatis ，jdbc 使用起来很灵活，但是如果项目比较大，业务比较复杂，那可能代码就比较乱了。这个时候就需要一个八股文式的写法，约定你怎么怎么写，就要安装这样写。

这个就是 mybatis ，就像如何把大象装进冰箱里，需要三步，先打开冰箱门，再把大象放进冰箱，再关闭冰箱门。

操作数据库，也是先连接数据库，再sql操作数据库，拿到结果后关闭数据库。mybatis 呢，连接数据库后，自己需要做的，先定义好所有需要的 sql，再写好操作数据库的 java 方法名，再一一将定义好的 sql 和 java 映射起来。这样代码中就不需要再写sql 了，只需要写在预先定义好的 sql 文件中。

也就是 sql 都写在一个地方， java 方法写在一个地方，代码中需要调用操作数据库的时候，只要调用 java 方法，然后就能调用 sql ，然后就能操作数据库了，这样就分好层了。

java 的方法名，就是配置 sql 的地方中的 id ，通过 id 联系起来。然后sql既然操作数据库了，那操作的结果必然有类型的，查询要有结果，这个结果的类型是什么，删除也要有类型。而这里的结果的类型，是通过 resultType 定义，给其传个已经定义好的比如 User 类也行，或者 List<Map<String, Object>> 也行。

# 总之

反正 jdbctemplate 就是简单，快速写 SQL ，然后再给其定义一下结果的类型就好了。
Mybatis 是先安装规定的地方定义好 sql ，然后结果的返回类型，和 java 方法名。使用的时候直接调用 java 类。
