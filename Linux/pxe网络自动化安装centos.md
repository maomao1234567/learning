# PXE
  PXE(preboot execute environment)是由Intel公司开发的最新技术,工作于Client/Server的网络模式，支持工作站通过网络从远端服务器下载映像，并由此支持来自网络的操作系统的启动过程，其启动过程中，终端要求服务器分配IP地址，再用TFTP（trivial file transfer protocol）或MTFTP(multicast trivial file transfer protocol)协议下载一个启动软件包到本机内存中并执行，由这个启动软件包完成终端基本软件设置，从而引导预先安装在服务器中的终端操作系统。
  简单的来说pxe就是通过网络自动化安装系统的一套方案。首先带有pxe支持的网卡的主机，需要在局域网提供一个DHCP服务器或者一个中继代理的能够转发广播到DHCP服务器。DHCP服务器主要是提供ip地址给待安装的机器，并且在分配ip地址的时候将安装引导文件，以及存放文件的tftp服务器ip返回。还需提供一个TFTP服务器以及http服务器，分别用来提供安装引导文件，linux内核文件，启动加载文件，http服务主要提供用来安装系统的应答文件，以及对应系统的软件包。
  
 ## 搭建dhcp服务器
   dhcp服务器使用来给本网段的机器自动分配ip的服务器，将本网段ip统一管理。它可以给每个分配的ip提供一个租期时间，提供续租的功能。它本身的ip地址最好是静态配置，它是不是只能管理它自己本网段的ip分配需要继续深究。
## 搭建tftp服务器
   tftp服务器它是一个简单的文件传输协议，在这里主要是用它来发放系统安装启动文件，linux内核文件，系统初始预启动的文件，以及启动安装菜单。
## 搭建httpd服务器
  安装运行httpd服务器都很容易，主要是制作应答文件，以及centos的镜像package放在http可以访问的路径下。应答文件主要是告诉机器如何初始化语言，分区，以及安装的pacakge和初始化的脚本。

## 总结
本身搭建这几个服务不是很难的事情，主要是需要对linux系统安装启动的过程需要有一个详细的了解。在了解基础上才知道如何制作应答文件需要放置生么样的文件到各自的服务器上。


<!--stackedit_data:
eyJoaXN0b3J5IjpbNTAwNDYyNjUsLTgzMzMyNzE5LDQ0Njc3Mz
g5OSwxMjY3MjQyNDUxLC01Njc5OTU2OSwyMDU3NzIxMjYsLTkw
MzI4ODM3NF19
-->