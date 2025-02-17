## 本地项目上传到Gitee
- 方法1、先将仓库clone到本地，修改后再push到码云的仓库仓库
    - $ git clone https://gitee.com/zhangjzm/study-demo.git #将远程仓库克隆到本地
    ```
    $ git add . #将当前目录所有文件添加到git暂存区
    $ git commit -m "my first commit" #提交并备注提交信息
    $ git push origin master #将本地提交推送到远程仓库
    ```


## 强制推送
    ```
    $ git add . #将当前目录所有文件添加到git暂存区
    $ git commit -m "my first commit" #提交并备注提交信息
    $ git push origin master #将本地提交推送到远程仓库
    
    $ git push origin master -f  // 不加f就普通推送
    ```
