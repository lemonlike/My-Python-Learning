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
