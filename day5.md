# DAY5

## 第六章 续

### 文件与目录管理

ls命令参数补充

```
-d 仅输出目录本身
-F 根据文件、目录等信息给与附加数据结构：*代表可执行文件,/代表目录,=代表socket文件,|代表FIFO文件
-h 文件容量用GB MB 表示
-t 以时间排序
```

复制、删除与移动

```
cp,rm,mv
cp -a 复制所有
cp -d 若源文件为链接文件，则复制链接文件属性而非文件本身
cp -f 强制执行
cp -i 增加询问，例如在目标文件已存在时
cp -p 连同文件属性（权限、用户、时间）一同复制，而非使用默认属性（备份常用）
cp -r 递归
cp -s 复制为软链接文件

rm 
rm -i 互动模式
rm -f force
rm -r 递归

mv [-fiu] source destination 
mv -u (update)
```

取得路径文件名与目录名称

```
olknow76@kali:~$ basename /etc/sysconfig/network
network
olknow76@kali:~$ dirname /etc/sysconfig/network
/etc/sysconfig
```

![image-20210309192100879](G:\linux_review\image-20210309192100879.png)

### 文件内容查询

```
cat由第一行开始显示文件内容
tac从最后一行开始显示，可以看出tac 是cat的倒着写
nl 显示的时候，顺道输出行号
more 一页一页的显示文件内容
less 与 more类似，但是比 more更好的是，他可以往前翻页
head 只看头几行
tail 只看尾巴几行
od 二进制方式读取文件
```

cat参数

```
选项与参数:
-A:相当于-vET的整合选项，可列出一些特殊字符而不是空白而已;
-b:列出行号，仅针对非空白行做行号显示，空白行不标行号!
-E:将结尾的断行字符$显示出来;
-n：打印出行号，连同空白行也会有行号，与-b 的选项不同;
-T:将[ t ab]按键以^I显示出来;
-v:列出一些看不出来的特殊字符
```

nl 添加行号打印 参数

```
-b:指定行号指定的方式，主要有两种:
	-b a :表示不论是否为空行，也同样列出行号(类似 cat -n);
	-b t :如果有空行，空的那一行不要列出行号(默认值);
-n :列出行号表示的方法，主要有三种:
	-n ln :行号在屏幕的最左方显示;
	-n rn :行号在自己字段的最右方显示，且不加0 ;
	-n rz :行号在自己字段的最右方显示，且加0 ;
-w:行号字段的占用的字符数。
```

more按键

```
空格键( space):代表向下翻一页;
Enter:		代表向下翻『一行;
/字符串:	代表在这个显示的内容当中，向下搜寻「字符串」这个关键词;
: f:	立刻显示出文件名以及目前显示的行数;
q:		代表立刻离开more ，不再显示该文件内容。
b或[ctrl]-b :	代表往回翻页，不过这动作只对文件有用，对管线无用。
```

less按键

```
空格键:	向下翻动页;
[ pagedown]:	向下翻动一页;
[pageup] :	向上翻动一页;
/字符串:	向下搜寻「字符串』的功能;
?字符串:	向上搜寻『字符串』的功能;
n	:重复前一个搜寻(与/或﹖有关!)
N	:反向的重复前一个搜寻(与/或﹖有关! )
g	:前进到这个资料的第一行去;
G	:前进到这个数据的最后一行去（注意大小写);
q	:离开less这个程序;
```

head 取出前面几行

```
head [-n number] file	若number为负数 则显示该数字(负数即倒数的几行)之前的所有行
```

![image-20210309215501867](G:\linux_review\image-20210309215501867.png)

tail 取出后面几行

```
tail [-n number] file
tail =f 持续侦测后面所接的文档名，^c才会停止，常用于log文件，一直更新的文件
```

### 对非文本文档的读取 	od

```
od [-t TYPE] file
```

![image-20210309220117900](G:\linux_review\image-20210309220117900.png)

touch 修改文件时间或新建文件

Linux下时间参数

- mtime (modification time)
- ctime (status time)
- atime (access time) 

![image-20210309220352877](G:\linux_review\image-20210309220352877.png)

```
touch [-acdmt] file
-a 仅修改atime
-c 仅修改文件的时间，若不存在创建新文件
略
```

### 文件与目录的默认权限与隐藏权限

umask 

umask显示的数字为被取走的权限

![image-20210309223137763](G:\linux_review\image-20210309223137763.png)

```
umask [-S] number 
```

![image-20210309223303540](G:\linux_review\image-20210309223303540.png)

配置 chattr	利用chattr配置文件案隐藏权限

![image-20210309223548566](G:\linux_review\image-20210309223548566.png)

查看 lasttr

![image-20210309223559761](G:\linux_review\image-20210309223559761.png)

### 文件特殊权限 SUID 	SGID	SBIT

Set UID suid 

```
sUID权限仅对二进制程序(binary program)有效;
执行者对于该程序需要具有x的可执行权限;
本权限仅在执行该程序的过程中有效(run-time);
执行者将具有该程序拥有者(owner)的权限。
```

类似于私有属性只能由类定义的方法调用，SUID的文件只能由特定命令进入。比如/etc/shadow 记录账户和密码 用户只能通过passwd 命令修改自己的密码

Set GID SGID 同理

但即可用于程序

```
程序执行者对于该程序来说，需具备x 的权限;
执行者在执行的过程中将会获得该程序群组的支持!
```

能够用具备sgid权限的程序读取不具备正常 读取权限的文件

也可用于目录：

```
用户若对于此目录具有r与x的权限时，该用户能够进入此目录;
用户在此目录下的有效群组(effective group)将会变成该目录的群组;
用途:若用户在此目录下具有 w 的权限(可以新建文件)，则使用者所建立的新文件，该新文件的群组与此目录的群组相同。
```

Sticky Bit SBIT 只针对目录有效

```
当用户对于此目录具有w,x权限，亦即具有写入的权限时;
当用户在该目录下建立文件或目录时，仅有自己与 root才有权力删除该文件
```

chmod 修改权限第一个数字

```
4为SUID
2为SGID
1为SBIT
```

### file 查看文件类型

### 脚本文件搜索

#### which		查找${PATH}范围内目录

```
which [-a] command
```

![image-20210312192146337](G:\linux_review\image-20210312192146337.png)

对于bash内建指令 可透过type查找

### 文档搜索

#### whereis	只查找特定目录 速度较快

```
-l:	可以列出whereis会去查询的几个主要目录而已
-b:	只找binary格式的文件
-m:	只找在说明文件manual路径下的文件
-s:	只找source来源文件
-u:	搜寻不在上述三个项目当中的其他特殊文件
```

![image-20210312192431354](G:\linux_review\image-20210312192431354.png)
#### locate/updatedb 查找数据库中的文件名/部分名称

速度较快，可用updatedb手动更新

```
-i:	忽略大小写的差异;
-c:	不输出档名，仅计算找到的文件数量
-l:	仅输出儿行的意思，例如输出五行则是- l 5
-S:	输出 locate所使用的数据库文件的相关信息，包括该数据库纪录的文件/目录数量等
- r:后面可接正规表示法的显示方式
```

updatedb：根据 /etc/updatedb.conf 的设定去搜寻系统硬盘内的文件名，并更新 /var/lib/mlocate 内的数据库 文件； 

 locate：依据 /var/lib/mlocate 内的数据库记载，找出用户输入的关键词文件名。

#### find  [PATH] [option] [action]

1. 与时间相关参数
2. 与使用者或者组名相关参数
3. 与文件权限及名称相关
4. 可额外进行的动作