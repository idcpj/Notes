[TOC]


1. 终端执行subl即可打开Sublime Text
`ln -s  "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sub`

2. 使用Package Control组件安装的插件
按Ctrl+~ 调出console

	`import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())`

	重启Sublime Text 3。如果在`Perferences->package settings`中看到`package control`这一项，则安装成功
    
3. 安装插件
	快捷键`Ctrl + Shift + p`然后在控制窗口中输入`Package Control: Install Package；`

    
## 插件
1. Emmet
2. BracketHighlighter
	高亮括号配对
3. ChineseLocalization
	中文补丁
4. ini
	ini语法高亮
    
## 快捷键

`Cmd + d` 选择相同的文字
`Cmd + Enter` 在任意位置跳到下行
