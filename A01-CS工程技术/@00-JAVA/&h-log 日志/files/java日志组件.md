[TOC]
## 一、常用日志组件介绍

1、**Log4j**

**Apache Log4j**是一个基于Java的日志记录工具。它是由Ceki Gülcü首创的，现在则是Apache软件基金会的一个项目。 Log4j是几种Java日志框架之一。

通过使用Log4j，我们可以控制日志信息输送的目的地是控制台、文件、GUI组件、甚至是套接口服务器、NT的事件记录器、UNIX Syslog守护进程等；用户也可以控制每一条日志的输出格式；通过定义每一条日志信息的级别，用户能够更加细致地控制日志的生成过程。这些可以通过一个 配置文件来灵活地进行配置，而不需要修改程序代码。

2015年8月5日，项目管理委员会宣布Log4j 1.x已达到使用寿命。建议用户使用Log4j 1升级到Apache Log4j2

2、**Log4j2**

**Apache Log4j2**是apache开发的一款Log4j的升级产品。

Log4j2是Log4j1的升级版本。Log4j2基本上把Log4j1版本的核心全部重构掉了，而且基于Log4j1做了很多优化和改变。并提供了Logback中可用的许多改进，同时修复了Logback架构中的一些固有问题。

引入依赖：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-log4j2</artifactId>
    <version>2.0.3.RELEASE</version>
