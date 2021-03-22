### linux  boot 启动流程
1. 开机加电自检，目的是检查基本的硬件是否正常（cpu, 内存，硬盘）等，通过运行主板ROM中的程序来执行, 这个程序一般是设备在出厂时刻录进去的。
2. 选择一个启动设备（硬盘，光盘，usb等），通常是硬盘。
3. 运行bootloader 引导程序，例如grub，grub分为三个阶段，首先是通过读取硬盘的第一个分区中的MBR信息，找到boot分区，然后通过后面几个分区获取boot分区的文件系统内核程序获取boot中的linux 内核程序，最后加载linux内核，通过boot下的另外一个重要文件，加载根分区。
4. 运行第一个系统进程，并且启动其他开机服务。
###
  linux主要就是由kernel（内核）以及三方工具以及函数库构成。
###  systemd
centos7 开始采用systemd作为系统管理的工具，它集成很多的功能包括但是不限于
<!--stackedit_data:
eyJoaXN0b3J5IjpbODgyMzUyNzU0LC0yMzc2NjM1MjcsLTk4MD
Q5NTg4OSwxOTExMzIxNDgyLDczMDk5ODExNl19
-->