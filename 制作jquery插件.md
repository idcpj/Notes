[TOC]

## 简单dmeo
1. 无链式调用
```
$.fn.changeStyle = function(colorStr){
         this.css("color",colorStr);
}

$(".change").changeStyle("red");
```

2.  链式调用
```
$.fn.changeStyle=function(colorStr){
    this.css('color',colorStr);
    return this;
}

$(".change").changeStyle("red").addClass("bgblue"); //文字变红,且添加背景为蓝色
```

## 防止$符号污染的jQuery插件
```
(function($){
    $.fn.changeStyle = function(colorStr){
        this.css("color",colorStr);
        return this;
    }
}(jQuery));


$(".change").changeStyle("red").addClass("bgblue");
```

## 传参插件
1. 直接传参
```
(function($){
    $.fn.changeStyle = function(colorStr,fontSize){
        this.css("color",colorStr).css("fontSize",fontSize+"px");
        return this;
    }
}(jQuery));

$(".change").changeStyle("red",32);
```
2. 通过对象传值
```
(function($){
    $.fn.changeStyle = function(option){
        this.css("color",option.colorStr).css("fontSize",option.fontSize);
        return this;
    }
}(jQuery));

$(".change").changeStyle({
    colorStr:'red',
    fontSize:32,
});

```

3. 通过 `$.extend`参数设置默认值   [推荐方案]
```
(function ($) {

    $.fn.changeStyle = function (option) {
        var defaultSetting = {colorStr: "green", fontSize: 12};
        var setting = $.extend(defaultSetting, option); //合并两个对象,后面的值覆盖前面的值
        this.css("color", setting.colorStr).css("fontSize", setting.fontSize + "px");
        return this;
    }
}(jQuery));


$(".change").changeStyle({
    colorStr: 'red',
    fontSize: 32,
});
```