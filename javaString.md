[TOC]

## 技巧
1. 字符串不可改变，改变字符串实际上是指向了新创建的字符串对象
```
String s1 = "imooc";
s1 ="i love"+s1;
```
2. 如果需要一个可以改变的字符串，我们可以使用StringBuffer或者StringBuilder
3. 每次 new 一个字符串就是产生一个新的对象，即便两个字符串的内容相同，使用 ”==” 比较时也为 ”false” ,如果只需比较内容是否相同，应使用 ”equals()” 方法
4. 当多个变量指向同一个字符串,imooc为常量字符串，多次出现时会被编译器优化，只创建一个对象
5. 在需要频繁对字符串进行修改操作时使用 StringBuilder 的效率比 String 要高
```
String s1 = "imooc";
String s2 = "imooc";
```

## StringBuilder与
StringBuffer 是线程安全的，而 StringBuilder 则没有实现线程安全功能
```
StringBuilder hobby=new StringBuilder("爱慕课");        
System.out.println(hobby);
```
|方法|说明|
|---|---|
|`Stringbuilder append(参数)`| 追加内容到末尾|
|`Stringbuilder insert(位置，参数)`| 将内容插入到对象到指定位置|
|`String toString()`| 将对象转为String 对象|
|`Int  length()`| 获取字符串长度|