[TOC]
> [参考代码](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html)
## 原始demo1
```
var cookie ={
    name:'acas',
    setCookie:function () {
        alert("asd");
    }
}
alert(cookie.name)
alert(cookie.setCookie)
```

### demo2
缺点:浪费内存
```
 function Cat(name,color){
    this.name=name;
    this.color=color;
    this.func = function (param) {
        alert(this.name+param);
    }
}
var cat1 = new Cat('asd1',"aaa");
cat1.func("haha")
```
## 通过原型链 
```
 function Cat(name,color){
    this.name=name;
    this.color=color;
}

Cat.prototype.func=function (parma) {
    alert(this.name+parma);
}

//实例化调用
var cat1 = new Cat('asd1',"aaa");
cat1.func("haha")

//不实例化,直接调用
Cat.prototype.func("asd")
```

## 构造函数的继承
方法一:构造函数绑定
```
function Animal(){
    this.species = "动物";
}
function Cat(name,color){
    Animal.apply(this, arguments);
    this.name = name;
    this.color = color;
}

//实例化调用
var cat1 = new Cat('asd1',"aaa");
alert(cat1.species);
```
方法二: prototype模式
```
 function Animal(){
    this.species = "动物";
}

function Cat(name,color){
    this.name = name;
    this.color = color;
}

Cat.prototype = new Animal();
var cat1 = new Cat("大毛","黄色");
alert(cat1.species); // 动物
```