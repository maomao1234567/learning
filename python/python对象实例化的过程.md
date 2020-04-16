## Python 对象实例化过程
首先创建一个简单的class
```markdown
#!/usr/bin/env python3
class Foo(object):  
    def __init__(self, x, y):  
        self.x = x  
        self.y = y
```
实例化一个Foo对象的方法就是 foo = Foo(1, 2)，之前的理解这里只是调用了__init__方法来初始化这个对象。其实并不是这样的，Foo(1, 2) 与Foo.__call__(1, 2)是对等的。这个__call__方法是由
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTg4MzcwMjFdfQ==
-->