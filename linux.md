## linux 

https://www.linux.org/pages/download/

linux版本分为两种

内核版本  

发行版本

## 虚拟机Vmware、linux安装  

https://blog.csdn.net/qq_44714603/article/details/88829423

## linux的常用命

Linux命令大全.chm 

[liunx大全](docs/Linux命令大全.chm )

```
ls：目录下文件
ls -a: 目录下中包含隐藏文件
ls -l :目录下详细文件相当于ll

cd ~:到root目录
cd -:返回上一层目录

mkdir 目录名：创建目录
rmdir 目录名： 删除空目录
mkdir -p aa/bb :创建两级或多级目录

#浏览文件
cat 文件名：查询所有文件内容
more 文件名：一屏幕显示 
less 文件名：滚动查看

tail -10 文件名：查看最后10行
tail -f 文件名：动态查看内容

文件操作
cp 复制
mv 剪贴
rm 删除 ：rm -r :询问是否删除，rm -rf:不询问删除

tar 打包和解压
tar -cvf 文件打包
tar -zcvf 打包并压缩
tar -xvf 压缩
tar -zcvf 加压tar.gz

查找
find 查找文件
find / -name "tomcat*" 查找文件名为tomcat开头的
find /-name "tomcat*" -ls 
find /-perm -777 -type d -ls 查找权限是777的文件

grep查找文件中的字符串
grep lang 文件名：查找文件中带有lang字符串
grep lang 文件名 -color ：查找文件中带有lang字符串 高亮显示

pwd
touch :创建一个空文件 touch a.txt
clear 清屏

ps -ef 查看所有进程
ps -ef |grep tomcat 查看某一个进程
kill -9 强制杀死进程
```

## 文件权限命令

![](E:\gitbook\book\img\liunx01.png)

chmod 777 文件名：最高权限

## 常用的上网操作

### 1.主机名配置

/etc/sysconfig/network

文件增加hostname 名字

### 2.IP地址配置

/etc/sysconfig/network-scripts/ifcfg-eth0 文件

以下是ip配置文件默认的配置：
IPV6 INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_PEERDNS=yes
IPV6_PEERROUTES=yes
IPV6_FAILURE_FATAL=no
NAME=eno16777735
UUID=6128ac6c-b173-434f-8f8f-9ba1ea96c4bb
DEVICE=eno16777735
ONBOOT=no
要永久修改ip地址，需设置以下参数：
ONBOOT=yes #系统启动时是否激活此设备
IPADDR=192.168.0.1 #ip地址
BOOTPROTO=static #ip地址的分配方式（static表示静态ip地址，dhcp表示自动分配ip地址）
NETMASK=255.255.255.0 #子网掩码
GATEWAY=192.168.0.2 #默认网关
DNS1=192.168.12.15 #DNS域名解析服务器
DNS2=125.168.12.5


设置DNS配置文件路径：
/etc/resolv.conf文件中。
以下是DNS文件的配置
nameserver 8.8.8.8 #google域名服务器


设置好配置文件保存好后，需要重启网卡才会生效（或者重启服务器）
service newwork restart #重启网络服务
或者
systemctl restart network

也可以单个网卡重启
ifdown eth0
ifup eth0

重启好网卡后，查看ip地址。centos查看ip地址的指令：
ip addr

配置完ip地址后，还需检查配置好的ip地址是否生效。
比较常用的方法就是先ping一下ip地址（注：如果ping不通，也不能表示ip配置错了，也可能是被防火墙拦截）
centos关闭防火墙的方法：
查看防火墙状态：systemctl statuc firewalld.service
关闭防火墙：systemctl stop firewalld
启动防火墙：systemctl start firewalld
开机自动关闭：systemctl disable firewalld
开启自动启动：systemctl enable firewalld
查看开启是否启动：chkconfig --list|grep network
ip地址能ping通后，还需ping一下域名服务器，检查DNS是否生效，因为一般网络协议都是通过域名来映射ip地址，这样便于上网。
国内一般都是ping www.baidu.com(百度地址)，如果也能ping得通，说明现在可以正常上网了。

### 域名映射

vi /etc/hosts在最后加上ip及映射的域名

192.168.229.111 node001

192.168.229.112 node002

192.168.229.113 node003

### 网络服务管理

```
service network status 查看指定服务状态
service network stop/start/restart ：

service --status -all 查看系统所有后台服务
netstat -nltp: 查看系统中网络进程端口监控情况

```

```
防火墙设置
# 查看防火墙状态
service iptables status  
# 停止防火墙
service iptables stop 
# 启动防火墙
service iptables start 
# 重启防火墙
service iptables restart  
# 永久关闭防火墙
chkconfig iptables off 
# 永久关闭后重启
chkconfig iptables on　　

2、开启80端口
vim /etc/sysconfig/iptables
# 加入如下代码
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
保存退出后重启防火墙
```



