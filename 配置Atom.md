[TOC]

使用Package Control组件安装的插件
按Ctrl+`调出console

`import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())`

重启Sublime Text 3。如果在Perferences->package settings中看到package control这一项，则安装成功