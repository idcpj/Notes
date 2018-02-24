[TOC]

## 破解
[简书教程](https://www.jianshu.com/p/3c87487e7121)
[破解网站](http://idea.lanyus.com/)

## 汉化
网址 : [github](https://github.com/ewen0930/IntelliJ-IDEA-Chinese)

## 创建项目
[参考网址](http://blog.csdn.net/qq_27093465/article/details/52795186)
文件->new->java 模块->选择Project SDK（如何没有new一个新的 选择到目录即可）->create project from template

## table 技巧
|代码|效果|
|---|---|
|`main`| `public static void main(String[] args) {    }`|
|`ps`|`private String `|
|`pi`|`private int `|
|`print` |`System.out.println()`|
|`"hello word".sout`  | `System.out.println("hello word");`|
|`values.iter`|`for (String value : values) {        }`|
|`100.fori`|`for (int i = 0; i < 100; i++) { }`|


## Alt+Enter 技巧
|代码|选项|效果|
|---|---|
|`System.out.println("name："+name+",age："+age);`|Replace'+'with'String.format()'|`System.out.printf("name：%s,age：%d%n", name, age);`|

## 调试
### 条件断点
```
//打上断点 ，并且右键断点 在条件中输入 i==50，此时，在i50时，会进行中断
for (int i = 0; i < 100; i++) {
            System.out.println(i);
        }
```
### 配置调试
在运行/调试配置中，添加程序参数
```
public static void main(String[] args) {
    System.out.println(args[0]); //cpj
}
```
