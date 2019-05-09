# mac 安装redis
> 可以去[官网](https://redis.io/download)下载
> 或者```wget http://download.redis.io/releases/redis-5.0.4.tar.gz```

下载成功后
> sudo mv /usr/local        #放到你想放的位置就行
> cd /usr/local
> sudo make install
> nohup redis-server
> vim redis.conf  修改配置文件

```bin
redis-server: Redis服务器
redis-cli: 命令行客户端
redis-benchmark: Redis的性能测试工具
redis-check-aof: AOF文件修复工具
redis-check-dump: RDB文件检测工具
redis.conf: Redis的配置文件
```

```properties
这是守护进程的开关，改为 yes
deamonize yes
bind 0.0.0.0 所有网落都可以访问
```

# brew 安装
> brew install redis
> brew services start redis 后台运行redis