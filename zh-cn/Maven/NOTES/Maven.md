## Maven 是一款服务于 Java 平台的自动化构建工具，主要有以下两个作用：

## 对jar包的管理
## 项目的一键构建
- 构建是什么？指的是编译、测试、运行、打包、安装、部署的整个过程。整个构建过程都可以用 maven 来进行管理。
- maven 的构建过程：clean --> compile --> test --> package --> install --> deploy
    - 清理：将以前编译得到的旧class字节码文件删除。
    - 编译：将Java源程序编译成class字节码文件。
    - 测试：自动测试，自动调用junit程序。
    - 报告：测试程序执行的结果。
    - 打包：打war包或jar包。
    - 安装：maven特定概念，将打包得到的文件复制到“仓库”中指定位置。
    - 部署：war包或jar包部署



## Maven 目录结构
- maven中约定的目录结构：
    ```
    Project(项目名)
    |---src(源码)
    |---|---main(主程序)
    |---|---|---java(java代码)
    |---|---|---resources(配置文件，资源文件)
    |---|---test(测试文件)
    |---|---|---java(测试java代码)
    |---|---|---resources(测试的配置文件，资源文件)
    |---pom.xml
    ```

## POM
- POM含义：Project Object Model 项目对象模型



## 依赖
- 常用的依赖范围：
     
    - compile（默认范围）
        - 对主程序是否有效：有效
        - 对测试程序是否有效：有效
        - 是否参与打包：参与
    - test
        - 对主程序是否有效：无效
        - 对测试程序是否有效：有效
        - 是否参与打包：不参与
        - 是否参与部署：不参与
        - 典型例子：junit.jar
    - provided
        - 对主程序是否有效：有效
        - 对测试程序是否有效：有效
        - 是否参与打包：不参与
        - 是否参与部署：不参与
        - 典型例子：servlet-api.jar
        - 依赖具有传递性（非compile范围不可传递）。

- 依赖的排除：
```
<exclusions>
    <exclusion>
      <groupId>xxx</groupId>
    <artifactId>xxx</artifactId>
  </exclusion>
</exclusions>
```

## 继承
- 将一个 Maven 工程作为父工程。注意：打包方式为pom。
- 子工程即可对父工程进行引用，继承父工程的依赖。
```
<!-- 子工程中声明父工程 -->
<parent>
    <groupId>xxx</groupId>
  <artifactId>xxx</artifactId>
  <version>xxx</version>
</parent>
```


- POM 模板

```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.zhe</groupId>
  <artifactId>ssm_demo</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>war</packaging>
  <dependencies>
  <!-- 引入spring的相关依赖 -->
  <!-- 1)spring核心依赖 -->
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-core</artifactId>
	    <version>4.3.7.RELEASE</version>
	</dependency>
	
	<dependency>
   	    <groupId>org.springframework</groupId>
   	    <artifactId>spring-beans</artifactId>
   	    <version>4.2.0.RELEASE</version>
 	 </dependency>

	<dependency>
  	   <groupId>org.springframework</groupId>
   	   <artifactId>spring-context</artifactId>
   	   <version>4.2.0.RELEASE</version>
  	</dependency>

	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-aop</artifactId>
	    <version>4.3.7.RELEASE</version>
	</dependency>
	
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-aspects</artifactId>
	    <version>4.3.7.RELEASE</version>
	</dependency>
	
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-web</artifactId>
	    <version>4.3.7.RELEASE</version>
	</dependency>

	<!-- 2)spring dao层依赖 -->
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-jdbc</artifactId>
	    <version>4.3.7.RELEASE</version>
	</dependency>
	
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-tx</artifactId>
	    <version>4.3.7.RELEASE</version>
	</dependency>


	<!-- 3)spring web相关依赖 -->

	
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-webmvc</artifactId>
	    <version>4.3.7.RELEASE</version>
	</dependency>
	
	<!-- 4)spring test相关依赖 -->
  	<dependency>
  	    <groupId>org.springframework</groupId>
   	    <artifactId>spring-test</artifactId>
  	    <version>4.2.0.RELEASE</version>
  	</dependency>
	
  	
  	<!-- 引入mybatis的依赖 -->
	<dependency>
	    <groupId>org.mybatis</groupId>
	    <artifactId>mybatis</artifactId>
	    <version>3.3.0</version>
	</dependency>
  	
  	<!-- 引入spring和mybatis结合的依赖 -->
	<dependency>
	    <groupId>org.mybatis</groupId>
	    <artifactId>mybatis-spring</artifactId>
	    <version>1.3.1</version>
	</dependency>
	
	<!-- 引入oracle的驱动依赖 -->
	<dependency>
		<groupId>com.oracle</groupId>
		<artifactId>ojdbc6</artifactId>
		<version>11.2.0.3.0</version>
	</dependency>



	<!-- 引入mysql的驱动依赖 -->
	<dependency>
		<groupId>mysql</groupId>
		<artifactId>mysql-connector-java</artifactId>
		<version>5.0.45</version>
		<scope>runtime</scope>
	</dependency>



	<!--引入连接池dbcp  -->
	<dependency>
	    <groupId>org.apache.commons</groupId>
	    <artifactId>commons-dbcp2</artifactId>
	    <version>2.5.0</version>
	</dependency>
	
	<dependency>
	    <groupId>org.apache.commons</groupId>
	    <artifactId>commons-pool2</artifactId>
	    <version>2.5.0</version>
	</dependency>
	
	<!-- 引入json的相关依赖 -->
	<!-- Jackson -->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.9.4</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-annotations</artifactId>
            <version>2.9.4</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>2.9.4</version>
        </dependency>
	

     <!--:3：servlet web相关依赖 -->
      <!-- 引入standard的依赖 -->
       <dependency>
          <groupId>taglibs</groupId>
          <artifactId>standard</artifactId>
          <version>1.1.2</version>
       </dependency>

     <!-- 引入jstl的依赖 -->
      <dependency>
         <groupId>jstl</groupId>
         <artifactId>jstl</artifactId>
         <version>1.2</version>
      </dependency>
     
     <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
     </dependency>
	
	
	
	<!-- 引入log4j的依赖 -->
	<dependency>
	    <groupId>log4j</groupId>
	    <artifactId>log4j</artifactId>
	    <version>1.2.17</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/com.fasterxml/classmate -->
	<dependency>
	    <groupId>com.fasterxml</groupId>
	    <artifactId>classmate</artifactId>
	    <version>1.1.0</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.hibernate.validator/hibernate-validator -->
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.1.1.Final</version>
</dependency>
	<!-- https://mvnrepository.com/artifact/org.jboss.logging/jboss-logging -->
<dependency>
    <groupId>org.jboss.logging</groupId>
    <artifactId>jboss-logging</artifactId>
    <version>3.1.4.GA</version>
</dependency>
<!-- https://mvnrepository.com/artifact/javax.validation/validation-api -->
<dependency>
    <groupId>javax.validation</groupId>
    <artifactId>validation-api</artifactId>
    <version>1.1.0.Final</version>
</dependency>
<!-- 引入servlet的依赖 -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.0.1</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>jsp-api</artifactId>
    <version>2.2</version>
    <scope>provided</scope>
</dependency>
	
  </dependencies>
</project>


```

