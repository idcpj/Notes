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