[TOC]

## 技巧

### 元组赋值

    s = ("hello",'word');
    a,b=s
    print(a,b) #hello word
    
### 切片

	L = range(1, 101)
    print L[4::5][-10::]  #最后10个5的倍数。
    
### *args 和**kw的区别
```
def name(*args, **kw):
    print(*args)     # hello word
    print(args)      # ('hello', 'word') 
    print(*kw)       # name age
    print(kw)        # {'name': 'cpj', 'age': '12'}
	
name('hello', 'word', name="cpj", age="12")
```
### 给类型增加属性

```
class Person(object):
    def __init__(self, name, gender, **kw):
        self.name=name
        self.gender = gender
        for k , v in kw.iteritems():
            setattr(self,k,v)
                        
p = Person('Bob', 'Male', age=18, course='Python')
```
### 实现__xx__方法

对象中的`__enter__` ,` __call__`,`__exit__`等方法必须得在对象中实现才可以用

### for循环
```
    for i in range(1,6):
        print(i)
```

### `__name__`作用

	#打印入口文件
		print(__name__) #__main__
        
	# test3.py 
		print(__name__)
    #在入口文件引入 test3
    #输出:test3

### 获取命令行参数

```python
#文件
import sys
if __name__ =='__main__':
    for arg in sys.argv:
        print(arg)
        
#命令窗口
python test2.py 0 1 2 3 

test2.py
0
10
1
```

### 转码

    a = unicode.encode(u'慕课','utf-8')
    print(a) #b'\xe6\x85\x95\xe8\xaf\xbe
    
### 特定编码写入或读取

	import codecs
    f = codecs.open("test.txt",'w','utf-8')
    
### `__init__.py` 文件用法
```
#目录结构
	Phone
        ├ Isdn.py 	
        ├ G3.py 	
        ├ _init__.py
        
# _init__.py文件
    from Pots import Pots
    from Isdn import Isdn
    from G3 import G3
    
# 导入import Phone时就可以共用Pots,Isdn等的包
```
### python3.x 与python2.x的字符串区别
    #在2.7中
    #字符串生成使用u
        a = 'hello word'
        type(a) #str
        
        a = u'hello word'
        type(a) #unicode

   	#在3.0中
    str 都是unicode
    
### 迭代
```
L = ['Adam', 'Lisa', 'Bart', 'Paul']	
T = ('Adam', 'Lisa', 'Bart', 'Paul')
S = set(L)
for index, name in enumerate(T,1):
    print(index, '-', name)
```
> 数组,元祖set,都可以通过`enumerate`打出索引与值

*字典迭代*
```
D = {'a':'A','b':'B'}
for key,value in D.items():
    print(key,'-',value)
```

### 生成器
```
for i in xrange(10):
    print i 
```    

### 字典/集合 解析
```
my_dict = {i: i * i for i in xrange(100)} 
my_set = {i * 15 for i in xrange(100)}~~~[api]
get:/url
*string:id=默认值#说明文字
name#说明文字
<<<
success

<<<
error

~~~

```

### 对Python表达式求值
    import ast 
    my_list = ast.literal_eval(expr)  
    
### 三元运算符
    result = (2,1)[3==3]    ->1
    result = 1 if 3==3 else 2   ->1
    
### 正则
    str = "imooc python Imooc"
	print(re.search('python',str).group()) #python
    print(re.findall('imo+c',str,re.I))  # ['imooc', 'Imooc']
    print(re.sub('imooc','imoc',str))	# imoc python imoc

### 字典转json字符串
    dict = {'name':'cpj','age':'12'}
    print(json.dumps(dict))

### 事件钩子
```
def hook_reponse():
    print("this is a hook")

def demo(name,hook=None):
    if hook is not None:
        eval(hook)()  # 把字符串转为函数
    print(" hello "+name)

demo('cpj',hook='hook_reponse')
```

### 编码问题
>python3.5，在window下,新文件的默认编码是gbk
>`open("output.html",'w',encoding='utf-8')`得用encode规定打开写入文件的格式
>mac和linux 都是utf-8 所以无需encoding

### 同时遍历两个数组
```
 a = ['Pradeepto', 'Kushal']
 b = ['OpenSUSE', 'Fedora']
 for x, y in zip(a, b):
     print("{} uses {}".format(x, y))
```