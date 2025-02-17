# AJAX
## 介绍
- 1.AJAX 指异步 **JavaScript** 及 **XML**（Asynchronous JavaScript And XML）
    - Ajax的核心是JavaScript对象XmlHttpRequest。
    - 一种用于创建更好更快以及交互性更强的Web应用程序的技术
- 2.传统的网页，想要更新内容或提交一个表单，都需要重新加载整个页面
    - 使用Ajax，通过在后台服务器进行少量的数据交换，就可以实现异步局部更新
    
- H5 + 网页 + 客户端 + 手机端（Android，IOS）+小程序
- 使用jQuery需要先导入jQuery的js文件（jQuery官网下载）



# 一个简单的页面嵌套

  ```      
      <html>
      <head>
          <title>IframeTest</title>
      
          <script>
              function go(){
                  var url = document.getElementById("url").value;
                  document.getElementById("iframe1").src=url;
      
              }
          </script>
      </head>
      <body>
      
      <div>
          <p>please input URL</p>
          <p>
              <input type="text" id="url" value="https://www.bilibili.com/video/BV1aE41167Tu?p=24&spm_id_from=pageDriver">
              <input type="button" value="submit" onclick="go()">
          </p>
      </div>
      
      <div>
          <iframe id="iframe1"  style="width:100%;height: 500px"></iframe>
      </div>
      </body>
      </html>
  
  
  ```



# Ajax
- 必须了解的事件机制!!



- javaScript切版本
  ![img.png](img.png)









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






