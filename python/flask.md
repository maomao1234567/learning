# flask
flask作为一个轻量级的python web框架，很值得拜读一下。flask是基于werkzeug作为web server，JInjia2作为模版引擎来实现的。
## werkzeug
首先简单的介绍下werkzeug，它封装了HTTP协议提供了一个具有完整功能的web server，提供的功能包括请求数据封装（Request), 响应数据封装（Response), 路由的生成以及解析（Map, Rule, MapAdapter), 以及一些常见的Middleware。
## flask 启动流程
首先python web 框架都需要遵循wsgi协议，所有的python web 框架都需要根据wsgi提供的接口来实现。简单的来说就是每个python web应用都是一个可调用的接口（callable), 在flask中，这个对象就是app = Flask(__name__)实例化的对象。因为在Flask类中实现了def __call__(environ, start_response)方法，所以由Flask实例化出的对象就是一个可调用的对象。flask应用启动的流程是这样的，首先flask实现了一个run()方法，在run()方法里调用werkzeug .serving.run_simple(host, port, app)启动一个web server并将app绑定在这个web server上。通过下图的HTTP请求处理返回的全过程，可以得到当一个请求发出后首先是web server收到这个HTTP请求，然后web server根据之前绑定的application，调用application.因此这里解释了什么所有的web 应用都需要实现一个__call__(environ, start_response)的原因。web server就是通过调用这个方法来处理请求。

![](https://assets.toptal.io/uploads/blog/image/91961/toptal-blog-image-1452784558794-7851992813e17ce0d5ca9802cf7ac719.jpg)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg4MTcwMzExMiwtMTA3Mjc4NjEwNSwxNz
QwMDc2NDU3LC0xNTA0NzY3NjE2XX0=
-->