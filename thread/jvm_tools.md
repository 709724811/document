## jvm tools

### 1，jstat

jstat命令可以查看堆内存各部分的使用量，以及加载类的数量。命令格式：

jstat [-命令选项] [vmid] [间隔时间/毫秒] [查询次数]

**类加载统计**

```bash
[apps@mvxl5695 logs]$ jstat -class 29044
Loaded  Bytes  Unloaded  Bytes     Time   
 12078 21123.3        0     0.0      10.88
```

- **Loaded:**加载class的数量

- **Bytes：**所占用空间大小

- **Unloaded：**未加载数量

- **Bytes:**未加载占用空间

- **Time：**时间

**编译统计**

```bash
[apps@mvxl5695 logs]$ jstat -compiler 29044
Compiled Failed Invalid   Time   FailedType FailedMethod
   12870      1       0    91.07          1 java/lang/reflect/AccessibleObject isAnnotationPresent
```

- **Compiled：** 编译的类数量

- **Failed：** 失败的类数量

- **Invalid：** 不可用的数量

- **Time：** 编译花费的时间

- **FailedType：** 失败的类型

- **FailedMethod：** 失败的类和方法ass

**垃圾回收统计**

```bash
[apps@mvxl5695 logs]$ jstat -gc 29044
 S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT   
1024.0 1024.0 640.0   0.0   50688.0  30872.1   236544.0   80945.0   64856.0 61847.0 8320.0 7776.3   8956   43.103   3      0.444   43.547
```

- **S0C：** 第一个幸存区的大小

- **S1C：** 第二个幸存区的大小

- **S0U：** 第一个幸存区已使用大小

- **S1U：** 第二个幸存区已使用大小

- **EC：** 伊甸园区的大小

- **EU：** 伊甸园区已使用大小

- **OC：** 老年代的大小

- **OU：** 老年代已使用大小

- **MC：** 方法区的大小

- **MU：** 方法去的已使用大小

- **CCSC：** 压缩类的空间大小

- **CCSU：** 压缩类已使用空间大小

- **YGC：** 年轻代垃圾回收次数

- **YGCT：** 年轻代垃圾回收耗时

- **FGC：** 老年代垃圾回收次数

- **FGCT：** 老年代垃圾回收耗时

- **GCT：** 垃圾回收消耗总时间

**堆内存统计**

```bash
[apps@mvxl5695 logs]$ jstat -gccapacity 29044
 NGCMN    NGCMX     NGC     S0C   S1C       EC      OGCMN      OGCMX       OGC         OC       MCMN     MCMX      MC     CCSMN    CCSMX     CCSC    YGC    FGC 
 86016.0 1372672.0  52736.0 1024.0 1024.0  50688.0   172032.0  2745856.0   236544.0   236544.0      0.0 1105920.0  64856.0      0.0 1048576.0   8320.0   8956     3
```

- **NGCMN：** 新生代最小容量

- **NGCMX：** 新生代最大容量

- **NGC：** 当前新生代容量

- **S0C：** 第一个幸存区大小

- **S1C：** 第二个幸存区大小

- **EC：** 伊甸园区的大小

- **OGCMN：** 老年代的最小容量

- **OGCMX：** 老年代的最大容量

- **OGC：** 当前老年代的容量

- **MCMN：** 元数据(meta)空间最小容量

- **MCMX：** 元数据(meta)空间最大容量

- **MC：** 元数据空间当前容量

- **CCSMN（Compressed class space minimum capacity ）：** 压缩类最小空间大小

- **CCSMX（Compressed class space max capacity ）：** 压缩类最大空间大小

- **CCSC：** 当前压缩类空间大小 

- **YGC：** 年轻代GC次数

- **FGC：** 年老代GC次数

  

**新生代垃圾回收统计**

```bash
[apps@mvxl5695 logs]$ jstat -gcnew 29044
 S0C    S1C    S0U    S1U   TT MTT  DSS      EC       EU     YGC     YGCT  
1024.0 1024.0    0.0  603.0 15  15 1024.0  50688.0   2057.6   8959   43.117
```

- **S0C：** 第一个幸存区大小
- **S1C：** 第二个幸存区大小
- **S0U：** 第一个幸存区使用大小
- **S1U：** 第二个幸存区使用大小
- **TT：** 对象在新生代存活的次数
- **MTT：** 对象在新生代最大的存活次数
- **DSS：** 期望的幸存区大小
- **EC：** 伊甸园区大小
- **EU：** 伊甸园区使用大小
- **YGC：** 年轻代垃圾回收次数
- **YGCT：** 年轻代垃圾回收用时



