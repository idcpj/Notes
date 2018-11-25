[TOC]

 ## 安装
1. docker 安装
`docker pull influxdb`

## 启动
1. docker 启动
`docker run -d -p 8086:8086 --name my_influxdb influxdb`
## 进入 docker 镜像
```bash
// 进入docker镜像：
docker exec -it my_influxdb bash

//进入/usr/bin目录，这里面有Influxdb的工具
root@aec85244ff22:/usr/bin# find | grep influx  
./influx
./influx_inspect
./influx_stress
./influx_tsm
./influxd

//进入Influxdb客户端命令行
/usr/bin/influx

```
## 利用influxdb的API来写数据
> [官网教程](https://docs.influxdata.com/influxdb/v1.4/tools/api/#write)

## sql 常用
```
#创建数据库
create database "db_name"
#显示所有的数据库
show databases
#删除数据库
drop database "db_name"
#使用数据库
use db_name
# 查询
select * from table_name
#显示该数据库中所有的表
show measurements
#创建表，直接在插入数据的时候指定表名
insert test,host=127.0.0.1,monitor_name=test count=1
#删除表
drop measurement "measurement_name"
```