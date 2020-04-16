## Python 对象实例化过程
首先创建一个简单的class
```markdown
#!/usr/bin/env python3
class Foo(object):  
    def __init__(self, x, y):  
        self.x = x  
        self.y = y
```
实例化一个Foo对象的方法就是 foo = Foo(1, 2)，之前的理解这
<!--stackedit_data:
eyJoaXN0b3J5IjpbODcyNjc0MzI3XX0=
-->