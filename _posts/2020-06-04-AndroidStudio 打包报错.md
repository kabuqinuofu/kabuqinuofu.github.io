---
layout: post
title: "AndroidStudio 打包报Error:Execution failed for task ':app:lintVitalRelease'"
date: 2020-06-04 
description: "打包报错情况处理"
tag: Android 
---   


```
需在app下的gradle文件的android部分添加代码：
lintOptions {
        checkReleaseBuilds false
        abortOnError false
}
```

