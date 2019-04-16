Ubuntu系统安装Redis

> ```shell
> $sudo apt-get update
> $sudo apt-get install redis-server
> ```

Redis启动

> ```shell
> $ redis-server
> ```

Redis启动是否成功

> ```shell
> $ redis-cli
> 或
> $ ps -ef|grep redis
> ```

用apt-get或者yum install安装的redis，可以直接通过下面的命令停止/启动/重启redis

> /etc/init.d/redis-server stop 
> /etc/init.d/redis-server start 
> /etc/init.d/redis-server restart

找到Redis配置文件redis.conf

> find / -name redis.conf
>
> 文件在etc/redis/下

Redis的常用配置

> ```markdown
> `#bind 127.0.0.1port 6379 #这个为redis端口 #修改这个为yes,以守护进程的方式运行，就是关闭了远程连接窗口，redis依然运行daemonize yes #将protected-mode模式修改为noprotected-mode no #设置需要密码才能访问,password修改为你自己的密码requirepass password`
> ```

