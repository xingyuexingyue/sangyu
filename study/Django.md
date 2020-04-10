## 模型层以及如何通过模型层来建表

Django 提供了一个抽象的模型 ("models") 层

- 什么是模型层？
    -  这里模型的思想与Java中的ORM（Object Relationship Mapping） 对象关系映射类似
    - 模型准确且唯一的描述了数据
    - 它包含要储存的数据的字段
    - 一般来说，每一个模型都映射一张数据库表

- 如何创建模型？
    - 每个模型都是一个 Python 的类，这些类继承 `django.db.models.Model`
    - 模型类的每个属性都相当于一个数据库的字段
    - 利用这些，Django 提供了一个自动生成访问数据库的 API，可以通过这些API对数据库进行增删改查

- Settings.py 文件中增加一些配置
    - INSTALLED_APPS：定义了你的模型后，需要将模型添加到Django，所以需要将包含models的模块名称添加进去
    - DATABASES：数据库连接信息

-  定义一个Person模型
    -  first_name 和 last_name 是模型的 字段
    - 每个字段都被指定为一个类属性，并且每个属性映射为一个数据库列。

#### 代码实例

1. 当前项目的目录结构

![](https://upload-images.jianshu.io/upload_images/2765653-b5b74e030c8b5981.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 包含models.py 所在目录名称为：signtest，将它添加到settings.py

![](https://upload-images.jianshu.io/upload_images/2765653-91bb7ecb279f4fa0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. settings.py中增加数据库的连接信息（我这里使用的是mysql）

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': '127.0.0.1',  # 数据库主机
        'PORT': 3306,  # 数据库端口
        'USER': 'root',  # 数据库用户名
        'PASSWORD': 'abcd123456',  # 数据库用户密码
        'NAME': 'my_dj_test'  # 数据库名字
    }
}
```

4. models.py 中增加模型类

```
from django.db import models 

class Musician(models.Model):
    first_name = models.CharField(max_length=50)  #每个变量对应的是数据库中每个字段
    last_name = models.CharField(max_length=50)
    instrument = models.CharField(max_length=100)

class Album(models.Model):
    artist = models.ForeignKey(Musician, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)
    release_date = models.DateField()
    num_stars = models.IntegerField()
```

5. 因为我创建的项目用的是python的虚拟环境，virtualenv就是用来为一个应用创建一套“隔离”的Python运行环境。所以需要安装一些环境的依赖

```
# 因为我现在的Django版本是3.x会出现一些版本不对应的情况，所以我将版本降到了2.1.7 ，没有这个问题的不需要此操作
$ pip3 install Django==2.1.7 
# Successfully installed Django-2.1.7
```

```
# 安装pymysql
$ pip3 install pymysql
# Successfully installed pymysql-0.9.3
```

6. 在包含settings.py的目录下的__init__.py文件中，将下面的代码放进去

```
import pymysql
pymysql.install_as_MySQLdb()
```

7. 先执行数据库迁移的命令 `manage.py makemigrations`，再执行建表的命令`manage.py migrate`

```
$ python3 manage.py makemigrations
Migrations for 'signtest':
  signtest/migrations/0001_initial.py
    - Create model Album
    - Create model Musician
    - Add field artist to album
```

```
$ python3  manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions, signtest
Running migrations:
  Applying contenttypes.0001_initial... OK
# ...
(venv) pengyapandeMacBook-Air:sangyu pengyapan$ 
```

8. 进入数据库查看

![](https://upload-images.jianshu.io/upload_images/2765653-b7e8fa3f47883260.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

9. 到这就里就根据Django模型在数据库建表成功了

10. 其他的一些命令，可能用不到只是记录下

```
# 卸载mysqlclient
pip uninstall mysqlclient
# 异常：mysqlclient 1.3.13 or newer is required; you have 0.9.3
# 可能是由于Django版本不一致的问题改成，也可以通过修改/Users/lixiang/.env/lib/python3.6/site-packages/django/db/backends/mysql/base.py 这个文件下的注释掉version < (1, 3, 13)
# 这是在sql中执行的命令的，主要是记录建表信息会记录在这个表django_migrations中
DELETE FROM django_migrations WHERE app='your-app-name';
# 下载依赖时增加版本信息
mysql-connector-python==1.0.12
# 要为应用创建初始迁移，请运行makemigrations并指定应用名称。将创建迁移文件夹
./manage.py makemigrations <myapp>
```




