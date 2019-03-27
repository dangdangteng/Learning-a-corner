# linxu 之 SSH

1. 判断一个服务器是否开启了ssh
```
    ps -e | grep ssh   查看是否存在sshd进程
```
如果不存在,通过``` /etc/init.d/ssh -start ```启动ssh进程,如果提示不存在通过
```sudo apt-get install openssh-server```进行安装

2. 第一步骤走完发现ssh 链接不上
```
    检查防火墙
       --Ubuntu :  sudo ufw status
       
       关闭              sudo ufw disable
       
       --centos :  sudo firewall-cmd --state
       
       关闭             systemctl stop firewalld.service
    关闭防火墙或者放开22端口即可,个人不建议关闭
```

3. ssh 远程链接
```
    ssh username@ip  
    eg: ssh root@192.168.1.1  会提示让你输入密码,输入密码即可
```