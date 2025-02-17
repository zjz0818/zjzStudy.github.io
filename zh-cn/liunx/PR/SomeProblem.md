# 
无法使用su,报错
解除措施:
启动终端，输入命令sudo passwd root，输入用户密码，提示以下信息，意思是设置新的root密码.


yum 不可用

sudo apt-get update
sudo apt-get upgrade


- 安装linux（ubuntu）安装 GCC 和 G++ C++ 开发环境
- 1.先安装 ：sudo apt-get install build-essential

2.查看 gcc 版本 然后安装 统一版本的 g++

gcc --version


3 安装 g++

sudo apt-get install g++-4.4

4查看安装版本
g++ --version
g++ (Ubuntu/Linaro 4.4.4-14ubuntu5) 4.4.5


- 使用xshell连接ubuntu
Xshell是一个安全终端模拟软件，可以进行远程登录。我使用XShell的主要目的是在Windows环境下登录Linux终端，传输一些大文件到Linux环境上去。

1、下载安装xshell客户端，在安装时可以选择个人/学校免费版，这样不需要付费。

2、安装完成之后，如果你直接连接Ubuntu主机会发现连接不上，这是因为Ubuntu主机没有开启SSH服务，需要开启openssh-server：

root@ubuntu:~# sudo apt-get install openssh-server
使用

root@ubuntu:~# ps -e | grep ssh
如果只有ssh-agent表示还没启动，需要

root@ubuntu:~# /etc/init.d/ssh start
如果显示sshd则说明已启动成功。

ifconfig -a命令 查看ip






