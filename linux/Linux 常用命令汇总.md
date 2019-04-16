# linux 命令总结
------------------
- ~~linux~~ 核心万物皆文件
- **个人感觉**
```
    histroy 如字面历史回查记录最好的方法，举例如果你忘记了某个敲过的命令了 history就会帮到你了
    ls          显示当前路径下的文件信息，不是全部显示 -a 全部显示 -l 显示时间 -h提供技术支持
    pwd      输出你所在位置的详细信息
    cd        进入某一个路径 cd /etc 重当前路径进入etc路径 cd .. 或cd/ 回到上一路径和回到跟目录
    tab       补全键 神器记不住那你就tab吧  
    env       查看配置
    ping ip 测试网络是否畅通
```
-----------------
- ssh 命令
```
    ssh -i ~/.ssh/liyddsshkey root@192.168.1.1 -p 123456
    ssh root@192.168.1.1
    ssh
     ···远程登陆方式的一种linux 系统下的便捷公交
     ···第一种是携带秘密文件 密钥密码登陆 root用户
     ···第二种root用户登陆，过程会让你输入秘密提示
    ssh 默认自动开启，协议端口：22
```
- etc 核心目录
```
    etc/passwd 用户配置
    etc/group  分组配置
    etc/profile 相当于windows下的path
```
- chmod
```
    chmod 1-777 文件名 
    linux 系统下文件有3种全新可读r  可写w 可执行x
    r = 4 
    w = 2
    x = 1
    chmod abc filename abc对应含义是：
     a = user 用户
     b = group 分组
     c = other 另外
```
- ip 本机查询
```
   windows > ipconfig
   linux > ip addr -or- ifconfig(需要预装） 
```
- 网关，路由，进程简介
```
    1.tracert
    2.netstat
    3.ps
```
- linux 任务调度crontab
```
    crontab
```
- mv and cp
```
    mv 移动 修改文件名称
    cp 复制
```
- 查看rpm安装信息
```
    rpm -qa a代表全部  
    rpm -q 加文件名 
    rpm -e 文件名 删除某个程序
    rpm -qa|grep a  查询是否存在命令a
```
- find命令
```
     find /home -amin -10  十分钟内存取的文件或目录
     find /home -atime -10 十小时内存取的文件或目录
     find /home -cmin -10 十分钟内更改过的文件或目录
     find /home -ctime +10 十小时前更改过的文件或目录
     find /home -size +10k  查找/home目录下大小为10k的文件
```
- 压缩tar zip gzip 7z 后追加文件路径
```
• tar命令
解包：tar -zxvf FileName.tar
压缩：tar -zcvf FileName.tar DirName
压缩多个文件：tar zcvf FileName.tar.gz DirName1 DirName2 DirName3 ...
• gz命令
解压1：gunzip FileName.gz
解压2：gzip -d FileName.gz
压缩：gzip FileName
• bz2命令
解压1：bzip2 -d FileName.bz2
解压2：bunzip2 FileName.bz2
压缩： bzip2 -z FileName
.tar.bz2
解压：tar jxvf FileName.tar.bz2
压缩：tar jcvf FileName.tar.bz2 DirName
• bz命令
解压1：bzip2 -d FileName.bz
解压2：bunzip2 FileName.bz
• Z命令
解压：uncompress FileName.Z
压缩：compress FileName
• zip命令
解压：unzip FileName.zip
压缩：zip FileName.zip DirName
```
- vim

```
  ctrl+s  进入假死状态  
  ctrl+q 解除假死状态
  i 进入编译模式
  esc :wq 保存推出
  :q 退出
  /a 快速检索 为a的内容并确定其所在位置
```
uname -a 查看系统信息
date 查看系统时间
hwclock 查看系统硬件时间
```
    1.  安装ntpdate工具
    # yum -y install ntp ntpdate
    2.  设置系统时间与网络时间同步
    # ntpdate cn.pool.ntp.org
    3.  将系统时间写入硬件时间
    # hwclock --systohc 
```
tcp 最大链接数：65535



查询历史快捷键

> control + r 快速在历史记录中匹配