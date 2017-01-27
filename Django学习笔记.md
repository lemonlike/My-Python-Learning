#Django学习笔记
---
## 在models.py文件中
- verbose_name= "xxx" 是对数据库列字段的注释，在后台管理中有大用。

----------

```python
 class Meta:  
    verbose_name="xxx"
    verbose_name_plural= verbose_name #指定后台显示的复数信息
    db_table="xxx"  #定义表名  数据库中的表名Django默认是“应用名_类名”
    ording="-object_id" #自定义排序，注意前面的“-”表明倒序排列
    
```
---
- 新建的app 要在setting.py中的INSTALLED_APPS进行注册
- 若文件有中文，要在文件的开头加上`-*- coding: utf-8 -*-` 标识该文件使用UTF-8格式编码。

---
>models.EmailField 邮箱类型
.ForeignKey外键类型
.DateTimeFileld 日期类型
.IntegerField 整型
.IpAddressField IP地址类型
.FileField 文件类型
.ImageField 图片类型

---
- 自定义主键  
比如：  
object_id = models.CharFeild(primary_key=Ture,max_length=50,default="",verbose_name="主键")  
- from .models import xxx 前面的点表示在位于当前文件的同级目录中找models文件

## 在view.py文件中 
查询数据库中的记录
>如：all_message = UserMessage.objects.all() 
all() 返回表中所有的记录，返回的记录可以执行for循环
.filter(name='lemon', address='北京') 在filter中添加条件来返回特定的记录
...................
往表中写记录
如：
user_message = UserMessage()
user_message.name = "xxx"
...
user_message.save() #向表中保存数据

---
