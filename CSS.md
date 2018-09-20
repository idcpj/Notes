[TOC]


## 水平居中
 **图片垂直据居中**
        是通过给父元素设置` text-align:center`
        
 **定宽元素居中**
        `margin:0 auto;`
        
 **不定宽元素居中**
     `display:table;margin:0 auto;`

## 垂直居中
**文字或内敛元素垂直居中**
   ` height`与`line-height`高度相同且 `overflow: hidden;`
    
 **几个标签的垂直居中**
`.class1,class2,class3{vertical-align:midde}`

## 水平垂直居中
```css
.demo{
	position: absolute;
    top: 50%;
    left:50%;
    transform:translate(-50%,-50%)
}
```

## 类的命名技巧
具体的物品_item
物品中的图片_item_img
物品中的文字_item_text
用xx_box 里面放置左右浮动

##  inline-block 等顶部对齐
`vertical-align:top`

## 产生空白间隙的原因
eg:
```
<span></span>
<span></span>
```
两个 `span` 进行换行的话,就会产生空白间隙
处理方法两个
1. 在span 的父级写`font-size:0`
2. 取消回车`<span></span><span></span>`

## `box-sizing`更改用于计算元素宽度和高度的默认的 CSS 盒子模型
```
box-sizing: content-box;
box-sizing: border-box;
```
> `content-box`(默认值): `width` 与 `height` 只会应用到这个元素的内容区`border` 或 `padding`不再 `width`中
> `border-box`: width = border + padding + 内容的  width，

在响应式布局中,推荐使用`border-box`

## 元素硬件加速
给元素添加
```
.demo{
	translate3D(0,0,0,)
}
```

##  长宽相等的 div
如合适一个长宽相等的一个.用于显示如图片等信息
```
width:100%
height:0
padding-top:100%
```
> 原理: 把高度设置为0 用 `padding-top:100%` 100%所代表的是宽度的大小

demo:
```
.image-header
    position:relative
    width:100%
    height:0
    padding-top:100%
    img
        position:absolute
        top:0
        left:0
        width:100%
        height:100%
```
## media
~~~css
//页面大于960px 像素
@media screen and (min-width:960px){ 
    body{background:orange;}
}

//大于960px小于1200px
@media screen and (min-width:960px) and (max-width:1200px){
    body{background:yellow;}
}
~~~

## 固定标签的宽高
即离最顶部有距离的 div, 如标签分页等
```
position:absolute
top:174px
bottom:0
left:0
width:100%
overflow:hidden
```

