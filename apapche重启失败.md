[TOC]

## 端口被占用
错误提示
```
httpd not running, trying to start
(48)Address already in use: AH00072: make_sock: could not bind to address [::]:80
(48)Address already in use: AH00072: make_sock: could not bind to address 0.0.0.0:80
no listening sockets available, shutting down
AH00015: Unable to open logs
```
查看占用的端口

```
udo lsof -iTCP:80 -sTCP:LISTEN

COMMAND   PID USER   FD   TYPE            DEVICE SIZE/OFF NODE NAME
httpd   86705 root    4u  IPv6 0x1817cbf642aa1a7      0t0  TCP *:http (LISTEN)
httpd   86723 _www    4u  IPv6 0x1817cbf642aa1a7      0t0  TCP *:http (LISTEN)
```

关闭端口
`kill 86705`

重启
`udo apachectl restart`
