[TOC]

> [参考](https://blog.csdn.net/King_818/article/details/51395589)


## demo
1. 创建一个带分区的表
```
 CREATE TABLE part_tab ( c1 int default NULL, 
    c2 varchar(30) default NULL, 
    c3 date default NULL 
  ) engine= InnoDB
  PARTITION BY RANGE (year(c3)) (
  PARTITION p0 VALUES LESS THAN (1995), 
  PARTITION p1 VALUES LESS THAN (1996) , PARTITION p2 VALUES LESS THAN (1997) , 
  PARTITION p3 VALUES LESS THAN (1998) , PARTITION p4 VALUES LESS THAN (1999) , 
  PARTITION p5 VALUES LESS THAN (2000) , PARTITION p6 VALUES LESS THAN (2001) , 
  PARTITION p7 VALUES LESS THAN (2002) , PARTITION p8 VALUES LESS THAN (2003) , 
  PARTITION p9 VALUES LESS THAN (2004) , PARTITION p10 VALUES LESS THAN (2010), 
  PARTITION p11 VALUES LESS THAN MAXVALUE 
); 
```
2. 创建没有分区的表
```
CREATE TABLE `no_part_tab` (
  `c1` int(11) DEFAULT NULL,
  `c2` varchar(30) DEFAULT NULL,
  `c3` date DEFAULT NULL
) ENGINE=InnoDB
```
3. 创建一个生成个很数据的存储过程
```
CREATE PROCEDURE load_part_tab() 
     begin 
     declare v int default 0; 
              while v < 8000000 
     do 
     insert into part_tab 
     values (v,'testing partitions',adddate('1995-01-01',(rand(v)*36520) mod 3652)); 
     set v = v + 1; 
     end while; 
     end 
     ```