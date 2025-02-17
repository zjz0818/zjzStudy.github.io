# GIT命令(GitHub  GITEE一样用)

######                                                                           常规操作 一.3（克隆）  三.3（add）  四.1（commit）六 (push)

## 一、新建代码库

 1.在当前目录新建一个Git代码库  

```linux
$ git init
```

2.新建一个目录，将其初始化为Git代码库

```linux
$ git init [project-name]
```

##### 3.下载一个项目和它的整个代码历史（常用）---复制项目

```linux
$ git clone [url]
```

## 二、配置（一次就好）

1. 显示当前的Git配置

   ```linux
   $ git config --list
   ```

2. 编辑Git配置文件

   ```linux
   $ git config -e [--global]
   ```

3.  设置提交代码时的用户信息

```linux
 //name and email
$ git config [--global] user.name "[name]"
 
$ git config [--global] user.email "[email address]"
```

## 三、增加/删除文件

1.  添加指定文件到暂存区

   ```linux
   $ git add [file1] [file2] ... 
   ```

2.  添加指定目录到暂存区，包括子目录 

   ```linux
   $ git add [dir]
   ```

3.  添加当前目录的**所有文件**到暂存区（**常用**）

   ```
   $ git add .
   ```

    添加每个变化前，都会要求确认

4.  对于同一个文件的多处变化，可以实现分次提交

   ```linux
   $ git add -p
   ```

5.   删除工作区文件，并且将这次删除放入暂存区

   ```linux
   $ git rm [file1] [file2] ..
   ```

6.   停止追踪指定文件，但该文件会保留在工作区 

   ```
   $ git rm --cached [file]
   ```

   

7.  改名文件，并且将这个改名放入暂存区

   ```linux
   $ git mv [file-original] [file-renamed]
   ```

   

   ## 四、代码提交（核心核心哈）

1.   提交暂存区到仓库区 （**常用**）

   ```linux
   $ git commit -m [message]
   ```

   

2.   提交暂存区的指定文件到仓库区

   ```linux
   $ git commit [file1] [file2] ... -m [message]
   ```

   

3.  提交工作区自上次commit之后的变化，直接到仓库区

   ```linux
   $ git commit -a
   ```

   

4.   提交时显示所有diff信息

   ```
   $ git commit -v
   ```

   

5.   使用一次新的commit，替代上一次提交

    如果代码没有任何新变化，则用来改写上一次commit的提交信息 

   ```
   $ git commit --amend -m [message]
   ```

   

6.  重做上一次commit，并包括指定文件的新变化

   ```
   $ git commit --amend [file1] [file2] ...
   ```

   

   ## 五、分支（目前推荐gitEE上直接弄）

   1.列出所有本地分支

   ```
   $ git branch
   ```

   2.列出所有远程分支

   ```
   $ git branch -r
   ```

   3.列出所有本地分支和远程分支

   ```
   $ git branch -a
   ```

   4.新建一个分支，但依然停留在当前分支

   ```
   $ git branch [branch-name]
   ```

   5.新建一个分支，并切换到该分支

   ```
   $ git checkout -b [branch]
   ```

   6.新建一个分支，指向指定commit

   ```
   $ git branch [branch] [commit]
   ```

   7.新建一个分支，与指定的远程分支建立追踪关系

   ```
   $ git branch --track [branch] [remote-branch]
   ```

   8.切换到指定分支，并更新工作区

   ```
   $ git checkout [branch-name]
   ```

   9.切换到上一个分支

   ```
   $ git checkout -
   ```

   10.建立追踪关系，在现有分支与指定的远程分支之间

   ```
   $ git branch --set-upstream [branch] [remote-branch]
   ```

   11.合并指定分支到当前分支

   ```
   $ git merge [branch]
   ```

   12.选择一个commit，合并进当前分支

   ```
   $ git cherry-pick [commit]
   ```

   13.删除分支

   ```
   $ git branch -d [branch-name]
   ```

   14.删除远程分支

   ```
   $ git push origin --delete [branch-name]
    
   $ git branch -dr [remote/branch]
   ```

   

   ## 六、远程同步

   ​	1.下载远程仓库的所有变动

   ```
   $ git fetch [remote]
   ```

   2. 显示所有远程仓库

   ```
   $ git remote -v 
   ```

   3. 显示某个远程仓库的信息

   ```
   $ git remote show [remote]
   ```

   4. 增加一个新的远程仓库，并命名

   ```
   $ git remote add [shortname] [url]
   ```

   5. 取回远程仓库的变化，并与本地分支合并（**常用**）

   ```
   $ git pull [remote] [branch]
   ```

   ​	6.上传本地指定分支到远程仓库 （**常用**）

   ```
   $ git push [remote] [branch]
   ```

   7. 强行推送当前分支到远程仓库，即使有冲突（**常用**）

   ```
   $ git push [remote] --force 
   ```

   8. 推送所有分支到远程仓库

   ```
   $ git push [remote] --all
   ```





# 我的常用：

```csharp
git add .   添加所有
git commit -m 'msg'  提交
git push orgin master // 这个之前需要提供 gitHub 账号和密码  push
```