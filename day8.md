# BASH / shell

## 定义 什么是shell/bash

shell 操作应用程序的接口

bash 是Bourne Again SHell 的简称 是Linux的通用shell 版本

查询系统支持的shell 在/etc/shells 文件

![image-20210313133833263](G:\linux_review\image-20210313133833263.png)

## bash优点

#### bash内建command

##### history

```
history -[raw] histfile
history n
history -c
```

<img src="G:\linux_review\image-20210313200256938.png" alt="image-20210313200256938" style="zoom:200%;" />

history 记录默认在 ~/.bash_history

账号注销时，才会写入bash_history ，注意多账户同时登入写入内容

##### alias 别名

#### tab

#### shell scripts

#### wildcard 通配符

#### 可用type观察指令是否是bash内建指令

#### 小技巧

![image-20210313140340406](G:\linux_review\image-20210313140340406.png)

ctrl + a /e  光标快速左移/右移 

CTRL+ u /k 删除光标左侧全部 / 右侧全部

#### BASH进站与欢迎信息

默认执行文件为/etc/issue 文件下

### bash环境配置文件 

#### login / non-login shell

##### login shell 读取 

1. /etc/profile 系统整体设定，最好不要动
2. ~/.bash_profile (or ~/.bash_login or ~/.profile) 个人设定，可以改写

可用source读取环境配置文件而不用重新登入

##### non-login shell 只会读~/.bashrc

### 终端机环境设置 stty(settting tty)

## shell变量

变量前加$ 

### tips

变量内容用引号时，双引号保留特殊字符，单引号转换为纯文本

\可用

### ` 反单引号

反单引号

```shell
`command` 或者 $(command) 
```

可从command中获得内容

"$变量"或${变量}为变量扩增内容

unset取消变量

### env 观察环境变量

### set观察所有变量

### 语系变量 locale

### export

### read	[-p/t]  variable

从command line 读取内容到变量

```
-p 接提时符号
-t 设定限制时间
```

### declare 变量声明

```

-a:	将后面名为variable的变量定义成为数组( array)类型
-i:	将后面名为 variable的变量定义成为整数数字(integer)类型
-x:	用法与 export一样，就是将后面的variable变成环境变量;
-r:	将变量设定成为readonly类型，该变量不可被更改内容，也不能unset
```

### ulimit 配置用户系统资源

```
[ dmt sai@s tudy ~]$ ulimit [ -SHacdf1tu][配额选项与参数]:
-H: hard limi t ，严格的设定，必定不能超过这个设定的数值;
-s : soft limit ，警告的设定，可以超过这个设定值，但是若超过则有警告讯息。
	在设定上，通常soft会比 hard 小，举例来说，soft可设定为80 而 hard设定为100，那	么你可以使用到90(因为没有超过100)，但介于80~100之间时，系统会有警告讯息通知你!
-a:	后面不接任何选项与参数，可列出所有的限制额度;
-c:	当某些程序发生错误时，系统可能会将该程序在内存中的信息写成文件(除错用)，这种文件就被称为核心文件(core file)。此为限制每个核心文件的最大容量。-f:此 shell可以建立的最大文件容量(一般可能设定为2GB)单位为 Kbytes-d :程序可使用的最大断裂内存(segment)容量;
-l:	可用于锁定( lock)的内存量
-t:	可使用的最大CPU时间（单位为秒)
-u:	单一用户可以使用的最大程序(process)数量。
```

### 变量删除与内容替换

![image-20210313195416067](G:\linux_review\image-20210313195416067.png)

## 简单shell

#### 数据流重导向

```
<	导入
<<	停止导入
>	覆盖导出
>>	叠加导出
```

指令回传值

![image-20210314001652894](G:\linux_review\image-20210314001652894.png)

&& cmd1&&cmd2 cmd1执行完毕且正确才执行cmd2

||  	cmd1||cmd2 	cmd1执行完毕且错误才执行cmd2，若正确，cmd2不执行

![image-20210314002023716](G:\linux_review\image-20210314002023716.png)

注意：无论执行结果正确或错误 若不进行重定向，显示屏均会有

#### pipe 管道

注意：

管线命令仅会处理standard output，对于standard error output会予以忽略
管线命令必须要能够接受来自前一个指令的数据成为standard input 继续处理才行。

##### cut grep

![image-20210314124156406](G:\linux_review\image-20210314124156406.png)

grep [-acinv]  'matchstring' filename

```
-a:	将binary文件以text文件的方式搜寻数据:
-c:	计算找到'搜寻字符串′的次数
-i:	忽略大小写的不同，所以大小写视为相同
-n:	顺便输出行号
-v:	反向选择，亦即显示出没有'搜寻字符串′内容的那一行!
--color=auto :可以将找到的关键词部分加上颜色的显示喔!
```

##### 排序指令sort wc uniq

![image-20210314125447596](G:\linux_review\image-20210314125447596.png)

![image-20210314130014915](G:\linux_review\image-20210314130014915.png)

```
wc [-lwm]
-l 仅列出行
-w 仅列出多少字
-m 多少字符
```

![image-20210314130234404](G:\linux_review\image-20210314130234404.png)

只输入wc 显示行数、字数、字符数 和-lwm三个参数对应

##### 字符转换命令

tr 删除或替换

col 特殊字符处理

join 相同数据合并

paste 同一行粘贴 以tab隔离

expand tab转空格

##### split 分区命令

```
split [-bl] filename DONENAME
-b 接分区大小
-l 按行数分区
 split  -b 1b ~/test do
```

