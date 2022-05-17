# Kubernetes
kubernetes是目前云原生技术栈的核心技术，它是由Google将自己10余年的容器编排系统brog通过go语言实现并开源出来的。云原生技术栈就是以kubernetes为核心来组织的。
## kubernetes架构
kubernetes集群的工作节点（服务器）主要分为两种角色类型，分为master节点与node节点，master节点主要的工作是维护整个集群的状态、各节点之间的管理，node节点也就是工作节点主要是管理运行应用容器的。在master节点上主要运行的组件包括（kube-apiserver、kube-scheduler、kube-controller-manager），node节点运行的组件包括（kubelet、kube-proxy），额外还需要一个etcd集群，etcd也可以安装在master节点上。
![kubernetes架构图](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2Njk4ODEzOTgsMTAwNDk1OTgzNCwtMT
UxODM5ODkwMiwtODM1NTAxNDQyLDk4NjE3NjI3M119
-->