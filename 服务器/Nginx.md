[TOC]

## 反向代理

```
server {  
    listen       80;                                                         
    server_name  localhost;                                               
    client_max_body_size 1024M;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host:$server_port;
    }
}
```
>localhost的时候，就相当于访问localhost:8080了


## 负载均衡

### RR（默认）
1. 每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除
2. 可以配置在虚拟站点下, 但是此时只会走8080 或者8081 81端口本身不会成为站点
```
upstream test {
    server 127.0.0.1:8080;
    server 127.0.0.1:8081;
}
server {
    listen       81;                                                         
    server_name  127.0.0.1;                                               
    client_max_body_size 1024M;

    location / {
        proxy_pass http://test;
        proxy_set_header Host $host:$server_port;
    }
}
```
>当访问calohost:81时,如果localhost:8081 挂了,也不会影响正常访问

### 权重

```
upstream test {
    server localhost:8080 weight=9;
    server localhost:8081 weight=1;
}
```
>10次一般只会有1次会访问到8081，而有9次会访问到8080


### ip_hash
PR 和权重  在有`session` 进行访问时,由于随机访问,导致`session`无效,需要使用`ip_hash`
```
upstream test {
    ip_hash;
    server localhost:8080;
    server localhost:8081;
}
```

### fair（第三方）

按后端服务器的响应时间来分配请求，响应时间短的优先分配。
```
upstream backend { 
    fair; 
    server localhost:8080;
    server localhost:8081;
}
```

### url_hash（第三方）
按访问url的hash结果来分配请求，使每个url定向到同一个后端服务器，后端服务器为缓存时比较有效。 在upstream中加入hash语句，server语句中不能写入weight等其他的参数，hash_method是使用的hash算法。
```
upstream backend { 
    hash $request_uri; 
    hash_method crc32; 
    server localhost:8080;
    server localhost:8081;
} 
```

## HTTP服务器
```
server {
    listen       80;                                                         
    server_name  localhost;                                               
    client_max_body_size 1024M;


    location / {
           root   e:wwwroot;
           index  index.html;
       }
}
```
> 这样如果访问http://localhost 就会默认访问到E盘wwwroot目录下面的index.html，如果一个网站只是静态页面的话，那么就可以通过这种方式来实现部署。

### 动静分离
```
server {  
  listen       80;  
  server_name  localhost;  

  location / {  
      root   e:wwwroot;  
      index  index.html;  
  }  

  # 所有静态请求都由nginx处理，存放目录为html  
  location ~ .(gif|jpg|jpeg|png|bmp|swf|css|js)$ {  
      root    e:wwwroot;  
  }  

  # 所有动态请求都转发给tomcat处理  
  location ~ .(jsp|do)$ {  
      proxy_pass  http://test;  
  }  

  error_page   500 502 503 504  /50x.html;  
  location = /50x.html {  
      root   e:wwwroot;  
  }  
}  
```

> 当访问gif,jpeg时 直接访问`e:wwwroot; `,正则自行配置


## 热启动
Nginx重新读取配置的命令

`nginx -s reload  `


