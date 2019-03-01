---
layout: post
title: "NumberFormat"
date: 2019-03-01
description: "格式转换"
tag: JAVA 
---   

目标：

对 6666.00 这种数字不想要后面的00，6666.10处理之后666.1

```

String mNumBefore = "666.00";

NumberFormat numberFormat = NumberFormat.getInstance();
同时如果不想要千分位标示“,”的话，可以增加以下设置,如果不设置为false的话，
默认格式化之后是6,666类似这样
//numberFormat.setGroupingUsed(false);

String mNumAfter = numberFormat.format(mNum);

```


