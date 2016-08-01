---
layout: post
title: 【WebView的cookie机制 】轻松搞定WebView cookie同步问题
categories: [Android]
tags: [心得,cookie,WebView]
description: 在进行APP+H5混合开发的时候，一些功能是用native方法实现的,如登陆，一些功能是用H5实现的。所以往往需要将在native方法登陆的状态同步到H5中避免再次登陆。这种情况在Android开发中比较常见，因为Android不会自动同步cookie到WebView。做iOS开发则不用担心这个问题，因为iOS内部已经实现了cookie同步。本文将会介绍两种cookie同步的方式，并重点分析WebView的cookie机制。在开始之前先讲一下基于session的登录验证。      
fullview: false
comments: true
---

在进行APP+H5混合开发的时候，一些功能是用native方法实现的,如登陆，一些功能是用H5实现的。所以往往需要将在native方法登陆的状态同步到H5中避免再次登陆。这种情况在Android开发中比较常见，因为Android不会自动同步cookie到WebView。做iOS开发则不用担心这个问题，因为iOS内部已经实现了cookie同步。本文将会介绍两种cookie同步的方式，并重点分析WebView的cookie机制。在开始之前先讲一下基于session的登录验证。   
**基于session的登录验证：**  
基于session的登录验证，会在程序请求接口的时候判断服务器端是否有当前会话的session，如果没有则被认为没有登录。客户端没有session这一概念，但有cookie与其对应。每一个session都有一个session id作为唯一标识。在登录成功后服务器会在请求头中返回cookie，cookie包含着这次登录会话的session id，在接下来的请求中只需要将登陆返回的cookie设置到请求头中便可以通过验证。

### 方式一：客户端将cookie传给H5

#### 如何做：
- 客户端：将登陆时从服务器取得的cookie传给html。
- html：ajax从参数中取出客户端传来的cookie，ajax发请求时将客户端传来cookie设置到请求头中。

**ajax修改cookie的方式**  

```jquery
$.ajax({
   headers: {'Cookie' : document.cookie },
   url: "sub.domain.com",
   success: function(){}
})
```

#### 缺点：
1. 兼容性差，多数浏览器为了安全起见，都做了禁止修改请求中的cookie的限制。比如iOS的WebView会拦截ajax修改的cookie。
2. 繁琐，每次请求都需要拼接cookie作为参数，比较繁琐。

### 方式二：将cookie同步到WebView(推荐)  

#### 原理分析：
**WebView的cookie机制**    

WebView是基于webkit内核的UI控件，相当于一个浏览器客户端。它会在本地维护每次会话的cookie(保存在data/data/package_name/app_WebView/Cookies.db)。
如图：
![查看APP cookie](http://img.blog.csdn.net/20160527161307114)  
当WebView加载URL的时候,WebView会从本地读取该URL对应的cookie，并携带该cookie与服务器进行通信。   
WebView通过android.webkit.[CookieManager](https://developer.android.com/reference/android/webkit/CookieManager.html)类来维护cookie。[CookieManager](https://developer.android.com/reference/android/webkit/CookieManager.html)是WebView的cookie管理类。

#### 如何做：
下面我们就通过CookieManager将cookie同步到WebView中。  
之前同步cookie需要用到CookieSyncManager类，现在这个类已经被deprecated。如今WebView已经可以在需要的时候自动同步cookie了，所以不再需要创建CookieSyncManager类的对象来进行强制性的同步cookie了。现在只需要获得 CookieManager的对象将cookie设置进去就可以了。

**第一步：登录时从服务器的返回头中取出cookie**      
根据Http请求的客户端不同，取cookie的方式也不同，我就不一一罗列了，需要的网友可以自行Google，以HttpURLcollection为例：  
`String cookieStr = conn.getHeaderField("Set-Cookie");`  
**第二步：将cookie同步到WebView中**    

```java
/**
 * 将cookie同步到WebView
 * @param url WebView要加载的url
 * @param cookie 要同步的cookie
 * @return true 同步cookie成功，false同步cookie失败
 * @Author JPH
 */
public static boolean syncCookie(String url,String cookie) {
    if (Build.VERSION.SDK_INT < Build.VERSION_CODES.LOLLIPOP) {
		CookieSyncManager.createInstance(context);
	}
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.setCookie(url, cookie);//如果没有特殊需求，这里只需要将session id以"key=value"形式作为cookie即可
    String newCookie = cookieManager.getCookie(url);
    return TextUtils.isEmpty(newCookie)?false:true;
}
```    

如图：  
![同步cookie](http://img.blog.csdn.net/20160527161243168)  

如果设置成功，通过` cookieManager.getCookie(url)`方法就可取得刚才设置的cookie，如果两次设置cookie的url相同，则CookieManager会将上一次设置的cookie覆盖，已达到更新的效果。  
下面我们查看一下Cookie数据库中发生的变化。  
如图：  
![查看WebView cookie](http://img.blog.csdn.net/20160527161223066)  
**提示：**   
1.    同步cookie要在WebView加载url之前，否则WebView无法获得相应的cookie，也就无法通过验证。
2.    每次登录成功后都需要调用"syncCookie"方法将cookie同步到WebView中，同时也达到了更新WebView的cookie。如果登录后没有及时将cookie同步到WebView可能导致WebView拿的是旧的session id和服务器进行通信。     

#### 优点：   
1. 方便，只需要在登陆后将cookie同步到WebView即可，省去了每次请求都需要设置一次的繁琐。  
2. 兼容性好，因为是系统原生支持的，所以兼容性自然比方式一要好，不存在cookie被拦截的问题。  
