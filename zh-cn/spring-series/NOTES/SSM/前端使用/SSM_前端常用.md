# Ajax
- 必须了解的事件机制!!



- javaScript切版本
![img.png](img.png)


# HTML + CSS:略懂 + js(超级熟练)

- js:
 - 函数:闭包()()
 - DOM -id name tag
   - create remove
 - BOM
    - window document
    
- 前端化工程:SSM+VUE+BootStrap

# 逻辑
- 判断
- 循环

# 事件
- 浏览器事件:window document
- Dom事件:增,删,遍历,修改节点元素


- jQuery

# 视图
- html
- css  :难点:BootStrap


# 通信
- xhr  ajax
- 




# 事件
> 比如点击,离开焦点,触发一些东西


- 点击:
```
    script中写
    
    $(function (){
    $("#btn").click(function (){
    console.log("111");
    })
    });
    
    
    <input type="button" value="加载数据" id="btn">
    
    
    
    
    应用:打印restController或者Response
        <script>

        $(function (){
            $("#btn").click(function (){
                /*
                * $.post(url,param[可以省略],success)
                * */
                $.post("${pageContext.request.contextPath}/a2",function (data){
                    console.log(data);
                })
            })
        });
    </script>
    
    
    
```

- 焦点

```
    script-
            function a(){
          $.post({
            url:"${pageContext.request.contextPath}/a1",
            data:{"name":$("#username").val()},
          success:function (data){
            alert(data);
          }
      })
    
        };


  用户名:<input type="text" id="username" onblur="a()">

```

- 取json 
    -   var XXX="<>";
        })
        $("#content").html(XXX);


可以在 $(document).ready(function(){    })里面写
