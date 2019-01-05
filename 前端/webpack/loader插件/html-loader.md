[TOC]
> [手册](https://webpack.docschina.org/loaders/html-loader/)

默认情况下，每个本地的 `<img src="image.png"> `都需要通过 `require `（require('./image.png')）`来进行加载。你可能需要在配置中为图片指定 `loader`（推荐 `file-loader` 或 `url-loader` ）

你可以通过查询参数 attrs，来指定哪个标签属性组合(tag-attribute combination)应该被此 loader 处理。传递数组或以空格分隔的` <tag>:<attribute> `组合的列表。（默认值：`attrs=img:src`）