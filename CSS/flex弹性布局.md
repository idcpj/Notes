
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
![justify-content](images/20171229_135448.jpg =200x300)

---

**align-items  项目在交叉轴上如何对齐**
`flex-start | flex-end | center | baseline | stretch;`
![align-items](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png =200x200)
### 项目属性
**flex-grow 所占比例**
`flex-grow: <number>; /* default 0 */`

>参考阮一峰[网址](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)