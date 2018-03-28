---
layout: post
title: "Android Service"
date: 2017-02-12
excerpt: "Service是Android系统中的四大组件之一，它是一种长生命周期的，没有可视化界面，运行于后台的一种服务程序。"
tags: [android, service, java]
comments: true
---

## 1 Service与AIDL ##
Service是Android中实现程序后台运行的解决方案，适合用于那些不需要和用户交互而且还要求长期运行的任务。但不要被“后台”二字所迷惑，Service默认并不会运行在子线程中，它也不运行在一个独立的进程中，它同样执行在UI线程中，因此，不要在Service中执行耗时的操作，除非你在Service中创建了子线程来完成耗时操作。

Service的运行不依赖于任何用户界面，即使程序被切换到后台或者用户打开了另一个应用程序，Service仍然能够保持正常运行，这也正是Service的使用场景。当某个应用程序进程被杀掉时，所有依赖于该进程的Service也会停止运行。
### 1.1 普通Service ###
Service的生命周期只有三个，分别为**onCreate**、**onStartCommand**和**onDestory**。一旦在项目的任何位置调用了Context的startService()函数，相应的服务就会启动起来，首次创建时会调用onCreate函数，然后回调onStartCommand()函数。服务启动之后会一直保持运行状态，直到stopService()或stopSelf()函数被调用。虽然每调用一次startService()函数，onStartCommand()就会执行一次，但实际上每个服务都只会存在一个实例。所以不管你调用了多少次startService()函数，只需调用一个stopService()或stopSelf()函数，服务就会被停止。

与Activity一样，Service也需要在AndroidManifest.xml中进行注册。

### 1.2 IntentService ###
IntentService将用户的请求执行在一个子线程中，用户只需要覆写onHandleIntent函数，并且在该函数中完成自己的耗时操作即可。需要注意的是，在任务执行完毕之后IntentService会调用stopSelf自我销毁，因此，它适用于完成一些短期的耗时任务。

### 1.3 运行在前台的Service ###
将Service运行在前台不仅不会被系统无情地回收，它还会在通知栏显示一条消息，下拉状态栏后可以看到更加详细的信息。例如，墨迹天气在前台运行了一个Service，并且在Service中定时更新通知栏上的天气信息。

### 1.4 AIDL ###
Android Interface Definition Language(Android接口定义语言)，同行用于进程间通信（Android系统中的进程之间不能共享内存）。  

Note: Using AIDL is necessary only if you allow clients from different applications to access your service for IPC and want to handle multithreading in your service. If you do not need to perform concurrent IPC across different applications, you should create your interface by implementing a Binder or, if you want to perform IPC, but do not need to handle multithreading, implement your interface using a Messenger. Regardless, be sure that you understand Bound Services before implementing an AIDL.

“只有当你允许来自不同的客户端访问你的服务并且需要处理多线程问题时你才必须使用AIDL”，其他情况下你都可以选择其他方法，如使用Messager，也能跨进程通讯。可见AIDL是处理多线程、多客户端并发访问的。而Messager是单线程处理。