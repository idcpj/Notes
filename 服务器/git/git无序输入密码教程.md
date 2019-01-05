[TOC]

> [参考网站](https://segmentfault.com/a/1190000008435592)


## 方法一:手动创建

在你的用户目录下新建一个文本文件.git-credentials
```
Windows：C:/Users/username
Mac OS X： /Users/username
Linux： /home/username
```
文件内容
```
https:{username}:{password}@github.com
{username}和{password}是你的github的账号和密码
```
修改git配置
执行命令：

`git config --global credential.helper store`
上述命令会在.gitconfig文件(.gitconfig与.git-credentials在同目录下)末尾添加如下配置:

经过上述三步配置之后, 你push代码到github时, 便无需再输入用户名密码了

## 方法二手动配置(推荐)
在命令行输入命令:

`git config --global credential.helper store`

这一步会在用户目录下的.gitconfig文件最后添加：
```
[credential]
    helper = store
```
只需要在第一次push 时输入密码即可