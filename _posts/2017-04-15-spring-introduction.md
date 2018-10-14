---
layout: post
title: "Spring"
date: 2017-04-15
excerpt: "Spring是一个开放源代码的设计层面框架，他解决的是业务逻辑层和其他各层的松耦合问题，因此它将面向接口的编程思想贯穿整个系统应用。Spring是于2003 年兴起的一个轻量级的Java 开发框架，由Rod Johnson创建。简单来说，Spring是一个分层的JavaSE/EE full-stack(一站式) 轻量级开源框架。"
tags: [spring, java]
comments: true
---
## 	Why
为什么要使用Spring？

Spring主要两个有功能为我们的业务对象管理提供了非常便捷的方法：

- DI（Dependency Injection，依赖注入）
- AOP（Aspect Oriented Programming，面向切面编程）

### Java Bean

每一个类实现了Bean的规范才可以由Spring来接管，那么Bean的规范是什么呢？

- 必须是个公有(public)类
- 有无参构造函数
- 用公共方法暴露内部成员属性(getter,setter)

实现这样规范的类，被称为Java Bean。即是一种可重用的组件。

### DI-依赖注入
简单来说，一个系统中可能会有成千上万个对象。如果要手工维护它们之间的关系，这是不可想象的。我们可以在Spring的XML文件描述它们之间的关系，由Spring自动来注入它们——比如A类的实例需要B类的实例作为参数set进去。

### AOP-面向切面编程
就以日志系统为例。在执行某个操作前后都需要输出日志，如果手工加代码，那简直太可怕了。而且等代码庞大起来，也是非常难维护的一种情况。这里就需要面向切面来编程

##  How
### 关于Bean
#### Bean的生命周期

如你所见，在bean准备就绪之前，bean工厂执行了若干启动步骤。我们对图进行详细描述：

1. Spring对bean进行实例化；
2. Spring将值和bean的引用注入到bean对应的属性中；
3. 如果bean实现了BeanNameAware接口，Spring将bean的ID传递给setBean-Name()方法；
4. 如果bean实现了BeanFactoryAware接口，Spring将调用setBeanFactory()方法，将BeanFactory容器实例传入；
5. 如果bean实现了ApplicationContextAware接口，Spring将调用setApplicationContext()方法，将bean所在的应用上下文的引用传入进来；
6. 如果bean实现了BeanPostProcessor接口，Spring将调用它们的post-ProcessBeforeInitialization()方法；
7. 如果bean实现了InitializingBean接口，Spring将调用它们的after-PropertiesSet()方法。类似地，如果bean使用init-method声明了初始化方法，该方法也会被调用；
8. 如果bean实现了BeanPostProcessor接口，Spring将调用它们的post-ProcessAfterInitialization()方法；
9. 此时，bean已经准备就绪，可以被应用程序使用了，它们将一直驻留在应用上下文中，直到该应用上下文被销毁；
10. 如果bean实现了DisposableBean接口，Spring将调用它的destroy()接口方法。同样，如果bean使用destroy-method声明了销毁方法，该方法也会被调用。

#### Bean的作用域

Spring定义了多种Bean作用域，可以基于这些作用域创建bean，包括：

- 单例（Singleton）：在整个应用中，只创建bean的一个实例。
- 原型（Prototype）：每次注入或者通过Spring应用上下文获取的时候，都会创建一个新的bean实例。
- 会话（Session）：在Web应用中，为每个会话创建一个bean实例。
- 请求（Rquest）：在Web应用中，为每个请求创建一个bean实例。

在代码里看起来是这样的：
{% highlight java %}
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class MyIsBean{...}
{% endhighlight %}
XML版本：  
{% highlight html %}
<bean id="BEANID"
  class = "net.itxm.beans"
  scope="prototype"
>
{% endhighlight %}
在默认情况下，Spring应用上下文中所有bean都是作为以单例（singleton）的形式创建的。也就是说，不管给定的一个bean被注入到其他bean多少次，每次所注入的都是同一个实例。

在大多数情况下，单例bean是很理想的方案。初始化和垃圾回收对象实例所带来的成本只留给一些小规模任务，在这些任务中，让对象保持无状态并且在应用中反复重用这些对象可能并不合理。

