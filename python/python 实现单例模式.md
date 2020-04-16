## 单例模式
  单例是一种设计模式，属于创建型模式。意思是在某一个类只存在一个实例化对象。它的实现原理是，在实例化对象的时候检查是否存在该类的实例如果存在就直接返回这个实例如果不存在就先实例化一个改类的对象存在一个类变量中并且返回这个实例。在python中主要有四种实现单例模式的方法，分别是装饰器函数、装饰器类、__new__函数实现、元类实现。虽然有四种方式但是核心的实现还是一样的，前两种方式的实现其实是一样的方式只不过一个是函数的形式一个类的形式。
  #### 装饰器函数，类装饰器实现单例模式
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
通过前面的两种方式实现单例模式可以看出，都是使用的装饰器的特性在类实例化时添加额外的一些操作来满足只有一个实例化对象存在的情况。核心思想就是使用一个全局的变量来存储在第一种实现方式上使用一个dict _instance, key 为类的一个唯一标识，value就是类的实例化对象。在这里我的理解就是，通过装饰器来代理类的实例化操作只是在实例化之前判断一下实例是否存在。
#### 使用__new__实现单例模式
使用这种方式来实现单例模式前提是必须了解，python类实例化对象的全过程，这个问题在前面有讲解，这里简单的说下python实例化对象是先调用__new__创建一个实例然后返回这个实例再由__init__方法对这个实例进行初始化。因此，这种方式就是重写__new__在创建实例的时候判断是否存在该类的实例化对象。当然核心的实现方式也是需要一个全局的变量来存储类实例。
下面看看这种方式的代码实现：
```markdown
#
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMDUyNzA1NDUsLTE4NjU0NzA2MjQsMT
I2ODM1NTQ1OCw3MzA5OTgxMTZdfQ==
-->