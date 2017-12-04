[TOC]

## ES6

**箭头函数**
箭头函数没有`this` 所有调用的是外层的`this`
```
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

foo.call({ id: 42 });  //id：42
```
**对象的简介写法**
```
let name='cpj'
let age = 12
{name,age} //{name: "cpj", age: 12}
```