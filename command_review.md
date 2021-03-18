# command review

## about	cpu

###  top

```
相当于windows下的任务管理器
进入后 
M	按内存使用排序
P	按cpu使用排序
N	以pid大小排序
```

### pidstat

```
 pidstat主要用于监控全部或指定进程占用系统资源的情况，如CPU，内存、设备IO、任务切换、线程等。pidstat首次运行时显示自系统启动开始的各项统计信息，之后运行pidstat将显示自上次运行该命令以后的统计信息。用户可以通过指定统计的次数和时间来获得所需的统计信息。
 -u	cpu使用统计
 -r	内存使用统计
 =d	IO情况统计
 -p	选定特定进程
```

## about ROM

### free

```
free指令会显示内存的使用情况
包括实体内存，虚拟的交换文件内存，共享内存区段，以及系统核心使用的缓冲区
[ljtj@ljtjhome ~]$ free -h
              total        used        free      shared  buff/cache   available
Mem:          4.3Gi       1.6Gi       1.7Gi        17Mi       946Mi       2.4Gi
Swap:         3.0Gi          0B       3.0Gi

```

## about 	disk

### fdisk / gdisk

```
分区工具
```

### mkfs

```
make file system
硬盘格式化命令 
-t 指定file system
```

### dstat

```
实时地看到所有系统资源
```

## about NAT

### ifstat / iftop

```
默认ifstat不监控回环接口，显示的流量单位是KB。
-a	监控所有网络接口
```

### netstat

```
-a (all)显示所有选项，默认不显示LISTEN相关
-t (tcp)仅显示tcp相关选项
-u (udp)仅显示udp相关选项
-n 拒绝显示别名，能显示数字的全部转化成数字。
-l 仅列出有在 Listen (监听) 的服務状态

-p 显示建立相关链接的程序名
-r 显示路由信息，路由表
-e 显示扩展信息，例如uid等
-s 按各个协议进行统计
-c 每隔一个固定时间，执行该netstat命令。
LISTEN和LISTENING的状态只有用-a或者-l才能看到
```

## 监测命令

### perf

```
软件性能分析的工具
应用程序可以利用 PMU，tracepoint 和内核中的特殊计数器来进行性能统计
```

