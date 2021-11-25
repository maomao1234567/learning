# kong
kong是在nginx上封装的一个API网关组件，在微服务的架构中可以使用kong作为各个服务的访问入口, 也就是网关入口。在我自己的理解中kong可以用作微服务中的服务注册与发现的功能。kong还通过第三方插件的形式提供比如权限认证，跨域处理等功能。

## 实践过程
### services
services 是kong反向代理的上游服务，kong通过路由匹配到对应的上游服务。service真正提供url处理的对象。
### routes
routes 是在service注册到kong是提供的匹配规则，kong就根据这些路由规则匹配到对应的service上。
### consumers
consumer 是消费kong的api的一些实体对象，在这里可以充当consumer的实体对象包括user，可以把客户端用户抽象成一个consumer。我们可以通过给consumer增加权限认证等一系列的操作。可以通过acl来控制consumer能访问的服务，进行对服务的保护。
### application


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NjA2NjYzMTgsLTk1MDQ4NTEwMCwtOT
UwNDg1MTAwLC05NTA0ODUxMDAsMTQ1MTQ1OTU5N119
-->