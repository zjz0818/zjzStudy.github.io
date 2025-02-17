# Proxy
> 使用代理模式，代理和真实对象之间的的关系通常在编译时就已经确定了，代理不支持多层嵌套。
> 

- 代理模式中类的关系不需要客户端去配置，客户只需要使用代理类就ok了。但是装饰者模式中，类之间的关系需要客户指定。需要看自己是开发者还是客户
- 代理不支持多层嵌套
- 使用的场景不一样。比如IO流使用的装饰者模式，可以层层增加功能。

- 代理和装饰其实从另一种角度更容易去理解这两个模式的区别：
  - 代理更多的是强调控制对对象的访问，
    比如说：访问A对象的查询功能时，访问B对象的更新功能时，访问C对象的删除功能时都需要判断用户是否登录，
    那么我需要将判断用户是否登录功能抽出来，并对A对象，B对象，C对象进行代理使访问它们时都需要去判断用户是否登录，
  - **简单说就是将某个控制访问权限应用到多个对象上**；AOP..
  - 而装饰更多的强调现在我要给A对象增加唱歌功能，跳舞功能，说唱功能等等，
  - **简单说就是讲多个功能附加在一个对象上**





## 先脑思一个
- 代理的关键就是对目标的**再封装**
- 所以要不是静态代理(有一个共同的父类)
- 要不就是动态代理,通过Proxy的反射class

- 代理中的思路---本质:包裹目标
    - 1.首先获取目标
    - 2.设置一个set方法,将目标可以set进来 
    - 3.区别来了!!!!
        - 静态:get对象的方法,将对象的方法一个个get到..
            - this.target.Method1(); this.target.Method2(); ...
        - 动态:相对于静态来说,操作有点多:
            - 1.使用Proxy的方法获取对象
             - `Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), this);`
            - 2.重写invoke 实现对象本身的方法
              - Object result = method.invoke(target, args);
    - 4.写自己要加入的方法
        - 写一个同目标类型一样的方法.放进去




- 动态代理:::
    
    ```
     /*
              * 目的：生成一个代理对象，并执行被代理人方法
              * 交互--被代理人方法，以及生成代理对象，提供一个调用代理人对象的方法
              * 1.被代理人的方法的获取，必须要获取到被代理人的对象
              * 2.生成代理对象，必须要依托于代理人的方法（接口）以及它的加载器（要不jvm处理不了）
              *
              * */
        
              
              import java.lang.reflect.InvocationHandler;
              import java.lang.reflect.Method;
              import java.lang.reflect.Proxy;
              
              public class ProxyInvocationHandler implements InvocationHandler {
              
                  private Object target; // 被代理的人-对象
              
                  public void setTarget(Object target) {
                      this.target = target;
                  }
              
              
                  // 调用代理人对象的方法，以及生成代理对象
                  public Object getProxy(){
              
                      Object proxyInstance = Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), this);
                      return proxyInstance;
                  }
              
                  // 被代理人方法
                  @Override
                  public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                  System.out.println("执行"+method.getName()+"方法---");
                      Object result = method.invoke(target, args); // 此时执行被代理人的方法
              
                      return result;
                  }
              }
        
    
    
    
    
    
    
    ```





