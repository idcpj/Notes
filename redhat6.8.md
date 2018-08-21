
[TOC]

## 替换源
> [参考文档](https://www.8090st.com/redhat-enterprise-6-x86_64-centos6-8-yum.html)
1. 删除redhat原有的yum
`rpm -aq|grep yum|xargs rpm -e --nodeps`

2. 下载以下安装包
```
wget http://soft.8090st.com/redhat/yum/yum-3.2.29-73.el6.centos.noarch.rpm
wget http://soft.8090st.com/redhat/yum/yum-metadata-parser-1.1.2-16.el6.x86_64.rpm
wget http://soft.8090st.com/redhat/yum/yum-plugin-fastestmirror-1.1.30-37.el6.noarch.rpm
wget http://soft.8090st.com/redhat/yum/python-iniparse-0.3.1-2.1.el6.noarch.rpm
wget http://soft.8090st.com/redhat/yum/python-urlgrabber-3.9.1-11.el6.noarch.rpm
```
3. 进行安装yum
4. 更改yum源 #我们使用网易的CentOS镜像源
```
cd /etc/yum.repos.d/
wget http://mirrors.163.com/.help/CentOS6-Base-163.repo
```
替换为一下内容,把文件里面的$releasever全部替换为版本号
```
[root@node2 /]# cd /etc/yum.repos.d/
[root@node2 yum.repos.d]# cat CentOS6-Base-163.repo 
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client. You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the 
# remarked out baseurl= line instead.
#

[base]
name=CentOS-6 - Base - 163.com
baseurl=http://mirrors.163.com/centos/6/os/$basearch/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=os
gpgcheck=1
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6
#released updates
[updates]
name=CentOS-6 - Updates - 163.com
baseurl=http://mirrors.163.com/centos/6/updates/$basearch/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=updates
gpgcheck=1
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6
#additional packages that may be useful
[extras]
name=CentOS-6 - Extras - 163.com
baseurl=http://mirrors.163.com/centos/6/extras/$basearch/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=extras
gpgcheck=1
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6
#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-6 - Plus - 163.com
baseurl=http://mirrors.163.com/centos/6/centosplus/$basearch/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=centosplus
gpgcheck=1
enabled=0
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6
#contrib - packages by Centos Users
[contrib]
name=CentOS-6 - Contrib - 163.com
baseurl=http://mirrors.163.com/centos/6/contrib/$basearch/
#mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=contrib
gpgcheck=1
enabled=0
gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6
```

5. 清理yum缓存
`yum clean all`
6.  加载缓存：
`yum makecache`