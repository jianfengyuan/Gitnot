1. from __future__ import print_function用法
在开头加上`from __future__ import print_function`这句之后，即使在python2.X，使用print就得像python3.X那样加括号使用。python2.X中print不需要括号，而在python3.X中则需要。在Python2.x用运用Python3.x的语法
**举例如下：**
在python2.x的环境是使用下面语句，则第二句语法检查通过，第三句语法检查失败
```python3
from __future__ import print_function
print('you are good')
print 'you are good'
```
2. 