有时候，可能会发现，你所使用的类是易变的（mutable），它们会保持一些状态，因此重用是不安全的。在这种情况下，将class声明为单例的bean就不是什么好主意了，因为对象会被污染，稍后重用的时候会出现意想不到的问题。

#### 声明Bean

以下是声明Bean的注解：

- @Component 组件，没有明确的角色
- @Service 在业务逻辑层使用
- @Repository 在数据访问层使用
- @Controller 在展现层使用(MVC -> Spring MVC)使用
- 在这里，可以指定bean的id名：Component(“yourBeanName”)
- 同时，Spring支持将@Named作为@Component注解的替代方案。两者之间有一些细微的差异，但是在大多数场景中，它们是可以互相替换的。

### 关于依赖注入

#### 注入Bean的注解

**@Autowired Spring提供的注解**

不仅仅是对象，还有在构造器上，还能用在属性的Setter方法上。

不管是构造器、Setter方法还是其他的方法，Spring都会尝试满足方法参数上所声明的依赖。假如有且只有一个bean匹配依赖需求的话，那么这个bean将会被装配进来。

如果没有匹配的bean，那么在应用上下文创建的时候，Spring会抛出一个异常。为了避免异常的出现，你可以将@Autowired的required属性设置为false。

将required属性设置为false时，Spring会尝试执行自动装配，但是如果没有匹配的bean的话，Spring将会让这个bean处于未装配的状态。但是，把required属性设置为false时，你需要谨慎对待。如果在你的代码中没有进行null检查的话，这个处于未装配状态的属性有可能会出现NullPointerException。

`@Inject`注解来源于Java依赖注入规范，该规范同时还为我们定义了@Named注解。在自动装配中，Spring同时支持`@Inject`和`@Autowired`。尽管`@Inject`和`@Autowired`之间有着一些细微的差别，但是在大多数场景下，它们都是可以互相替换的。

`@Autowired` 是最常见的注解之一，但在老项目中，你可能会看到这些注解，它们的作用和`@Autowired` 相近：

`@Inject` 是JSR-330提供的注解
`@Resource` 是JSR-250提供的注解

#### 条件化的Bean

假设你希望一个或多个bean只有在应用的类路径下包含特定的库时才创建。或者我们希望某个bean只有当另外某个特定的bean也声明了之后才会创建。我们还可能要求只有某个特定的环境变量设置之后，才会创建某个bean。

在Spring 4之前，很难实现这种级别的条件化配置，但是Spring 4引入了一个新的@Conditional注解，它可以用到带有@Bean注解的方法上。如果给定的条件计算结果为true，就会创建这个bean，否则的话，这个bean会被忽略。

通过ConditionContext，我们可以做到如下几点：

- 借助getRegistry()返回的BeanDefinitionRegistry检查bean定义；
- 借助getBeanFactory()返回的ConfigurableListableBeanFactory检查bean是否存在，甚至探查bean的属性；
- 借助getEnvironment()返回的Environment检查环境变量是否存在以及它的值是什么；
- 读取并探查getResourceLoader()返回的ResourceLoader所加载的资源；
- 借助getClassLoader()返回的ClassLoader加载并检查类是否存在。

#### 处理自动装配的歧义性

**标示首选的bean**

在声明bean的时候，通过将其中一个可选的bean设置为首选（primary）bean能够避免自动装配时的歧义性。当遇到歧义性的时候，Spring将会使用首选的bean，而不是其他可选的bean。实际上，你所声明就是“最喜欢”的bean。

**限定自动装配的bean**

设置首选bean的局限性在于@Primary无法将可选方案的范围限定到唯一一个无歧义性的选项中。它只能标示一个优先的可选方案。当首选bean的数量超过一个时，我们并没有其他的方法进一步缩小可选范围。

与之相反，Spring的限定符能够在所有可选的bean上进行缩小范围的操作，最终能够达到只有一个bean满足所规定的限制条件。如果将所有的限定符都用上后依然存在歧义性，那么你可以继续使用更多的限定符来缩小选择范围。

