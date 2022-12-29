
# JDK Version 1.0

_1996-01-23 Oak(橡树)_

> 初代版本，伟大的一个里程碑，但是是纯解释运行，使用外挂JIT，性能比较差，运行速度慢。

---

# JDK Version 1.1

_1997-02-19_

> -   JDBC(Java DataBase Connectivity);
> -   支持内部类;
> -   RMI(Remote Method Invocation) ;
> -   反射;
> -   Java Bean;

---

# JDK Version 1.2

_1998-12-08 Playground(操场)_

> -   集合框架;
> -   JIT(Just In Time)编译器;
> -   对打包的Java文件进行数字签名;
> -   JFC(Java Foundation Classes), 包括Swing 1.0, 拖放和Java2D类库;
> -   Java插件;
> -   JDBC中引入可滚动结果集,BLOB,CLOB,批量更新和用户自定义类型;
> -   Applet中添加声音支持.

---

# JDK Version 1.3

_2000-05-08 Kestrel(红隼)_

> -   Java Sound API;
> -   jar文件索引;
> -   对Java的各个方面都做了大量优化和增强;

---

# JDK Version 1.4

_2002-02-13 Merlin(隼)_

> -   XML处理;
> -   Java打印服务;
> -   Logging API;
> -   Java Web Start;
> -   JDBC 3.0 API;
> -   断言;
> -   Preferences API;
> -   链式异常处理;
> -   支持IPV6;
> -   支持正则表达式;
> -   引入Imgae I/O API.

---

# JAVA 5

_2004-09-30 Tiger(老虎)_

> -   泛型;
> -   增强循环,可以使用迭代方式;
> -   自动装箱与自动拆箱;
> -   类型安全的枚举;
> -   可变参数;
> -   静态引入;
> -   元数据(注解);
> -   Instrumentation;

---

# JAVA 6

_2006-12-11 Mustang(野马)_

> -   支持脚本语言;
> -   JDBC 4.0API;
> -   Java Compiler API;
> -   可插拔注解;
> -   增加对Native PKI(Public Key Infrastructure), Java GSS(Generic Security Service),Kerberos和LDAP(Lightweight Directory Access Protocol)支持;
> -   继承Web Services;

---

# JAVA 7

_2011-07-28 Dolphin(海豚)_

> -   switch语句块中允许以字符串作为分支条件;
> -   在创建泛型对象时应用类型推断;
> -   在一个语句块中捕获多种异常;
> -   支持动态语言;
> -   支持try-with-resources(在一个语句块中捕获多种异常);
> -   引入Java NIO.2开发包;
> -   数值类型可以用二进制字符串表示,并且可以在字符串表示中添加下划线;
> -   钻石型语法(在创建泛型对象时应用类型推断);
> -   null值得自动处理;

---

# JAVA 8

_2014-03-18_ 

