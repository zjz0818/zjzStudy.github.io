# SSM
- Thinking is more important than learning
- Interaction is the principle
> SSM= Mybatis+Spring+SpringMVC
> 
> 1.为什么整合？2.三者之间的关系 3.整合涉及 4.整合完有的功能，它们负责的功能 5.整合完怎么用？
>

## 为什么整合
- Mybatis--一个专用于数据持久化的操作， 实现与数据库的交互，提供数据，根据需求提供操作数据的方法
- Spring --IOC，AOP--IOC解决的是所有对象的处理流程，AOP解决的是事务，log，以及一些其它的代理式的功能
- SpringMVC -- 管控全局，一个核心的遥控器。本质是一个servlet，它是连通web层的关键，也是项目动起来的原因。
    - 它的启动，初始，毁灭，都依托于web服务器
    - 它的操作，依托于Spring（对象管理） 间接依赖于Mybatis（数据的交互）
    
- 三个为一体，层层连接起来，实现从用户界面直达数据库的操作。


## 三者之间的关系
- Mybatis 实现与数据库的交互，对象操作交由Spring，它的方法交由Service层，经Service处理后，返回于Controller
- Spring -作为**全局**的服务者
- SpringMVC - 用户的请求，响应用户。--请求进来，经过Mapping，Adapter，找到了对应的Controller
    - 对应的Controller拿上经过Service层整处来的数据，再依据规范，把视图名给整上，形成ModelAndView的一个返回体
    - 经由Adapter给了DispatchServlet，然后它通过视图解析器获取到图，还得管一下Web的东西。。。JSP毕竟要提供视图
  
- 注意：关于Web，web操作的DispatchServlet，操作的视图，但是是DispatchServlet选择的视图，提供给web
  - 所以我们之前直接网址使用.jsp是通过web服务器访问，当然一些ahref都是由web管的，
  - 但是对于功能的实现，是由web服务器给DispatchServlet的遥控板，然后它进一步处理，返回对应的图
  - 所以我们可以配置，放在WEB-INF,让用户无法直接跳过去
  

- 两个外部交流--服务器-数据库，需知道怎么连上的

## 它们负责的功能
- Mybatis  数据库的交流--数据的交流
- Spring -全局的服务者
- SpringMVC - 前端的交流 --拿操作，给对应操作，关键是操作，动作


## 整合涉及：
- 1.数据库  数据库连接过程的操作，（如数据池，JDBC的一些操作）Mybatis只是连上就行，，
- 2.Web容器，启动的关键---或者不启动，使用其它方式ping通架构
- 3.操作的框架SSM



- dao 提供数据就好,一直被service用---注意的是:每一个mapper.xml都需要在mybatis核心配置文件中注册
  - `<mapper class="com.zjz.dao.XXXMapper"/>`
- service 接口几乎和mapper一样,
  - 但是实现类,要引入对应的mapper接口对象(不需要new,只需要定义,还需要
    对它有个set,因为在dao的时候,没有dao的实现类,无法对dao进行装配,到时没有dao层的bean)
  - 值得注意的是,我们需要把它放入bean容器中,否则Controller无法使用   
  ```  
      <!--BookServiceImpl注入到IOC容器中-->
      <bean id="BookServiceImpl" class="com.zjz.service.BookServiceImpl">
        <property name="bookMapper" ref="bookMapper"/>
      </bean>
  ```

- controller 提供与界面的交互
  - 值得注意的是,它得引入service层的serviceimpl
  -  ` @Autowired
      @Qualifier("BookServiceImpl")
      private BookService bookService;`
     
  ```
      <!-- 自动扫描包，让指定包下的注解生效,由IOC容器统一管理 -->
      <context:component-scan base-package="com.zjz.controller"/>
  
  ```













# 功能:
## 增加
- 1.mapper接口 int addXXX(XXX xxx); -- mapper.xml insert..
- 2.service 接口:一般都与mapper一样,因为要直接取值
  - 接口,,值得注意的时候,此时要引入mapper接口.
  


- 输出...
-  response.getWriter().print("false");













