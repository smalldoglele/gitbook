#### JDK5 新特性之线程同步工具类
+ Semaphore  [ˈseməfɔ:(r)] 旗语 色摸佛
Semaphore可以控制同时访问资源的线程个数, 实现资源允许的并发访问数.
  - acquire() 获得通道
  - release() 释放通道
  
+ CyclicBarrier [ˈsaɪklɪk] 周期的，循环的;轮转的 塞科理科 [ˈbæriə(r)] 屏障;障碍;栅栏;分界线
CyclicBarrier  表示大家彼此等待，集合好后才开始出发，分散活动后又在指定地点集合碰面。
   - await() 先到的等待后到的，当全部都到达时才会继续向下执行 
   - getNumberWaiting() 获得到达的数量
+ CountDownLatch [lætʃ] 门闩;弹簧锁
CountDownLatch 犹如倒计时计数器, 调用CountDownLatch对象的countDown方法就将计数器减一, 当计数到达0时, 则所有等待者或单个等待者开始执行.
  - await（）线程等待
  - countDown() 将计数器减1，当计数为0的时候，主线程启动
+ Exchanger  [ɪks'tʃeɪndʒə] 交换器
用于实现两个人之间的数据交换, 每个人在完成一定的事务后想与对方交换数据, 第一个先拿出数据的人将一直等待第二个人拿着数据到来时, 才能彼此交换数据:
 - exchange(data) 交换数据
 #### JDK 5 新特性之线程池
 1. 线程池的概念
   - 降低资源消耗，通过重复利用已经创建的线程减低线程创建和销毁的消耗
   - 提高响应速度，当任务到达的时候后 任务可以不需要等待线程的创建就能立刻执行
   - 提高线程的可管理性，线程是稀缺资源，如果无限制的消耗系统同资源，会降低系统的稳定性
   
 线程池：首先创建一些线程，当服务器接收到一个客户请求后，就从线程池中取出一个空闲的线程为之服务，服务完成之后不关闭该线程，而是将该线程回到线程池中；
 在线程池的编程模式下，任务是提交给整个线程池的，而不是直接交给某个线程，线程池在拿到任务后，它就在内部找有无空闲的线程，找到后再把任务交给内部某个空闲的线程，这就是封装。记住：任务是提交给整个线程池的，一个线程同时只能执行一个任务，但可以同时向一个线程池提交多个任务。
 2. 线程的创建与关闭
 
   1. 创建固定大小的线程池
   `ExecutorService threadPool=Executors.newFixedThreadPool(3)`
   2.创建缓存线程池
   `ExecutorService threadPool=Executors.newCacachedThreadPool()`
   3.创建单一线程池：线程死后有会重新创建一个新的
   `ExecutorService threadPool=Executors.newSingleThreadExecutor()`
   4.关闭线程池
   ```java
   threadPool.shutdown() //所有任务完成后就结束线程
   threadPool.shutdownNow() //马上结束线程
   ```
 3.用线程池启动定时器
 ```java
ScheduledExecutorService service = Executors.newScheduledThreadPool(3);
service.schedule();
service.scheduleAtFixedRate();


 ```
 
   