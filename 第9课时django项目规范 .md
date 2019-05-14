## 1.url与是凸函数的映射

## urls文件中

```
from django.contrib import admin
from django.urls import path
from django.http import HttpResponse

def index(request):
    return HttpResponse("豆瓣首页")
def book(request):
    return HttpResponse("图书首页")
urlpatterns = [
    path('admin/', admin.site.urls),
    #相当于http：//127.0.0.1:8000/index/当匹配到以下url时执行index函数，然后“豆瓣首页”返回前端
    path('',index),
    #http：//127.0.0.1:8000/book/ /book/为路径名称
    path('book/',book),

]
```

# 2.将视图凸函数放入新的pythonpackage中

新建名为book的pythonpackage，新建名为views.py的python文件，然后将本在urls.py中的book视图函数转移至该文件中，文件代码如下：

```
#导入HttpResponse函数
from django.http import HttpResponse
def book(request):
    return HttpResponse("图书首页")
```

与此同时，urls文件要调用book视图函数需要以下操作：

`from book.views import book`

即导入视图函数，这样

`path('book/',book),`才能正常使用。

# 3.APP分层

名为book的python包相当于一个app，其中的forms，model分别是表单和模型文件

快速在终端创建类book的app圈子指令：
` python manage.py startapp 圈子`

# 4.总结

将所有视图函数按照功能或模块分层，分入不同的app，所有和某个功能有关的视图都放在相应app中的views.py文件中，模型同理。django已经提供了方便创建app的命令

`python manage.py startapp 【app名称】`