---
layout: post
title: 教你轻松将Android library 发布到JCenter
tags: [Android,教程]
description: JCenter是全世界最大的Java仓库,也是Android Studio中repositories的默认节点。JCenter支持Maven, Gradle, Ivy, SBT 等大部分构建工具。将项目发布到JCenter大致流程如下  
fullview: false
comments: true
catalog: true
---


JCenter是全世界最大的Java仓库,也是Android Studio中repositories的默认节点。JCenter支持Maven, Gradle, Ivy, SBT 等大部分构建工具。将项目发布到JCenter大致流程如下：
![将项目发布到JCenter流程](http://img.blog.csdn.net/20160514171659774)

## 具体步骤：  
----

## 第一步：注册Bintray拿到API Key  
如果你已经有账号，则可以跳过这一步，直接往下看。
JCenter是由[Bintray公司](https://bintray.com/)在维护，因此你必须[注册一个Bintray账号](https://bintray.com/)，注册完账号后Bintray会分配给你一个API Key。  
登陆后在首页右上角点击用户名选项下的"Your Profile"进入个人主页，然后点击用户名下面的Edit进入个人信息编辑页面，接下来点击页面左边列表的最后一项API Key。  
![查看bintray api key](http://img.blog.csdn.net/20160514172040901)

## 第二步：发布前的配置

### 首先：添加maven-gradle、gradle-bintray插件  
在项目的最外层的build.gradle文件中的dependencies节点下添加：

```groovy
classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'   
classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.6'
```
android-maven-gradle-plugin插件是用来打包Maven所需文件的。  
gradle-bintray-plugin插件是用来将生成的Maven所需文件上传到Bintray的。  

```groovy  
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.0.0'
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.6'
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
allprojects {
    repositories {
        jcenter()
    }
}
task clean(type: Delete) {
    delete rootProject.buildDir
}   
```       


### 其次，在library model下的build.gradle中进行相应配置      

```groovy     
apply plugin: 'com.github.dcendents.android-maven'
apply plugin: 'com.jfrog.bintray'
// This is the library version used when deploying the artifact
version = "1.0.0"

def siteUrl = 'https://git.oschina.net/crazycodeboy/ScanProj'      // 项目的主页
def gitUrl = 'https://git.oschina.net/crazycodeboy/ScanProj.git'   // Git仓库的url
group = "com.jph.scan.zxing"                                        // Maven Group ID for the artifact，一般填你唯一的包名
install {
    repositories.mavenInstaller {
        // This generates POM.xml with proper parameters
        pom {
            project {
                packaging 'aar'
                // Add your description here
                name 'multi-format 1D/2D barcode image processing use zxing.'
                url siteUrl
                // Set your license
                licenses {
                    license {
                        name 'The Apache Software License, Version 2.0'
                        url 'http://www.apache.org/licenses/LICENSE-2.0.txt'
                    }
                }
                developers {
                    developer {
                        id 'you id'		//填写的一些基本信息
                        name 'your name'
                        email 'your email'
                    }
                }
                scm {
                    connection gitUrl
                    developerConnection gitUrl
                    url siteUrl
                }
            }
        }
    }
}
task sourcesJar(type: Jar) {
    from android.sourceSets.main.java.srcDirs
    classifier = 'sources'
}
task javadoc(type: Javadoc) {
    source = android.sourceSets.main.java.srcDirs
    classpath += project.files(android.getBootClasspath().join(File.pathSeparator))
}
task javadocJar(type: Jar, dependsOn: javadoc) {
    classifier = 'javadoc'
    from javadoc.destinationDir
}
artifacts {
    archives javadocJar
    archives sourcesJar
}
Properties properties = new Properties()
properties.load(project.rootProject.file('local.properties').newDataInputStream())
bintray {
    user = properties.getProperty("bintray.user")
    key = properties.getProperty("bintray.apikey")
    configurations = ['archives']
    pkg {
        repo = "maven"
        name = "ScanProj"	//发布到JCenter上的项目名字
        websiteUrl = siteUrl
        vcsUrl = gitUrl
        licenses = ["Apache-2.0"]
        publish = true
    }
}
javadoc { //jav doc采用utf-8编码否则会报“GBK的不可映射字符”错误
    options{
        encoding "UTF-8"
        charSet 'UTF-8'
    }
}    

```

**其实这些配置脚本也可以从model的build.gradle文件中抽离出来，现在下library model下创建一个bintrayUpload.gradle文件然后将上述代码复制进去，之后再library model的build.gradle中加入如下代码：**     

```groovy
apply from: "bintrayUpload.gradle"  
```

### 最后，在local.properties文件中添加从Bintray申请到的API Key     

```properties
#bintray
bintray.user=your bintray username
bintray.apikey=your apikey
```

**建议将local.properties文件加入忽略文件中不上传，以保护你的apikey**  

## 第三步：将项目提交到Bintray  
如果你一完成了上述的配置后，下面只需要一行代码就可以完成将项目提交到Bintray。  
打开终端进入项目目录下，执行gradlew bintrayUpload命令即可。  
执行完成后，打开你的bintray主页如果在"Owned Repositories"下的maven选中看到你的仓库，则说明你已经将你的仓库成功上传到bintray了。
如图：
![将项目提交到Bintray](http://img.blog.csdn.net/20160514171244554)

## 第四步：将提交到Bintray的项目发布到JCenter  
完成上述的步骤只是将项目提交到bintray，还无法使用该项目库，因为还没有发布到JCenter。
登入Bintray网站，进入个人中心，在右侧的Owned Repositories区域点击Maven的图标，进入你的Maven项目列表。
如果已经上传成功了，在这里就能看到你的项目，进入项目详情，在右下角的Linked To区域点击Add to JCenter，然后在Comments输入框里随便填写下信息，最后点Send提交请求即可。一般情况下当天就会审核，审核通过后会给你发邮件通知你，并且以后更新项目就不需要再审核了。
审核成功后就可以使用你发布到JCenter上的项目了。

**使用你发布到JCenter上的项目**
在Bintray的搜索输入框中输入你的项目：
如图：
![在jcenter搜索项目](http://img.blog.csdn.net/20160514171323265)

单击搜索结果中你的项目，进入项目预览便可以看到项目的引用方式：
如图：
![引用jcenter上的项目](http://img.blog.csdn.net/20160514171336304)
