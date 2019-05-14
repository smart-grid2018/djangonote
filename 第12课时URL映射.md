# 1.URL映射

1.为什么会去urls.py寻找映射是因为在setting.py文件中配置了`Root_URLCONF`为`urls.py`，所有django都回去`urls.py`中寻找

2.在`urls.py`中的映射都应放在urlpatterns变量中。

3.所有映射使用path函数等函数进行包装的。

