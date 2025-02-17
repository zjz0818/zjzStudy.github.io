# maven怎么用
- 
- 
- 
## maven命令

- 2

## pom文件
- 1.打包方式:packaging
- 2.定义版本号的properties
    ```
        <properties>
            <maven.compiler.source>8</maven.compiler.source>   // maven的
            <maven.compiler.target>8</maven.compiler.target>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  //项目的
            <junit.version>4.12</junit.version> // 自己导入依赖的
            <lombok.verion>1.16.10</lombok.verion>
            <log4j.version>1.2.17</log4j.version>
        </properties> 
  
    ```
  
- 3.依赖管理dependencyManagement-->dependencies-->dependency
    - 如果使用依赖管理dependencyManagement就不会自动导包了,意味着他是一个父级的,提供者
    
### SpringCloud中的操作
- 这个子pom拿到另一个子pom的东西
  - dependency拿
    - ```
        <!--我们需要拿到实体类,所以配置API Module-->
        <dependency>
            <groupId>org.example</groupId>
            <artifactId>springcloud-api</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
      
      ```