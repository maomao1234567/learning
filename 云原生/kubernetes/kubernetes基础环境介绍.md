# Kubernetes
kubernetes是目前云原生技术栈的核心技术，它是由Google将自己10余年的容器编排系统brog通过go语言实现并开源出来的。云原生技术栈就是以kubernetes为核心来组织的。
## kubernetes架构
kubernetes集群的工作节点（服务器）主要分为两种角色类型，分为master节点与node节点，master节点主要的工作是维护整个集群的状态、各节点之间的管理，node节点也就是工作节点主要是管理运行应用容器的。在master节点上主要运行的组件包括（kube-apiserver、kube-scheduler、kube-controller-manager），node节点运行的组件包括（kubelet、kube-proxy），额外还需要一个etcd集群，etcd也可以安装在master节点上。
![kubernetes架构图](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)
上面的kubernetes的架构表示的是一个单master节点三个node节点的集群，集群之间的交互都是通过master上的api-server组件进行交互。
所有的组件都不会直接操作etcd。
### kube-apiserver
kubernetes通过apiserver暴露所有的api接口，因此apiserver相当人的大脑用于接收、发送指令，一切对集群状态以及所有资源的增删改查的操作都需要通过apiserver然后apiserver在对操作完成认证、权限检查等准入控制后，再由apiserver将合法的操作写入到ectd中去。因此在生产环境中需要部署多个master节点的集群，将api-server变成一个高可用的集群，api-server在部署的时候会暴露两个端口一个是http的用于集群内部组件的交互，一个是https的用于集群外部客户端的交互比如kubectl
### kube-scheduler
kube-scheduler组件的主要功能是根据调度算法，将待运行Pod调度到一个最适合的node（节点）上去执行。它监听api-server上的创建Pod的事件，然后将待分配节点列表默认是选择一个资源占用较少的节点去部署。当然也可以自定义调度规则调度Pod到合适的节点运行，一般可以设置亲缘行于反亲缘来调度Pod。
### kube-controller-manager
kube-controller-manager组件的主要作用就是管理用户在k8s中创建所有资源，通过不同的控制器去管理不同的资源，控制器的主要目的将是
k8s集群中对应资源的状态保持在用户所定义的状态，比如ReplicaSet Controller的功能就是将让Pod的数量保持在用户定义副本数，如果Pod没达到配置的副本数controller请求apiserver创建对应的Pod再由scheduler调度到合适的节点运行。如果超过了配置的副本数controller会请求apiserver终止掉多的Pod。
### kubelet 
kubelet组件是在工作节点上安装的，它的功能主要是管理机器的资源，以及与容器运行时进行交互调用容器接口进行容器的创建管理。kubelet会定时想apiserver请求报告节点的资源占用情况节点状态，以及pod的状态等。
### kube-proxy
kube-proxy组件的功能是代理转发服务请求到真实pod上，在k8s里service是一个虚拟的IP地址，通过kube-proxy管理service到真实提供服务的entripoint去服务。kube-proxy通过userspace，iptables，ipvs三种模式去管理，目前userspace的模式已经被废弃。主要就是通过写入iptables的规则链去将请求转发到真正的pod，kube-proxy通过监听apiserver如果有service资源的变化以及endpoint的变化，kube-proxy就会调用相应的内核模块去更新network规则表。
### etcd
etcd是一个提供强一致行的分布式key-value的存储，它是基于raft协议实现的。主要是为k8s集群提供数据保存的，k8s集群的所有资源状态数据都有etcd管理，但是在整个k8s集群中只有apiserver直接与etcd通信。其他组件都是通过apiserver间接与etcd通信。

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwOTU2MDY4MjYsMzEzMjUxNDA2LDI2OD
MzMzAxNCw1NzkxNTEzNzMsLTM1NDU2NjM2NSwtNzg4NzY4NTcw
LC04MjEwOTgxOTMsLTI2Nzc5NDM4OSwtMTU3ODAzNzczNywyNz
ExNjU0ODQsNjAwMDM2MzcxLDEzMjc0MDMwMTgsLTE2Njk4ODEz
OTgsMTAwNDk1OTgzNCwtMTUxODM5ODkwMiwtODM1NTAxNDQyLD
k4NjE3NjI3M119
-->