# flask
flask作为一个轻量级的python web框架，很值得拜读一下。flask是基于werkzeug作为web server，JInjia2作为模版引擎来实现的。
## werkzeug
首先简单的介绍下werkzeug，它封装了HTTP协议提供了一个具有完整功能的web server，提供的功能包括请求数据封装（Request), 响应数据封装（Response), 路由的生成以及解析（Map, Rule, MapAdapter), 以及一些常见的Middleware。
## flask 启动流程
首先python web 框架都需要遵循wsgi协议，所有的python web 框架都需要根据wsgi提供的接口来实现。简单的来说就是每个python web应用都是一个可调用的接口（callable), 在flask中，这个对象就是app = Flask(__name__)实例化的对象。因为在Flask类中实现了def __call__(envi
![](https://assets.toptal.io/uploads/blog/image/91961/toptal-blog-image-1452784558794-7851992813e17ce0d5ca9802cf7ac719.jpg)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzU2NjQwNTAzLC0xMDcyNzg2MTA1LDE3ND
AwNzY0NTcsLTE1MDQ3Njc2MTZdfQ==
-->