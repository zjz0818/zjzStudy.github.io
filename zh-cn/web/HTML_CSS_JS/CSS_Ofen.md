# CSS 常使用
- 1.界面去哪里找？？？不要自己每次都新加一个吧？？ 
  - 去模板之家下一个！http://www.cssmoban.com/
  - https://element.faas.ele.me/#/zh-CN
- 2.引入 ` <link rel="stylesheet" href="css/style.css" type="text/css">  `
  - 或者 head <style></style>
- 3.写逻辑的时候，由外到内，由上到下 --- 修改时记得--
- 4.边框：`border: 1px solid red;`  /*宽度，风格（样式），颜色*/
- 5.body默认有margin值，style中 body{} 可修改
- 6.可以多个操作（包括id，class），`h1,ul,li,a,body{ }`
     ```
        h1,ul,li,a,body{ 
            margin: 0;      /*外边距*/  
            padding: 0;   /*内边距*/  
            text-decoration: none;   /* 下划线   */  
            list-style: none;/*原点和序号消失*/
            font-size: 12px;/*字体大小，一般为12*/
            line-height: 25px;/*行高25*/
        }
     ```
      
-  7.实现图像变圆，变扇形，等等  
  - border-radius: 30px 50px 0px 0px; /* 左上，右上，右下，左下*/
- 8.简单记忆 . --class  # --id 
- 9.div要常用
  - form常用
  ```
  <div id="app">
    <h2>登&nbsp;&nbsp;录</h2>
    <form action="" method="get">
      <div>
          <span>名字:</span>
          <input type="">
      </div>
  
        <div>
          <span>密码:</span>
          <input type="">
      </div>
  
        <div>
          <span>邮箱:</span>
          <input type="">
      </div>
    </form>
  
  </div>
  
  ```

- 10.选择提示（主要）
```
  /*选择提示*/
  a:hover{
    background: brown;
    color: #e58f4a;
    font-size: 50px;
  }
```


## 11.没有id，class，怎么找元素？？？
- 使用结构伪列选择器（重点）
- nth-child(n) ---n指的是总共的第n个
  - ①父元素 子元素:nth-child(n){//表示父元素下的第n个元素(**不分类型**的排序)。}
    - 核实第n个是不是子元素类型，不是就不显示  一个个挨着排号
    - 比如div p:nth-child(2)表示div下的第二个p元素、如果不是p元素则没有匹配的元素(就没表现)
  - ②父元素 空格 :nth-child(n){//表示父元素下的第n个元素(**不分类型**的排序,就是第n个)。}
    - 只要第n个元素存在就会表现
  - ③XX元素:nth-child(n){//表示每一层（包括body）的第n个XX元素}
    - 每一层总排序后的第n个如果是XX元素，则显示
- nth-of-type(n)---n指的是类型的第n个---所以可能很多个
  - nth-of-type(n) ---**肯定分类型**的指定
  - ①父元素 子元素:nth-of-type(n) {//表示父元素下的子类型的第ｎ个元素，没的话不显示(**分类型**的指定)}
    - 比如div p:nth-of-type(2)表示div下ｐ类型的第二个元素 --依据类型进行排号选择
  - ②父元素  空格 :nth-of-type(n) --表示父元素下的每个类型的第n个元素，
    - div :nth-of-type(n) **分类型**
    - 每个类型的第n个都被选中
  - ③XX元素:nth-of-type(n) --表示XX元素下XX类型的第n个元素---**分类型**
- child和type 的最大区别
  - 总的来说 child 是总排序，第n个存在（指定的就得复核）就显示 type是类型排序，类排序的第n个存在就显示
  
## 12.浮动问题----父级边框塌陷的问题
- 小结：
  - 1.浮动元素后面增加空的div
    - 代码中尽量避免空div
  - 2.设置父元素的高度
    - 简单，元素假设有了固定的高度，就会被限制
  - 3.overflow --- 父级元素加
    - 简单，下拉的场景避免去使用
  - 4.父类元素中添加伪类--（推荐使用）
    - 写法稍微复杂一点，但是没有副作用，推荐使用 
  
- 13.定位（重点）
  -  1.相对定位--position: relative; /*相对定位：上下左右*/
    - 然后就可以使用基于自身的top，left进行改变
  - 2.层次定位-z-index ---最底层是0----最高……
    - z-index: 999;
  
## opacity: 0.8; /*背景透明度0-1*/
## 属性选择器
