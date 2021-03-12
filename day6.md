# day6

## 第七章Linux磁盘与文件系统管理

耗时40m+

磁盘分区 两种格式：MBR分区表、GPT分区表（限制少。支持2TB以上）

虚拟化 /dev/sd[a-p]

### 文件系统特性 

Linux 正统文件系统为Ext2(Linux second extended file system)

#### 索引式文件系统 EXT2/EXT3/EXT4

文件系统将两部分参数（文件权限与文件属性）分别放置不同区块。权限与属性放置inode。实体数据放置 data block，superlock超级区块记录文件系统整体信息，包括inode、block 总量、使用量、剩余量等

​	问题：格式化慢

```
superblock:记录此 filesystem 的整体信息，包括 inode/block 的总量、使用量、剩余量，以及文件系统的格式与相关信息等;
inode:记录义件的属性，一个义件占用一个inode，同时记录此文件的数据所在的 block号码;
block:实际记录文件的内容，若文件太大时，会占用多个block 。
```

ext2 分区索引

![image-20210310162800555](G:\linux_review\image-20210310162800555.png)

其中，最前面的为启动扇区 boot sector 

上图datablock中

![image-20210310162948470](G:\linux_review\image-20210310162948470.png)

##### inode详解

inode记录的数据类型至少有

```
该文件的存取模式(read/write/excute):
该文件的拥有者与群组(owner/group);该文件的容量:
该文件建立或状态改变的时间(ctime);
最近一次的读取时间(atime);
最近修改的时间(mtime);
定义文件特性的旗标(flag)，如 SetUID...;
该文件真正内容的指向(pointer):
```

1、每个inode大小固定128bytes（ext4与xfs可设定256bytes）

2、每个文件都会占用inode，故文件系统能简历的文件数量与inode的数量有关

3、读取文件时需先找到inode，并分析inode权限是否符合。符合后才可开始读取block内容

##### superblock

主要记录有

```
block 与 inode 的总量;
未使用与已使用的 inode / block数量;
block 与 inode 的大小(block 为 1,2,4K，inode为 128bytes或256bytes);
filesystem 的挂载时间、最近一次写入数据的时间、最近一次检验磁盘(fsck)的时间等文件系统的相关信息;
一个valid bit数值，若此文件系统已被挂载，则 valid bit为 0，若未被挂载，则valid bit为 1。
```

#### dumpe2fs：查询Ext家族superblock信息

```
dumpe2fs [-bh] nameofdev
```



#### 查看当前linux 文件系统 df -T

### 日志式文件系统的出现是为了简化数据一致性检查

### XFS  一种日志式文件系统

#### data dection 资料区

包括 inode/data block/superblock 等数据，都 放置在这个区块。 这个数据区与 ext 家族的 block group 类似，也是分为多个储存区群组 (allocation groups) 来分别放置文件系统所需要的数据。 每个储存区群组都包含了 (1)整个文件系 统的 superblock、 (2)剩余空间的管理机制、 (3)inode 的分配与追踪

#### log section 活动登录区

来纪录文件系统的变化，其实有点像是日志区啦！文件的变化会在这 里纪录下来，直到该变化完整的写入到数据区后， 该笔纪录才会被终结

#### realtime section 实时运作区

有文件要被建立时，xfs 会在这个区段里面找一个到数个的 extent 区块，将文件放置在这个区 块内，等到分配完毕后，再写入到 data section 的 inode 与 block 去

#### xfs_info XFS 文件系统的描述数据观察

## Linux异步处理  asynchronously

常用文件数据放入内存，加速读写，若内存中的文件数据被更改，进行标记。不定时将标记内存数据写入磁盘，保持磁盘与内存数据一致性。

## mount point

可用 ls -ild 查看inode

#### df命令查看磁盘整体使用情况

#### du评估文件系统的磁盘使用量

/proc 为linux系统加载的系统数据，且是挂在内存中的

/dev/shm内存虚拟的磁盘空间

#### ln hard link/symbolic link

##### hard link		ln 不加参数

硬链接实际为链接到某inode号码的关联记录  	既不增加inode 也不号用block

不能跨filesystem

不能link目录

##### sysbomlic link

ln -s  可连接目录 相当快捷方式

## 磁盘的分区、格式化、校验和挂载

lsblk查看所有磁盘状态

gdisk/fdisk 进行磁盘分区

mkfs 磁盘格式化（建立文件系统）

xfs_repair 文件系统校验

fsck 

mount / umount 挂载与解除

![image-20210312220221362](G:\linux_review\image-20210312220221362.png)

### 开机挂载

/etc/fstab

/etc/mtab