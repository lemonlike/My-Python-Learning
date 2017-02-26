- request.path  
`{% if request.path|slice:'9' == '/org/list' %}class="active"{% endif %}`  
可以使用request.path 取到url的相对路径（不包含ip地址），进行一些操作。上面的例子是配合slice截取特定的字符串，使含相同字符串的URL指向的页面的显示效果一致。  

- 网页重定向  
```
from django.http import HttpResponse, HttpResponseRedirect  
class LogoutView(View):
    """
    用户登出
    """
    def get(self, request):
        logout(request)
        from django.core.urlresolvers import reverse
        return HttpResponseRedirect(reverse("index"))
```

