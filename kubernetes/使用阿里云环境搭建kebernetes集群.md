### 如何快速搭建kubernetes 集群在阿里云上
----
#### 资源准备 (vpc, nat, elp, ecs)
1. 准备一个vpc网络环境，部署的kubernetes集群在一个隔离的vpc网络环境中。vpc 创建需要根据实际需求选择一个合适的私有网段，我这里选择的是172.16.0.0/16 这个网段。在一个可用区里创建一个交换机，最好在一个vpc中创建两个及以上的虚拟交换机在不同的可用区中。
2. 创建一个NAT网关，nat网关主要的作用就是vpc的网络流量的出口与入口。通过设置SNAT（vpc 访问公网的规则）以及DNAT（公网访问vpc的规则）。
3. 创建一个ELP弹性公网IP，并且绑定在NAT网关上。
4.  创建ECS实例，我这里创建了3个ECS实例。一个作为master节点两个作为worker节点。
####  部署kubernetes 集群
开始部署前需要在ECS上安装相应的软件包，我这里的节点使用的是Centos7.5作为宿主机的操作系统。因此使用yum安装相应的软件包，详细步骤如下：
1.  首先配置yum的docker源以及kubernetes源，因为国内的网络环境的原因，因此我选择的是阿里云的yum源配置。
2. 先选择一个节点当作master节点，并且安装好docker-ce, kubelet, kubeadm,  kubectl. 这里解释下这几个软件，docker-ce就是容器环境，kubernetes支持的容器还有containerd等，kubelet是工作在每个节点上的与master上的apiServer通信的组件，主要作用就是接收新的或修改的Pod规范，并且使pod在期望的配置下运行尽可能达到期望的状态。kubectl则是外部环境与kubernets集群通信的组件，kubernetes de
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE2MzQwNTA5LDE1MTEwNjM2NDAsMjQ2Mz
I4NDI3XX0=
-->