> -   **Lambda 表达式** − Lambda允许把函数作为一个方法的参数（函数作为参数传递进方法中。
>     
> -   **方法引用** − 方法引用提供了非常有用的语法，可以直接引用已有Java类或对象（实例）的方法或构造器。与lambda联合使用，方法引用可以使语言的构造更紧凑简洁，减少冗余代码。
>     
> -   **默认方法** − 默认方法就是一个在接口里面有了一个实现的方法。
>     
> -   **新工具** − 新的编译工具，如：Nashorn引擎 jjs、 类依赖分析器jdeps。
>     
> -   **Stream API** −新添加的Stream API（java.util.stream） 把真正的函数式编程风格引入到Java中。
>     
> -   **Date Time API** − 加强对日期与时间的处理。
>     
> -   **Optional 类** − Optional 类已经成为 Java 8 类库的一部分，用来解决空指针异常。
>     
> -   **Nashorn, JavaScript 引擎** − Java 8提供了一个新的Nashorn javascript引擎，它允许我们在JVM上运行特定的javascript应用。
>     
> -   详细参考:[Java 8 新特性 | 菜鸟教程](http://www.runoob.com/java/java8-new-features.html "Java 8  新特性 | 菜鸟教程")
>     

---

# JAVA 9

_2017-09-22_

> -   **模块系统**：模块是一个包的容器，Java 9 最大的变化之一是引入了模块系统（Jigsaw 项目）。
> -   **REPL (JShell)**：交互式编程环境。
> -   **HTTP 2 客户端**：HTTP/2标准是HTTP协议的最新版本，新的 HTTPClient API 支持 WebSocket 和 HTTP2 流以及服务器推送特性。
> -   **改进的 Javadoc**：Javadoc 现在支持在 API 文档中的进行搜索。另外，Javadoc 的输出现在符合兼容 HTML5 标准。
> -   **多版本兼容 JAR 包**：多版本兼容 JAR 功能能让你创建仅在特定版本的 Java 环境中运行库程序时选择使用的 class 版本。
> -   **集合工厂方法**：List，Set 和 Map 接口中，新的静态工厂方法可以创建这些集合的不可变实例。
> -   **私有接口方法**：在接口中使用private私有方法。我们可以使用 private 访问修饰符在接口中编写私有方法。
> -   **进程 API**: 改进的 API 来控制和管理操作系统进程。引进 java.lang.ProcessHandle 及其嵌套接口 Info 来让开发者逃离时常因为要获取一个本地进程的 PID 而不得不使用本地代码的窘境。
> -   **改进的 Stream API**：改进的 Stream API 添加了一些便利的方法，使流处理更容易，并使用收集器编写复杂的查询。
> -   **改进 try-with-resources**：如果你已经有一个资源是 final 或等效于 final 变量,您可以在 try-with-resources 语句中使用该变量，而无需在 try-with-resources 语句中声明一个新变量。
> -   **改进的弃用注解 @Deprecated**：注解 @Deprecated 可以标记 Java API 状态，可以表示被标记的 API 将会被移除，或者已经破坏。
> -   **改进钻石操作符(Diamond Operator)** ：匿名类可以使用钻石操作符(Diamond Operator)。
> -   **改进 Optional 类**：java.util.Optional 添加了很多新的有用方法，Optional 可以直接转为 stream。
> -   **多分辨率图像 API**：定义多分辨率图像API，开发者可以很容易的操作和展示不同分辨率的图像了。
> -   **改进的 CompletableFuture API** ： CompletableFuture 类的异步机制可以在 ProcessHandle.onExit 方法退出时执行操作。
> -   **轻量级的 JSON API**：内置了一个轻量级的JSON API
> -   **响应式流（Reactive Streams) API**: Java 9中引入了新的响应式流 API 来支持 Java 9 中的响应式编程。
> -   详细参考:[Java 9 新特性 | 菜鸟教程](http://www.runoob.com/java/java9-new-features.html "Java 9 新特性 | 菜鸟教程")

---

# JAVA 10

_2018-03-20_

根据官网的公开资料，共有12个重要特性，如下：

> -   [JEP286](http://openjdk.java.net/jeps/286 "JEP286")，var 局部变量类型推断。
> -   [JEP296](http://openjdk.java.net/jeps/296 "JEP296")，将原来用 Mercurial 管理的众多 JDK 仓库代码，合并到一个仓库中，简化开发和管理过程。
> -   [JEP304](http://openjdk.java.net/jeps/304 "JEP304")，统一的垃圾回收接口。
> -   [JEP307](http://openjdk.java.net/jeps/307 "JEP307")，G1 垃圾回收器的并行完整垃圾回收，实现并行性来改善最坏情况下的延迟。
> -   [JEP310](http://openjdk.java.net/jeps/310 "JEP310")，应用程序类数据 (AppCDS) 共享，通过跨进程共享通用类元数据来减少内存占用空间，和减少启动时间。
> -   [JEP312](http://openjdk.java.net/jeps/312 "JEP312")，ThreadLocal 握手交互。在不进入到全局 JVM 安全点 (Safepoint) 的情况下，对线程执行回调。优化可以只停止单个线程，而不是停全部线程或一个都不停。
> -   [JEP313](http://openjdk.java.net/jeps/313 "JEP313")，移除 JDK 中附带的 javah 工具。可以使用 javac -h 代替。
> -   [JEP314](http://openjdk.java.net/jeps/314 "JEP314")，使用附加的 Unicode 语言标记扩展。
> -   [JEP317](http://openjdk.java.net/jeps/317 "JEP317")，能将堆内存占用分配给用户指定的备用内存设备，使用 Graal 基于 Java 的编译器，可以预先把 Java 代码编译成本地代码来提升效能。
> -   [JEP318](http://openjdk.java.net/jeps/318 "JEP318")，在 OpenJDK 中提供一组默认的根证书颁发机构证书。开源目前 Oracle 提供的的 Java SE 的根证书，这样 OpenJDK 对开发人员使用起来更方便。
> -   [JEP322](http://openjdk.java.net/jeps/322 "JEP322")，基于时间定义的发布版本，即上述提到的发布周期。版本号为\$FEATURE.\$INTERIM.\$UPDATE.\$PATCH，分别是大版本，中间版本，升级包和补丁版本。

---

# JAVA 11

_2018-09-25_ 

翻译后的新特性有：

> -   181:Nest-Based访问控制
> -   309:动态类文件常量
> -   315:改善Aarch64 intrinsic
> -   318:无操作垃圾收集器
> -   320:消除Java EE和CORBA模块
> -   321:HTTP客户端(标准)
> -   323:局部变量的语法λ参数
> -   324:Curve25519和Curve448关键协议
> -   327:Unicode 10
> -   328:飞行记录器
> -   329:ChaCha20和Poly1305加密算法
> -   330:发射一列纵队源代码程序
> -   331:低开销堆分析
> -   332:传输层安全性(Transport Layer Security,TLS)1.3
> -   333:动作:一个可伸缩的低延迟垃圾收集器 (实验)
> -   335:反对Nashorn JavaScript引擎
> -   336:反对Pack200工具和API

---

# JAVA 12

_2019-03-19_

作为“功能性版本”，JDK 12 总共包含 8 个新的 JEP ，分别为：

> -   189: [Shenandoah: A Low-Pause-Time Garbage Collector (Experimental)](http://openjdk.java.net/jeps/189 "Shenandoah: A Low-Pause-Time Garbage Collector (Experimental)") ：新增一个名为 Shenandoah 的垃圾回收器，它通过在 Java 线程运行的同时进行疏散 (evacuation) 工作来减少停顿时间。
>     
> -   230: [Microbenchmark Suite](http://openjdk.java.net/jeps/230 "Microbenchmark Suite")：新增一套微基准测试，使开发者能够基于现有的 Java Microbenchmark Harness（JMH）轻松测试 JDK 的性能，并创建新的基准测试。
>     
> -   325: [Switch Expressions (Preview)](http://openjdk.java.net/jeps/325 "Switch Expressions (Preview)") ：对 switch 语句进行扩展，使其可以用作语句或表达式，简化日常代码。
>     
> -   334: [JVM Constants API](http://openjdk.java.net/jeps/334 "JVM Constants API") ：引入一个 API 来对关键类文件 (key class-file) 和运行时工件的名义描述（nominal descriptions）进行建模，特别是那些可从常量池加载的常量。
>     
> -   340: [One AArch64 Port, Not Two](http://openjdk.java.net/jeps/340 "One AArch64 Port, Not Two") ：删除与 arm64 端口相关的所有源码，保留 32 位 ARM 移植和 64 位 aarch64 移植。
>     
> -   341: [Default CDS Archives](http://openjdk.java.net/jeps/341 "Default CDS Archives") ：默认生成类数据共享（CDS）存档。
>     
> -   344: [Abortable Mixed Collections for G1](http://openjdk.java.net/jeps/344 "Abortable Mixed Collections for G1") ：当 G1 垃圾回收器的回收超过暂停目标，则能中止垃圾回收过程。
>     
> -   346: [Promptly Return Unused Committed Memory from G1](http://openjdk.java.net/jeps/346 "Promptly Return Unused Committed Memory from G1") ：改进 G1 垃圾回收器，以便在空闲时自动将 Java 堆内存返回给操作系统。
>     

>  原文地址：[JDK 12](http://openjdk.java.net/projects/jdk/12/ "JDK 12")

我们知道，JDK 11 是一个 LTS (Long Term Support) 版本，那么，该怎么选择呢？（反正 JDK 8 还是主流，我真的困惑吗？）

> 我该用12还是 11：[我该用 Java 12 还是坚持 Java 11？_CSDN资讯的博客-CSDN博客](https://blog.csdn.net/csdnnews/article/details/83753246 "我该用 Java 12 还是坚持 Java 11？_CSDN资讯的博客-CSDN博客") 

---

# JAVA 13

2019-09-17

新特性：

> -   350    [Dynamic CDS Archives](https://openjdk.java.net/jeps/350 "Dynamic CDS Archives")     对appCDS进行性了扩展，允许在Java应用执行结束时动态归档类。归档类包括包括默认的基础层CDS(class data-sharing) 存档中不存在的所有已加载的应用程序类和类库。通过此仿瓷提高了AppCDS的可用性；
> -   351    [ZGC: Uncommit Unused Memory](https://openjdk.java.net/jeps/351 "ZGC: Uncommit Unused Memory")   对ZGC进行了增强，在以前的版本中，java GC之后并不会将系统内存释放给OS，因为每次释放都意味着重新调整jvm的内存大小，存在一定的消耗；随着软件的发展，我们发现在很多时候内存是比较昂贵的资源，所以将不用的内存释放回去给OS是非常有必要的；此功能在默认情况下已开始，但可以通过-xx:-zuncommit参数禁用；注意：如果最新内存参数设置比最大内存参数大，那么此功能将隐式禁用。
> -   353    [Reimplement the Legacy Socket API](https://openjdk.java.net/jeps/353 "Reimplement the Legacy Socket API")    在这个版本中，将使用新的实现来代替java.net.socket和java.net.serversocket API的底层实现。新版本中旧的API还未删除，可以通过配置系统属性"jdk.net.useplansocketimpl"来使用他们。但默认实现是最新版本的。
> -   354    [Switch Expressions (Preview)](https://openjdk.java.net/jeps/354 "Switch Expressions (Preview)")    扩展开关，以便它可以用作语句或表达式，并且两种形式都可以使用传统的情况…：标签（带有贯穿线）或新案例…->标签（没有掉进去），还有一个新的语句，用于从开关表达式中产生值。这些变化将简化日常编码，并为在交换机中使用模式匹配做好准备。这是jdk 13中的一个预览语言特性。
> -   355    [Text Blocks (Preview)](https://openjdk.java.net/jeps/355 "Text Blocks (Preview)")    向Java语言添加文本块。文本块是一个多行字符串文本，它避免了大多数转义序列的需要，自动以可预测的方式格式化字符串，并在需要时让开发人员控制格式。这是jdk 13中的一个预览语言特性。

此外，JDK8的截止时间为2019年1月份，到期后，Oracle将不再提供补丁及其它的更新服务。官网称可能会更久，JDK9的截止时间是2018年3月，JDK10的截止版本是2018年9月。（详细请前往：[Oracle Java SE Support Roadmap](http://www.oracle.com/technetwork/java/javase/eol-135779.html?ssSourceSiteId=otncn "Oracle Java SE Support Roadmap")），JDK 9和 JDK 10都是一个短期版本，故稳定长期的版本可能是JAVA 11(LTS - Long Term Support)版本。

---

# JAVA 14

2020-03-17

> -   305    [Pattern Matching for instanceof (Preview)](https://openjdk.java.net/jeps/305 "Pattern Matching for instanceof (Preview)")    instanceof 的模式匹配（预览）
> -   343    [Packaging Tool (Incubator)](https://openjdk.java.net/jeps/343 "Packaging Tool (Incubator)")    打包工具（孵化）
> -   345    [NUMA-Aware Memory Allocation for G1](https://openjdk.java.net/jeps/345 "NUMA-Aware Memory Allocation for G1")    G1 的NUMA 内存分配优化
> -   349    [JFR Event Streaming](https://openjdk.java.net/jeps/349 "JFR Event Streaming")    JFR事件流
> -   352    [Non-Volatile Mapped Byte Buffers](https://openjdk.java.net/jeps/352 "Non-Volatile Mapped Byte Buffers")    非原子性的字节缓冲区映射
> -   358    [Helpful NullPointerExceptions](https://openjdk.java.net/jeps/358 "Helpful NullPointerExceptions")    非常有帮助的空指针异常
> -   359    [Records (Preview)](https://openjdk.java.net/jeps/359 "Records (Preview)")    Records（预览）
> -   361    [Switch Expressions (Standard)](https://openjdk.java.net/jeps/361 "Switch Expressions (Standard)")    Switch 表达式（标准）
> -   362    [Deprecate the Solaris and SPARC Ports](https://openjdk.java.net/jeps/362 "Deprecate the Solaris and SPARC Ports")    弃用 Solaris 和S PARC 端口
> -   363    [Remove the Concurrent Mark Sweep (CMS) Garbage Collector](https://openjdk.java.net/jeps/363 "Remove the Concurrent Mark Sweep (CMS) Garbage Collector")    移除 CMS（Concurrent Mark Sweep）垃圾收集器
> -   364    [ZGC on macOS](https://openjdk.java.net/jeps/364 "ZGC on macOS")    macOS 系统上的 ZGC
> -   365    [ZGC on Windows](https://openjdk.java.net/jeps/365 "ZGC on Windows")    Windows 系统上的 ZGC
> -   366    [Deprecate the ParallelScavenge + SerialOld GC Combination](https://openjdk.java.net/jeps/366 "Deprecate the ParallelScavenge + SerialOld GC Combination")    弃用 ParallelScavenge + SerialOld GC 组合
> -   367    [Remove the Pack200 Tools and API](https://openjdk.java.net/jeps/367 "Remove the Pack200 Tools and API")    移除Pack200 Tools和API
> -   368    [Text Blocks (Second Preview)](https://openjdk.java.net/jeps/368 "Text Blocks (Second Preview)")    文本块（第二个预览版）
> -   370    [Foreign-Memory Access API (Incubator)](https://openjdk.java.net/jeps/370 "Foreign-Memory Access API (Incubator)")    外部存储器API（孵化）

---

# JAVA 15

2020-09-15

> -   339    [Edwards-Curve Digital Signature Algorithm (EdDSA)](https://openjdk.java.net/jeps/339 "Edwards-Curve Digital Signature Algorithm (EdDSA)")    蒙哥马利与扭曲爱德华曲线签名算法
> -   360    [Sealed Classes (Preview)](https://openjdk.java.net/jeps/360 "Sealed Classes (Preview)")    密封类(预览)
> -   371    [Hidden Classes](https://openjdk.java.net/jeps/371 "Hidden Classes")    隐藏类
> -   372    [Remove the Nashorn JavaScript Engine](https://openjdk.java.net/jeps/372 "Remove the Nashorn JavaScript Engine")    移除nasorn JavaScript引擎
> -   373    [Reimplement the Legacy DatagramSocket API](https://openjdk.java.net/jeps/373 "Reimplement the Legacy DatagramSocket API")    重新实现旧的DatagramSocket API
> -   374    [Disable and Deprecate Biased Locking](https://openjdk.java.net/jeps/374 "Disable and Deprecate Biased Locking")    禁用和弃用偏置锁
> -   375    [Pattern Matching for instanceof (Second Preview)](https://openjdk.java.net/jeps/375 "Pattern Matching for instanceof (Second Preview)")    模式匹配的instanceof(第二次预览)
> -   377    [ZGC: A Scalable Low-Latency Garbage Collector](https://openjdk.java.net/jeps/377 "ZGC: A Scalable Low-Latency Garbage Collector")    ZGC:一个可扩展的低延迟垃圾收集器
> -   378    [Text Blocks](https://openjdk.java.net/jeps/378 "Text Blocks")    文本块
> -   379    [Shenandoah: A Low-Pause-Time Garbage Collector](https://openjdk.java.net/jeps/379 "Shenandoah: A Low-Pause-Time Garbage Collector")    Shenandoah:低暂停时间垃圾收集器
> -   381    [Remove the Solaris and SPARC Ports](https://openjdk.java.net/jeps/381 "Remove the Solaris and SPARC Ports")    移除Solaris和SPARC端口
> -   383    [Foreign-Memory Access API (Second Incubator)](https://openjdk.java.net/jeps/383 "Foreign-Memory Access API (Second Incubator)")    外部内存访问API(第二个孵化器)
> -   384    [Records (Second Preview)](https://openjdk.java.net/jeps/384 "Records (Second Preview)")    记录(第二次预览)
> -   385    [Deprecate RMI Activation for Removal](https://openjdk.java.net/jeps/385 "Deprecate RMI Activation for Removal")    建议移除RMI激活

---

# JAVA 16

2021-03-16

他来了他来了，就在这个月！！！！发布了！！！

> -   338    [Vector API (Incubator)](https://openjdk.java.net/jeps/338 "Vector API (Incubator)")    病媒API(孵化器)
> -   347    [Enable C++14 Language Features](https://openjdk.java.net/jeps/347 "Enable C++14 Language Features")    启用C++ 14种语言特性
> -   357    [Migrate from Mercurial to Git](https://openjdk.java.net/jeps/357 "Migrate from Mercurial to Git")    从Mercurial迁移到Git
> -   369    [Migrate to GitHub](https://openjdk.java.net/jeps/369 "Migrate to GitHub")    迁移到GitHub
> -   376    [ZGC: Concurrent Thread-Stack Processing](https://openjdk.java.net/jeps/376 "ZGC: Concurrent Thread-Stack Processing")    ZGC:并发线程堆栈处理
> -   380    [Unix-Domain Socket Channels](https://openjdk.java.net/jeps/380 "Unix-Domain Socket Channels")    Unix-Domain 套接字通道
> -   386    [Alpine Linux Port](https://openjdk.java.net/jeps/386 "Alpine Linux Port")    Alpine Linux端口
> -   387    [Elastic Metaspace](https://openjdk.java.net/jeps/387 "Elastic Metaspace")    弹性Metaspace
> -   388    [Windows/AArch64 Port](https://openjdk.java.net/jeps/388 "Windows/AArch64 Port")    Windows / AArch64端口
> -   389    [Foreign Linker API (Incubator)](https://openjdk.java.net/jeps/389 "Foreign Linker API (Incubator)")    国外连接器API(孵化器)
> -   390    [Warnings for Value-Based Classes](https://openjdk.java.net/jeps/390 "Warnings for Value-Based Classes")    对基于值的类的警告
> -   392    [Packaging Tool](https://openjdk.java.net/jeps/392 "Packaging Tool")    包装工具
> -   393    [Foreign-Memory Access API (Third Incubator)](https://openjdk.java.net/jeps/393 "Foreign-Memory Access API (Third Incubator)")    外存储器访问API(第三孵化器)
> -   394    [Pattern Matching for instanceof](https://openjdk.java.net/jeps/394 "Pattern Matching for instanceof")    instanceof匹配模式
> -   395    [Records](https://openjdk.java.net/jeps/395 "Records")    记录
> -   396    [Strongly Encapsulate JDK Internals by Default](https://openjdk.java.net/jeps/396 "Strongly Encapsulate JDK Internals by Default")    默认情况下对JDK内部进行强封装
> -   397    [Sealed Classes (Second Preview)](https://openjdk.java.net/jeps/397 "Sealed Classes (Second Preview)")    密封类(第二次预览)

---

# JAVA 17

2021-09-14

> -   306    [Restore Always-Strict Floating-Point Semantics](https://openjdk.java.net/jeps/306 "Restore Always-Strict Floating-Point Semantics")    恢复总是严格的浮点语义
> -   356    [Enhanced Pseudo-Random Number Generators](https://openjdk.java.net/jeps/356 "Enhanced Pseudo-Random Number Generators")    增强型伪随机数发生器
> -   382    [New macOS Rendering Pipeline](https://openjdk.java.net/jeps/382 "New macOS Rendering Pipeline")    新的 macOS 渲染管道
> -   391    [macOS/AArch64 Port](https://openjdk.java.net/jeps/391 "macOS/AArch64 Port")    将 JDK 移植到 macOS/AArch64
> -   398    [Deprecate the Applet API for Removal](https://openjdk.java.net/jeps/398 "Deprecate the Applet API for Removal")    不赞成删除 Applet API
> -   403    [Strongly Encapsulate JDK Internals](https://openjdk.java.net/jeps/403 "Strongly Encapsulate JDK Internals")    强封装 JDK 内部构件
> -   406    [Pattern Matching for switch (Preview)](https://openjdk.java.net/jeps/406 "Pattern Matching for switch (Preview)")    模式匹配开关(预览)
> -   407    [Remove RMI Activation](https://openjdk.java.net/jeps/407 "Remove RMI Activation")    删除 RMI 激活
> -   409    [Sealed Classes](https://openjdk.java.net/jeps/409 "Sealed Classes")    封闭类别
> -   410    [Remove the Experimental AOT and JIT Compiler](https://openjdk.java.net/jeps/410 "Remove the Experimental AOT and JIT Compiler")    删除实验 AOT 和 JIT 编译器
> -   411    [Deprecate the Security Manager for Removal](https://openjdk.java.net/jeps/411 "Deprecate the Security Manager for Removal")    请求删除安全管理器
> -   412    [Foreign Function & Memory API (Incubator)](https://openjdk.java.net/jeps/412 "Foreign Function & Memory API (Incubator)")    外部函数与内存 API (孵化器)
> -   414    [Vector API (Second Incubator)](https://openjdk.java.net/jeps/414 "Vector API (Second Incubator)")    矢量 API (第二孵化器)
> -   415    [Context-Specific Deserialization Filters](https://openjdk.java.net/jeps/415 "Context-Specific Deserialization Filters")    特定于上下文的反序列化过滤器

Java 17 目前已经进入 Rampdown Phase One 阶段，所有的功能特性都已经被冻结。这说明 Java 17的新特性已经定了，不会再增加新的 JEP (JDK增强建议)！

# JAVA 18

2022-03-22

> -   400    [UTF-8 by Default](https://openjdk.java.net/jeps/400 "UTF-8 by Default")    默认 UTF-8
> -   408    [Simple Web Server](https://openjdk.java.net/jeps/408 "Simple Web Server")    简单的网络服务器
> -   413    [Code Snippets in Java API Documentation](https://openjdk.java.net/jeps/413 "Code Snippets in Java API Documentation")   代码片段
> -   416    [Reimplement Core Reflection with Method Handles](https://openjdk.java.net/jeps/416 "Reimplement Core Reflection with Method Handles")   重构 Reflection
> -   417    [Vector API (Third Incubator)](https://openjdk.java.net/jeps/417 "Vector API (Third Incubator)")  计算向量的 API
> -   418    [Internet-Address Resolution SPI](https://openjdk.java.net/jeps/418 "Internet-Address Resolution SPI")    互联网地址解析 SPI
> -   419    [Foreign Function & Memory API (Second Incubator)](https://openjdk.java.net/jeps/419 "Foreign Function & Memory API (Second Incubator)")    新API，让 JAVA 程序能够与其他非 JAVA 运行时的程序或数据进行交互
> -   420    [Pattern Matching for switch (Second Preview)](https://openjdk.java.net/jeps/420 "Pattern Matching for switch (Second Preview)")    开关模式匹配
> -   421    [Deprecate Finalization for Removal](https://openjdk.java.net/jeps/421 "Deprecate Finalization for Removal")   弃用 finalize

来了来了它来了，JAVA 18 已于 2022年3月22日发布！！！！ 

#  JAVA 19

2022-09-20

> -   405   [Record Patterns (Preview)](https://openjdk.org/jeps/405 "Record Patterns (Preview)") 记录模式
> -   422   [Linux/RISC-V Port](https://openjdk.org/jeps/422 "Linux/RISC-V Port") Linux/RISC-V 移植
> -   424   [Foreign Function & Memory API (Preview)](https://openjdk.org/jeps/424 "Foreign Function & Memory API (Preview)") 外部函数和内存 API
> -   425   [Virtual Threads (Preview)](https://openjdk.org/jeps/425 "Virtual Threads (Preview)") 虚拟线程
> -   426   [Vector API (Fourth Incubator)](https://openjdk.org/jeps/426 "Vector API (Fourth Incubator)") 向量 API
> -   427   [Pattern Matching for switch (Third Preview)](https://openjdk.org/jeps/427 "Pattern Matching for switch (Third Preview)") Switch 模式匹配
> -   428   [Structured Concurrency (Incubator)](https://openjdk.org/jeps/428 "Structured Concurrency (Incubator)") 结构化并发


参考： [全网最全的JAVA所有版本特性【JAVA 1.0 - JAVA 19】_冯一朔的博客-CSDN博客](https://blog.csdn.net/qq934235475/article/details/82220076)