</dependency>
```

Commons Logging Apache基金会所属的项目，是一套Java日志接口，之前叫Jakarta Commons Logging，后更名为Commons Logging。

3、**Logback**

logback和log4j是同一个作者创作，它是log4j的升级版

Logback主要建立于**Logger、Appender 和 Layout** 这三个类之上。  
**Logger**: ***日志的记录器***，把它关联到应用的对应的context上后，主要用于存放日志对象，也可以定义日志类型、级别。Logger对象一般多定义为静态常量.  
**Appender**: 用于指定***日志输出***的目的地，目的地可以是控制台、文件、远程套接字服务器、 MySQL、 PostreSQL、Oracle和其他数据库、 JMS和远程UNIX Syslog守护进程等。  
**Layout**:负责把事件***转换成字符串，格式化的日志信息的输出***。

**4、Jul (Java Util Logging)**

JUL全称Java util Logger是java原生的日志框架，使用时不需要另外引用类库，相对其他日志框架方便，学习简单，能够在小型应用中灵活使用。

## 二、日志框架是如何桥接的

![](https://pic3.zhimg.com/80/v2-2106a572de35e147c697c23c58c38c46_720w.webp)

![](https://pic1.zhimg.com/80/v2-4e08efd7ef2e500cf996a9ec24cafa7c_720w.webp)

上图来自SLF4J官网。如图，上层都是使用SLF4JAPI对外暴露接口。SLF4JAPI使用的是slf4j-api.jar包。接着下层各个日志框架的实现就不一样了，最左边的是slf4j的一个空实现。第二列和第五列是logback和slf4j的一个简单实现，这2个框架没有使用所谓的桥接器，直接继承slf4j，实现slf4j的接口。log4j和jul的实现是要依靠桥接器，如上，slf4j-log412.jar和slf4j-jdk14.jar就是桥接器，分别连接slf4j，log4j和slf4j，jul。下面的log4j.jar和JVM runtime便是具体实现。

## 三、slf4j是什么，主要作用是什么？

**slf4j只是一个日志标准，并不是日志系统的具体实现。**

slf4j是门面模式的典型应用。所谓的门面模式，其核心为**外部与一个子系统的通信必须通过一个统一的外观对象进行，使得子系统更易于使用**。用一张图来表示门面模式的结构为：

![](https://pic2.zhimg.com/80/v2-f68d3095eb2912bcad4aca904d8d6a69_720w.webp)

门面模式的核心为Facade即门面对象，门面对象核心为几个点：

-   知道所有子角色的功能和责任
-   将客户端发来的请求委派到子系统中，没有实际业务逻辑
-   不参与子系统内业务逻辑的实现

slf4j的作用：

它是把不同的日志系统的实现进行了具体的抽象化，只提供了统一的日志使用接口，使用时只需要按照其提供的接口方法进行调用即可，由于它只是一个接口，并不是一个具体的可以直接单独使用的日志框架，所以最终日志的格式、记录级别、输出方式等都要通过接口绑定的具体的日志系统来实现，这些具体的日志系统就有log4j,logback,java.util.logging等，它们才实现了具体的日志系统的功能。

在同一个系统中，可能不同的模块使用的是不同的日志系统。比如A模块为log4j，B模块为slf4j-simple，C模块为logback，这样的话系统中必须同时支持并维护logback、log4j、slf4j-simple三种日志框架，非常不便。

解决这个问题的方式就是引入一个适配层，由适配层决定使用哪一种日志系统，而调用端只需要做的事情就是打印日志而不需要关心如何打印日志，slf4j或者commons-logging就是这种适配层。

因此，相当于slf4j只做了两件事：

-   提供日志接口
-   提供获取具体日志对象的方法

回到刚才的例子：其中，slf4j-simple、logback都是slf4j的具体实现，log4j并不直接实现slf4j，但是有专门的一层桥接slf4j-log4j12来实现slf4j。

**所以引入slf4j的作用就是：只要所有代码都使用门面对象slf4j，我们就不需要关心其具体实现，最终所有地方使用一种具体实现即可，更换、维护都非常方便。**

slf4j的实现原理：

slf4j的用法通常是"**Logger logger = LoggerFactory.getLogger(Object.class);**"，就是通过LoggerFactory去拿slf4j提供的一个Logger接口的具体实现。

其中getLogger的时候会去classpath下找**STATIC_LOGGER_BINDER_PATH**，STATIC_LOGGER_BINDER_PATH值为"org/slf4j/impl/StaticLoggerBinder.class"，即**所有slf4j的实现，在提供的jar包路径下，一定是有"org/slf4j/impl/StaticLoggerBinder.class"存在的。**

```java
static Set<URL> findPossibleStaticLoggerBinderPathSet() {
    // use Set instead of list in order to deal with bug #138
    // LinkedHashSet appropriate here because it preserves insertion order
    // during iteration
    Set<URL> staticLoggerBinderPathSet = new LinkedHashSet<URL>();
    try {
        ClassLoader loggerFactoryClassLoader = LoggerFactory.class.getClassLoader();
        Enumeration<URL> paths;
        if (loggerFactoryClassLoader == null) {
            paths = ClassLoader.getSystemResources(STATIC_LOGGER_BINDER_PATH);
        } else {
            paths = loggerFactoryClassLoader.getResources(STATIC_LOGGER_BINDER_PATH);
        }
        while (paths.hasMoreElements()) {
            URL path = paths.nextElement();
            staticLoggerBinderPathSet.add(path);
        }
    } catch (IOException ioe) {
        Util.report("Error getting resources from path", ioe);
    }
    return staticLoggerBinderPathSet;
}
```

我们不能避免在系统中同时引入多个slf4j的实现，所以接收的地方是一个Set。

```java
private static void reportMultipleBindingAmbiguity(Set<URL> binderPathSet) {
    if (isAmbiguousStaticLoggerBinderPathSet(binderPathSet)) {
        Util.report("Class path contains multiple SLF4J bindings.");
        for (URL path : binderPathSet) {
            Util.report("Found binding in [" + path + "]");
        }
        Util.report("See " + MULTIPLE_BINDINGS_URL + " for an explanation.");
    }
}
```

同时存在三个"org/slf4j/impl/StaticLoggerBinder.class"的情况下，编译期间，编译器会选择其中一个StaticLoggerBinder.class进行绑定，这个地方sfl4j也在reportActualBinding方法中报告了绑定的是哪个日志框架。

```java
private static void reportActualBinding(Set<URL> binderPathSet) {
     // binderPathSet can be null under Android
     if (binderPathSet != null && isAmbiguousStaticLoggerBinderPathSet(binderPathSet)) {
         Util.report("Actual binding is of type [" + StaticLoggerBinder.getSingleton().getLoggerFactoryClassStr() + "]");
     }
 }
```

不同的StaticLoggerBinder其getLoggerFactory实现不同，拿到ILoggerFactory之后调用一下getLogger即拿到了具体的Logger，可以使用Logger进行日志输出。