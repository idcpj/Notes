[TOC]


## pdfminer3k-解析pdf
```
import logging
from urllib.request import urlopen

logging.Logger.propagate = False
logging.getLogger().setLevel(logging.ERROR)

from pdfminer.converter import PDFPageAggregator
from pdfminer.layout import LAParams
from pdfminer.pdfinterp import PDFResourceManager, PDFPageInterpreter
from pdfminer.pdfparser import PDFParser, PDFDocument

fp = open('template/pdftest.pdf', 'rb')
# 在线
# fp = urlopen('http://www.tencent.com/zh-cn/articles/8003251479983154.pdf')

# 创建一个与文档关联的解析器
parser = PDFParser(fp)

# PDF文档对象
doc = PDFDocument()

# 链接解析器和文档对象
parser.set_document(doc)
doc.set_parser(parser)

# 初始化文档
doc.initialize("")

# 创建DPF资源管理器
resource = PDFResourceManager()

# 参数分析器
laparam = LAParams()

# 聚合器
device = PDFPageAggregator(resource, laparams=laparam)

# 创建页面解析器
interpreter = PDFPageInterpreter(resource, device)

# 使用文档对象从pdf中读取内容
for page in doc.get_pages():
    # 使用页面解析器
    interpreter.process_page(page)

    layout = device.get_result()
    # 使用聚合器获取内容
    for out in layout:
        # 判断是否有get_text属性
        if hasattr(out, 'get_text'):
            print(out.get_text())

if __name__ == '__main__':
    pass
```