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

//UserForMe.java  - 构造方法
public class UserForMe {
    public UserForMe(String names){
        System.out.println("userforme:"+names);
    }
}

```

## 方法的重载
同一个类中包含了两个以上方法名相同、方法参数的个数、顺序或类型不同的方法，则称为方法的重载
当调用被重载的方法时， Java 会根据参数的个数和类型来判断应该调用哪个重载方法，参数完全匹配的方法将被执行

## static 静态方法
在静态方法中,不能调用非静态的属性和方法,可通过new 个自己的类进行调用
```
// Main.java
public class Main {
    public static void main(String[] args) {
        System.out.println(UserForMe.from);  //china
        System.out.println(UserForMe.sayHello()); //hello word
        
        UserForMe user =  new UserForMe();
        System.out.println(user.sayHello()); //hello word
    }

}

//UserForMe.java
public class UserForMe {
    static String from="china";
    public static String sayHello() {
        return "hello word";
    }
}
```

## 静态初始化块
执行顺序  1.静态初始化块  -> 2.初始化块  ->构造方法
并且 静态初始化块 只在第一次实例化时,调用.
```
public class HelloWorld {
    String name; // 声明变量name
	String sex; // 声明变量sex
	static int age;// 声明静态变量age
    
    // 构造方法
	public   HelloWorld     () { 
		System.out.println("通过构造方法初始化name -3");
		name = "tom";
	}
    // 初始化块
	{ 
		System.out.println("通过初始化块初始化sex -2");
		sex = "男";
	}
    // 静态初始化块
	 static { 
		System.out.println("通过静态初始化块初始化age -1 ");
		age = 20;
	}
	public void show() {
		System.out.println("姓名：" + name + "，性别：" + sex + "，年龄：" + age);
	}
    
	public static void main(String[] args) {
        // 创建对象
		HelloWorld hello = new HelloWorld();
		// 调用对象的show方法
        hello.show();
        HelloWorld hello2 = new HelloWorld();
        
	}
}
```

## 内部类

### 调用内部类
要使用内部类,需要首先对主类进行实例化,在实例化内部类
```
//外部类HelloWorld
public class HelloWorld {
    // 内部类Inner，类Inner在类HelloWorld的内部
    public class Inner {
		// 内部类的方法
		public void show() {
			System.out.println("welcome to imooc!");
		}
	}
    
	public static void main(String[] args) {
        // 创建外部类对象
		HelloWorld hello = new HelloWorld();
        // 创建内部类对象
		Inner i = hello.new Inner();
        // 调用内部类对象的方法
		i.show();
	}
}
```
### 内部类调用外部类属性
如何具有相同属性,内部类需要加`this`,进行访问
```
public class Inner {
    String name = "爱慕课";
    //内部类中的方法
    public void show() { 
        System.out.println("外部类中的name：" +HelloWorld.this.name );
        System.out.println("内部类中的name：" +name);
        System.out.println("外部类中的age：" + age);
    }
}
```

### 静态内部类
```
public class HelloWorld {
    private static int score = 84;
    
    // 创建静态内部类
	public static class SInner {
        int score = 91;
        
		public void show() {
			System.out.println("访问外部类中的score：" +  HelloWorld.score);  //调用外部类
			System.out.println("访问内部类中的score：" + score);
		}
	}

	// 测试静态内部类
	public static void main(String[] args) {
        SInner si = new SInner();
		si.show();
	}
}
```

### 方法内部类
内部类定义在外部方法中

