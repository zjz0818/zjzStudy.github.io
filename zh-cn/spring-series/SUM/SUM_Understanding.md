# SSM中-zjz的见解
## 一些记录心里活动的见解
- 多看，多看
- 在20210911时，观看了以下好久之前写的登录模块
    - 看了下郑的和我的，对比了一下，发现区别不小，
    - 1.他采用快速开发，我采用多场景复用
        - 1）.DAO 我采用的是依据单值获取对象，他采用双值锁定对象使用`@Param`
          - 我的高度分离（只需一个值获取对象），可以用来做其它的事（除了登入，比如查询）
          - 他的只是适用于目前场景，其它再次使用还得输两个值--快速有效获取对象
        - 2）.Service 我编写逻辑  它直接依据数据获取一个对象（没任何处理）
        - 3）.Controller 我直接依据Service返回的Boolean， 它直接判断对象是否存在
    - 2.总：
      - 他的适用于快速开发，甚至不需要service层 
      - 我的复用性较好，适用于多个功能之间得使用--成功实现service该有的作用
    
## 一切的增删改都得处理事务，怎么处理？







## 对于Mybatis操作
> 如果有自增,以及引入别的类,以及日期
- pojo类,如果自增,日期,二者出其一,我们就得重写编写构造器,如果有其它类,只定义属性写上就行了
    - 如果自增,构造器中除了自增,剩下都得有
    - 如果日期,构造器在this.日期时进行处理

- mapper接口无变动
- mapper.xml
    - 按照构造器写就行,自增的不用写,如果是计算的年龄也不用写,日期正常写
    

- 对于多对一,这个一有可能有两个属性
- pojo就写属性就行,
- mapper接口无变化
- mapper.xml
    - 1.查询返回resultMap  -- sql语句写上:
        - 1.所有的select 都得写别名,如:Student s,Teacher t,,,那么你将所有的s.-->sid,sname 所有的t.-->tid,tname(根据要的来)
        - 2.where 连接上表,如果要ById那么and下就行
    - 2.结果集id 对应resultMap type为主pojo---那么子pojo?--在association或者 collection中
        - 1.其实也好记,就是一个property(pojo里的set)对应一个column(上面的别名)
        - 2.遇到association -- 多对一
            - property为主pojo引入的名字,javaType也是主pojo引入的名字
            - 里面对应好子查询的pojo和别名就行
        - 3.遇到collection---一对多
            - property为主pojo引入的名字,ofType是子pojo名字,要对应主pojo的泛型
            - 里面对应好子查询的pojo和别名就行


- zjz说:如果是联表查询
    - 关于查询,别名,连接
    - 关于结果集,前面的property对应好主pojo的属性,后面的column就是上面写的别名
    - 遇到association或者 collection中,里面对应好子查询的pojo属性(property)和别名
    - 前端的时间处理`${#dates.format(emp.getBirth(),'yyyy-MM-dd HH:mm:ss')}`



