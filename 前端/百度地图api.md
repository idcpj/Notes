[TOC]

> [百度地图api](http://lbsyun.baidu.com/jsdemo.htm#c2_4)
> [百度地图清除指定覆盖物（Overlay）的方法](https://www.jianshu.com/p/e6ab36f85b5b)
> [地图接口方法,参数说明](http://lbsyun.baidu.com/cms/jsapi/reference/jsapi_reference.html)


## 添加详细信息
详情查看 查看 百度地图官网的**信息窗口示例** ,弹出框
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

## 添加更多自定义信息
如需要添加更多人员信息,  先在一个全局添加人员数组
```
var deviceList=new Array;
deviceList.push({name:"ccc".age:'asd'})//相关人员 

//给marker 添加点击事件,
marker.addEventListener("click", function(){
    var deviceInfo = getDeviceInfo(marker.getLabel().getContent()); //通过getContent去获取name 值
    if (null == deviceInfo){
        return;
    }
    $("#userName").val(deviceInfo.name);
    $("#deptName").val(deviceInfo.deptName);
    $("#userSex").val(deviceInfo.userSex ? '男' : '女');
    $("#longitude").val(deviceInfo.point.lng);
    $("#latitude").val(deviceInfo.point.lat);
});

// 通过人名,获取设备信息
function getDeviceInfo(name){
    for (i = 0; i < deviceList.length; ++i){
        if (deviceList[i].name == name){ 
            return deviceList[i];
        }
    }
    return null;
}

```