`@Qualifier`注解是使用限定符的主要方式。它可以与`@Autowired`和`@Inject`协同使用，在注入的时候指定想要注入进去的是哪个bean。例如，我们想要确保要将IceCream注入到setDessert()之中：

{% highlight java %}
@Autowired
@Qualifier("iceCream")
public void setDessert(Dessert dessert){
  this.dessert = dessert;
}
{% endhighlight %}

这是使用限定符的最简单的例子。为`@Qualifier`注解所设置的参数就是想要注入的bean的ID。所有使用`@Component`注解声明的类都会创建为bean，并且bean的ID为首字母变为小写的类名。因此，`@Qualifier(“iceCream”)`指向的是组件扫描时所创建的bean，并且这个bean是IceCream类的实例。

实际上，还有一点需要补充一下。更准确地讲，`@Qualifier(“iceCream”)`所引用的bean要具有String类型的“iceCream”作为限定符。如果没有指定其他的限定符的话，所有的bean都会给定一个默认的限定符，这个限定符与bean的ID相同。因此，框架会将具有“iceCream”限定符的bean注入到setDessert()方法中。这恰巧就是ID为iceCream的bean，它是IceCream类在组件扫描的时候创建的。

基于默认的bean ID作为限定符是非常简单的，但这有可能会引入一些问题。如果你重构了IceCream类，将其重命名为Gelato的话，那此时会发生什么情况呢？如果这样的话，bean的ID和默认的限定符会变为gelato，这就无法匹配setDessert()方法中的限定符。自动装配会失败。

这里的问题在于setDessert()方法上所指定的限定符与要注入的bean的名称是紧耦合的。对类名称的任意改动都会导致限定符失效。

#### SpringEL

- Value实现资源的注入  

#### Bean的初始化和销毁

- Java配置方式：initMethod和destoryMethod
- 注解：@PostConstruct和@PreDestory

#### Profile

提供在不同的环境下使用不同的配置

**激活Profile**

Spring在确定哪个profile处于激活状态时，需要依赖两个独立的属性：spring.profiles.active和spring.profiles.default。如果设置了spring.profiles.active属性的话，那么它的值就会用来确定哪个profile是激活的。但如果没有设置spring.profiles.active属性的话，那Spring将会查找spring.profiles.default的值。如果spring.profiles.active和spring.profiles.default均没有设置的话，那就没有激活的profile，因此只会创建那些没有定义在profile中的bean。

**使用profile进行测试**

当运行集成测试时，通常会希望采用与生产环境（或者是生产环境的部分子集）相同的配置进行测试。但是，如果配置中的bean定义在了profile中，那么在运行测试时，我们就需要有一种方式来启用合适的profile。

Spring提供了`@ActiveProfiles`注解，我们可以使用它来指定运行测试时要激活哪个profile。在集成测试时，通常想要激活的是开发环境的profile。

比如`Profile(“dev”)`

#### Application Event

使用Application Event可以做到Bean与Bean之间的通信

Spring的事件需要遵循如下流程：

- 自定义事件，集成ApplicationEvent
- 定义事件监听器，实现ApplicationListener
- 使用容器发布事件

### 关于AOP
#### 名词介绍

**通知（Advice）**

通知定义了切面是什么以及何时使用。除了描述切面要完成的工作，通知还解决了何时执行这个工作的问题。它应该应用在某个方法被调用之前？之后？之前和之后都调用？还是只在方法抛出异常时调用？

Spring切面可以应用5种类型的通知：

- 前置通知（Before）：在目标方法被调用之前调用通知功能；
- 后置通知（After）：在目标方法完成之后调用通知，此时不会关心方法的输出是什么；
- 返回通知（After-returning）：在目标方法成功执行之后调用通知；
- 异常通知（After-throwing）：在目标方法抛出异常后调用通知；
- 环绕通知（Around）：通知包裹了被通知的方法，在被通知的方法调用之前和调用之后执行自定义的行为。  

对应注解：

