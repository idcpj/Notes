
[TOC]


> [参考一-纯js操作](http://www.cnblogs.com/chris-shao/archive/2012/12/27/2835986.html)
> [参考二返回jsonp](https://blog.csdn.net/hedong37518585/article/details/6591762)


## 纯js 原理
1.`1.html`  登录需要获取cookie 的网址,在其中嵌入`iframe`
```
<body>
<!--需要去拿cookie的网站-->
<iframe src='http://192.168.0.111:81/2.html' width='0' height='0' style="border-width: 0">
</iframe>
<textarea id="sogou_cookie">
</textarea>
</body>
```

2. `2.html` 跳转到A页面的3.html
```
<body>
<script>
    window.location="http://192.168.0.70:8000/3.html?"+document.cookie;
</script>
</body>
```
3. 在`3.html`中 设置cookie值
```
<body>
<script>
    //展示获取到的cookie 值
    let param = window.location.toString().indexOf("?");

    let paramStr = window.location.toString().substring(param+1);
    window.parent.document.getElementById("sogou_cookie").value= paramStr;
	//todo 清空原cookie

    //保存获取的cookie
    paramArr = paramStr.split(';%20');
    for (var i=0;i<paramArr.length;i++){
        document.cookie=paramArr[i]
    }

</script>
</body>
```