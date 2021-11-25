# PXE
  PXE(preboot execute environment)是由Intel公司开发的最新技术,工作于Client/Server的网络模式，支持工作站通过网络从远端服务器下载映像，并由此支持来自网络的操作系统的启动过程，其启动过程中，终端要求服务器分配IP地址，再用TFTP（trivial file transfer protocol）或MTFTP(multicast trivial file transfer protocol)协议下载一个启动软件包到本机内存中并执行，由这个启动软件包完成终端基本软件设置，从而引导预先安装在服务器中的终端操作系统。
  简单的来说pxe就是通过网络自动化安装系统的一套方案。首先带有pxe支持的网卡的主机，需要在局域网提供一个DHCP服务器或者一个中继代理的能够转发广播到DHCP服务器。DHCP服务器主要是提供ip地址给待安装

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwMzI4ODM3NF19
-->