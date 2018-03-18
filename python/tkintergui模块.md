[TOC]
---

> [官方文档](https://docs.python.org/3.6/library/tkinter.html)
[中文参考文档](https://morvanzhou.github.io/tutorials/python-basic/tkinter/2-01-label-button/)
---

## 组件的三种使用方式
```
import tkinter as tk

window = tk.Tk()
window.title("窗口标题-demo")
window.geometry('200x100')

def demo():
    print("测试出发效果")


# 方法一
oneButton = tk.Button(window)  # 通过查看源码可查看Button的标准参数和特定参数
oneButton['text'] = '测试按钮'
oneButton['command'] = demo
oneButton.pack()

# 方法二
twoButton = tk.Button(window, text='测试按钮2', command=demo)
twoButton.pack()


# 方法三 类
class ThreeButton(object):
    def __init__(self, window):
        self.window = window
        self.create_button()

    def create_button(self):
        self.treeButton = tk.Button(self.window)
        # self.threeButton=tk.Button(self)  #或直接输入slef 即可
        self.treeButton['text'] = '测试按钮三'
        self.treeButton['command'] = self.treeDemo
        self.treeButton.pack()

    def treeDemo(self):
        print("测试按钮三")


ThreeButton(window)  # 实例化

window.mainloop()
```
