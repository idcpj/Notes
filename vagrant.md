
# Vagrant

---
[TOC]

### 流程
1. 添加虚拟机
    1. `vagrant box add centos/7` 官网下载  `centos/7` 为官网包
    2.  添加镜像 下载xxx.box  `vagrant box add centos_test /Downloads/centos7.box`  cetnos_test 名称可随意
3. `vagrant init  cetnos/7`   初始化
    * 新建**centos_7_64**目录
    *  在该目录下 `vagrant init  cetnos/7 `
    在到centos_7_64目录的`vagrant`文件 修改
    ```
    config.vm.box = "centos/7"   修改对应的box
    ```
4. `vagrant up` 启动
5. 修改`Vagrantfile`文件的配置

    ```
 	config.vm.synced_folder ".","/vagrant",type:"virtualbox"
	config.vm.network "public_network", ip: "192.168.0.17"
    ``` 
    
6. 连接虚拟机
```
window 用户登录
主机：127.0.0.1
端口号：2222
用户名：vagrant
密码：私钥

mac 用户登录
vagrant ssh
```

**错误处理**
1. `vagrant up` 时,`/sbin/mount.vboxsf: mounting failed with the error: No such device`

    在宿主机命令窗口安装 `vagrant plugin install vagrant-bindfs`
    
---

### 端口转发
    方法一: 通过virtual Box  配置
                在设置->网络/端口转发
    方法二: 在vagrant 配置文件中配置
                在宿主对应文件夹下 的vagrant 
    		    	Vagrant.configure("2") do |config|
                      # ...
                      config.vm.network "forwarded_port", guest: 80, host: 8080
                    end
    注意:host 的端口号 必须大于 1024

---

### 优化
1. 优化虚拟机
```
config.vm.provider "virtualbox" do |vb|
		#虚拟机名称
		vb.name = "ubuntu_box"
		#虚拟机主机名
		config.vm.hostname = "ubox"
		#配置虚拟机内存和CPU
		vb.memory = "1024"
		vb.cpus=2
  end
```

2. 自动更新源
```
config.vm.provision "shell", inline: <<-SHELL
    sudo yum -y update
    cd /etc/yum.repos.d
	sudo mv CentOS-Base.repo CentOS-Base.repo.bak
	sudo wget http://mirrors.163.com/.help/CentOS-Base-163.repo
	sudo yum clean all
	sudo  yum makecache
SHELL
```
3. 同步文件
    [官方说明][1]

```
1. ngnix
    sudo /etc/ngnix/ngnix.conf
    	http{
    		sendfile off;
    	}

2. apache 
    默认已关
    EnableSendfile Off
```
---
### 打包  
`vagrant package --output xxx.box --base 虚拟机名称`

        
---
### 推荐版本! 

- vagrant_1.8.6
- VirtualBox-5.1.22-115126-Win


----------


### 常用命令 

|命令|说明|
|---|---|
|vagrant box list|查看box列表|
|vagrant box  add|新增一个box|
|vagrant box  reomve|删除制定box|
|vagrant box list|查看box列表|


----------

|命令|说明|
|---|---|
|vagrant init|初始化box|
|vagrant up|启动虚拟机|
|vagrant ssh|登录虚拟机|
|vagrant suspend|休眠|
|vagrant halt|关闭虚拟机|
|vagrant reload|重启,更新配置|


  [1]: https://www.vagrantup.com/docs/synced-folders/virtualbox.html