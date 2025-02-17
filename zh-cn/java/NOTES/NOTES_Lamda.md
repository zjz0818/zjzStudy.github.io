# Lamda表达式
> 它是一个简化匿名内部类 
> 
> 简化了谁?
> 
> 函数式接口?
> 
> 怎么写这个表达式
>
  
- [⑨NOTES_Lamda](zh-cn/java/NOTES/NOTES_Lamda.md)
- [⑩InnerClass](zh-cn/java/NOTES/InnerClass.md)


## 介绍
- 希腊字母表中排序第十一位的字母，英语名称为Lambda 
- 避免匿名内部类定义过多
- 其实质属于函数式编程的概念

- new Thread(()->System.out.println(“多线程学习。。。。”)).start();

- 为什么要使用lambda表达式 
  - 避免匿名内部类定义过多 
  - 可以让你的代码看起来很简洁 
  - 去掉了一堆没有意义的代码，只留下核心的逻辑。
    
## 理解函数接口
- 理解函数式接口(Functional Interface) 是学习java8 Lambda表达式的关键所在
- 函数式接口的定义
    - 任何接口,如果**只包含唯一一个抽象方法**,那么他就是一个函数式接口
    - 对于函数式接口,我们可以通过Lambda表达式来创建该接口的对象



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



## 总结
  - 最好就是
  - 接口定义----Int i = null;
  - 使用: i = (参数1,参数2)->{方法1;方法2;};
- 必须是函数式接口---


