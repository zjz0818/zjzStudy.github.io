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
> 线程  - [Review_Thread.md](zh-cn/刷题/Review_java/Review_Thread.md)
>
> java同其他的交互 - [Review_javaInteraction](zh-cn/刷题/Review_java/Review_javaInteraction.md)
>


- 多线程一共有三种实现方式
    - 方式1：继承Thread类，并重写run()方法
    - 方式2：实现Runnable接口，实现run()方法
    - 方式3：实现Callable接口，线程结束后可以有返回值，但是该方式是依赖于线程池的。