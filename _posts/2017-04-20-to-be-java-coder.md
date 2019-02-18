---
layout: post
title: "Java工程师之路"
date: 2017-04-20
excerpt: "Java知识体系。"
tags: [java]
comments: true
---
# Java工程师之路

![](https://img.shields.io/badge/version-v2.0.0-green.svg) ![](https://img.shields.io/badge/author-Hollis-yellow.svg) ![](https://img.shields.io/badge/license-GPL-blue.svg)

## 一、基础篇

### 面向对象

#### 什么是面向对象

1. 面向对象、面向过程

2. 面向对象的三大基本特征和五大基本原则

#### 平台无关性

1. Java如何实现的平台无关

2. JVM还支持哪些语言（Kotlin、Groovy、JRuby、Jython、Scala）

#### 值传递

1. 值传递、引用传递

2. 为什么说Java中只有值传递

#### 封装、继承、多态

1. 什么是多态、方法重写与重载

2. Java的继承与实现

3. 构造函数与默认构造函数

4. 类变量、成员变量和局部变量

5. 成员变量和方法作用域

### Java基础知识

#### 基本数据类型

1. 7种基本数据类型：整型、浮点型、布尔型、字符型

2. 整型中byte、short、int、long的取值范围

3. 什么是浮点型？什么是单精度和双精度？为什么不能用浮点型表示金额？

#### 自动拆装箱

1. 什么是包装类型、什么是基本类型、什么是自动拆装箱

2. Integer的缓存机制

#### String

1. 字符串的不可变性

2. JDK 6和JDK 7中substring的原理及区别、

3. replaceFirst、replaceAll、replace区别、

4. String对“+”的重载、字符串拼接的几种方式和区别

5. String.valueOf和Integer.toString的区别、

6. switch对String的支持

7. 字符串池、常量池（运行时常量池、Class常量池）、intern

#### 熟悉Java中各种关键字

1. transient、instanceof、volatile、synchronized、final、static、const 原理及用法。

#### 集合类

1. 常用集合类的使用、ArrayList和LinkedList和Vector的区别 、SynchronizedList和Vector的区别、HashMap、HashTable、ConcurrentHashMap区别、

2. Set和List区别？Set如何保证元素不重复？

3. Java 8中stream相关用法、apache集合处理工具类的使用、不同版本的JDK中HashMap的实现的区别以及原因

4. Collection和Collections区别

5. Arrays.asList获得的List使用时需要注意什么

6. Enumeration和Iterator区别

7. fail-fast 和 fail-safe

8. CopyOnWriteArrayList、ConcurrentSkipListMap

#### 枚举

1. 枚举的用法、枚举的实现、枚举与单例、Enum类

2. Java枚举如何比较

3. switch对枚举的支持

4. 枚举的序列化如何实现

5. 枚举的线程安全性问题

#### IO

1. 字符流、字节流、输入流、输出流、

2. 同步、异步、阻塞、非阻塞、Linux 5种IO模型

3. BIO、NIO和AIO的区别、三种IO的用法与原理、netty

#### Java反射与javassist

1. 反射与工厂模式、 反射有什么作用

2. Class类

3. `java.lang.reflect.*`

#### 动态代理

1. 静态代理、动态代理

2. 动态代理和反射的关系

3. 动态代理的几种实现方式

4. AOP

#### 序列化

1. 什么是序列化与反序列化、为什么序列化、序列化底层原理、序列化与单例模式、protobuf、为什么说序列化并不安全

#### 注解

1. 元注解、自定义注解、Java中常用注解使用、注解与反射的结合

2. Spring常用注解

#### JMS

1. 什么是Java消息服务、JMS消息传送模型

#### JMX

1. `java.lang.management.*`、 `javax.management.*`

#### 泛型

1. 泛型与继承、类型擦除、泛型中K T V E ？ object等的含义、泛型各种用法

2. 限定通配符和非限定通配符、上下界限定符extends 和 super

3. List<Object>和原始类型List之间的区别?

4. List<?>和List<Object>之间的区别是什么?

#### 单元测试

1. junit、mock、mockito、内存数据库（h2）

#### 正则表达式

1. `java.lang.util.regex.*`

#### 常用的Java工具库

1. `commons.lang`, `commons.*...` `guava-libraries` `netty`

#### API&SPI

1. API、API和SPI的关系和区别

2. 如何定义SPI、SPI的实现原理

#### 异常

1. 异常类型、正确处理异常、自定义异常

2. Error和Exception

3. 异常链、try-with-resources

4. finally和return的执行顺序

#### 时间处理

1. 时区、冬令时和夏令时、时间戳、Java中时间API

2. 格林威治时间、CET,UTC,GMT,CST几种常见时间的含义和关系

3. SimpleDateFormat的线程安全性问题

4. Java 8中的时间处理

5. 如何在东八区的计算机上获取美国时间

#### 编码方式

1. Unicode、有了Unicode为啥还需要UTF-8

2. GBK、GB2312、GB18030之间的区别

3. UTF8、UTF16、UTF32区别

4. URL编解码、Big Endian和Little Endian

5. 如何解决乱码问题

#### 语法糖

1. Java中语法糖原理、解语法糖

2. 语法糖：switch 支持 String 与枚举、泛型、自动装箱与拆箱、方法变长参数、枚举、内部类、条件编译、 断言、数值字面量、for-each、try-with-resource、Lambda表达式、

### 阅读源代码

1. String、Integer、Long、Enum、BigDecimal、ThreadLocal、ClassLoader & URLClassLoader、ArrayList & LinkedList、 HashMap & LinkedHashMap & TreeMap & CouncurrentHashMap、HashSet & LinkedHashSet & TreeSet

### Java并发编程

#### 并发与并行

1. 什么是并发

2. 什么是并行

3. 并发与并行的区别

#### 线程

1. 线程的实现、线程的状态、优先级、线程调度、创建线程的多种方式、守护线程

2. 线程与进程的区别

#### 线程池

1. 自己设计线程池、submit() 和 execute()、线程池原理

2. 为什么不允许使用Executors创建线程池

#### 线程安全

1. 死锁、死锁如何排查、线程安全和内存模型的关系

#### 锁

1. CAS、乐观锁与悲观锁、数据库相关锁机制、分布式锁、偏向锁、轻量级锁、重量级锁、monitor、

2. 锁优化、锁消除、锁粗化、自旋锁、可重入锁、阻塞锁、死锁

#### 死锁

1. 死锁的原因

2. 死锁的解决办法

#### synchronized

1. synchronized是如何实现的？

2. synchronized和lock之间关系、不使用synchronized如何实现一个线程安全的单例

3. synchronized和原子性、可见性和有序性之间的关系

#### volatile

1. happens-before、内存屏障、编译器指令重排和CPU指令重排

2. volatile的实现原理

3. volatile和原子性、可见性和有序性之间的关系

4. 有了symchronized为什么还需要volatile

#### sleep 和 wait

#### wait 和 notify

#### notify 和 notifyAll

#### ThreadLocal

#### 写一个死锁的程序

#### 写代码来解决生产者消费者问题

### 并发包

#### 阅读源代码，并学会使用

1. Thread、Runnable、Callable、ReentrantLock、ReentrantReadWriteLock、Atomic*、Semaphore、CountDownLatch、、ConcurrentHashMap、Executors

## 二、底层篇

### JVM

#### JVM内存结构

1. class文件格式、运行时数据区：堆、栈、方法区、直接内存、运行时常量池、

2. 堆和栈区别

3. Java中的对象一定在堆上分配吗？

#### Java内存模型

1. 计算机内存模型、缓存一致性、MESI协议

2. 可见性、原子性、顺序性、happens-before、

3. 内存屏障、synchronized、volatile、final、锁

#### 垃圾回收

1. GC算法：标记清除、引用计数、复制、标记压缩、分代回收、增量式回收

2. GC参数、对象存活的判定、垃圾收集器（CMS、G1、ZGC、Epsilon）

#### JVM参数及调优

1. -Xmx、-Xmn、-Xms、Xss、-XX:SurvivorRatio、

2. -XX:PermSize、-XX:MaxPermSize、-XX:MaxTenuringThreshold

#### Java对象模型

1. oop-klass、对象头

#### HotSpot

1. 即时编译器、编译优化

#### 虚拟机性能监控与故障处理工具

1. jps, jstack, jmap、jstat, jconsole, jinfo, jhat, javap, btrace、TProfiler

2. Arthas

### 类加载机制

1. classLoader、类加载过程、双亲委派（破坏双亲委派）、模块化（jboss modules、osgi、jigsaw）

### 编译与反编译

1. 什么是编译（前端编译、后端编译）、什么是反编译

2. JIT、JIT优化（逃逸分析、栈上分配、标量替换、锁优化）

3. 编译工具：javac

4. 反编译工具：javap 、jad 、CRF

## 三、 进阶篇

### Java底层知识

#### 字节码、class文件格式

#### CPU缓存，L1，L2，L3和伪共享

#### 尾递归

#### 位运算

1. 用位运算实现加、减、乘、除、取余

### 设计模式

1. 设计模式的六大原则：

1. 开闭原则（Open Close Principle）、里氏代换原则（Liskov Substitution Principle）、依赖倒转原则（Dependence Inversion Principle）

2. 接口隔离原则（Interface Segregation Principle）、迪米特法则（最少知道原则）（Demeter Principle）、合成复用原则（Composite Reuse Principle）

#### 了解23种设计模式

1. 创建型模式：单例模式、抽象工厂模式、建造者模式、工厂模式、原型模式。

2. 结构型模式：适配器模式、桥接模式、装饰模式、组合模式、外观模式、享元模式、代理模式。

3. 行为型模式：模版方法模式、命令模式、迭代器模式、观察者模式、中介者模式、备忘录模式、解释器模式（Interpreter模式）、状态模式、策略模式、职责链模式(责任链模式)、访问者模式。

#### 会使用常用设计模式

1. 单例的七种写法：懒汉——线程不安全、懒汉——线程安全、饿汉、饿汉——变种、静态内部类、枚举、双重校验锁

2. 工厂模式、适配器模式、策略模式、模板方法模式、观察者模式、外观模式、代理模式等必会

#### 不用synchronized和lock，实现线程安全的单例模式

#### 实现AOP

#### 实现IOC

#### nio和reactor设计模式

### 网络编程知识

#### tcp、udp、http、https等常用协议

1. 三次握手与四次关闭、流量控制和拥塞控制、OSI七层模型、tcp粘包与拆包

#### http/1.0 http/1.1 http/2之间的区别

1. http中 get和post区别

2. 常见的web请求返回的状态码

3. 404、302、301、500分别代表什么

#### http/3

#### Java RMI，Socket，HttpClient

#### cookie 与 session

1. cookie被禁用，如何实现session

#### 用Java写一个简单的静态文件的HTTP服务器

#### 了解nginx和apache服务器的特性并搭建一个对应的服务器

#### 用Java实现FTP、SMTP协议

#### 进程间通讯的方式

#### 什么是CDN？如果实现？

#### DNS？

1. 什么是DNS 、记录类型:A记录、CNAME记录、AAAA记录等

2. 域名解析、根域名服务器

3. DNS污染、DNS劫持、公共DNS：114 DNS、Google DNS、OpenDNS

#### 反向代理

1. 正向代理、反向代理

2. 反向代理服务器

### 框架知识

#### Servlet

1. 生命周期

2. 线程安全问题

3. filter和listener

4. web.xml中常用配置及作用

#### Hibernate

1. 什么是OR Mapping

2. Hibernate的缓存机制

3. Hibernate的懒加载

4. Hibernate/Ibatis/MyBatis之间的区别

#### Spring

1. Bean的初始化

2. AOP原理

3. 实现Spring的IOC

4. spring四种依赖注入方式

#### Spring MVC

1. 什么是MVC

2. Spring mvc与Struts mvc的区别

#### Spring Boot

1. Spring Boot 2.0、起步依赖、自动配置、

2. Spring Boot的starter原理，自己实现一个starter

#### Spring Security

### Spring Cloud

1. 服务发现与注册：Eureka、Zookeeper、Consul

2. 负载均衡：Feign、Spring Cloud Loadbalance

3. 服务配置：Spring Cloud Config

4. 服务限流与熔断：Hystrix

5. 服务链路追踪：Dapper

6. 服务网关、安全、消息

### 应用服务器知识

#### JBoss

#### tomcat

#### jetty

#### Weblogic

### 工具

#### git & svn

#### maven & gradle

#### Intellij IDEA

1. 常用插件：Maven Helper 、FindBugs-IDEA、阿里巴巴代码规约检测、GsonFormat、aceJump

2. Lombok plugin、.ignore、Mybatis plugin

## 四、 高级篇

### 新技术

#### Java 8

1. lambda表达式、Stream API、时间API

#### Java 9

1. Jigsaw、Jshell、Reactive Streams

#### Java 10

1. 局部变量类型推断、G1的并行Full GC、ThreadLocal握手机制

#### Java 11

1. ZGC、Epsilon、增强var、

#### Spring 5

1. 响应式编程

#### Spring Boot 2.0

### http/2

### http/3

### 性能优化

1. 使用单例、使用Future模式、使用线程池、选择就绪、减少上下文切换、减少锁粒度、数据压缩、结果缓存

### 线上问题分析

#### dump获取

1. 线程Dump、内存Dump、gc情况

#### dump分析

1. 分析死锁、分析内存泄露

#### dump分析及获取工具

1. jstack、jstat、jmap、jhat、Arthas

#### 自己编写各种outofmemory，stackoverflow程序

1. HeapOutOfMemory、 Young OutOfMemory、MethodArea OutOfMemory、ConstantPool OutOfMemory、DirectMemory OutOfMemory、Stack OutOfMemory Stack OverFlow

#### Arthas

1. jvm相关、class/classloader相关、monitor/watch/trace相关、

2. options、管道、后台异步任务

3. 文档：https://alibaba.github.io/arthas/advanced-use.html

#### 常见问题解决思路

1. 内存溢出、线程死锁、类加载冲突

#### 使用工具尝试解决以下问题，并写下总结

1. 当一个Java程序响应很慢时如何查找问题、

2. 当一个Java程序频繁FullGC时如何解决问题、

3. 如何查看垃圾回收日志、

4. 当一个Java应用发生OutOfMemory时该如何解决、

5. 如何判断是否出现死锁、

6. 如何判断是否存在内存泄露

7. 使用Arthas快速排查Spring Boot应用404/401问题

8. 使用Arthas排查线上应用日志打满问题

9. 利用Arthas排查Spring Boot应用NoSuchMethodError

### 编译原理知识

#### 编译与反编译

#### Java代码的编译与反编译

#### Java的反编译工具

1. javap 、jad 、CRF

#### 即时编译器

#### 词法分析，语法分析（LL算法，递归下降算法，LR算法），语义分析，运行时环境，中间代码，代码生成，代码优化

### 操作系统知识

#### Linux的常用命令

#### 进程间通信

#### 进程同步

1. 生产者消费者问题、哲学家就餐问题、读者写者问题

#### 缓冲区溢出

#### 分段和分页

#### 虚拟内存与主存

#### 虚拟内存管理

#### 换页算法

### 数据库知识

#### MySql 执行引擎

#### MySQL 执行计划

1. 如何查看执行计划，如何根据执行计划进行SQL优化

#### 索引

1. Hash索引、B树索引（B+树、和B树、R树）

2. 普通索引、唯一索引

3. 覆盖索引、最左前缀原则、索引下推

#### SQL优化

#### 数据库事务和隔离级别

1. 事务的隔离级别、事务能不能实现锁的功能

#### 数据库锁

1. 行锁、表锁、使用数据库锁实现乐观锁、

#### 连接

1. 内连接，左连接，右连接

#### 数据库主备搭建

#### binlog

#### redolog

#### 内存数据库

1. h2

#### 分库分表

#### 读写分离

#### 常用的nosql数据库

1. redis、memcached

#### 分别使用数据库锁、NoSql实现分布式锁

#### 性能调优

#### 数据库连接池

### 数据结构与算法知识

#### 简单的数据结构

1. 栈、队列、链表、数组、哈希表、

2. 栈和队列的相同和不同之处

3. 栈通常采用的两种存储结构

#### 树

1. 二叉树、字典树、平衡树、排序树、B树、B+树、R树、多路树、红黑树

#### 堆

1. 大根堆、小根堆

#### 图

1. 有向图、无向图、拓扑

#### 排序算法

1. 稳定的排序：冒泡排序、插入排序、鸡尾酒排序、桶排序、计数排序、归并排序、原地归并排序、二叉排序树排序、鸽巢排序、基数排序、侏儒排序、图书馆排序、块排序

2. 不稳定的排序：选择排序、希尔排序、Clover排序算法、梳排序、堆排序、平滑排序、快速排序、内省排序、耐心排序

3. 各种排序算法和时间复杂度

#### 深度优先和广度优先搜索

#### 全排列、贪心算法、KMP算法、hash算法

#### 海量数据处理

1. 分治，hash映射，堆排序，双层桶划分，Bloom Filter，bitmap，数据库索引，mapreduce等。

#### 两个栈实现队列，和两个队列实现栈

### 大数据知识

#### Zookeeper

1. 基本概念、常见用法

#### Solr，Lucene，ElasticSearch

1. 在linux上部署solr，solrcloud，，新增、删除、查询索引

#### Storm，流式计算，了解Spark，S4

1. 在linux上部署storm，用zookeeper做协调，运行storm hello world，local和remote模式运行调试storm topology。

#### Hadoop，离线计算

1. HDFS、MapReduce

#### 分布式日志收集flume，kafka，logstash

#### 数据挖掘，mahout

### 网络安全知识

#### XSS

1. XSS的防御

#### CSRF

#### 注入攻击

1. SQL注入、XML注入、CRLF注入

#### 文件上传漏洞

#### 加密与解密

1. 对称加密、非对称加密、哈希算法、加盐哈希算法

2. MD5，SHA1、DES、AES、RSA、DSA

3. 彩虹表

#### DDOS攻击

1. DOS攻击、DDOS攻击

1. memcached为什么可以导致DDos攻击、什么是反射型DDoS

1. 如何通过Hash碰撞进行DOS攻击

#### SSL、TLS，HTTPS

#### 用openssl签一个证书部署到apache或nginx

## 五、架构篇

### 分布式

1. 数据一致性、服务治理、服务降级

#### 分布式事务

1. 2PC、3PC、CAP、BASE、 可靠消息最终一致性、最大努力通知、TCC

#### Dubbo

1. 服务注册、服务发现，服务治理

2. http://dubbo.apache.org/zh-cn/

#### 分布式数据库

1. 怎样打造一个分布式数据库、什么时候需要分布式数据库、mycat、otter、HBase

#### 分布式文件系统

1. mfs、fastdfs

#### 分布式缓存

1. 缓存一致性、缓存命中率、缓存冗余

#### 限流降级

1. Hystrix、Sentinal

#### 算法

1. 共识算法、Raft协议、Paxos 算法与 Raft 算法、拜占庭问题与算法

2. 2PC、3PC

### 微服务

1. SOA、康威定律

#### ServiceMesh

1. sidecar

#### Docker & Kubernets

#### Spring Boot

#### Spring Cloud

### 高并发

#### 分库分表

#### CDN技术

#### 消息队列

1. ActiveMQ

### 监控

#### 监控什么

1. CPU、内存、磁盘I/O、网络I/O等

#### 监控手段

1. 进程监控、语义监控、机器资源监控、数据波动

#### 监控数据采集

1. 日志、埋点

#### Dapper

### 负载均衡

1. tomcat负载均衡、Nginx负载均衡

2. 四层负载均衡、七层负载均衡

### DNS

1. DNS原理、DNS的设计

### CDN

1. 数据一致性

## 六、 扩展篇

### 云计算

1. IaaS、SaaS、PaaS、虚拟化技术、openstack、Serverlsess

### 搜索引擎

1. Solr、Lucene、Nutch、Elasticsearch

### 权限管理

1. Shiro

### 区块链

1. 哈希算法、Merkle树、公钥密码算法、共识算法、Raft协议、Paxos 算法与 Raft 算法、拜占庭问题与算法、消息认证码与数字签名

#### 比特币

1. 挖矿、共识机制、闪电网络、侧链、热点问题、分叉

#### 以太坊

#### 超级账本

### 人工智能

1. 数学基础、机器学习、人工神经网络、深度学习、应用场景。

#### 常用框架

1. TensorFlow、DeepLearning4J

### IoT

### 量子计算

### AR & VR

### 其他语言

1. Groovy、Python、Go、NodeJs、Swift、Rust

## 六、 推荐书籍

1. 《深入理解Java虚拟机》
2. 《Effective Java》
3. 《深入分析Java Web技术内幕》
4. 《大型网站技术架构》
5. 《代码整洁之道》
6. 《架构整洁之道》
7. 《Head First设计模式》
8. 《maven实战》
9. 《区块链原理、设计与应用》
10. 《Java并发编程实战》
11. 《鸟哥的Linux私房菜》
12. 《从Paxos到Zookeeper》
13. 《架构即未来》

-------------
