## 安装docker app即可

### mysql

> docker run -p 3306:3306 --name mymysql -v ~/docker/mysql/conf:/etc/mysql/conf.d -v ~/docker/mysql/logs:/logs -v ~/docker/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql

```bash
-p 3306:3306：将容器的 3306 端口映射到主机的 3306 端口。

-v -v ~/docker/mysql/conf:/etc/mysql/conf.d：将主机当前目录下的 conf/my.cnf 挂载到容器的 /etc/mysql/my.cnf。

-v ~/docker/mysql/logs:/logs：将主机当前目录下的 logs 目录挂载到容器的 /logs。

-v ~/docker/mysql/data:/var/lib/mysql ：将主机当前目录下的data目录挂载到容器的 /var/lib/mysql 。

-e MYSQL_ROOT_PASSWORD=123456：初始化 root 用户的密码。
```

### redis

> docker run -p 6379:6379 -v ~/docker/redis/data:/data  -d redis redis-server --appendonly yes

```bash
-p 6379:6379 : 将容器的6379端口映射到主机的6379端口

-v ~/docker/redis/data:/data : 将主机中当前目录下的data挂载到容器的/data

redis-server --appendonly yes : 在容器执行redis-server启动命令，并打开redis持久化配置
```



> docker ps -a         查看所有容器包含停止的
>
> docker rm containerid/name         移除容器
>
> docker stop containerid/name      停止容器
>
> docker start containerid/name	  开启容器
>
> docker kill containerid/name	强制退出容器