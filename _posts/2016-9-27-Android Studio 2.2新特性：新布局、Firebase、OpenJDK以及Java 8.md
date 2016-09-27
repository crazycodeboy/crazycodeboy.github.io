---
layout:     post
title:      "Android Studio 2.2新特性：新布局、Firebase、OpenJDK以及Java 8"
subtitle:   "Android Studio2.22新特性"
date:       2016-09-27 20:00:00
author:     "CrazyCodeBoy"
linear-gradient:   "linear-gradient(120deg,#2b488a,#ca3749)"
catalog: true
tags: [Android Studio,Android]
---

前几天，收到了Android Studio 2.2的更新推送，于是迫不及待的更新了一下。不负众望Android Studio 2.2带来了很多新的特性，能让我眼前一亮。

[Android Studio 2.2](https://developer.android.com/studio/install.html)所带来的增强涉及到开发过程的所有阶段——设计、开发、构建与测试，其中包含新的Constraint布局、布局编辑器（Layout Editor）、Firebase插件、示例代码浏览器、对Java 8的支持、OpenJDK、GPU调试器等。

## 设计

* [Constraint布局](https://developer.android.com/training/constraint-layout/index.html)：类似于RelativeLayout，但是更加灵活并且更易于在布局编辑器中使用。它有助于创建复杂的布局，在这个过程中不需要对它们进行嵌套。
![layout-editor.png](http://upload-images.jianshu.io/upload_images/904056-1eae954ef8fad8e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* [布局编辑器](https://developer.android.com/studio/write/layout-editor.html)：用户界面工具，能够以拖拽的方式设计应用的布局，其中还包含了一个属性编辑器。
* [实验性的布局探测器（Layout Inspector）](http://tools.android.com/tech-docs/layout-inspector)：用于创建当前模拟器或实际设备的视图结构快照，用来确定某个布局的渲染是否符合预期。

## 开发
* Firebase服务：AdMob、分析、认证和通知能够非常容易地集成到已有或全新的应用中。
* 示例代码浏览器：查找示例代码，在GitHub上展现了变量、方法或类型是如何使用的。
* 更好的代码分析 & Lint检查：包含了260个Android Lint和代码检查点，包括Java 8检查和跨文件分析。
* IDE更新：在IDE方面，AndroidStudio采用了IntelliJ 2016.1.3。

## 构建
* [Jack编译器工具链](https://source.android.com/source/jack.html)：支持注解处理和增量构建。
* [JDK采用JDK8](https://developer.android.com/guide/platform/j8-jack.html)：在JDK方面，AndroidStudio采用了JDK8，所以安装了AndroidStudio2.2的小伙伴，需要将你的JDK更新到8以保证AndroidStudio能更好的工作。另外，AndroidStudio2.2支持了一些Java 8的语言特性，包括lambda表达式、类型注解、接口方法和方法引用。
* 合并的Manifest视图：用于查看添加依赖后，Manifest是如何进行合并的。
* 实验性的构建缓存：文件或目录是在之前的构建中创建的，甚至可以位于不同的项目中，它们会进行存储和重用，从而提升构建的速度。
* Android Studio现在已经捆绑了OpenJDK，如果需要的话，可以使用不同的JDK。

## 测试

Espresso测试记录器（beta）：记录与UI的交互，从而可以在本地的Espresso测试或Firebase上进行回放。
GPU调试器（beta）：用于调试OpenGL ES应用。
APK分析器：提供APK中各种组件大小的信息。
Android Studio 2.2包含了稳定性问题的修正以及性能的提升。关于新特性的更多细节信息，大家可以查看[AndroidStudio发布说明](https://developer.android.com/studio/releases/index.html)。

## 更新AndroidStudio2.2

### 方式一： 自动检查更新
Menu(菜单)->Help(帮助)->Check for updates(检查更新)。
然后AndroidStudio会自动检查是否有更新，然后按照提示一路点下去就行，通过这种方式更新失败的小伙伴，可以往下看。

### 方式二：完整包更新
大家也可以通过这种方式来更新你的AndroidStudio。
首先，到[Android开发者网站](https://developer.android.com/studio/install.html)下载最新的AndroidStudio，然后进行安装即可。
考虑到大部分小伙伴访问不了Google服务器，我把AndroidStudio最新版下载后放到了百度网盘上，供小伙伴们下载。
[AndroidStudio2.2 for Mac](http://pan.baidu.com/s/1dFun0pN)  密码`xt53`
[AndroidStudio2.2 for Windows](http://pan.baidu.com/s/1dEW6UUt) 密码`zikl`

## 最后

**既然来了，留下个喜欢再走吧，鼓励我继续创作(^_^)∠※**   

**如果喜欢我的文章，那就关注我的[博客](http://www.cboy.me/)吧，让我们一起做朋友~~**

#### 戳这里,加关注哦:   

>**[微博](http://weibo.com/u/6003602003)：第一时间获取推送**    
**[个人博客](http://www.cboy.me/)：干货文章都在这里哦**  
**[GitHub](https://github.com/crazycodeboy/)：我的开源项目**     