[TOC]

## Promise
### 简单实例
```
// ajax函数将返回Promise对象:
function ajax(method, url, data) {
    var request = new XMLHttpRequest();
    return new Promise(function (resolve, reject) {
        request.onreadystatechange = function () {
            if (request.readyState === 4) {
                if (request.status === 200) {
                    resolve(request.responseText);
                } else {
                    reject(request.status);
                }
            }
        };
        request.open(method, url);
        request.send(data);
    });
}

//执行
var p = ajax('GET', '/api/categories');
p.then(function (text) { // 如果AJAX成功，获得响应内容
    console.log(text);
}).catch(function (status) { // 如果AJAX失败，获得响应代码
    console.log(text);
});
```
###  `Promise.all()` 与`Promise.race()`
```
var p1 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 500, 'P1');
});
var p2 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 600, 'P2');
});

// 同时执行p1和p2，并在它们都完成后执行then:
Promise.all([p1, p2]).then(function (results) {
    console.log(results); // 获得一个Array: ['P1', 'P2']
});
//只需要获得先返回的结果即可,增加容错,如同时向两个URL读取用户的个人信息
Promise.race([p1, p2]).then(function (result) {
    console.log(result); // 'P1'
});
```
## class
old:
```
function Student(name) {
    this.name = name;
}

Student.prototype.hello = function () {
    alert('Hello, ' + this.name + '!');
}
```
new:
```
class Student {
    constructor(name) {
        this.name = name;
    }

    hello() {
        alert('Hello, ' + this.name + '!');
    }
}
```
调用方式都是一样
```
var student = new Student("word");
student.hello()
```
## Map
不支持ie 10及以下
```
//初始化方式一
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
m.get('Michael'); // 95

//初始化方式二
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined
```
属性
`Set.prototype.size`
方法
```
Map.prototype.set(key, value)
Set.prototype.clear()
Set.prototype.delete(value)
Set.prototype.has(value)
```

## Set
也是一组key的集合,且没有重复的key,不支持ie 10及以下
```
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3, 3]); // 含1, 2, 3
s2.add(9)
s2.delete(3)
console.log(s2.has(1)); // 1 => true 3 =>false
for(var v of s2){
    console.log(v);//1 2 9
}
```
属性
`Set.prototype.size`
方法
```
Set.prototype.add(value)
Set.prototype.clear()
Set.prototype.delete(value)
Set.prototype.has(value)
```







