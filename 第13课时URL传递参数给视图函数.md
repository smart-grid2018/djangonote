# 1.URL传递参数

传递book_id参数：代码如下

```
from django.contrib import admin
from django.urls import path
from django.http import HttpResponse
from book import views
from 圈子.views import quanzi
#视图函数
def index(request):
    return HttpResponse("图书库首页")

urlpatterns = [
    path('admin/', admin.site.urls),
    #相当于http：//127.0.0.1:8000/index/当匹配到以下url时执行index函数，然后“豆瓣首页”返回前端
    path('',index),
    #http：//127.0.0.1:8000/book/ /book/为路径名称
    path('book/',views.book),
    #book/detail/1/则1传递给参数book_id
    path('book/detail/<book_id>',views.book_detail),
    path('quanzi/',quanzi),
]
```

相应views文件里的视图函数如下：
``

```
from django.http import HttpResponse
def book(request):
    return HttpResponse("图书首页")
def book_detail(request,book_id):
    #根据book_id提取信息
    text="您获取的图书id是： %s"%book_id
    return HttpResponse(text)
```

那么在访问http://0.0.0.0:8000/book/detail/id/时会返回相应的id，

# 2.查询字符串类url

视图函数参数request包括客户端请求的数据，包括查询字符串

查询字符串类请求属于GET请求，因此在调用相应的视图函数时，需要用request参数内置的GET来获取相应的查询字符串，在视图函数中使用`request.GET.get('参数名称')的方式来获取`

相应book.views.py代码如下：

```
def author_detail(request):
    author_id = request.GET.get('id')#注意这里获取参数id的方式
    text='作者的id是 %s' % author_id
    return HttpResponse(text)
```

相应urls.py代码如下

`path('book/author/',views.author_detail),`

则在访问时访问

http://0.0.0.0:8000/book/author/?id=1

返回结果为：作者的id是1