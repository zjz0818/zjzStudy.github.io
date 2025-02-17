# REVIEW
>
> 先分为四大板块
# REVIEW
>
> 先分为五大板块
>
> 基础-类，变量，抽象，接口，常规操作，异常 - [Review_javaBase](zh-cn/刷题/Review_java/Review_javaBase.md)
>
> 容器：- [Review_javaContainer.md](zh-cn/刷题/Review_java/Review_javaContainer.md)
>
> 网络编程 - [Review_NetWork](zh-cn/刷题/Review_java/Review_NetWork.md)
>
> 线程
>
> java同其他的交互 - [Review_javaInteraction](zh-cn/刷题/Review_java/Review_javaInteraction.md)
> 


# 交互：
## 前后的的交互

### 容器，服务器，小应用程序
- 服务器
    - Apache就是一个Http服务器，静态的html  Apache还可以处理，

- 容器
    - Tomcat是一个web容器， 动态的需要Http服务器转发给Tomcat去处理了，比如jsp页面，请求先经由Apache转发给Tomcat再由Tomcat解析请求。
    - 所以应该是web容器去解析成request对象
    - web容器是一种服务程序，在服务器一个端口就有一个提供相应服务的程序，而这个程序就是处理从客户端发出的请求，
      如JAVA中的Tomcat容器，ASP的IIS或PWS都是这样的容器。一个服务器可以多个容器

- 小应用程序
    - servlet是运行在服务器端的小应用程序，是接收网络服务的请求和产生响应的一种方式。
    - servlet的功能：接受http请求，产生动态http响应。














