# SSM架构搭建
## 个人见解
> POJO  --- 提供一个实体（ORM），对对象的基本操作啊，set，get值
 
> Dao  --- 提供数据-怎么提供？--依照你输入的参数获取想要的返回（返回对象需new对象）
  
> Service --- 数据处理--怎么处理？--数据来源：引入dao，以及方法的参数---dao的处理：拿到dao的数据封装一下（这么做的意义？Controller直接拿dao不好吗？）
> - 作用：---实现本层数据共享（不同controller都可以调用Service）---1.获取**两类型**数据---2.对数据进行**处理**，如：判别，对数据进行计算
> - 怎么获取的？ 通过**入参**啊，然后**调用dao的**获取的数据。。。
> - 怎么处理的？ 两个数据都有了，1.比对？（用户登录）2.。。。
- 解析：1.从引入dao来说，如果你直接由controller来进行，那么DAO发生替换（比如从oracle迁移mysql），需要找到所有controller里的调用点，逐一修改。
- 2.如果每个判别，操作都由controller来进行，那么同层的controller并不能互通（处理数据），比如：折扣计算，反作弊判定
> Controller
>

















## 对于Mybatis操作
> 如果有自增,以及引入别的类,以及日期
- pojo类,如果自增,日期,二者出其一,我们就得重写编写构造器,如果有其它类,只定义属性写上就行了
    - 如果自增,构造器中除了自增,剩下都得有
    - 如果日期,构造器在this.日期时进行处理

- mapper接口无变动
- mapper.xml
    - 按照构造器写就行,如果是计算的年龄也不用写,自增的不用写,日期正常写


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




