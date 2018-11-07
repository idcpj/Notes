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




## 设置/获取内容
```js
//设置内容
$("#test1").text("Hello world!"
$("#test2").html("<b>Hello world!</b>")
$("#test3").val("18岁")

//设置属性
$("#runoob").attr("href","www.runoob.com")
```

## 添加元素
```js
//元素内部
$("p").append("追加文本")
$("p").append("<li>asd</li>")

//在被选元素外部
$("img").after("在后面添加文本")
$("img").before("在后面添加文本")
```

## 移除元素
```
$("#div1").remove();  //移除本身
$("#div1").empty();  //不移除本身
```

## $().each与$.each
### $().each()
```
$(“input[name=’ch’]”).each(function(i){
    if($(this).attr(‘checked’)==true)
    {
        //一些操作代码
    }
}
```

### $.each()
```
情况一:一位数组
        var arr1 = [ “one”, “two”, “three”, “four”, “five” ];
        $.each(arr1, function(){
            alert(this);
        });
        //输出：one   two  three  four   five

情况二;二维数组
        var arr2 = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
        $.each(arr2, function(i, item){
            alert(item[0]);
        });
        //输出：1   4   7

情况三:对象
        var obj = { one:1, two:2, three:3, four:4, five:5 };
            $.each(obj, function(key, val) {
                alert(obj[key]);
            });
		//输出：1   2  3  4  5	
```
## 懒加载
```
<img src="img1" src="small.jpg" data-realsrc='abc.png'>
<script type="text/javascript">
	var img1 = document.getElementById('img1')
	img1.src= img1.getAttribute('data-realsrc')
</script>
```
## 异步文件下载
[bh_msg_tips() 方法详情](https://www.kancloud.cn/idcpj/python/770267#_53)
```
$(".downfile").click(function () {
    //显示等待效果
    bh_msg_tips("下载中...");
    var url = $(this).data('href');
    $.getJSON(url,function (res) {
        if(res.status===0){
            alert("请求出错"+res.msg);
            return ;
        }
        var showname  =res.data.showname;
        var filename  =res.data.filename;
        var down_url = "{:U('down_file')}?showname="+showname+"&filename="+filename;
        
        var a = document.createElement('a');
//        a.download = showname;  //自定义文件名
        a.href = down_url;
        $("body").append(a);    // 修复firefox中无法触发click
        a.click();
        $(a).remove();
        
        remove_tips();//取消提示
    });

    return false;
});
```

## jquery 获取下载进度条参数
异步下载文件需要在嵌套一层异步

```js
//使用了 progressJs 插件
$.post(url,data,function(res){
 var res.info=res.downurl
     $.ajax({
        type:'GET',
        url: res.info,
        xhrFields:{
            onprogress:function(event){
                // console.log(event);
                if(event.lengthComputable){
                    // console.log(event.total);
                    // console.log(event.loaded);
                    var percent =(event.loaded/event.total)*100;
                    var percent = percent.toFixed(2);
                    progressJs().set(percent)  //按百分之5加载
                }
            }
        },
        complete: function() {
            progressJs().end()
        },
    });
},"JSON");
```
## jquery文件上传显示进度
```
 $.ajax({
    url:uploadUrl + "?flag=input",
    type: 'POST',
    cache: false,
    data: new FormData($('#form_input')[0]),
    processData: false,
    contentType: false,
    beforeSend: function(){
        progressJs().start();
    },
    success: function(result) {
        progressJs().end();

    },
    error: function (result) {
    },
    xhr: function(){
        var xhr = $.ajaxSettings.xhr();
        if(onprogress && xhr.upload) {
            xhr.upload.addEventListener("progress" , onprogress, false);
            return xhr;
        }
    }
    });
```
## 全选与全部选
```
//切换全选与全不选
$("#checkAll").click(function() {
    $('input[name="ids[]"]').prop("checked",this.checked);
});
//如果手动全不选中,则显示全选
var $subBox = $("input[name='ids[]']");
$subBox.click(function(){
    $("#checkAll").prop("checked",$subBox.length == $("input[name='ids[]']:checked").length ? true : false);
});
```
## bind() on() click() 区别
1. `click` 不支持 动态扩展的元素

2. `on`  [推荐]
可监听动态扩展的元素,通过第二个`selector`参数,但必须 其父元素不是动态添加的
```
格式:   .on(events [,selector] [,data], handler)
$('ul').on('click', 'li', function(){console.log('click');}
```
3. `bind`
`格式 .bind(events [,eventData], handler)`
缺点: 
1. 性能问题,会绑定到所有选择元素上,
2. 不会绑定到动态添加的元素上
3. 页面加载完,才能使用bind. 存在效率问题
优点:
1. 兼容性好,
2.  `.click(),.hover()` 是其简化处理结果
3. 如果使用 绑定的是`id`唯一等元素,可优先考虑`bind`

on,与bind 方法对data 参数的使用
```
 function bindClick( event ) {
        var type = event.data.type; //可在事件参数的data属性中获取
        if (type=="1") {
            alert(event.data.msg)
        }else if(type =="2"){
            alert(event.data.msg)
        }
    };
    $( "p" ).on( "click",{type:"1",msg:"hello"},bindClick );
    $( "p" ).on( "click",{type:"2",msg:"word"},bindClick );
```



