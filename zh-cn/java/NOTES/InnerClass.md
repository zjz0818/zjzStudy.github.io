# 内部类
- 目前只了解对应的使用!!
- 只要知道是在类的内部写的就行
- 必须懂静态内部类

- [⑨NOTES_Lamda](zh-cn/java/NOTES/NOTES_Lamda.md)   
- [⑩InnerClass](zh-cn/java/NOTES/InnerClass.md)


## 静态内部类
-  简单记忆
    - 位置,在主类里的类
    - 加static的内部类



```
public class 主类{
    // 静态内部类
    static class Like1 implements ILike{
        @Override
        public void lambda() {
            System.out.println("静态内部类::--->lambda");
        }
    }
}

```


## 局部内部类
- 简单记忆,
  - 位置:在方法中的类
    
## 匿名内部类
> 一个接口只有一个方法!!! 
- 简单记忆
    - 位置:在方法中
    - 定义:它的定义有别于所有java的操作!!!
    - 他必须依托抽象类,接口,父类---注意得有封号结尾
    - 操作:new 对象时后面直接{};  ---{};里面写重写的方法!!!
    - 直接用接口了.....直接是父类--父类
    

    ```
         // 5.匿名内部类,没有类的名称,必须借助接口,父类
        ILike like3 = new ILike(){
            @Override
            public void lambda(){
                System.out.println("匿名内部类::--->lambda");
            }
        };
    
        like3.lambda();
    
    
    ```




### lamda
- 直接将匿名内部类的方法名后面的拿过来..也就是
  ```
      (){
        System.out.println("匿名内部类::--->lambda");
        };
  
  ``` 

- 然后() 和{}中间写个->
  - 当然前面的对象等于.. ----这个对象的要求????
    - 对象的要求,必须是父类.父类(接口,抽象方法)
    - 也就是

  ```
       // 6.用lambda简化
      父类(接口,抽象方法)
      ILove love = (int a)-> {
                System.out.println("LOVE?"+a);
        };
  
  ``` 

- 常规操作
  - 要求,得是一个父类(接口,抽象方法)
    - new Thread(()-> System.out.println("XXX"))





