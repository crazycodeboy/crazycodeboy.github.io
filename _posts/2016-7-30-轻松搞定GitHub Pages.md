---
layout: post
title: 轻松搞定GitHub Pages
categories: [Tools,教程,GitHub]
tags: [GitHub Pages,创建个人博客]
description: GitHub支持创建个人或组织以及项目这两种类型的网站。  <br>本文章将向大家分享如何为项目、组织或个人创建一个GitHub Pages。
fullview: false
comments: true
---


GitHub支持创建个人或组织以及项目这两种类型的网站。  
本文章将向大家分享如何为项目、组织或个人创建一个GitHub Pages。


## 为项目创建GitHub Pages
你可以为你的项目创建一个GitHub Pages，大致分为以下步骤：  

### 第一步：仓库设置  
在GitHub上打开你的仓库首页，单击设置(Settings)页签  
 ![打开仓库设置页面]
![打开仓库设置页面.png](http://upload-images.jianshu.io/upload_images/904056-46c3ad9ec97ef97b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 第二步：使用自动生成器生成GitHub Pages
下拉设置页面到**GitHub Pages**，单击**Launch automatic page generator**
![使用自动生成器生成GitHub Pages.png](http://upload-images.jianshu.io/upload_images/904056-5bb3fbb7a9155e1a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 第三步：添加内容  
使用GitHub编辑器为编辑网站内容。如果项目中已经存在README.md，可以使用README.md作为网站内容。  
![添加内容.png](http://upload-images.jianshu.io/upload_images/904056-ba3f8bc2cbc3884e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

编辑完成后单击右下方的**Continue to Layouts**按钮。

### 第四步：选择主题  
你可以为GitHub Pages选择一个主题：  
![选择主题.png](http://upload-images.jianshu.io/upload_images/904056-2e2e461cf00b256a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


选择好主题后，单击Publish 按钮即可完成GitHub Pages的发布。  
至此，你的GitHub Pages已经创建完成并发布，打开浏览器即可浏览：http://username.github.io/repository.  

## 为组织或个人创建GitHub Pages  
GitHub支持创建组织或个人创建GitHub Pages，通过以下步骤即可完成创建：  

### 第一步：创建一个仓库    
你需要创建一个`username.github.io`格式的仓库,username为你的GiHub账户的账户名或组织名。
![创建一个仓库.png](http://upload-images.jianshu.io/upload_images/904056-327ba46c7f169cea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 第二步：将仓库clone到本地
将仓库clone到本地：  
![将仓库clone到本地.png](http://upload-images.jianshu.io/upload_images/904056-58240da0c41496fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 第三步：创建首页  
在仓库的根目录中创建一个名为index.html的文件。   

![创建GitHub Pages首页.png](http://upload-images.jianshu.io/upload_images/904056-11e9c22bf11b05c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 第四步：发布GitHub Pages
index.html文件就是你的GitHub Pages的首页，编辑这个文件，然后将它push到你的远程仓库即可。

![发布GitHub Pages.png](http://upload-images.jianshu.io/upload_images/904056-cf2498c979baec27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 第五步：打开浏览器查看你的GitHub Pages  
在浏览器中输入`http://username.github.io.`,username改为你的GitHub 账户名。  

![查看你的GitHub Pages.png](http://upload-images.jianshu.io/upload_images/904056-cf394f6673f61221.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 参考  
[GitHub Pages](https://pages.github.com/)
