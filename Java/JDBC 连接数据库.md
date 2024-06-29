
1. application.yaml 配置 datasource
2. 然后 `jdbcTemplate` 写 sql 查表。

当然，可以这样认为，springboot 自带的 datasource ，然后可以通过getConnection() 获取一个对数据库操作的连接，处理完之后再 close 就好了。

jdbc 是 java database connection ，是一种规范。

*下面的 jdbc 是依赖包 jdbc 。*

但是自带的不够智能，所以我们引入了依赖，jdbc ，那么就可以直接通过 jdbc 写 sql 对数据库操作了。不需要先初始化一个 datasource 再 close，而是 jdbc 都自带了。

```java
  
@Autowired  
private JdbcTemplate jdbcTemplate;  
  
List<Map<String, Object>> getDogList(){  
    String sql = "select * from dog";  
    List<Map<String, Object>> result = jdbcTemplate.queryForList(sql);  
    return result;  
}
```

