# Annotation

## 注解太多了
> 1.统计注解
> 
> 2.使用前的配置
> 
> 3.限制，规范
> 
> 4.应用场景！
> 


# java
- java中直接就能用的
    - @SuppressWarnings --镇压警告  -:TYPE FIELD METHOD…… Retention SOURCE
    - @Resource    自动装配通过名字，类型 - Target({TYPE, FIELD, METHOD})--  Retention(RUNTIME)
    
- 导junit 的
  - @Test  测试类 Target(METHOD)   Retention(RUNTIME) 
    







# Spring
## 在  `<!--注解驱动--> <context:annotation-config/>`
- @Autowired   自动注入（主类引入子类）    -Target:({FIELD METHOD……})---Retention(RetentionPolicy.RUNTIME)
- @Nullable  可以为null                 -Target:({FIELD METHOD……})--- Retention(RetentionPolicy.RUNTIME)
- @Qualifier(value = "XXX") 专门用于对应ID     -Target({TYPE, FIELD, METHOD})---Retention(RetentionPolicy.RUNTIME)
 - springboot中用于注入(Autowired下)  对用config配置的bean的名称
## 在注解驱动,扫描之下的

```
    <!-- 指定要扫描的包，这个包下的注解就会生效-->
    <context:component-scan base-package="com.zjz.pojo"/>

    <!--注解驱动-->
    <context:annotation-config/>
```

- @Component 组件 放在类上，说明这个类被Spring管理了
  -  @Component 有几个衍生注解，比如在web开发中，会按照mvc三层架构分层---都是组件的意思
  - dao【@Repository】
  - service[@Service]
  - controller【@Controller】
- 四个功能都一样，都是代表将某个类注册到Spring中，装配Bean  
- @Value("zjz") --- 在set上直接用，直接赋值
- @Scope("singleton")  作用域
- @Configuration //代表这是一个配置类 

- @Aspect 切面类注解
  - @Before  之前
  - @After  之后 



# SpringMVC
- @Controller 使用它，再也不用专门配controller的javabean
- @RequestMapping("/hello") 跳转的地方action  TYPE，METHOD    RUNTIME
   - 使用后就可以点击底下的return 值; 就可以跳得jsp页面
   - 注意，如果类上加了@RequestMapping("/Type")  然后方法上加@RequestMapping("/method") 那么方法的路径就是/type/method

- @RequestMapping({"/","/index"}) 点进去可以看下,它可以是一个数组
- @PathVariable  RestFul风格--使用它 搭配    @RequestMapping("/add/{a}/{b}") 实现在地址栏输值

- 与网页交互：：：：：请求体 @GetMapping    @PostMapping  @RequestMapping  获取网页数据！！！

- 参数 @RequestParam("XXX")  ---最好加上，防止出错，，，，多个必须加！！！
  

- 都是直接返回字符串
  - 响应体@ResponseBody  // 只要加了ResponseBody 就不会走视图解析器，会直接返回一个字符串
  - @RestController---标注的类，只会返回字符串 而@Controller 会走视图解析器
 


# SpringBoot
## 配置系列
## @EnableXXX开启某个功能
- 1.@SpringBootApplication 来标注一个主程序类(主配置类)，说明这是一个SpringBoot应用
  
- 2.@ComponentScan
- 这个注解在Spring中很重要 ,它对应XML配置中的元素。
  - 作用：自动扫描并加载符合条件的组件或者bean ， 将这个bean定义加载到IOC容器中
  
- 3.@SpringBootConfiguration
  - 作用：SpringBoot的配置类 ，标注在某个类上 ， 表示这是一个SpringBoot的配置类；

- 4.@Configuration，说明这是一个配置类 ，配置类就是对应Spring(bean)的xml 配置文件；------重要!!
  - 里面方法加@Bean 也就是一个Bean了
  - 绑定@ConfigurationProperties(prefix = "spring.datasource")
  
- 5.@Component 这就说明，启动类本身也是Spring中的一个组件而已，负责启动应用！
- 6.@EnableAutoConfiguration：开启自动配置功能
- 7.@AutoConfigurationPackage ： 自动配置包
- 8.@ConfigurationProperties(prefix = "person")---手动参数推荐!!!---配置文件控制项目的关键--必须背会
- 9.开启大V校验 JSR-303
  - 1.主类上写@Validated  // 数据校验
  - 2.属性上写@Email(message="邮箱格式错误")
  - 3.@Pattern 正则表达式
  
- 10.AutoConfiguration类上面注解@EnableConfigurationProperties(ServerProperties.class)
  - 插一句:决定这个类生效不生效是依据@ConditionalOnXXXX---注解,它用来看你依赖是否够了
  
- 11.@RequestParam("XXX")  controller用来接收View返回的值,很少用..

- 12.ConditionalOnMissingBean() //当不存在时这个方法生效
- 13@ConfigurationProperties(prefix="XXX"")  一般在properties中必有,作用就是前缀

- 14.@Qualifier(value = "XXX") 专门用于对应ID     -Target({TYPE, FIELD, METHOD})---Retention(RetentionPolicy.RUNTIME)
- springboot中用于注入(Autowired下)  对用config配置的bean的名称

## SpringBoot+Mybatis
- 1.@Mapper 用于Mapper接口--表示是mybatis的mapper类
- 或者在主运行类下加@MappperScan("...mapper") 扫描mapper



## SpringSecurity
- @EnableXXX开启某个功能
- @EnableWebSecurity：开启WebSecurity模式



## Swagger
- @ApiModel("用户实体类") ---给pojo类上加,用于swagger中查看
- @ApiModelProperty("用户名")---给pojo属性上加,用于swagger中查看
 

1
## Lombok
- @Data  -- get&&set
- @AllArgsConstructor ----所有参有参构造
- @NoArgsConstructor---无参构造
- @Accessors(chain = true) -- 链式写法---使用set后无限套娃,,true为开启,默认false
--- 值得一提的是,如果你涉及自增,自定义(DIY),那么你得重载一个构造器



# SpringCloud

## Hystrix
- @HystrixCommand 服务熔断,对可能崩的方法上加
- @EnableCircuitBreaker  对熔断的支持,主run上加


## Mybatis-plus
-  @TableId(type = IdType.AUTO) // 主键自增,需配合数据库自增使用--都不设置就是**雪花算法**
- 



## 操作系列








