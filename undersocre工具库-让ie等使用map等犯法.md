[TOC]
> [undersocre官网](http://www.bootcss.com/p/underscore/)
> [undersocre.min.js 文件](https://underscorejs.org/underscore-min.js)
> [lodash 新](https://lodash.com/docs/4.17.11)
## 优点
让低版本浏览器支持 js 的高级函数
Array有map()和filter()方法，可是Object没有这些方法。

## 简单实例
```
/js 原生
var a1 = [1, 4, 9, 16];
var a2 = a1.map(Math.sqrt); // [1, 2, 3, 4]

 //underscore 写法
_.map([1, 2, 3], (x) => x * x); // [1, 4, 9]
```
## 数组与对象常用方法
### map/filter
```
var obj = {
    name: 'bob',
    school: 'No.1 middle school',
};

//如果对象只处理 value, 且返回是数组
var upper = _.map(obj, function (value,key) {
    return value+"2";  
});//["bob2","No.1 middle school2"]

//处理对象,且返回对象, 但也只能处理value
var upper = _.mapObject(obj, function (value,key) {
    return value+"2";  
});//{"name":"bob2","school":"No.1 middle school2"}
```
### every / some
```
// 满足所有条件返回 true 所有元素都大于0？
_.every([1, 4, 7, -3, -9], (x) => x > 0); // false
// 有一个满足 至少一个元素大于0？
_.some([1, 4, 7, -3, -9], (x) => x > 0); // true
```

### max / min
获取最大/最小的值
```
var arr = [3, 5, 7, 9];
_.max(arr); // 9
_.min(arr); // 3
```
### groupBy - 按条件分组
```
var scores = [20, 81, 75, 40, 91, 59, 77, 66, 72, 88, 99];
var groups = _.groupBy(scores, function (x) {
    if (x < 60) {
        return 'C';
    } else if (x < 80) {
        return 'B';
    } else {
        return 'A';
    }
});
// 结果:
// {
//   A: [81, 91, 88, 99],
//   B: [75, 77, 66, 72],
//   C: [20, 40, 59]
// }
```
## findWhere  通过key:value查找 数组的某个对象
```
var publicServicePulitzers=[
    {name:"a",newsroom: "a"},
    {name:"b",newsroom: "b"},
    {name:"c",newsroom: "c"},
]
var a  =_.findWhere(publicServicePulitzers, {newsroom: "b"});
```

## Arrays 常用函数
### first / last
```
var arr = [2, 4, 6, 8];
_.first(arr); // 2
_.last(arr); // 8
```
### flatten
```
_.flatten([1, [2], [3, [[4], [5]]]]); // [1, 2, 3, 4, 5]  
```
### zip / unzip  两个数组合并为`[[],[],...]`的数组

```
//zip
var names = ['Adam', 'Lisa', 'Bart'];
var scores = [85, 92, 59];
_.zip(names, scores);
// [['Adam', 85], ['Lisa', 92], ['Bart', 59]]

//unzip
var namesAndScores = [['Adam', 85], ['Lisa', 92], ['Bart', 59]];
_.unzip(namesAndScores);
// [['Adam', 'Lisa', 'Bart'], [85, 92, 59]]
```
### object  两个数组合并为key-value 的对象
```
var names = ['Adam', 'Lisa', 'Bart'];
var scores = [85, 92, 59];
_.object(names, scores);
// {Adam: 85, Lisa: 92, Bart: 59}
```
### range  按开始,结束,间隔的参数 生成数组
```
// 从0开始小于10:
_.range(10); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

// 从1开始小于11：
_.range(1, 11); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// 从0开始小于30，步长5:
_.range(0, 30, 5); // [0, 5, 10, 15, 20, 25]

// 从0开始大于-10，步长-1:
_.range(0, -10, -1); // [0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
```
## Chaining
```
var r = _.chain([1, 4, 9, 16, 25])
         .map(Math.sqrt)
         .filter(x => x % 2 === 1)
         .value();//知道调用vlaue()  才返回值
```
