# ubuntu 安装mysql
1. 执行install 命令安装
```
    sudo apt-get install mysql-server
    sudo apt install mysql-client
    sudo apt install libmysqlclient-dev
```

2. 执行```ps -ef | grep mysql```查看安装状态;如果返回
```
    root      5542  7966  0 21:07 pts/1    00:00:00 grep --color=auto msyql
```
安装成功

3. 初次登录
```
    mysql -u root -p                 "设置root密码"
```

4. 修改配置文件
```
    vi /etc/mysql/mysql.conf.d/mysqld.cnf
    将bind-address = 127.0.0.1
    改#bind-address = 127.0.0.1
```

5. 进入mysql 服务```mysql -u root -p```进行授权
```
    grant all on *.* to root@'%' identified by '你的密码' with grant option;
    flush privileges;
```

6. 重启服务
```
    service mysql restart
```