| 注解   |   通知
|----
| @After   | 通知方法会在目标方法返回或抛出异常后调用   |
|----
| @AfterReturning   | 通知方法会在目标方法返回后调用   |
|----
| @AfterThrowing   | 通知方法会在目标方法抛出异常后调用   |
|----
| @Around   | 通知方法会将目标方法封装起来   |
|----
| @Before   | 通知方法会在目标方法调用之前执行   |
|----

**连接点（Join point）**

连接点是在应用执行过程中能够插入切面的一个点。这个点可以是调用方法时、抛出异常时、甚至修改一个字段时。切面代码可以利用这些点插入到应用的正常流程之中，并添加新的行为。

**切点（Pointcut）**

如果说通知定义了切面的“什么”和“何时”的话，那么切点就定义了“何处” 。切点的定义会匹配通知所要织入的一个或多个连接点。我们通常使用明确的类和方法名称，或是利用正则表达式定义所匹配的类和方法名称来指定这些切点。有些AOP框架允许我们创建动态的切点，可以根据运行时的决策（比如方法的参数值）来决定是否应用通知。

**切面（Aspect）**

通知+切点=切面

**引入（Introduction）**

引入允许我们向现有的类添加新方法或属性

**织入（Weaving）**

织入是把切面应用到目标对象并创建新的代理对象的过程。切面在指定的连接点被织入到目标对象中。在目标对象的生命周期里有多个点可以进行织入：

- 编译期：切面在目标类编译时被织入。这种方式需要特殊的编译器。AspectJ的织入编译器就是以这种方式织入切面的。
- 类加载期：切面在目标类加载到JVM时被织入。这种方式需要特殊的类加载器（ClassLoader），它可以在目标类被引入应用之前增强该目标类的字节码。AspectJ 5的加载时织入（load-time weaving，LTW）就支持以这种方式织入切面。
- 运行期：切面在应用运行的某个时刻被织入。一般情况下，在织入切面时，AOP容器会为目标对象动态地创建一个代理对象。Spring AOP就是以这种方式织入切面的。

#### Spring对AOP的支持：

1. 基于代理的经典Spring AOP；
2. 纯POJO切面（4.x版本需要XML配置）；
3. @AspectJ注解驱动的切面；
4. 注入式AspectJ切面（适用于Spring各版本）。

**例子**

{% highlight java %}
public interface Performance(){
  public void perform();
}
{% endhighlight %}

现在来写一个切点表达式，这个表达式能够设置当perform()方法执行时触发通知的调用。

{% highlight java %}
execution(* concert.Performance.perform(..))
//execution：在方法执行时触发
//*：返回任意类型
//concert.Performance：方法所属类
//perform：方法名
//(..)：使用任意参数
{% endhighlight %}

不仅如此，还可以写的更复杂一点

{% highlight java %}
execution(* concert.Performance.perform(..)&&within(concert.*))
//增加了一个与操作，当concert包下的任意类方法被调用时也会触发
{% endhighlight %}

在切点中选择bean

{% highlight java %}
execution(*concert.Performance.perform()) and bean('woodstock')
//限定bean id为woodstock
{% endhighlight %}

来个完整的切面

{% highlight java %}
@Aspect
public class Audience{
  @Before("execution(**concert.Performance.perform(..))")
  public void silenceCellPhones(){
    System.out.println("Silencing cell phones");
  }
  @Before("execution{** concert.Performance.perform{..}}")
  public void taskSeats(){
    System.out.println("Talking seats");
  }
  @AfterReturning("execution{** concert.Performance.perform{..}}")
  public void applause(){
    System.out.println("CLAP CLAP CLAP!!!");
  }
  @AfterThrowing("execution{** concert.Performance.perform{..}}")
  public void demanRefund(){
    System.out.println("Demanding a refund");
  }
}
{% endhighlight %}

可以简化一下

{% highlight java %}
@Aspect
public class Audience{
  //避免频繁使用切点表达式
  @Pointcut("execution(** concert.Performance.perform(..))")
  public void performance(){}
 
  @Before("performance()")
  public void silenceCellPhones(){
    System.out.println("Silencing cell phones");
  }
  @Before("performance()")
  public void taskSeats(){
    System.out.println("Talking seats");
  }
  @AfterReturning("performance()")
  public void applause(){
    System.out.println("CLAP CLAP CLAP!!!");
  }
  @AfterThrowing("performance()")
  public void demanRefund(){
    System.out.println("Demanding a refund");
  }
}
{% endhighlight %}

