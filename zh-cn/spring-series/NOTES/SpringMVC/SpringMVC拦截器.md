# 拦截器
> 拦截器是Spring-AOP思想的具体应用。
> 
> 作用: 
- SpringMVC的处理器拦截器类似于Servlet开发中的过滤器Filter,用于对处理器进行预处理和后处理。开发者可以自己定义一些拦截器来实现特定的功能。
> 

- 过滤器
    - servlet规范中的一部分，任何java web工程都可以使用
    - 在url-pattern中配置了/*之后，可以对所有要访问的资源进行拦截
- 拦截器
    - 拦截器是SpringMVC框架自己的，只有使用了SpringMVC框架的工程才能使用
    - 拦截器只会拦截访问的控制器方法， 如果访问的是jsp/html/css/image/js是不会进行拦截的


# 自定义拦截器
- 编写一个类,实现HandlerInterceptor
  
  ```
  
  
      public class MyInterceptor implements HandlerInterceptor {
      
      
      
          // return true;执行下一个拦截器,放行
          // return false;不执行下一个拦截器,放行
          @Override
          public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
      
              System.out.println("------------------处理前--------------------");
      
              return true;
          }
      
          @Override
          public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
              System.out.println("------------------处理后--------------------");
      
      
          }
      
          @Override
          public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
              System.out.println("------------------清理--------------------");
          }
      }
  
  
  
  ```




- 加入配置MVC

  ```
        <mvc:interceptors>
            <mvc:interceptor>
    <!--/** 包括这个请求下面的所有请求   一个*当前目录下的,两个**,代表所有-->
                <mvc:mapping path="/**"/>
                <bean class="com.zjz.config.MyInterceptor"/>
            </mvc:interceptor>
        </mvc:interceptors>
    
  
  
  ```















