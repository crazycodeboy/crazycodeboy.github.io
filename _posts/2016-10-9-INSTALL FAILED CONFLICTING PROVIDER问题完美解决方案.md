---
layout:     post
title:      "INSTALL FAILED CONFLICTING PROVIDER问题完美解决方案"
date:       2016-10-9 20:00:00
author:     "CrazyCodeBoy"
linear-gradient:   "linear-gradient(120deg,#2b488a,#ca3749)"
catalog: true
tags: [Android,心得,教程]
---

![INSTALL FAILED CONFLICTING PROVIDER.png](http://upload-images.jianshu.io/upload_images/904056-7d3c093e15d75acf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在安装Android应用时出现`INSTALL FAILED CONFLICTING PROVIDER`问题，是不是感觉很抓狂呢，下面就跟大家分享一下出现这个问题的原因及解决方案。

## 问题原因
在Android中`authority`要求必须是唯一的，比如你在定义一个`provider`时需要为它指定一个唯一的`authority`。如果你在安装一个带有`provider`的应用时，系统会检查当前已安装应用的`authority`是否和你要安装应用的`authority`相同，如果相同则会弹出上述警告，并且安装失败。

## 解决方案

在定义`provider`是，使用软编码的形式，如下：

```xml
<provider
    android:name="android.support.v4.content.FileProvider"
    android:authorities="${applicationId}.fileprovider"
    android:grantUriPermissions="true"
    android:exported="false">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/file_paths" />
</provider>
```

上述代码中通过`${applicationId}.fileprovider`的形式来指定`provider`的`authorities`，所以该`provider`的`authorities`会根据`applicationId`的不同而不同，从而避免了`authorities`的冲突问题。

**那么如何使用刚才定义的`authorities`呢？**    
我们在定义`authorities`是采用了applicationId+fileprovider的形式，在获取`authorities`的时候，我们就可以通过包名+fileprovider来获取，代码如下：

```java
public final static String getFileProviderName(Context context){
    return context.getPackageName()+".fileprovider";
}
```

## 最后

**既然来了，留下个喜欢再走吧，鼓励我继续创作(^_^)∠※**   

**如果喜欢我的文章，那就关注我的[博客](http://www.cboy.me/)吧，让我们一起做朋友~~**

#### 戳这里,加关注哦:   

>**[微博](http://weibo.com/u/6003602003)：第一时间获取推送**    
**[个人博客](http://www.cboy.me/)：干货文章都在这里哦**  
**[GitHub](https://github.com/crazycodeboy/)：我的开源项目**   



