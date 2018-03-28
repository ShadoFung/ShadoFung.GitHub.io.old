---
layout: post
title: "Android Activity"
date: 2017-02-02
excerpt: "Activity是Android组件中最基本也是最为常见用的四大组件（Activity，Service服务,Content Provider内容提供者，BroadcastReceiver广播接收器）之一。
Activity通常就是一个屏幕，可以显示一些控件也可以监听并处理用户的事件做出响应。"
tags: [android, java]
comments: true
---
## 1.1 Activity ##
### 1.1.1 Activity的生命周期 ###
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/android_activity/actiVity_lifecycle.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/android_activity/activity_lifecycle.png"></a>
	<figcaption>Activity的生命周期</figcaption>
</figure>
**1.onCreate()**

onCreate()方法会在Activity第一次被创建时调用，通常会在这个函数中完成Activity的初始化操作，如设置布局、初始化视图、绑定事件等。

**2.onStart()**

这个函数在Activity可见之前被调用。

**3.onResume()**

这个函数在Activity变为可见时被调用，执行完onResume之后，Activity就会请求AMS渲染它所管理的视图。此时的Activity一定位于返回栈的栈顶，并且处于运行状态。可见的、有焦点的。

**4.onPause()**

这个函数在Activity失去焦点，从可见变为不完全可见时调用。

**5.onStop()**

这个函数在Activity完全不可见时调用。

**6.onDestroy()**

这个函数在Activity被销毁之前调用，之后Activity的状态变为销毁状态。在这个函数里释放内存。

**7.onRestart()**

这个函数在Activity由停止状态重新变为运行状态之前调用，下一个调用onStart()。

###1.1.2 Activity的构成 ###
PhoneWindow→DecorView→DefultLayout→ViewGroup:mContentParent→用户自己的xml布局
### 1.1.3 Activity的4种启动模式 ###
**1.standard**

在这种模式下启动的Activity可以被多次实例化，每启动一个Activity都会在栈顶创建一个新的实例。实际开发中，闹钟程序通常使采用这种模式。如果Activity是一个非常耗资源的类，那么将会使应用消耗更多的系统资源。

**2.singleTop**

singleTop模式启动Activity时，首先会判断要启动Acitity实例是否位于栈顶，如果位于栈顶则直接复用，否则与standard模式相同，创建一个新的实例。实际开发中，浏览器的书签通常采用这种模式。

**3.singleTask**

singleTask模式可以保证一个任务栈中只能有一个该Activity实例。每次启动该Activity时，首先会判断该Acitivity是否存在任务栈中，如果已存在，系统会销毁该Activity之上的所有Activity实例，最终让该Activity实例位于栈顶。如果任务栈中没有该Activity实例，会新创建一个实例并放在栈顶。在实际开发中，浏览器主界面通常采用这种模式。

**4.singleInstance**

设置为singleInstance模式的Activity会启动一个独立的任务栈来管理Activity实例，并且这个任务栈中有且只有一个实例。如果要启动的Activity已存在，无论当前Activity位于哪个程序哪个任务栈中，系统都会把Activity所在的任务栈转移到前台，从而使Activity显示。实际开发中，来电界面通常采用这种模式。