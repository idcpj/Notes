# web.py
[TOC]

## 安装
```
pip3 install db 
pip install utils
git clone https://github.com/webpy/webpy.git
cd webpy
python setup.py install
pip list 
查看是否添加了webpy
```
## 入门
code
```
import web
render =web.template.render("template")
urls = (
    '/index', 'index',
    '/blog/\d+', 'blog',
    '/(.*)', 'hello',
)

app = web.application(urls, globals())


class hello:
    def GET(self, name):
        return "<html>hello word</html>"

if __name__ == "__main__":
    app.run()
```
### 模版
	def GET(self, name):
            return open('./hello.html','r').read()
### URL映射

    urls = (
        '/index', 'index',
        '/blog/\d+', 'blog',
        '/(.*)', 'hello',
    )
    
 ### 请求处理
 ```python
#请求参数
#地址:http://127.0.0.1:8080/index?name=cpj&age=13

class index:
    def GET(self):
        query = web.input()
        return query
        
#输出 <Storage {'age': '13', 'name': 'cpj'}>
```

### 响应处理

### 模版文件读取
```
#python文件

import web
render =web.template.render("template")
urls = (
    '/(.*)', 'hello',
)
app = web.application(urls, globals())
class hello:
    def GET(self, name):
        return render.hello1(name)   #hello1 与template下的hello.html相同
if __name__ == "__main__":
app.run()


# hello1.html文件

    $def with(name)
    <input type="text" name="username" value="$name">  
```
### 结果数据获取
```python
config = {'host': '127.0.0.1', 'port': 3306, 'user': 'root', 'password': 'root', 'db': 'imooc_o2o',
                        'charset': 'utf8mb4', 'cursorclass': pymysql.cursors.DictCursor, }
class article:
    def GET(self):
        db = pymysql.connect(**config)  #导入配置
        cursor = db.cursor()
        cursor.execute("select `name`,`create_time` from `o2o_category`")
        results = cursor.fetchall()
        db.close()
        cursor.close()
        return render.article(results)

#article.html模版

$def with(r)
<h1>文章列表</h1>
<ul>
    $for l in r:
    <li>$l['name']=>$l.get('create_time')</li>  
</ul>
```

> `l.['name']`与`l.get('name')` 效果相同