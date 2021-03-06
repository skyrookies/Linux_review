# daytwo

## 计算机概述 

略  耗时27m

- 常x86架构与arm架构略作区分 x86为CISC 复杂指令集的代表 arm为精简指令集RISC的代表

## 什么是linux

略 耗时30m

### 关于版本tips：

![image-20210306105827264](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306105827264.png)

主、次版本为奇数，发展中版本（development）

主、次版本为偶数，稳定版本（stable）

以上tips在3.0之后失效（啊这）

3.0之后分为EOL（end of live）与longterm（长期维护）

## 磁盘分区

### 常见设备

![image-20210306183130437](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306183130437.png)

![image-20210306184146907](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306184146907.png)

## 配置本机（实体机）到虚拟机ssh

耗时1h	大部分时间用来检查原来centos的虚拟机 发现iptables等命令全忘光了 囧

发现跨虚拟机截图切换等功能不好用，尝试用putty连接虚拟机方便截图等。悲剧的发现以前常用的两个centos因为之前的iptables、DHCP等实验搞了许多乱七八糟的转发，不太好用，故尝试利用kali虚拟机重新配置ssh

虚拟机版本workstation pro 15 kali

![image-20210306201038876](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306201038876.png)

1. 直接打开sshd配置文件

   ![image-20210306203636525](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306203636525.png)

2. 添加监听端口

   ![image-20210306203613927](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306203613927.png)

3. 启动（重启ssh服务）

   ![image-20210306203651207](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306203651207.png)

4. putty用非root账号登录

![image-20210306203737445](C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306203737445.png)

成功登录

注：若使用root账号，需在sshd_config配置文件中修改PermitRootLogin yes

未修改情况下不可使用root账号登录

<img src="C:\Users\Mechrevo\AppData\Roaming\Typora\typora-user-images\image-20210306204119232.png" alt="image-20210306204119232" style="zoom:50%;" />