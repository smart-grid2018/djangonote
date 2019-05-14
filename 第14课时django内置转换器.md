# 1.route 参数

传递参数是通过尖括号<>来指定的，在传递参数时可以指定参数的数据类型，例如文章的id为int类型，可以这样写<int:id>，以后匹配时只会匹配到id为int类型的url而不是其他url。

常用参数类型还有：

str;int;slug;uuid;path

# 2.django内置的URL转换器converters

在urls.py通过以下代码导入该转换器

```
from django.urls import converters
```

内置了不同类型的的参数类型函数：

以int为例

```
class IntConverter:
    regex = '[0-9]+' #+号表示有一个或多个这样的数字

    def to_python(self, value):
        return int(value)

    def to_url(self, value):
        return str(value)
```

regex为正则表达式

再以str为例：

```
class StringConverter:
    regex = '[^/]+' #其中的^为托字符表示除其后面的/外任意字符可视为字符串

    def to_python(self, value):
        return value

    def to_url(self, value):
        return value
```

满足条件：除了斜杠以外字符

int：阿拉伯数字

path：所有字符默认满足

uuid：特定格式满足

slug：英文中的横杆字符或阿拉伯数字