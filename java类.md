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
```
public class HelloWorld {
    private String name = "爱慕课";
    
    public void show() { 
		// 定义方法内部类
		class MInner {
			int score = 83;
			public int getScore() {
				return score + 10;
			}
		}
        
        MInner mi = new MInner();
		int newScore = mi.getScore();
		System.out.println("姓名：" + name + "\n加分后的成绩：" + newScore);
	}
    
	// 测试方法内部类
	public static void main(String[] args) {
        HelloWorld  mo = new HelloWorld();
		mo.show();
	}
}
```
## final 关键字
1. 修饰变量 ->变量的值只能赋值一次,常量
2. 修饰类->该类不允许被继承
3. 修饰方法->该方法不允许被覆盖
4. 修饰属性->  二选一(类的初始化必须有值或者构造方法中赋值)

## super关键字
1. 可以调用父类的属性 `super.age`
2. 可以调用父类的方法 `super.eat()`
3. 调用子类的构造方法相当于隐式的在子类构造方法中调用``super()`
```java
public Dofg(){
	super();
    System.out.println("hello word")
}
```

## Object()类
所有类的父类
常用Object类中的方法

**toString()**
print 直接打印出是类的内存地址

**equals()  - 比较两个类的是否指向同一个内存地址**
```
Dog dog  = new Dog();
Dog dog2  = new Dog();
//返回false,因为内存地址不相同 类似dog ==dog2
if(dog.equals(dog2)){
	return true;
}else{
	return false;
}
```

## 多态
1. 引用多态
```
public static void main(String[] args){
	Animal obj1 = new Animal(); //父类的应用指向本类
    Animal obj2 = new Dog();  //父类的应用指向子类
    Dog obj3 = new Animal();  //子类应用父类错误
}
```
2. 方法多态
3. 应用类型转换
向上类型转换(隐私/自动类型转换),是小类型到大类型的转换
向下类型转换(强制类型转换),大类型到小类型
```
Dog dog = new Dog();
Animal animal = dog; // 自动类型提升,向上转换
Dog dog2 = (Dog) animal; //向下类型转换 强制类型转换

//Cat cat = (Cat) animal;  因为不存在Cat 类,所以转换失败
//可以通过 Instanceof 做判断

if ( animal instanceof Cat){
	Cat cat = (Cat) animal;
}else{
	System.out.println("无法进行类型转换");
}

//为了保证程序的安全性 类型转换时,都时候instanceof 做验证
if(animal instanceof Dog ){
	Dog dog2 = (Dog) animal; 
}else{
	//todo
}
```

## 接口
1. 普通继承
```
public class SmartPhone extends Telphone implementsIPlayGame{
	//todo
}
```
2. 匿名内部类
```
// 方法一
IPlayGame ip3 = new IPlayGame(){
	public void playGame(){
    	System.out.println("使用匿名内部类实现接口")
    }
}
ip3.playGame();

//方法二
new IPlayGame{
	public void playGame(){
    	System.out.println("使用匿名内部类实现接口");
    }
}.playGame();

```

## 包装类
例如 int、float、double、boolean、char 等。基本数据类型是不具备对象的特性的，为了让基本数据类型也具备对象的特性， Java 为每个基本数据类型都提供了一个包装类
|基本类型| 对应到包装类|
|---|---|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
|char|Charcter|
|boolean|Boolean|

如 Integer类型
两个构造方法
|构造方法|说明|
|---|---|
|`Integer (int value)`| 创建一个Integer对象，表示指定到int值|
|`Integer (String s)`|创建一个Integer对象，表示String参数所指示到int值|
```
int i =2;
Integer m = new Integer(5);
Inter n = new Integer("8");
```

