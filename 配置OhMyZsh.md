[TOC]

> 主要流程配置 [参考网站](https://www.jianshu.com/p/7de00c73a2bb)
> 参考配置网站[知乎](https://zhuanlan.zhihu.com/mactalk/19556676)
>  zsh[主题预览](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes#agnoster)
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
推荐字体 `Meslo LG M dz for powerline`
## 别名设置
`~/.zshrc`
```
alias cls='clear'
alias ll='ls -l'
alias la='ls -a'
alias vi='vim'
alias grep="grep --color=auto"
alias -s gz='tar -xzvf'   
alias -s tgz='tar -xzvf'
alias -s zip='unzip'
alias -s bz2='tar -xjvf'
```