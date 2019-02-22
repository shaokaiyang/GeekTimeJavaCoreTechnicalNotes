# GeekTimeJavaCoreTechnicalNotes
**记录在《极客时间》平台上《java核心技术36讲》专栏的学习笔记**  
**作者信息：杨晓峰 前Oracle首席工程师**    
**课程海报如下：欢迎扫描海报右下方二维码订阅（有优惠哦）** 
 
![课程海报](./picture/javacore.jpg ) 

# 目录
* [开篇词，以面试题为切入点有效提升Java内功](#0)
* [第1讲 谈谈你对Java平台的理解](#1)
* [第2讲 Exception和Error有什么区别？](#2)
* [第3讲 谈谈final、finally、finalize有什么不同？](#3)
* [第4讲 强引用、软引用、弱引用、幻象引用有什么区别？](#4)
* [第5讲 String、StringBuffer、StringBuilder有什么区别？](#5)
* [第6讲 动态代理是基于什么原理？](#6)
* [第7讲 int和Integer有什么区别？](#7)
* [第8讲 对比Vector、ArrayList、LinkedList有何区别？](#8)
* [第9讲 对比Hashtable、HashMap、TreeMap有什么不同？](#9)
* [第10讲 如何保证集合是线程安全的？](#10)
* [第11讲 Java提供了那些IO方式？NIO如何实现多路复用？](#11)
* [第12讲 Java有几种文件拷贝方式？哪一种最高效？](#12)
* [第13讲 谈谈接口和抽象类有什么区别？](#13)
* [第14讲 谈谈你知道的设计模式](#14)
* [第15讲 synchronized和ReentrantLock有什么区别？](#15)
* [Java学习和面试看法](#15-1)
* [第16讲 synchronized底层如何实现？什么是锁的升级和降级？](#16)
* [第17讲 一个线程两次调用start()方法会出现什么状况？](#17)
* [第18讲 什么情况下Java程序会产生死锁？如何定位、修复？](#18)
* [第19讲 Java并发包提供了哪些并发工具类？](#19)
* [第20讲 并发包中的ConcurrentLinkedQueue和LinkedBlockingQueue有什么区别与联系？](#20)
* [第21讲 Java并发类库提供的线程池有哪几种？分别有什么特点？](#21)
* [第22讲 AtomicInteger底层实现原理是什么？如何在自己的产品代码中应用？](#22)
* [第23讲 类加载过程，什么是双亲委派模型？](#23)
* [第24讲 有哪些方法可以在运行时动态生成一个Java类？](#24)
* [第25讲 JVM内存区域的划分，哪些区域可能发生UotOfMemoryError？](#25)
* [第26讲 如何监控和诊断JVM堆内存和堆外内存使用？](#26)
* [第27讲 Java常见的垃圾收集器有哪些？](#27)
* [第28讲 谈谈你的GC调优思路？](#28)
* [第29讲 Java内存模型中的happen-before是什么？](#29)
* [第30讲 Java程序运行在Docker等容器环境有哪些新问题？](#30)
* [第31讲 Java应用开发中的注入攻击](#31)
* [第32讲 如何写出安全的Java代码？](#32)
* [第33讲 后台服务出现明显“变慢”，谈谈你的诊断思路？](#33)
* [第34讲 “Lambda能让Java程序慢30倍”你怎么看？](#34)
* [第35讲 JVM优化Java代码时都做了什么？](#35)
* [Java工程师必读书单](#35-1)
* [第36讲 谈谈MySQL支持的事务隔离级别，以及悲观锁和乐观锁的应用和原理](#36)
* [第37讲 谈谈SpringBean的生命周期和作用域](#37)
* [第38讲 对比Java标准NIO类库，你知道Netty是如何实现高性能的吗？](#38)
* [第39讲 谈谈常用的分布式ID的设计方案？Snowflake是否受冬令时切换影响？](#39)
* [结束语 技术没有终点](#40)
* [完结](#99)

# 正文
<h2 id="0">开篇词，以面试题为切入点有效提升Java内功</h2>
* Java初级、中级工程师要求：扎实的Java和计算机科学基础，掌握主流开发框架的使用。  
* Java高级工程师考察Java IO/NIO,Java虚拟机，底层源代码，分布式、安全和性能领域。  
* 涉及内容：Java基础，Java进阶，Java应用开发扩展，Java安全基础，Java性能基础  

<h2 id="1">第1讲 谈谈你对Java平台的理解</h2>
问题：谈谈你对Java平台的理解？“Java是解释执行”这句话正确吗？  
* Java是面向对象的语言，显著特点：（1）write once run anywhere；（2）垃圾回收，内存的分配和回收；  
* JRE是Java运行环境，包括JVM和Java类库及一些模块；JDK是JRE的一个超集，提供了更多的工具如编译器、各种诊断工具；  
* Java源代码首先通过javac编译成为字节码，然后通过JVM内嵌的解释器讲字节码转化为机器码。但是我们使用的Oracle JDK提供的Hotspot JVM提供了JIT编译器（动态编译器），可以在运行时将热点代码编译成机器码，这时候就是编译执行。  
* Java源代码经过javac编译成“.class”类型的字节码，在运行时JVM通过类加载器（Clacc-Loader）加载字节码，解释或者编译执行。-Xint参数表示只进行解释执行；-Xcomp参数表示关闭解释执行；-Xmixed参数表示混合模式；  
* 其他新的编译方式：AOT：直接将字节码编译成机器代码，Java9中就实验性的引入AOT特性。 
* Java语言的基本特性：面向对象，反射，泛型、Java类库：集合，网络，安全、Java虚拟机：垃圾收集器，运行时，动态编译，辅助功能、Java工具：jlink,jar,javac,sjavac,jmap,jstack、Java生态:spring,hadoop,spark,elasticsearch,maven.  

<h2 id="2">第2讲 Exception和Error有什么区别？</h2>
问题：对比exception和error，运行时异常与一般异常有什么区别？
* exception和error都继承了throwable类，Java中只有throwable类型的实例才可以被抛出或者捕获；  
* exception和error是Java平台设计者对不同异常情况的分类处理。exception是程序正常运行中，可以预料的意外情况，应该被捕获并处理；error是不大可能出现的情况会导致程序处于非正常的不可恢复的状态；  
* exception可分为可检查异常和不可检查异常，可检查异常在源代码中必须显式进行捕获处理，不检查异常就是运行是异常。  
* 常见error：LinkageError，NoClassDefFoundError,ExceptionInInitializerError,VirtualMachineError,OutOfMemoryError,StackOverflowError;常见exception：IOException,RuntimeException,ClassNotFoundException;  
* ClassNotFoundException当动态加载class的时候找不到类会抛出，一般在执行class.forName(),classLoader.loadClass()时候抛出；NoClassDefFoundError当编译成功以后执行过程中class找不到导致抛出该错误由JVM的运行时系统抛出。  
* 异常处理的基本语法：try-cache-finally,throw,throws  
* 异常处理注意：1尽量不要捕获类似于exception这样的通用异常，应该捕获特定异常；2不要生吞异常，不要假设这段代码可能不会发生。  
* try-cache代码段会产生额外的性能开销，要仅对有必要的代码段进行捕获，不用异常进行代码流程控制；Java每实例化一个exception都会对当时的栈进行快照，这是一个比较重的操作。  

<h2 id="3">第3讲 谈谈final、finally、finalize有什么不同？</h2>
* final可以用来修饰类、方法和变量，final修饰的类不可以继承扩展，修饰的变量不可以修改，修饰的方法不可以重写。  
* finally是Java保证重点代码一定要被执行的一种机制，可以使用try-finally来进行类似关闭JDBC连接、保证unlock锁等动作。  
* finalize是基础类java.lang.Object的一个方法，目的是保证对象在被垃圾收集前完成特定资源的回收。  
* final可以防止API被更改保证平台安全，可以避免意外赋值导致的编程错误，保护只读数据，减少额外开销。  
* final只能约束strList这个引用不可以被赋值，但是strList对象的行为不被final影响。List.of（）创建的本身就是不可变的List.  
* 实现一个immutable类需要做到：class自身声明为final，成员变量定义为private和final且不实现set方法，构造对象时成员变量使用深度拷贝来进行初始化，实现get方法时使用copy-on-write原则建立私有copy。  
* finally中的代码不被执行的情况：1 try-cache异常退出，system.exit(1)，2 无限循环，3 线程被杀死；  

<h2 id="4">第4讲 强引用、软引用、弱引用、幻象引用有什么区别？</h2>
不同的引用类型主要体现在对象不同的可达性状态和对垃圾收集的影响。  
* 强引用：（直接调用，不回收）最常见的普通对象引用，只要还有强引用指向一个对象就能表明对象还“活着”，垃圾收集器不会进行收集。对于一个普通的对象，如果没有其他引用关系，只要超过了引用的作用域或者显式地将强引用赋值为null，就可以被收集。  
* 软引用：（通过get（）方法，视内存情况回收）可以豁免一些垃圾收集，只有当JVM认为内存不足时才会去试图回收软引用指向的对象。软引用通常用来实现内存敏感的缓存，保证使用缓存的同时不会耗尽内存。  
* 弱引用：（通过get（）方法，永远回收）不能豁免垃圾收集，仅仅提供一种访问在弱引用状态下对象的途径。例如维护一种非强制性的映射关系，如果试图获取时对象还在，就使用它，否则重新实例化，是很多缓存实现的选择。  
* 幻想引用（虚引用）：（无法取得，不回收）不能通过他访问对象。提供了一种确保对象被finalize以后做某些事情的机制。Java平台自身的cleaner机制，利用幻想引用监控对象的创建和销毁。  
* 除了幻想引用，如果对象还没有被销毁，可以通过get方法获取原有对象，利用软引用和弱引用可以改变对象的可达性状态，如果错误的保持了强引用，对象就不能变回类似弱引用的可达性状态了，就会产生内存泄露。  

<h2 id="5">第5讲 String、StringBuffer、StringBuilder有什么区别？</h2>
* string是Java语言非常基础和重要的类，是immutable类，其不可变性导致类似拼接、剪裁字符串等动作都会产生新的string对象。  
* stringbuffer可以使用append或者add方法把字符串添加到已有序列的末尾或者指定位置，是一个线程安全的可修改字符串序列。  
* stringbuilder去掉了线程安全，有效减小了开销。  
* 字符串设计和实现考量：stringbuffer中通过添加synchronized关键字实现线程安全。构建时初始字符串长度加16，底层采用char（JDK9之后是byte）数组。  
* 字符串缓存：intern是一种显式地排重机制。  
* string自身的演化：Java9之前string采用char数组存储，Java9中通过一个byte数组加上一个标识编码来存储。  

<h2 id="6">第6讲 动态代理是基于什么原理？</h2>

<h2 id="7">第7讲 int和Integer有什么区别？</h2>
<h2 id="8">第8讲 对比Vector、ArrayList、LinkedList有何区别？</h2>
<h2 id="9">第9讲 对比Hashtable、HashMap、TreeMap有什么不同？</h2>
<h2 id="10">第10讲 如何保证集合是线程安全的？</h2>
<h2 id="11">第11讲 Java提供了那些IO方式？NIO如何实现多路复用？</h2>
<h2 id="12">第12讲 Java有几种文件拷贝方式？哪一种最高效？</h2>
<h2 id="13">第13讲 谈谈接口和抽象类有什么区别？</h2>
<h2 id="14">第14讲 谈谈你知道的设计模式</h2>
<h2 id="15">第15讲 synchronized和ReentrantLock有什么区别？</h2>
<h2 id="15-1">Java学习和面试看法</h2>
<h2 id="16">第16讲 synchronized底层如何实现？什么是锁的升级和降级？</h2>
<h2 id="17">第17讲 一个线程两次调用start()方法会出现什么状况？</h2>
<h2 id="18">第18讲 什么情况下Java程序会产生死锁？如何定位、修复？</h2>
<h2 id="19">第19讲 Java并发包提供了哪些并发工具类？</h2>
<h2 id="20">第20讲 并发包中的ConcurrentLinkedQueue和LinkedBlockingQueue有什么区别与联系？</h2>
<h2 id="21">第21讲 Java并发类库提供的线程池有哪几种？分别有什么特点？</h2>
<h2 id="22">第22讲 AtomicInteger底层实现原理是什么？如何在自己的产品代码中应用？</h2>
<h2 id="23">第23讲 类加载过程，什么是双亲委派模型？</h2>
<h2 id="24">第24讲 有哪些方法可以在运行时动态生成一个Java类？</h2>
<h2 id="25">第25讲 JVM内存区域的划分，哪些区域可能发生UotOfMemoryError？</h2>
<h2 id="26">第26讲 如何监控和诊断JVM堆内存和堆外内存使用？</h2>
<h2 id="27">第27讲 Java常见的垃圾收集器有哪些？</h2>
<h2 id="28">第28讲 谈谈你的GC调优思路？</h2>
<h2 id="29">第29讲 Java内存模型中的happen-before是什么？</h2>
<h2 id="30">第30讲 Java程序运行在Docker等容器环境有哪些新问题？</h2>
<h2 id="31">第31讲 Java应用开发中的注入攻击</h2>
<h2 id="32">第32讲 如何写出安全的Java代码？</h2>
<h2 id="33">第33讲 后台服务出现明显“变慢”，谈谈你的诊断思路？</h2>
<h2 id="34">第34讲 “Lambda能让Java程序慢30倍”你怎么看？</h2>
<h2 id="35">第35讲 JVM优化Java代码时都做了什么？</h2>
<h2 id="35-1">Java工程师必读书单</h2>
<h2 id="36">第36讲 谈谈MySQL支持的事务隔离级别，以及悲观锁和乐观锁的应用和原理</h2>
<h2 id="37">第37讲 谈谈SpringBean的生命周期和作用域</h2>
<h2 id="38">第38讲 对比Java标准NIO类库，你知道Netty是如何实现高性能的吗？</h2>
<h2 id="39">第39讲 谈谈常用的分布式ID的设计方案？Snowflake是否受冬令时切换影响？</h2>
<h2 id="40">结束语 技术没有终点</h2>
<h2 id="99">完结</h2>

## 觉得有价值 感谢支持
![赞赏码](./picture/AppreciationCode.jpg ) 