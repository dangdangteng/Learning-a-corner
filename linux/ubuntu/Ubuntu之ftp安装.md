**ftp服务**

```bash
vsftpd -version   # 查看ftp 版本信息
ps -ef | grep ftp # 查看是否有正在运行的ftp服务

apt-get purge vsftpd  # 卸载ftp服务 非root用户命令前加sudo

apt-get install vsftpd # 安装ftp服务 非root用户命令前加sudo

useradd -m 新用户  # 添加一个用户
passwd 新用户  #修改新用户的密码

vim /etc/vsftpd.conf  #编辑配置文件
增添
local_root=/home/sunftp/ftpdir
allow_writeable_chroot=YES

```

**具体配置**

```bash
listen=NO 
listen_ipv6=YES #vsftpd 将监听 ipv6 而不是 IPv4，你可以根据你的网络情况设置 anonymous_enable=NO #不允许匿名用户 
local_enable=YES #允许本地用户登录 
write_enable=YES #允许用户有修改文件权限 
local_umask=022 #本地用户创建文件的 umask 值 
dirmessage_enable=YES #用户第一次进入目录时的提示消息 
use_localtime=YES #使用本地时间 
xferlog_enable=YES #一个存有详细的上传和下载信息的日志文件 
connect_from_port_20=YES #在服务器上针对 PORT 类型的连接使用端口 20 
chroot_local_user=YES #本地用户将进入 chroot 环境，当登录以后默认情况下是其 home 目录 secure_chroot_dir=/var/run/vsftpd/empty #当vsftpd不需要访问系统文件的权限时，就会将使用者限制在此资料夹中 
pam_service_name=vsftpd #这个字符串是PAM服务vsftpd将使用的名称。必须启用 rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem #此选项指定用于SSL的RSA证书的位置，加密连接。必须开启 
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key #加密链接私匙 ssl_enable=NO 
pasv_enable=Yes 
pasv_min_port=10000 
pasv_max_port=10100 
local_root=/var/www/html #登录默认目录 
allow_writeable_chroot=YES #默认情况下，出于安全原因，VSFTPD 不允许 chroot 目录具有可写权限。然而，我们可以通过选项 allow_writeable_chroot=YES 来改变这个设置
```

ftp服务器运行

```bash
sudo /etc/init.d/vsftpd start
sudo /etc/init.d/vsftpd stop
sudo /etc/init.d/vsftpd restart
```

帮助文献

[Ubuntu16.04安装ftp服务器](https://blog.csdn.net/yancey_blog/article/details/52790451)

[ubuntu 16.04 搭建ftp服务器](https://blog.csdn.net/lj402159806/article/details/78209103)

[Ubuntu 18.04 安装FTP服务](https://blog.csdn.net/zhaoyi2/article/details/82804788)

[ubuntu18.04安装ftp服务](https://blog.csdn.net/sunxiaoju/article/details/85224602)

