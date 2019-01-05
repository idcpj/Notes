[TOC]

> [官网手册](http://lesscss.org/)

## phpstorm 支持 less
> [https://plugins.jetbrains.com/plugin/7059-less-css-compiler](https://plugins.jetbrains.com/plugin/7059-less-css-compiler)
>  下载并导入 phpstrom

在`首选项/LESSProfiles` 中配置 less 的源码路径 与 css 的输出路径

## 注释
在`less`中
`/**/` 注释可再编译后保留在 css
`//` 编译后不保留在 css -推荐

## 导入
```
@import 'ku'  //导入 ku.less 文件
@import (less)'a.css';  //直接把 a.css 合并到 目标文件, 且在合并在导入的位置:如import 写在60行,则把 css 从60行开始插入

```
## 变量
```
@font-width:22px;

p{
  font-size: @font-width;
}
.content{
	@font-width:23px;
	.title{
    	font-width:@font-width;
    }
}
```

## 混合
### 不参数
```
p{
   font-size: @font-with;
   .red
 }

.red{
  color: red;
  border:solid 1px slateblue;
}

//outpt css
p {
  font-size: 22px;
  color: red;
  border: solid 1px slateblue;
}
.red {
  color: red;
  border: solid 1px slateblue;
}
```
### 传参
```
.border_02(@border_width){
  border: solid @border_width seagreen;
}
.test_border{
  .border_02(300px);
}

//output css
.test_border {
  border: solid 300px #2e8b57;
}

```
### 默认参数
```
.border_02(@border_width:30px){
  border: solid @border_width seagreen;
}
.test_border{
  .border_02();
}

//output css
.test_border {
  border: solid 30px #2e8b57;
}
```
## 匹配模式
```
.class_1(left){
  border-left:solid 2px red;
}
.class_1(right){
  border-right:solid 2px red;
}

.clss{
  .class_1(right);
}
```
## 运算
```
@dwidth:200px;
.demo{
  width: @dwidth+20*2; //240px
}
```
## 嵌套
1. 普通嵌套
```
.list{
  width:60px;
  height:60px;
  li{
    height:30px;
    line-height: 30px;
    span{
      font-size:12px;
    }
  }
  a{
    float: right;
  }
}
```
2. & 上层选择器
```
a {
  padding:3px;
  &:hover{  //上层选择器
    color: red;
  }
}

//output css
a:hover {
  color: red;
}
```

## @arguments
```
.demo1(@p:1px,@c:red,@l:solid){  //必须要有默认值
  border:@arguments; //等价于 @p @c @l  
}
```
## 避免编译
```
.demo{
  width:~'calc(300px-30px)'; //~'xxx' 中的内容原样输出
}
```


### 技巧
1. 生成三角形
```

.triangle(buttom,@w:5px,@c:#ccc){
  border-width:@w;
  border-color: @c transparent transparent;
  border-style: solid dashed  dashed ;
}
.triangle(left,@w:5px,@c:#ccc){
  border-width:@w;
  border-color: transparent  @c transparent transparent;
  border-style: dashed solid dashed ;
}
.triangle(top,@w:5px,@c:#ccc){
  border-width:@w;
  border-color: transparent transparent  @c;
  border-style: dashed dashed  solid;
}
.triangle(right,@w:5px,@c:#ccc){
  border-width:@w;
  border-color: transparent transparent transparent @c;
  border-style: dashed dashed solid;
}

.triangle(@_,@w:5px,@c:#ccc){
  width:0;
  height:0;
  overflow: hidden;
}

.sanjiao{
  .triangle(right,5px,red);
}
```

2.  类名简写
```
<div class="item">
    <li class="item_title"></li>
</div>

.tiem{
	&_title{  //就是 item_title
    }
}

```