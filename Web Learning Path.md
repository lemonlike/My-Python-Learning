# My Python Web Learning Path

标签： Python

---
## HTML
## CSS
## BootStrap
## Python
## Django
### 安装Django 
- 安装过程：  
 在Django官网下载最新版的django（我并不是使用pip来安装的），下载好后解压到自己建的目录下，在cmd中运行`python setup.py install`即可完成安装。

- 新建第一个Django项目   
`django-admin.py startproject xxx` 即可创建一个新项目  
在这个过程中我看一些教程上使用`django-admin startproject xxx`，**我目前没搞明白使用**`django-admin`和`django-admin.py`的区别。
执行上述指令时，系统会提示你django-admin.py不是内部指令或外部指令，这需要你将admin.py的路径加入到系统的环境变量的path中。我的admin.py的路径是：D:\Python2.7.12\Lib\site-packages\Django-1.10.5-py2.7.egg\django\bin 
还有可能遇到让你选择打开admin.py的默认程序，这说明你打开.py文件的默认程序没有设置，只需先设置默认打开程序为python.exe 再次运行新建指令就可以了。

- 启动Django内置web服务器  
进入新建项目目录下 可以看到有一个manage.py 的文件，在cmd中输入`python manage.py runserver` 即可启动内置服务器，默认地址为 127.0.0.1:8000  
也可自己修改默认的端口号 `python manage.py runserver 8888`端口号改为了8888 。

- 在Django项目中创建应用  
`python manage.py startapp xxx`