[TOC]

## 安装vim
`brew install vim`

`~/.vimrc` ,如果没有，就自己创建一个
```
" 显示行号
set number
" 显示标尺
set ruler
" 历史纪录
set history=1000
" 输入的命令显示出来，看的清楚些
set showcmd
" 状态行显示的内容
set statusline=%F%m%r%h%w\ [FORMAT=%{&ff}]\ [TYPE=%Y]\ [POS=%l,%v][%p%%]\ %{strftime(\"%d/%m/%y\ -\ %H:%M\")}
" 启动显示状态行1，总是显示状态行2
set laststatus=2
" 语法高亮显示
syntax on
set fileencodings=utf-8,gb2312,gbk,cp936,latin-1
set fileencoding=utf-8
set termencoding=utf-8
set fileformat=unix
set encoding=utf-8
" 配色方案
colorscheme desert
" 指定配色方案是256色
set t_Co=256

set wildmenu
" 去掉有关vi一致性模式，避免以前版本的一些bug和局限，解决backspace不能使用的问题
set nocompatible
set backspace=indent,eol,start
set backspace=2

" 启用自动对齐功能，把上一行的对齐格式应用到下一行
set autoindent

" 依据上面的格式，智能的选择对齐方式，对于类似C语言编写很有用处
set smartindent

" vim禁用自动备份
set nobackup
set nowritebackup
set noswapfile

" 用空格代替tab
set expandtab

" 设置显示制表符的空格字符个数,改进tab缩进值，默认为8，现改为4
set tabstop=4

" 统一缩进为4，方便在开启了et后使用退格(backspace)键，每次退格将删除X个空格
set softtabstop=4

" 设定自动缩进为4个字符，程序中自动缩进所使用的空白长度
set shiftwidth=4

" 设置帮助文件为中文(需要安装vimcdoc文档)
set helplang=cn

" 显示匹配的括号
set showmatch

" 文件缩进及tab个数
au FileType html,python,vim,javascript setl shiftwidth=4
au FileType html,python,vim,javascript setl tabstop=4
au FileType java,php setl shiftwidth=4
au FileType java,php setl tabstop=4
" 高亮搜索的字符串
set hlsearch

" 检测文件的类型
filetype off
filetype plugin on
filetype indent on

" C风格缩进
set cindent
set completeopt=longest,menu

" 功能设置

" 去掉输入错误提示声音
set noeb
" 自动保存
set autowrite
" 突出显示当前行 
" set cursorline

"设置光标样式为竖线vertical bar
 "Change cursor shape between insert and normal mode in iTerm2.app
"if $TERM_PROGRAM =~ "iTerm"
let &t_SI = "\<Esc>]50;CursorShape=1\x7" " Vertical bar in insert mode
let &t_EI = "\<Esc>]50;CursorShape=0\x7" " Block in normal mode
"endif
" 共享剪贴板
set clipboard+=unnamed
" 文件被改动时自动载入
set autoread
" 顶部底部保持3行距离
set scrolloff=3

```
插件安装和配置
`git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
`
```
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
Plugin 'gmarik/Vundle.vim'
" Plugin 'tpope/vim-surround'
" Plugin 'scrooloose/nerdtree'
Plugin 'Lokaltog/vim-powerline'
Plugin 'valloric/youcompleteme'
Plugin 'yggdroot/indentline'
Plugin 'jiangmiao/auto-pairs
call vundle#end()
filetype plugin indent on

```

## YouCompleteMe 代码提示插件

`brew install macvim`
在当前shell中 如：“.zshrc”
`alias vim='mvim -v'`
1. 在 .vimrc 中添加如下内容。位置在 call vundle#begin() 和 call vundle#end() 之间。
`Bundle 'Valloric/YouCompleteMe'`
2. 安装YouCompleteMe
`brew install CMake`
3. 在vim中使用`:BundleInstall`
4. 编译YouCompleteMe，可选择哪些语言代码不全
```
cd ~/.vim/bundle/YouCompleteMe
./install.py --help
./install.py --all    #安装全部
```

