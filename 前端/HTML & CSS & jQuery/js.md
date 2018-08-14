[TOC]

## 技巧

1. querySelector
```
document.querySelector("#root") //类似 $("#root");
```

2.  从二位数组中通过某个字段的value 找到这个数组
```
var inventory = [
    {name: 'apples', quantity: 2},
    {name: 'bananas', quantity: 0},
    {name: 'cherries', quantity: 5}
];

function findCherries(fruit) { 
    return fruit.name === 'cherries';
}

console.log(inventory.find(findCherries)); // { name: 'cherries', quantity: 5 }
```

3. 原生js 添加事件
```js
var a = document.querySelector('body')
//添加触摸事件
a.addEventListener('touchstart',()=>{console.log("asd")},false)
```