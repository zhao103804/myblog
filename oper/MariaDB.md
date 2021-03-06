
# CentOS 7安装MariaDB 10详解以及相关配置

## 第一步：添加 MariaDB yum 仓库

首先在CentOS操作系统中/etc/yum.repos.d/目录下添加 MariaDB的YUM配置文件MariaDB.repo文件。  
```
vi /etc/yum.repos.d/MariaDB.repo
```
在该文件中添加以下内容保存：  
```
[mariadb]  
name = MariaDB  
baseurl = http://yum.mariadb.org/10.2/centos7-amd64  
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB  
gpgcheck=1
```

## 第二步：安装 MariaDB

通过yum命令轻松安装 MariaDB。  
```
yum install MariaDB-server MariaDB-client -y
```
MariaDB 安装完毕后，立即启动数据库服务守护进程。  
```
systemctl start mariadb
```
设置 MariaDB 在操作系统重启后自动启动服务。  
```
systemctl enable mariadb
``` 
查看 MariaDB 服务当前状态。  
```
systemctl status mariadb
```

设置MariaDB数据库密码  
```
mysqladmin -u root password 'newpassword'
```
如果root已经设置过密码，采用如下方法   
```
mysqladmin -u root -p 'oldpassword' password 'newpassword'
```

root账户中的host项是localhost表示该账号只能进行本地登录，我们需要修改权限，输入命令：  
```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

刷新生效  
```
FLUSH PRIVILEGES;
```