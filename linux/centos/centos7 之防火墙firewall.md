# centos 7 

### 查看已经开放的端口：
```firewall-cmd --list-ports```

### 开启端口:

```firewall-cmd --zone=public --add-port=80/tcp --permanent```

命令含义：
```
    –zone #作用域
    –add-port=80/tcp #添加端口，格式为：端口/通讯协议
    –permanent #永久生效，没有此参数重启后失效
```
### 重启防火墙
```
    firewall-cmd --reload #重启firewall
    systemctl stop firewalld.service #停止firewall
    systemctl disable firewalld.service #禁止firewall开机启动
    firewall-cmd --state #查看默认防火墙状态（关闭后显示notrunning，开启后显示running）
```
[来自:<https://www.linuxidc.com/Linux/2016-12/138979.htm> ](<https://www.linuxidc.com/Linux/2016-12/138979.htm> )
 

# centos7的一些变化,firewalld替换iptables、systemctl 替换service

1. 防火墙命令用firewalld取代了iptables了。
```
    查看防火墙状态   systemctl status firewalld
    临时关闭防火墙命令，reboot之后，防火墙自动起来。   systemctl stop firewalld
    永久关闭防火墙命令。reboot之后，防火墙不会自动启动    systemctl disable firewalld
    启动防火墙命令   systemctl enable firewalld
``` 
2. 用systemctl 代替了service，不过为了向后兼容，centos7中，service还是可以用的。
```
    如使用systemctl关闭防火墙
    systemctl stop firewalld.service
```
[来自: <https://www.cnblogs.com/qq1871707128/p/8065747.html> 
]( <https://www.cnblogs.com/qq1871707128/p/8065747.html> 
)

[过滤防火墙](https://stackoverflow.com/questions/24756240/how-can-i-use-iptables-on-centos-7)

[Centos7 防火墙概念
](http://blog.51cto.com/13554487/2055630)