**XML中声明切面**

| AOP配置元素   | 用途
|----
| `<aop:advisor>`   | 定义AOP通知器   |
|----
| `<aop:after>`   | 定义AOP后置通知（不管被通知的方法是否执行成功）   |
|----
| `<aop:after-returning>`   | 定义AOP返回通知   |
|----
| `<aop:after-throwing>`   | 定义AOP异常通知   |
|----
| `<aop:around>`   | 定义AOP环绕通知   |
|----
| `<aop:aspect>`   | 定义一个切面   |
|----
| `<aop:aspectj-autoproxy>`   | 启用@AspectJ注解驱动的切面   |
|----
| `<aop:before>`   | 定义一个AOP前置通知   |
|----
| `<aop:config>`   | 顶层的AOP配置元素。大多数的<aop:*>元素必须包含在<aop:config>元素内   |
|----
| `<aop:declare-parents>`   | 以透明的方式为被通知的对象引入额外的接口   |
|----
| `<aop:pointcut>`   | 定义一个切点   |
|----

来个栗子

{% highlight java %}
public class Audience{
  public void silenceCellPhones(){
    System.out.println("Silencing cell phones");
  }
  public void taskSeats(){
    System.out.println("Talking seats");
  }
  public void applause(){
    System.out.println("CLAP CLAP CLAP!!!");
  }
  public void demandRefund(){
    System.out.println("Demanding a refund");
  }
}
{% endhighlight %}

通过XML将无注解的Audience声明为切面

{% highlight html %}
<aop:config>
  <aop:aspect ref="audience">
    <aop:before
      pointcut ="execution(** concert.Performance.perform(..))"
      method="sillenceCellPhones"/>
    <aop:before
      pointcut ="execution(** concert.Performance.perform(..))"
      method="taskSeats"/>
    <aop:after-returning
      pointcut ="execution(** concert.Performance.perform(..))"
      method="applause"/>
    <aop:After-throwing
        pointcut ="execution(** concert.Performance.perform(..))"
        method="demanRefund"/>
  </aop:aspect>
</aop:config>
{% endhighlight %}

AspectJ关于Spring AOP的AspectJ切点，最重要的一点就是Spring仅支持AspectJ切点指示器（pointcut designator）的一个子集。让我们回顾下，Spring是基于代理的，而某些切点表达式是与基于代理的AOP无关的。下表列出了Spring AOP所支持的AspectJ切点指示器。

Spring借助AspectJ的切点表达式语言来定义Spring切面

AspectJ指示器  | 描述
---|---
arg()  | 限制连接点匹配参数为指定类型的执行方法
@args()  | 限制连接点匹配参数由指定注解标注的执行方法
execution()  | 用于匹配是连接点的执行方法
this()  | 限制连接点匹配AOP代理的bean引用为指定类型的类
target  | 限制连接点匹配目标对象为指定类型的类
@target()  | 限制连接点匹配特定的执行对象，这些对象对应的类要具有指定类型的注解
within()  | 限制连接点匹配指定的类型
@within()  | 限制连接点匹配指定注解所标注的类型（当使用Spring AOP时，方法定义在由指定的注解所标注的类里）
@annotation  | 限定匹配带有指定注解的连接点

### Spring高级特性

由于Spring特殊的依赖注入技巧，导致Bean之间没有耦合度。

但是Bean有时需要使用spring容器本身的资源，这时你的Bean必须意识到Spring容器的存在。所以得使用Spring Aware，下面来看看Spring Aware提供的接口

| BeanNameAware  | 获得到容器中Bean的名称
|---|---
| BeanFactory  | 获得当前的bean factory，这样可以调用容器的服务
| ApplicationContextAware*  | 当前application context，这样可以调用容器的服务
| MessageSourceAware  | 获得Message source
| ApplicationEventPublisherAware  | 应用时间发布器，可以发布时间，
| ResourceLoaderAware  | 获得资源加载器，可以获得外部资源文件

#### @TaskExecutor

