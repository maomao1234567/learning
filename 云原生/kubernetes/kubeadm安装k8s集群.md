# Kubeadm
>Kubeadm 是一个用来快速创建K8s集群的工具包，它屏蔽了kubernetes各个组件之间的复杂性。能够让才学习kubernetes的用户能够一键部署一个kubernetes集群，它通过将kubernetes中的各个组件本身也作为一个个容器运行起来。虽然kubeadm降低了部署k8s的难度，但是正是它屏蔽掉了复杂性也就失去很多的灵活性所以在生产环境尽量还是使用二进制包来部署这样便于后期的排错管理。
## 1.kubeadm部署单master节点的K8s集群
###  1.1 资源配置清单
|角色|IP|硬件资源|
|:---:|:---:|:---:|
|master|172.16.90.100|2c/8G/40G|
|etcd|172.16.90.100|2c/8G/40G|
|node1|172.16.90.101|2c/4G/50G|
|node2|172.16.90.102|2c/4G/50G|

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxNjMyMjkzOSwtMjk3Nzc1NTgxLC0xMD
cwNTc3OTYyLDEzNTA5OTk4NDddfQ==
-->