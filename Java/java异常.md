[TOC]

## error
1. 虚拟机错误
2. 线程死锁
一旦Error出现了，程序就彻底的挂了，被称为程序终结者；

## Exception
Exception类主要指编码、环境、用户操作输入出现问题
### 非检查异常（RuntimeException）
1. 空指针异常 
2. 数组下标越界异常
3. 类型转换异常
4. 算术异常。
程序会自动抛出该类异常

### 检查异常（其他的一些异常）
1. 文件异常 (IOExcption)
2. SQL异常  (SQLException)

## 语法
先捕获子类，在父类
finaly 会接收异常返回的return
如果在异常中没有return 值，那么执行完异常后（包括finaly异常）回继续往下执行
```
try{
	//todo
}catch(Exception e){
	//todo	
}catch(Exception2 e ){
	//todo
    result = 1
    return result;
}finaly{
	//todo
    System.out.println(result); //1
}
System.out.println("如果之前没有return，将回输出这句"); //1
```

## 异常链
在捕获一个异常之后抛出另外一个异常，并且我们希望在新的异常对象中保存原始异常对象的信息，实际上就是异常传递
在catch 捕获的异常再次抛出，即形成异常链
[简书](https://www.jianshu.com/p/8e1ffe60fbe4)