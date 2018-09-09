[TOC]

## 技巧

### querySelector
```
document.querySelector("#root") //类似 $("#root");
```

### 从二位数组中通过某个字段的value 找到这个数组
```
var inventory = [
    {name: 'apples', quantity: 2},
    {name: 'bananas', quantity: 0},
    {name: 'cherries', quantity: 5}
];

function findCherries(fruit) { 
    return fruit.name === 'cherries';
}

console.log(inventory.find(findCherries)); // { name: 'cherries', quantity: 5 }
```

### 原生js 添加事件
```js
var a = document.querySelector('body')
//添加触摸事件
a.addEventListener('touchstart',()=>{console.log("asd")},false)
```

### 使图层调动 GPU 的加速
在css 中加入`transform`
`transform: translate3d(0,0,0)`


### js循环输出内容
```js
	var list = document.getElementById("list");         
	if(localStorage.length>0){ 
	        var result = "<table border='1'>"; 
	        result += "<tr><td>网站名</td><td>网址</td></tr>"; 
	
	        for(var i=0;i<localStorage.length;i++){ 
	                var sitename = localStorage.key(i); 
	                var siteurl = localStorage.getItem(sitename); 
	                result += "<tr><td>"+sitename+"</td><td>"+siteurl+"</td></tr>"; 
	        } 
	        result += "</table>"; 
	        list.innerHTML = result; 
}
```

### 原生点击提示信息
```
 function bh_msg_tips(msg){
    var oMask = document.createElement("div");
    oMask.id = "bh_msg_lay";
    oMask.style.position="fixed";
    oMask.style.left="0";
    oMask.style.top="50%";
    oMask.style.zIndex="100";
    oMask.style.textAlign="center";
    oMask.style.width="100%";
    oMask.innerHTML =  "<span style='background: rgba(0, 0, 0, 0.65);color: #fff;padding: 10px 15px;border-radius: 3px; font-size: 14px;'>" + msg + "</span>";
    document.body.appendChild(oMask);
    setTimeout(function(){$("#bh_msg_lay").remove();},2000);
}
```


### 滚动屏幕,自动定位相应的标签
1. 计算出每个`li` 的高度,放入 `listheight` 数组中
2. 滚动时,获取实的高度,放入 `scrollY` 中
3. 判断`this.scrollY >= height1 && this.scrollY < height2` 返回对应`listheight`中的`key` 值,通过`key` 给对应的 li 添加 选中的样式