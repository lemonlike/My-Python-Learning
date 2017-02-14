- 定义UserProfile表覆盖默认的User表  
![](http://i.imgur.com/tBHRcFa.png)  
因为Django默认的User表中的列项字段不能满足实际使用过程中的字段，因此需要添加自定义字段就需要继承User表。  
需要注意的地方是：  
1.引入Django已经定义的User表 `AbstractUser`  
2.上传图片文件时的 `upload_to="image/%Y/%m`  
3.`__unicode__`方法  
![](http://i.imgur.com/A7sXVYR.png)  
4.choices的用法  
5.引入datetime  
注意：datetime.now() 加括号返回的是编译文件时的时间，不加括号返回的是记录添加的时间，一般使用时不加括号。  

- 使用ImageField类型需要安装插件 Pillow  
- 数据表之间一对一的关系，通过在两个模型中的任意一个中定义 OneToOneField 类型的字段来完成； 一对多的关系 通过在“附表”中设置到“主表”的外键引用（ForeignKey)来完成；多对多的关系 通过在两个模型中的任意一个中定义 ManyToManyField类型的字段来完成。  
- 在把所有应用app放到统一目录apps下后，需要把app加入的Python搜索目录下  
```
import sys  
sys.path.insert(0, os.path.join(BASE_DIR, 'apps'))
```
- Django admin（xadmin）后台管理系统的特点  
1.权限管理 2.少前端样式 3.快速开发

- 将后台管理系统设置为中文、调整时区  
![](http://i.imgur.com/8Q1tYDr.png)  

- 新建名为extra_apps的Python包，用来存放第三方源码包，如xadmin等。  
需要将这个包Mark为source包，不然在pycharm中会报错。若要在cmd中以manage.py方式运行项目，需要把包加入到项目搜索目录下，同 上面讲到的apps。

- 把表单注册到xadmin中  
![](http://i.imgur.com/vObsx7B.png)  
继承的是object类； 在search_fields和list_filter中要注意 变量是**外键类型**的情况。

- Xadmin全局配置  
放在adminx.py文件中  
![](http://i.imgur.com/z6aEzHx.png)  
![](http://i.imgur.com/UCuSxds.png)  

BaseSetting类配置主题  
GlobalSettings类配置左上角标题、底部名称、左侧菜单显示风格。  
注意注册方式，需要引入xadmin中的views  

-app显示名称的设置(以uses为例)  
在应用对应的apps.py文件中,设置`verbose_name = u"用户信息"`  
在__init__.py文件中 `default_app_config = "users(应用名).apps.UsersConfig"`  

