[TOC]

> 主要流程配置 [参考网站](https://www.jianshu.com/p/7de00c73a2bb)
> 参考配置网站[知乎](https://zhuanlan.zhihu.com/mactalk/19556676)
>  zsh[主题预览](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes#agnoster)
>  开源项目[github-oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)


## 前期
1. 首先下载 iTerm 2
2. 打开iTerm 2
3.  输入下面指令安装oh-my-zsh
`curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh`
4. 接下来安装Powerline
`pip install powerline-status`
5. 下载、安装库字体库
`git clone https://github.com/powerline/fonts`
运行
`./install.sh`
6. iTerm 2->Profile->都设置成 Powerline的字体
推荐字体`Roboto mono medium for powe` 类型 中黑
7. 安装配色方案
    [下载](https://github.com/altercation/solarized)    进入刚刚下载的工程的`solarized/iterm2-colors-solarized `下双击 `Solarized Dark.itermcolors` 和 `Solarized Light.itermcolors`
	`profiles`->`Colors`->选择对应配色

7. 设置agnoster 主题
	进入`~/.zshrc`将`ZSH_THEME="agnoster"`
    路径前缀过长: 在`~/.oh-my-zsh/themes/agnoster.zsh-theme`文件，将里面的build_prompt下的prompt_context字段在前面加#注释掉即可。
    
    
## 插件配置
在`~/.zshrc`
```
plugins=(  git autojump osx)
```
**git**
例如 `gco=’git checkout’、gd=’git diff’、gst=’git status’、g=’git’`等等，命令内容可以参考`~/.oh-my-zsh/plugins/git/git.plugin.zsh`

**os**
tab 增强

**autojump**
`brew install autojump`

## 使用技巧
2. 强大的历史纪录功能:输入cd 用上下箭头可以翻阅你执行的所有 cd 命令
3. 能拼写纠正` cd document` ->` cd Document`
4. 各种补全：路径补全、命令补全，命令参数补全，插件内容补全等等。
	补全项可以使用 ctrl+n/p/f/b上下左右切换。
    输入 `kill java + tab`键，如果有多个则会出现选择项供你选择。
    `ssh + 空格 + 两个tab`键，列出所有访问过的主机和用户名进行补全
5. 智能跳转，安装了autojump之后，zsh 会自动记录你访问过的目录，
	输入`j Doc [+tab]` 即可。`j –s` 可以看你的历史路径库。
6. 目录浏览和跳转：输入 `d`，列出访问的目录列表，输入列表前的序号，即可直接跳转。
7. 通配符搜索：`ls -l **/*.sh，可以递归显示当前目录下的.sh文件，

## 别名设置
`~/.zshrc`
```
alias cls='clear'
alias ll='ls -l'
alias la='ls -la'
alias vi='vim'
alias h='history'
alias grep="grep --color=auto"
alias -s gz='tar -xzvf'     #自动解压后缀为 gz 的压缩包
alias -s tgz='tar -xzvf'
alias -s zip='unzip'
alias -s bz2='tar -xjvf'
alias -s html=sub   # xx.html在 sublimt 中打开,前提是设置了sub 命令
alias -s rb=sub     # 在命令行直接输入 ruby 文件，会在 TextMate 中打开
alias -s py=sub       # 在命令行直接输入 python 文件，会用 vim 中打开，以下类似
alias -s js=sub
alias -s php=sub
alias -s css=sub
alias -s php=sub
alias -s c=vi
alias -s java=vi
alias -s txt=vi
```