[TOC]

> [插件网站](http://www.jq22.com/jquery-info15811)


##  自定义需求
如需要增加一个字段`userid`字段
```
//在46行左右
var obj = {
    id: item.id,
    name: item.name,
    userid:item.userid  //增加userid 字段
}
//或者
var obj = item;  直接全部复制
```

```
//在span 中增加 data-userid 属性
if(item.child && item.child.length > 0) {
    lihtml += "<i ischek='true' class='" + self.mouIconOpen + "'></i>" +
        "<span id='" + item.id + "'data-userid='"+item.userid+"'>" + item.name + "</span>";  //修改
    var _ul = self.proHTML(item.child);
    lihtml += _ul + "</li>";
} else {
    lihtml += "<i class='" + self.simIcon + "'></i>" +
        "<span id='" + item.id + "'data-userid='"+item.userid+"'>" + item.name + "</span>"; //修改
}
```
```
//在100行 更改
增加 var userid = $(this).data('userid')
```

## 配置 自定义
```
$(".innerUl").ProTree({
    arr: arr,
    close: true,  //true 自动打开  false  自动打开
    simIcon: "fa fa-file-o", //单个标题字体图标 不传默认glyphicon-file
    mouIconOpen: "fa fa-folder-open-o", //含多个标题的打开字体图标  不传默认glyphicon-folder-open
    mouIconClose: "fa fa-folder-o", //含多个标题的关闭的字体图标  不传默认glyphicon-folder-close
    callback: function(id, name) {
        alert("你选择的id是" + id + "，名字是" + name);
    }
});
```

## 注意事项
1. 顶级目录 `pid`必须为0