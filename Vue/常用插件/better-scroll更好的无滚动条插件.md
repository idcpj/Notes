
[TOC]

> [github](https://github.com/ustbhuangyi/better-scroll/blob/master/README_zh-CN.md)

注意：如果想要滚动生效,必须父类`wrapper`元素小于子类`content`
`wrapper`或其父类 不需要有 `position:absolute;top:50px;bottom:50px`
```
<div class="wrapper" ref="menuWrapper">
  <ul class="content">
    <li>...</li>
    <li>...</li>
    ...
  </ul>
  <!-- 这里可以放一些其它的 DOM，但不会影响滚动 -->
</div>



created(){
  this.$http.get(config.apiHost.goods).then((response)=>{
    if (response.status === ERR_OK){
        this.goods = response.body
      // 由于 goods 的渲染是异步方式,所以加入 nextTick 时,使其可精确计算DOM 高度
        this.$nextTick(()=>{
          this._initScroll()
        })
    }
  })
},
methods: {
  _initScroll(){
    this.menuScroll = new BScroll(this.$refs.menuWrapper, {})
  }
}
```