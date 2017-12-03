[TOC]

## flex弹性布局

```css
.partent{
    display:flex; 
    flex-direction: row | row-reverse | column | column-reverse;
    align-items:center;//垂直居中显示
   // justify-content:center;水平显示
}


```
### 主轴属性
**flex-direction   主轴方向**
`row | row-reverse | column | column-reverse;`

**flex-wrap   换行**

`nowrap | wrap | wrap-reverse;`

**justify-content   项目在主轴的方向**
`flex-start | flex-end | center | space-between (两端对齐) | space-around(每个项目两侧的间隔相等);`

**align-items  项目在交叉轴上如何对齐**
`flex-start | flex-end | center | baseline | stretch;`
### 项目属性
**flex-grow 所占比例**
`flex-grow: <number>; /* default 0 */`

>参考阮一峰[网址](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)


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