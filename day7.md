# day7 

## 第九章vi/vim

```
command mode
insert mode
command-line mode
```

:sp 分区窗口

ctrl+w + 方向 键盘切换分区

iconv 进行文件编码转换

:enconding=utf-8 改变显示的编码方式

![image-20210313132906610](G:\linux_review\image-20210313132906610.png)

常用命令如上图

## 进程相关命令补充

#### &

用在一个命令的最后，可以把这个命令放到后台执行
<Ctrl> +z
将一个正在前台执行的命令放到后台，并暂停

#### jobs

查看当前有多少在后台运行的进程。这是一个作业控制命令

#### fg(foreg roud process)

将后台中的命令调至前台继续运行。如果后台中有多个命令，可以用fg ljobnumber]将选中的命令调出，jobnumber是通过jobs命令查到的后台正在执行的命令的序号  (不是pid)

#### bg(back groud process)

将一个在后台暂停的命令，变成继续执行。如果后台中有多个命令，可以用bg  %jobnumber将选中的命令调出，%jobnumber是通过jobs命令查到的后台正在执行的命令的序号(不是pid)