# flask
flask作为一个轻量级的python web框架，很值得拜读一下。flask是基于werkzeug作为web server，JInjia2作为模版引擎来实现的。
### werkzeug
首先简单的介绍下werkzeug，它封装了HTTP协议提供了一个具有完整功能的web server，提供的功能包括请求数据封装（Request), 响应数据封装（Response), 路由的生成以及解析（Map, Rule, MapAdapter), 以及一些常见的Middleware。
### flask 启动流程
首先python web 框架都需要遵循wsgi协议，所有的python web 框架都需要根据wsgi提供的接口来实现。简单的来说就是每个python web应用都是一个可调用的接口（callable), 在flask中，这个对象就是app = Flask(__name__)实例化的对象。因为在Flask类中实现了def __call__(environ, start_response)方法，所以由Flask实例化出的对象就是一个可调用的对象。flask应用启动的流程是这样的，首先flask实现了一个run()方法，在run()方法里调用werkzeug .serving.run_simple(host, port, app)启动一个web server并将app绑定在这个web server上。通过下图的HTTP请求处理返回的全过程，可以得到当一个请求发出后首先是web server收到这个HTTP请求，然后web server根据之前绑定的application，调用application.因此这里解释了什么所有的web 应用都需要实现一个__call__(environ, start_response)的原因。web server就是通过调用这个方法来处理请求。在flask中的__call__ 方法中通过调用wsgi_app()来实现，这里开始很困惑为什么要这样实现，查了很多资料后明白了，flask这里的实现主要是方便使用MIddleware中间件来扩展flask应用可以通过
app.wsgi_app = MyMiddleware()来指定自己的实现的中间件。在flask中实现的wsgi_app()主要完成的任务就是，首先根据请求对象中的MapAdapter将路由解析到具体的endpoint以及请求参数，然后根据view_functions，找到对应endpoint的处理函数来处理这次请求, 最后根据返回的结果生成生成Response对象，最后返回Response对象，完成这次请求。

![](https://assets.toptal.io/uploads/blog/image/91961/toptal-blog-image-1452784558794-7851992813e17ce0d5ca9802cf7ac719.jpg)
### flask 上下文管理
在flask中的上下文包括，请求上下文、app上下文。这些上下文主要的目的是完成将应用需要的数据封装在一个个对象里方便使用。flask采用全局变量的方式来管理这些上下文 ，但是这样的方式会造成在多进程的情况下数据会发生混乱。因此flask使用栈结构来存放这些数据。
<!--stackedit_data:
eyJoaXN0b3J5IjpbODY4Njc3NjMsMTExMTU2MDYzOCw4MzMzNz
Y0MiwtMjA0Nzc5NjI0MSwxODcyOTY3OTUsLTQ3Mzg0NzYyNCwt
MTU5OTY0MjY4Myw0MjA5MzE4NzIsLTE4OTA5MzkyODYsLTg4MT
cwMzExMiwtMTA3Mjc4NjEwNSwxNzQwMDc2NDU3LC0xNTA0NzY3
NjE2XX0=
-->