
[TOC]

## 常用命令
`:set nu`  显示行数
`yy`		复制
`dd`		剪切
`p`			黏贴
`ddp`		交换上下文
`u` 			撤销
`>>`       缩进
`Shift+zz`		即可保存退出vim
`/foo`  +`n`     搜索后按`n` 继续搜索




## 普通模式
`Esc`或者`Ctrl+[`   进入普通模式

**删除,黏贴等**

|命令|	说明|
|---|---|
|`x` 与 `X`|	向后  / 向前删除|
|`dd`	|删除整行|
|`2dd`	|重复dd两次|
|`d1G` 与`dG`	|删除到文档结尾处(首部)|
|`d0` 与  `d$`| 光标所在位置删除至行首 (行尾) |
|`p` 与  `P` | 粘贴至光标下一行 (上一行) |
|`J` |  将光标所在列与下一列合并|
|`[Ctrl]+r`| 重复前一个动作| 
|`nyy`| 复制多行 n为复制行数 ,在p 进行粘贴 |
|`ctrl+v` + `y` + `p`|  区块复制  按下`ctrl+v` 后移动移动光标选中位置,在按下`y`复制 `p`粘贴|


**行间跳转**

|命令   |说明  |
|---|---|
|  `nG(n Shift+g)` |  游标移动到第 n 行 |
|  `gg` |  游标移动到到第一行 |
|  `G(Shift+g)`|  到最后一行 |
**`Ctrl+o`返回跳转前的位置**

**行内跳转**

|命令	|说明|
|---|---|
|`H`/`L`/`M`	|页首,	中页尾	,	中间|
|`w`	|到下一个单词的开头|
|`e`	|到当前单词的结尾|
|`0`或`^`	|到行头|
|`$`|	到行尾|
|`f<字母>`|	向后搜索<字母>并跳转到第一个匹配的位置(非常实用)|
|`F<字母>`	|向前搜索<字母>并跳转到第一个匹配的位置|

**替换**

|命令|	说明|
|---|---|
|`r+<待替换字母>`|	将游标所在字母替换为指定字母|
|`R`	|连续替换，直到按下Esc|
|`cc`	|替换整行，即删除游标所在行，并进入插入模式|
|`cw`|	替换一个单词，即删除一个单词，并进入插入模式|
|`C(大写)`	|替换游标以后至行末|
|`~`|	反转游标所在字母大小写|
|`u{n}`	|撤销一次或n次操作||
|`U(大写)`	|撤销当前行的所有修改|

**查找**

|  命令  | 说明   |
| --- | --- |
|   `/foo` 与 `?foo` |  向下 (上) 搜索    |
|   `n`  与 `N` | 继续搜索 / 反向搜索   |

##  方向键
![方向键](images/20171101_114229.jpg)

## 插入模式

** 进入插入模式**

|命令|说明|
|---|---|
|`i	`   与`a`  | 在当前光标 处(后 )进行编辑   |
|` I` 与 `A` |  在行 首(末) 插入  |
|`o ` 与  `O`  |在当前行后(前)插入一个新行   |
|`cw`  | 替换选中的一个单词 |

---
## 命令模式
**调整文本位置**
|命令|说明|
|---|---|
|`:ce` |   行文本居中|
|`:ri`    | 行文本靠中|
|`:le`   |  行文本靠左|

## 其他命令

|命令|说明|
|---|---|
|`:n1,n2 w [filename]`|    |

## 替换文字
|命令| 说明|
|---|---|
|`:n1,n2s/word1/word2/g`| 替换n1行到n2行 的文字  如 `:100,200s/name/age/g` |
|`:1,$s/word1/word2/g`| 第一行到最后一行的文字 |
|`:1,$s/word1/word2/gc`|  加c ,在替换前询问 |

## 多文件编辑

|命令|说明|
|---|---|
|`vim 1.txt 2.txt` |打开多文件-|
|`:n` 与 `:N`  |向后 向前切换文件-|
|`:e 3.txt`  |打开新文件3.txt-|
|`e#` |回到前一个文件|
|`ls`|可以列出以前编辑过的文档|
|`b 2.txt（或者编号）`|可以直接进入文件2.txt编辑|
|`f `|显示正在编辑的文件名|
|`f new.txt`|改变正在编辑的文件名字为new.txt|
>多文件下可以相互复制黏贴

## 视窗操作
|命令|说明
|--|---|
| `:new`|打开一个新的vim视窗|
|`Ctrl+w`|切换|
|`:sp 1.txt`|开新的水平分屏视窗来编辑1.txt|
|`:vsp  2.txt`|打开新的垂直分屏视窗来编辑2.txt|
|`Ctrl+w s`|将当前窗口分割成两个水平的窗口|
|`Ctrl+w v`|将当前窗口分割成两个垂直的窗口|
|`Ctrl+w q`|即 :q 结束分割出来的视窗。如果在新视窗中有输入需要使用强制符！即:q!|
|`Ctrl+w o`|打开一个视窗并且隐藏之前的所有视窗|
|`Ctrl+w j`|移至下面视窗,同`h`,`j`,`k`,`l`|
|`Ctrl+w J`|将当前视窗移至下面,同`H`,`J`,`K`,`L`|
|`Ctrl+w -`|减小视窗的高度|

## vim执行外部命令

|   命令 | 说明   |   
| --- | --- 
| ` :!ls`   |  用于显示当前目录的内容  |   
| ` :!rm`   |  FILENAME用于删除名为 FILENAME 的文件  |   
| ` :w`   | FILENAME可将当前 VIM 中正在编辑的文件另存为 FILENAME 文件   |   

## 代码补全
在foo.php中

|命令|说明|
|---|---|
|  `[ctrl]+x` -> `[ctrl]+o`  |   代码补全 |
| ` [ctrl]+x` ->` [ctrl]+f ` |   已当前目录的文件名为关键字 |
| ` [ctrl]+x` -> `[ctrl]+n ` |   档案文件的内容为关键字 |


## set 设置
|命令|说明|
|---|---|
|`:set nu` 与 `:set nonu`|   显示行数  / 取消行数 |
|`:set backup`  `:set nobackup`  |		修改内容后产生 `filename~` 的文件	|
|`:set`| 显示与系统预设不同的值|

### 预存设置
新建`~/.vimrc`
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
filetype on
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



