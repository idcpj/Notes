[TOC]

##  一键安装php开发环境 

[oneinstack](https://oneinstack.com/install/)

## 手动安装

### 更换源
```
cd /etc/yum.repos.d
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
yum clean all
yum makecache
```

### 安装apache服务器

```bash
#安装
yum install httpd -y   
#启动
systemctl start httpd   
#重启
systemctl restart httpd
#停止
systemctl stop httpd
#开启启动
systemctl enable httpd.service

#设置目录权限
把目录分组设置成httpd.conf中相同的用户:组名
如    chown  -R www:www  .

```
### 安装mysql数据库

```bash
#安装mariadb（mysql）数据库
yum install mariadb mariadb-server -y

#启动
systemctl start mariadb
#重启
systemctl restart mariadb
#停止
systemctl stop mariadb
#开启启动
systemctl enable mariadb

#配置mariadb数据库
#开始配置
mysql_secure_installation

#会提示你输入当前的root密码，如果没有设置过，就直接回车
Enter current password for root (enter for none):

#提示是否设置root密码，输入y
Set root password? [Y/n]
#输入root密码
New password: 
#确认root密码
Re-enter new password:
#移除匿名用户，输入y
Remove anonymous users? [Y/n]
#禁用远程root用户登录如果你想在远程连接mysql，你就输入n，回车；如果为了安全考虑，不允许的话，输入y，回车
Disallow root login remotely? [Y/n]
#是否移除test数据库，不想要的话，输入y，回车
Remove test database and access to it? [Y/n]
#刷新权限、表，输入y，回车
Reload privilege tables now? [Y/n]

```

###  安装php
```bash
#安装php及其扩展，默认安装的是php5.4
yum install php php-mysql php-gd libjpeg* php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-bcmath php-mhash -y

#如果想升级php到5.6/7.0
#首先需要升级软件仓库，依次执行下面2个命令
 rpm -Uvh https://mirror.webtatic.com/yum/el7/epel-release.rpm
 rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
#删除旧的php
yum remove php-common
#安装所需要的版本，5.6版本，
yum install -y php56w php56w-opcache php56w-xml php56w-mcrypt php56w-gd php56w-devel php56w-mysql php56w-intl php56w-mbstring
#安装所需要的版本，7.0版本
yum install -y php70w php70w-opcache php70w-xml php70w-mcrypt php70w-gd php70w-devel php70w-mysql php70w-intl php70w-mbstring
#检查php是否安装成功
php -v //可以看到自己安装的php版本信息
#重启服务器
systemctl restart httpd
```

### 安装phpmyadmin

```apache
#安装phpmyadmin
sudo yum install epel-release
yum install phpmyadmin php-mcrypt
vim /etc/httpd/conf.d/phpMyAdmin.conf
修改配置文件，如下：
   <IfModule mod_authz_core.c>
     # Apache 2.4
     <RequireAny>
      # Require ip 127.0.0.1  #注释掉
      # Require ip ::1   #注释掉
      Require all granted   #新添加
     </RequireAny>
 </IfModule>

   <IfModule mod_authz_core.c>
     # Apache 2.4
     <RequireAny>
      #Require ip 127.0.0.1  #注释掉
      #Require ip ::1   #注释掉
      Require all granted   #新添加
     </RequireAny>
   </IfModule>

然后重启Apache服务器
systemctl restart httpd

#访问
http://192.168.0.17/phpmyadmin
```