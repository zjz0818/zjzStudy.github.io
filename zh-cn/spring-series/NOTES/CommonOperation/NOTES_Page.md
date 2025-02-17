# 分页
>思考：为什么需要分页？
- 在学习mybatis等持久层框架的时候，会经常对数据进行增删改查操作，使用最多的是对数据库进行查
  询操作，如果查询大量数据的时候，我们往往使用分页进行查询，也就是每次处理小部分数据，这样对
  数据库压力就在可控范围内。
> 第一个学习分页时候的逻辑---他是基于数据库Limit 以及 ROWNUM  进行限制，每次点击下一页时，就会将它们两个值进行相应的修改。。
> 
> 
> 

  
## 使用SQL语句的方式
- UserMapper
  ```
      // 分页查询
      List<User> getUserLimit(Map<String,Object> map);
  ```

- UserMapper.xml

  ```
      <select id="getUserLimit" parameterType="map" resultType="user" >
          select * from user limit #{startIndex},#{pageSize}
      </select> 
  ```
  
- Test
  ```
        @Test
        public void testGetUserLimit(){
    
            logger.info("info：进入testGetUserLimit方法");
            SqlSession sqlSession = MybatisUtils.getSqlSession();
            UserMapper mapper = sqlSession.getMapper(UserMapper.class);
            Map<String, Object> map = new HashMap<>();
    
            map.put("startIndex",0);
            map.put("pageSize",1);
            
            List<User> userLimit = mapper.getUserLimit(map);
            System.out.println(userLimit.toString());
            sqlSession.close();
    
        }
  
  ```

  
## 利用java对象RowBounds
- 1.new RowBounds();
- 2.SqlSession 调用
- List<User> users = session.selectList("com.kuang.mapper.UserMapper.getUserByRowBounds", null, rowBounds);




## 分页插件
- PageHelper
- https://pagehelper.github.io/docs/howtouse/











