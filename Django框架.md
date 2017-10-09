# Django 快速入门
[TOC]

## 基础
### 创建项目
>在想要安置项目的目录
命令行输入 :`django-admin startproject 项目名称`
无报错,则安装成功
*提示:window用户可以在文件管理器地址中输入cmd,会跳转到命令窗口*

### 启动服务器
>`python manage.py runserver  [端口号]` 启动
>端口号可不填


### 创建应用
>在命令行输入`python manage.py startapp blog`  blog 为应用名 
>把应用名添加到settings.py中的`INSTALLED_APPS`中
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog'  #新增应用 
]
```

### 创建一个页面(响应)
1. 在`/blog/views.py`中
```
from django.http import HttpResponse

def index(request): #接受参数 默认为request
    return HttpResponse('hello word')
```

2. 在`/mysite/urls.py`中-优化url见下标签
```
import blog.views

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^index/', blog.views.index), 
]
```

### url配置
1. 在`/mysite/urls.py`中
```
urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^blog/', include('blog.urls')), # 使用include()函数
]
```
2. 复制`urls.py`至在`/blog/urls.py`
```
from django.conf.urls import url, include
from . import views

urlpatterns = [
    url(r'^index/$', views.index),  #index 后要加'/'
]
```

### Template
1. 在`/blog`中创建`templtes`目录
2. 在`templtes`中创建如 `index.html`文件
3. 在`views.py`中
```
def index(request):
    return render(request,'index.html',{"hello":"hello,blog!"})
    
```
4.在模版中用`{{hello}}`调用

**template文件名冲突**
在templates中html文件前加入模版的目录
如`/blog/templates/blog/index.html`
修改views.py文件的目录
```
def index(request):
    return render(request,'blog/index.html',{"hello":"hello,blog!"})
```
**template文件目录会根据INSTALLED_APPS 的顺序查找**


### Models 
1. 在`blog/models.py`中创建类 并集成 models.Model

```
from django.db import models

class Test(models.Model):
    title = models.CharField(max_length=32,default='title')
    content = models.CharField(null=True)
```
2. 生成数据表(默认为SQLlite)

```bash
#生成相关 blog/migrations/0001_initial.py 文件
python manage.py makemigrations blog  [可选] - 命令负责保存你的模型变化到一个迁移文件 
python manage.py migrate	-负责将改变提交到数据库

#注意:若没有在主键,那么在生成文件中会自动创建主键
```
3. 打印sql 
```
python manage.py sqlmigrate blog 0001   -0001即migrations目录生成的id

#输出
CREATE TABLE "blog_article" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "title" varchar(32) NOT NULL, "content" text NULL);

```

4. 获取数据 
`/blog/views.py`中
```
from . import models
def index(request):
    oneArticle = models.Article.objects.get(pk = 1)
    return render(request,'index.html',{"artcile":oneArticle})

```
`/blog/templates/index.html`中
```
<h1>{{artcile.title}}</h1>
<h1>{{artcile.content}}</h1>
```

5. 切换为mysql数据库
```
'default': {

        'ENGINE': 'django.db.backends.mysql',

        'NAME':'',

        'USER': '',

        'PASSWORD': '',

        'HOST': '127.0.0.1',

    }

#python3.6用的pymysql需要在myblog下的__init__.py加入下两行

import pymysql
pymysql.install_as_MySQLdb()


#测试mysql-无报错则正确

python manager.py shell  
from django.db import connection  
cursor = connection.cursor()  
```
### admin管理
1. 创建admin ` python manage.py createsuperuser `
2. `localhost:8000/admin/` Admin入口
3. 修改setting.py 中 `LANGUAGE_CODE= 'zh_Hans'`
4. 注册models
```
class ArticleAdmin(admin.ModelAdmin):
    list_display = ('title', 'content')  #admin中显示title 和content列表
    list_filter = ('pub_time',)  # 过滤器	类似分组
admin.site.register(Article,ArticleAdmin)
```

5. 修改数据默认显示名称
```
class Article(models.Model):
    title = models.CharField(max_length=32, default='title')
    content = models.TextField(null=True)

    def __str__(self):   # 添加魔术方法
        return self.title
```
### 模版渲染
```python
#列表数据
Article = models.Article.objects.all()
    return render(request,'blog/index.html',{"articles":Article})
    
#index.html中
{% for article in articles %}
    <li><a href="">{{article.title}}</a></li>
{% endfor %}

#文章数据
article = models.Article.objects.get(pk=article_id)
    return render(request,'blog/article_page.html',{'article':article})
```
>注:objects必须加`s`

#### 超链接的两种渲染
方法一(推荐)
```
href="/blog/details/{{article.id}}"
```
方法二
```python
#语法
{% url "app_name:url_name" param %}

-->  `app_name`  在`url(r'^blog/', include('blog.urls',namespace='blog'))`配置
-->  `url_name` 在  `url(r'^details/(?P<article_id>\d)$', views.article_page,name='article_page'),`

#实例
{% url 'blog:article_page' article.id %}
```
#### 表单处理
1. 在`form`表单中加入`{% csrf_token %}`
2. 接受参数并跳转首页
```
#查
article = models.Article.objects.get(pk=id)
#增
models.Article.objects.create(title=title, content=content)
#改
article = models.Article.objects.get(pk=id)
article.content = content
article.sav	e()
#删
 Article = models.Article.objects.get(pk=2)
Article.delete()
```

#### Django Shell
>用命令行操作数据
```
#启动
python manage.py shell

#实例
from blog.models import Article
Article.objects.all()   #打印所有Article数据

```