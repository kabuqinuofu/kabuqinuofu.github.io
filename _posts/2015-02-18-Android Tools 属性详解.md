---
layout: post
title: "Android Tools属性介绍"
date: 2015-02-18 
description: "Android Tools属性介绍"
tag: Android 
---   
安卓开发中，在写布局代码的时候，ide可以看到布局的预览效果。

但是有些效果则必须在运行之后才能看见，比如这种情况：TextView在xml中没有设置任何字符，而是在activity中设置了text。因此为了在ide中预览效果，你必须在xml中为TextView控件设置android:text属性

```
<TextView
  android:id="@+id/text_main"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:textAppearance="@style/TextAppearance.Title"
  android:layout_margin="@dimen/main_margin"
  android:text="I am a title" />
```
一般我们在这样做的时候都告诉自己，没关系，等写完代码我就把这些东西一并删了。但是你可能会忘，以至于在你的最终产品中也会有这样的代码。

####用tools吧，别做傻事

以上的情况是可以避免的，我们使用tools命名空间以及其属性来解决这个问题。

```
<TextView
 android:id="@+id/text_main"
 android:layout_width="match_parent"
 android:layout_height="wrap_content"
 android:textAppearance="@style/TextAppearance.Title"
 android:layout_margin="@dimen/main_margin"
 tools:text="I am a title" />
```
tools可以覆盖android的所有标准属性，将android:换成tools:即可。同时在运行的时候就连tools:本身都是被忽略的，不会被带进apk中。
####tools属性的种类

tools属性可以分为两种：一种是影响Lint提示的，一种是关于xml布局设计的。以上介绍的是tools的最基本用法：在UI设计的时候覆盖标准的android属性，属于第二种。下面介绍Lint相关的属性。
####Lint相关的属性

```
tools:ignore
tools:targetApi
tools:locale
```
ignore属性是告诉Lint忽略xml中的某些警告。

假设我们有这样的一个ImageView

```
<ImageView
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:layout_marginStart="@dimen/margin_main"
  android:layout_marginTop="@dimen/margin_main"
  android:scaleType="center"
  android:src="@drawable/divider" />
```

Lint会提示该ImageView缺少android:contentDescription属性。我们可以使用tools:ignore来忽略这个警告：

```
<ImageView
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:layout_marginStart="@dimen/margin_main"
  android:layout_marginTop="@dimen/margin_main"
  android:scaleType="center"
  android:src="@drawable/divider"
  tools:ignore="contentDescription" />
```

####tools:targetApi

假设minSdkLevel 15，而你使用了api21中的控件比如RippleDrawable

```
<ripple xmlns:android="http://schemas.android.com/apk/res/android"
  android:color="@color/accent_color" />
```
则Lint会提示警告。

为了不显示这个警告，可以：

```
<ripple xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  android:color="@color/accent_color"
  tools:targetApi="LOLLIPOP" />
```
####tools:locale（本地语言）属性
默认情况下res/values/strings.xml中的字符串会执行拼写检查，如果不是英语，会提示拼写错误，通过以下代码来告诉studio本地语言不是英语，就不会有提示了。

```
<resources
  xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  tools:locale="it">
 
  <!-- Your strings go here -->
 
</resources>
```
转载请注明原地址，小聪哥的博客：[http://www.wencong.com](http://http://www.wencong.com) 谢谢！
