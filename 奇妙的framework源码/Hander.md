https://mp.weixin.qq.com/s/36T03bTreDSAXBWo62gRvg

Handler是Android中的消息处理机制，是一种线程间通信的解决方案，同时你也可以理解为它天然的为我们在主线程创建一个队列，队列中的消息顺序就是我们设置的延迟的时间，如果你想在Android中实现一个队列的功能，不妨第一时间考虑一下它。本文分为三部分：

Handler的源码和常见问题的解答

一个线程中最多有多少个Handler，Looper，MessageQueue？

Looper死循环为什么不会导致应用卡死，会耗费大量资源吗？

子线程的如何更新UI，比如Dialog，Toast等？系统为什么不建议子线程中更新UI?

主线程如何访问网络？

如何处理Handler使用不当造成的内存泄漏？

Handler的消息优先级，有什么应用场景？

主线程的Looper何时退出？能否手动退出？

如何判断当前线程是安卓主线程？

正确创建Message实例的方式？


Handler深层次问题解答

ThreadLocal

epoll机制

Handle同步屏障机制

Handler的锁相关问题

Handler中的同步方法


Handler在系统以及第三方框架的一些应用

HandlerThread

IntentService

如何打造一个不崩溃的APP

Glide中的运用


Handler的源码和常见问题的解答

下面来看一下官方对其的定义：

A Handler allows you to send and process Message and Runnable objects associated with a thread's MessageQueue. Each Handler instance is associated with a single thread and that thread's message queue. When you create a new Handler it is bound to a Looper. It will deliver messages and runnables to that Looper's message queue and execute them on that Looper's thread.

大意就是Handler允许你发送Message/Runnable到线程的消息队列(MessageQueue)中，每个Handler实例和一个线程以及那个线程的消息队列相关联。当你创建一个Handler时应该和一个Looper进行绑定（主线程默认已经创建Looper了，子线程需要自己创建Looper），它向Looper的对应的消息队列传送Message/Runnable同时在那个Looper所在线程处理对应的Message/Runnable。下面这张图就是Handler的工作流程。