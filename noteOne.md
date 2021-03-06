1.动态路由协议分为内部网关协议（IGP）和外部网关协议（EGP）

 * 自治域内部采用的路由协议称为内部网关协议，常见的有RIP，OSPF。

 * 外部网关协议主要用于多个自治域之间的路由选择，常见的是BFP和BGP-4.

2.如果因为时间片用完而被暂停执行，则进程由执行到就绪。
如果因为某事件而使进程执行受阻，如访问某临界资源，而该资源正被其他进程访问，则进程由执行到等待。

![](https://i.imgur.com/gWQjN5Q.png)

3.关于死锁等

 * 饥饿是指一个可运行的进程尽管能继续执行，但被调度程序无限期地忽略，而不能被调度执行的情形。
 * 死锁是两个或两个以上的进程其中每个进程都在等待其他进程做完某些事而不能继续执行。
 * 互斥是当一个进程在临界区访问共同资源是时，其他进程不能进入该临界区访问任何共享资源。
 * 同步

4.死锁产生的四个必要条件

 * 互斥条件：一个资源每次只能被一个进程使用
 * 请求与保持条件：一个进程因请求资源而阻塞时，对已经获得的资源保持不放
 * 不剥夺条件：进程已获得的资源在未使用之前，不能强行剥夺
 * 循环等待条件：若干进程之间形成头尾相接的循环等待资源关系

相应的预防措施：
 * 采用静态资源分配策略，破坏部分分配条件
 * 允许进程剥夺其他进程的资源，破坏不可剥夺的条件
 * 采用字段有序分配，破坏环路条件
 * 注意：互斥条件无法被破坏的。 

5.数据库中where子句不能包含聚集函数，having可以有

6.三级模式之间存在两种映射，分别是模式和子模式（外模式）之间，模式和内模式之间。

7.避免活锁：先来先服务，避免死锁：一次封锁，顺序封锁