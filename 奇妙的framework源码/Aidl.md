 
 # AIDL
 ## AIDL简单介绍
 AIDL 意思即 Android Interface Definition Language，翻译过来就是Android接口定义语言，是用于定义服务器和客户端通信接口的一种描述语言，可以拿来生成用于IPC的代码。从某种意义上说AIDL其实是一个模板，因为在使用过程中，实际起作用的并不是AIDL文件，而是据此而生成的一个IInterface的实例代码

 ### AIDL支持的数据类型包括以下几种：

Java的8种基本数据类型：int，short，long，char，double，byte，float，boolean；
CharSequence类型，如String、SpannableString等；
ArrayList，并且T必须是AIDL所支持的数据类型；
HashMap<K，V>，并且K和V必须是AIDL所支持的数据类型；
所有Parceable接口的实现类，因为跨进程传输对象时，本质上是序列化与反序列化的过程；
AIDL接口，所有的AIDL接口本身也可以作为可支持的数据类型；


### 什么时候使用AIDL：

只有在你先允许来自不同应用的客户端跨进程通信访问你的Service，并且想要在你的Service处理多线程的时候才是必要的。

先了解一些概念

Binder:Binder是对IPC的具体实行，是IPC的一种具体实现.其本质也是调用系统底层的共享内存实现.

AIDL:进程间的通信，速度快(系统底层直接是共享内存)，性能稳，效率高，一般进程间通信就用它. AIDL是Binder机制向外提供的接口，目的就是为了方便对Binder的使用；

消息(Messager)：Messenger本质也是AIDL，只是进行了封装，开发的时候不用再写.aidl文件,效率应该是和Aidl是一样的，与Aidl的区别在于Messager是线程安全的，而Aidl是非线程安全的，所以Aidl在使用的时候应该注意这个问题;

广播(BroadcastReceiver):只要注册了广播，都能收到，优点范围广，缺点速度慢必须在一定时间完成处理操作,同其他Android四大组件一样,都不能执行耗时操作;

ContentProvider:暴露app的数据访问接口，让其他应该访问app数据.同时也能通过ContentProvider来访问第三方的一些app数据(如通讯录,日历等暴露接口的应用);

Intent:Intent是最高层级的封装，实质是封装了对Binder的使用，当然Intent也常常在同一进程中调用，只是把两种方式封装在一起了.

## 探秘Binder通信原理与驱动机制