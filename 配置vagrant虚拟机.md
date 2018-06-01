[TOC]

## 安装插件
`vagrant plugin install vagrant-vbguest`

>  这样widnow 就phpstorm 就可以配置目录了

 mysql 具有访问权限
```
mysql>  GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
mysql>  flush privileges;

username : 为mysql 的用户
password: mysql的密码
```

生成的路径为项目路径对应 虚拟机中的`\vagrant`中

## 连接方式
1. 映射端口 
```
config.vm.network "forwarded_port", guest: 8888, host: 1188
config.vm.network "forwarded_port", guest: 81, host: 1181
```
 方法简单,并且虚拟机能ping 同 主机,这样mysql 就可以顺利连接了
 
 2.  桥接
 `config.vm.network "public_network",, ip: "192.168.33.10"`
 ip查看必须符合网关在同一网段
 
 > 桥接问题比较多,请自行google