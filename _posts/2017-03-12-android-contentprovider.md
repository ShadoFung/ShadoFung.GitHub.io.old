---
layout: post
title: "Android ContentProvider"
date: 2017-03-12
excerpt: "Content Provider，即内容提供者，Android中的Content provider机制可支持在多个应用中存储和读取数据。这也是跨应用共享数据的方式之一，还有文件，sharePreference，SQLite数据库等方式存储共享数据库，但是ContentProvider更好的提供了数据共享接口的统一性。在android系统中，没有一个公共的内存区域，供多个应用共享存储数据。"
tags: [android, ContentProvider, java]
comments: true
---

## 1 ContentProvider ##
ContentProvider在android中的作用是可以通过ContentProvider把应用中的数据共享给其他应用访问，其他应用可以通过ContentProvider对应用中的数据进行增、删、改、查。使用ContentProvider对外共享数据的好处是，统一了数据的访问方式，它实际上是对SQLiteOpenHelper的进一步封装，通过Uri映射来判断选择需要曹组哦数据库中的哪个表，并且进行增、删、改、查处理。