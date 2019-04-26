

# ubuntu 随笔

### unbuntu 安装deb rpm文件

方法一：
1. 先安装 alien 和 fakeroot 这两个工具，其中前者可以将 rpm 包转换为 deb 包。安装命令为：
```sudo apt-get install alien fakeroot```
2. 将需要安装的 rpm 包下载备用，假设为 package.rpm。
3. 使用 alien 将 rpm 包转换为 deb 包：
```fakeroot alien package.rpm```
4. 一旦转换成功，我们可以即刻使用以下指令来安装：
```sudo dpkg -i package.deb```


### Ubuntu ssh启动


SSH分客户端```openssh-client```和```openssh-server```
如果你只是想登陆别的机器的SSH只需要安装```openssh-client```
ubuntu有默认安装，如果没有则```sudo 
apt-get install openssh-client```），如果要使本机开放SSH服务就需要安装openssh-server
```sudo apt-get install openssh-server```
然后确认sshserver是否启动了：
```ps -e |grep ssh```
如果看到sshd那说明ssh-server已经启动了。
如果没有则可以这样启动：```sudo /etc/init.d/ssh start``` 或者 ```service ssh start
ssh-server```配置文件位于```/etc/ssh/sshd_config```，在这里可以定义SSH的服务端口，默认端口是22，你可以自己定义成其他端口号，如222。
然后重启SSH服务：
```sudo /etc/init.d/ssh stop```
```sudo /etc/init.d/ssh start```
然后使用以下方式登陆SSH：
```ssh username@192.168.1.112 username为192.168.1.112``` 机器上的用户，需要输入密码。

来自 [原文](<http://www.cnblogs.com/nodot/archive/2011/06/10/2077595.html>)  

### 卸载

```apt-get purge / apt-get --purge remove```
删除已安装包（不保留配置文件)。 
如软件包a，依赖软件包b，则执行该命令会删除a，而且不保留配置文件

```apt-get autoremove ```
删除为了满足依赖而安装的，但现在不再需要的软件包（包括已安装包），保留配置文件。

```apt-get remove ```
删除已安装的软件包（保留配置文件），不会删除依赖软件包，且保留配置文件。

```apt-get autoclean ```
APT的底层包是dpkg, 而dpkg 安装Package时, 会将 *.deb 放在 ```/var/cache/apt/archives/```中，```apt-get autoclean ```只会删除 ```/var/cache/apt/archives/ ```已经过期的deb。

```apt-get clean ```
使用 ```apt-get clean``` 会将 ```/var/cache/apt/archives/``` 的 所有 deb 删掉，可以理解为 ```rm /var/cache/apt/archives/*.deb```