这样可以实现多线程和并发编程。通过@EnableAsync开启对异步任务的支持，并通过实际执行的Bean的方法始中使用@Async注解来声明其是一个异步任务

#### @Scheduled 计划任务

首先通过在配置类注解@EnableScheduling来开启对计划任务的支持，然后在要执行计划任务的方法上注解@Scheduled，声明这是一个计划任务

#### @Conditional

根据满足某一个特定条件创建一个特定的Bean。

#### 组合注解与元注解

元注解就是可以注解到别的注解上的注解，被注解的注解称之为组合注解，组合注解具备注解其上的元注解的功能。

**@Enable*注解的工作原理**

通过观察这些@Enable*注解的源码，我们发现所有的注解都有一个@Import注解，@Import是用来导入配置类的，这也就意外着这些自动开启的实现其实是导入了一些自动配置的Bean。这些导入配置的方式主要范围以下三种类型：

- 第一类：直接导入配置类
- 第二类：依据条件选择配置类
- 第三类：动态注册Bean

## What
简单的分析一下Spring。

Spring 框架中的核心组件只有三个：Core、Context 和 Bean。它们构建起了整个 Spring 的骨骼架构。没有它们就不可能有 AOP、Web 等上层的特性功能。下面也将主要从这三个组件入手分析 Spring。

### Spring的设计理念
用过Spring的同学都知道Bean在Spring的作用是非常重要的。通过一系列简单的配置来满足类与类之间的依赖关系——这叫做依赖注入。而依赖注入的关系是在一个叫IOC的容器中进行管理。

### 核心组件
我们说到Spring 框架中的核心组件只有三个：**Core**、**Context** 和 **Bean**。那么Core和Context是如何协作的呢？

我们知道 Bean 包装的是 Object，而 Object 必然有数据，如何给这些数据提供生存环境就是 Context 要解决的问题，对 Context 来说他就是要发现每个 Bean 之间的关系，为它们建立这种关系并且要维护好这种关系。所以 Context 就是一个 Bean 关系的集合，这个关系集合又叫 Ioc 容器 ，一旦建立起这个 Ioc 容器后 Spring 就可以为你工作了。那 Core 组件又有什么用武之地呢？其实 Core 就是发现、建立和维护每个 Bean 之间的关系所需要的一些列的工具。

#### Bean
前面已经说明了 Bean 组件对 Spring 的重要性，下面看看 Bean 这个组件式怎么设计的。Bean 组件在 Spring 的 org.springframework.beans 包下。这个包下的所有类主要解决了三件事：Bean 的定义、Bean 的创建以及对 Bean 的解析。对 Spring 的使用者来说唯一需要关心的就是 Bean 的创建，其他两个由 Spring 在内部帮你完成了，对你来说是透明的。

#### Context
ApplicationContext 是 Context 的顶级父类，他除了能标识一个应用环境的基本信息外，他还继承了五个接口，这五个接口主要是扩展了 Context 的功能。

ApplicationContext 的子类主要包含两个方面：

- ConfigurableApplicationContext 表示该 Context 是可修改的，也就是在构建 Context 中用户可以动态添加或修改已有的配置信息，它下面又有多个子类，其中最经常使用的是可更新的 Context，即 AbstractRefreshableApplicationContext类。
- WebApplicationContext 顾名思义，就是为 web 准备的 Context 他可以直接访问到 ServletContext，通常情况下，这个接口使用的少。

再往下分就是按照构建 Context 的文件类型，接着就是访问 Context 的方式。这样一级一级构成了完整的 Context 等级层次。

总体来说 ApplicationContext 必须要完成以下几件事：

- 标识一个应用环境
- 利用 BeanFactory 创建 Bean 对象
- 保存对象关系表
- 能够捕获各种事件

Context 作为 Spring 的 IOC 容器，基本上整合了 Spring 的大部分功能，或者说是大部分功能的基础。

#### Core
Core 组件作为 Spring 的核心组件，他其中包含了很多的关键类，其中一个重要组成部分就是定义了资源的访问方式。这种把所有资源都抽象成一个接口的方式很值得在以后的设计中拿来学习。