**新生代内存统计**

```bash
[apps@mvxl5695 logs]$ jstat -gcnewcapacity 29044
  NGCMN      NGCMX       NGC      S0CMX     S0C     S1CMX     S1C       ECMX        EC      YGC   FGC 
   86016.0  1372672.0    52736.0 457216.0   1024.0 457216.0   1024.0  1371648.0    50688.0  8959     3
```

- **NGCMN：** 新生代最小容量

- **NGCMX：** 新生代最大容量

- **NGC：** 新生代当前容量

- **S0CMX：** 最大幸存1区大小

- **S0C：** 幸存1区当前大小

- **S1CMX：** 最大幸存2区大小

- **S1C：** 幸存2区当前大小

- **ECMX：** 伊甸园区最大大小

- **EC：** 伊甸园区当前大小

- **YGC：** 年轻代垃圾回收次数

- **FGC：** 老年代回收次数

  

**老年代垃圾回收统计**

```bash
[apps@mvxl5695 logs]$ jstat -gcold 29044
   MC       MU      CCSC     CCSU       OC          OU       YGC    FGC    FGCT     GCT   
 64856.0  61847.0   8320.0   7776.3    236544.0     80953.0   8959     3    0.444   43.562
```

- **MC：** 方法区大小
- **MU：** 方法区已使用大小
- **CCSC：** 压缩类空间大小
- **CCSU：** 压缩类空间已使用大小
- **OC：** 年老代空间大小
- **OU：** 年老代已使用空间大小
- **YGC：** 年轻代GC次数
- **FGC：** 年老代GC次数
- **FGCT：** 年老代GC耗时
- **GCT：** GC总耗时



**老年代内存统计**

```bash
[apps@mvxl5695 logs]$ jstat -gcoldcapacity 29044
   OGCMN       OGCMX        OGC         OC       YGC   FGC    FGCT     GCT   
   172032.0   2745856.0    236544.0    236544.0  8959     3    0.444   43.562
```

- **OGCMN：** 老年代最小容量
- **OGCMX：** 老年代最大容量
- **OGC：** 老年代当前容量
- **OC：** 老年代大小
- **YGC：** 年轻代大小
- **FGC：** 年老代GC次数
- **FGCT：** 年老代GC耗时
- **GCT：** GC总耗时



**元数据空间统计**

```bash
[apps@mvxl5695 logs]$ jstat -gcmetacapacity 29044
   MCMN       MCMX        MC       CCSMN      CCSMX       CCSC     YGC   FGC    FGCT     GCT   
       0.0  1105920.0    64856.0        0.0  1048576.0     8320.0  8959     3    0.444   43.562
```

- **MCMN：** 最小元数据空间容量
- **MCMX：** 最大元数据空间容量
- **MC：** 元数据空间大小
- **CCSMN：** 最小压缩类空间大小
- **CCSMX：** 最大压缩类空间大小
- **CCSC：** 当前压缩类空间大小
- **YGC：** 年轻代大小
- **FGC：** 年老代GC次数
- **FGCT：** 年老代GC耗时
- **GCT：** GC总耗时



**总结垃圾回收统计**

```bash
[apps@mvxl5695 logs]$ jstat -gcutil 29044
  S0     S1     E      O      M     CCS    YGC     YGCT    FGC    FGCT     GCT   
 62.50   0.00   3.73  34.22  95.36  93.47   8960   43.123     3    0.444   43.567
```

- **S0：** 幸存1区当前使用比例
- **S1：** 幸存2区当前使用比例
- **E：** 伊甸园区当前使用比例
- **O：** 老年代当前使用比例
- **M：** 元数据空间当前使用比例
- **CCS：** 压缩使用比例
- **YGC：** 年轻代GC次数
- **YGCT：** 年轻代GC总耗时
- **FGC：** 老年代GC次数
- **FGCT：** 老年代GC耗时
- **GCT：** GC总耗时



**编译统计**

```bash
[apps@mvxl5695 logs]$ jstat -printcompilation 29044
Compiled  Size  Type Method
   12871   3256    1 com/sun/jmx/interceptor/DefaultMBeanServerInterceptor unregisterFromRepository
```

- **Compiled：** 最近编译的方法执行的编译任务数(Number of compilation tasks performed by the most recently compiled method.)
- **Size：** 最近编译方法的字节码数量( Number of bytes of byte code of the most recently compiled method.)
- **Type：** 最近编译方法的编译类型(Compilation type of the most recently compiled method.)
- **Method：** 方法名标识(Class name and method name identifying the most recently compiled method.)