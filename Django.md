



# Django3.2前言

之前我们介绍过web应用程序和http协议，简单了解过web开发的概念。Web应用程序的本质

> 1. 接收并解析HTTP请求，获取具体的请求信息
> 2. 处理本次HTTP请求，即完成本次请求的业务逻辑处理
> 3. 构造并返回处理结果——HTTP响应

```Python
import socket

server = socket.socket()
server.bind(('127.0.0.1', 8080))
server.listen(5)

while True:
    conn, addr = server.accept()
    data = conn.recv(1024)
    print("data:\n",data)
    # 路径解析
    request_path = data.decode('utf-8').split('\r\n')[0].split(' ')[1]

    if request_path == '/':
        with open("index.html", "rb") as f:
            data = f.read()
        conn.send(b'HTTP/1.1 200 OK\r\n\r\n' + data)
    elif request_path == '/timer':
        with open("login.html", "rb") as f:
            data = f.read()
        conn.send(b'HTTP/1.1 200 OK\r\n\r\n' + data)
    else:
        with open("notFound.html", "rb") as f:
            data = f.read()
        conn.send(b'HTTP/1.1 404 Not Found\r\n\r\n' + data)
```

那么什么是web框架呢?

> Web应用框架有助于减轻网页开发时共通性活动的工作负荷，例如许多框架提供数据库访问接口、标准样板以及会话管理等，可提升代码的可再用性。

说简单点就是web框架用于搭建Web应用程序，免去不同Web应用相同代码部分的重复。



# 一、Django介绍

![image-20211118141522986](assets/image-20211118141522986.png)

Python下有许多款不同的 Web 框架。Django是重量级选手中最有代表性的一位。许多成功的网站和APP都基于Django。Django 是一个开放源代码的 Web 应用框架，由 Python 写成。Django 遵守 BSD 版权，初次发布于 2005 年 7 月, 并于 2008 年 9 月发布了第一个正式版本 1.0 。

![image-20211001230147585](assets/image-20211001230147585-3100818.png)

