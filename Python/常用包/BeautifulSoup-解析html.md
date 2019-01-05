[TOC]


## BeautifulSoup-解析html
>文档地址  [中文文档](https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html)


code
```
html_doc = """
<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title"><b>The Dormouse's story</b></p>
<p class="story">
    Once upon a time there were three little sisters; and their names were
    <a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
    <a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
    <a href="http://example.com/tillie" class="sister1" id="link3">Tillie</a>;
    and they lived at the bottom of a well.
</p>

<p class="story">...</p>
"""

soup = bs4.BeautifulSoup(html_doc, "html.parser")
print(soup.a) #打印<a class="sister" href="http://example.com/elsie" id="link1">Elsie</a>
print(soup.a.string) #打印a标签的内容
print(soup.a['href']) #打印a标签的href属性的值
print(soup.find(id='link3'))
print(soup.find('a',class_='sister'))  #Python的class 有关键字所以加'_'
print(soup.find_all('a',class_='sister'))
print(soup.find('p',{'class','story'}).get_text())
print(soup.find_all("a",href=re.compile(r'^http://example.com')))
print(soup.find_all("input",type=re.compile('text'))) 
```