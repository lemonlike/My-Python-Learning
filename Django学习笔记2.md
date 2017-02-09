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

