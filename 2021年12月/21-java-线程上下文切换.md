每日一句
When I shiver with cold, not a snowflake is innocent. 当我冷得瑟瑟发抖时，没有一片雪花是无辜的。

概述
CPU 利用时间片轮询来为每个任务都服务一定的时间，然后把当前任务的状态保存下来，继续服务下一个任务。 任务的状态保存及再加载就叫做线程的上下文切换。

1. 进程：指一个运行中的程序的实例。在一个进程内部可以有多个线程在同时运行，并与创建它的进程共享同一地址空间（一段内存区域）和其他资源

2. 上下文：指线程切换时CPU寄存器和程序计数器所保存的当前线程的信息

3. 寄存器：指CPU内部容量较小但速度很快的内存区域（与之对应的是CPU外部相对较慢的RAM主内存）。寄存器通过对常用值（通常是运算的中间值）的快速访问来加快计算机程序运行的速度

4. 程序计数器：是一个专用的寄存器，用于表明指令序列中CPU正在执行的位置，存储的值为正在执行的指令的位置或者下一个将被执行的指令的位置，这依赖于特定的系统。

上下文切换
上下文切换指的是内核（操作系统的核心）在CPU上对进程或者线程进行切换。 上下文切换过程中的信息被保存在进程控制块（PCB-Process Control Block）中。PCB又被称作切换帧（SwitchFrame）。 上下文切换的信息会一直被保存在CPU的内存中，直到被再次使用。

上下文切换流程如下：

（1）挂起一个进程，将这个进程在CPU中的状态（上下文信息）存储于内存的PCB中。

（2）在PCB中检索下一个进程的上下文并将其在CPU的寄存器中恢复。

（3）跳转到程序计数器所指向的位置（即跳转到进程被中断时的代码行）并恢复该进程。

时间片轮转方式使多个任务在同一CPU上的执行有了可能.

引起线程上下文切换的原因
引起线程上下文切换的原因如下。

◎ 当前正在执行的任务完成，系统的CPU正常调度下一个任务。

◎ 当前正在执行的任务遇到I/O等阻塞操作，调度器挂起此任务，继续调度下一个任务。

◎ 多个任务并发抢占锁资源，当前任务没有抢到锁资源，被调度器挂起，继续调度下一个任务。

◎ 用户的代码挂起当前任务，比如线程执行sleep方法，让出CPU。

◎ 硬件中断。

美文佳句
人这一生，其实面临着很多选择。大到人生规划，小到日常生活，常常都不会尽善尽美。

我们的每一个选择，无论后来怎样，至少在我们选择的那一刻，一定是符合我们当时的需求的。

若选择之后，这山望着那山高，始终不满意自己的选择，一直惦记着其他选择，那只会让自己迷失在选择之中，错过今后更多的选择。

很多时候，选择无关对错，也无关优差。既然选择了一条路，试探再多的分岔路口，也不如走好脚下这条路。

曾看过这样一段话：生命怎么活都会有遗憾，关键在于你怎么去领悟，给这个遗憾的部分更崇高的向往，然后尊重、包容它，反而会把这个遗憾的部分变成一种生命力的圆满。

所以，有遗憾不可怕，可怕的是把遗憾一直当遗憾。其实，你不必羡慕任何人的选择，能把自己选择的路走好，也是一种了不起的能力。