[TOC]

## 远程筛选
```
 <div class="ui-widget">
      <label for="tags">标签：</label>
      <input id="tags" autocomplete="off" name="name">
    <input type="submit" value="提交">
  </div>
//js
$("#tags").autocomplete({
    minLength: 2, //至少 2 个字符在发送请求
    source: function (request, response) {
      var searchKey = request.term
      $.getJSON("a.php?term=" + searchKey, function (res) {
        //只有 label标签赋值才能显示
        return response($.map(res,function (item){
          return {
              label:item.user_name
            }
        }))
      })
    },
    //选择select 的操作
    select: function (event, ui) {
      var selectData =ui.item.value;
        //todo code
    }
});
```