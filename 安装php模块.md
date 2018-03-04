[TOC]

## 模块安装
1. 通过 `brew search php55-` 搜索要加载的模块
2. 通过`brew  install php55-ssh2  --with-apache`
>请注意:如果你希望以mac下的apache作为web server,编译时要加 --with-apache；如果你的web server 是 nginx这类,就需要加上 --with-fpm.

## 卸载
`brew uninstall php53` 		卸载

`brew cleanup -s` 			清除缓存以及老旧版本文件