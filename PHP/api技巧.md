[TOC]

## nginx 记录请求时间和响应时间
1. 配置 `nginx.conf` 文件
```
http{
	log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent $request_time $upstream_response_time  "$http_referer" '
                       '"$http_user_agent" "$http_x_forwarded_for"';
}
```
在原来的格式中加入 ` $request_time ` 请求时间 `$upstream_response_time ` 响应时间
main 为这个格式的名字
2. 配置`vhost.www.demo.conf`
```
access_log  /vagrant_data/access.log main;
```
在最后加入  `main` 指定 `access.log` 文件中的格式
3. 输出效果
`10.0.0.5 - - [12/Jun/2018:18:32:02 +0800] "GET /favicon.ico HTTP/1.1" 200 130 0.031 0.031  "http://10.0.0.111:81/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36" "-"
`