[TOC]

## css 部分


## js 部分
### 拟态框
只保持`data-target`的值与Model中Id 值一致即可
通过给 `modal-dialog`  加后缀,` modal-lg`
```css
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
  Launch demo modal
</button>

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
  <div class="modal-dialog modal-lg" role="document">
   
  </div>
</div>
```
