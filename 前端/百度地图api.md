[TOC]

> [百度地图api](http://lbsyun.baidu.com/jsdemo.htm#c2_4)


## 添加详细信息

详情查看 查看 百度地图官网的**信息窗口示例**
```
var marker = new BMap.Marker(point);
this.map.addOverlay(marker);

var label = new BMap.Label(labelFont,{offset:new BMap.Size(20,-10)});
marker.setLabel(label);

var opts = {
    width : 50,     // 信息窗口宽度
    height: 120,     // 信息窗口高度
    title : "用户详情"  // 信息窗口标题
}

var details='';
    details+='部门:'+points[i]['dept_name']+"<br/>";
    details+='姓名:'+points[i]['user_name']+"<br/>";
    details+='手机号:'+points[i]['user_mobile']+"<br/>";
    details+='邮箱:'+points[i]['user_email']+"<br/>";
    details+='性别:'+sex+"<br/>";

var infoWindow = new BMap.InfoWindow(details, opts);  // 创建信息窗口对象

marker.addEventListener("click",function (){
   // this.map.openInfoWindow(infoWindow, this.map.getCenter());      // 打开信息窗口
    this.map.openInfoWindow(infoWindow, point);

})
```