1. 问题——idea无法使用中文输入
   原因：idea本身版本过高，所以需要你强制减低它的jdk版本

解决：使用配置idea环境变量解决  ps：目前适用于任何版本的jdk和idea

步骤：
1.新建一个IDEA的home（如果有就覆盖它），配置IDEA_JDK_64 路径为java jdk路径

![img.png](img.png)


2.配置path %IDEA_JDK_64%
![img_4.png](img_4.png)
3.重启