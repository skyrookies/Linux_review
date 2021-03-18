# nginx反向代理本地实验

## 网络环境

win10（192.168.168.1） 桥接模式与contos8（192.168.168.128）相连

centos8作为服务器划分子网给centos7（10.10.10.88）分配网段（虚拟网卡实现）

## nginx环境 

Cenos8 nginx1.14.1

## 服务器环境

win10(64) apache2.4.41 php.ini文件

## 客户机环境

Centos7  正常情况下，win10打卡apache可布置php初试页面且客户机正常访问

![image-20210318220209267](G:\linux_review\image-20210318220209267.png)

## 实验目的

为win10配置反向代理，为centow7虚拟机提供服务，同时尝试负载均衡配置在一台服务器上

配置思路：nginx.config文件配置

```
server{
//一些全局配置，常规配置忽略
upstream name_as_you_like{
	server 192,168,168,1:80	weight=1;
	}
location	/	{
	root html//默认在上一级配置 尝试
	proxy_pass http://name_as_you_like
}
}
```

## 实验结果 成功

![image-20210318222654358](G:\linux_review\image-20210318222654358.png)

注意：此时客户机访问的是nginx主机的地址 192.168.168.128 

##  实验使用命令与总结

```
nginx -s reload
在nginx 执行文件目录下 执行文件选用-s reload参数 表示重新加载配置文件
执行文件目录/sbin/nginx
关于配置文件中host选项，若按照默认配置在location之外，无法实现，按照参考资料配置在location之内成功配置
```

### nginx.config配置文件一些实录

```
 upstream name_as_you_like{
                server 192.168.168.1:80 weight=1;
        }
        //upstream关键字，配置负载均衡，server地址之后，weight表示多服务器轮询权重
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
        root         /usr/share/nginx/html;
        proxy_pass http://name_as_you_like;
        //proxy_pass 配置反向代理,协议名加upstream选项名
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }

```

## 未配置反向代理时展示

该默认网站为早古时期百度直接拔的，见谅

![image-20210318223631819](G:\linux_review\image-20210318223631819.png)