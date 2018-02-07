[TOC]

## 技巧
1. 在同一个包中,类可以直接调用


## 构造方法
构造方法与类名相同,且没有返回值
```java
//Main.java 文件
public class Main {
    public static void main(String[] args) {
        UserForMe demo = new UserForMe("cpj");  //userforme:cpj
    }
}

//UserForMe.java
public class UserForMe {
    public UserForMe(String names){
        System.out.println("userforme:"+names);
    }
}

```