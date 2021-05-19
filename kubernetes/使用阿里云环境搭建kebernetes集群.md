### 如何快速搭建kubernetes 集群在阿里云上
----
#### 资源准备 (vpc, nat, elp, ecs)
1. 准备一个vpc网络环境，部署的kubernetes集群在一个隔离的vpc网络环境中。vpc 创建需要根据实际需求选择一个合适的私有网段，我这里选择的是172.16.0.0/16 这个网段。在一个可用区里创建一个交换机，最好在一个vpc中创建两个及以上的虚拟交换机在不同的可用区中。
2. 创建一个NAT网关，nat网关主要的作用就是根据
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ0NzIxNjY1NF19
-->