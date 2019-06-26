# xadmin
本库内容摘自<https://github.com/sshwsfc/xadmin>
下面是xadmin的一些配置步骤

### 1.下载xadmin放在项目目录中,与static同级

### 2.修改配置文件settings

```python
NSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'xadmin', #添加()
    'crispy_forms', #添加()
]
# 语言配置
LANGUAGE_CODE = 'zh-hans'#更改
TIME_ZONE = 'Asia/Shanghai'#更改
```

### 3.修改路由

```python
import xadmin 

urlpatterns = [
  # url(r'^admin/', admin.site.urls),注释原路由
  url(r'^xadmin/',include(xadmin.site.urls)),#添加新路由
]
```

### 4.增加配置文件

在每个APP目录下新建一个adminx.py文件

1. models.py

   ```python
   from django.db import models
   
   class User(models.Model):
       """用户表"""
       name = models.CharField(max_length=32, verbose_name="姓名")#verbose_name在后台显示的字段名
       gender = models.IntegerField(choices=Gender, verbose_name="性别")
       phone = models.CharField(max_length=11, verbose_name="手机号")
       email = models.CharField(max_length=64, verbose_name="邮箱")
   
       class Meta:
           verbose_name = '用户' #verbose_name 在后台显示的表名
           verbose_name_plural = verbose_name
   ```

2. adminx.py

   ```python
   import xadmin
   from apps.models import User
   
   class UserAdmin(object):
       list_display = ['name','gender','phone','email']#显示信息的字段
       search_fields = ['name','phone','email']#可查询字段
       list_filter = ['name']#可以根据该字段过滤
       
   xadmin.site.register(User,UserAdmin)
   ```

   

   

   
