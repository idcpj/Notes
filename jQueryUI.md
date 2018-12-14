[TOC]
>  [参考网址](http://www.runoob.com/jqueryui/jqueryui-tutorial.html)

## 安装
```
<link rel="stylesheet" href="//apps.bdimg.com/libs/jqueryui/1.10.4/css/jquery-ui.min.css">

<script src="//apps.bdimg.com/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="//apps.bdimg.com/libs/jqueryui/1.10.4/jquery-ui.min.js"></script>
```

## 特效
出发特效的方式
```
.effect()  //只是做出效果,在元素已经显示时时用
.hide()  
.show()
.toggle()  //切换元素时使用
```

###  .addClass() 特效
```
.addClass( className [, duration ] [, easing ] [, complete ] )
-duration  执行时间
-easing  参数 查看网址 http://www.runoob.com/jqueryui/api-easings.html
-complete  完成后的回调
```

```
//style
.big-blue {
    width: 200px;
    height: 200px;
    background-color: rgb(255, 217, 0);
}
//添加class
$(".foo").addClass( "big-blue", 1000, "easeInOutBounce" );
```
给foo 添加 big-blue类

### .removeClass() 特效
`.removeClass( className [, duration ] [, easing ] [, complete ] )`
```
$( this ).removeClass( "big-blue", 1000, "easeInBack" );
```

### .effect()
```
.effect( effect [, options ] [, duration ] [, complete ] )
- effect	    一个字符串，指示要使用哪一种特效。	
- options	    特效具体的设置和 easing。	
- duration		一个字符串或一个数字，指定动画将运行多久。
- complete	    一旦动画完成时要调用的函数。
```
demo
```
$( "div" ).effect( "bounce", "easeInOutBack" );
```
### 其他特效
1. 百叶窗特效
`$( "#toggle" ).toggle( "blind" );`
2. 反弹特效
`$( "#toggle" ).toggle( "bounce", { times: 3 }, "slow" );`  //time 表示次数
3. 剪辑特效
` $( "#toggle" ).toggle( "clip",{direction:"vertical"} );`
4. 颜色动画
```
$(".toggle").animate({
    backgroundColor: "rgb( 20, 20, 20 )",
    borderTopColor:"rgb(23,23,23,0.8)",
});
```
5. 降落特效
`$(".demo").toggle("drop",{direction:"up"})`
6. 爆炸特效
` $(".demo").toggle("explode",[{pieces:100}])`   //pieces 炸裂的碎片数
7. 淡入淡出特效
`$(".demo").toggle("fade")`
8. 折叠特效
`$(".demo").toggle("fold",[{size:100,horizFirst:false}])`//size:折叠的大小,horizFirst:是否进行水平折叠
9. 隐藏
```
.hide( effect [, options ] [, duration ] [, complete ] )
```
```
  $( "div" ).hide( "drop", { direction: "down" }, "slow" );
```
10. 膨胀特效
`$(".demo").toggle("puff",{percent:110})`
11. 缩放特效
```
$( "#toggle" ).toggle( "scale" );
$(".demo").toggle("scale",[{direction:"vertical",percent:200}])
```
12. 震动特效
```

```



