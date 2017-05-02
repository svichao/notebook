# [什么是 ANR？][1]

标签（空格分隔）： ANR

---

**什么是 ANR？**
ANR:Application Not Responding，即应用无响应

**ANR一般有三种类型：**

 1. KeyDispatchTimeout(5 seconds) --主要类型按键或触摸事件在特定时间内无响应
 2. BroadcastTimeout(10 seconds) --BroadcastReceiver在特定时间内无法处理完成
 3. ServiceTimeout(20 seconds) --小概率类型 Service在特定的时间内无法处理完成

**KeyDispatchTimeout**
Akey or touch event was not dispatched within the specified time（按键或触摸事件在特定时间内无响应）
具体的超时时间的定义在framework下的ActivityManagerService.java

    //How long we wait until we timeout on key dispatching.
    static final int KEY_DISPATCHING_TIMEOUT = 5*1000
**超时时间的计数一般是从按键分发给app开始。超时的原因一般有两种：**
(1)当前的事件没有机会得到处理（即UI线程正在处理前一个事件，没有及时的完成或者looper被某种原因阻塞住了）
(2)当前的事件正在处理，但没有及时完成

**一些避免 ANRs 的技巧**

 - 建议使用 AsycnTask 来异步处理后台数据
 - 相比起 AsycnTask 来说，创建自己的线程或者 HandlerThread 稍微复杂一点。如果你想这样做，你应该通过
   Process.setThreadPriority() 并传递 THREAD_PRIORITY_BACKGROUND
   来设置线程的优先级为"background"。
 - 如果你的程序需要响应正在后台加载的任务，在你的 UI 中可以显示 ProgressBar 来显示进度。
 - 对游戏程序，在工作线程执行计算的任务。
 - 如果你的程序在启动阶段有一个耗时的初始化操作，可以考虑显示一个闪屏，要么尽快的显示主界面，然后马上显示一个加载的对话框，异步加载数据。无论哪种情况，你都应该显示一个进度信息，以免用户感觉程序有卡顿的情况。
 - 使用性能测试工具，例如 Systrace 与 Traceview 来判断程序中影响响应性的瓶颈。

>参考自
[Android ANR 分析解决方法][2]
[官方文档（中文版）][3]


  [1]: http://ife.baidu.com/note/detail/id/56
  [2]: http://www.cnblogs.com/purediy/p/3225060.html
  [3]: http://hukai.me/android-training-course-in-chinese/performance/perf-anr/index.html