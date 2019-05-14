# 1.urls命名与反转

## 给url命名：

url经常变换，如果写死则经常要在视图文件中的重定向函数的重定向路径进行重命名

## 如何给url指定名称

在子urls文件中的path函数传递一个一个name参数可以指定，示例代码如下：

```
from django.urls import path
from . import views
urlpatterns = [
    path('',views.index, name = 'index'),
    path('login/',views.login,name = 'login'),
]
```



在相应views文件中导入shortcut模块中的redirect和reverser重定向和反转函数来分别实现网页的跳转以及url的命名，具体代码如下：

```
from django.http import HttpResponse
from django.shortcuts import redirect,reverse #重定向y与反转
def index(request):
    # ?username=xxx
    username = request.GET.get('username')
    if username:
        return HttpResponse('前台首页')
    else:
        return redirect(reverse('login'))#将名为login的url反转成path中的名称在进行重定向
def login(request):
    return HttpResponse('前台登录页面')
```

## 2.应用命名空间app_name

为了避免不同app的url命名重复导致访问错误，在子urls文件中添加应用命名，代码如下：

```
app_name = 'front'
```

同时在views文件中reverse即需要反转的路径名前加上应用名，代码如下：

```
def index(request):
    # ?username=xxx
    username = request.GET.get('username')
    if username:
        return HttpResponse('前台首页')
    else:
        return redirect(reverse('front:login'))#将名为login的url反转成path中的名称在进行重定向
```

以后就可以使用`应用命名空间:url名称` 方式来进行反转