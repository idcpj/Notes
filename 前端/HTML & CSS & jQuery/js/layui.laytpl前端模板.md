[TOC]

> [手册](https://www.layui.com/doc/modules/laytpl.html)

## demo

```
//引入js
<script src="layui/layui.js"></script>

<div id="view">
    <script id="demo" type="text/html">
        <h3>{{ d.title }}</h3>
        <ul>
            {{#  layui.each(d.list, function(index, item){ }}
            <li>
                <span>{{ item.modname }}</span>
                <span>{{ item.alias }}：</span>
                <span>{{ item.site || '' }}</span>
            </li>
            {{#  }); }}
            {{#  if(d.list.length === 0){ }}
            无数据
            {{#  } }}
        </ul>
    </script>
</div>
<script>
    layui.use('laytpl',function(){
        var data = { //数据
            "title":"Layui常用模块"
            ,"list":[{"modname":"弹层","alias":"layer","site":"layer.layui.com"},{"modname":"表单","alias":"form"}]
        }
        var domId= "#demo";
        var domView = "#view";

        var laytpl = layui.laytpl
        //第三步：渲染模版
        var getTpl = document.querySelector(domId).innerHTML
            , view = document.querySelector(domView);
        laytpl(getTpl).render(data, function (html) {
            view.innerHTML = html;
        });
    });
</script>
```