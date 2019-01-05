[TOC]


## requests-比urllib2简洁
>文档地址:[中文文档](http://docs.python-requests.org/zh_CN/latest/)

```
#GET带参数
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get("http://httpbin.org/get", params=payload)

#定制请求头
headers = {'user-agent': 'my-app/0.0.1'}
r = requests.get('http://www.baidu.com', headers=headers)

#post表单形式
dict = {"name":"cpj",'age':"123"}
requests.post("http://www.baidu.com",data=dict)

#异常处理
import requests
from requests import exceptions

try:
    response = requests.get("http://httpbin.org/ip",timeout=0.2)
    response.raise_for_status()  #抛出非200 异常的解释

except exceptions.Timeout as e:
    print("请求超时:",e)
except exceptions.HTTPError as e:
    print("状态码异常",e)
else:
    print(response.text)
    print(response.status_code)

#proxies代理
import requests
proxies = {'http': "socks5://127.0.0.1:1080",'https': "socks5://127.0.0.1:1080"}
response = requests.get('https://www.google.com',proxies=proxies)
print(response.content)
```