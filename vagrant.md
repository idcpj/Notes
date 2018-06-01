
[TOC]
> [vagrant box下载](https://app.vagrantup.com/boxes/search)

## 推荐版本
vagrant   2.0.4
VirtualBox 5.2.12

## 插件
1. vagrant-vbguest：自定义共享目录（建议安装）
`vagrant plugin install vagrant-vbguest`
有时候无法使用共享目录 可以安装此插件


## 流程
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

    ```bash
 	config.vm.synced_folder ".","/vagrant",type:"virtualbox"
    
    //如果是没有同步没有权限的文件用如下方法 (适合window)
    config.vm.synced_folder "bin", "/usr/local/bin", type: "rsync",
    rsync__exclude: ".git/",
    rsync__args: ["--verbose", "--rsync-path='sudo rsync'", "--archive", "--delete", "-z"]
    
     #这种方式可以用主机上的mysql管理软件连接虚拟机的mysql
	config.vm.network "public_network", ip: "192.168.1.11"
    ``` 
    
6. 连接虚拟机
- window 	用户登录
  方法一
     ```
    主机：127.0.0.1
    端口号：2222
    用户名：vagrant
    密码：私钥
	```
	方法二
    ```
    通过choco 安装 ssh
    
    vagrant ssh
    ```

- mac 用户登录
`vagrant ssh`

**错误处理**
1. `vagrant up` 时,`/sbin/mount.vboxsf: mounting failed with the error: No such device`

    在宿主机命令窗口安装 `vagrant plugin install vagrant-bindfs`
    
2. 疑问:如果有任何疑问,可以打开gui为true  查看错具体错误

---

## 端口转发
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

## 优化
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
## 打包  
`vagrant package --output xxx.box --base 虚拟机名称`

        
----------


## 常用命令 

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
|vagrant resume|环形休眠|
|vagrant halt|关闭虚拟机|
|vagrant reload|重启,更新配置|

> 实际使用过程中，通过 vagrant suspend/resume 来快速暂停 / 恢复最为方便。



  [1]: https://www.vagrantup.com/docs/synced-folders/virtualbox.html