[原文](https://blog.csdn.net/get_set/article/details/51276609)https://blog.csdn.net/get_set/article/details/51276609

### ubuntu 卡怎么办

1. 安装cpu频率管理软件
```sudo apt-get install cpufrequtils```
2. 查看cpu当前状态```cpufreq-info```
3. 设置cpu模式
```sudo cpufreq-set -g performance```
4. 设置当下策略下cpu频率

   ```sudo cpufreq-set -d 1800m -u 2700m   //适用模式：powersave|ondemand|conservative|performance```
   
   ```sudo cpufreq-set -f {1800m~2700m}   //适用模式：userspace ```
   
    -d 设置最小频率
   
    -u 设置最大频率

[原文](https://blog.csdn.net/Heimerdinger_Feng/article/details/79126365)https://blog.csdn.net/Heimerdinger_Feng/article/details/79126365

### 内存优化

1. 查看你的系统里面的swappiness
```cat /proc/sys/vm/swappiness ```
不出意外的话，你应该看到是 60 

2. 修改swappiness值为10
```sudo sysctl vm.swappiness=10 ```
但是这只是临时性的修改，在你重启系统后会恢复默认的60，所以，还要做一步：```sudo gedit /etc/sysctl.conf ```
在这个文档的最后加上这样一行：
```vm.swappiness=10```
定时释放内存
该操作可能导致部分浏览器页面内容丢失 

[原文](https://blog.csdn.net/qq_21398167/article/details/51657977) https://blog.csdn.net/qq_21398167/article/details/51657977

编译文件：```vim /root/satools/freemem.sh```
```
#!/bin/bash

used=`free -m | awk 'NR==2' | awk '{print $3}'`
free=`free -m | awk 'NR==2' | awk '{print $4}'`

echo "===========================" >> /var/log/mem.log
date >> /var/log/mem.log
echo "Memory usage | [Use：${used}MB][Free：${free}MB]" >> /var/log/mem.log

if [ $free -le 100 ] ; then
                sync && echo 1 > /proc/sys/vm/drop_caches
                sync && echo 2 > /proc/sys/vm/drop_caches
                sync && echo 3 > /proc/sys/vm/drop_caches
                echo "OK" >> /var/log/mem.log
else
                echo "Not required" >> /var/log/mem.log
fi
```
将脚本添加到crond任务，定时执行。

```echo "*/1 * * * * root /root/satools/freemem.sh" >> /etc/crontab```
或```crontab -e```添加```*/1 * * * * root /root/satools/freemem.sh```

[原文](https://blog.csdn.net/u010746357/article/details/81813739)https://blog.csdn.net/u010746357/article/details/81813739

### 添加.desktop文件应用

 在ubuntu系统的```/usr/share/applications```文件夹下面存放着系统中所有的快捷图标，我们也要在这里创建一个```***.desktop```这样就可以点击图标启动软件。这个话题也是这篇文章的重点。

          方法1： 模仿别的 .desktop文件   ，  这样成功的概率比较低，如果不熟悉的话。

          方法2： 使用gnome-panel，这个工具能够帮助我们创建快捷图标，能确保功能上的正常，但是图标需要自己修改以下路径。

```        
            //安装gnome-panel     sudo apt-get install gnome-panel                              

           //使用gnome-panel     gnome-desktop-item-edit   [选线] [路径]  [指令]

          gnome-desktop-item-edit /usr/share/applications/ --create-new    这条命令就是在/usr/share/applications/ 下创建一个新的图标
```
           会弹出对话框，填写name, excu, comment 等信息创建成功了，可以在该目录下看到，而且点击的时候就能打开软件，


[原文](https://blog.csdn.net/jameslong108159/article/details/40476517)https://blog.csdn.net/jameslong108159/article/details/40476517 

### ubuntu 防火墙

1. 安装

```sudo apt-get install ufw```

2. 启用

```sudo ufw enable```

```sudo ufw default deny```

运行以上两条命令后，开启了防火墙，并在系统启动时自动开启。关闭所有外部对本机的访问，但本机访问外部正常。

3. 开启/禁用

```sudo ufw allow|deny [service]```

打开或关闭某个端口，例如：
```
sudo ufw allow smtp　允许所有的外部IP访问本机的25/tcp (smtp)端口

sudo ufw allow 22/tcp 允许所有的外部IP访问本机的22/tcp (ssh)端口

sudo ufw allow 53 允许外部访问53端口(tcp/udp)

sudo ufw allow from 192.168.1.100 允许此IP访问所有的本机端口

sudo ufw allow proto udp 192.168.0.1 port 53 to 192.168.0.2 port 53

sudo ufw deny smtp 禁止外部访问smtp服务

sudo ufw delete allow smtp 删除上面建立的某条规则
```

4. 查看防火墙状态

```sudo ufw status```

一般用户，只需如下设置：
```
sudo apt-get install ufw

sudo ufw enable

sudo ufw default deny
```

以上三条命令已经足够安全了，如果你需要开放某些服务，再使用sudo ufw allow开启。

开启/关闭防火墙 (默认设置是’disable’)

```sudo  ufw enable|disable```

转换日志状态

```sudo  ufw logging on|off```

设置默认策略 (比如 “mostly open” vs “mostly closed”)

```sudo  ufw default allow|deny```

许 可或者屏蔽端口 (可以在“status” 中查看到服务列表)。可以用“协议：端口”的方式指定一个存在于/etc/services中的服务名称，也可以通过包的meta-data。 ‘allow’ 参数将把条目加入 /etc/ufw/maps ，而 ‘deny’ 则相反。基本语法如下：

```sudo ufw allow|deny [service]```

显示防火墙和端口的侦听状态，参见 /var/lib/ufw/maps。括号中的数字将不会被显示出来。

```sudo ufw status```

UFW 使用范例：

允许 53 端口

```$ sudo ufw allow 53```

禁用 53 端口

```$ sudo ufw delete allow 53```

允许 80 端口

```$ sudo ufw allow 80/tcp```

禁用 80 端口

```$ sudo ufw delete allow 80/tcp```

允许 smtp 端口

```$ sudo ufw allow smtp```

删除 smtp 端口的许可

```$ sudo ufw delete allow smtp```

允许某特定 IP

```$ sudo ufw allow from 192.168.254.254```

删除上面的规则

```$ sudo ufw delete allow from 192.168.254.254```

linux 2.4内核以后提供了一个非常优秀的防火墙工具：netfilter/iptables,他免费且功能强大，可以对流入、流出的信息进行细化控制，它可以 实现防火墙、NAT（网络地址翻译）和数据包的分割等功能。netfilter工作在内核内部，而iptables则是让用户定义规则集的表结构。

但是iptables的规则稍微有些“复杂”，因此ubuntu提供了ufw这个设定工具，以简化iptables的某些设定，其后台仍然是 iptables。ufw 即uncomplicated firewall的简称，一些复杂的设定还是要去iptables。

ufw相关的文件和文件夹有：

/etc /ufw/：里面是一些ufw的环境设定文件，如 before.rules、after.rules、sysctl.conf、ufw.conf，及 for ip6 的 before6.rule 及 after6.rules。这些文件一般按照默认的设置进行就ok。

若开启ufw之 后，/etc/ufw/sysctl.conf会覆盖默认的/etc/sysctl.conf文件，若你原来的/etc/sysctl.conf做了修 改，启动ufw后，若/etc/ufw/sysctl.conf中有新赋值，则会覆盖/etc/sysctl.conf的，否则还以/etc /sysctl.conf为准。当然你可以通过修改/etc/default/ufw中的“IPT_SYSCTL=”条目来设置使用哪个 sysctrl.conf.

/var/lib/ufw/user.rules 这个文件中是我们设置的一些防火墙规则，打开大概就能看明白，有时我们可以直接修改这个文件，不用使用命令来设定。修改后记得ufw reload重启ufw使得新规则生效。

下面是ufw命令行的一些示例：

````ufw enable/disable```:打开/关闭ufw

```ufw status```：查看已经定义的ufw规则

```ufw default allow/deny```:外来访问默认允许/拒绝

```ufw allow/deny 20```：允许/拒绝 访问20端口,20后可跟/tcp或/udp，表示tcp或udp封包。

```ufw allow/deny servicename```:ufw从/etc/services中找到对应service的端口，进行过滤。

```ufw allow proto tcp from 10.0.1.0/10 to 本机ip port 25```:允许自10.0.1.0/10的tcp封包访问本机的25端口。

```ufw delete allow/deny 20```:删除以前定义的"允许/拒绝访问20端口"的规则

[原文](https://www.cnblogs.com/sweet521/p/5733466.html)https://www.cnblogs.com/sweet521/p/5733466.html

### ubuntu 杀进程

１. 根据端口查找进程
```sudo lsof -i```:端口号

２. 杀掉进程
```sudo kill PID```号