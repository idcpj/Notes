[TOC]

## Collection  -数组
存储一个元素集合
Collection接口又有3种子类型，List、Set和Queue
### List-有序
[简书参考网址](https://www.jianshu.com/p/25aa92f8d681)

对于需要快速插入，删除元素，应该使用LinkedList。
对于需要快速随机访问元素，应该使用ArrayList。
对于“单线程环境” 或者 “多线程环境，但List仅仅只会被单个线程操作”，此时应该使用非同步的类(如ArrayList)。
```java
LinkedList linkedList = new LinkedList();
ArrayList arrayList = new ArrayList();
```
```
//设置Course 类
public class Course {
    public String id;
    public String name;

    public Course(String id,String name){
        this.id = id;
        this.name = name;
    }
}

public class Listtest {

    //被选课程List
    public List coursesToSelect;

    public Listtest(){
        this.coursesToSelect = new ArrayList();
    }
    public void testAdd(){
    	//单个添加
        Course cr1  = new Course("1","数据结构");
        coursesToSelect.add(cr1); //调用List  的add方法把数据放入List中
        
        Course cr2 = new Course("2","C语言");
        coursesToSelect.add(0,cr2); //把cr2 放入最前面
        
        //批量添加
        Course[] course = {new Course("3","离散数学"),new Course("4","汇编语言")};
        coursesToSelect.addAll(Arrays.asList(course));
        
        //获取coursesToSelect到某个值
        Course temp = (Course) coursesToSelect.get(3);
        System.out.println("添加课程" + temp.id + ":" + temp.name);
        
         //通过迭代器来遍历List
        Iterator it =  coursesToSelect.iterator();
        while(it.hasNext()){
            Course temp = (Course) it.next();
            System.out.println("迭代器输出的添加课程" + temp.id + ":" + temp.name);
        }
        
         //2.用foreach 遍历List
        for (Object obj :coursesToSelect){
            Course cr = (Course) obj;
            System.out.println("foreach输出的添加课程" + cr.id + ":" + cr.name);
        }
        
        //修改List的元素
        coursesToSelect.set(3,new Course("7","Php"));
        
        //比较
		//从Course 中取出的返回为true
        Course course = lists.get(0);
        System.out.println(lists.contains(course));//true
        //new 的值返回为false
        System.out.println(lists.contains(new Course("1","php")));//false ,
        //如果类型为字符串，整数等类型，则可以lists.contains("hello")
        
        
        //删除
        coursesToSelect.remove(1);
        
        //排序
        Collections.sort(coursesToSelect); //只能排字符串，整数范型 ，排列方式 0-9 -> A-Z -> a-z
        
         //批量删除
        Course[] courses = {(Course) coursesToSelect.get(0), (Course) coursesToSelect.get(3)};
        coursesToSelect.removeAll(Arrays.asList(courses));
    }
}
```


#### 范型
即“参数化类型

1. 不使用范型
```
public List coursesToSelect;
public void testAdd(){
	coursesToSelect.add("asdad");//在编辑器中不会报错
}
```
2. 使用范型
```
public class Listtest{
    public List<Course> coursesToSelect;
    //构造函数
	public Listtest(){
		//初始化coursesToSelect
    	this.coursesToSelect = new ArrayList<String>();
    }

    public void testAdd(){
        coursesToSelect.add("asdad");//在编译中报错，方便查看错误
    }
    
    public void testForEach(){
    	//由于规定了范型，所以直接转为Course类型，并输出，而不需要在转换为Course类型
    	for (Course cr : coursesToSelect){
        	System.out.println(cr.id+":"+cr.name)
        }
    }

}
```
3. 如果需要创建字符串List
```
List<String> list = new ArrayList<String>();
list.add("qqyumidi");
```
4. 范型可以添加范型的子类型的对象实例
```
public class CourseChild extends Course{
}
```
```
CourseChild cr1  = new CourseChild();
cr1.id = "6";
cr1.name="C++"；
coursesToSelect.add(cr1); //调用List  的add方法把数据放入List中
```

5. 范型集合中的限定类型不能使用基础数据类型，但是可以通过使用包装类限定允许存入的基本数据类型
```
int -> Integer
long -> Long
boolean -> Boolean
```

demo
```
List<Integer>  list= new ArrayList<Integer>();
list.add(12);

System.out.println(list.get(0));//12
```

### set 无序

1. Set集合中没有get(int index)方法，要获取元素，使用Iterator迭代器或for循环。
2. 向Set集合中添加元素 可以使用add()方法,但是是无序且不可重复。
```
Set<String> set = new HashSet<String>();
set.add("hello");
set.add("word");
set.add("!");

//Iterator 迭代器
Iterator it = set.iterator();
while(it.hasNext()){
    System.out.println(it.next());

}

//for 循环
for (String s: set) {
    System.out.println(s);
}
```


## Map - 键值对
[简书参考网址](https://www.jianshu.com/p/5f9ba40fbc4d);
```
//赋值
HashMap<Integer,String> h = new HashMap<Integer,String>();
h.put(3, "heihei");
h.put(4, "haha");
h.put(8, "xyy");

//for循环
Set<Integer> s = h.keySet();  //获取所有key
for(Integer i:s){
    System.out.println(i+","+h.get(i));
}
//java8中的lamda表达式
map.forEach((k,v)->System.out.println( k + " : " + v));

//删除
maps.remove(1);

//修改
maps.put(3,"hello word");

//是否有某个key值
maps.containsKey(3);

//是否包含某个value值
maps.containsValue("heihei")；
```

## Comparable & Comparator
使某个类可比较，如把**人**这个类按身高比较
### Comparable - 默认比较规则
1. 其实现类需实现compareTo()方法
2. compareTo() 方法返回正数表示大，负数表示小，0表示相等
```
//继承 Comparable接口，并实现compareTo()方法
public class Course implements Comparable<Course>{
    public String id;
    public String name;

    public Course(String id,String name){
        this.id = id;
        this.name = name;
    }

    @Override
    public int compareTo(Course course) {
        return this.id.compareTo(course.id);
    }
}

//调用
Course cr1 = new Course("4", "数据结构");
coursesToSelect.add(cr1); //调用List  的add方法把数据放入List中

Course cr2 = new Course("2", "C语言");
coursesToSelect.add(cr2);
        
Collections.sort(coursesToSelect); //注意字符串类型比较 1000 回在200 签名，是从第一个字符开始比较。

```

### Comparator - 临时比较规则
1. 用于定义临时比较规则，而不是默认比较规则
2. 其实现类需要实现compare()方法
```
//定义一个Comparator 类
public class CouserComparator implements Comparator<Course> {
    @Override
    public int compare(Course course, Course t1) {
        return course.id.compareTo(t1.id);
    }
}
//调用
Collections.sort(coursesToSelect,new CouserComparator());
```
