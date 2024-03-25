---
layout: post
title:  "Markdown加载base64图片"
date:   2019-3-26 10:21:10 +0700
tags:
  - Others

---

---

## Markdown加载base64图片

### 目的：

- markdown涉及到插入图片时，会出现小问题，现整理下。

### 在[Typora](https://so.csdn.net/so/search?q=Typora&spm=1001.2101.3001.7020)中插入图片常用的处理方法是：

1. 将本地的图片地址传入
2. 将网络上的图片地址传入

这两种方式都存在一个问题：链接不可用时，图片就展示不出来了！

### 解决方法

首先将图片通过在线[转码](https://so.csdn.net/so/search?q=转码&spm=1001.2101.3001.7020)工具转换成[base64](https://c.runoob.com/front-end/59/)的编码，并用以下格式嵌入即可，格式如下：

```
![image] (base64)
```

但是由于这[base64编码](https://so.csdn.net/so/search?q=base64编码&spm=1001.2101.3001.7020)往往都很长，很占篇幅，我们可以先给图片经行[压缩](https://www.imagerecycle.com/)，或者我们可以给图片编号，并将所有的图片base64编码放在文档的最后即可，格式如下：

```
在插入图片的地方使用：![image] [图片编号]
在文档最后使用：[图片编号]:base64编码
```

