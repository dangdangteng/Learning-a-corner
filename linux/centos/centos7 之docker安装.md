# Docker 安装

​		使用默认安装方式

> yum install docker

​		运行方式

> ​	systemctl start docker
>
> ​	systemctl stop docker

​		查询镜像

> ​	docker search mysql

​		拉取镜像

> ​	docker pull mysql:tag     指定版本拉取

​		查看已经存在的docker镜像

> ​	docker image

​		docker 常用操作

> ​	docker run —name names(应用名) -d(后台运行) 镜像名:tag(版本号)   运行docker镜像
>
> ​    docker stop container id / names      停止docker镜像
>
> ​	docker ps 		查看正在运行的docker      -a 查看所有容器
>
> ​	docker start 容器id   开始容器
>
> ​	docker rm 容器id    删除容器
>
> ​	docker run —name names -d -p 8888:6379 redis:tag    给redis容器起一个names名称并将主机端口8888 和容器端口6379 做映射
>
> ​	