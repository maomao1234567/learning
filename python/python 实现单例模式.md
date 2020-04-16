## 单例模式
  单例是一种设计模式，属于创建型模式。意思是在某一个类只存在一个实例化对象。它的实现原理是，在实例化对象的时候检查是否存在该类的实例如果存在就直接返回这个实例如果不存在就先实例化一个改类的对象存在一个类变量中并且返回这个实例。在python中主要有四种实现单例模式的方法，分别是装饰器函数、装饰器类、__new__函数实现、元类实现。虽然有四种方式但是核心的实现还是一样的，前两种方式的实现其实是一样的方式只不过一个是函数的形式一个类的形式。
  #### 装饰器函数实现单例模式
  首先看一下代码实现
   ```markdown
    #!/usr/bin/env python3
def singleton(cls):  
    _instance = {}  
  
    def inner(*args, **kwargs):  
        if cls not in _instance:  
            _instance[cls] = cls(*args, **kwargs)  
  
        return _instance[cls]  
    return inner  
  
  
@singleton  
class Cls(object):  
    def __init__(self, name):  
        self.name = name
```
接下来再看看使用类装饰器的实现方式
```markdown
#!/usr/bin/env python3
class Singleton(object):  
    def __init__(self, cls):  
        self.cls = cls  
        self._instance = None  
  
 def __call__(self, *args, **kwargs):  
        if self._instance is None:  
            self._instance = self.cls(*args, **kwargs)  
        return self._instance  
  
  
@Singleton  
class Cls(object):  
    def __init__(self, name):  
        self.name = name
```
通过前面的两种方式实现单例模式可以看出，都是使用的装饰器的te s
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MTY4OTkxMDMsLTE4NjU0NzA2MjQsMT
I2ODM1NTQ1OCw3MzA5OTgxMTZdfQ==
-->