[Django文档](https://www.djangoproject.com/)

Django 采用了 MVT 的软件设计模式，即模型（Model），视图（View）和模板（Template）。

这个MVT模式并非django首创，在其他的语言里面也有类似的设计模式MVC，甚至可以说django里面的MVT事实上是借鉴了MVC模式衍生出来的。

> M，Model，模型，是用于完成操作数据库的。
>
> V，View，视图，里面的代码就是用于展示给客户端的页面效果。
>
> C，Controller，控制器，是一个类或者函数，里面的代码就是用于项目功能逻辑的，一般用于调用模型来获取数据，获取到的数据通过调用视图文件返回给客户端。

而MVT指的是：

> 1. M全拼为Model，与MVC中的M功能相同，负责和数据库交互，进行数据处理。
> 2. V全拼为View，与MVC中的C功能相同，接收请求，进行业务处理，返回应答。
> 3. T全拼为Template，与MVC中的V功能相同，负责封装构造要返回的html。

MVT模型的工作流程

![image-20211004122200077](assets/image-20211004122200077.png)

> 路由控制器将请求转发给对应的视图函数，完成业务逻辑，视图函数将从model中获取的数据嵌入到template的中模板文件（html）渲染成一个页面字符串，返回给客户端的流程。

所以我们学习Django重点是四个部分：url路由器+MVT

# 二、Django下载运行

## 1、Django下载

![img](assets/release-roadmap.688d8d65db0b.png)

目前我们学习和使用的版本是3.2LTS版本

```bash
目前开源软件发布一般会有2个不同的分支版本:
1. 普通发行版本:                  经常用于一些新功能,新特性,但是维护周期短,不稳定.
2. 长线支持版本[LongTerm Supper]: 维护周期长,稳定

软件版本格式: 大版本.小版本.修订号
大版本一般是项目内容/软件的核心架构发生改动, 以前的代码已经不适用于新的版本
小版本一般是功能的删减, 删一个功能,小版本+1, 减一个功能,小版本+1
修订号一般就是原来的代码出现了bug, 会针对bug代码进行修复, 此时就会增加修订号的数值
```

![image-20210525103556002](assets/image-20210525103556002-1626660206042.png)

官网: `http://www.djangoproject.com`

文档:`https://docs.djangoproject.com/zh-hans/3.2/`

在本地安装

```python 
pip install django
pip install django==3.2
```

```bash
pip源:
    https://pypi.douban.com/simple/  豆瓣源
    https://pypi.tuna.tsinghua.edu.cn/simple   清华源
        
使用格式:
    pip install django -i https://pypi.douban.com/simple/
```

```bash
# 查看django版本号
django-admin --version
```

当然在以后开发或者学习中,我们肯定都会遇到在一台开发机子中,运行多个项目的情况,有时候还会出现每个项目的python解析器或者依赖包的版本有差异.

## 2、Django启动

创建虚拟环境并在虚拟环境中下载安装django包

```bash
pip install django==3.2 -i https://pypi.douban.com/simple/   # 1 安装django环境
cd ~/Desktop                                                 # 2 进入到一个目录    
django-admin startproject demo                               # 3 创建一个启动文件   自定义demo目录名
```

完成了以后,直接直接下pycharm下面的终端terminal中使用命令运行django

```bash
python manage.py runserver 8090            # 4 终端下输入启动命令  runserver  后面设置ip 端口
```

![image-20210723182232002](assets/image-20210723182232002.png)

在浏览器中访问显示的地址`http://127.0.0.1:8090`.效果如下则表示正确安装了.

![image-20210723181947547](assets/image-20210723181947547.png)

> runserver默认启动的wsgi.py文件作为web服务器接口

## 3、创建应用

创建自应用：

```python 
python manage.py startapp 子应用名称
```

Django完整的目录结构如下：

```bash
│─ manage.py    # 终端脚本命令,提供了一系列用于生成文件或者目录的命令,也叫脚手架
└─ dome/        # 主应用开发目录,保存了项目中的所有开发人员编写的代码, 目录是生成项目时指定的
    │- asgi.py      # django3.0以后新增的，用于让django运行在异步编程模式的一个web应用对象
    │- settings.py  # 默认开发配置文件
    │- urls.py      # 路由列表目录,用于绑定视图和url的映射关系
    │- wsgi.py      # wsgi就是项目运行在wsgi服务器时的入口文件
    └- __init__.py
└─ app01         # 子应用
    │- models    # 该应用的模型类模块
    │- views     # 该应用的视图模块
    │- tests     # 该应用的单元测试模块
    │- apps      # 该应用的一些配置，自动生成
    │- admin.py  # 该应用的后台管理系统配置
```

当然如果每次运行项目都要在终端下输入命令的话,很麻烦,这时候我们可以借助pycharm直接自动运行这段命令.当然,这个需要我们在pycharm配置一下的.

**![1604737500628](assets/1604737500628-1626660285528.png)**

![1604737537897](assets/1604737537897-1626660285529.png)(小三角形)

可以在runserver 参数后配置修改django监听的端口和IP地址,当然,只能是127.0.0.1对应的其他地址.不能是任意IP.否则无法运行或访问!!

![1604737556681](assets/1604737556681-1626660285529.png)

![image-20211005130421126](assets/image-20211005130421126.png)

## 4、快速使用

在django中要提供数据展示给用户,我们需要完成3个步骤.

> 需求：利用Django实现一个查看当前时间的web页面。
>
> 基于MTV模型，设计步骤如下：
>
> - step1：在urls.py中设计url与视图的映射关系。
> - step2：创建子应用，在views.py中构建视图函数。
> - step3：将变量嵌入到模板中返回客户端。

#### （1）创建应用

```bash
python manage.py startapp 子应用名称
```

> 子应用的名称将来会作为目录名而存在,所以不能出现特殊符号,不能出现中文等多字节的字符.

#### （2） 绑定路由

`demo/urls.py`代码:

```python
from django.contrib import admin
from django.urls import path
from home.views import index
urlpatterns = [
    path('admin/', admin.site.urls),         # 第一个参数是用户的路径匹配到此就会走第二个视图函数
    path("timer/", timer),
    path("",root)                            # 空就是代表根目录
]

```

#### （3）视图函数

`home/view.py`,代码:

```python
from django.shortcuts import render,HttpResponse

# Create your views here.
import datetime

def timer(request):  # 视图函数第一个参数必须是request                                         
    
    now=datetime.datetime.now().strftime("%Y-%m-%d %X")   # 生成了一个当前时间字符串
   
    return render(request,"timer.html",{"now":now})  
	 # render是一个渲染函数，用于返回一个html文件，第二位置是html文件路径，第三个位置是html内的模板参数，用字典构建来传至html内
```

#### （4）构建模板

html模板内用{{}}号进行占位，花括号内定义一个名。在视图函数传的参就会传至对应位置

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        span{
            color: red;
        }
    </style>
</head>
<body>

<h3>当前时间：<span>{{ now }}</span></h3>

</body>
</html>
```

因为上面我们绑定index视图函数的url地址是index,所以我们可以通过`http://127.0.0.1:8000/`拼接url地址`index`来访问视图函数

![image-20211004165611513](assets/image-20211004165611513.png)

# 三、路由控制器

Route路由, 是一种映射关系！路由是把客户端请求的url路径和用户请求的应用程序[这里意指django里面的视图进行绑定映射的一种关系。

> 请求路径和视图函数不是一对一映射关系！

在django中所有的路由最终都被保存到一个变量 `urlpatterns.`, urlpatterns必须声明在主应用下的urls.py总路由中。这是由配置文件settings设置的。

在django运行中，当客户端发送了一个http请求到服务端，服务端的web服务器则会从http协议中提取url地址, 从程序内部找到项目中添加到urlpatterns里面的所有路由信息的url进行遍历匹配。如果相等或者匹配成功，则调用当前url对象的视图方法。

在给urlpatterns路由列表添加路由的过程中,django一共提供了2个函数给开发者注册路由.

```python
from django.urls import path      # 字符串路由
from django.urls import re_path   # 正则路由，会把url地址看成一个正则模式与客户端的请求url地址进行正则匹配

# path和re_path 使用参数一致.仅仅在url参数和接收参数时写法不一样
```

#### （1）基本使用

正则内用`（）`括号分组的值会当成 `位置参数` 传到视图函数内

当给正则的分组进行了分组命名后就会当成 `命名参数` 传给视图函数，此时视频函数的形参就要对应到正则里的命名

```python 
path(r'^articles/2003/$', views.special_case_2003),
re_path(r'^articles/([0-9]{4})/$', views.year_archive),
re_path(r'^articles/([0-9]{4})/([0-9]{2})/$', views.month_archive),
re_path(r'^articles/(?P<year>[0-9]{4})/(?P<month>[0-9]{2})/$', views.month_archive2),
```

#### （2）路由分发

把全局上的urls的路径分到某app文件夹下的urls下（自行在app目录下创建urls）

```python
path('blog/', include('blog.urls'))
# 全局urls下收到以 blog/ 路径开头的就把blog/后的路径分发到 blog 目录下的 urls 文件内。此时blog/后是空的代表是根目录
```

```python 
1. Import the include() function: from django.urls import include, path
2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
```

#### （3）路由转发

有时候上面的内置的url转换器并不能满足我们的需求，因此django给我们提供了一个接口可以让我们自己定义自己的url转换器。

就是把urls内的路径正则拿出来单独匹配

```python
from django.urls import register_converter
from django.shortcuts import HttpResponse
# 自定义路由转换器
class MobileConverter(object):
    regex = "1[3-9]\d{9}"                             # 这里定义正则规则
    def to_python(self,value):
        print(type(value))
        # 将匹配结果传递到视图内部时使用
        # 返回str还是int主要看需求,纯数字的可以返回int
        return value

    def to_url(self,value):
        # 将匹配结果用于反向解析传值时使用
        return value
    
# register_converter(路由转换器的类名,调用别名)
register_converter(MobileConverter,"mobile")
```

```python 
path("index/<mobile:mobile>",index)
```

```python 
def index(request,mobile):
    print(":::",type(mobile))
    return HttpResponse(f"hi,{mobile}用户")
```

#### （4）反向解析

在使用Django 项目时，一个常见的需求是获得URL 的最终形式，以用于嵌入到生成的内容中（视图中和显示给用户的URL等）或者用于处理服务器端的导航（重定向等）。人们强烈希望不要硬编码这些URL（费力、不可扩展且容易产生错误）或者设计一种与URLconf 毫不相关的专门的URL 生成机制，因为这样容易导致一定程度上产生过期的URL。

**简单说	就是给路由路径取一个别名，*在模板和视图函数内使用反向解析的别名后*，urls路由的路径变了模板那也能跟着走**

在需要URL 的地方，对于不同层级，Django 提供不同的工具用于URL 反查：

- 在模板中：使用url模板标签
- 在Python 代码中：使用from django.urls import reverse 函数。

urls.py中为url设置别名参数：

```python
from django.conf.urls import url
from . import views

urlpatterns = [
     #  |  原生路径可任意更换       | |  视图函数        |  |用name=取一个别名，模板和函数使用别名就可不理原生路径变化
    url(r'^articles/([0-9]{4})/$', views.year_archive, name='news-year-archive'), 
    #...
]
```

应用之在模板中反向解析:

**模板反向解析调用路径格式：{% url "`别名`" %}**

```html
<a href="{% url 'news-year-archive' 2012 %}">2012 Archive</a>
<a href="/articles/2012/">2012 Archive</a>
```

应用之在py文本中反向解析:

视图函数路径的反向解析：先导入`reverse`；生成路径变量调用：`path=reverse("别名")`

```python
from django.shortcuts import redirect
from django.urls import reverse

def redirect_to_year(request):
    year = 2006
    reverse_path=reverse('news-year-archive', args=(year,))
    return redirect(reverse_path)  # 等效 redirect("/articles/2006/")
```



# 四、视图

django的视图主要有2种,分别是**函数视图**和**类视图**.现在刚开始学习django,我们先学习函数视图(FBV),后面再学习类视图[CBV].

## 1、请求方式

web项目运行在http协议下,默认肯定也支持用户通过不同的http请求发送数据来。django支持让客户端只能通过指定的Http请求来访问到项目的视图

`home/views.py`,代码:

```python
# 让用户发送POST才能访问的内容
from django.views.decorators.http import require_http_methods
@require_http_methods(["POST"])
def login(request):
    return HttpResponse("登录成功！")
```

路由绑定，`demo/urls.py`,代码:

```python
from django.contrib import admin
from django.urls import path
from home.views import index
urlpatterns = [
    path('admin/', admin.site.urls),
    path("index", index),
    path("login", login),
]
```

通过浏览器，访问效果`http://127.0.0.1:8090/login`:

![image-20210723213148400](assets/image-20210723213148400.png)





## 2、请求对象

#### HttpRequest

django将请求报文中的请求行、首部信息、内容主体封装成 request 类中的属性。 除了特殊说明的之外，其他均为只读的。

##### 属性方法

HttpRequest对象包含当前请求URL的一些信息：

| **属性**      | **描述**                                                     |
| ------------- | ------------------------------------------------------------ |
| path          | 请求页面的全路径,不包括域名—例如, "/hello/"。                |
| method        | 请求中使用的HTTP方法的字符串表示。全大写表示。例如:if request.method == 'GET':   do_something() elif request.method == 'POST':   do_something_else() |
| GET           | 包含所有HTTP GET参数的类字典对象。参见QueryDict 文档。       |
| POST          | 包含所有HTTP POST参数的类字典对象。参见QueryDict 文档。服务器收到空的POST请求的情况也是有可能发生的。也就是说，表单form通过HTTP POST方法提交请求，但是表单中可以没有数据。因此，不能使用语句if request.POST来判断是否使用HTTP POST方法；应该使用if request.method == "POST" (参见本表的method属性)。注意: POST不包括file-upload信息。参见FILES属性。 |
| REQUEST       | 为了方便，该属性是POST和GET属性的集合体，但是有特殊性，先查找POST属性，然后再查找GET属性。借鉴PHP's $_REQUEST。例如，如果GET = {"name": "john"} 和POST = {"age": '34'},则 REQUEST["name"] 的值是"john", REQUEST["age"]的值是"34".强烈建议使用GET and POST,因为这两个属性更加显式化，写出的代码也更易理解。 |
| COOKIES       | 包含所有cookies的标准Python字典对象。Keys和values都是字符串。 |
| FILES         | 包含所有上传文件的类字典对象。FILES中的每个Key都是<input type="file" name="" />标签中name属性的值. FILES中的每个value 同时也是一个标准Python字典对象，包含下面三个Keys:filename: 上传文件名,用Python字符串表示content-type: 上传文件的Content typecontent: 上传文件的原始内容注意：只有在请求方法是POST，并且请求页面中<form>有enctype="multipart/form-data"属性时FILES才拥有数据。否则，FILES 是一个空字典。 |
| META          | 包含所有可用HTTP头部信息的字典。 例如:CONTENT_LENGTHCONTENT_TYPEQUERY_STRING: 未解析的原始查询字符串REMOTE_ADDR: 客户端IP地址REMOTE_HOST: 客户端主机名SERVER_NAME: 服务器主机名SERVER_PORT: 服务器端口META 中这些头加上前缀 **HTTP_** 为 Key, 冒号(:)后面的为 Value， 例如:HTTP_ACCEPT_ENCODINGHTTP_ACCEPT_LANGUAGEHTTP_HOST: 客户发送的HTTP主机头信息HTTP_REFERER: referring页HTTP_USER_AGENT: 客户端的user-agent字符串HTTP_X_BENDER: X-Bender头信息 |
| user          | 是一个django.contrib.auth.models.User 对象，代表当前登录的用户。如果访问用户当前没有登录，user将被初始化为django.contrib.auth.models.AnonymousUser的实例。你可以通过user的is_authenticated()方法来辨别用户是否登录：`if request.user.is_authenticated():    # Do something for logged-in users. else:    # Do something for anonymous users. `只有激活Django中的AuthenticationMiddleware时该属性才可用 |
| session       | 唯一可读写的属性，代表当前会话的字典对象。只有激活Django中的session支持时该属性才可用。 |
| raw_post_data | 原始HTTP POST数据，未解析过。 高级处理时会有用处。           |

Request对象也有一些有用的方法：

| 方法             | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| __getitem__(key) | 返回GET/POST的键值,先取POST,后取GET。如果键不存在抛出 KeyError。  这是我们可以使用字典语法访问HttpRequest对象。  例如,request["foo"]等同于先request.POST["foo"] 然后 request.GET["foo"]的操作。 |
| has_key()        | 检查request.GET or request.POST中是否包含参数指定的Key。     |
| get_full_path()  | 返回包含查询字符串的请求路径。例如， "/music/bands/the_beatles/?print=true" |
| is_secure()      | 如果请求是安全的，返回True，就是说，发出的是HTTPS请求。      |



#### QueryDict对象

##### 创建QueryDict对象

```python
from django.http import QueryDict

 new_query_dict = QueryDict(mutable=True)  	# 创建的对象可使用QueryDict对象的方法
 new_query_dict['key'] = "value"     
```



在HttpRequest对象中, GET和POST属性是django.http.QueryDict类的实例。

QueryDict类似字典的自定义类，用来处理单键对应多值的情况。

##### 属性方法

QueryDict实现所有标准的词典方法。还包括一些特有的方法：

| **方法**    | **描述**                                                     |
| :---------- | :----------------------------------------------------------- |
| __getitem__ | 和标准字典的处理有一点不同，就是，如果Key对应多个Value，__getitem__()返回最后一个value。 |
| __setitem__ | 设置参数指定key的value列表(一个Python list)。注意：它只能在一个mutable QueryDict 对象上被调用(就是通过copy()产生的一个QueryDict对象的拷贝). |
| get()       | 如果key对应多个value，get()返回最后一个value。               |
| update()    | 参数可以是QueryDict，也可以是标准字典。和标准字典的update方法不同，该方法添加字典 items，而不是替换它们:`>>> q = QueryDict('a=1') >>> q = q.copy() # to make it mutable >>> q.update({'a': '2'}) >>> q.getlist('a')  ['1', '2'] >>> q['a'] # returns the last ['2'] ` |
| items()     | 和标准字典的items()方法有一点不同,该方法使用单值逻辑的__getitem__():`>>> q = QueryDict('a=1&a=2&a=3') >>> q.items() [('a', '3')] ` |
| values()    | 和标准字典的values()方法有一点不同,该方法使用单值逻辑的__getitem__(): |

此外, QueryDict也有一些方法，如下表：

| **方法**                 | **描述**                                                     |
| :----------------------- | :----------------------------------------------------------- |
| copy()                   | 返回对象的拷贝，内部实现是用Python标准库的copy.deepcopy()。该拷贝是mutable(可更改的) — 就是说，可以更改该拷贝的值。 |
| getlist(key)             | 返回和参数key对应的所有值，作为一个Python list返回。如果key不存在，则返回空list。 It's guaranteed to return a list of some sort.. |
| setlist(key,list_)       | 设置key的值为list_ (unlike __setitem__()).                   |
| appendlist(key,item)     | 添加item到和key关联的内部list.                               |
| setlistdefault(key,list) | 和setdefault有一点不同，它接受list而不是单个value作为参数。  |
| lists()                  | 和items()有一点不同, 它会返回key的所有值，作为一个list, 例如:`>>> q = QueryDict('a=1&a=2&a=3') >>> q.lists() [('a', ['1', '2', '3'])] ` |
| urlencode()              | 返回一个以查询字符串格式进行格式化后的字符串(例如："a=2&b=3&b=5")。 |









#### 1 获取请求方式

```python 
request.method  # 获取到浏览器发送的请示方式是什么
# POST
```

####  2 POST请求时获取数据方式

post数据在请求体位置

POST  # 一个类似于字典的对象，如果请求中包含表单数据，则将这些数据封装成 QueryDict 对象。

键值对的值是多个的时候,比如checkbox类型的input标签，select标签，需要用：         		 request.POST.getlist("hobby")

```python
request.body   # 数据格式是 urlencoded 和json者都行 取出是原生的未处理的字符串
request.POST   # 只有数据格式是 urlencoded才能取 取出的是字典键对一个列表  {"键":["值"]}

user = request.POST.get("user")   			# 拿到字典直接用get方法取值，会直接取到列表的最后一个值

hobby = request.POST.getlist("hobby")       # 用getlist取值会获取到列表
```

#### 3 GET请求时获取数据方式

get没有请求体，请求数据是放在请求行的路径后面的，一个类似于字典的对象，包含 HTTP GET 的所有参数。

```python
request.GET    # <QueryDict: {'a': ['1'], 'b': ['2']}>,直接拿到字典
```

#### 4 获取请求路径

```python
request.path               # /users       只获取纯路径 表示请求的路径组件（不含get参数）
request.get_full_path()    # /users?a=1   获取路径后的所有 含参数路径
```

####  5 取请求头数据

```python
request.META                           # 一个标准的Python 字典，包含所有的HTTP 首部。具体的头部信息取决于客户端和服务器
request.META.get("HTTP_HOST")          #用get（键）取值
```









## 4.3、响应对象

> 响应对象主要有三种形式：
>
> - HttpResponse()
> - render()
> - redirect()

#### HttpResponse()

Django服务器接收到客户端发送过来的请求后，会将提交上来的这些数据封装成一个 HTTPRequest 对象传给视图函数。那么视图函数在处理完相关的逻辑后，也需要返回一个响应给浏览器。而这个响应，我们必须返回 HttpResponseBase 或者他的子类的对象。而 HttpResponse 则是 HttpResponseBase 用得最多的子类。

常用属性： 

> 1. content：返回的内容。
> 2. status：返回的HTTP响应状态码。
> 3. content_type：返回的数据的MIME类型，默认为 text/html 。浏览器会根据这个属性，来显示数据。如果是 text/html ，那么就会解析这个字符串，如果 text/plain ，那么就会显示一个纯文本。
> 4. 设置响应头： response['X-Access-Token'] = 'xxxx' 。

JsonResponse类：

用来对象 dump 成 json 字符串，然后返回将 json 字符串封装成 Response 对象返回给浏览器。并且他的 Content-Type 是 application/json 。示例代码如下：

`````python
from django.http import JsonResponse

def index(request):
    
    return JsonResponse({"title":"三国演义","price":199})
`````

> 默认情况下 JsonResponse 只能对字典进行 dump ，如果想要对非字典的数据进行 dump ，那么需要给 JsonResponse 传递一个 safe=False 参数。示例代码如下：

#### render()

```python
render(request, template_name[, context]）
#结合一个给定的模板和一个给定的上下文字典，并返回一个渲染后的 HttpResponse 对象。
```

参数：

```java
 /*
 request： 用于生成响应的请求对象。
 template_name：要使用的模板的完整名称，可选的参数
 context：添加到模板上下文的一个字典,
          默认是一个空字典。如果字典中的某个值是可调用的，视图将在渲染模板之前调用它。
          */
```

render方法就是将一个模板页面中的模板语法进行渲染，最终渲染成一个html页面作为响应体。

#### redirect方法

当您使用Django框架构建Python Web应用程序时，您在某些时候必须将用户从一个URL重定向到另一个URL，

通过redirect方法实现重定向。客户端会发起二次请求

参数可以是:

- 一个绝对的或相对的URL, 将原封不动的作为重定向的位置.
- 一个url的别名:　可以使用reverse来反向解析url

传递要重定向到的一个具体的网址

```python
def my_view(request):
    ...
    return redirect("/some/url/")
```

当然也可以是一个完整的网址

```python
def my_view(request):
    ...
    return redirect("http://www.baidu.com")
```

传递一个视图的名称

```python
def my_view(request):
    ...
    return redirect(reverse("url的别名"))　
```

![image-20210812135707162](assets/image-20210812135707162.png)

小知识：APPEND_SLASH：

APPEND_SLASH的实现就是基于redirect，当用户的url地址结尾少了个`/`，djauno就会重定向一个补全了/的地址给浏览重发。

APPEND_SLASH默认是True，如果不想自动补全就到配置文件settings.py文件修改成False

```python
# 项目目录下/settings.py
APPEND_SLASH = False
```







# 五、模板语法

模板引擎是一种可以让开发者把服务端数据填充到html网页中完成渲染效果的技术。它实现了把前端代码和服务端代码分离的作用，让项目中的业务逻辑代码和数据表现代码分离，让前端开发者和服务端开发者可以更好的完成协同开发。

> 静态网页：页面上的数据都是写死的，万年不变
>
> 动态网页：页面上的数据是从后端动态获取的（比如后端获取当前时间；后端获取数据库数据然后传递给前端页面）

Django框架中内置了web开发领域非常出名的一个DjangoTemplate模板引擎（DTL）。[DTL官方文档](https://docs.djangoproject.com/zh-hans/3.2/topics/templates/)

要在django框架中使用模板引擎把视图中的数据更好的展示给客户端，需要完成3个步骤：

> 1.  在项目配置文件中指定保存模板文件的模板目录。一般模板目录都是设置在项目根目录或者主应用目录下。
>
> 2.  在视图中基于django提供的渲染函数绑定模板文件和需要展示的数据变量
>
> 3.  在模板目录下创建对应的模板文件，并根据模板引擎内置的模板语法，填写输出视图传递过来的数据。

### 模板的查找顺序

1. 根目录下的templates下找
2. 根目录下无就按app注册顺序的app中的templates中找



## 1 配置模板目录

当前项目根目录下创建了模板目录templates. 然后在settings.py, 模板相关配置，找到TEMPLATES配置项，填写DIRS设置模板目录。

```python
# 模板引擎配置
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
            BASE_DIR / "templates",  		# 路径拼接
        ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

### 简单案例

1 创建创建一个新的子应用 tem

```bash
python manage.py startapp tem
```

2 注册子应用

```python
# settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'tem',  						 # 开发者创建的子应用，这填写就是子应用的导包路径
]
```

3 路由分发 

```python
# urls.py
from django.contrib import admin
from django.urls import path,include
urlpatterns = [
    path('admin/', admin.site.urls),
    
    # path("路由前缀/", include("子应用目录名.路由模块"))
    path("users/", include("users.urls")),
    path("tem/", include("tem.urls")),
]
```

4 在子应用目录下创建urls.py子路由文件

```python
"""子应用路由"""
from django.urls import path, re_path
from . import views

urlpatterns = [
    path("index", views.index),
]
```

5 业务逻辑

```python
# tem.views
from django.shortcuts import render

def index(request):
	name = "hello DTL!"
    # return render(request, "模板文件路径",context={字典格式：要在客户端中展示的数据})
	return render(request, "index.html",context={"name":name})
```

6 模板文件 templates.index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>来自模板的内容</h1>
    <p>输出变量name的值：{{ name }}</p>
</body>
</html>
```





## 2 render函数内部本质

![image-20210530032914557](assets/image-20210530032914557.png)

```python 
from django.shortcuts import render
from django.template.loader import get_template
from django.http.response import HttpResponse

def index(request):
	name = "hello world!"
	# 1. 初始化模板,读取模板内容,实例化模板对象
    # get_template会从项目配置中找到模板目录，我们需要填写的参数就是补全模板文件的路径
	template = get_template("index.html")
	# 2. 识别context内容, 和模板内容里面的标记[标签]替换,针对复杂的内容,进行正则的替换
	context = {"name": name}
	content = template.render(context, request) # render中完成了变量替换成变量值的过程，这个过程使用了正则。
	print(content)
	# 3. 通过response响应对象,把替换了数据的模板内容返回给客户端
	return HttpResponse(content)
	# 上面代码的简写,直接使用 django.shortcuts.render
	 return render(request, "index.html",context={"name":name})
     return render(request,"index3.html", locals())            # locals()会把函数内的所有变量传入到模板html中
     data = {}
     data["name"] = "xiaoming"
     data["message"] = "你好！"
     return render(request,"index3.html", data)
```

> 1. DTL模板文件与普通html文件的区别在哪里？
>
>   DTL模板文件是一种带有特殊语法的HTML文件，这个HTML文件可以被Django编译，可以传递参数进去，实现数据动态化。在编译完成后，生成一个普通的HTML文件，然后发送给客户端。
>
> 2. 开发中，我们一般把开发中的文件分2种，分别是静态文件和动态文件。
>
> ```
> * 静态文件，数据保存在当前文件，不需要经过任何处理就可以展示出去。普通html文件，图片，视频，音频等这一类文件叫静态文件。
> * 动态文件，数据并不在当前文件，而是要经过服务端或其他程序进行编译转换才可以展示出去。 编译转换的过程往往就是使用正则或其他技术把文件内部具有特殊格式的变量转换成真实数据。 动态文件，一般数据会保存在第三方存储设备，如数据库中。django的模板文件，就属于动态文件。
> ```





## 3 模板语法

> 1. 变量渲染（深度查询、过滤器）
>
>    ```python
>    {{val}}
>    {{val|filter_name:参数}}
>    ```
>
> 2. 标签   
>
>    ```
>    {% tag_name %}
>    ```
>
> 3. 嵌套和继承

### 1、深度查询

> locals()把所有变量传入至index.html模板内。有列表字典变量，有对象变量。
>
> 在模板内用 变量加 `.`索引；就能取到对应索引值；字典就变量`.`键名取对应值
>
> 对于嵌套的可以：列表`.`索引`.`键；一直点到要的值

```python 
def index(request):
    name = "root"
    age = 13
    sex = True
    lve = ["swimming", "shopping", "coding", "game"]
    bookinfo = {"id": 1, "price": 9.90, "name": "python3天入门到挣扎", }
    book_list = [
        {"id": 10, "price": 9.90, "name": "python3天入门到挣扎", },
        {"id": 11, "price": 19.90, "name": "python7天入门到垂死挣扎", },
    ]
    return render(request, 'index.html', locals())
```

模板代码，`templates/index.html`：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <p>name={{ name }}</p>
    <p>{{ age }}</p>
    <p>{{ sex }}</p>
    <p>列表成员</p>
    <p>{{ lve }}</p>
    <p>{{ lve.0 }}</p>
    <p>{{ lve | last }}</p>

    <p>字典成员</p>
    <p>id={{ bookinfo.id }}</p>
    <p>price={{ bookinfo.price }}</p>
    <p>name={{ bookinfo.name }}</p>

    <p>复杂列表</p>
    <p>{{ book_list.0.name }}</p>
    <p>{{ book_list.1.name }}</p>

</body>
</html>
```

> 通过句点符号深度查询

`tem.urls`，代码：

```python
"""子应用路由"""
from django.urls import path, re_path
from . import views

urlpatterns = [
	# ....
    path("index", views.index),
]

```

### 2、内置过滤器

内置过滤器

| 过滤器          | 用法                                     | 代码                            |
| --------------- | ---------------------------------------- | ------------------------------- |
| last            | 获取列表/元组的最后一个成员              | {{liast \| last}}               |
| first           | 获取列表/元组的第一个成员                | {{list\|first}}                 |
| length          | 获取数据的长度                           | {{list \| length}}              |
| defualt         | 当变量没有值的情况下, 系统输出默认值,    | {{str\|default="默认值"}}       |
| safe            | 让系统不要对内容中的html代码进行实体转义 | {{htmlcontent\| safe}}          |
| upper           | 字母转换成大写                           | {{str \| upper}}                |
| lower           | 字母转换成小写                           | {{str \| lower}}                |
| title           | 每个单词首字母转换成大写                 | {{str \| title}}                |
| date            | 日期时间格式转换                         | `{{ value| date:"D d M Y" }}`   |
| cut             | 从内容中截取掉同样字符的内容             | {{content \| cut:"hello"}}      |
| list            | 把内容转换成列表格式                     | {{content \| list}}             |
| add             | 加法                                     | {{num\| add}}                   |
| filesizeformat  | 把文件大小的数值转换成单位表示           | {{filesize \| filesizeformat}}  |
| `join`          | 按指定字符拼接内容                       | {{list\| join("-")}}            |
| `random`        | 随机提取某个成员                         | {list \| random}}               |
| `slice`         | 按切片提取成员                           | {{list \| slice:":-2"}}         |
| `truncatechars` | 按字符长度截取内容                       | {{content \| truncatechars:30}} |
| `truncatewords` | 按单词长度截取内容                       | 同上                            |



#### 模板语法

```
{{ 变量名 | 过滤器：可选参数 }}
```

模板过滤器可以在变量被显示前修改它，过滤器使用管道字符，如下所示：

```
{{ name|lower }}
```

{{ name }} 变量被过滤器 lower 处理后，文档大写转换文本为小写。

过滤管道可以被* 套接* ，既是说，一个过滤器管道的输出又可以作为下一个管道的输入：

```
{{ my_list|first|upper }}
```

以上实例将第一个元素并将其转化为大写。

有些过滤器有参数。 过滤器的参数跟随冒号之后并且总是以双引号包含。 例如：

```
{{ bio|truncatewords:"30" }}
```

这个将显示变量 bio 的前30个词。







其他过滤器

#### **filesizeformat**

以更易读的方式显示文件的大小（即'13 KB', '4.1 MB', '102 bytes'等）。

字典返回的是键值对的数量，集合返回的是去重后的长度。

**HelloWorld/HelloWorld/views.py 文件代码：**

```python
**from** django.shortcuts **import** render

**def** runoob(request):
  num=1024
  **return** render(request, "runoob.html", {"num": num})
```

**HelloWorld/templates/runoob.html 文件代码：**

```
{{ num|filesizeformat}}
```

再次访问 http://127.0.0.1:8000/runoob，可以看到页面：

![img](https://www.runoob.com/wp-content/uploads/2015/01/Django_7.png)

#### **date**

根据给定格式对一个日期变量进行格式化。

格式 **Y-m-d H:i:s**返回 **年-月-日 小时:分钟:秒** 的格式时间。

HelloWorld/HelloWorld/views.py 文件代码：

```python
**from** django.shortcuts **import** render

**def** runoob(request):
  **import** datetime
  now  =datetime.datetime.now()
  **return** render(request, "runoob.html", {"time": now})
```

HelloWorld/templates/runoob.html 文件代码：

```html
{{ time|date:"Y-m-d" }}
```

再次访问 http://127.0.0.1:8000/runoob，可以看到页面：

![img](https://www.runoob.com/wp-content/uploads/2015/01/Django_9.png)



#### **truncatechars**

如果字符串包含的字符总个数多于指定的字符数量，那么会被截断掉后面的部分。

截断的字符串将以 **...** 结尾。

**HelloWorld/HelloWorld/views.py 文件代码：**

```python
**from** django.shortcuts **import** render

**def** runoob(request):
  views_str = "菜鸟教程"
  **return** render(request, "runoob.html", {"views_str": views_str})
```

**HelloWorld/templates/runoob.html 文件代码：**

```
{{ views_str|truncatechars:2}}
```

再访问访问 http://127.0.0.1:8000/runoob，可以看到页面：

![img](https://www.runoob.com/wp-content/uploads/2015/01/Django_10.png)





#### **safe**

将字符串标记为安全，不需要转义。

要保证 views.py 传过来的数据绝对安全，才能用 safe。

和后端 views.py 的 mark_safe 效果相同。

Django 会自动对 views.py 传到HTML文件中的标签语法进行转义，令其语义失效。加 safe 过滤器是告诉 Django 该数据是安全的，不必对其进行转义，可以让该数据语义生效。

**HelloWorld/HelloWorld/views.py 文件代码：**

```python
**from** django.shortcuts **import** render

**def** runoob(request):
  views_str = "<a href='https://www.runoob.com/'>点击跳转</a>"	
  **return** render(request, "runoob.html", {"views_str": views_str})
```

**HelloWorld/templates/runoob.html 文件代码：**

```
{{ views_str|safe }}
```

再访问访问 http://127.0.0.1:8000/runoob，可以看到页面：

![img](https://www.runoob.com/wp-content/uploads/2015/01/Django_1.gif)













### 3 自定标签和过滤器

#### 1、在应用目录下创建 **templatetags** 目录(与 templates 目录同级，目录名只能是 templatetags)。

```
HelloWorld/
|-- HelloWorld
|   |-- __init__.py
|   |-- __init__.pyc
|   |-- settings.py
...
|-- manage.py
`-- templatetags
`-- templates
```

#### 2、在 templatetags 目录下创建任意 py 文件，如：**my_tags.py**。

#### 3、my_tags.py 文件代码如下：

```python
from django import template

register = template.Library()   #register的名字是固定的,不可改变
```

修改 settings.py 文件的 TEMPLATES 选项配置，添加 libraries 配置：

**settings.py 配置文件**

```python
...
TEMPLATES = [
  {
    'BACKEND': 'django.template.backends.django.DjangoTemplates',
    'DIRS': [BASE_DIR, "/templates",],
    'APP_DIRS': True,
    'OPTIONS': {
      'context_processors': [
        'django.template.context_processors.debug',
        'django.template.context_processors.request',
        'django.contrib.auth.context_processors.auth',
        'django.contrib.messages.context_processors.messages',
      ],
      "libraries":{              # 添加这边三行配置
        'my_tags':'templatetags.my_tags'  # 添加这边三行配置     
      }                    # 添加这边三行配置
    },
  },
]
...
```



#### 4、利用装饰器 @register.filter 自定义过滤器。

**注意：**装饰器的参数最多只能有 2 个。

```python
@register.filter
def my_filter(v1, v2):
    return v1 * v2
```

虽然官方已经提供了许多内置的过滤器给开发者,但是很明显,还是会有存在不足的时候。例如:希望输出用户的手机号码时, 13912345678 ---->>  `139*****678`，这时我们就需要自定义过滤器。要声明自定义过滤器并且能在模板中正常使用,需要完成2个前置的工作:

```python 
# 1. 当前使用和声明过滤器的子应用必须在setting.py配置文件中的INSTALLED_APPS中注册了!!!
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'home',
]

```

```python
# home.templatetags.my_filters.py代码:
# 2. 自定义过滤器函数必须被 template.register进行装饰使用.而且过滤器函数所在的模块必须在templatetags包里面保存
# 在home子应用下创建  templatetags  包[必须包含__init__.py], 在包目录下创建任意py文件

from django import template

register = template.Library()
@register.filter("mobile") 				# 自定义过滤器
def mobile(content):
	return content[:3]+"*****"+content[-3:]

```

```python
# home.views.py,代码:
# 3. 在需要使用的模板文件中顶部使用load标签加载过滤器文件my_filters.py并调用自定义过滤器

def index(request):
    
	moblie_number = "13312345678"
	return render(request,"index2.html",locals())

```

templates/index2.html

```html
{% load my_filters %}             #  my_filters是自定义过滤器的py文件
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {{ moblie_number| mobile }}   # mobile 是自定义的过滤器名
</body>
</html>
```







#### 5、利用装饰器 @register.simple_tag 自定义标签。

```python
@register.simple_tag
def my_tag1(v1, v2, v3):
    return v1 * v2 * v3
```

#### 6、在使用自定义标签和过滤器前，要在 html 文件 body 的最上方中导入该 py 文件。

```
{% load my_tags %}
```

#### 7、在 HTML 中使用自定义过滤器。

```
{{ 11|my_filter:22 }}
```

#### 8、在 HTML 中使用自定义标签。

```
{% my_tag1 11 22 33 %}
```

#### 9、语义化标签

在该 py 文件中导入 mark_safe。

```
from django.utils.safestring import mark_safe
```

定义标签时，用上 mark_safe 方法，令标签语义化，相当于 jQuery 中的 html() 方法。

和前端HTML文件中的过滤器 safe 效果一样。

```python
@register.simple_tag
def my_html(v1, v2):
    temp_html = "<input type='text' id='%s' class='%s' />" %(v1, v2)
    return mark_safe(temp_html)
```

在HTML中使用该自定义标签，在页面中动态创建标签。

```
{% my_html "zzz" "xxx" %}
```







### 4、if  及for 标签

#### （1）if 标签

  哪个条件成立就显示哪条标签

```python
 # 文件 模板.html
    {% if user_lve == lve.0 %}                   # 开头
        <p>那么巧，你喜欢游泳，海里也能见到你~</p>
    {% elif user_lve == lve.1 %}
        <p>那么巧，你也来收快递呀？~</p>
    {% elif user_lve == lve.2 %}
        <p>那么巧，你也在老男孩？</p>
    {% else %}
        <p>看来我们没有缘分~</p>
    {% endif %}                                    #结尾
```

视图代码,tem.views.py:

```python
def index(request):
    name = "xiaoming"
    age = 19
    sex = True
    lve = ["swimming", "shopping", "coding", "game"]
    user_lve = "sleep"
    bookinfo = {"id": 1, "price": 9.90, "name": "python3天入门到挣扎", }
    book_list = [
        {"id": 10, "price": 9.90, "name": "python3天入门到挣扎", },
        {"id": 11, "price": 19.90, "name": "python7天入门到垂死挣扎", },
    ]
    return render(request, 'index.html', locals())
```

模板代码,templates/index.html，代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
{# 来自django模板引擎的注释~~~~ #}
{% comment %}
多行注释，comment中的所有内容全部都不会被显示出去
{% endcomment %}

{#    {% if age < 18 %}#}
{#        <p>你还没成年，不能访问我的网站！</p>#}
{#    {% endif %}#}
{##}
{#    {% if name == "root" %}#}
{#        <p>超级用户，欢迎回家！</p>#}
{#    {% else %}#}
{#        <p>{{ name }},你好，欢迎来到xx网站！</p>#}
{#    {% endif %}#}


    {% if user_lve == lve.0 %}
        <p>那么巧，你喜欢游泳，海里也能见到你~</p>
    {% elif user_lve == lve.1 %}
        <p>那么巧，你也来收快递呀？~</p>
    {% elif user_lve == lve.2 %}
        <p>那么巧，你也在老男孩？</p>
    {% else %}
        <p>看来我们没有缘分~</p>
    {% endif %}
</body>
</html>
```

路由代码：

```python
"""子应用路由"""
from django.urls import path, re_path
from . import views

urlpatterns = [
	# ....
    path("index", views.index),
]
```

#### （2）for标签

```python
{% for book in book_list1 %}   # 循环列表的每个对象  开头
    <tr>
       <td>{{ book.id }}</td>
       <td>{{ book.name }}</td>
       <td>{{ book.price }}</td>
    </tr>#}
{% endfor %}                    # 结尾
```



视图代码, home.views.py:

```python
def index7(request):
    book_list1 = [
        {"id": 11, "name": "python基础入门", "price": 130.00},
        {"id": 17, "name": "Go基础入门", "price": 230.00},
        {"id": 23, "name": "PHP基础入门", "price": 330.00},
        {"id": 44, "name": "Java基础入门", "price": 730.00},
        {"id": 51, "name": "C++基础入门", "price": 300.00},
        {"id": 56, "name": "C#基础入门", "price": 100.00},
        {"id": 57, "name": "前端基础入门", "price": 380.00},
    ]
    return render(request, 'index.html', locals())
```

template/index.html，代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <table width="800" align="center" border="1">
        <tr>
            <td>序号</td>
            <td>id</td>
            <td>标题</td>
            <td>价格</td>
        </tr>
        {# 多行编辑，alt+鼠标键，alt不要松开，左键点击要编辑的每一行 #}
{#        {% for book in book_list1 %}#}
{#            <tr>#}
{#                <td>{{ book.id }}</td>#}
{#                <td>{{ book.name }}</td>#}
{#                <td>{{ book.price }}</td>#}
{#            </tr>#}
{#        {% endfor %}#}

{# 建议不要直接使用for循环一维字典，此处使用仅仅展示for嵌套for而已 #}
{#        {% for book in book_list1 %}#}
{#            <tr>#}
{#                {% for field,value in book.items %}#}
{#                <td>{{ field }} == {{ value }}</td>#}
{#                {% endfor %}#}
{#            </tr>#}
{#        {% endfor %}#}

{#        {% for book in book_list1 %}#}
{#            <tr>#}
{#                <td>{{ book.id }}</td>#}
{#                <td>{{ book.name }}</td>#}
{#                {% if book.price > 200 %}#}
{#                    <td bgcolor="#ff7f50">{{ book.price }}</td>#}
{#                {% else %}#}
{#                    <td>{{ book.price }}</td>#}
{#                {% endif %}#}
{#            </tr>#}
{#        {% endfor %}#}

        {# 逆向循环数据 #}
{#        {% for book in book_list1 reversed %}#}
{#            <tr>#}
{#                <td>{{ book.id }}</td>#}
{#                <td>{{ book.name }}</td>#}
{#                {% if book.price > 200 %}#}
{#                    <td bgcolor="#ff7f50">{{ book.price }}</td>#}
{#                {% else %}#}
{#                    <td>{{ book.price }}</td>#}
{#                {% endif %}#}
{#            </tr>#}
{#        {% endfor %}#}

        {% for book in book_list1 %}
            <tr>
{#                <td>{{ forloop.counter }}</td>#}
{#                <td>{{ forloop.counter0 }}</td>#}
{#                <td>{{ forloop.revcounter }}</td>#}
{#                <td>{{ forloop.revcounter0 }}</td>#}
{#                <td>{{ forloop.first }}</td>#}
                <td>{{ forloop.last }}</td>
                <td>{{ book.id }}</td>
                <td>{{ book.name }}</td>
                {% if book.price > 200 %}
                    <td bgcolor="#ff7f50">{{ book.price }}</td>
                {% else %}
                    <td>{{ book.price }}</td>
                {% endif %}
            </tr>
        {% endfor %}

    </table>
</body>
</html>
```

路由代码：

```python
"""子应用路由"""
from django.urls import path, re_path
from . import views

urlpatterns = [
	# ....
    path("index", views.index),
]

```

循环中, 模板引擎提供的forloop对象,用于给开发者获取循环次数或者判断循环过程的.

| 属性                | 描述                                      |
| ------------------- | ----------------------------------------- |
| forloop.counter     | 显示循环的次数,从1开始                    |
| forloop.counter0    | 显示循环的次数,从0开始                    |
| forloop.revcounter0 | 倒数显示循环的次数,从0开始                |
| forloop.revcounter  | 倒数显示循环的次数,从1开始                |
| forloop.first       | 判断如果本次是循环的第一次,则结果为True   |
| forloop.last        | 判断如果本次是循环的最后一次,则结果为True |
| forloop.parentloop  | 在嵌套循环中，指向当前循环的上级循环      |



### 5、模板嵌套继承

##### 模板继承

模板可以用继承的方式来实现复用，减少冗余内容。

网页的头部和尾部内容一般都是一致的，我们就可以通过模板继承来实现复用。

父模板用于放置可重复利用的内容，子模板继承父模板的内容，并放置自己的内容。

##### 父模板

**标签 block...endblock:** 父模板中的预留区域，该区域留给子模板填充差异性的内容，不同预留区域名字不能相同。

```
{% block 名称 %} 
预留给子模板的区域，可以设置设置默认内容
{% endblock 名称 %}
```

##### 子模板

子模板使用标签 extends 继承父模板：

```
{% extends "父模板路径"%} 
```

子模板如果没有设置父模板预留区域的内容，则使用在父模板设置的默认内容，当然也可以都不设置，就为空。

子模板设置父模板预留区域的内容：

```
{ % block 名称 % }
内容 
{% endblock 名称 %}
```

接下来我们先创建之前项目的 templates 目录中添加 base.html 文件，代码如下：

**HelloWorld/templates/base.html 文件代码：**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
    <h1>Hello World!</h1>
    <p>菜鸟教程 Django 测试。</p>
    {% block mainbody %}
       <p>original</p>
    {% endblock %}
</body>
</html>
```

以上代码中，名为 mainbody 的 block 标签是可以被继承者们替换掉的部分。

所有的 {% block %} 标签告诉模板引擎，子模板可以重载这些部分。

runoob.html 中继承 base.html，并替换特定 block，runoob.html 修改后的代码如下：

**HelloWorld/templates/runoob.html 文件代码：**

```html
{%extends "base.html" %}
 
{% block mainbody %}
<p>继承了 base.html 文件</p>
{% endblock %}
```

第一行代码说明 runoob.html 继承了 base.html 文件。可以看到，这里相同名字的 block 标签用以替换 base.html 的相应 block。

重新访问地址 http://127.0.0.1:8000/runoob，输出结果如下：

![img](https://www.runoob.com/wp-content/uploads/2015/01/F54E0EF3-2E76-4B3E-B1DA-1541EDCB5CD2.jpg)





传统的模板分离技术,依靠{% include "模板文件名"%}实现,这种方式,虽然达到了页面代码复用的效果,但是由此也会带来大量的碎片化模板,导致维护模板的成本上升.因此, Django框架中除了提供这种模板分离技术以外,还并行的提供了 模板继承给开发者.

````python
{% include "模板文件名"%}  # 模板嵌入

{% extends "base.html" %} # 模板继承 
````

#### (1)  继承父模板

> {% extends "base.html" %}

视图, home.views.py代码:

```python
def index(request):
	"""模板继承"""
	return render(request,"index.html",locals())
```

子模板, templates/index.html

在字模板顶部引用

```html
{% extends "base.html" %}           
```

父模板, templates/base.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>base.html的头部</h1>
    <h1>base.html的内容</h1>
    <h1>base.html的脚部</h1>
</body>
</html>
```





#### \(2) 自定义父模板内容

```
如果你在模版中使用 `{% extends %}` 标签，它必须是模版中的第一个标签。其他的任何情况下，模版继承都将无法工作。

在base模版中设置越多的 `{% block %}` 标签越好。请记住，子模版不必定义全部父模版中的blocks，所以，你可以在大多数blocks中填充合理的默认内容，然后，只定义你需要的那一个。多一点钩子总比少一点好。

为了更好的可读性，你也可以给你的 `{% endblock %}` 标签一个 *名字* 。例如：`{``%` `block content``%``}``...``{``%` `endblock content``%``},`在大型模版中，这个方法帮你清楚的看到哪一个　 `{% block %}` 标签被关闭了。

不能在一个模版中定义多个相同名字的 `block` 标签。
```

用法

1 `父模板base.html`： 在父模板任意位置加入  `{%block %}    {%endblock%}`标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}{% endblock  %}</title>
</head>
<body>
    <h1>base.html的头部</h1>
    {% block content %}                   {# 1 开头 设置给子模板自定义的区域 #}
    <h1>base.html的内容</h1>
	{% endblock %}                       {# 结尾 中间的默认内容，子模块看需求要不要#}
    <h1>base.html的脚部</h1>
</body>
</html>
```

2 `子模板index.html:`：在子模板内先`{% extends "base.html" %}`继承父模板，然后在`{%block %}  独立内容  {%endblock%}`标签内设置任意内容就会映射到父模板设置此标签的位置

```python
{% extends "base.html" %}

{% block title %}index3的标题{% endblock  %}
{% block content %}
    {{ block.super }}                          {# 读取到父级模板同名block标签的内容加进来 #}
    <h1>index3.html的独立内容</h1>				{# 这添加自己的内容 #}
    {{ block.super }}
{% endblock %}
```

```python
{%block %}  独立内容  {%endblock%}

{{block.super}}                                      ：读取父模板默认的内容到子标签，不加父标签默认内容就会给覆盖
```





### 6 函数的模板渲染方法

自定义不同的数据到父模板，可用于多级菜单

1 在子app下创建一个py文件

```python
# rbac.py
from django.template import Library					# 1.1 导入此模块
register = Library()					   		   # 1.2 实例Library()得到register对象

@register.inclusion_tag('rbac/static_menu.html')     # 1.3 用 对象.inclusion_tag("子模板路径")当装饰器装饰函数
def static_menu(request):						   # 1.4 装饰器下创建相应函数
    # 获取session数据传入子模板
    menu_list = request.session["xxx"]
    return {'menu_list': menu_list}
```

2  创建一个子模板文件，给装饰器引用，模板内可以引用上面传入的数据

```html
<!--   static_menu.html      -->

<div class="static-menu">
    {% for item in menu_list %}
        <a href="{{ item.url }}">
            <span class="icon-wrap"><i class="fa {{ item.icon }}"></i></span> {{ item.title }}</a>
    {% endfor %}
</div>
```

3 在父模板中引入`rbac.py`文件并调用创建的函数的子模板渲染至父模板

```html
<!--   父模板.html      -->

{% load rbac %}						<!--  3.1 在顶部先引入rbac.py  -->



{% static_menu request %}			<!--  3.2 在任意位置调用创建的函数，还要传入 request 给static_menu调用 -->
```

**调用后父模板的对应位置就会渲染出子模板的内容**







## 4 静态文件

#### 配置静态文件

1、在项目根目录下创建 statics 目录。

![img](https://www.runoob.com/wp-content/uploads/2015/01/64DE342B-BBB8-424F-ADE7-B93EA124FDCD.jpg)

2、在 settings 文件的最下方配置添加以下配置：

```
STATIC_URL = '/static/' # 别名 
STATICFILES_DIRS = [ 
    os.path.join(BASE_DIR, "statics"), 
]
```

![img](https://www.runoob.com/wp-content/uploads/2015/01/Django_18.png)

3、在 statics 目录下创建 css 目录，js 目录，images 目录，plugins 目录， 分别放 css文件，js文件，图片，插件。

4、把 bootstrap 框架放入插件目录 plugins。

5、在 HTML 文件的 head 标签中引入 bootstrap。

**注意：**此时引用路径中的要用配置文件中的别名 static，而不是目录 statics。

```
<link rel="stylesheet" href="/static/plugins/bootstrap-3.3.7/dist/css/bootstrap.css">
```

在模板中使用需要加入 **{% load static %}** 代码，以下实例我们从静态目录中引入图片。

**HelloWorld/HelloWorld/views.py 文件代码：**

```python
**from** django.shortcuts **import** render

**def** runoob(request):
  name ="菜鸟教程"
  **return** render(request, "runoob.html", {"name": name})
```



HelloWorld/templates/runoob.html 文件代码：

```html
{% load static %} 
{{name}}<img src="{% static 'images/runoob-logo.png' %}" alt="runoob-logo">
```

再访问访问 http://127.0.0.1:8000/runoob，可以看到页面：

![img](https://www.runoob.com/wp-content/uploads/2015/01/87493622-D5C4-4883-8229-0813B608BB4A.jpg)











开发中在开启了debug模式时，django可以通过配置，允许用户通过对应的url地址访问django的静态文件。

setting.py，代码：

```python
STATIC_ROOT = BASE_DIR / 'static'
STATIC_URL = '/static/'   				# django模板中，可以引用{{STATIC_URL}}变量避免把路径写死。
```

#### 模板引入文件

```python
# xx.html
{% load static  %}			# 在顶部引入 static 文件夹
{% load rbac %}				# 也可引入rbac.py文件


						  # 使用时 {% static '文件路径' %} 就可调用
<script src="{% static 'js/jquery-3.3.1.min.js' %} "></script>
<script src="{% static 'plugins/bootstrap/js/bootstrap.js' %} "></script>
<script src="{% static 'rbac/js/rbac.js' %} "></script>
```

总路由，urls.py，代码：

```python
from django.views.static import serve as serve_static
urlpatterns = [
    path('admin/', admin.site.urls), 
    # 对外提供访问静态文件的路由，serve_static 是django提供静态访问支持的映射类。依靠它，客户端才能访问到django的静态文件。
    path(r'static/<path:path>', serve_static, {'document_root': settings.STATIC_ROOT},),
]
```

注意：项目上线以后，关闭debug模式时，django默认是不提供静态文件的访问支持，项目部署的时候，我们会通过收集静态文件使用nginx这种web服务器来提供静态文件的访问支持。







# 六、模型层（ORM）

Django中内嵌了ORM框架，不需要直接编写SQL语句进行数据库操作，而是通过定义模型类，操作模型类来完成对数据库中表的增删改查和创建等操作。

![image-20211008150813304](assets/image-20211008150813304.png)

> O是object，也就**类对象**的意思。
>
> R是relation，翻译成中文是关系，也就是关系数据库中**数据表**的意思。
>
> M是mapping，是**映射**的意思。

映射：

> 类：sql语句table表
>
> 类成员变量：table表中的字段、类型和约束
>
> 类对象：sql表的表记录

ORM的优点

> - 数据模型类都在一个地方定义，更容易更新和维护，也利于重用代码。
>
> - ORM 有现成的工具，很多功能都可以自动完成，比如数据消除、预处理、事务等等。
>
> - 它迫使你使用 MVC 架构，ORM 就是天然的 Model，最终使代码更清晰。
>
> - 基于 ORM 的业务代码比较简单，代码量少，语义性好，容易理解。
>
> - 新手对于复杂业务容易写出性能不佳的 SQL,有了ORM不必编写复杂的SQL语句, 只需要通过操作模型对象即可同步修改数据表中的数据.
>
> - 开发中应用ORM将来如果要切换数据库.只需要切换ORM底层对接数据库的驱动【修改配置文件的连接地址即可】

ORM 也有缺点

> - ORM 库不是轻量级工具，需要花很多精力学习和设置，甚至不同的框架，会存在不同操作的ORM。
> - 对于复杂的业务查询，ORM表达起来比原生的SQL要更加困难和复杂。
> - ORM操作数据库的性能要比使用原生的SQL差。
> - ORM 抽象掉了数据库层，开发者无法了解底层的数据库操作，也无法定制一些特殊的 SQL。【自己使用pymysql另外操作即可，用了ORM并不表示当前项目不能使用别的数据库操作工具了。】

我们可以通过以下步骤来使用django的数据库操作

```text
1. 配置数据库连接信息
2. 在models.py中定义模型类
3. 生成数据库迁移文件并执行迁文件[注意：数据迁移是一个独立的功能，这个功能在其他web框架未必和ORM一块的]
4. 通过模型类对象提供的方法或属性完成数据表的增删改查操作
```

## 1 配置数据库连接

在settings.py中保存了数据库的连接配置信息，Django默认初始配置使用**sqlite**数据库。

1. 使用**MySQL**数据库首先需要安装驱动程序

   ```shell
   pip install PyMySQL
   ```

2. 在Django的工程同名子目录的`__init__`.py文件中添加如下语句

   ```python
   from pymysql import install_as_MySQLdb
   install_as_MySQLdb() # 让pymysql以MySQLDB的运行模式和Django的ORM对接运行
   ```

   作用是让Django的ORM能以mysqldb的方式来调用PyMySQL。

3. 修改**DATABASES**配置信息

   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.mysql',
           'HOST': '127.0.0.1',  # 数据库主机
           'PORT': 3306,  # 数据库端口
           'USER': 'root',  # 数据库用户名
           'PASSWORD': '123',  # 数据库用户密码
           'NAME': 'student'  # 数据库名字
       }
   }
   ```

4. 在MySQL中创建数据库

   ```mysql
   create database student; # mysql8.0默认就是utf8mb4;
   create database student default charset=utf8mb4; # mysql8.0之前的版本
   ```

5. 注意3: 如果想打印orm转换过程中的sql，需要在settings中进行如下配置：

   ```python
   LOGGING = {
       'version': 1,
       'disable_existing_loggers': False,
       'handlers': {
           'console':{
               'level':'DEBUG',
               'class':'logging.StreamHandler',
           },
       },
       'loggers': {
           'django.db.backends': {
               'handlers': ['console'],
               'propagate': True,
               'level':'DEBUG',
           },
       }
   }　　
   ```



## 2 定义模型类

定义模型类

> - 模型类被定义在"子应用/models.py"文件中。
> - 模型类必须直接或者间接继承自django.db.models.Model类。



settings.py，代码：设去置中确认是否已经引入了当前应用

```python
INSTALLED_APPS = [
	# ...
    'student',
]
```



在models.py 文件中定义模型类。

```python
from django.db import models
from datetime import datetime

# 模型类必须要直接或者间接继承于 models.Model
class BaseModel(models.Model):
	"""公共模型[公共方法和公共字段]"""
	# created_time = models.IntegerField(default=0, verbose_name="创建时间")
	created_time = models.DateTimeField(auto_now_add=True, verbose_name="创建时间")
	# auto_now_add 当数据添加时设置当前时间为默认值
	# auto_now= 当数据添加/更新时, 设置当前时间为默认值
	updated_time = models.DateTimeField(auto_now=True)
	class Meta(object):
		abstract = True # 设置当前模型为抽象模型, 当系统运行时, 不会认为这是一个数据表对应的模型.

class Student(BaseModel):
	"""Student模型类"""
	#1. 字段[数据库表字段对应]
	SEX_CHOICES = (
		(0,"女"),
		(1,"男"),
		(2,"保密"),
	)

	# 字段名 = models.数据类型(约束选项1,约束选项2, verbose_name="注释")
	# SQL: id bigint primary_key auto_increment not null comment="主键",
    # id = models.AutoField(primary_key=True, null=False, verbose_name="主键") # django会自动在创建数据表的时候生成id主键/还设置了一个调用别名 pk

    # SQL: name varchar(20) not null comment="姓名"
    # SQL: key(name),
    name = models.CharField(max_length=20, db_index=True, verbose_name="姓名" )

    # SQL: age smallint not null comment="年龄"
    age = models.SmallIntegerField(verbose_name="年龄")

    # SQL: sex tinyint not null comment="性别"
    # sex = models.BooleanField(verbose_name="性别")
    sex = models.SmallIntegerField(choices=SEX_CHOICES, default=2)

    # SQL: class varchar(5) not null comment="班级"
    # SQL: key(class)
    classmate = models.CharField(db_column="class", max_length=5, db_index=True, verbose_name="班级")
    # SQL: description longtext default "" not null comment="个性签名"
    description = models.TextField(default="", verbose_name="个性签名")

	#2. 数据表结构信息
	class Meta:
		db_table = 'tb_student'  # 指明数据库表名,如果没有指定表明,则默认为子应用目录名_模型名称,例如: users_student
		verbose_name = '学生信息表'  # 在admin站点中显示的名称
		verbose_name_plural = verbose_name  # 显示的复数名称

	#3. 自定义数据库操作方法
	def __str__(self):
		"""定义每个数据对象的显示信息"""
		return "<User %s>" % self.name
```

### 1  数据库表名

模型类如果未指明表名db_table，Django默认以 **小写app应用名_小写模型类名** 为数据库表名。

可通过**db_table** 指明数据库表名。



### 2 关于主键

django会为表创建自动增长的主键列，每个模型只能有一个主键列。

如果使用选项设置某个字段的约束属性为主键列(primary_key)后，django不会再创建自动增长的主键列。

```python
class Student(models.Model):
    # django会自动在创建数据表的时候生成id主键/还设置了一个调用别名 pk
    id = models.AutoField(primary_key=True, null=False, verbose_name="主键") # 设置主键
```

默认创建的主键列属性为id，可以使用<mark>pk</mark>代替，pk全拼为<mark>primary key</mark>。



### 3 属性命名限制

- 不能是python的保留关键字。

- 不允许使用连续的2个下划线，这是由django的查询方式决定的。__ 是关键字来的，不能使用！！！

- 定义属性时需要指定字段类型，通过字段类型的参数指定选项，语法如下：

  ```python
  属性名 = models.字段类型(约束选项, verbose_name="注释")
  ```



### 4 字段类型

| 类型             | 说明                                                         |
| :--------------- | :----------------------------------------------------------- |
| AutoField        | 自动增长的IntegerField，通常不用指定，不指定时Django会自动创建属性名为id的自动增长属性 |
| BooleanField     | 布尔字段，值为True或False                                    |
| NullBooleanField | 支持Null、True、False三种值                                  |
| CharField        | 字符串，参数max_length表示最大字符个数，对应mysql中的varchar |
| TextField        | 大文本字段，一般大段文本（超过4000个字符）才使用。           |
| IntegerField     | 整数                                                         |
| DecimalField     | 十进制浮点数， 参数max_digits表示总位数， 参数decimal_places表示小数位数,常用于表示分数和价格  Decimal(max_digits=7, decimal_places=2)  ==> 99999.99~ 0.00 |
| FloatField       | 浮点数                                                       |
| DateField        | 日期<br>参数auto_now表示每次保存对象时，自动设置该字段为当前时间。<br>参数auto_now_add表示当对象第一次被创建时自动设置当前。<br>参数auto_now_add和auto_now是相互排斥的，一起使用会发生错误。 |
| TimeField        | 时间，参数同DateField                                        |
| DateTimeField    | 日期时间，参数同DateField                                    |
| FileField        | 上传文件字段,django在文件字段中内置了文件上传保存类, django可以通过模型的字段存储自动保存上传文件, 但是, 在数据库中本质上保存的仅仅是文件在项目中的存储路径!! |
| ImageField       | 继承于FileField，对上传的内容进行校验，确保是有效的图片      |



### 5 约束选项

| 选项         | 说明                                                         |
| :----------- | ------------------------------------------------------------ |
| null         | 如果为True，表示允许为空，默认值是False。相当于python的None  |
| blank        | 如果为True，则该字段允许为空白，默认值是False。  相当于python的空字符串，“” |
| db_column    | 字段的名称，如果未指定，则使用属性的名称。                   |
| db_index     | 若值为True, 则在表中会为此字段创建索引，默认值是False。 相当于SQL语句中的key |
| default      | 默认值，当不填写数据时，使用该选项的值作为数据的默认值。     |
| primary_key  | 如果为True，则该字段会成为模型的主键，默认值是False，一般不用设置，系统默认设置。 |
| unique       | 如果为True，则该字段在表中必须有唯一值，默认值是False。相当于SQL语句中的unique |
| choices      | 每个二元组的第一个值会储存在数据库中，而第二个值将只会用于在表单中显示。 |
| verbose_name | 字段备注名，如果未指定该参数值， Django 会自动使用字段的属性名作为该参数值，并且把下划线转换为空格。 |
|              |                                                              |

**注意：null是数据库范畴的概念，blank是表单验证范畴的**







`choices` 对于一个模型实例，要获取该字段二元组中相对应的第二个值，使用 [`get_FOO_display()`](https://www.bookstack.cn/read/django-3.2-zh/cfb50d3eb65c1cac.md#django.db.models.Model.get_FOO_display) 方法。例如：

```python
# 定义的模型类
from django.db import models
class Person(models.Model):
    SHIRT_SIZES = (
        ('S', 'Small'),
        ('M', 'Medium'),
        ('L', 'Large'),
    )
    name = models.CharField(max_length=60)
    shirt_size = models.CharField(max_length=1, choices=SHIRT_SIZES)	
  
# 使用方法
>>> p = Person(name="Fred Flintstone", shirt_size="L")
>>> p.save()
>>> p.shirt_size
'L'
>>> p.get_shirt_size_display()
'Large'
```





### 6 外键

在设置外键时，需要通过**on_delete**选项指明主表删除数据时，对于外键引用表数据如何处理，在django.db.models中包含了可选常量：

- **CASCADE** 级联，删除主表数据时连通一起删除外键表中数据

- **PROTECT** 保护，通过抛出**ProtectedError**异常，来阻止删除主表中被外键应用的数据

- **SET_NULL** 设置为NULL，仅在该字段null=True允许为null时可用

- **SET_DEFAULT** 设置为默认值，仅在该字段设置了默认值时可用

- **SET()** 设置为特定值或者调用特定方法，例如：

  ```python
  from django.conf import settings
  from django.contrib.auth import get_user_model
  from django.db import models
  
  def get_sentinel_user():
      return get_user_model().objects.get_or_create(username='deleted')[0]
  
  class UserModel(models.Model):
      user = models.ForeignKey(
          settings.AUTH_USER_MODEL,
          on_delete=models.SET(get_sentinel_user),
      )
  ```

- **DO_NOTHING** 不做任何操作，如果数据库前置指明级联性，此选项会抛出**IntegrityError**异常



### 7 表名自定义

在模型类中创建 Meta 类，类下设置字段 db_table = "数据表名"

```python
class StudentDetail(models.Model):
    description = models.TextField(null=True, verbose_name="个性签名")
    class Meta:
        db_table = "db_student_detail"
```







### 8 跨文件模型

关联另一个应用中的模型是当然可以的。为了实现这一点，在定义模型的文件开头导入需要被关联的模型。接着就可以在其他有需要的模型类当中关联它了。比如：

```python
from django.db import models
from geography.models import ZipCode # 导入
class Restaurant(models.Model):
    # ...
    zip_code = models.ForeignKey(
        ZipCode,
        on_delete=models.SET_NULL,
        blank=True,
        null=True,
    )
```



### 9 模型继承

#### 抽象基类

抽象基类在你要将公共信息放入很多模型时会很有用。编写你的基类，并在 [Meta](https://www.bookstack.cn/read/django-3.2-zh/f73a4117a5add268.md#meta-options) 类中填入 `abstract=True`。该模型将不会创建任何数据表。当其用作其它模型类的基类时，它的字段会自动添加至子类。

一个例子：

```python
from django.db import models
class CommonInfo(models.Model):
    name = models.CharField(max_length=100)
    age = models.PositiveIntegerField()
    class Meta:
        abstract = True
class Student(CommonInfo):
    home_group = models.CharField(max_length=5)
```

`Student` 模型拥有3个字段： `name`， `age` 和 `home_group`。 `CommonInfo` 模型不能用作普通的 Django 模型，因为它是一个抽象基类。它不会生成数据表，也没有管理器，也不能被实例化和保存。

从抽象基类继承来的字段可被其它字段或值重写，或用 `None` 删除。

对很多用户来说，这种继承可能就是你想要的。它提供了一种在 Python 级抽出公共信息的方法，但仍会在子类模型中创建数据表。













## 3 数据迁移

将模型类定义表架构的代码转换成SQL同步到数据库中，这个过程就是数据迁移。django中的数据迁移，就是一个类，这个类提供了一系列的终端命令，帮我们完成数据迁移的工作。

### 1 生成迁移文件

所谓的迁移文件, 是类似模型类的迁移类,主要是描述了数据表结构的类文件.

```python
python manage.py makemigrations
```

### 2 同步到数据库中

```python
python manage.py migrate
```





### 3 admin站点管理

补充：在django内部提供了一系列的功能，这些功能也会使用到数据库，所以在项目搭建以后第一次数据迁移的时候，会看到django项目中其他的数据表被创建了。其中就有一个django内置的admin站点管理。

```
# admin站点默认是开启状态的，我们可以通过http://127.0.0.1:8000/admin
# 这个站点必须有个管理员账号登录，所以我们可以在第一次数据迁移，有了数据表以后，就可以通过以下终端命令来创建一个超级管理员账号。

python manage.py createsuperuser
```

![image-20210728143245619](assets/image-20210728143245619.png)

![image-20210728143428753](assets/image-20210728143428753.png)







## 4 数据库基本操作

### 添加记录

#### 1	save方法

通过创建模型类对象，执行对象的save()方法保存到数据库中。

```python
student = Student(
    name="刘德华",
    age=17,
    sex=True,
    clasmate=301,
    description="一手忘情水"
)
student.save()
print(student.id) # 判断是否新增有ID
```

#### 2 create方法

通过模型类.objects.create()保存，返回生成的模型类对象。

```python
student = Student.objects.create(
    name="赵本山",
    age=50,
    sex=True,
    class_number=301,
    description="一段小品"
)
print(student.id)
```

#### 3 批量添加

```python
sc_list =[] 												# 1创建个列表
s = Schedules(self_number=a, task_date=b, zg_id=c, place_id=d)  #2 批量实例化对象传入值
sc_list.append(s) 											#3 把实例的对象添加到列表
Schedules.objects.bulk_create(sc_list)						   # 4 把列表对象拿来添加到数据库
```





### 基础查询

ORM中针对查询结果的限制,提供了一个查询集[QuerySet].这个QuerySet,是ORM中针对查询结果进行保存数据的一个类型,我们可以通过了解这个QuerySet进行使用,达到查询优化,或者限制查询结果数量的作用。

#### （1）all()

查询所有对象，返回queryset对象。查询集，也称查询结果集、QuerySet，表示从数据库中获取的对象集合。

```python
students = Student.objects.all()
print("students:",students)
```

#### （2）filter()

筛选条件相匹配的对象，返回queryset对象。

```python
# 查询所有的女生
students = Student.objects.filter(sex=0)
print(students)
```

#### （3）get()

返回与所给筛选条件相匹配的对象，返回结果有且只有一个， 如果符合筛选条件的对象超过一个或者没有都会抛出错误。

```python 
student = Student.objects.get(pk=1)
print(student)
print(student.description)
get使用过程中的注意点：get是根据条件返回多个结果或者没有结果，都会报错
try:
    student = Student.objects.get(name="刘德华")
    print(student)
    print(student.description)
except Student.MultipleObjectsReturned:
    print("查询得到多个结果！")
except Student.DoesNotExist:
    print("查询结果不存在！")
```

#### （4）first()、last()

分别为查询集的第一条记录和最后一条记录

```python 
# 没有结果返回none，如果有多个结果，则返回模型对象
students = Student.objects.all()
# print(students.name)
print(students[0].name)
stu01 = Student.objects.first()
stu02 = Student.objects.last()

print(stu01.name)
print(stu02.name)
```

#### （5）exclude()

筛选条件不匹配的对象，返回queryset对象。

```python
# 查询张三以外的所有的学生
students = Student.objects.exclude(name="张三")
print(students)
```

#### （6）order_by()

对查询结果排序

```python 
# order_by("字段")  # 按指定字段正序显示，相当于 asc  从小到大
# order_by("-字段") # 按字段倒序排列，相当于 desc 从大到小
# order_by("第一排序","第二排序",...)

# 查询所有的男学生按年龄从高到低展示
# students = Student.objects.all().order_by("-age","-id")
students = Student.objects.filter(sex=1).order_by("-age", "-id")
print(students)
```

#### （7）count()

查询集中对象的个数

```python 
# 查询所有男生的个数
count = Student.objects.filter(sex=1).count()
print(count)
```

#### （8）exists()

判断查询集中是否有数据，如果有则返回True，没有则返回False

````python
# 查询Student表中是否存在学生
print(Student.objects.exists())
````

#### （9）values()、values_list()

* `values()`把结果集中的模型对象转换成**字典**,并可以设置转换的字段列表，达到减少内存损耗，提高性能

* `values_list()`: 把结果集中的模型对象转换成**列表**，并可以设置转换的字段列表（元祖），达到减少内存损耗，提高性能

```python 
# values 把查询结果中模型对象转换成字典
student_list = Student.objects.filter(classmate="301")
student_list = student_list.order_by("-age")
student_list = student_list.filter(sex=1)
ret1 = student_list.values() # 默认把所有字段全部转换并返回
ret2 = student_list.values("id","name","age") # 可以通过参数设置要转换的字段并返回
ret3 = student_list.values_list() # 默认把所有字段全部转换并返回
ret4 = student_list.values_list("id","name","age") # 可以通过参数设置要转换的字段并返回
print(ret4)
return JsonResponse({},safe=False)
```

#### （10）distinct()

从返回结果中剔除重复纪录。返回queryset。

````python
# 查询所有学生出现过的年龄
print(Student.objects.values("age").distinct())
````





### 模糊查询

#### （1）模糊查询之contains

> 说明：如果要包含%无需转义，直接写即可。

例：查询姓名包含'华'的学生。

```python
Student.objects.filter(name__contains='华')
```

#### （2）模糊查询之startswith、endswith

例：查询姓名以'文'结尾的学生

```python
Student.objects.filter(name__endswith='文')
```

> 以上运算符都区分大小写，在这些运算符前加上i表示不区分大小写，如iexact、icontains、istartswith、iendswith.

#### （3）模糊查询之isnull

例：查询个性签名不为空的学生。

```python
# 修改Student模型description属性允许设置为null，然后数据迁移
description = models.TextField(default=None, null=True, verbose_name="个性签名")
# 添加测试数据
NSERT INTO student.db_student (name, age, sex, class, description, created_time, updated_time) VALUES ('刘德华', 17, 1, '407', null, '2020-11-20 10:00:00.000000', '2020-11-20 10:00:00.000000');

# 代码操作
tudent_list = Student.objects.filter(description__isnull=True)
```

#### （4）模糊查询之in

例：查询编号为1或3或5的学生

```python
Student.objects.filter(id__in=[1, 3, 5])
```

#### （5）模糊查询之比较查询

- **gt** 大于 (greater then)
- **gte** 大于等于 (greater then equal)
- **lt** 小于 (less then)
- **lte** 小于等于 (less then equal)

例：查询编号大于3的学生

```python
Student.objects.filter(id__gt=3)
```

#### （6）模糊查询之日期查询

**year、month、day、week_day、hour、minute、second：对日期时间类型的属性进行运算。**

例：查询2010年被添加到数据中的学生。

```python
Student.objects.filter(born_date__year=1980)
```

例：查询2016年6月20日后添加的学生信息。

```python
from django.utils import timezone as datetime
student_list = Student.objects.filter(created_time__gte=datetime.datetime(2016,6,20),created_time__lt=datetime.datetime(2016,6,21)).all()
print(student_list)
```



### 进阶查询

#### （1） F查询

之前的查询都是对象的属性与常量值比较，两个属性怎么比较呢？ 答：使用F对象，被定义在django.db.models中。

语法如下：

```sql
"""F对象：2个字段的值比较"""
# 获取从添加数据以后被改动过数据的学生
from django.db.models import F
# SQL: select * from db_student where created_time=updated_time;
student_list = Student.objects.exclude(created_time=F("updated_time"))
print(student_list)
```

#### （2） Q查询

**多个过滤器逐个调用表示逻辑与关系，同sql语句中where部分的and关键字。**

例：查询年龄大于20，并且编号小于30的学生。

```python
Student.objects.filter(age__gt=20,id__lt=30)
或
Student.filter(age__gt=20).filter(id__lt=30)
```

**如果需要实现逻辑或or的查询，需要使用Q()对象结合|运算符**，Q对象被义在django.db.models中。

语法如下：

```text
Q(属性名__运算符=值)
Q(属性名__运算符=值) | Q(属性名__运算符=值)
```

例：查询年龄小于19或者大于20的学生，使用Q对象如下。

```python
from django.db.models import Q
student_list = Student.objects.filter( Q(age__lt=19) | Q(age__gt=20) ).all()
```

**Q对象可以使用&、|连接，&表示逻辑与，|表示逻辑或****

例：查询年龄大于20，或编号小于30的学生，只能使用Q对象实现

```python
Student.objects.filter(Q(age__gt=20) | Q(pk__lt=30))
```

`Q对象左边可以使用~操作符，表示非not。但是工作中，我们只会使用Q对象进行或者的操作，只有多种嵌套复杂的查询条件才会使用&和~进行与和非得操作`。

例：查询编号不等于30的学生。

```python
Student.objects.filter(~Q(pk=30))
```

Q的or查询

```py
from django.db.models import Q
	search_list = ['name__contains', 'email__contains']			# 筛选条件，name字段模糊与email字段模糊
    search_value = request.GET.get('q', '')  					# 读取用户搜索内容
    conn = Q()  											  # 创建Q对象
    conn.connector = 'OR'
     for item in search_list:
    	conn.children.append((item, search_value))  			# 把筛选配置与筛选内容以元组append Q对象内。
    
    queryset = self.model_class.objects.filter(conn)			# 进行查找
```







#### （3）聚合查询

使用aggregate()过滤器调用聚合函数。聚合函数包括：**Avg** 平均，**Count** 数量，**Max** 最大，**Min** 最小，**Sum** 求和，被定义在django.db.models中。

例：查询学生的平均年龄。

```python
from django.db.models import Sum,Count,Avg,Max,Min

Student.objects.aggregate(Avg('age'))
```

注意：aggregate的返回值是一个字典类型，格式如下：

```python
  {'属性名__聚合类小写':值}
```

使用count时一般不使用aggregate()过滤器。

例：查询学生总数。

```python
Student.objects.count() # count函数的返回值是一个数字。
```

#### （4）分组查询

```python
QuerySet对象.annotate()
# annotate() 进行分组统计，按前面select 的字段进行 group by
# annotate() 返回值依然是 queryset对象，增加了分组统计后的键值对
模型对象.objects.values("id").annotate(course=Count('course__sid')).values('id','course')
# 查询指定模型， 按id分组 , 将course下的sid字段计数，返回结果是 name字段 和 course计数结果 

# SQL原生语句中分组之后可以使用having过滤，在django中并没有提供having对应的方法，但是可以使用filter对分组结果进行过滤
# 所以filter在annotate之前，表示where，在annotate之后代表having
# 同理，values在annotate之前，代表分组的字段，在annotate之后代表数据查询结果返回的字段
```

#### （5）原生查询

执行原生SQL语句,也可以直接跳过模型,才通用原生pymysql.

```python
 ret = Student.objects.raw("SELECT id,name,age FROM db_student")  # student 可以是任意一个模型
 # 这样执行获取的结果无法通过QuerySet进行操作读取,只能循环提取
 print(ret,type(ret))
 for item in ret:
    print(item,type(item))
```



### 字符串查找字段对象

通过字符串找到字段的对象

```python
# model_class ：表模型类
# 'gender' ;模型类中的字段名
field_object = model_class._meta.get_field('gender')
```

















### 修改记录

#### （1） 使用save更新数据

```python 
student = Student.objects.filter(name='刘德华').first()
print(student)
student.age = 19
student.classmate = "303"
# save之所以能提供给我们添加数据的同时，还可以更新数据的原因？
# save会找到模型的字段的主键id的值，
# 主键id的值如果是none，则表示当前数据没有被数据库，所以save会自动变成添加操作
# 主键id有值，则表示当前数据在数据库中已经存在，所以save会自动变成更新数据操作
student.save()
```

#### （2）update更新（推荐）

**使用模型类.objects.filter().update()**，会返回受影响的行数

```python
# update是全局更新，只要符合更新的条件，则全部更新，因此强烈建议加上条件！！！
student = Student.objects.filter(name="赵华",age=22).update(name="刘芙蓉",sex=True)
print(student)
```





### 删除记录

删除有两种方法

#### （1）模型类对象.delete

```python
student = Student.objects.get(id=13)
student.delete()
```

#### （2）模型类.objects.filter().delete()

```python
Student.objects.filter(id=14).delete() 
```

代码：

```python
# 1. 先查询到数据模型对象。通过模型对象进行删除
# student = Student.objects.filter(pk=13).first()
# student.delete()

# 2. 直接删除
ret = Student.objects.filter(pk=100).delete()
print(ret)
# 务必写上条件，否则变成了清空表了。ret = Student.objects.filter().delete()
```



## 5 创建关联模型

实例：我们来假定下面这些概念，字段和关系

> - 班级模型: 班级名称、导员。
> - 课程模型：课程名称、讲师等。
> - 学生模型： 学生有姓名，年龄，只有一个班级，所以和班级表是一对多的关系(one-to-many);选修了多个课程，所以和课程表是多对多的关系(many-to-many)
> - 学生详情：学生的家庭地址，手机号，邮箱等详细信息，和学生模型应该是一对一的关系（one-to-one）

#### 一对多

```python
from django.db import models

class Clas(models.Model):
    name = models.CharField(max_length=32, unique=True, verbose_name="班级名称")

class Student(models.Model):
    sex_choices = (
        (0, "女"),
        (1, "男"),
        (2, "保密"),
    )
    name = models.CharField(max_length=32, unique=True, verbose_name="姓名")
    age = models.SmallIntegerField(verbose_name="年龄", default=18)  # 年龄
    sex = models.SmallIntegerField(choices=sex_choices)
    
    clas = models.ForeignKey("Clas", on_delete=models.CASCADE)
    # on_delete= 关联关系的设置
	# models.CASCADE    删除主键以后, 对应的外键所在数据也被删除
    # models.DO_NOTHING 删除主键以后, 对应的外键不做任何修改
	# 反向查找字段 related_name
```



#### 多对多

```python
from django.db import models

class Course(models.Model):
    name = models.CharField(max_length=32, unique=True, verbose_name="课程名称")
    class Meta:
        db_table = "db_course"

class Student(models.Model):
    name = models.CharField(max_length=32, unique=True, verbose_name="姓名")
    age = models.SmallIntegerField(verbose_name="年龄", default=18)  # 年龄
 
    courses = models.ManyToManyField("Course", db_table="db_student2course")
    # 建立多对多的关系,ManyToManyField可以建在两个模型中的任意一个表中，自动创建第三张表
    # db_table= ：设置第三张表名称
```



#### 一对一

```python 
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=32, unique=True, verbose_name="姓名")
    age = models.SmallIntegerField(verbose_name="年龄", default=18)  # 年龄   

    stu_detail = models.OneToOneField("StudentDetail", on_delete=models.CASCADE)
	# 一对一字段设置 models.OneToOneField
    
class StudentDetail(models.Model):
    description = models.TextField(null=True, verbose_name="个性签名")
    class Meta:
        db_table = "db_student_detail"

```









## 6 关联数据操作

### 1一对多与一对一

```python 
 stu = Student.objects.create(name="王五", age=23, sex=1, birthday="1991-11-12", clas_id=9, stu_detail_id=6)
  print(stu.clas_id)  				# 6
  print(stu.stu_detail_id)  		# 5
  print(stu.clas)  					# 模型类对象
  print(stu.stu_detail)  			# 模型类对象
  print(stu.clas.name)				 # 查询stu这个学生的班级名称
  print(stu.stu_detail.tel)			 # 查询stu这个学生的手机号
```



### 2 多对多

#### 添加多对多的数据

```python
 # 添加多对多方式1
    c1 = Course.objects.get(title="思修")
    c2 = Course.objects.get(title="逻辑学")
    stu.courses.add(c1,c2)

    # 添加多对多方式2
    stu = Student.objects.get(name="张三")
    stu.courses.add(5,7)

    # 添加多对多方式3
    stu = Student.objects.get(name="李四")
    stu.courses.add(*[6,7])
```



#### 删除多对多记录

```python 
   stu = Student.objects.get(name="李四")
   stu.courses.remove(7)
```



#### 清空多对多记录：clear方法

```python
    stu = Student.objects.get(name="rain")
    stu.courses.clear()
```





#### 重置多对多记录：set方法

```python
stu = Student.objects.get(name="李四")
stu.courses.set([5,8])
```



#### 多对多记录查询： all

```python
    # 查询李四所报课程的名称
    stu = Student.objects.get(name="李四")
    courses = stu.courses.all()
    courses = stu.courses.all().values("title")
    print(courses)  # <QuerySet [<Course: Course object (5)>, <Course: Course object (8)>]>

```













## 7 关联查询

### 1、基于对象查询（子查询）

#### 一对多查询

```python
# 查询张三所在班级的名称
stu = Student.objects.get(name="张三")
print(stu.clas.name)

# 查询计算机科学与技术2班有哪些学生
clas = Clas.objects.get(name="计算机科学与技术2班")

# 反向查询方式1：
ret = clas.student_set.all()  					# 反向查询按表名小写_set
print(ret) 										# <QuerySet [<Student: 张三>, <Student: 李四>]>

# 反向查询方2：
print(clas.student_list.all())  				# <QuerySet [<Student: 张三>, <Student: 李四>]>

```



#### 对一查询

```python
# 查询李四的手机号
stu = Student.objects.get(name="李四")
print(stu.stu_detail.tel)

# 查询110手机号的学生姓名和年龄
stu_detail = StudentDetail.objects.get(tel="110")

# 反向查询方式1： 表名小写
print(stu_detail.student.name)
print(stu_detail.student.age)

# 反向查询方式2： related_name
print(stu_detail.stu.name)
print(stu_detail.stu.age)
```



#### 多对多查询

```python 
# 查询张三所报课程的名称
stu = Student.objects.get(name="张三")
print(stu.courses.all())  # QuerySet [<Course: 近代史>, <Course: 篮球>]>

# 查询选修了近代史这门课程学生的姓名和年龄
course = Course.objects.get(title="近代史")

# 反向查询方式1： 表名小写_set
print(course.student_set.all()) # <QuerySet [<Student: 张三>, <Student: 李四>]>

# 反向查询方式2：related_name
print(course.students.all())
print(course.students.all().values("name","age"))
# <QuerySet [{'name': '张三', 'age': 22}, {'name': '李四', 'age': 24}]>

```

> （1）正向查询按字段
>
> （2）反向查询按表名小写或者related_name













### 2、基于双下划线查询（join查询）

```python 
# 查询张三的年龄
ret = Student.objects.filter(name="张三").values("age")
print(ret) # <QuerySet [{'age': 22}]>

# (1) 查询年龄大于22的学生的姓名以及所在名称班级
# 方式1 ： Student作为基表
ret = Student.objects.filter(age__gt=22).values("name","clas__name")
print(ret)

# 方式2 ：Clas表作为基表
ret = Clas.objects.filter(student_list__age__gt=22).values("student_list__name","name")
print(ret)

# (2) 查询计算机科学与技术2班有哪些学生
ret = Clas.objects.filter(name="计算机科学与技术2班").values("student_list__name")
print(ret)  #<QuerySet [{'student_list__name': '张三'}, {'student_list__name': '李四'}]>

# (3) 查询张三所报课程的名称

ret = Student.objects.filter(name="张三").values("courses__title")
print(ret) # <QuerySet [{'courses__title': '近代史'}, {'courses__title': '篮球'}]>

# (4) 查询选修了近代史这门课程学生的姓名和年龄

ret = Course.objects.filter(title="近代史").values("students__name","students__age")
print(ret) 
# <QuerySet [{'students__name': '张三', 'students__age': 22}, {'students__name': '李四', 'students__age': 24}]>

# (5) 查询李四的手机号
ret = Student.objects.filter(name='李四').values("stu_detail__tel")
print(ret)  # <QuerySet [{'stu_detail__tel': '911'}]>


# (6) 查询手机号是110的学生的姓名和所在班级名称
# 方式1
    ret = StudentDetail.objects.filter(tel="110").values("stu__name","stu__clas__name")
    print(ret) # <QuerySet [{'stu__name': '张三', 'stu__clas__name': '计算机科学与技术2班'}]>

# 方式2：
    ret = Student.objects.filter(stu_detail__tel="110").values("name","clas__name")
    print(ret) # <QuerySet [{'name': '张三', 'clas__name': '计算机科学与技术2班'}]>

```

> （1）正向关联按关联字段
>
> （2）反向按表名小写或related_name



### 3、关联分组查询

````python 
from django.db.models import Avg, Count, Max, Min

ret = Student.objects.values("sex").annotate(c = Count("name"))
print(ret) # <QuerySet [{'sex': 0, 'c': 1}, {'sex': 1, 'c': 3}]>

# （1）查询每一个班级的名称以及学生个数
ret = Clas.objects.values("name").annotate(c = Count("student_list__name"))
print(ret)
# <QuerySet [{'name': '网络工程1班', 'c': 0}, {'name': '网络工程2班', 'c': 0}, {'name': '计算机科学与技术1班', 'c': 0}, {'name': '计算机科学与技术2班', 'c': 1}, {'name': '软件1班', 'c': 3}]>


# （2）查询每一个学生的姓名,年龄以及选修课程的个数
ret = Student.objects.values("name","age").annotate(c=Count("courses__title"))
print(ret)
# <QuerySet [{'name': 'rain', 'c': 0}, {'name': '张三', 'c': 2}, {'name': '李四', 'c': 2}, {'name': '王五', 'c': 0}]>

ret = Student.objects.all().annotate(c=Count("courses__title")).values("name","age","sex","c")
# print(ret)


# (3) 每一个课程名称以及选修学生的个数
ret = Course.objects.all().annotate(c = Count("students__name")).values("title","c")
print(ret)
# <QuerySet [{'title': '近代史', 'c': 2}, {'title': '思修', 'c': 0}, {'title': '篮球', 'c': 1}, {'title': '逻辑学', 'c': 1}, {'title': '轮滑', 'c': 0}]>


# (4)  查询选修课程个数大于1的学生姓名以及选修课程个数
ret = Student.objects.all().annotate(c=Count("courses__title")).filter(c__gt=1).values("name","c")
print(ret)
# <QuerySet [{'name': '张三', 'c': 2}, {'name': '李四', 'c': 2}]>


# (5) 查询每一个学生的姓名以及选修课程个数并按着选修的课程个数进行从低到高排序
ret = Student.objects.all().annotate(c=Count("courses__title")).order_by("c").values("name","c")
print(ret)
````









# 七、Ajax请求

客户端（浏览器）向服务端发起请求的形式：

1. 地址栏：GET
2. 超链接标签：GET
3. form表单：GET或POST
4. Ajax（重要）：GET或POST或PUT或DELETE

AJAX（Asynchronous Javascript And XML）翻译成中文就是“异步Javascript和XML”。即使用Javascript语言与服务器进行异步交互，传输的数据为XML（当然，传输的数据不只是XML,现在更多使用json数据）。

AJAX的特点和优点：

- 异步
- 局部刷新

应用：

![image-20210812104733820](assets/image-20210812104733820.png)



## json数据

```python 
'''
Supports the following objects and types by default:

    +-------------------+---------------+
    | Python            | JSON          |
    +===================+===============+
    | dict              | object        |
    +-------------------+---------------+
    | list, tuple       | array         |
    +-------------------+---------------+
    | str               | string        |
    +-------------------+---------------+
    | int, float        | number        |
    +-------------------+---------------+
    | True              | true          |
    +-------------------+---------------+
    | False             | false         |
    +-------------------+---------------+
    | None              | null          |
    +-------------------+---------------+

'''
```

### 1 python的序列化和反序列化方法

```python 
import json

dic = {"name": "yuan"}
dic_json = json.dumps(dic)
dic = json.dumps(dic_json)
```

### 2 Django支持的序列化方法

关于Django中的序列化主要应用在将数据库中检索的数据返回给客户端用户，特别的Ajax请求一般返回的为Json格式。

```python 
# 序列化响应类
from django.http import JsonResponse
JsonResponse({})
# 序列化queryset
from django.core import serializers
ret = models.Book.objects.all()
data = serializers.serialize("json", ret)
```





## Ajax请求案例

![image-20210812113615978](assets/image-20210812113615978.png)

#### (1) 视图

```python 
# Create your views here.
def reg(request):
    return render(request, "reg.html")

def reg_user(request):
    data = {"msg": "", "state": "success"}
    user = request.POST.get("user")
    if user == "yuan":
        data["state"] = "error"
        data["msg"] = "该用户已存在！"

    return JsonResponse(data)
```

#### (2) 模板：reg.html

```html 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<p>用户名：<input type="text"><span class="error" style="color: red"></span></p>

<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.6.0/jquery.js"></script>
<script>

    $(":text").blur(function () {
        // 发送Ajax请求
        $.ajax({
            url: "http://127.0.0.1:8008/reg_user/",
            type: "post",
            data: {
                user: $(":text").val(),
            },
            success: function (response) {
                console.log(response);
                $(".error").html(response.msg);
            }
        })
    })

</script>

</body>
</html>
```

#### (3) 流程图

![image-20210812114853512](assets/image-20210812114853512.png)







## 同源策略

### 1 同源策略和跨域

现在我们将reg.html单独放在客户端，用浏览器打开，再触发事件，会发现报错：

![image-20210812115456734](assets/image-20210812115456734.png)

这是因为浏览器的同源策略导致的。

同源策略（Same origin policy）是一种约定，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，则浏览器的正常功能可能都会受到影响。可以说Web是构建在同源策略基础之上的，浏览器只是针对同源策略的一种实现。

> 同源策略，它是由Netscape提出的一个著名的安全策略。现在所有支持JavaScript 的浏览器都会使用这个策略。所谓同源是指，域名，协议，端口相同。当一个浏览器的两个tab页中分别打开来 百度和谷歌的页面当浏览器的百度tab页执行一个脚本的时候会检查这个脚本是属于哪个页面的，即检查是否同源，只有和百度同源的脚本才会被执行。如果非同源，那么在请求数据时，浏览器会在控制台中报一个异常，提示拒绝访问。

那么如何解决这种跨域问题呢，我们主要由三个思路：

> 1. jsonp
> 2. cors
> 3. 前端代理

这里主要给大家介绍第二个：cors

CORS需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，IE浏览器不能低于IE10。

整个CORS通信过程，都是浏览器自动完成，不需要用户参与。对于开发者来说，CORS通信与同源的AJAX通信没有差别，代码完全一样。浏览器一旦发现AJAX请求跨源，就会自动添加一些附加的头信息，有时还会多出一次附加的请求，但用户不会有感觉。

因此，实现CORS通信的关键是服务器。只要服务器实现了CORS接口，就可以跨源通信。

所以，服务器方面只要添加一个响应头，同意跨域请求，浏览器也就不再拦截：

```python 
response = JsonResponse(data)
response["Access-Control-Allow-Origin"] = "*"
```

![image-20210812121643296](assets/image-20210812121643296.png)

### 2 cors

cors有两种请求：简单请求和非简单请求

只要同时满足以下两大条件,就属于简单的请求

```text
（1) 请求方法是以下三种方法之一：
HEAD
GET
POST
（2）HTTP的头信息不超出以下几种字段：
Accept
Accept-Language
Content-Language
Last-Event-ID
Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、text/plain
```

凡是不同时满足上面两个条件，就属于非简单请求。浏览器对这两种请求的处理，是不一样的。

简单请求:一次请求

非简单请求:两次请求，在发送数据之前会先发一次请求用于做“预检”，只有“预检”通过后才再发送一次请求用于数据传输。

```
- 请求方式：OPTIONS
- “预检”其实做检查，检查如果通过则允许传输数据，检查不通过则不再发送真正想要发送的消息
- 如何“预检”
     => 如果复杂请求是PUT等请求，则服务端需要设置允许某请求，否则“预检”不通过
        Access-Control-Request-Method
     => 如果复杂请求设置了请求头，则服务端需要设置允许某请求头，否则“预检”不通过
        Access-Control-Request-Headers
```

支持跨域,简单请求:

```text
服务器设置响应头：Access-Control-Allow-Origin = '域名' 或 '*'
```

支持跨域复杂请求:

```
由于复杂请求时，首先会发送“预检”请求，如果“预检”成功，则发送真实数据。
“预检”请求时，允许请求方式则需服务器设置响应头：Access-Control-Request-Method
“预检”请求时，允许请求头则需服务器设置响应头：Access-Control-Request-Headers
```

cors在Django中的实现：

在返回结果中加入允许信息(简单请求):

```python
def test(request):
    import json
    obj=HttpResponse(json.dumps({'name':'yuan'}))
    # obj['Access-Control-Allow-Origin']='*'
    obj['Access-Control-Allow-Origin']='http://127.0.0.1:8004'
    return obj
```

放到中间件中处理复杂和简单请求:

```python
from django.utils.deprecation import MiddlewareMixin
class MyCorsMiddle(MiddlewareMixin):
    def process_response(self, request, response):
        # 简单请求:
        # 允许http://127.0.0.1:8001域向我发请求
        # ret['Access-Control-Allow-Origin']='http://127.0.0.1:8001'
        # 允许所有人向我发请求
        response['Access-Control-Allow-Origin'] = '*'
        if request.method == 'OPTIONS':
            # 所有的头信息都允许
            response['Access-Control-Allow-Headers'] = '*'
        return response
```

在settings中配置即可,在中间件中的位置可以随意放置.

也可以通过第三方组件：pip install django-cors-headers

```python
# (1)
pip install django-cors-headers

# (2)
 INSTALLED_APPS = (
 'corsheaders',
)
  
# (3)
 1 MIDDLEWARE = [
 2     'django.middleware.security.SecurityMiddleware',
 3     'django.contrib.sessions.middleware.SessionMiddleware',
 4     'django.middleware.csrf.CsrfViewMiddleware',
 5     'django.contrib.auth.middleware.AuthenticationMiddleware',
 6     'django.contrib.messages.middleware.MessageMiddleware',
 7     'django.middleware.clickjacking.XFrameOptionsMiddleware',
 8     'corsheaders.middleware.CorsMiddleware',  # 按顺序
 9     'django.middleware.common.CommonMiddleware',  # 按顺序
10 ]
  
  # 配置白名单
 1 CORS_ALLOW_CREDENTIALS = True#允许携带cookie
 2 CORS_ORIGIN_ALLOW_ALL = True
 3 CORS_ORIGIN_WHITELIST = ( '*')#跨域增加忽略
 4 CORS_ALLOW_METHODS = ( 'DELETE', 'GET', 'OPTIONS', 'PATCH', 'POST', 'PUT', 'VIEW', )
 5 #允许的请求头
 6 CORS_ALLOW_HEADERS = (
 7     'XMLHttpRequest',
 8     'X_FILENAME',
 9     'accept-encoding',
10     'authorization',
11     'content-type',
12     'dnt',
13     'origin',
14     'user-agent',
15     'x-csrftoken',
16     'x-requested-with',
17     'Pragma',
18 )
  
```

> 前端项目设置请求头记得添加到CORS_ALLOW_HEADERS









# 八、Django的组件

## 1  中间件

中间件顾名思义，是介于request与response处理之间的一道处理过程，相对比较轻量级，并且在全局上改变django的输入与输出。因为改变的是全局，所以需要谨慎使用，用不好会影响到性能。

中间件应用

 ```
做IP访问频率限制,某些IP访问服务器的频率过高，进行拦截，比如限制每分钟不能超过20次。
 ```

Django的中间件的定义：

```text 
Middleware is a framework of hooks into Django’s request/response processing. 
It’s a light, low-level “plugin” system for globally altering Django’s input or output.

MiddleWare，是 Django 请求/响应处理的钩子框架。
它是一个轻量级的、低级的“插件”系统，用于全局改变 Django 的输入或输出。【输入指代的就是客户端像服务端django发送数据，输出指代django根据客户端要求处理数据的结果返回给客户端】
```

如果你想修改请求，例如被传送到view中的**HttpRequest**对象。 或者你想修改view返回的**HttpResponse**对象，这些都可以通过中间件来实现。

django框架内部声明了很多的中间件，这些中间件有着各种各种的用途，有些没有被使用，有些被默认开启使用了。而被开启使用的中间件，都是在settngs.py的MIDDLEWARE中注册使用的。

Django默认的`Middleware`：

```python 
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```



### 1.自定义中间件

1定义中间件

创建存放自定义中间件的文件这里选择在app01里创建mdws.py文件：

```python
from django.utils.deprecation import MiddlewareMixin


class Md1(MiddlewareMixin):

    def process_request(self, request):
        print("Md1请求")
        # return HttpResponse("Md1中断")    # 拦截

    def process_response(self, request, response):
        print("Md1返回")
        return response


class Md2(MiddlewareMixin):

    def process_request(self, request):
        print("Md2请求")
        # return HttpResponse("Md2中断")

    def process_response(self, request, response):
        print("Md2返回")
        return response

```

> 1. process_request默认返回None，返回None，则继续执行下一个中间件的process_request；一旦返回响应体对象，则会拦截返回。
> 2. process_response必须有一个形参response，并return response；这是view函数返回的响应体，像接力棒一样传承给最后的客户端。

![image-20210812132734549](assets/image-20210812132734549.png)

2 注册中间件

```python 
MIDDLEWARE = [
    ...
    'app01.mdws.Md1',
    'app01.mdws.Md2'
]
```

3 构建index路由

```python 
# path('index/', views.index),


def index(request):
    print("index 视图函数执行...")
    return HttpResponse("hello yuan")
```

启动项目，访问index路径：
![image-20210812130256052](assets/image-20210812130256052.png)

后台打印结果：

````text 
Md1请求
Md2请求
index 视图函数执行...
Md2返回
Md1返回
````

所以，通过结果我们看出中间件的执行顺序：

![中间件](assets/%E4%B8%AD%E9%97%B4%E4%BB%B6-16287456116091.png)











## 2 Cookie与Session

我们知道HTTP协议是无状态协议，也就是说每个请求都是独立的！无法记录前一次请求的状态。但HTTP协议中可以使用Cookie来完成会话跟踪！在Web开发中，使用session来完成会话跟踪，session底层依赖Cookie技术。 

### 1 cookie

Cookie翻译成中文是小甜点，小饼干的意思。在HTTP中它表示服务器送给客户端浏览器的小甜点。其实Cookie是key-value结构，类似于一个python中的字典。随着服务器端的响应发送给客户端浏览器。然后客户端浏览器会把Cookie保存起来，当下一次再访问服务器时把Cookie再发送给服务器。 Cookie是由服务器创建，然后通过响应发送给客户端的一个键值对。客户端会保存Cookie，并会标注出Cookie的来源（哪个服务器的Cookie）。当客户端向服务器发出请求时会把所有这个服务器Cookie包含在请求中发送给服务器，这样服务器就可以识别客户端了！

> cookie可以理解为每一个浏览器针对每一个服务器创建的key-value结构的本地存储文件

#### 1 cookie流程图

![image-20210812145309289](assets/image-20210812145309289.png)

#### 2 cookie语法

```python
# (1) 设置cookie：
res = HttpResponse(...) 或 rep ＝ render(request, ...) 或 rep ＝ redirect() 
res.set_cookie(key,value,max_age...)      			 # 明文发送给浏览器
res.set_signed_cookie(key,value,salt='加密盐',...)　  #加密发送给浏览器
# (2) 获取cookie：
request.COOKIES
request.get_signed_cookie("user_id", salt="12*$35867241")
# (3) 删除cookie
response.delete_cookie("cookie_key",path="/",domain=name)
```

### 2 session

> Django 提供对匿名会话(session)的完全支持。这个会话框架让你可以存储和取回每个站点访客任意数据。它在服务器端存储数据, 并以cookies的形式进行发送和接受数据。

#### 1 session流程

![image-20210813164309357](assets/image-20210813164309357-16288441998871.png)

#### 2 session语法与案例

> ```python 
> # 1、设置Sessions值
>        request.session['session_name'] ="admin"
> # 2、获取Sessions值
>        session_name = request.session["session_name"]
> # 3、删除Sessions值
>        del request.session["session_name"]
> # 4、flush()
>   # 删除当前的会话数据并删除会话的Cookie。这用于确保前面的会话数据不可以再次被用户的浏览器访问
> ```

```python 
def s_login(request):
    if request.method == "GET":
        return render(request, "login.html")
    else:
        user = request.POST.get("user")
        pwd = request.POST.get("pwd")
        try:
            user_obj = User.objects.get(user=user,pwd=pwd)  # 用户名去数据库查找，没有就报错
            # 写session
            request.session["is_login"] = True              # 写一个登陆状态
            equest.session["username"] = user_obj.user      # 写一个用户名
            return redirect("/s_index/")			
        except:
            return redirect("/s_login/")					

          
def s_index(request):
    # 读session
    is_login = request.session.get("is_login")
    if is_login:
        username = request.session.get("username")
        return render(request, "index.html", {"user": username})
    else:
        return redirect("/s_login/")
'''
shop.html:
<p>
客户端最后一次访问时间：{{ last_time|default:"第一次访问" }}
</p>
<h3>商品页面</h3>
'''

def shop(request):
    last_time = request.session.get("last_time")
    now = datetime.datetime.now().strftime("%Y-%m-%d %X")
    request.session["last_time"] = now

    return render(request, "shop.html", {"last_time": last_time})


def s_logout(request):					# 删除session
    # request.session.flush()
    del request.session["username"]
    del request.session["is_login"]
    return redirect("/s_login/")

```

> 1. session 在服务器端，cookie 在客户端（浏览器）
> 2. session 默认被存在在服务器的一个文件里（不是内存）
> 3. session 的运行依赖 session id，而 session id 是存在 cookie 中的.
> 4. session 可以放在 文件、数据库、或内存中都可以。
> 5. 用户验证这种场合一般会用 session

#### 3 session配置

````python 
# Django默认支持Session，并且默认是将Session数据存储在数据库中，即：django_session 表中。
   
# 配置 settings.py
   
    SESSION_ENGINE = 'django.contrib.sessions.backends.db'   # 引擎（默认）
       
    SESSION_COOKIE_NAME ＝ "sessionid"               # Session的cookie保存在浏览器上时的key，即：sessionid＝随机字符串（默认）
    SESSION_COOKIE_PATH ＝ "/"                               # Session的cookie保存的路径（默认）
    SESSION_COOKIE_DOMAIN = None                             # Session的cookie保存的域名（默认）
    SESSION_COOKIE_SECURE = False                            # 是否Https传输cookie（默认）
    SESSION_COOKIE_HTTPONLY = True                           # 是否Session的cookie只支持http传输（默认）
    SESSION_COOKIE_AGE = 1209600                             # Session的cookie失效日期（2周）（默认）
    SESSION_EXPIRE_AT_BROWSER_CLOSE = False                  # 是否关闭浏览器使得Session过期（默认）
    SESSION_SAVE_EVERY_REQUEST = False                       # 是否每次请求都保存Session，默认修改之后才保存（默认）
````

### 3 用户认证组件

Django默认已经提供了认证系统Auth模块，我们认证的时候，会使用auth模块里面给我们提供的表。认证系统包含：

- 用户管理
- 权限
- 用户组
- 密码哈希系统
- 用户登录或内容显示的表单和视图
- 一个可插拔的后台系统 admin



#### 1 Django用户模型类

Django认证系统中提供了用户模型类User保存用户的数据，默认的User包含以下常见的基本字段：

| 字段名             | 字段描述                                                     |
| ------------------ | ------------------------------------------------------------ |
| `username`         | 必选。150个字符以内。 用户名可能包含字母数字，`_`，`@`，`+` `.` 和`-`个字符。 |
| `first_name`       | 可选（`blank=True`）。 少于等于30个字符。                    |
| `last_name`        | 可选（`blank=True`）。 少于等于30个字符。                    |
| `email`            | 可选（`blank=True`）。 邮箱地址。                            |
| `password`         | 必选。 密码的哈希加密串。 （Django 不保存原始密码）。 原始密码可以无限长而且可以包含任意字符。 |
| `groups`           | 与`Group` 之间的多对多关系。                                 |
| `user_permissions` | 与`Permission` 之间的多对多关系。                            |
| `is_staff`         | 布尔值。 设置用户是否可以访问Admin 站点。                    |
| `is_active`        | 布尔值。 指示用户的账号是否激活。 它不是用来控制用户是否能够登录，而是描述一种帐号的使用状态。 |
| `is_superuser`     | 是否是超级用户。超级用户具有所有权限。                       |
| `last_login`       | 用户最后一次登录的时间。                                     |
| `date_joined`      | 账户创建的时间。 当账号创建时，默认设置为当前的date/time。   |

上面缺少一些字段，所以后面我们会对当前内置的用户模型进行改造，比如说它里面没有手机号字段，后面我们需要加上。

#### 2 重要方法

Django 用户认证（Auth）组件需要导入 auth 模块

```python 
# 认证模块
from django.contrib import auth
# 对应数据库用户表,可以继承扩展
from django.contrib.auth.models import User
```

#### 3 用户对象

```python
create() # 创建一个普通用户，密码是明文的。
create_user() # 创建一个普通用户，密码是密文的。
create_superuser() # 与create_user() 相同，但是设置is_staff 和is_superuser 为True。

set_password(*raw_password*)
# 设置用户的密码为给定的原始字符串，并负责密码的。 不会保存User对象。当None为raw_password时，密码将设置为一个不可用的密码。
check_password(*raw_password*)
# 如果给定的raw_password是用户的真实密码，则返回True，可以在校验用户密码时使用。
```

#### 4 认证方法

```python 
auth.authenticate(username,password) 
# 将输入的密码转为密文去认证，认证成功返回用户对象，失败则返回None
```

#### 5 登录和注销方法

```python 
from django.contrib import auth
# 该函数接受一个HttpRequest对象，以及一个认证了的User对象。此函数使用django的session框架给某个已认证的用户附加上session id等信息。
auth.login() 
# 该函数接受一个HttpRequest对象，无返回值。当调用该函数时，当前请求的session信息会全部清除。该用户即使没有登录，使用该函数也不会报错。
auth.logout() 
```

#### 6 request.user

````text 
Django有一个默认中间件，叫做AuthenticationMiddleware，每次请求进来都会去session中去一个userid，取不到的话，赋值request.user = AnonymousUser() , 一个匿名用户对象。
当用户组件auth.login一旦执行，将userid到session中后，再有请求进入Django,将注册的userid对应的user对象赋值给request.user，即再后面的任何视图函数中都可以从request.user中取到该客户端的登录对象。
````

#### 7 自定义用户表

> from django.contrib.auth.models import AbstractUser
>
> 设置Auth认证模块使用的用户模型为我们自己定义的用户模型
>
> 格式：“子应用目录名.模型类名”
>
> AUTH_USER_MODEL = 'users.User'

## 3 Django的分页器

> ```python
> from django.core.paginator import Paginator
> ```

![image-20210813175020727](assets/image-20210813175020727.png)

### 1 index视图

```python 
def index(request):
    '''
    批量导入数据:

    Booklist=[]
    for i in range(100):
        Booklist.append(Book(title="book"+str(i),price=30+i*i))
    Book.objects.bulk_create(Booklist)



    分页器的使用:

    book_list=Book.objects.all()                 所有对象

    paginator = Paginator(book_list, 10)        10个为一页面

    print("count:",paginator.count)           #数据总数
    print("num_pages",paginator.num_pages)    #总页数
    print("page_range",paginator.page_range)  #页码的列表



    page1=paginator.page(1) # 第1页的page对象
    for i in page1:         # 遍历第1页的所有数据对象
        print(i)

    print(page1.object_list) #第1页的所有数据


    page2=paginator.page(2)

    print(page2.has_next())            #是否有下一页   True
    print(page2.next_page_number())    #下一页的页码    3
    print(page2.has_previous())        #是否有上一页   True
    print(page2.previous_page_number()) #上一页的页码  1



    # 抛错
    #page=paginator.page(12)   # error:EmptyPage

    #page=paginator.page("z")   # error:PageNotAnInteger

    '''

    book_list = Book.objects.all()

    paginator = Paginator(book_list, 10)
    page = request.GET.get('page', 1)
    current_page = int(page)

    try:
        print(page)
        book_list = paginator.page(page)
    except PageNotAnInteger:
        book_list = paginator.page(1)
    except EmptyPage:
        book_list = paginator.page(paginator.num_pages)

    return render(request, "index.html", {"book_list": book_list, "paginator": paginator, "currentPage": current_page})

```

### 2 index.html

```html 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" 
    integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
</head>
<body>

<div class="container">

    <h4>分页器</h4>
    <ul>

        {% for book in book_list %}
             <li>{{ book.title }} -----{{ book.price }}</li>
        {% endfor %}

     </ul>


    <ul class="pagination" id="pager">

                 {% if book_list.has_previous %}
                    <li class="previous"><a href="/index/?page={{ book_list.previous_page_number }}">上一页</a></li>
                 {% else %}
                    <li class="previous disabled"><a href="#">上一页</a></li>
                 {% endif %}


                 {% for num in paginator.page_range %}

                     {% if num == currentPage %}
                       <li class="item active"><a href="/index/?page={{ num }}">{{ num }}</a></li>
                     {% else %}
                       <li class="item"><a href="/index/?page={{ num }}">{{ num }}</a></li>

                     {% endif %}
                 {% endfor %}



                 {% if book_list.has_next %}
                    <li class="next"><a href="/index/?page={{ book_list.next_page_number }}">下一页</a></li>
                 {% else %}
                    <li class="next disabled"><a href="#">下一页</a></li>
                 {% endif %}

            </ul>
</div>



</body>
</html>
```

## 4 FBV与CBV

> 1 FBV ：function based view
>
> 2 BCV：class based view

### 1、前后端分离模式

在开发Web应用中，有两种应用模式：

1. 前后端不分离[客户端看到的内容和所有界面效果都是由服务端提供出来的。]

![前后端不分离](assets/depended_frontend_backend.png)

2. 前后端分离【把前端的界面效果(html，css，js分离到另一个服务端，python服务端只需要返回数据即可)】

前端形成一个独立的网站，服务端构成一个独立的网站

![](assets/indepent_frontend_backend-16318493319127.png)

### 2、api接口

应用程序编程接口（Application Programming Interface，API接口），就是应用程序对外提供了一个操作数据的入口，这个入口可以是一个函数或类方法，也可以是一个url地址或者一个网络地址。当客户端调用这个入口，应用程序则会执行对应代码操作，给客户端完成相对应的功能。

当然，api接口在工作中是比较常见的开发内容，有时候，我们会调用其他人编写的api接口，有时候，我们也需要提供api接口给其他人操作。由此就会带来一个问题，api接口往往都是一个函数、类方法、或者url或其他网络地址，不断是哪一种，当api接口编写过程中，我们都要考虑一个问题就是这个接口应该怎么编写？接口怎么写的更加容易维护和清晰，这就需要大家在调用或者编写api接口的时候要有一个明确的编写规范！！！

为了在团队内部形成共识、防止个人习惯差异引起的混乱，我们都需要找到一种大家都觉得很好的接口实现规范，而且这种规范能够让后端写的接口，用途一目了然，减少客户端和服务端双方之间的合作成本。

目前市面上大部分公司开发人员使用的接口实现规范主要有：restful、RPC。

RPC（ Remote Procedure Call ）: 翻译成中文:远程过程调用[远程服务调用]. 从字面上理解就是访问/调用远程服务端提供的api接口。这种接口一般以服务或者过程式代码提供。

- 服务端提供一个**唯一的访问入口地址**：http://api.xxx.com/ 或 http://www.xx.com/api 或者基于其他协议的地址

- 客户端请求服务端的时候，所有的操作都理解为动作(action)，一般web开发时，对应的就是HTTP请求的post请求

- 通过**请求体**参数，指定要调用的接口名称和接口所需的参数

  action=get_all_student&class=301&sex=1

  m=get_all_student&sex=1&age=22

  command=100&sex=1&age=22

rpc接口多了,对应函数名和参数就多了,前端在请求api接口时难找.对于年代久远的rpc服务端的代码也容易出现重复的接口

restful: 翻译成中文: 资源状态转换.(表征性状态转移)

- 把服务端提供的所有的数据/文件都看成资源， 那么通过api接口请求数据的操作，本质上来说就是对资源的操作了.

  因此，restful中要求，我们把当前接口对外提供哪种资源进行操作，就把**资源的名称写在url地址**。

- web开发中操作资源，最常见的最通用的无非就是增删查改，所以restful要求在地址栏中声明要操作的资源是什么。然后通过**http请求动词**来说明对该资源进行哪一种操作.

  > POST http://www.xxx.com/api/students/ 添加学生数据
  >
  > GET http://www.xxx.com/api/students/ 获取所有学生
  >
  > GET http://www.xxx.com/api/students/1/ 获取id=pk的学生
  >
  > DELETE http://www.xxx.com/api/students/1/ 删除id=pk的一个学生
  >
  > PUT http://www.xxx.com/api/students/1/ 修改一个学生的全部信息 [id,name,sex,age,]
  >
  > PATCH http://www.xxx.com/api/students/1/ 修改一个学生的部分信息[age]

也就是说，我们仅需要通过url地址上的资源名称结合HTTP请求动作，就可以说明当前api接口的功能是什么了。restful是以资源为主的api接口规范，体现在地址上就是资源就是以名词表达。rpc则以动作为主的api接口规范，体现在接口名称上往往附带操作数据的动作。

### 3、RESTful API规范

![restful](assets/restful.gif)

REST全称是Representational State Transfer，中文意思是表述（编者注：通常译为表征）性状态转移。 它首次出现在2000年Roy Fielding的博士论文中。

RESTful是一种专门为Web 开发而定义API接口的设计风格，尤其适用于前后端分离的应用模式中。

这种风格的理念认为后端开发任务就是提供数据的，对外提供的是数据资源的访问接口，所以在定义接口时，客户端访问的URL路径就表示这种要操作的数据资源。

而对于数据资源分别使用POST、DELETE、GET、UPDATE等请求动作来表达对数据的增删查改。

| GET      | /students  | 获取所有学生       |
| :------- | :--------- | :----------------- |
| 请求方法 | 请求地址   | 后端操作           |
| POST     | /students  | 增加学生           |
| GET      | /students/ | 获取编号为pk的学生 |
| PUT      | /students/ | 修改编号为pk的学生 |
| DELETE   | /students/ | 删除编号为pk的学生 |

restful规范是一种通用的规范，不限制语言和开发框架的使用。事实上，我们可以使用任何一门语言，任何一个框架都可以实现符合restful规范的API接口。

参考文档：http://www.runoob.com/w3cnote/restful-architecture.html

接口实现过程中，会存在**幂等性**。所谓幂等性是指代**客户端发起多次同样请求时，是否对于服务端里面的资源产生不同结果**。如果**多次请求**，服务端**结果**还是**一样**，则属于**幂等接口**，如果多次请求，服务端产生结果是不一样的，则属于**非幂等接口**。

| 请求方式  | 是否幂等 | 是否安全 |
| :-------- | :------- | :------- |
| GET       | 幂等     | 安全     |
| POST      | 不幂等   | 不安全   |
| PUT/PATCH | 幂等     | 不安全   |
| DELETE    | 幂等     | 不安全   |

### 4、CBV使用

之前我们用的视图函数叫FBV（也就是函数型视图函数），这里我们来试试CBV（类视图函数）的写法。类视图函数可以让代码看起来更简洁，用起来更方便。

```python
# FBV
# def index(request):
#     if request.method == "GET":
#
#         return HttpResponse("GET")
#     elif request.method == "POST":
#
#         return HttpResponse("POST")
#
#     elif request.method == "DELETE":
#         return HttpResponse("DELETE")

# CBV模式: 基于restful开发

class IndexView(View):

    def get(self, request):
        return HttpResponse("CBV GET")

    def post(self, request):
        return HttpResponse("CBV POST")


class BookView(View):

    def get(self, request):
        # 获取数据
        book_list = Book.objects.all()

        # 序列化：json
        data_json = serializers.serialize("json", book_list)

        return HttpResponse(data_json, content_type="json")

```

```python 
# FBV模式
# path('index/', views.index),
# CBV模式
path("index/",views.IndexView.as_view()),
path("books/",views.BookView.as_view())
```

## 5 csrftoken（跨站请求伪造）

CSRF（Cross-Site Request Forgery，跨站点伪造请求）是一种网络攻击方式，该攻击可以在受害者毫不知情的情况下以受害者名义伪造请求发送给受攻击站点，从而在未授权的情况下执行在权限保护之下的操作，具有很大的危害性。具体来讲，可以这样理解CSRF攻击：攻击者盗用了你的身份，以你的名义发送恶意请求，对服务器来说这个请求是完全合法的，但是却完成了攻击者所期望的一个操作，比如以你的名义发送邮件、发消息，盗取你的账号，添加系统管理员，甚至于购买商品、虚拟货币转账等。



csrf_token 用于form表单中，作用是跨站请求伪造保护。

```
如果不用 {% csrf_token %} 标签，在用 form 表单时，要再次跳转页面会报 403 权限错误。

用了{% csrf_token %} 标签，在 form 表单提交数据时，才会成功。
```



**解析：**

```
首先，向服务器发送请求，获取登录页面，此时中间件 csrf 会自动生成一个隐藏input标签，该标签里的 value 属性的值是一个随机的字符串，用户获取到登录页面的同时也获取到了这个隐藏的input标签。

然后，等用户需要用到form表单提交数据的时候，会携带这个 input 标签一起提交给中间件 csrf，原因是 form 表单提交数据时，会包括所有的 input 标签，中间件 csrf 接收到数据时，会判断，这个随机字符串是不是第一次它发给用户的那个，如果是，则数据提交成功，如果不是，则返回403权限错误。
```



[参考文章](https://www.pianshen.com/article/62531249043/)

token其实就是一个令牌，用于用户验证的，token的诞生离不开CSRF。正是由于上面的Cookie/Session的状态保持方式会出现CSRF，所以才有了token。

- 解除中间件注释

![img](assets/v2-48184dcedfa833a81ed801e6050f3e3e_1440w.jpg)

- 无csrf_token数据的post请求

![img](assets/v2-77374da1a47fa241039f9fe1e5eadbc1_1440w.jpg)









### 1、基本使用

#### form表单提交

在html页面form表单中直接添加{% csrf_token%}

![屏幕快照 2021-10-31 下午10.30.29](assets/屏幕快照 2021-10-31 下午10.30.29.png)

#### ajax提交

方式1：放在请求数据中。

```js
$.ajax({
  url: '/csrf_test/',
  method: 'post',
  data: {'name': $('[name="name"]').val(),
         'password': $('[name="password"]').val(),
         'csrfmiddlewaretoken':$('[name="csrfmiddlewaretoken"]').val()           
        },
  success: function (data) {
    console.log('成功了')
    console.log(data)           },
})
```

方式2：放在请求头

```js
$.ajax({
            url: '/csrf_test/',
            method: 'post',
            headers:{'X-CSRFToken':'token值'},  // 注意放到引号里面
            data:{}
}
```

### 2、全局使用，局部禁csrf

#### 1 在视图函数上加装饰器

```python 
from django.views.decorators.csrf import csrf_exempt,csrf_protect
@csrf_exempt
def 函数名(request):  # 加上装饰器后,这个视图函数,就没有csrf校验了
```

#### 2视图类

```python
from django.views.decorators.csrf import csrf_exempt,csrf_protect
from django.utils.decorators import method_decorator
@method_decorator(csrf_exempt,name='dispatch')
class index(View):
    def get(self,request):
        return HttpResponse("GET")
    def post(self,request):
        return HttpResponse("POST")
```











## 6 ORM进阶

### 1、queryset特性

#### （1）可切片

使用Python 的切片语法来限制`查询集`记录的数目 。它等同于SQL 的`LIMIT` 和`OFFSET` 子句。

```python
>>> Article.objects.all()[:5]   # (LIMIT 5)
>>> Article.objects.all()[5:10]    # (OFFSET 5 LIMIT 5)
```

不支持负的索引（例如`Article.objects.all()[-1]`）。通常，`查询集` 的切片返回一个新的`查询集` —— 它不会执行查询。

#### （2）可迭代

```python
articleList=models.Article.objects.all()

for article in articleList:
    print(article.title)
```

#### （3）惰性查询

`查询集` 是惰性执行的 —— 创建`查询集`不会带来任何数据库的访问。你可以将过滤器保持一整天，直到`查询集` 需要求值时，Django 才会真正运行这个查询。

```python
queryResult=models.Article.objects.all() # not hits database
print(queryResult) # hits database
for article in queryResult:
    print(article.title)    # hits database
```

 一般来说，只有在“请求”`查询集` 的结果时才会到数据库中去获取它们。当你确实需要结果时，`查询集` 通过访问数据库来*求值*。 关于求值发生的准确时间。

#### （4）缓存机制

每个`查询集`都包含一个缓存来最小化对数据库的访问。理解它是如何工作的将让你编写最高效的代码。

在一个新创建的`查询集`中，缓存为空。首次对`查询集`进行求值 —— 同时发生数据库查询 ——Django 将保存查询的结果到`查询集`的缓存中并返回明确请求的结果（例如，如果正在迭代`查询集`，则返回下一个结果）。接下来对该`查询集` 的求值将重用缓存的结果。

请牢记这个缓存行为，因为对`查询集`使用不当的话，它会坑你的。例如，下面的语句创建两个`查询集`，对它们求值，然后扔掉它们：

```python
queryset = Book.objects.all()
print(queryset) # hit database
print(queryset) # hit database
```

> 注：简单地打印查询集不会填充缓存。

这意味着相同的数据库查询将执行两次，显然倍增了你的数据库负载。同时，还有可能两个结果列表并不包含相同的数据库记录，因为在两次请求期间有可能有Article被添加进来或删除掉。为了避免这个问题，只需保存`查询集`并重新使用它：

```python
queryset = Book.objects.all()
ret = [i for i in queryset] # hit database
print(queryset) # 使用缓存
print(queryset) # 使用缓存
```

何时查询集会被缓存?

> 1. 遍历queryset时
> 2. if语句（为了避免这个，可以用exists()方法来检查是否有数据）

所以单独queryset的索引或者切片都不会缓存。

```python
queryset = Book.objects.all()
one = queryset[0] # hit database
two = queryset[1] # hit database
print(one)
print(two)
```

#### （5）exists()与iterator()方法

##### exists

简单的使用if语句进行判断也会完全执行整个queryset并且把数据放入cache，虽然你并不需要这些 数据！为了避免这个，可以用exists()方法来检查是否有数据：

```python
 if queryResult.exists():
    #SELECT (1) AS "a" FROM "blog_article" LIMIT 1; args=()
        print("exists...")
```

##### iterator

当queryset非常巨大时，cache会成为问题。

处理成千上万的记录时，将它们一次装入内存是很浪费的。更糟糕的是，巨大的queryset可能会锁住系统 进程，让你的程序濒临崩溃。要避免在遍历数据的同时产生queryset cache，可以使用iterator()方法 来获取数据，处理完数据就将其丢弃。

```python
objs = Book.objects.all().iterator()
# iterator()可以一次只从数据库获取少量数据，这样可以节省内存
for obj in objs:
    print(obj.title)
#BUT,再次遍历没有打印,因为迭代器已经在上一次遍历(next)到最后一次了,没得遍历了
for obj in objs:
    print(obj.title)
```

当然，使用iterator()方法来防止生成cache，意味着遍历同一个queryset时会重复执行查询。所以使 #用iterator()的时候要当心，确保你的代码在操作一个大的queryset时没有重复执行查询。

queryset的cache是用于减少程序对数据库的查询，在通常的使用下会保证只有在需要的时候才会查询数据库。 使用exists()和iterator()方法可以优化程序对内存的使用。不过，由于它们并不会生成queryset cache，可能 会造成额外的数据库查询。　

总结:在使用缓存机制还是生成器机制的选择上如果是，数据量大情况主要使用生成器；数据少使用次数多的情况使用缓存机制。

### 2、中介模型

处理类似搭配 pizza 和 topping 这样简单的多对多关系时，使用标准的`ManyToManyField` 就可以了。但是，有时你可能需要关联数据到两个模型之间的关系上。

例如，有这样一个应用，它记录音乐家所属的音乐小组。我们可以用一个`ManyToManyField` 表示小组和成员之间的多对多关系。但是，有时你可能想知道更多成员关系的细节，比如成员是何时加入小组的。

对于这些情况，Django 允许你指定一个中介模型来定义多对多关系。 你可以将其他字段放在中介模型里面。源模型的`ManyToManyField` 字段将使用`through` 参数指向中介模型。对于上面的音乐小组的例子，代码如下：

```python
from django.db import models
 
class Person(models.Model):
    name = models.CharField(max_length=128)
 
    def __str__(self):              # __unicode__ on Python 2
        return self.name
 
class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(Person, through='Membership')
 
    def __str__(self):              # __unicode__ on Python 2
        return self.name
 
class Membership(models.Model):
    person = models.ForeignKey(Person)
    group = models.ForeignKey(Group)
    date_joined = models.DateField()
    invite_reason = models.CharField(max_length=64)
```

既然你已经设置好`ManyToManyField` 来使用中介模型（在这个例子中就是`Membership`），接下来你要开始创建多对多关系。你要做的就是创建中介模型的实例：

```python
>>> ringo = Person.objects.create(name="Ringo Starr")
>>> paul = Person.objects.create(name="Paul McCartney")
>>> beatles = Group.objects.create(name="The Beatles")
>>> m1 = Membership(person=ringo, group=beatles,
...     date_joined=date(1962, 8, 16),
...     invite_reason="Needed a new drummer.")
>>> m1.save()
>>> beatles.members.all()
[<Person: Ringo Starr>]
>>> ringo.group_set.all()
[<Group: The Beatles>]
>>> m2 = Membership.objects.create(person=paul, group=beatles,
...     date_joined=date(1960, 8, 1),
...     invite_reason="Wanted to form a band.")
>>> beatles.members.all()
[<Person: Ringo Starr>, <Person: Paul McCartney>]
```

与普通的多对多字段不同，你不能使用`add`、 `create`和赋值语句（比如，`beatles.members = [...]`）来创建关系：

```python
# THIS WILL NOT WORK
>>> beatles.members.add(john)
# NEITHER WILL THIS
>>> beatles.members.create(name="George Harrison")
# AND NEITHER WILL THIS
>>> beatles.members = [john, paul, ringo, george]
```

为什么不能这样做？ 这是因为你不能只创建 `Person`和 `Group`之间的关联关系，你还要指定 `Membership`模型中所需要的所有信息；而简单的`add`、`create` 和赋值语句是做不到这一点的。所以它们不能在使用中介模型的多对多关系中使用。此时，唯一的办法就是创建中介模型的实例。

 `remove()`方法被禁用也是出于同样的原因。但是`clear()` 方法却是可用的。它可以清空某个实例所有的多对多关系：

```python
>>> # Beatles have broken up
>>> beatles.members.clear()
>>> # Note that this deletes the intermediate model instances
>>> Membership.objects.all()
[]
```

### 3、数据库表反向生成模型类

众所周知，Django较为适合原生开发，即通过该框架搭建一个全新的项目，通过在修改models.py来创建新的数据库表。但是往往有时候，我们需要利用到之前的已经设计好的数据库，数据库中提供了设计好的多种表单。那么这时如果我们再通过models.py再来设计就会浪费很多的时间。所幸Django为我们提供了inspecdb的方法。他的作用即使根据已经存在对的mysql数据库表来反向映射结构到models.py中.

我们在展示django ORM反向生成之前，我们先说一下怎么样正向生成代码。

> 正向生成，指的是先创建model.py文件，然后通过django内置的编译器，在数据库如mysql中创建出符合model.py的表。
>
> 反向生成，指的是先在数据库中create table，然后通过django内置的编译器，生成model代码。

```python
python manage.py inspectdb > models文件名
```



### 4、查询优化

#### select_related()

对于一对一字段（OneToOneField）和外键字段（ForeignKey），可以使用select_related 来对QuerySet进行优化。

select_related 返回一个`QuerySet`，当执行它的查询时它沿着外键关系查询关联的对象的数据。它会生成一个复杂的查询并引起性能的损耗，但是在以后使用外键关系时将不需要数据库查询。

简单说，在对QuerySet使用select_related()函数后，Django会获取相应外键对应的对象，从而在之后需要的时候不必再查询数据库了。

下面的例子解释了普通查询和`select_related()` 查询的区别。

查询id=2的的书籍的出版社名称,下面是一个标准的查询：

```python
# Hits the database.
book= models.Book.objects.get(nid=2)
# Hits the database again to get the related Blog object.
print(book.publish.name)
```

如果我们使用select_related()函数：

```python
books=models.Book.objects.select_related("publish").all()
for book in books:
     #  Doesn't hit the database, because book.publish
     #  has been prepopulated in the previous query.
     print(book.publish.name)
```

多外键查询

这是针对publish的外键查询，如果是另外一个外键呢？让我们一起看下：

```python
book=models.Book.objects.select_related("publish").get(nid=1)
print(book.authors.all())
```

 观察logging结果，发现依然需要查询两次，所以需要改为：

```python
book=models.Book.objects.select_related("publish","").get(nid=1)
print(book.publish)
```

 或者：

```python
book=models.Article.objects
　　　　　　　　　　　　　.select_related("publish")
　　　　　　　　　　　　　.select_related("")
　　　　　　　　　　　　　.get(nid=1)  # django 1.7 支持链式操作
print(book.publish)
```

#### prefetch_related()

对于多对多字段（ManyToManyField）和一对多字段，可以使用prefetch_related()来进行优化。

prefetch_related()和select_related()的设计目的很相似，都是为了减少SQL查询的数量，但是实现的方式不一样。后者是通过JOIN语句，在SQL查询内解决问题。但是对于多对多关系，使用SQL语句解决就显得有些不太明智，因为JOIN得到的表将会很长，会导致SQL语句运行时间的增加和内存占用的增加。若有n个对象，每个对象的多对多字段对应Mi条，就会生成Σ(n)Mi 行的结果表。

prefetch_related()的解决方法是，分别查询每个表，然后用Python处理他们之间的关系。

```python
# 查询所有文章关联的所有标签
books=models.Book.objects.all()
for book in books:
  	print(book.authors.all())  #4篇文章: hits database 5
```

改为prefetch_related：

```python
# 查询所有文章关联的所有标签
books=models.Book.objects.prefetch_related("authors").all()
for book in books:
  	print(book.authors.all())  #4篇文章: hits database 2
```

#### extra

```python
extra(select=None, where=None, params=None, 
      tables=None, order_by=None, select_params=None)
```

有些情况下，Django的查询语法难以简单的表达复杂的 `WHERE` 子句，对于这种情况, Django 提供了 `extra()` `QuerySet`修改机制 — 它能在 `QuerySet`生成的SQL从句中注入新子句

extra可以指定一个或多个 `参数`,例如 `select`, `where` or `tables`. 这些参数都不是必须的，但是你至少要使用一个!要注意这些额外的方式对不同的数据库引擎可能存在移植性问题.(因为你在显式的书写SQL语句),除非万不得已,尽量避免这样。

##### 参数之select

The `select` 参数可以让你在 `SELECT` 从句中添加其他字段信息，它应该是一个字典，存放着属性名到 SQL 从句的映射。

```
queryResult=models.Article
　　　　　　　　　　　.objects.extra(select={'is_recent': "create_time > '2017-09-05'"})
```

结果集中每个 Entry 对象都有一个额外的属性is_recent, 它是一个布尔值，表示 Article对象的create_time 是否晚于2017-09-05.

##### 参数之`where` / `tables`

您可以使用`where`定义显式SQL `WHERE`子句 - 也许执行非显式连接。您可以使用`tables`手动将表添加到SQL `FROM`子句。

`where`和`tables`都接受字符串列表。所有`where`参数均为“与”任何其他搜索条件。

举例来讲：

```python
queryResult=models.Article
　　　　　　　　　　　.objects.extra(where=['nid in (3，4) OR title like "py%" ','nid>2'])
```

## 7 上传文件

### 1、form表单上传文件

```html
<h3>form表单上传文件</h3>


<form action="/upload_file/" method="post" enctype="multipart/form-data">
    <p><input type="file" name="upload_file_form"></p>
    <input type="submit">
</form>

```

```python
def index(request):
    return render(request,"index.html")

def upload_file(request):
    print("FILES:",request.FILES)
    print("POST:",request.POST)
    return HttpResponse("上传成功!")
```

### 2、Ajax(基于FormData)

FormData是什么呢？

XMLHttpRequest Level 2添加了一个新的接口`FormData`.利用`FormData对象`,我们可以通过JavaScript用一些键值对来模拟一系列表单控件,我们还可以使用XMLHttpRequest的`send()`方法来异步的提交这个"表单".比起普通的ajax,使用`FormData`的最大优点就是我们可以异步上传一个二进制文件.

所有主流浏览器的较新版本都已经支持这个对象了，比如Chrome 7+、Firefox 4+、IE 10+、Opera 12+、Safari 5+。

```html
<h3>Ajax上传文件</h3>

<p><input type="text" name="username" id="username" placeholder="username"></p>
<p><input type="file" name="upload_file_ajax" id="upload_file_ajax"></p>

<button id="upload_button">提交</button>
{#注意button标签不要用在form表单中使用#}

<script>
    $("#upload_button").click(function(){

        var username=$("#username").val();
        var upload_file=$("#upload_file_ajax")[0].files[0];

        var formData=new FormData();
        formData.append("username",username);
        formData.append("upload_file_ajax",upload_file);


        $.ajax({
            url:"/upload_file/",
            type:"POST",
            data:formData,
            contentType:false,
            processData:false,

            success:function(){
                alert("上传成功!")
            }
        });


    })
</script>

```

```python
def index(request):
  
    return render(request,"index.html")
  
  
def upload_file(request):
    print("FILES:",request.FILES)
    print("POST:",request.POST)
    return HttpResponse("上传成功!")
```

### 3、ImageField 和 FileField

ImageField 和 FileField 可以分别对图片和文件进行上传到指定的文件夹中。

1. 在下面的 models.py 中 ：

picture = models.ImageField(upload_to='avatars/', default="avatars/default.png",blank=True, null=True) 注:定义 ImageField 字段时必须制定参数 upload_to这个字段要写相对路径，

这个参数会加在 settings.py 中的 MEDIA_ROOT后面, 形成一个路径, 这个路径就是上 传图片的存放位置，默认在Django项目根路径下，也就是MEDIA_ROOT默认是Django根目录

所以要先设置好 mysite/settings.py中的 settings.py 中的 MEDIA_ROOT

```python
class Userinfo(models.Model):
    name = models.CharField(max_length=32)
    avatar_img = models.FileField("avatars/") 
```

```python
username = request.POST.get("username")
#获取文件对象
file = request.FILES.get("file")   
#插入数据，将图片对象直接赋值给字段
user = Userinfo.objects.create(name=username,avatar_img=file)
```

Django会在项目的根目录创建avatars文件夹，将上传文件下载到该文件夹中，avatar字段保存的是文件的相对路径。

2. 在 mysite/settings.py中 :

```python
MEDIA_ROOT = os.path.join(BASE_DIR,"media")
MEDIA_URL='/media/'
```

> MEDIA_ROOT:存放 media 的路径, 这个值加上 upload_to的值就是真实存放上传图片文件位置
>
> MEDIA_URL:给这个属性设值之后,静态文件的链接前面会加上这个值，如果设置这个值，则UserInfo.avatar.url自动替换成：/media/avatars/default.png，可以在模板中直接调用：<img src="{{ user.avatar.url }}" alt="">。

3.url.py:

```python
from django.views.static import serve
# 添加media 配置
re_path(r'^media/(?P<path>.*)$', serve, {'document_root': settings.MEDIA_ROOT}),
```

浏览器可以直接访问http://127.0.0.1:8000/media/yuan/avatars/%E7%86%8A%E7%8C%AB.webp，即我们的用户上传文件。

最后再给大家补充一个用户文件夹路径

```python
def user_directory_path(instance, filename):
    return os.path.join(instance.name,"avatars", filename)

class Userinfo(models.Model):
    name = models.CharField(max_length=32)
    avatar_img = models.FileField(upload_to=user_directory_path)  

```

4.FileField 和 ImageFiled 相同。

### 4、导入表格批量创建数据

```python
# Create your tests here.
def multi_create(request):
    # 将接受到的excel文件转到mysql
    # （1）下载文件到服务器

    emp_excel = request.FILES.get("emp_excel")
    print(emp_excel) # 期末题目（陕西联通）.xlsx
    print(emp_excel.name) # "期末题目（陕西联通）.xlsx"
    # 下载文件
    with open("files/"+emp_excel.name,"wb") as f:

        for line in emp_excel:
            f.write(line)


    # 读取excel，批量导入到mysql中

    import os
    from openpyxl import load_workbook
    file_path = os.path.join("files",emp_excel.name)

    # 加载某一个excel文件
    wb = load_workbook(file_path)
    # 获取sheet对象
    print("wb.sheetnames",wb.sheetnames)
    worksheet = wb.worksheets[0]

    for row in worksheet.iter_rows(min_row=3):
        print(row)
        if row[0].value == None:
            break
        Employee.objects.create(name=row[0].value,
                                age=row[1].value,
                                ruzhi_date=row[2].value,
                                dep=row[3].value,
                                salary=row[4].value,
                                )



    return redirect("/index/")
```





## 8  forms组件

**概念：**django框架提供了一个Form类，来进行web开发中的表单提交数据的处理工作。

### forms校验功能

```python
   form=UserForm(request.POST)
    # 实例化用户表单的字典数据
```

#### 验证是否通过

```python
form.is_valid()
# 返回True:通过验证
# 返回False:为不通过验证
```

#### 获取表单数据，通过

```python
form.cleaned_data
# 返回验证通过的键值，不在UserForm类里面的字段会无视
```

#### 获取表单数据，不通过

```python
form.errors
# 返回的是字典格式 键是字段名，值是个列表，内放验证失败的错误信息
# 取错误信息用get取某个字段，在用[0]取列表内信息
```



#### 使用步骤

 1 创建表单类(可以直接在views.py文件中创建，也可以自己再新建一个forms.py的模块，然后写到这个模块下

```python
#使用表单首先导入forms类
from django import forms
from django.forms import widgets

class UserForm(forms.Form):
    name = forms.CharField(max_length=32, widget=widgets.TextInput,label="用户名" )
    pwd = forms.CharField(max_length=32, widget=widgets.PasswordInput)
    r_pwd = forms.CharField(max_length=32, widget=widgets.PasswordInput)
    email = forms.EmailField(widget=widgets.EmailInput)
    tel = forms.CharField(max_length=32, widget=widgets.TextInput)
```

模板: register.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

</head>
<body>

<form action="" method="post">
    {% csrf_token %}
    <div>
        <label for="user">用户名</label>
        <p><input type="text" name="name" id="name"></p>
    </div>
    <div>
        <label for="pwd">密码</label>
        <p><input type="password" name="pwd" id="pwd"></p>
    </div>
    <div>
        <label for="r_pwd">确认密码</label>
        <p><input type="password" name="r_pwd" id="r_pwd"></p>
    </div>
     <div>
        <label for="email">邮箱</label>
        <p><input type="text" name="email" id="email"></p>
    </div>
    <input type="submit">
</form>

</body>
</html>
```



2 在views.py里定义访问函数

```python
from django.shortcuts import render
from .forms import UserForm   		#导入自定义的表单
    
# 业务函数
def register(request):
    if request.method=="POST":
        form=UserForm(request.POST)  		# 实例化forms类，传入对应的字典键值对，值与设置的格式都对上返回回True
        if form.is_valid():				   # form.is_valid()方法返回True,或False
            print(form.cleaned_data)       # 所有正确的字段以及对应的值
        else:
            print(form.cleaned_data)       #
            print(form.errors)             # ErrorDict : {"校验错误的字段":["错误信息",]}
            print(form.errors.get("name")) # ErrorList ["错误信息",]
        return HttpResponse("OK")
    
    form=UserForm()						
    return render(request,"register.html",locals())
```



### forms渲染功能

1. 生成模板文件的input标签
2. 可以自定义字段名的中文名，用于模板中循环生成input标签时有输入备注，如用户名，密码
3. 用户输入不合规则时，符合的会当成value值传入模板，用户合规则的内容就不用在重新输入
4. 可以把用户的错误信息，渲染到模板中，无错误时隐藏。

 views.py

```python
from django.shortcuts import render
from .forms import UserForm   					#导入自定义的表单
# 业务函数
def register(request):
    if request.method=="POST":
        form=UserForm(request.POST)  			# 实例化forms类，传入对应的字典键值对，值与设置的格式都对上返回回True
        if form.is_valid():				   	    # form.is_valid()方法返回True,或False
            print(form.cleaned_data)       		 # 所有正确的字段以及对应的值
            # 进行验证通过的处理
        else:
            print(form.errors)             		 # ErrorDict : {"校验错误的字段":["错误信息",]}
            print(form.errors.get("name")) 		 # ErrorList ["错误信息",]
            
            # 这里传入的form是有值的对象，会有用户输入符合规则的内容和错误的信息
        	return render(request,"register.html",locals()) 
    
    form=UserForm()			  					# get请求时传入form对象用于循环生成input标签			
    return render(request,"register.html",locals())
```

register.html模板

```html
<form action="" method="post" novalidate> 				<!-- form头要手写 -->
    {% csrf_token %}
    
    {% for field in form %}						  	   <!-- 循环传入的form对象，每个循环就是每个字段 -->
        <div>
            <label for="">{{ field.label }}</label>	     <!-- 字段.label就是自定义的中文名 -->
            
            <!-- 每个field会生成对应input标签,type属性根据字段设置的生成   -->
            {{ field }} <span class="pull-right" style="color: red">{{ field.errors.0 }}</span>
            <!-- 在每个标签后可以调用错误信息{{ field.errors.0 }}，有错误时才显示 -->
        </div>
    {% endfor %}
    <input type="submit" class="btn btn-default">

</form>
```



### forms参数配置

1. 设置标签的type类型: `widget=widgets.PasswordInput`
2. 设置中文字段名:  `label="自定义"`
3. 设置自定义的错误信息显示: `error_messages={"required":"此字段不可空"}` 
4. 设置模板内标签的属性值：设置完type类型后在（）内 `attrs={"属性名":"属性值"}`

```python
#使用表单首先导入forms类
from django import forms
from django.forms import widgets # 导入类

class UserForm(forms.Form):    
    name = forms.CharField(max_length=32, widget=widgets.TextInput(),label="用户名" )        # 1 2
    pwd = forms.CharField(max_length=32, error_messages={"required":"此字段不可空"}           # 3
    r_pwd = forms.CharField(max_length=32, widget=widgets.PasswordInput())    
    email = forms.EmailField(widget=widgets.EmailInput())    
    tel = forms.CharField(max_length=32, widget=widgets.TextInput(attrs={"属性名":"属性值"}))  # 4
	
```





### forms局部钩子

**自定义用户输入的数据验证规则，只能取到一个字段和只验证一个字段**

```python
from django import forms
from django.forms import widgets 						# 导入类型类
from django.core.exceptions import ValidationError  	  # 1 引入一个错误

class UserForm(forms.Form):    
    name = forms.CharField(max_length=32, widget=widgets.TextInput,label="用户名" )    
    pwd = forms.CharField(max_length=32, widget=widgets.PasswordInput,error_messages={"required":"此字段不可空"}  
    r_pwd = forms.CharField(max_length=32, widget=widgets.PasswordInput)    
    email = forms.EmailField(widget=widgets.EmailInput)    
    tel = forms.CharField(max_length=32, widget=widgets.TextInput)
                          
    def clean_name(self):							   # 2 创建一个类方法，方法名必须 clean_字段名(self):
        val = self.cleaned_data.get("name")   			 # 3 取到用户输入的值
        if val:										  # 4 此处做逻辑判断
              return val							   # 5 无问题返回原来的值
        else:
              raise ValidationError("值不可为空")		 # 6 有问题抛出错误
```





### forms全局钩子

**每个字段都校验完后都会走的方法，所以可以取所有字段来进行自定义验证**

```python
from django import forms
from django.forms import widgets 						# 导入类型类
from django.core.exceptions import ValidationError  	  # 1 引入一个错误

class UserForm(forms.Form):    
    name = forms.CharField(max_length=32, widget=widgets.TextInput,label="用户名" )    
    pwd = forms.CharField(max_length=32, widget=widgets.PasswordInput,error_messages={"required":"此字段不可空"}  
    r_pwd = forms.CharField(max_length=32, widget=widgets.PasswordInput)    
    email = forms.EmailField(widget=widgets.EmailInput)    
    tel = forms.CharField(max_length=32, widget=widgets.TextInput)
                  
                          
    def clean(self):				        		  # 2 创建一个clean方法，self.cleaned_data有所有的规则过滤后的值
       pwd = self.cleaned_data.get("pwd") 			 	
       r_pwd = self.cleaned_data.get("r_pwd")  		    # 3 取两个字段的值
                          
          if pwd and r_pwd:							  # 4 先判断值是否空，空就是前面规则没过，直接返回原数据
              if pwd == r_pwd:						  # 5 做对应的逻辑判断操作
                 return self.cleaned_data			   # 6 判断符合就返回原数据
              else:
                  raise ValidationError("两次密码不一致")# 7 不符合就抛出错误，放在错误信息的__all__键里        
           else:
               return self.cleaned_data                      
```

views.py

```python
from django.shortcuts import render
from .forms import UserForm 

def register(request):
    if request.method=="POST":
       form=UserForm(request.POST)  	
    
       _all = form.errors.get("__all__")[0]         # 8 全局的错误的键名是__all__,把取到的错误在传入模板
       return render(request,"register.html",locals()) 
    form=UserForm()			  							
    return render(request,"register.html",locals())
```

```html
<form action="" method="post" novalidate> 			
    {% csrf_token %}
    {% for field in form %}						  	
        <div>
            <label for="">{{ field.label }}</label>	     
            {{ field }} <span class="pull-right" style="color: red">{{ field.errors.0 }}</span>
            <span class="pull-right" style="color: red">{{ _all }}</span> <!-- 9 在原有的错误基础上加个全局错误 -->
        </div>
    {% endfor %}
    <input type="submit" class="btn btn-default">

</form>
```









## 9 modelForm组件

在写[表单](https://so.csdn.net/so/search?q=表单&spm=1001.2101.3001.7020)的时候，会发现表单中的Field和模型中的Field基本上是一模一样的。而且一般情况下表单中需要验证的数据就是我们模型中需要保存的数据。那么这个时候我们就可以将模型中的字段和表单中的字段进行绑定。

modelform是一个神奇的组件，通过名字我们可以看出来，这个组件的功能就是把model和form组合起来。

比如我们的数据库中有这样一张学生表，字段有姓名，年龄，爱好，邮箱，电话，住址，注册时间等等一大堆信息，现在让你写一个创建学生的页面，你的后台应该怎么写呢？

* 前端：首先会在前端一个一个罗列出这些字段，让用户去填写，然后后台一个一个接收用户的输入
* 后台：定义一个学生模型，用来保存学生信息
* 后台：定义一个学生表单，用来验证前端传递过来的数据
* 后台：在视图函数中使用get()方法来一个一个的获取已通过验证的数据，然后使用模型中的QuerySet方法将数据保存起来

在上面示例中：其实表单的定义和模型的定义其实是差不多的，但是如果按照上面这种方式来的话，一个差不多的东西我们就需要完整的定义两边，这样就显得混麻烦了。因此Django就提供了ModelForm组件：这个组件主要就是用来整合表单和模型，将它们两个连接起来使用。就不需要完整的定义两次了。

### `Form`组件和`ModelForm`区别

1. `ModelForm`是`Django Model.py`和`Form`组件的结合体，可以简单、快速使用 Form验证和数据库操作功能，但不如Form组件灵活
2. 如果在使用`Django`做web开发过程中验证的数据和数据库字段相关(可以对表进行增、删、改操)，建议优先使用`ModelForm`，用起来更方便些。
3. `ModelForm`适合中小型应用程序。因为`ModelForm`是依赖于models的。而Form更适合大型应用程序。`Django`中Model负责操作数据库，并且具有简单的数据库验证功能(基本不用)；Form用于用户请求的验证，具有强悍的数据库验证功能；`ModelForm`是将二者合二为一，即可用于数据库操作(部分)，也可用于用户请求的验证(部分)。但由于`ModelForm`的耦合性太强，其作用一般用作于结构简单的小站点



### ModelForm类的创建使用

 `models.py`

```python
from django.db import models											# 1 创建模型类

class Student(models.Model):
    name = models.CharField(max_length=5)
    age = models.IntegerField()
    birth = models.DateField()
    email = models.EmailField()
    createDate = models.DateField(auto_now_add=True)
```

### Meta类的属性

![image-20220406140606130](Django.assets/image-20220406140606130-16492251673611.png)

`forms.py`

```python
from app01.models import Student
from django.forms import ModelForm									# 2 导入创建的模型类及ModelForm类
from django.forms import widgets as wid  							# widgets用法的模块 因为重名，所以起个别名

class StudentModelForm(ModelForm):									# 3 创建类继承ModelForm类
    class Meta:													  # 4 类下在创建固定 Meta名的类，在类中做相应操作
        # 对应的Model中的哪个类校验
        model = Student  	
        
        # 对模型类中哪个字段校验，如果是 fields = "__all__" ,就是表示列出所有的字段校验
        fields =["name","age","email","birth"]
        
        #对模型类中哪个字段不校验
        exclude = ["createDate"]											  

        # 自定义错误信息 name = 字段; 
        error_messages = {'name': {'required': "用户名不能为空"},}
        
        # 自定义字段标签的属性
        widgets = {"birthday": wid.Input(attrs={"type": "date", 'class': 'form-control'}),}
        
        # labels，自定义在前端显示的名字
        labels = {"name": "用户名",}
        
        # 局部校验,局部钩子
        def clean_name(self):
            pass
```







### 设置错误信息全局为中文

设置后所有input框的错误信息都会翻译成中文

在设置settings.py中，把 LANGUAGE_CODE = 'en-us' 的 'en-us' 改成'zh-hans'

![image-20220612152329144](Django.assets/image-20220612152329144.png)



### 标签class属性全局设置

对于每个字段设置一次class会重复许多操作，对于通用的可以设置成全局

![image-20220612154243593](Django.assets/image-20220612154243593.png)

```python
class UpdateUserModelForm(forms.ModelForm):
    class Meta:
        model = models.UserInfo
        fields = ['name', 'email', ]

    def __init__(self, *args, **kwargs):
        super(UpdateUserModelForm, self).__init__(*args, **kwargs)
        # 统一给ModelForm生成字段添加样式
        for name, field in self.fields.items():
            field.widget.attrs['class'] = 'form-control'

```









### ModelForm的添加数据库

`views.py`

```python
from forms import StudentModelForm								# 5 导入创建的ModelForm类StudentModelForm
# 添加的业务函数
def addstus(request):
    
    if request.method == "GET":
        # 6 实例化类生成 studentModelFormObj对象 传入模板，模板内就可调用生成input标签，模板内操作参forms渲染功能
        studentModelFormObj = StudentModelForm() 
        
        return render(request, "addstu.html", {"studentModelFormObj": studentModelFormObj})
    else:
      	# 7 对用户提交的数据实例化生成 studentModelFormObj 对象
        studentModelFormObj = StudentModelForm(data=request.POST)
       
    	# 8 对象.is_valid(): 验证用户输入是否合规则
        if studentModelFormObj.is_valid():
          	
            # 9 对象.save() 把本条用户输入的数据 create() 新增到数据库
            studentModelFormObj.save()
            return HttpResponse("添加成功！")
        else:
            return JsonResponse(studentModelFormObj.errors)
```

### ModelForm的编辑数据库

`views.py`

```python
# 修改的业务函数
def editstus(request,id):
    instance = Student.objects.get(pk=1)                           # 10 创建要修改的学生对象
    
    if request.method == "GET":
        
        # 11 创建传入学生对象的实例对象传给模板，模板内渲染的input标签的value值就会有此学生的数据
        studentModelFormObj = StudentModelForm(instance=instance)  
        
        return render(request, "editstu.html", {"studentModelFormObj": studentModelFormObj,"instance":instance})
    else:
        
     	# 12 实例化ModelForm类时，有instance=学生对象的参数，生成的对象.save()方法就会取用户输入的数据进行 update 修改
        studentModelFormObj = StudentModelForm(instance=instance,data=request.POST)
       
        if studentModelFormObj.is_valid():
		    studentModelFormObj.save()							# 13 校验用户输入合规则后进行修改
             return HttpResponse("编辑成功！")
        else:
            return JsonResponse(studentModelFormObj.errors)
```







## 10 Admin 管理工具

Django 提供了基于 web 的管理工具。

Django 自动管理工具是 django.contrib 的一部分。你可以在项目的 settings.py 中的 INSTALLED_APPS 看到它：

**/HelloWorld/HelloWorld/settings.py 文件代码：**

```python
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
)
```

django.contrib是一套庞大的功能集，它是Django基本代码的组成部分。

------

### 激活管理工具

通常我们在生成项目时会在 urls.py 中自动设置好，我们只需去掉注释即可。

配置项如下所示：

**/HelloWorld/HelloWorld/urls.py 文件代码：**

```python
# urls.py
from django.conf.urls import url
from django.contrib import admin
 
urlpatterns = [
    url(r'^admin/', admin.site.urls),
]
```

当这一切都配置好后，Django 管理工具就可以运行了。

------

### 使用管理工具

启动开发服务器，然后在浏览器中访问 http://127.0.0.1:8000/admin/，得到如下界面：

![img](https://www.runoob.com/wp-content/uploads/2015/01/admin1.png)

你可以通过命令 **python manage.py createsuperuser** 来创建超级用户，如下所示：

```python
# python manage.py createsuperuser
Username (leave blank to use 'root'): admin
Email address: admin@runoob.com
Password:
Password (again):
Superuser created successfully.
[root@solar HelloWorld]#
```

之后输入用户名密码登录，界面如下：

![img](https://www.runoob.com/wp-content/uploads/2015/01/A995340B-8F8C-4777-9B79-846B6A34508A.jpg)

为了让 admin 界面管理某个数据模型，我们需要先注册该数据模型到 admin。比如，我们之前在 TestModel 中已经创建了模型 Test 。修改 TestModel/admin.py:

**HelloWorld/TestModel/admin.py: 文件代码：**

```python
from django.contrib import admin
from TestModel.models import Test
 
# Register your models here.
admin.site.register(Test)
```

刷新后即可看到 Testmodel 数据表:

![img](https://www.runoob.com/wp-content/uploads/2015/01/05F45176-FD08-4DD3-B17C-5759C7EBF515.jpg)

------

### 复杂模型

管理页面的功能强大，完全有能力处理更加复杂的数据模型。

先在 TestModel/models.py 中增加一个更复杂的数据模型：

HelloWorld/TestModel/models.py: 文件代码：

```python
from django.db import models
 
# Create your models here.
class Test(models.Model):
    name = models.CharField(max_length=20)
 
class Contact(models.Model):
    name   = models.CharField(max_length=200)
    age    = models.IntegerField(default=0)
    email  = models.EmailField()
    def __unicode__(self):
        return self.name
 
class Tag(models.Model):
    contact = models.ForeignKey(Contact, on_delete=models.CASCADE,)
    name    = models.CharField(max_length=50)
    def __unicode__(self):
        return self.name
```

这里有两个表。Tag 以 Contact 为外部键。一个 Contact 可以对应多个 Tag。

我们还可以看到许多在之前没有见过的属性类型，比如 IntegerField 用于存储整数。

![img](https://www.runoob.com/wp-content/uploads/2015/01/admin4.png)

在 TestModel/admin.py 注册多个模型并显示：

**HelloWorld/TestModel/admin.py: 文件代码：**

```python
from django.contrib import admin
from TestModel.models import Test,Contact,Tag
 
# Register your models here.
admin.site.register([Test, Contact, Tag])
```

刷新管理页面，显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2015/01/30A3C1A0-B31D-4E98-B129-D3F64BE3D5F4.jpg)

在以上管理工具我们就能进行复杂模型操作。











## 11 Formset表单集合

### 一、Formset简介

Formset（表单集）是多个表单的集合。Formset在Web开发中应用很普遍，它可以让用户在同一个页面上提交多张表单，一键添加多个数据，比如一个页面上添加多个用户信息。

Django针对不同的formset提供了三种方法：formset_factory、modelformset_factory和inlineformset_factory。

### 二、formset_factory

对于继承forms.Form的自定义表单，我们可以使用formset_factory。

```python
# forms.py
from django.forms import formset_factory
from django import forms

class BookForm(forms.Form):
    name = forms.CharField(max_length=100)
    title = forms.CharField()
    pub_date = forms.DateField(required=False) 

BookFormSet = formset_factory(BookForm, extra=3, max_num=2)

# extra: 想要显示空表单的数量
# max_num: 表单显示最大数量，可选，默认1000
```

在视图文件views.py里，我们可以像使用form一样使用formset

```python
# views.py - formsets example.
from .forms import BookFormSet
from django.shortcuts import render

def manage_books(request):
    if request.method == 'POST':
        formset = BookFormSet(request.POST)
        if formset.is_valid():
            # do something with the formset.cleaned_data
            pass
    else:
        formset = BookFormSet()
        #如果想传入初始数据可设置initial = [{'name':'python','pub_date':'北京出版社'}]
    return render(request, 'manage_books.html', {'formset': formset})
```

**注意：**如果使用了 `initial` 来显示formset，那么您需要在处理formset提交时传入相同的 `initial` ，以便formset检测用户更改了哪些表单。例如，您可能有这样的： `BookFormSet(request.POST, initial=[...])`。

模板里可以这样使用formset：

```html
<form action=”.” method=”POST”>
{{ formset }}
</form>
```

也可以这样使用：

```html
<form method="post">
    {{ formset.management_form }}   #一定要加这行代码
    <table>
        {% for form in formset %}
        {{ form }}
        {% endfor %}
    </table>
</form>
```

formset_factory()参数解释：

1、如果 `max_num` 的值大于初始数据现有数量，那空白表单可显示的数量取决于 `extra` 的数量，只要总表单数不超过 `max_num` 。例如， `extra=2` ， `max_num=2` 并且formset有一个 `initial` 初始化项，则会显示一张初始化表单和一张空白表单。

2、如果初始数据项的数量超过 `max_num` ，那么 `max_num` 的值会被无视，所有初始数据表单都会显示，并且也不会有额外的表单显示。例如，假设 `extra=3` ， `max_num=1` 并且formset有两个初始化项，那么只会显示两张有初始化数据的表单。

`3、max_num` 的值 `None` (默认值)，它限制最多显示(1000)张表单，其实这相当于没有限制。

### 三、modelformset_factory

Formset也可以直接由模型model创建，这时你需要使用modelformset_factory。可以指定需要显示的字段和表单数量。由ModelForm创建formset：

```python
from django.forms import modelformset_factory
from myapp.models import StudentStudyRecord						# 传入一个模型类
class StudentStudyRecordModelForm(forms.ModelForm):
    class Meta:
        model=StudentStudyRecord                # 模型类
        fields=["score","homework_note"]	    # 字段
        									 
model_formset_cls = modelformset_factory (model=StudentStudyRecord,form=StudentStudyRecordModelForm,extra=0)
                  							# 实例化出modelformset	
```

views.py

```python
class RecordScoreView(View):
    def get(self, request,class_study_record_id):
        # 实例出model_formset
        model_formset_cls = modelformset_factory(model=StudentStudyRecord,form=StudentStudyRecordModelForm,extra=0)
        # 取出一条对象
        queryset = StudentStudyRecord.objects.filter(classstudyrecord=class_study_record_id)
        # 把对象传入
        formset = model_formset_cls(queryset=queryset)
        return render(request,"student/record_score.html",locals())
    
    def post(self, request,class_study_record_id):
        # 实例出model_formset
        model_formset_cls = modelformset_factory(model=StudentStudyRecord, form=StudentStudyRecordModelForm, extra=0)# 传入用户输入的数据
        formset=model_formset_cls(request.POST)
		# 验证用户输入格式
        if formset.is_valid():
            # 无误保存
            formset.save()

        return redirect(request.path)
```

模板：

```html
　　　　　　　　<form method="post" action="">
                    {% csrf_token %}
                    {{ formset.management_form }}
                    <table class="table table-bordered">
                        <thead>
                        <tr>
                            <th>姓名</th>
                            <th>考勤</th>
                            <th>作业成绩</th>
                            <th>作业评语</th>
                        </tr>
                        </thead>
                        <tbody>
                        {% for form in formset %}
                            <tr>
                                {{ form.id }}
                                <td>{{ form.instance.student }}</td>
                                <td>{{ form.instance.get_record_display }} </td>
                                <td>{{ form.score }} </td>
                                <td>{{ form.homework_note }}</td>
                            </tr>
                        {% endfor %}
                        </tbody>
                    </table>
                    <input type="submit" value="保存">
                </form>
```

### 四、inlineformset_factory

试想我们有如下recipe（菜谱）模型，Recipe（菜谱）与Ingredient（原料）是一对多的关系。一般的formset只允许我们一次性提交多个Recipe或多个Ingredient。但如果我们希望同一个页面上添加一个菜谱(Recipe)和多个原料(Ingredient)，这时我们就需要用使用inlineformset了。

```python
from django.db import models

class Recipe(models.Model):
    title = models.CharField(max_length=255)
    description = models.TextField()

class Ingredient(models.Model):
    recipe = models.ForeignKey(Recipe, on_delete=models.CASCADE, related_name='ingredient')
    name = models.CharField(max_length=255)
```

利用inlineformset_factory创建formset的方法如下所示。该方法的第一个参数和第二个参数都是模型，其中第一个参数必需是ForeignKey。

```python
# forms.py
from django.forms import ModelForm
from django.forms import inlineformset_factory
from .models import Recipe, Ingredient, Instruction

class RecipeForm(ModelForm):
    class Meta:
        model = Recipe
        fields = ("title", "description",)
IngredientFormSet = inlineformset_factory(Recipe, Ingredient, fields=('name',)
                                          ,extra=3, can_delete=False, max_num=5)
```

views.py中使用formset创建和更新recipe（菜谱）的代码如下。在对IngredientFormSet进行实例化的时候，必需指定recipe的实例。

```python
def recipe_update(request, pk):       #更新
    recipe = get_object_or_404(Recipe, pk=pk)
    if request.method == "POST":
        form = RecipeForm(request.POST, instance=recipe)
        if form.is_valid():
            recipe = form.save()
            ingredient_formset = IngredientFormSet(request.POST, instance=recipe)
            if ingredient_formset.is_valid():
                ingredient_formset.save()     
        return redirect('/recipe/')
    else:
        form = RecipeForm(instance=recipe)
        ingredient_formset = IngredientFormSet(instance=recipe)

    return render(request, 'recipe/recipe_update.html', {'form': form, 'ingredient_formset': ingredient_formset,})


def recipe_add(request):      #创建
    if request.method == "POST":
        form = RecipeForm(request.POST)
        if form.is_valid():
            recipe = form.save()
            ingredient_formset = IngredientFormSet(request.POST, instance=recipe)
            if ingredient_formset.is_valid():
                ingredient_formset.save()
        return redirect('/recipe/')
    
    else:
        form = RecipeForm()
        ingredient_formset = IngredientFormSet()
    return render(request, 'recipe/recipe_add.html', {'form': form, 'ingredient_formset': ingredient_formset,})
```

模板recipe/recipe_add.html代码如下：

```html
<h1>Add Recipe</h1>
<form action="." method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <fieldset>
        <legend>Recipe Ingredient</legend>
        {{ ingredient_formset.management_form }}
        {{ ingredient_formset.non_form_errors }}
        {% for form in ingredient_formset %}
                {{ form.name.errors }}
                {{ form.name.label_tag }}
                {{ form.name }}
            </div>
      {% endfor %}
    </fieldset>
    <input type="submit" value="Add recipe" class="submit" />
</form>
```

### 整个formset的验证

formset由多个表单组成，单个表单的验证可以通过自定义的clean方法来完成，然而有时我们需要对整个formset的数据进行验证。一个常见例子就是去重。

比如下面例子中用户一次性提交多篇文章标题后，我们需要检查title是否已重复。我们先定义一个BaseFormSet，然后使用formset=BaseArticleFormSet添加formset的验证。

```python
from django.forms import BaseFormSet
from django.forms import formset_factory
from myapp.forms import ArticleForm
 
class BaseArticleFormSet(BaseFormSet):
    def clean(self):
        """检查两篇文章的标题是否相同。"""
		if any(self.errors):
            return
 
        titles = []
        for form in self.forms:
            title = form.cleaned_data['title']
            if title in titles:
                raise forms.ValidationError("集合中的文章必须具有不同的标题。")
        titles.append(title)
 
ArticleFormSet = formset_factory(ArticleForm, formset=BaseArticleFormSet)
```

给Formset添加额外字段

在BaseFormSet里我们不仅可以添加formset的验证，而且可以添加额外的字段，如下所示:

```python
from django.forms import BaseFormSet
from django.forms import formset_factory
from myapp.forms import ArticleForm

class BaseArticleFormSet(BaseFormSet):
    def add_fields(self, form, index):
        super().add_fields(form, index)
        form.fields["my_field"] = forms.CharField()
          
ArticleFormSet = formset_factory(ArticleForm, formset=BaseArticleFormSet)
```

小结

Formset真的非常有用，属于Django必备的基础知识之一。使用的时候先定义单个的form，然后利用factory生成formset。你需要根据不同应用场景选择不同的formset，并了解如何进行formset的验证。



























# 九、Django3的ASGI



## 1 Web应用程序和web服务器

Web应用程序（Web）是一种能完成web业务逻辑，能让用户基于web浏览器访问的应用程序，它可以是一个实现http请求和响应功能的函数或者类，也可以是Django、Flask、sanic等这样的web框架，当然也可以是其他语言的web程序或web框架。

Web服务器（Web Server）是一种运行于网站后台（物理服务器）的软件。Web服务器主要用于提供网页浏览或文件下载服务，它可以向浏览器等Web客户端提供html网页文档，也可以提供其他类型的可展示文档，让客户端用户浏览；还可以提供数据文件下载等。目前世界上最主流的Web服务器有 Nginx 、Apache、IIS、tomcat。

```python
问：Web服务器和Web应用程序的区别？
答：Web应用程序主要是完成web应用的业务逻辑的处理，Web服务器则主要是应对外部请求的接收、响应和转发。
    需要使用web服务器启动运行，web应用程序才能被用户访问到。
    而django框架中，我们之所以只有一个web应用程序就跑起来了，是因为我们在终端执行了一个命令，python manage.py runserver。这个命令启动了django框架中内置提供的测试web服务器。
```

## 2 网关接口

网关接口（Gateway Interface，GI）就是一种为了实现加载动态脚本而运行在Web服务器和Web应用程序中的通信接口，也可以理解为一份协议/规范。只有Web服务器和Web应用程序都实现了网关接口规范以后，双方的通信才能顺利完成。常见的网关接口协议：CGI，FastCGI，WSGI，ASGI。

![image-20210608222947398](assets/image-20210608222947398.png)

#### （1）CGI

CGI(Common Gateway Inteface): 字面意思就是通用网关接口，

> 它是外部应用程序与Web服务器之间的接口标准

意思就是它用来规定一个程序该如何与web服务器程序之间通信从而可以让这个程序跑在web服务器上。当然，CGI 只是一个很基本的协议，在现代常见的服务器结构中基本已经没有了它的身影，更多的则是它的扩展和更新。

FastCGI: CGI的一个扩展， 提升了性能，废除了 CGI fork-and-execute （来一个请求 fork 一个新进程处理，处理完再把进程 kill 掉）的工作方式，转而使用一种长生存期的方法，减少了进程消耗，提升了性能。

这里 FastCGI 就应用于前端 server（nginx）与后端 server（uWSGI）的通信中，制定规范等等，让前后端服务器可以顺利理解双方都在说什么（当然 uWSGI 本身并不用 FastCGI, 它有另外的协议）

#### （2）WSGI

WSGI（Python Web Server GateWay Interface）:它是用在 python web 框架编写的应用程序与后端服务器之间的规范（本例就是 Django 和 uWSGI 之间），让你写的应用程序可以与后端服务器顺利通信。在 WSGI 出现之前你不得不专门为某个后端服务器而写特定的 API，并且无法更换后端服务器，而 WSGI 就是一种统一规范， 所有使用 WSGI 的服务器都可以运行使用 WSGI 规范的 web 框架，反之亦然。

WSGI和ASGI，都是基于Python设计的网关接口（Gateway Interface，GI）。

![image-20210608223815714](assets/image-20210608223815714.png)

Web服务器网关接口（Python Web Server Gateway Interface，WSGI），是Python为了解决**Web服务器端与客户端之间的通信**基于CGI标准而设计的。实现了WSGI协议的web服务器有：uWSGI、uvicorn、gunicorn。像django框架一般开发中就不会使用runserver来运行，而是采用上面实现了WSGI协议的web服务器来运行。

django中运行runserver命令时，其实内部就启动了wsgiref模块作为web服务器运行的。wsgiref是python内置的一个简单地遵循了wsgi接口规范的web服务器程序。

```python
from wsgiref.simple_server import make_server
# application 由wsgi服务器调用、函数对http请求与响应的封装、使得Python专注与HTML
# environ http 请求 (dist)
# start_response 响应 (function)
def application(environ, start_response):
    # 请求
    if environ['REQUEST_METHOD'] == 'GET' and environ['PATH_INFO'] == '/':
        # 响应
        start_response('200 OK', [('Content-Type', 'text/html')])
        return [b'<h1>hi, python!</h1>']

if __name__ == '__main__':
    # 启动服务器 | 这个服务器负责与 wsgi 接口的 application 函数对接数据
    httpd = make_server('127.0.0.1', 8000, application)

    # 监听请求
    httpd.serve_forever()
    
    
# 1. 监听8000端口,
# 2. 把http请求根据WSGI协议将其转换到applcation中的environ参数, 然后调用application函数.
# 3. wsgiref会把application函数提供的响应头设置转换为http协议的响应头,
# 4. 把application的返回(return)作为响应体, 根据http协议,生成响应, 返回给浏览器.
```

开发中，我们一般使用uWSGI或者Gunicorn作为web服务器运行django。

#### （3）uWSGI

[uWSGI](https://uwsgi-docs.readthedocs.io/) 是一个快速的，自我驱动的，对开发者和系统管理员友好的应用容器服务器，用于接收前端服务器转发的动态请求并处理后发给 web 应用程序。完全由 C 编写，实现了WSGI协议,uwsgi,http等协议。注意：uwsgi 协议是一个 uWSGI服务器自有的协议,用于定义传输信息的类型，常用于uWSGI服务器与其他网络服务器的数据通信中。

uwsgi: 是uWSGI服务器实现的独有的协议， 网上没有明确的说明这个协议是用在哪里的，我个人认为它是用于前端服务器与 uwsgi 的通信规范，相当于 FastCGI的作用。

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg-blog.csdnimg.cn%2F20210512235751822.png%3Fx-oss-process%3Dimage%2Fwatermark%2Ctype_ZmFuZ3poZW5naGVpdGk%2Cshadow_10%2Ctext_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0thaVNhckg%3D%2Csize_16%2Ccolor_FFFFFF%2Ct_70&refer=http%3A%2F%2Fimg-blog.csdnimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1639038508&t=17089204ac04f14b3eb9058ddf473b48)

![在这里插入图片描述](assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2d5bWFpc3ls,size_16,color_FFFFFF,t_70.png)

![img](assets/1454579-20181209002415550-68432975.png)





## 3 关于ASGI

### 1、历史趣谈

2019 年 12 月，[Django](https://so.csdn.net/so/search?from=pc_blog_highlight&q=Django)3.0 发布，它具有一个有趣的新特性——支持 ASGI 服务器。

2003 年，诸如Zope、Quixote之类的各式各样的 [Python](https://so.csdn.net/so/search?from=pc_blog_highlight&q=Python) Web 框架都附带了自己的 Web 服务器，或者拥有自己的本地接口来与流行的网络服务器（如 Apache）进行通信。

成为一名 Python Web 开发人员意味着要全身心投入到一个完整的技术栈中，但是如果需要另一个框架时，则必须重新学习所有内容。可以想象到这会导致碎片化。PEP 333，即 Python Web 服务器网关接口 v1.0，尝试通过定义一个被称为 WSGI（Web Server Gateway Interface）的简单标准接口来解决这个问题。它的卓越之处在于它的简单性。

WSGI 如此流行，以至它不仅被诸如 [Django](https://so.csdn.net/so/search?from=pc_blog_highlight&q=Django) 和 Pylons 之类的大型 Web 框架所采用，还被诸如 Bottle 之类的微框架所采用。

#### 为什么有ASGI的出现

如果我们对 WSGI 非常满意的话，为什么还要提出 ASGI 呢？如果仔细检查网络请求的整个处理流程，那么答案就非常明显了。您可以查看 在Django中网络请求如何工作 的动画。请注意，在数据库查询之后且响应发送之前，框架是如何等待的。这就是同步处理的缺点。

坦白说，直到 2009 年 Node.js 出现时，这种缺陷才变得明显或紧迫。Node.js 的创建者 Ryan Dahl 受到 C10K 问题的困扰，即为什么像 Apache 这样的流行 Web 服务器无法处理 10,000 个或更多的并发连接（给定典型的 Web 服务器硬件，内存将会耗尽）。他思考到 “查询数据库时，软件在做什么？”。

当然，答案是什么也没有发生。它正在等待数据库的响应。Ryan 认为网络服务器根本不应该去等待 I / O 活动。换言之，它应该切换为处理其他请求，并在较慢的活动完成时能得到通知。

越来越明显的是，基于异步事件的架构是解决多种并发问题的正确方法。也许这就是为什么 [Python](https://so.csdn.net/so/search?from=pc_blog_highlight&q=Python) 的创建者 Guido 亲自为 Tulip 项目提供语言级别支持的原因，这个项目后来成为了 asyncio 模块。最终，Python 3.7 添加了新的关键字 async 和 await ，用于支持异步事件循环。这不仅对如何编写 Python 代码而且对代码执行也具有重大意义。

#### Python 的两个世界

虽然使用 Python 编写异步代码非常简单，在函数定义前添加 async 关键字，但是您必须非常小心，不要打破一个重要的规则：不要随意混合使用同步代码和异步代码。

这是因为同步代码可以阻止异步代码中的事件循环。这种情况会使您的应用程序陷入停顿。正如 Andrew Goodwin 所写：这会将您的代码分为两个世界——具有不同库和调用风格的“同步代码”和“异步代码”。

回到 WSGI，这意味着我们无法编写异步可调用对象并将其嵌入。WSGI 是为同步世界编写的。我们将需要一种新的机制来调用异步代码。但是，如果每个人都编写自己的一套机制，我们将回到最初的不兼容地狱。因此，对于异步代码，我们需要一个类似于 WSGI 的新标准。因此，ASGI 诞生了。

ASGI 还有其他一些目的。但是在此之前，让我们看一下两种类似的 Web 应用程序“Hello World”，它们分别采用 WSGI 和 ASGI 风格。

与 WSGI 一样，ASGI 可调用对象可以一个接一个地链接在一起，以处理 Web 请求（以及其他协议请求），即链式调用。实际上，ASGI 是 WSGI 的超集且可以调用 WSGI 可调用对象。ASGI 还支持长时间轮询，慢速流媒体和其他响应类型，而无需侧向加载，从而可以加快响应速度。

因此，ASGI 引入了构建异步 Web 界面和处理双向协议的新方式。客户端或服务器端都无需等待对方进行通信——这可以随时异步发生。现存且以同步代码编写的基于 WSGI 的 Web 框架将不支持这种事件驱动的工作方式。

#### Django 演变

同时，想将所有这些异步优势带给 Django 面临一个重大的问题 —— 所有 Django 代码都是以同步风格编写的。如果我们需要编写任何异步代码，那么需要一个采用异步风格编写的整个 Django 框架的副本。换句话说，创建两个 Django 世界。

好吧，不要惊慌——我们可能不必编写一个完整的副本，因为有聪明的方式可以在两个世界之间重用一些代码。正如领导 Django Async 项目的安德鲁·戈德温（Andrew Godwin）正确地指出的那样，“这是 Django 历史上最大规模的修订之一”。一个雄心勃勃的项目采用异步风格重新实现 ORM、请求处理程序（request handler）、模板渲染器（Template renderer）等组件。这将分阶段进行，并在多个版本中完成。如下是安德鲁的预想（这不视为已提交的时间表）：

-  Django 3.0-ASGI 服务器
-  Django 3.1-异步视图
-  Django 3.2 / 4.0-异步 ORM

您可能正在考虑其余的组件，例如模板渲染、表单和缓存等。它们可能仍然保持同步或者其异步实现会纳入到将来的技术路线中。但是以上是 Django 在异步世界中发展的关键里程碑。





### 2、asgi的使用

ASGI，是构建于WSGI接口规范之上的**异步服务器网关接口**，是WSGI的延伸和扩展。

```
A指的是Async，异步的意思。
```

| 协议，规范 | 支持的请求协议（常见，未列全） | 同步/异步 | 支持的框架                                              |
| ---------- | ------------------------------ | --------- | ------------------------------------------------------- |
| CGI        | HTTP                           |           | CGI程序                                                 |
| WSGI       | HTTP                           | 同步      | django3.0以前，Flask1.0                                 |
| ASGI       | HTTP，HTTP2，WebSocket等       | 同步/异步 | FastAPI，Quart，Sanic，Tornado，django3.0以后，flask2.0 |

在 Python3.5 之后增加 async/await 特性之后简化了协程操作以后，异步编程变得异常火爆，越来越多开发者投入异步的怀抱。

3.0版本以前，django所提供的所有内部功能都是基于同步编程的。所以，在以往django开发中，针对网络请求，数据库读取等IO操作形成的阻塞，往往会导致项目运行性能的下降。虽然等待I/O操作数微秒时，但是随着流量的增加和操作的频率上升，这一点点的阻塞就会导致整个项目运作的缓慢。而如果换成异步就不会有任何阻塞，还可以同时处理其他任务，从而以较低的延迟处理更多的请求。所以在目前python开发中，越来越多的框架开始支持了异步编程。所以，3.0版本以后，django开始支持异步编程，可以让开发者在django中使用python第三方异步模块，推出了asgi异步web服务器。3.1版本推出了异步视图，当然，目前django的异步编程还不够完善，django中只有极少的功能是支持了异步操作。

![image-20210608235013829](assets/image-20210608235013829.png)

Uvicorn 是一个快速的 ASGI 服务器，Uvicorn 是基于 uvloop 和 httptools 构建的，是 Python 异步生态中重要的一员。

Uvicorn 当前支持 HTTP / 1.1 和 WebSockets，将来计划支持HTTP / 2。

文档：https://www.uvicorn.org/

安装uvicorn

```bash
pip install uvicorn
```

项目根目录下，运行django项目

```bash
# uvicorn 主应用目录名.asgi:application --reload
uvicorn homework.asgi:application --reload
```

开发中一般使用gunicorn来管理uvicorn。所以可以一并安装

```python
pip install gunicorn
```

运行

```python
# gunicorn -w 4 主应用目录名.asgi:application -k uvicorn.workers.UvicornWorker --reload
gunicorn -w 4 homework.asgi:application -k uvicorn.workers.UvicornWorker --reload
```







# 其它

## 1 获取当前时间时区默认的设置

![image-20220807131548682](Django.assets/image-20220807131548682.png)





​	
