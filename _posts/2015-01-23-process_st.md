---
layout : post
title : process status
---

## Linux 下的进程状态：

首先查看进程状态的命令PS

PS的用法：ps  -  parameter

常用参数：

`-A` 显示所有的进程(等价于`-e`)

`-a` 显示一个终端的所有进程

`c`   显示进程的真实名称

`-e`  等价于`-A`

`-N`  忽略选择

`-d`  显示所有进程，但是省略所有的会话引线

`-x`  显示没有控制终端的进程，同时显示各个命令的具体路径。`dx`  不可合用

`-p` pid进程使用cpu时间

`-u` uid or username选择有效的用户id或者用户名

`-g` gid or groupname 显示组的所有进程

`U`  username显示该用户下的所有进程，且显示各个命令的线下路径ps U zhangsan

`-f` 全部列出，通常和显示选项联用。ps -fa or ps -fx

`-m` 显示所有的线程

`-H` 显示进程的层次 ps -Ha

<hr>
#### ps -aux输出格式

`USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND USER`

`USER` 进程拥有者

`PID` 进程pid

`%CPU` 占用cpu的使用率

`%MEM` 占用内存大小

`VSZ` 占用虚拟内存大小

`RSS`  占用物理内存

`TTY` linux的终端号pts/1

<hr>
**`STAT`  运行的状态：**

 - D：不可中断终端的休眠状态(IO进程)

 - R：正在运行，在可中断队列中

 - S：处于休眠状态，静止状态

 - T：停止或被跟踪，暂停执行

 - W：进入内存交换

 - X：杀死的进程

 - Z：僵死进程不存在但暂时无法消除

 - s：进程的领导者(在它之下有子进程)

 - l：多进程的(CLONE_THREAD,类似NPTL pthreads)

 - +：位于后台的进程组

<hr>
#### Kill终止进程有十几种控制进程的方法

`kill -STOP [pid]`发送SIGSTOP(17,19,23)停止一个进程，而不消灭这个进程

`kill -CONT [pid]` 发送SIGCONT(19,18,25)重新开始一个停止进程

`kill -KILL [pid]` 发送SIGKILL(9)强迫进程立即停止，不实施清理操作

`kill -9 -1` 终止你拥有的全部进程

SIGKILL和SIGSTOP信号不能被，封锁或者忽略，但是，其他信号可以

####bash下Ctr-C，Ctr-D，Ctr-Z的区别

`Ctr-C` To terminate 终止进程，发送SIGINT信号
`Ctr-D` signals EOF 文件结束符发送SIGTSTP信号
`Ctr-Z` suppends a program 暂停一个进程

测试程序

```
<?php 
while(true) {
	echo "Hello\n";
	sleep(1);
}
?>
```

`Ctr-D`没有效果

`Ctr-Z`显示如下：

```
[1]+  Stopped  /home/work/lamp/php5/bin/php while.php

```

此时这个进程只是被暂停掉了，并没有kill掉

而使用`Ctr-C`这个进程就是被kill掉了

对于`Ctr-D`的作用不是发送信号，而是表示一个特殊的二进制值，表示EOF

```


```

对于暂停了的进程如何恢复执行：

`jobs`命令把暂停的进程显示出来

fg %jobnumber 将后台的任务拿到前台来处理

bg %jobnumber 将任务放到后台去处理

kill 管理后台的任务

