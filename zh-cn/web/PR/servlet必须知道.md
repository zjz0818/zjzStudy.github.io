# servlet 启动顺序
> 当一个web容器产生一个servlet实例时，它的基本顺序如下：
> 
- 1、web容器首先调用这个servlet的init()方法，它建会初始化一个资源给servlet使用。
     列如一个logger。这个init()方法在**整个servlet的生存周期只会被调用一次**。
    - 所以dispatcherServlet初始化会初始一大堆beanFactory里的东西
    
- 2、init()方法初始化了一个对象，对象继承了java.servlet.ServletConfig接口。
  这个对象使servlet能够初始化那些被声明在部署描述符的参数。
  ServletConfig也使servlet有权使用一个 javax.servlet.**ServletContext 的对象**，
  用这个对象servlet可以记录信息，分派请求到其他的web组件上并且**能够使用在同一个应用上**的**其他web资源**。
  
- 3、web容器调用这个servlet的service()方法去响应servlet的一些请求。
  根据HttpServlets,service()自动的调用合适的HTTP方法去处理请求通过调用servlet的doGet()或者doPost()方法。
  举个例子，用户发送了个Post请求，这时servlet通过doPost()方法的执行来响应这个请求。
  
- 4、当调用两个主要的HttpServlet的doPost(),doGet()方法，
  这个servlet容器将产生javax..servlet.http.HttpServletRequest和HttpServletResponse 的对象
  并且**把它们作为参数传到这些处理请求的方法**中。
  
- 5、管理一个servlet的生命周期，或者决定这个servlet实例对request请求的处理，在java虚拟机上的存在时间。
  当一个web容器开始移除一个servlet的时候将调用servlet的destroy（）方法，
  在这个方法中能够释放所有的资源，比如一个数据库连接。
