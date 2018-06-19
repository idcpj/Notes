[TOC]

> [phpstorm 配置 nodejs](/python/preview/PHPStorm/%E9%85%8D%E7%BD%AEnodejs.md)
## require、exports、module
1. require - 引入模块
```
var foo1 = require('./foo'); //js 文件可省略 js 后缀

var data = require('./data.json');  //引入json  默认带了对json的解析
```

2. exports - 导出对象的属性和方法

```
//util/counter.js
exports.count = function () {//对象方法   
    return 1+1;
};

exports.sum = function () {  
    return 2+2;
};
exports.page =12;  //对象属性

```
```
//main.js
var counter1 = require('./util/counter');

console.log(counter1.page); //调用方法
console.log(counter1.sum());//调用属性
```
3. module -  把默认的到处对象改为到处函数
```
//util/counter.js

module.exports = function () {
    console.log('Hello World!');
};
```
```
// main.js
var Hello = require('./util/counter');
console.log(Hello());
```

## 操作文件
1. 小文件操作
```
//main.js
var fs = require('fs');

function copy(src, dst) {
    fs.writeFileSync(dst, fs.readFileSync(src));
}

function main(argv) {
    copy(argv[0], argv[1]);
}

main(process.argv.slice(2));
```
```
# 把package-lock.json 复制到 同级目录并改为package-lock.json.back	
> node main.js  package-lock.json package-lock.json.back
```
2. 大文件操作
```
var fs = require('fs');

function copy(src, dst) {
    fs.createReadStream(src).pipe(fs.createWriteStream(dst));
}

function main(argv) {
    copy(argv[0], argv[1]);
}

main(process.argv.slice(2));
```