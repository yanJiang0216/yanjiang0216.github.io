---
layout: post
title: "Python中strip()函数"
categorys: Python
---

**函数原型**

声明：s为字符串，rm为要删除的字符序列

s.strip(rm)   删除s字符串中开头、结尾处，在rm序列中的字符

s.lstrip(rm)   删除s字符串中开头处，在rm序列中的字符

s.rstrip(rm)   删除s字符串中结尾处，在rm序列中的字符

## 注意

1.当rm为空时，默认删除空白符（包括‘\n’,'\r','\t',' '）

例如：

![strip函数图1]({{site.url}}D:\yanjiang0216.github.io\picture\strip函数图1.png)

2.这里的rm中只要存在的，就都要删除掉。

例如：

![strip函数图2]({{site.url}}D:\yanjiang0216.github.io\picture\strip函数图2.png)