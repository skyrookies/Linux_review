# day9

## 文件格式化处理

### sed工具 sed [-nefr] [action]

```
sed [-nefr] [action]
-n silent模式，仅显示经过sed处理的行或动作
-e 直接在命令行上进行动作编辑
-f 直接将sed 动作写在文件内 -f filename 执行filename内的sed动作
-r 支持正则表达式
-i 直接修改读取的文件内容，不由屏幕输出

action
a	新增，后接字符串
c	取代
d	delete 删除
i	insert 插入
p	print 打印
s	取代，可搭配正则
```

### s script 

```
[address]s/pattern/replacement/flags
address 表示指定要操作的具体行，pattern 指的是需要替换的内容，replacement 指的是要替换的新内容，flags为标记为，有
n	1~512 之间的数字，表示指定要替换的字符串出现第几次时才进行替换，例如，一行中有 3 个 A，但用户只想替换第二个 A，这是就用到这个标记；
g	对数据中所有匹配到的内容进行替换，如果没有 g，则只会在第一次匹配成功时做替换操作。例如，一行数据中有 3 个 A，则只会替换第一个 A；
p	会打印与替换命令中指定的模式匹配的行。此标记通常与 -n 选项一起使用。
w file	将缓冲区中的内容写到指定的 file 文件中；
&	用正则表达式匹配的内容进行替换；
\n	匹配第 n 个子串，该子串之前在 pattern 中用 \(\) 指定。
\	转义（转义替换部分包含：&、\ 等）。
```

### d script

```
[address]d
sed '3,$d' data6.txt 
$代表文件结尾字符
```

### a / i script

```
[address]a（或 i）\新文本内容
i在前面插入
a在后面添加
```

### c  script

```
[address]c\用于替换的新文本
c 命令表示将指定行中的所有内容，替换成该选项后面的字符串。该命令的基本格式为：
```

### y script

```
y 转换命令是唯一可以处理单个字符的 sed 脚本命令
[address]y/inchars/outchars/
转换命令会对 inchars 和 outchars 值进行一对一的映射，即 inchars 中的第一个字符会被转换为 outchars 中的第一个字符，第二个字符会被转换成 outchars 中的第二个字符...这个映射过程会一直持续到处理完指定字符。如果 inchars 和 outchars 的长度不同，则 sed 会产生一条错误消息。
```

### p script

```
p 命令表示搜索符号条件的行，并输出该行的内容，此命令的基本格式为：
[address]p
p 命令常见的用法是打印包含匹配文本模式的行
```

### w script

```
[address]w filename
w 命令用来将文本中指定行的内容写入文件中
```

### sed 脚本命令的寻址方式

两种方式都可以用如下两种格式

```
[address]脚本命令
或者
address {
    多个脚本命令
}
```



#### 以数字形式指定行区间

指定的地址可以是单个行号，或是用起始行号、逗号以及结尾行号指定的一定区间范围内的行

#### 以文本模式匹配指定具体行区间

```
/pattern/action
注意，必须用正斜线将要指定的 pattern 封起来，sed 会将该命令作用到包含指定文本模式的行上。
pattern支持正则
```

### awk基础  

#### awk基础语法

```
awk [options] 'BEGIN{ action;… } pattern{ action;… }pattern{ action;… } END{ action;… }' file
awk [ -F 分隔符] [ -v 变量名=值 ] 'BEGING{语句} 条件类型1{动作1} 条件类型2{动作2}... END{语句}' 输入的文件
  命令格式说明:
  （1）awk命令格式由四部分组成。选项、BEGIN、END和带条件类型和动作的语句。这四个部分都是可选项，可省略任意部分。
  （2）-F表示设置列分隔符，默认为空格。设置的分隔符需用双引号标注。
  （3）-v 表示初始化一个变量或者用于向awk命令传入外部变量值，shell编程中常用。
  （4）条件类型可以是正则表达式、条件语句、复合语句以及行匹配范围等内容。条件类型为可选设置。如果设置条件，只处理匹配条件的行执行动作。如果未设置，awk命令则认为所有行都是匹配的，并执行动作语句。动作表示执行的命令，命令必须放在大括号{}内。
常见命令如：print
  （5）必须了解这些符号。$0表示行，$1、$2、$3...$n分别表示第1列、第2列、第3列...第n列。awk命令经常会使用这些符号去做匹配、打印指定指定列等操作。

```

#### awk 工作原理

```
（1）：执行[option]相关内容，也就是-f，-F，-v选项内容。
（2）：执行BEGIN{action;… } 语句块中的语句。BEGIN 语句块在awk开始从输入流中读取行之前被执行，这是一个可选的语句块，比如变量初始化、打印输出表格的表头等语句通常可以写在BEGIN 语句块中。
（3）：从文件或标准输入(stdin) 读取每一行，然后执行pattern{action;… }语句块，它逐行扫描文件，从第一行到最后一行重复这个过程，直到文件全部被读取完毕。pattern语句块中的通用命令是最重要的部分，也是可选的。如果没有提供pattern 语句块，则默认执行{ print } ，即打印每一个读取到的行，awk 读取的每一行都会执行该语句块。
（4）：当读至输入流末尾时，也就是所有行都被读取完执行完后，再执行END{action;…} 语句块。END 语句块在awk从输入流中读取完所有的行之后即被执行，比如打印所有行的分析结果这类信息汇总都是在END 语句块中完成，它也是一个可选语句块。
```

#### awk内置变量

```
[1]$n 是当前行的按照指定域分隔符（默认是空格或[TAB]]键）分割后的第n个字段，比如n为1 表示第1个字段，n为2表示第2个字段
[2]$0 则是记录了执行过程中当前行的文本内容
[3]NF 每一行($0)拥有的字段总数
[4]NR 目前awk所处理的"第几行"数据
[5]FNR 表示当前所处理的文本内的"第几行"数据
[6]FS 目前的域分割符号，可以通过FS字段指定文本的域分割符
[7]OFS 输出字段的分割符（默认是一个空格）
[8]ORS 输出的记录分割符（默认是一个换行）
[9]ARGIND 命令行中处理的当前文件的位置（从1开始）
[10]ARGC 命令行参数的数目
[11]ARGV 命令行参数的数组
[12]RS：输入记录分隔符(输入换行符)， 指定输入时的换行符
```

### awk模式匹配

#### 正则表达式匹配

```
awk [options] 'BEGIN{ action;… } pattern{ action;… } END{ action;… }' file
在[options]输入匹配正则表达式
```

```
  ~ cat /etc/passwd | awk '/^s/{print $0}'
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
systemd-network:x:100:102:systemd Network Management,,,:/run/
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
syslog:x:104:110::/home/syslog:/usr/sbin/nologin
sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
```

#### 匹配整行

默认情况下匹配整行

#### 匹配操作符 ~

```
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/usr/bin/zsh
➜  ~ cat /etc/passwd | awk -F ":" '$3~/1000/{print $0}'
```

对指定项匹配