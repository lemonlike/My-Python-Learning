# Django快速入门

---
#### 安装Django  
 在Django官网下载最新版的django（我并不是使用pip来安装的），下载好后解压到自己建的目录下，在cmd中运行`python setup.py install`即可完成安装。

#### 新建第一个Django项目  
`django-admin.py startproject xxx` 即可创建一个新项目 如：`django-admin.py startproject myblog`  
在这个过程中我看一些教程上使用`django-admin startproject xxx`，**我目前没搞明白使用**`django-admin`和`django-admin.py`的区别。
执行上述指令时，系统会提示你django-admin.py不是内部指令或外部指令，你需要将admin.py的路径加入到系统的环境变量的path中。我的admin.py的路径是：D:\Python2.7.12\Lib\site-packages\Django-1.10.5-py2.7.egg\django\bin 
你还有可能遇到一个问题是 提示你选择打开admin.py的默认程序，这说明你打开.py文件的默认程序没有设置，只需先设置默认打开程序为python.exe 再次运行新建指令就可以了。

#### 启动Django内置web服务器  
进入新建项目目录下 可以看到有一个manage.py 的文件，在cmd中输入`python manage.py runserver` 即可启动内置服务器，默认地址为 127.0.0.1:8000  
也可自己修改默认的端口号 `python manage.py runserver 8888`端口号改为了8888 。

#### 在Django项目中创建应用  
`python manage.py startapp xxx` 例如新建个blog应用 `python manage.py startapp blog` 在下面将用到这个例子。

#### 创建第一个页面响应，来演示Django的路由映射功能  
第一步：在myblog/blog/view.py 中建立一个路由响应方法：  

```python
from django.http import HttpResponse

def welcome(request):
    return HttpResponse("Hello Lemon")
```
第二步：通过URL映射将用户的http访问与该方法绑定起来：  
在myblog/blog/目录中新建一个urls.py 文件，管理该应用app中的所有URL映射  

```python
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^welcome/', views.welcome),
]
```
第三步：在该项目URL文件myblog/urls.py 的 urlpatterns中增加一项，声明对应用app中urls.py文件的引用：  

```python
from django.conf.urls import url, include  #新增include
from django.contrib import admin

urlpatterns = [
    url(r'^admin', admin.site.urls),
    url(r'^blog/', include('blog.urls')),  #本行新增
]
```
通过include()函数将两个urlpatterns连接了起来。
接下来启动django的内置web服务器，在浏览器中输入127.0.0.1/blog/welcome/ 就可以实现访问了。

**注意：**  
- 根urls.py针对app配置的URL名称是该app所有URL的总路径。  
- 配置URL时注意正则表达式结尾符号$和/  




#### 生成数据移植文件
`python manage.py makemigrations 应用名`
#### 移植到数据库
`python manage.py migrate`


## 写代码时注意的点
- 在POST的请求表单中添加一句代码{%csrf-token%}，目的是防止csrf攻击。
- ![Django中的超链接配置](http://i.imgur.com/EKFLDKm.jpg)
- ![超链接参数配置](http://i.imgur.com/gF3WOgC.jpg)

