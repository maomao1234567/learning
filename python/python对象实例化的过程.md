## Python 对象实例化过程
首先创建一个简单的class
```markdown
#!/usr/bin/env python3
class Foo(object):  
    def __init__(self, x, y):  
        self.x = x  
        self.y = y
```
实例化一个Foo对象的方法就是 foo = Foo(1, 2)，之前的理解这里只是调用了__init__方法来初始化这个对象。其实并不是这样的，Foo(1, 2) 与Foo.__call__(1, 2)是对等的。这个__call__方法是由type元类实现的，因为Foo就是由type实例化的对象，以为其实现了__call__方法因此通过Foo(1, 2)实例化的对象的时候就是执行call方法，由此可见在type里实现的call方法主要就是创建对象，初始化对象。下面看一下type
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQzMzkwNjMxLC0xMTg3MzMzODY3XX0=
-->