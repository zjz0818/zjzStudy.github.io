# Linux
- 消息队列(Kafka,RabbitMQ,ROckeetMQ),缓存(Redis),搜索引擎(ES),集群分布式(需要购买多台..)
- 一切皆文件(读写,权限)
- java,tomcat,docker




## 环境安装
> 三种方式:rpm,解压缩,yum在线安装
> 




> yum安装
- yum -y install 包名  
    - yum -y install gcc
    - yum -y install gcc-c++
    
- 安装docker
  
- 切换到 /etc/yum.repos.d 目录下，将所有 docker 相关的 repo全部删掉
- yum install -y yum-utils device-mapper-persistent-data lvm2
- sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

- yum makecache fast
- yum -y install docker-ce docker-ce-cli containerd.io
- 启动::systemctl start docker
  
- 测试
  
    ```
        docker version
         docker run hello-world
          docker images
    
    ```
