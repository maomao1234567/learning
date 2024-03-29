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
2. 先选择一个节点当作master节点，并且安装好docker-ce, kubelet, kubeadm,  kubectl. 这里解释下这几个软件，docker-ce就是容器环境，kubernetes支持的容器还有containerd等，kubelet是工作在每个节点上的与master上的apiServer通信的组件，主要作用就是接收新的或修改的Pod规范，并且使pod在期望的配置下运行尽可能达到期望的状态。kubectl则是外部环境与kubernets集群通信的组件，kubernetes通过apiServer向外提供基于restful的api接口管理kubernetes 的所有资源, kubectl 则是将这些api封装成一个工具。kubeadm则是一个快速创建部署kubernetes集群的工具，它很方便的将kubernetes集群中需要部署的组件通过部署成静态的Pod将这些基础组件本身套管在kubernetes集群中。这些基础组件包括（apiServer, controller-manager,  scheduler,  kube-proxy, coredns, etcd)
3. 安装好基础的软件后，本以为可以开开心心的一条命令就创建出kubernetes 集群了，我还是低估了国内的网络环境了。应为kubeadm 需要将apiServer的基础组件运行成集群的Pod，因此需要能下载这些组件的docker镜像，kubeadm默认使用的是Google镜像仓库，因此在国内不能直接访问到google镜像仓库。这里提供两种解决方式一是给docker设置代理，通过代理访问到google镜像仓库，另外一种方式就是将这些镜像通过能访问的镜像仓库下载到本地然后重新给这些镜像打tag命名成 google镜像仓库的命名。
4. 修改docker cgroup driver，因为kubelet 与 docker所使用的cgroup driver 不一致，因此需要修改docker 或者 kubelet的 cgroup driver我这里选择的是修改docker的cgroup driver, 修改kubelet是否对Swap支持，默认kubernetes对swap不支持，如果宿主机开启了swap kubelet默认启动会失败，因此需要禁用宿主机swap或者配置kubelet 支持swap.这些修改完了就启动docker 以及将docker 以及 kubelet 设置为开机启动。
5. 使用kuneadm init 初始化集群
6. 现在一个基本的kubernetes 集群已经部署完毕了，但是通过查看集群健康状态发现scheduler 以及 controller manager处于unhealthy 状态，这时需要注释掉/etc/kubernetes/manifests下的kube-controller-manager.yaml和kube-scheduler.yaml的- – port=0然后重启kubelet, 通过获取集群pods发现coredns一直处于pending状态。这是因为需要部署一个网络插件给集群的pods提供网络功能，常见的网络插件有flannel、calico等，选择一个合适网络插件部署在集群中。这样一个可用的kubenetes集群就搭建完毕，但是现在集群中只有一个master节点，接下来就需要将worker 节点加入到集群中。
7. 将worker节点加入到集群中，将之前拉去的docker镜像打包发给worker节点并且在worker节点上解包出所需的docker镜像。然后使用kubeadm join 加入到kubernetes 集群中。
#### 技术总结
 总的来说使用kubeadm部署kubernetes非常的方便让我感受到了一键部署kubernetes集群，对于一个新手来说屏蔽了各个组件之间的关系不需要一步一步的搭建，但是通过这样的方式搭建kubernetes只能停留在一个会用的基础层面如果想深了解整个kubernetes  的各个组件只能一步一步的搭建才能掌握各个组件之间的关系。在整个搭建的过程中需要特殊解决的就是国内网络环境不能访问google镜像仓库的问题，在这个过程中因为需要和重复在worker节点操作，我使用了一个运维管理工具ansible来操作。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUwMjc5MDcwMV19
-->