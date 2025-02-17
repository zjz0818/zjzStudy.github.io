## window下根据端口杀死进程的方式
- 1.查看该端口被占用的进程号

`netstat -nao | findstr "端口号"`
- 2.删除指定的进程

`taskkill /f /pid "进程号"`

## Linux下根据端口杀死进程
- 1.查看
    - `ps -ef|grep 名字`
- 2.杀死
    - `kill -9 PID`
