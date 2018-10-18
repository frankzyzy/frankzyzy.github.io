---
layout: post
title: markdown基本语法使用
date: 2018-10-12 10:00:00 +0300
description: markdown 语法十分简单，非常有利于写作，这里做一个简单介绍
img: workflow.jpg # Add image post (optional)
tags: [Productivity, Software] # add tag
---

markdown 语法十分简单，非常有利于写作，这里做一个简单介绍。

#表示标题，##表示2级标题，同理####表示4级标题

# 表示标题
## 表示2级标题，同理
#### 表示4级标题

空行表示新的段落，如果不空行的话，markdown 认为是同一段落

[A](B) 这样样式表示为链接，A为你想要显示的文字，B为实际的链接

![A](B) 这种样式表示图片，A为图片的描述文字，B为图片链接

*表示无序列表
* A
* B
* C

1,2,3 表示有序列表
1 A
2 B
3 C

---

```java
System.out.print();
```

# 创建文章的文件

发表一篇新文章，你所需要做的就是在 _posts 文件夹中创建一个新的文件。文件名的命名非常重要。
Jekyll 要求一篇文章的文件名遵循下面的格式：

```
年-月-日-标题.MARKUP
```


在这里，年是 4 位数字，月和日都是 2 位数字。MARKUP扩展名代表了这篇文章是用什么格式写的。
下面是一些合法的文件名的例子：
2011-12-31-new-years-eve-is-awesome.markdown
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.textile

