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
每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除
```
upstream test {
    server localhost:8080;
    server localhost:8081;
}
server {
    listen       81;                                                         
    server_name  localhost;                                               
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