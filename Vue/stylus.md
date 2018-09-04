
[TOC]


## 使用`stylus` 编辑
> [参考文档]()
```
npm install stylus --save-dev
npm install stylus-loader --save-dev
```
在`..vue`文件中使用
```
<style scoped lang="stylus" type="stylesheet/stylus">
    #app
        .tab
            display:flex
            color:red

</style>
````
载入样式
1. 在`*.vue` 中载入
```$
<style scoped lang="stylus" type="stylesheet/stylus">
    @import "./common/stylus/maxin.styl";    /*stylus的引入语法*/
</style>
```
2. 在`*.js`中载入
```$xslt
import "./common/stylus/index.styl"
```
3. 在`*.stylus` 中载入
```$xslt
@import "./base.styl" /*.styl  可省略*/
```


## 使用`&.class`
```
    .star-48
    .star-item
        width:20px
        height:20px
        margin-right:22px
        background-size:20px 20px
        &.last-child
            margin-right:0
        &.on
            bg-image('img/star48_on')
        &.half
            bg-image('img/star48_half')
        &.off
            bg-image('img/star48_off')
```
> 加入 `&` 表示改类的同级类  如`<p class="star-item on"></p>`