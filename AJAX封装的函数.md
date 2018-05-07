[TOC]

## js-ajax-get
```
<a class="js-ajax-get" href="{:url('plinks/follow_chapter',['aid'=>$a['ji_no'],'nid'=>$books['id']])}">设为关注章节</a>

$(document).ready(function(){

//无弹框
    $('a.js-ajax-get').click(function(event){
        event.preventDefault();
        var url = $(this).attr('href');
        console.log(url);
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

$(document).ready(function(){

   $('a.js-ajax-get-dialog').click(function(event){
        if (confirm("确认操作吗?")) {
            event.preventDefault();
            var url = $(this).attr('href');
            console.log(url);
            $.getJSON(url,function(res){
                if (res.code == 1) {
                    alert("设置成功！");
                    window.location.reload();
                }
            });
        }
    });

})
```


