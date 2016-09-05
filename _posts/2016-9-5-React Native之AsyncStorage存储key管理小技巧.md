---
layout: post
title: AsyncStorage存储key管理小技巧
categories: [Android,iOS,教程,React Native]
tags: [React,心得,ES6,JavaScript]
description: AsyncStorage是React Native推荐的数据存储方式。当我们需要根据条件从本地查询出多条记录时，你会想到来一个`select * from xx where xx`。但是很不幸的告诉你，AsyncStorage是不支持sql的，因为AsyncStorage是Key-Value存储系统。
fullview: false
comments: true
---


本文出自[《React Native 每日一学(Learn a little every day)》](https://github.com/crazycodeboy/RNStudyNotes/tree/master/React%20Native%20%E6%AF%8F%E6%97%A5%E4%B8%80%E5%AD%A6)栏目。

AsyncStorage存储key管理小技巧
------

### 场景

AsyncStorage是React Native推荐的数据存储方式。当我们需要根据条件从本地查询出多条记录时，你会想到来一个`select * from xx where xx`。但是很不幸的告诉你，AsyncStorage
是不支持sql的，因为AsyncStorage是Key-Value存储系统。

**那么如何才能快速的从众多记录中将符合条件的记录查询出来呢？**
请往下看...

###  AsyncStorage key管理

为了方便查询多条符合规则的记录，我们可以在保存数据前，对这条数据进行分类，然后记录下这条记录的key。下次再查询该数据前，只需要先查询之前保存的key，然后通过
`static multiGet(keys, callback?) `API，将符合规则的数据一并查询出来。

### 用例

>保存数据

**第一步：保存数据**

```javascript
  saveFavoriteItem(key,vaule,callback) {
    AsyncStorage.setItem(key,vaule,(error,result)=>{
      if (!error) {//更新Favorite的key
        this.updateFavoriteKeys(key,true);
      }
    });
  }
```

**第二步：更新key**

```javascript
/**
   * 更新Favorite key集合
   * @param isAdd true 添加,false 删除
   * **/
  updateFavoriteKeys(key,isAdd){
    AsyncStorage.getItem(this.favoriteKey,(error,result)=>{
      if (!error) {
        var favoriteKeys=[];
        if (result) {
          favoriteKeys=JSON.parse(result);
        }
        var index=favoriteKeys.indexOf(key);
        if(isAdd){
          if (index===-1)favoriteKeys.push(key);
        }else {
          if (index!==-1)favoriteKeys.splice(index, 1);
        }
        AsyncStorage.setItem(this.favoriteKey,JSON.stringify(favoriteKeys));
      }
    });
  }
```

>查询批量数据

**第一步：查询key**

```javascript
getFavoriteKeys(){//获取收藏的Respository对应的key
    return new Promise((resolve,reject)=>{
      AsyncStorage.getItem(this.favoriteKey,(error,result)=>{
        if (!error) {
          try {
            resolve(JSON.parse(result));
          } catch (e) {
            reject(error);
          }
        }else {
          reject(error);
        }
      });
    });
  }
```

**第二步：根据key查询数据**

```javascript
AsyncStorage.multiGet(keys, (err, stores) => {
    try {
      stores.map((result, i, store) => {
        // get at each store's key/value so you can work with it
        let key = store[i][0];
        let value = store[i][1];
        if (value)items.push(JSON.parse(value));
      });
      resolve(items);
    } catch (e) {
      reject(e);
    }
 });
 ```

>**以上是我在使用AsyncStorage进行批量数据查询的一些思路，大家根据实际情况进行调整。**


## About
本文出自[《React Native 每日一学(Learn a little every day)》](https://github.com/crazycodeboy/RNStudyNotes/tree/master/React%20Native%20%E6%AF%8F%E6%97%A5%E4%B8%80%E5%AD%A6)栏目。

#### 了解更多，可以关注我的:

>**[GitHub](https://github.com/crazycodeboy/)**
**[微博](http://weibo.com/u/6003602003)**
**[http://jiapenghui.com](http://jiapenghui.com)**

推荐阅读
----
* [React Native 学习笔记](https://github.com/crazycodeboy/RNStudyNotes)
* [React Native Awesome(汇聚知识，分享精华)](https://github.com/crazycodeboy/react-native-awesome)：汇集了各类react-native学习资料、工具、组件、开源App、资源下载、以及相关新闻等。