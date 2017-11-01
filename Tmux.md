[TOC]

## 在Bash命令行的命令

`tmux ls`											列出所有未退出的session
`tmux attach -t session_name`			打开session
`tmux new -s my-session-name`		创建session
`tmux new -s my-session-name -d`		创建一个后台session
`tmux kill-server`				删除错误

## 窗格
`Ctrl+b %`  		垂直窗格
`Ctrl+b "` 			水平窗格

## 窗口

`Ctrl+b c` 	 										在session回话中,新建窗口
`Ctrl+b 数字，Ctrl+B 方向键`			切换窗口

## 回话
`Ctrl+b s，按 q 返回`			获取会话列表
`Ctrl+b D（在开启了多个会话的时候使用）`		脱离当前会话
`Ctrl+b d`				暂时脱离当前会话
`Ctrl+b z`					挂起当前会话
`Ctrl+b $`				重命名当前会话


# 配置文件

`touch ~/.tmux.conf`  如果不存在则创建

```
# Send prefix
#把prefix的ctrl+b变为了ctrl+a

set-option -g prefix C-a
unbind-key C-a
bind-key C-a send-prefix

# Use Alt-arrow keys to switch panes
#不用按prefix，直接用alt+箭头在pane之间switch
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Shift arrow to switch windows
#不用按prefix，直接用shift+箭头在window之间switch。
bind -n S-Left previous-window
bind -n S-Right next-window

# Mouse mode
#开启鼠标模式。用鼠标就能切换window，pane，还能调整pane的大小
set -g mouse on


# Set easier window split keys
#这一部分是用来更方便切分pane的。prefix + v 代表竖着切，prefix + h 代表横着切
bind-key v split-window -h
bind-key h split-window -v

# Easy config reload
#下一次如果修改了.tmux.conf的设置的话，不用关掉tmux。直接用prefix+r,
bind-key r source-file ~/.tmux.conf \; display-message "tmux.conf reloaded"

```