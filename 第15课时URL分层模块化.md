# 1.URL分层模块化

## include函数

如果项目变大urls都放urls.py就不好管理，可以将每个app自己的urls放在自己的app文件夹中的urls.py来存储相关的urls

需要注意：

1.在主urls.py文件中导入include函数包含子urls.py，子urls.py的路径是相对于项目的，具体代码如下：

主urls中

`from django.urls import path,include`

导入主路径book即可

```
path('book/',include('book.urls')),
```

在子urls（即book.urls）中，需要将所有相关path放入urlpattern的变量中。代码如下

```
urlpatterns =[
    #意味着之前的路径部分为book/
    path('',views.book),
    path('detail/<book_id>/<category_id>',views.book_detail)
]#这里的book，book_detial都是views文件里面相应的函数
```