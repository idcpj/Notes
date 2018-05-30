[TOC]

## 安装插件
1. vagrant-vbguest：自定义共享目录（建议安装）
`vagrant plugin install vagrant-vbguest`

2. 配置映射端口
```
config.vm.network "forwarded_port", guest: 8888, host: 1188
config.vm.network "forwarded_port", guest: 81, host: 1181
```

3. mysql 具有访问权限
```
mysql>  GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
mysql>  flush privileges;

username : 为mysql 的用户
password: mysql的密码
```