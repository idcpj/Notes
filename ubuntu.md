[TOC]

## 使用前准备
1. 安装宝塔山
2. 安装google浏览器
```
sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -
sudo apt-get update
sudo apt-get install google-chrome-stable
```
3. 安装影梭
	安装qt5版本
    ```
    sudo add-apt-repository ppa:hzwhuang/ss-qt5
    sudo apt-get update
    sudo apt-get install shadowsocks-qt5
    ```
    安装命令行版
    ```
    apt-get install python-pip       //安装pippython-pip环境
    pip install shadowsocks        //安装ss
    vim /etc/shadowsocks.json        //打开ss配置文件
    {
    “server”:”0.0.0.0″,                         #ec2使用的是NAT，不能填公网ip，而应该用0.0.0.0
    “server_port”:端口,                        
    “password”:”连接密码”,                 
    “timeout”:300,
    “method”:”aes-256-cfb”,
    “fast_open”: false
    }
    ssserver -c /etc/shadowsocks.json -d start           //启动ss
    ```
4. SwitchyOmega配置
	[参考网站](https://blog.csdn.net/u013401853/article/details/72997524) 