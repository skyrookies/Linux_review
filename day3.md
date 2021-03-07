# day3

## 第3章 安装centos7

略 	耗时20m

以前没看过这本书，但是也太基础了吧。。。 感觉要加快进度了

## 第4章 初入linux

tips：![image-20210307103215159](G:\linux_review\image-20210307103215159.png)

man 帮助

![image-20210307104743622](G:\linux_review\image-20210307104743622.png)

![image-20210307104752810](G:\linux_review\image-20210307104752810.png)

<img src="G:\linux_review\image-20210307105147453.png" alt="image-20210307105147453"  />

![image-20210307105227293](G:\linux_review\image-20210307105227293.png)

另一个帮助命令 info

```
info info
```

kali下暂不支持info，尝试失败

网络管理命令

```
netstat 
```

![image-20210307110323767](G:\linux_review\image-20210307110323767.png)

## 第5章 Linux文件权限和目录配置

简单复习 耗时1h

![image-20210307190700231](G:\linux_review\image-20210307190700231.png)

- d 目录
- -文件
- l link file
- b 接口设备
- c 串行端口设备
- [][]\[user]\[group]\[others]权限

权限相关常用命令

```
chgrp
chown
chmod	chmod u=rwx,g=rx,o=r filename
```

![image-20210307191522162](G:\linux_review\image-20210307191522162.png)

新东西 FHS Filesystem Hierarchy Standard 

![image-20210307192309578](G:\linux_review\image-20210307192309578.png)

常见目录

- /usr（unix software resourse） unix 操作系统软件资源
- /etc 配置文件
- /opt 第三方软件
- /boot 开机与核心
- /var（variable）/mail 邮件信箱
- /var/run 程序相关
- /lib 函式库/共享库
- /var 内容经常变化的目录 如缓冲文件、日志文件

### /user 的意义和内容

​	FHS基本定义：可分享但不可变动的数据

- /usr/bin/	一般用户使用的指令
- /usr/lib/ 基本同/lib
- /usr/local/   管理员自行安装软件建议目录
- /usr/sbin  非系统正常运作的系统指令

P236 

5555 今天并没有好好看书 明天继续 