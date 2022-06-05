# 安装Ubuntu 18.04 server
ubuntu 是Linux开源发行版中，支持容器技术最优雅的。因此选择ubuntu作为底层系统。
### 1.选择镜像源
使用的是ubuntu-18.04 live server镜像源

![](file:////private/var/folders/w_/lyyvzm1s4m3fgfchv0rdc0580000gn/T/com.kingsoft.wpsoffice.mac/wps-chunchunmaomao/ksohtml/wpsmXWxUf.jpg)

### 2.配置虚拟机的硬件环境

硬件环境：2c/4G/40G

网络：配置Nat虚拟网卡

### 3.选择语言

### 4.键盘布局

### 5.配置网络信息

配置网络可以默认使用DHCP，这样虚拟机会安装时会请求dhcp服务器自动下发IP地址等网络信息。这里安装的是服务器因此采用静态配置IP地址的方式;

### 6.配置镜像源

默认使用的是ubuntu官方镜像源地址，考虑国内的网络环境这里配置使用阿里云镜像源；

### 7.自定义硬盘分区

默认安装会将整个磁盘挂载到根分区上，我们在安装的时候最好是根据不同类型的服务器自定义最佳的分区方案；

### 8.选择安装ssh  server

需要远程链接就必须安装

### 9.创建用户信息

### 10.选择预原装环境

<![if !supportLists]>10.<![endif]>等待安装

![](file:////private/var/folders/w_/lyyvzm1s4m3fgfchv0rdc0580000gn/T/com.kingsoft.wpsoffice.mac/wps-chunchunmaomao/ksohtml/wpsWmtnZy.jpg)

<![if !supportLists]>11.<![endif]>修改root用户密码

Sudo passwd root

ubuntu为了安全，默认创建root并默认密码，因此需要需要root密码

![](file:////private/var/folders/w_/lyyvzm1s4m3fgfchv0rdc0580000gn/T/com.kingsoft.wpsoffice.mac/wps-chunchunmaomao/ksohtml/wps0PQ3nQ.jpg)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY3NDM3MzM0NiwtMTc5MDk3MjE2MiwyMD
I0MDgxMTU5LDE1MDAyNzAxMzEsMTAyMzI5OTU2OCwtMTY3OTY3
OTI4MV19
-->