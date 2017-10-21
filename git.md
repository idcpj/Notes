

[TOC]

##  全局配置
```
$ git config --global user.name "Scott Chacon"
$ git config --global user.email "schacon@gmail.com"
```
>查看 `cat ~/.gitconfig`
>

## 操作

`git clone https://github.com/shiyanlou/gitproject`		克隆项目

### 新建项目
` git init`    初始化
`git status`  查看状态
`git add .` or `git add filename` 	 添加所有/`filename`文件
` git commit -m "提交说明"`    添加到本地仓库
`git remote add origin https://github.com/idcpj/shiyanlou.git`   连接到远程服务器
`git push origin master`  推送到远程服务器

### 分支
`git branch 分支名`   创建分支
`git branch`			查看分支
`git checkout 分支名`    切换分支
`git merge  -m '注释说明'  分支名`  合并分支

#### 合并冲突
`git status` 查看冲突文件 
`vim 冲突文件` 去掉`<<<<<<`  手动合并内容
`git add 冲突文件`和`git commit` 提交修改后的文件
`git branch -d/–D 分值名`       			删除分支`-D`强制删除(合并完分支后,即可删除) 
`git reset --hard HEAD^`  		撤销合并
>'*' 星号标识了你当工作在哪个分支下
>创建新分支后 需要 `git add `  在 `git commit` 才可上传


## Git日志
` git log`   查看日志
`git log v2.5.. Makefile fs/`		找出所有从"v2.5“开始在fs目录下的所有Makefile的修改：
`git log --stat`			打印出文件添加和修改的详细内容
`git log --pretty=oneline`  	格式化日志  每次修改显示一行数据
`git log --graph --pretty=oneline`		画出提交历史(commit history)线