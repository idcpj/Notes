
[TOC]

## 常用代码

### format() 方法将日期转换为指定格式的文本
```java
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
Date now = new Date();
System.out.println(sdf.format(now));//2018-02-14 13:22:12
```
### parse() 方法将文本转换为日期
```
public static void main(String[] args) throws ParseException {
    String d = "2014-6-1 21:05:36";
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    Date date = sdf.parse(d);
    System.out.println(date);//Sun Jun 01 21:05:36 CST 2014
}
```

