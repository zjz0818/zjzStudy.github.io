- 本阶段代码可直接从gitee上拉取https://gitee.com/zhangjzm/spring-boot1.git
## 1.通过session的方式

- controller配置
- src/main/java/com/example/springboot/controller/LoginController.java
    ```
    @Controller
    public class LoginController {
    
        @RequestMapping("/user/login")
    
    //    @ResponseBody  有这个是跳转到文字，没得话就是跳转到视图
        //Model 回显数据
        public String login(
                @RequestParam("username") String username,
                @RequestParam("password") String password,
                Model model, HttpSession session){
    
            //具体业务
            if(!StringUtils.isEmpty(username) && "123456".equals(password)){
                session.setAttribute("loginUser",username); //登录成功传session
                return "redirect:/main.html";
                //防止地址栏出现密码
            }else {
                //告诉用户，你登录失败了
                model.addAttribute("msg","用户名或密码错误!");
                return "index";
            }
    
        }
    
    }
    ```


- 自制拦截器：
- src/main/java/com/example/springboot/config/LoginHandlerInterceptor.java
    ```
    //自制的拦截器
    public class LoginHandlerInterceptor implements HandlerInterceptor {
    
        //放行不放行
        @Override
        public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    
            //登录成功后，应该有用户的session
            Object loginUser = request.getSession().getAttribute("loginUser");
            if(loginUser==null){
                request.setAttribute("msg","没有权限，请先登录");
                request.getRequestDispatcher("/index.html").forward(request,response);
                return false;
            }else{
                return true;
            }
            
        }
    
    }
    
    ```

- 配置容器中的拦截器
- src/main/java/com/example/springboot/config/MyMvcConfig.java
    ```
      @Override
        public void addInterceptors(InterceptorRegistry registry) {
            registry.addInterceptor(new LoginHandlerInterceptor())
                    .addPathPatterns("/**")
                    .excludePathPatterns("/index.html","/","/user/login","/css/*","/img/*","/js/*");
            //拦截请求addPathPatterns  不拦截一些excludePathPatterns
        }
    ```


- 页面输出session记录的名字
    ```
    <a class="navbar-brand col-sm-3 col-md-2 mr-0" 
    href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">[[${session.loginUser}]]</a>
    ```