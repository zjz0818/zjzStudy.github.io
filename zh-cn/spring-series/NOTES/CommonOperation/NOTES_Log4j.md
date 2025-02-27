# Log4j
> 定义：
>
> 干啥的？作用于哪一方面？
>
> 基本配置，基本操作？
>

## LOG4J
> 定义 ，怎么使用？ 配置？
>
### 定义：
- 简介
    -  1.Log4j是Apache的一个开源项目
    -  2.通过使用Log4j，我们可以控制日志信息**输送的目的地**：控制台，文本，GUI组件....
    -  3.我们也可以**控制每一条日志的输出格式**；
    -  4.通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。最令人感兴趣的就
       是，这些可以**通过一个配置文件**来灵活地进行配置，而不需要修改应用的代码。

### 使用：
- 1.导入log4j包
    ```
        <!-- https://mvnrepository.com/artifact/log4j/log4j -->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>

    ```

- 2.CLASSPATH路径建log4j.properties
  ```
      #将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
      # 日志输出级别：ERROR、WARN、INFO、DEBUG
      #ERROR 为严重错误 主要是程序的错误
      #WARN 为一般警告，比如session丢失
      #INFO 为一般要显示的信息，比如登录登出
      #DEBUG 为程序的调试信息
      log4j.rootLogger=DEBUG,console,file
      
      #控制台输出的相关设置
      log4j.appender.console = org.apache.log4j.ConsoleAppender
      log4j.appender.console.Target = System.out
      log4j.appender.console.Threshold=DEBUG
      log4j.appender.console.layout = org.apache.log4j.PatternLayout
      log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
      
      #文件输出的相关设置
      log4j.appender.file = org.apache.log4j.RollingFileAppender
      log4j.appender.file.File=./log/zjz.log
      #文件大小-超10M就切分
      log4j.appender.file.MaxFileSize=10mb
      log4j.appender.file.Threshold=DEBUG
      log4j.appender.file.layout=org.apache.log4j.PatternLayout
      log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
      
      #日志输出级别
      log4j.logger.org.mybatis=DEBUG
      log4j.logger.java.sql=DEBUG
      log4j.logger.java.sql.Statement=DEBUG
      log4j.logger.java.sql.ResultSet=DEBUG
      log4j.logger.java.sql.PreparedStatement=DEBUG
  
  ```

- 3.配置lOG4j的日志实现mybatis-config.xml配置

   ```
     <!--log4j日志-->
        <settings>
            <setting name="logImpl" value="LOG4J"/>
        </settings>
        
    ```

## log4j在java中的使用
    - 一般
      `    static Logger logger = Logger.getLogger(UserMapperTest.class); //对应目前的类
      logger.info("info：进入getUserListLog4j方法");   // 提示信息  `

  ```
       //注意导包：org.apache.log4j.Logger
        static Logger logger = Logger.getLogger(UserMapperTest.class); //对应目前的类
        @Test
        public void getUserListLog4j() {
            logger.info("info：进入getUserListLog4j方法");   // 提示信息
            logger.debug("debug：进入getUserListLog4j方法"); // debug信息
            logger.error("error: 进入getUserListLog4j方法"); // 错误信息
            SqlSession session = MybatisUtils.getSqlSession();
    
            UserMapper mapper = session.getMapper(UserMapper.class);
            List<Object> users = mapper.getUserList();
            System.out.println(users.toString());
            session.close();
    
        }
    
  
  ```

