[TOC]

## 安装
1. centos
`yum -y install httpd-tools`

## 参数说明
```
-n  即requests，用于指定压力测试总共的执行次数。
-c  即concurrency，用于指定的并发数。
-t  即timelimit，等待响应的最大时间(单位：秒)。
-w  以HTML表格形式打印结果。
-C  添加cookie信息，例如："Apache=1234"(可以重复该参数选项以添加多个)。
-H  添加任意的请求头，例如："Accept-Encoding: gzip"，请求头将会添加在现有的多个请求头之后(可以重复该参数选项以添加多个)。
-A  添加一个基本的网络认证信息，用户名和密码之间用英文冒号隔开。
-P  添加一个基本的代理认证信息，用户名和密码之间用英文冒号隔开。
-X  指定使用的端口号，例如:"126.10.10.3:88"。
-k  使用HTTP的KeepAlive特性。
-h  显示用法信息，其实就是ab -help。
```

## demo
`ab -c 100 -n 10000 http://www.baidu.com/`   注意只有域名会报错,需要使用 `/`

```
Server Software:        nginx/1.10.2 	(服务器软件名称及版本信息)
Server Hostname:        192.168.1.106	(服务器主机名)
Server Port:            80 (服务器端口)
Document Path:          /index1.html. 		(供测试的URL路径)
Document Length:        3721 bytes		 (供测试的URL返回的文档大小)
Concurrency Level:      1000 			(并发数)
Time taken for tests:   2.327 seconds 			(压力测试消耗的总时间)
Complete requests:      5000 				(的总次数)
Failed requests:        688				 (失败的请求数)
Write errors:           0 				(网络连接写入错误数)
Total transferred:      17402975 bytes				 (传输的总数据量)
HTML transferred:       16275725 bytes 				(HTML文档的总数据量)
Requests per second:    2148.98 [#/sec] (mean) 		(平均每秒的请求数) 这个是非常重要的参数数值，服务器的吞吐量 
Time per request:       465.338 [ms] (mean) 		(所有并发用户(这里是1000)都请求一次的平均时间)
Time  request:       0.247 [ms] (mean, across all concurrent requests) 		(单个用户请求一次的平均时间)
Transfer rate:          7304.41 [Kbytes/sec] received 		每秒获取的数据长度 (传输速率，单位：KB/s)
...
Percentage of the requests served within a certain time (ms)
  50%    347  ## 50%的请求在347ms内返回 
  66%    401  ## 60%的请求在401ms内返回 
  75%    431
  80%    516
  90%    600
  95%    846
  98%   1571
  99%   1593
 100%   1619 (longest request)
 ```