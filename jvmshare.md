JVM分享-2018.06.20
===========================
### 一些概念
- 1.jvm与普通虚拟机
- 2.jvm/jre/jdk
- 3.为什么需要jvm
### 核心
- 1.JVM运行流程
- 2.JVM运行时数据区域
- 3.JVM内存模型
### 类加载器
- 1.双亲委派模型(检查自底而上,启动自上而下)
- 2.为什么要双亲委派模型（避免重复加载不安全问题）
  * 2.1 启动类加载器 lib/rt.jar
  * 2.2 扩展类加载器 lib/ext/
  * 2.3 应用加载器 classpath
  * 2.4 自定义类加载器
### 垃圾收集算法
  * 1.标记—清除算法
  * 2.复制算法
  * 3.标记—整理算法
  * 4.分代收集算法
### 垃圾收集器
- 1.Serial收集器
- 2.ParNew收集器
- 3.ParallelScavenge收集器
- 4.SerialOld收集器
- 5.ParallelOld收集器
- 6.CMS收集器
- 7.G1收集器
### GC日志分析
### 工具使用
- jps：虚拟机进程状况工具
- jstat：虚拟机统计信息监视工具
- jinfo：Java配置信息工具
- jmap：Java内存映像工具
- jhat：虚拟机堆转储快照分析工具
- jstack：Java堆栈跟踪工具
- JConsole：Java监视与管理控制台
- VisualVM：多合一故障处理工具
### JVM调优
### JAVAP指令集
### JVM参数整理
- java堆栈大小设置相关
  * -Xms :设置Java堆栈的初始化大小
  * -Xmx :设置最大的java堆大小
  * -Xmn :设置Young区大小
  * -Xss :设置java线程堆栈大小
  * -XX:PermSize and MaxPermSize :设置持久带的大小
  * -XX:NewRatio :设置年轻代和老年代的比值
  * -XX:NewSize :设置年轻代的大小
  * -XX:SurvivorRation=n :设置年轻代中Eden区与两个S区的比值

- 打印垃圾回收信息及设置垃圾回收器
  * -verbose:gc :记录GC运行以及运行时间,一般用来查看GC是否有瓶颈
  * -XX:+PrintGCDetails :记录GC运行时的详细数据信息，包括新生占用的内存大小及消耗时间
  * -XX:-PrintGCTimeStamps :打印收集的时间戳
  * -XX:+UseParallelGC :使用并行垃圾收集器
  * -XX:ParallelGCThreads=N，设置并行垃圾回收的线程数，此值可以设置与机器处理机数量一致（有建议core+3/4）；
  * -XX:-UseConcMarkSweepGC :使用并发标志扫描收集器
  * -XX:-UseSerialGC :使用串行垃圾收集器
  * -Xloggc:filename :设置GC记录的文件
  * -XX:+UseGCLogFileRotation :启用GC日志文件的自动转储
  * -XX:GCLogFileSize=1M :控制GC日志文件的大小
  * -XX:+UseAdaptiveSizePolicy 设置此选项后，并行收集器会自动选择年轻代区大小和相应的Survivor区比例，以达到目标系统规定的最低相应时间或者收集频率等，此值建议使用并行收集器时，一直打开。
  * -XX:GCTimeRatio=n:设置垃圾回收时间占程序运行时间的百分比。公式为1/(1+n)
  * -XX:+UseCMSCompactAtFullCollection：使用并发收集器时，开启对年老代的压缩。
  * -XX:CMSFullGCsBeforeCompaction=0：上面配置开启的情况下，这里设置多少次Full GC后，对年老代进行压缩
  * -XX:+PrintGCApplicationConcurrentTime:打印每次垃圾回收前，程序未中断的执行时间。可与上面混合使用输出形式：Application time: 0.5291524 seconds
  * -XX:+PrintGCApplicationStoppedTime：打印垃圾回收期间程序暂停的时间。可与上面混合使用，输出形式：Total time for which application threads were stopped: 0.0468229 seconds
  * -XX:PrintHeapAtGC:打印GC前后的详细堆栈信息  

- 调试参数
  * -Xdebug
  * -Xnoagent
  * -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8000
  * -XX:HeapDumpPath=./java_pid.hprof :Path to directory or file name for heap dump.
  * -XX:-PrintConcurrentLocks :Print java.util.concurrent locks in Ctrl-Break thread dump.
  * -XX:-PrintCommandLineFlags :Print flags that appeared on the command line.

- 关于性能
  * -Xprof
  * -Xrunhprof

- 类加载和跟踪类加载和卸载的信息
  * Xbootclasspath :指定需要加载，但不想通过校验类路径。
  * JVM会对所有的类在加载前进行校验并为每个类通过一个int数值来应用
  * -XX:+TraceClassLoading :跟踪类加载的信息(诊断内存泄露很有用)
  * -XX:+TraceClassUnloading :跟踪类卸载的信息(诊断内存泄露很有用)
