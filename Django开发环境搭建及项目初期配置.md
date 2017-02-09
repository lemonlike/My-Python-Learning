#Django开发环境搭建及项目初期配置
---
##开发环境搭建
- 首先需要明确的是安装好Python之后，就可以使用pip命令安装一些需要使用的软件（比如virtualenv django等）。在cmd中如果系统不能识别pip命令，则需要将你的Python安装路径添加到系统环境变量的path中（比如我的是安装路径D:\Python2.7.12\Scripts）。

- 安装虚拟环境virtualenv （**重要！**）  
  virtualenv用来处理多个用Python语言进行开发的项目，在同一台机器上部署，不同项目依赖不同第三方库版本所造成的问题。打个比方，现在你机器上要部署2个Django项目，A项目是用Django1.8开发的，B项目是用Django1.10开发的，2个项目部署到一台机子上如果不做处理肯定会有冲突。virtualenv的功能就是在机器上创建多个python虚拟环境，然后不同的第三方Python库和这些库的不同版本按项目要求安装到各自的虚拟环境中，项目彼此之间就会不影响了。  
  **virtualenv** 是目前最流行的 python 虚拟环境配置工具。它不仅同时支持 python2 和 python3，而且可以为每个虚拟环境指定 python 解释器，并选择不继承基础版本的包。  
**virtualenvwrapper** 顾名思义 virtualenvwrapper 是对 virtualenv 的一个封装，目的是使后者更好用。但由于它基于 shell 开发，在 Windows 系统上，不能使用标准版本，而应使用针对 Windows batch shell 的 virtualenvwrapper-win 。  
**我使用的是virtualenvwrapper**，使用pip命令安装它 `pip install virtualenvwrapper-win`   
新建一个虚拟环境 起名为testvir `mkvirtualenv testvir` 新建的虚拟环境默认目录为C:\Users\asd\Envs\testvir   
一些常用命令：`workon`:查看系统中的虚拟环境； `workon xxx`:进入某一个虚拟环境； `deactivate`:退出虚拟环境。

- 使用pip安装一些需要用到的软件开发包  
进入某个虚拟环境，使用`pip list`可以查看当前虚环境中的安装的开发包。  
在虚拟环境中安装Django   `pip install Django==1.10.5`  

- 在pycharm中 可以在 Tools——> Run manage.py Task... 中使用命令 新建应用等，就不需要在cmd中输入很长的命令来操作django了。  
![文件目录](http://i.imgur.com/w1aHoxr.png)  
在django项目自动生成的目录之外，还需要自己建立新的文件夹来存放不同的内容。  
如新建static文件夹用来存放JS CSS 图片等文件； log存放日志文件； media存放用户上传文件；apps存放新建的应用文件。  

- 安装mysql-Python驱动（**重要！**）  
如果在项目中要用到mysql数据库，就需要在虚拟环境中安装mysql-python驱动。进入虚拟环境 `pip install mysql-python`  **Windows用户在安装的过程中很可能遇到错误！！**  
就是下面这个错误
_mysql.c(42) : fatal error C1083: Cannot open include file: 'config-win.h': No such file or directory error: command '"C:\Users\fnngj\AppData\Local\Programs\Common\Microsoft\Visual C ++ for Python\9.0\VC\Bin\amd64\cl.exe"' failed with exit status 2


>网上一般的解释是，重新安装mysql并在安装mysql里选择安装c++的编译器。。。  
我虽然没试过，但感觉肯定行不通啊，我只是想装一个可以让python远程连接mysql的包而已，管本地mysql什么事？有些解释真是误人子弟。  
但错误提示里也谢了缺少C++的相关环境，后来在网上找到解决办法。
方法如下：  
在[http://www.lfd.uci.edu/~gohlke/pythonlibs/#mysql-python](http://www.lfd.uci.edu/~gohlke/pythonlibs/#mysql-python)下载对应的包版本，  
![](http://i.imgur.com/BDXlrfO.png)  
如果是 64位2.7版本的python，就下载  
MySQL_python-1.2.5-cp27-none-win_amd64.whl
然后在虚拟环境中执行`pip install MySQL_python-1.2.5-cp27-none-win_amd64.whl` 就可以安装完成了。  

**我在安装的过程中出现了安装64位版本失败的问题！！**
![](http://i.imgur.com/q0Ph2p3.jpg)    
错误提示是告诉我的这个平台不能安装此版本，于是我就去百度问题出现的原因，是我的mysql问题？ 还是我的Python版本问题？还是我的pip版本问题？找了两个多小时，找到了一些类似问题的解答：  
![](http://i.imgur.com/mvCEjOE.png)  
这个小哥说，他在安装numpy时遇到了64位安装失败的错误，他升级了pip版本后，成功解决了。可是我之前已经将我的pip升级到最新版了，啊，我这样做没用。  
...................................  
...................................  
继续往下看，我看到了另一个小哥的回答：  
![](http://i.imgur.com/pfjAR3P.png)  
他说他在64位的windows上安装64位版本失败了，他认为.whl文件的版本不是相对于Windows版本的，而是相对于Python版本的。他的Python版本是32位的，于是他安装了32位的 安装成功了。我自己试了下发现我也安装成功了！！ 难道我之前安装的Python版本是32位的？？应该不是吧。。难道我安装的是假64位的Python？（笑哭脸）疲于去深究了。  总之，总算是迈过这个坑了。  

- settings.py中的一些配置   

![](http://i.imgur.com/eFZW90H.png)  
####数据库的配置  
![](http://i.imgur.com/CovzL77.png)  
####templates路径的配置  
![](http://i.imgur.com/Ww84zUW.png)  
####static路径配置  
![](http://i.imgur.com/z86m3fW.png)  

###如果你想学习Django，那么以上我写的都是你将要做的一些事和面临的一些问题，希望对你的Django学习有所帮助。  
![](http://i.imgur.com/WMfbMnO.jpg)  
（未完待续）
