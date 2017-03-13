- HTML页面中静态文件的引用方法  
在开头写上`{% load staticfiles %}`  
引用静态文件的书写格式，如：`{% static 'css/login.css' %}`  

- 一个简易的验证码插件 `django-simple-captcha`  
安装方法: `pip install django-simple-captcha==0.4.6`  
一定要安装`0.4.6`的版本  
开发文档： [http://django-simple-captcha.readthedocs.io/en/latest/usage.html#installation](http://django-simple-captcha.readthedocs.io/en/latest/usage.html#installation)  

- 在用户注册时需要向数据库提交用户信息，其中password在数据库中是以密文形式存储的，所以在向数据库写入时需要将明文转化为密文，方法：  
```
from django.contrib.auth.hashers import make_password
user_profile.password = make_password(pass_word)  
```  
- 在注册时需要发送邮箱验证，发送邮箱的配置如下：  
```
在settings.py文件中配置
EMAIL_HOST = "smtp.sina.com"
EMAIL_PORT = 25
EMAIL_HOST_USER = "lemonyolo@sina.com"
EMAIL_HOST_PASSWORD = "liuminglei123"
EMAIL_USE_TLS = False
EMAIL_FROM = "lemonyolo@sina.com"
```
发送邮件的内容：  

	```
	from django.core.mail import send_mail
	
	def send_register_email(email, send_type="register"):
	    email_record = EmailVerifyRecord()
	    code = random_str(16)
	    email_record.code = code
	    email_record.email = email
	    email_record.send_type = send_type
	    email_record.save()
	
	    if send_type == "register":
	        email_title = u"lemONline学习网注册激活链接"
	        email_body = u"请点击下面链接激活你的账号：
			http://127.0.0.1:8000/active/{0}".format(code)
	
	        send_status = send_mail(email_title, email_body, EMAIL_FROM, [email])
	```  

	`send_status`方法是django内置的方法，实现向注册用户的邮箱发送邮件  

- 在配置好发送邮件的邮箱后，调试时遇到了这个错误`django 535, '5.7.12 SMTP access disabled'` 通过百度后找到解决方法是，将邮箱的密码重置，结果这个错误真的解决了，但是那个解答的人也不知道为什么这样...（这个问题留到以后再研究）。  


- 发送的邮件链接中有一段随机字符串，这段字符串的生成方法如下：  
	  
	```
	def random_str(randomlength=8):
	    str = ''
	    chars = 'AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsTtUuVvWwXxYyZz0123456789'
	    length = len(chars) - 1
	    random = Random()
	    for i in range(randomlength):
	        str += chars[random.randint(0, length)]
	    return str
	```  
- 验证邮箱的流程：
首先从链接中截取到后面的随机字符串，方法是`url(r'^active/(?P<active_code>.*)/$', ActiveUserView.as_view(), name="user_active")`  然后根据这段随机字符串，在验证码表查到该字段，再根据该字段中的邮箱在用户信息表中查到对应的用户，再将该用户的is_active设置为True(激活态)，完成用户的激活。  

- 找回密码的流程：  
首先跳转到找回密码页面，填写邮箱、验证码，提交后，后台向邮箱中发送验证链接。点击链接跳转到修改密码页面。填写密码，提交过程中对表单验证，无误后，将新密码写入数据库，最后跳转到登陆页面。  
一些细节的地方，比如注册时邮箱已存在则需要返回提示信息等等，需要在开发时考虑周全，在这就不再赘述了。  

- Template模板继承  
包裹需要继承的部分：  
`{% block xxx %} {% endblock %}`  
在新html页面中引入：  
`{% extends 'base.html' %} {% endblock %}`  

- 处理上传文件的配置  

```
settings.py文件中：  
MEDIA_URL = '/media/'  
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')  
TEMPLATES中：
'django.core.context_processors.media' 

配置url：  
from django.views.static import serve  
url(r'^media/(?P<path>.*)$', serve, {"document_root": MEDIA_ROOT}),

HTML中：
{{ MEDIA_URL }}{{ 图片的相对路径 }}  
```
- 分页功能  
安装`pip install django-pure-pagination`  
相关配置和使用方法 请参考它在github上的使用文档  

- ModelForm  
参考样例：  
![](http://i.imgur.com/ebrkHk5.png)  
可自定义验证的方法，定义的方法名称需要以clean开头  
![](http://i.imgur.com/yTbDY6R.png)  
使用ModelForm可以直接向数据库中存数据  
返回的提示信息使用json ajax 这个地方得好好看看  

- URL的inclue实现URL的分发  
`url(r'^org/', include('organization.urls', namespace="org")),`  

- 一对多关系中  
![](http://i.imgur.com/NHtj77U.png)  
在“多”中定义“一”的外键，可以使用xxx(一)一条记录.xxx（多）_set.all()方法从“一”中取得“多”的所有值。

- 在Models中定义的表，其中有的字段若使用了choices，则在html中调用该字段时需要这样调用：  
```
如Models中定义：  
degree = models.CharField(choices
(('gj', '高级'), ('zj', '中级'), ('cj', '初级')), max_length=3)  
-
在html中为了让其显示文字的值，调用该字段时：
course.get_degree_display
若使用 course.degree 则显示的值是 gj zj cj 。
```

- 可以在models中定义函数，这样可以取到有外键关系的表值。  
![](http://i.imgur.com/zrLwQjn.png)  

- 在表中可自定义一个tag(标签)字段，使用filter来检索具有相同tag的记录，达到进行相关推荐的效果。  

- 在models中添加一个外键字段时，需要设置null=True blank=True，不然在migrate时会报错。  

- 相关推荐  
![](http://i.imgur.com/FEwdYoL.png)  

- 登陆验证，若未登录，则跳转到登录页面  
![](http://i.imgur.com/bGHLZ0m.png)  
