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
.toggleClass()  
.addClass()
.removeClass()
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
$(".demo").effect("shake",{direction:"up",distance:200,times:10})
```
13. 尺寸特效
```
$(".demo").effect("size",{
    to:{width:200,height:60}
},1000)
```
14. 滑动特效
`$(".demo").effect("slide",{distance:"50%",direction:"up"})`
15. 转移特效
```
//style
 .ui-effects-transfer {
    border: 1px dotted black;
  }

//js
 $(".demo").effect("transfer",{
  to:$(".demo3")
},1000)
```
## 实例
### 拖拽和放置
```
$( "#draggable" ).draggable();
$( "#droppable" ).droppable({
  drop: function() {
    alert( "dropped" );
  }
});
```
### 可调整尺寸小部件
demo
```
//style
  .ui-resizable-helper { border: 1px dotted gray; }  //给拖动的部件添加虚线

$(".demo").resizable({
          animate: true,
        aspectRatio: 16 / 9 , //保持纵横比
        containment: "#container",  //限制缩放区域
        helper: "ui-resizable-helper",  //默认 ui-resizable-helper  拖动时自动添加的类
        ghost: true,//一个半透明视觉框
})

```
选项
```
alsoResize:Selector            同步调整其他 部件
animate:Boolean                设置动画
aspectRatio:Boolean,Number     限制长宽比
autoHide:Boolean               当用户鼠标没有悬浮在元素上时是否隐藏手柄
delay:Number                   鼠标按下调整按钮的生效时间
disabled:Boolean               禁用拖拽
ghost:Boolean                  为调整尺寸显示一个半透明的辅助元素
grid:Array                     可调整尺寸元素对齐到网格，每个 x 和 y 像素。数组形式必须是 [ x, y ]
minHeight-maxHeight            设置元素的高界限
minWidth-maxWidth              设置元素的高界限
```
事件
```
create( event, ui )	当 resizable 被创建时触发。
resize( event, ui )	在调整尺寸期间当调整手柄拖拽时触发。
start( event, ui )	当调整尺寸操作开始时触发。
stop( event, ui )	当调整尺寸操作停止时触发。
```
###  鼠标选择单个元素或一组元素
获取选中的值
```
//style
  #selectable .ui-selecting { background: #FECA40; }
  #selectable .ui-selected { background: #F39814; color: white; }
  #selectable { list-style-type: none; margin: 0; padding: 0; width: 60%; }
  #selectable li { margin: 3px; padding: 0.4em; font-size: 1.4em; height: 18px; }

//js
 $("#selectable").selectable({
    stop:function(){
      //.ui-selected  选择的类
      //.ui-selecting  选择中的类的类
      var selectArr=[];
      $(this).find(".ui-selected").each(function(){
        selectArr.push($(this).html())
        console.log(selectArr); //["2", "3", "6", "7"]
      })            
    },
  })
```
### 排序
```
$(function () {
  $("#sortable").sortable({
    stop:function(){
      var  orderArr=[];
      $(this).children("li").each(function(){
        orderArr.push($(this).data("order"))
        console.log(orderArr); //[1, 3, 2, 4, 5, 7, 6]
      })
    }
  });
  $("#sortable").disableSelection();
});    
```
### 折叠面板
```
//html
<div id="accordion">
  <h3> 标题1 </h3>
  <div> 标题一内容标题一内容标题一内容标题一内容标题一内容标题一内容 </div>
  <h3> 标题2 </h3>
  <div> 标题一内容标题一内容标题一内容标题一内容标题一内容标题一内容 </div>
  <h3> 标题3 </h3>
  <div> 标题一内容标题 <br/> 一内容标题<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>一内容标题一内容标题一内容标题一内容 </div>
</div>

//js
var icons = {
    header: "ui-icon-circle-arrow-e",//关闭
    activeHeader: "ui-icon-circle-arrow-s" //打开
};

$("#accordion").accordion({
    collapsible: true, //默认false,至少有一个不折叠
    icons:icons, //图片
    heightStyle :"fill", //设置fill 则不能超过父级的高度,设置 content 则显示内容的高度
});



