---
layout: post
title: 轻松搞定MarkDown
tags: [Tools, 教程]
description: MarkDown是一种轻量级标记语言，创始人为约翰·格鲁伯（John Gruber）。它允许人们“使用易读易写的纯文本格式编写文档。MarkDown从推出至今已吸引了大量的粉丝，如大家经常用的为知笔记、简书、和开发者爱好的GitHub以及国内的CSDN等，都对MarkDown提供了支持。   
fullview: false
comments: true
catalog: true
---

## MarkDown是什么？  
MarkDown是一种轻量级标记语言，创始人为约翰·格鲁伯（John Gruber）。它允许人们“使用易读易写的纯文本格式编写文档。MarkDown从推出至今已吸引了大量的粉丝，如大家经常用的为知笔记、简书、和开发者爱好的GitHub以及国内的CSDN等，都对MarkDown提供了支持。   
**PS.**  
因为它的优点很多，目前也被越来越多的写作爱好者，撰稿者广泛使用。看到这里大家不要被「标记」、「语言」所迷惑。其实，Markdown 的语法十分简单。常用的标记符号也不超过十个，这种相对于更为复杂的HTML 标记语言来说，Markdown 可谓是十分轻量的，学习成本也不需要太多，且一旦熟悉这种语法规则，会有一劳永逸的效果。

## 为什么选择MarkDown ？
Markdown 用简洁的语法代替排版，而不像一般我们用的文字处理软件 Word 或 Pages 有大量的排版、字体设置。它使我们专心于码字，用「标记」语法，来代替常见的排版格式。
PS.在刚才的导语里提到Markdown可以让你专注写作内容：不再纠结字体、标题大小、行间距等等版式问题，而是专注于文章内容本身的编写。这种让写作人专注于文章的内容而不是其华丽的外表的特点，也是我喜欢用MarkDown的原因。  

## 使用 Markdown 的优点  
* 专注你的文字内容而不是排版样式。  
* 轻松的导出 HTML、PDF 和本身的 .md 文件。  
* 纯文本内容，兼容所有的文本编辑器与文字处理软件。  
* 可读，直观。是个适合所有人的写作语言。    

## 用什么工具进行编辑？  
在 Mac OS X 上，建议你用Mou 。 Mou ：是款免费且十分好用的 Markdown 编辑器，它支持实时预览，既左边是你编辑的 Markdown ，右边会实时的生成预览效果。   
在Windows上，建议你用MarkdownPad。MarkdownPad：的效果和Mou 一样甚至比它更强大，但是是收费的。  
**PS.**  
如果你不追求实时预览效果的话，其实用记事本编写MarkDown也是一个不错的选择，另外在各大编译器中也有对应的MarkDwon编辑插件，如用在IntelliJ IDEA中MultiMarkDwon插件。   

## MarkDown的基本使用  

### 如何设置标题？
可以在标题内容前输入特定数量的井号('#')来实现对应级别的HTML样式的标题(HTML提供六级标题)。  
例如：       

![Markdown与HTML在标题上的对比](http://upload-images.jianshu.io/upload_images/904056-8e201f2d935cbb17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**PS.**  
在这里你想设置几级标题就敲几个#就可以了对比Html表示标题的方法，MarkDown是不是简单多了。   
注意：因为在HTML中最多支持6级标题，所以在markdown中超出6个的#将不会起作用。   

### 如何换行？  
在行尾插入至少两个空格即可。
例如：

![Markdown与HTML在换行上的对比](http://upload-images.jianshu.io/upload_images/904056-b0566a7977187071.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 如何加粗和斜体？       
加粗：在要加粗的文字两端加入\*\*或\_\_ 。
斜体：在要进行斜体的文字两端加入\*或\_。
例子：
**加粗***斜体*
***加粗和斜体***

### 如何插入链接？   
\[链接文字\](链接地址)  
例子：   
\[fengyuzhengfan](http://blog.csdn.net/fengyuzhengfan)  
[fengyuzhengfan](http://blog.csdn.net/fengyuzhengfan)  
注意：这里的小括号是英文状态下的

### 如何插入图片？
!\[图片的替代文字](链接地址)  
例子：   
!\[百度](https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo/bd_logo1_31bdc765.png)
![百度](https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo/bd_logo1_31bdc765.png)  

### 如何插入引用？
只需要在文本前加入 > 这种尖括号（大于号）即可。  
例子：  
\> 例如这样  

> 例如这样

### 如何插水平线？

在单独一行里输入3个或以上的短横线、星号或者下划线实现。以下每一行都产生一条水平分区线。  
例子：  
\***  

***
\- - -  

- - -      
PS.短横线和星号之间可以输入任意空格。

### 如何设置列表？
无序列表：
-、+、*都能表示列表，要注意的是 前后都要有空格。
有序列表：
数字加点加空格。  
例如：

1. 第一
2. 第二
3. 第三   

## MarkDown的高级应用（常见问题的解决办法）  

### 如何插入代码？
插入代码的方式有两种：
方式一：在每行代码前加入4个空格或者添加一个制表符（TAB键）
方式二：在代码两侧添加三个反引号(```)。
如：    

```javascript   

     $(document).ready(function () {
	  alert('hello world');   
});
```   

PS.   
这里可以指定代码所属的语言，只要在第一组反引号后面添加相应的语言名称即可。这样就会以javascript的语法格式来显示所包含的代码。

### 如何设置首行缩进？
可以在段首加入&  ensp;来输入一个空格。加入&    emsp;来输入两个空格。   

### 文档中用到了MarkDown语法中的符号：
**符号转义：**
如果你的描述中需要用到 markdown 的符号，比如 \_ # \* 等，但又不想它被转义，这时候可以在这些符号前加反斜杠，如 \\_ \\# \\* 进行避免。

### 如何设置语法高亮？  
在\`\`（两个反引号）之间的文字会被高亮显示。
例子：
`GitHub`现在成了主流，不仅提供`Git`代码托管（取代SVN）、`Issue`追踪（取代JIRA）

### 如何结束先前的格式状态？
在改变格式时，添加一个空行。
PS.这是空行的妙用的其中一个地方，另外，段与段之间建议加一个空行，因为在某些平台上，如果段与段之间没有空行的话，两段内容会柔和在一起，这是不同平台对Markdown语法的解析不同有关，为了防止兼容性问题建议大家在段与段之间建议加一个空行。

### 文档通用问题：
如果你用Markdown写好文章，需要放在好几个博客上，但有的博客又不支持Markdown语法？
可以将Markdown转换成html或者PDF文件来解决这个问题，具体转换方式可以在网上查找，如果你用的是MarkdownPad，直接Export就可以了。
