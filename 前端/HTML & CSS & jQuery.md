[TOC]

## form表单ajax 提交
```js
$(".ajax_form").submit(function(e){
        e.preventDefault();
        var data = $(this).serializeArray()
        var url = $(this).attr('action');

        $.post(url,data,function(result){
            if (result.code == 200){
                alert(result.message);
            }else{
                alert(result.message);
            }
        },'JSON');

    });
```

## 设置select 的默认值  
只需要在select 属性添加`default `属性即可
```
<form action="./" method="get">

<select name="type"  default="{$_GET['type']}">
    <option value="1">11</option>
    <option value="2">22</option>
    <option value="3">333</option>
</select>

<input type="submit" value="提交">
</form>

<script>
$(function(){
    // 调整默认选择内容
    $("select").each(function(index, element) {
        $(element).find("option[value='"+$(this).attr('default')+"']").attr('selected','selected');
    });
});
</script>

```

## js-ajax-get
```
<a class="js-ajax-get" href="{:url('plinks/follow_chapter',['aid'=>$a['ji_no'],'nid'=>$books['id']])}">设为关注章节</a>

$(document).ready(function(){

//无弹框
    $('a.js-ajax-get').click(function(event){
        event.preventDefault();
        var url = $(this).attr('href');
        $.getJSON(url,function(res){
            if (res.code == 1) {
                alert("设置成功！");
                window.location.reload();
            }
        });
    });


})
```

## js-ajax-get-dialog  - 异步前弹出对话框
```
<a class="js-ajax-get-dialog" href="{:url('plinks/follow_chapter',['aid'=>$a['ji_no'],'nid'=>$books['id']])}">设为关注章节</a>


$('a.js-ajax-get-dialog').click(function(event){
    event.preventDefault();
    if (confirm("确认操作吗?")) {
        event.preventDefault();
        var url = $(this).attr('href');
        $.getJSON(url,function(res){
            if (res.code == 1) {
                alert("设置成功！");
                window.location.reload();
            }
        });
    }
});

```



## js循环输出内容
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


## 原生点击提示信息
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
