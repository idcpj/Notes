[TOC]

## 基础

1. 声明数组
```java
int[] scores;    //整数数组
int scores[];    //整数数组
double height[];  //浮点数数组
String[] names;  //字符串数组
```

2. 分配空间
```java
scores = new int[5]
height = new double[5];
names = new Stringp[5];
```

3. 在声明数组的同时为它分配空间
```java
int[] scores = new int[5];
```
4. 直接创建数组
```java
int[] scores = {78,91,83,68};
int score[] = new int[] { 34, 90, 87, 54, 24 };
```
5. 赋值
```java
scores[0]=89;
scores[1]=90;
```
## Arrays 类
```java
import java.util.Arrays; //引入

String[] hobbies = { "sports", "game", "movie" };
Arrays.sort(hobbies);
Arrays.toString(hobbies); //[game, movie, sports]
```
## foreach 方法
```java
int[] scores = {56,23,89,45};
sum=0;
for (int score : scores){
	System.out.println(score);
    System.out.println("数组索引"+sum);
    sum++;
}
```

## 二维数组
```java
//声明2行3列的二维数组
int[][] num = new int[2][3];       

//声明并赋值
String[][]      names={{"tom","jack","mike"},{"zhangsan","lisi","wangwu"}};

取值
names[1][2];
```