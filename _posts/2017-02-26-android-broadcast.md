---
layout: post
title: "Android Broadcast"
date: 2017-02-26
excerpt: "Broadcast即广播，是一个全局的监听器，属于Android四大组件之一,作用是监听 / 接收 应用 App 发出的广播消息，并做出相应的响应"
tags: [android, service, java]
comments: true
---

## 1.3 Broadcast(广播) ##
Broadcast是一种广泛运用的、在应用程序之间传输信息的机制，一个广播可以有任意个接收者。广播机制是一个典型的发布——订阅模式，最大的特点就是发送方不关心接收方是否接到数据，也不关心是如何处理数据的，通过这样的形式来达到接、收双方的完全解耦合。

Android中的广播使用了**设计模式**中的**观察者模式**：基于消息的发布 / 订阅事件模型

Android广播机制包含3个基本要素，分别是用于发送广播的Broadcast、接收广播的BroadcastReceiver以及用于传递信息的Intent。Android广播可分为普通广播、有序广播、本地广播和Sticky。

### 1.3.1 普通广播 ###
  普通广播是完全**异步**的，通过Context的sendBroadcast()函数发送，
**优点**：消息传递的效率比较高。
**缺点**：receivers(接收器)的执行顺序不确定，接收者不能讲处理结果传递给下一个接收者，并且无法终止广播Intent的传播，直到没有与之匹配的广播接收器为止。
1、首先定义一个广播接收器，如下：
{% highlight java %}
public class HelloBroadcastReceiver extends BroadcaseReceiver {
	@Override
	public void onReceive(Context context, Intent intent) {
		Toast.makeText（context, "hello", Toast.LENGTH_LONG).show();
	}
}
{% endhighlight %}
2、注册广播，可以通过AndroidManifest.xml静态注册或者代码动态注册。

AndroidManifest.xml静态注册：
`<receiver android:name=".broadcast.HelloBroadcastReceiver"></receiver>`

代码动态注册：
{% highlight java %}
private void registerHelloBroadcast() {
	registerReceiver(new HelloBroadcastReceiver(), new IntentFilter(HELLO_ACTION));
}
{% endhighlight %}

如果是在Activity或者Fragment中动态测试，那么不要忘了在执行onDestory时注销该广播。

3、发送广播
{% highlight java %}
private void sendNormalBroadcast() {
	sendBroadcast(new Intent(HELLO_ACTION));
}
{% endhighlight %}
然后就会调用HelloBroadcastReceiver的onReceive函数，在该函数中执行相关操作即可。

### 1.3.2 有序广播 ###
有序广播通过Context.sendOrderedBroadcast()来发送，所有的广播接收器按照优先级依次执行，广播接收器的优先级通过AndroidManifest.xml中的receiver的intent-filter中的android:priority属性来设置，数值越大优先级越高。当广播接收器接收到广播后，可以使用setResult()函数来将结果传给下一个广播接收器接收，然后通过getResult()函数来取得上个广播接收器返回的结果，并可以用abortBroadcast()函数来让系统丢弃该广播，使该广播不再传送到别的广播接收器。

### 1.3.3 本地广播 ###
之前的广播都是全局的，所有应用程序都可以接收到，这样就会带来安全隐患。
LocalBroadcastManager能够实现限于应用内的广播，只是进程内使用，提高程序的安全性。

### 1.3.4 sticky广播 ###
sticky广播通过Context.sendStickyBroadcast()函数来发送，用此函数发送的广播会一直滞留，当有匹配此广播的广播接收器被注册后，该广播接收器就会收到此条广播。使用此函数发送广播时，需要获得BROADCAST_STICKY权限：

`<uses-permission android:name="android.permission.BROADCAST_STICKY" />`

sendStickyBroadcast只保留最后一条广播，并且一直保留下去，这样即使已经有广播接收器处理了该广播，当再有匹配的广播接收器被注册时，此广播仍会被接收。如果你只想处理一遍该广播，可以通过removeStickyBroadcast函数实现。