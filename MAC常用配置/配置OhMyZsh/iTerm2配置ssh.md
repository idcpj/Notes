[TOC]

1. 创建shell命令文件，具体的路径自己放置
`vim ~/iterm2login.sh`
内容:
```
#!/usr/bin/expect

set timeout 30
spawn ssh -p [lindex $argv 0] [lindex $argv 1]@[lindex $argv 2]
expect {
        "(yes/no)?"
        {send "yes\n";exp_continue}
        "password:"
        {send "[lindex $argv 3]\n"}
}
interact
```

2. 赋予权限
`chmod +x ~/iterm2login.sh`

3. 测试,是否成功登陆
`~/iterm2login.sh 22 username 127.0.0.1 password`

4. 配置在item2中
![](https://upload-images.jianshu.io/upload_images/3069960-f92722d3654fff01.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)


