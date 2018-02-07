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

## 方法的重载
同一个类中包含了两个以上方法名相同、方法参数的个数、顺序或类型不同的方法，则称为方法的重载
当调用被重载的方法时， Java 会根据参数的个数和类型来判断应该调用哪个重载方法，参数完全匹配的方法将被执行