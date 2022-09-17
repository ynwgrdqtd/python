# 1 关于前后端分离

接下来，你将进入 **前后端分离项目开发** 模块。 这也是现在企业中比较常见的开发模式。

疑问：

- 什么是前后端分离？与之前的开发模式有什么区别？
- 企业为什么要用前后端分离？



### 1. 什么是前后端分离？

- 前后端不分离，像咱们之前学习django、案例、crm项目、bug管理 时的那些模块。

  ```
  特点：
  	- 用户访问URL
  	- 执行视图函数，视图进行业务处理
  	- 视图render，读取HTML模块+数据渲染，将渲染完成的HTML/CSS/JS返回并呈现在用户浏览器上。
  	
  配合开发：
  	- 前端，写HTML、CSS、JS
  	- 后端，前端代码给我后端，后端代码 + 前端代码 集成到项目中。
  ```

  ![image-20210828135148077](drf.assets/image-20210828135148077.png)

  ![image-20210819121547705](drf.assets/image-20210819121547705.png)

- 前后端分离

  ```
  特点：
  	- 一般基于 vue.js、react.js、angular.js 框架来编写前端页面（本质上是HTML、CSS、JS）。
  	- 页面上如果需要呈现数据，则需要则需要通过 ajax 的形式向后端发送请求（URL）并获取数据。
  	- 后端接收到请求后，执行视图函数并进行业务处理
  	- 后端的视图执行完毕后，给前端返回JSON格式数据。
  	- 前端接收到JSON格式数据后呈现在浏览器上即可。
  	
  配合开发：
  	- 前端，写HTML、CSS、JS（数据都是通过调用后端API获得）
  	- 后端，写API接口
  	- 前后端约定好接口的规则。
  ```

  ![image-20210819122103573](drf.assets/image-20210819122103573.png)

  <img src="drf.assets/image-20210807125206445.png" alt="image-20210807125206445" />

  

![image-20210807124425671](drf.assets/image-20210807124425671.png)



### 2.为什么要使用前后端分离？

目前企业一般都会采用前后端分离的形式来进行项目开发，这种模式：

- 前后端职责清晰，前端开发者只vue.js、react.js、angular.js等框架编写页面；后端开发者只用Python编写后端代码；（两者通过json格式请求数据的传输）。
- 开发高效，前后端做自己擅长的领域且使用vue.js等前端框架比用传统的HTML、CSS、JS、jQuery等开发速度快很多。
- 有利于项目的扩展（开发APP、微信小程序等）。

![image-20210819122740927](drf.assets/image-20210819122740927.png)

**注意：**前后端不分离的项目，现在一般用于开发用户量少、简单的项目。





# 2 RESTful规范

![image-20210819123735927](drf.assets/image-20210819123735927.png)

对于后端开发者，本质上就是提供URL给前端开发者调用并返回相应的数据。例如：

<img src="drf.assets/image-20210807125206445-16587588947337.png" alt="image-20210807125206445" style="zoom: 33%;" />



现在咱们大家知道前端后端分离的项目是需要：前端、后端 双方来进行合作开发，既然合作进行开发就必须要提前约定一些规范，以防止双方”打架“，例如：

- 数据传输用XML格式？JSON格式？

- 出现错误时，错误信息有谁来提供？

  ```
  方案1：错误时后端返回错误信息，前端只做呈现即可。
  	{
  		code:40001,
  		error:"xxx错误"
  	}
  方案2：错误时后端返回错误码，前端根据错误码的对应关系呈现。
  	{
  		code:40001
  	}
  ```

- 等等等...

所以，我们需要先来学习下规范，然后再来进行后续开发。











restful是主流的一套API规范，企业进行前后端分离开发一般都会遵循它，他定义了很多规范的条款。

例如：如果现在让大家来开发一个对 **用户表** 进行增删改查的接口，在不了解restful规范前， 大家一定会这样来搞：

```
接口：/users/list/			用户列表
接口：/users/add/			添加用户
接口：/users/detail/(\d+)	用户详细信息
接口：/users/edit/(\d+)	更新用户
接口：/users/del/(\d+)		删除用户
```

很早之前开发者们也确实都是这么干的，直到后来有人提出了 restful API规范（包含了很多规定），如果按照这个规范来开发上述的功能的话：

```
接口：/users/			方法：GET     =>   用户列表
接口：/users/			方法：POST    =>   添加列表
接口：/users/(\d+)/	方法：GET     =>   获取单条数据
接口：/users/(\d+)/	方法：DELETE  =>   删除数据
接口：/users/(\d+)/	方法：PUT     =>   更新数据
```

暂且不说restful规范有多好，对于前端和后端只要能统一了规范，对大家的开发效率都会有很大的帮助，不用再做很多无效的沟通了。



所以，接下来咱们就是学习最常见的restful规范。



### 1.HTTPS协议

建议使用https协议替代http协议，让接口数据更加安全。

这一条其实与开发无关，在最后的项目部署时只要使用https部署即可。

![image-20210807135928170](drf.assets/image-20210807135928170.png)



如果是基于HTTP协议，则意味着用户浏览器再向服务器发送数据时，都是以明文的形式传输，如果你在某咖啡厅上网，他就可以把你网络传输的数据明文都获取到。

如果是基于HTTPS协议，则意味着用户浏览器再向服务器发送数据时，都是以密文的形式传输，中途即使有非法用户获取到网络数据，也可以密文的，无法破译。

HTTPS保证了数据安全，但由数据传输存在着加密和解密的过程，所以会比HTTP协议慢一些。



注意：此处大家先了解https和http的不同，至于底层原理和部署，在项目部署时再细讲。

参考文档：https://www.cnblogs.com/wupeiqi/p/11647089.html



### 2. 域名

对于后端API接口中要体现API标识，例如：

- https://**api**.example.com
- https://www.example.com/**api**/



![image-20210807141747844](drf.assets/image-20210807141747844.png)

![image-20210807141524804](drf.assets/image-20210807141524804.png)



![image-20210807142204010](drf.assets/image-20210807142204010.png)





### 3. 版本

对于后端API接口中要体现版本，例如：

```
- http://api.example.com/v1/

- http://api.example.com/?version=v1

- http://v1.example.com/

- http://api.example.com/
  请求头：Accept: application/json; version=v1
```

![image-20210807142526704](drf.assets/image-20210807142526704.png)



### 4. 路径

restful API这种风格中认为网络上的一切都称是资源，围绕着资源可以进行 增删改查等操作。

这些资源，在URL中要使用名词表示（可复数），围绕着资源进行的操作就用Method不同进行区分。

```
https://api.example.com/v1/person
https://api.example.com/v1/zoos
https://api.example.com/v1/animals
https://api.example.com/v1/employees
```



### 5. 请求方法

根据请求方法不同进行不同的操作。

```
GET		在服务器取出资源（一项或多项）
POST	在服务器新建一个资源
PUT		在服务器更新资源（客户端提供改变后的完整资源）
PATCH	在服务器更新资源（客户端提供改变的属性）
DELETE	在服务器删除资源
```

例如：

```
https://api.example.com/v1/users
https://api.example.com/v1/users/1/

接口：/users/			方法：GET     =>   用户列表
接口：/users/			方法：POST    =>   添加用户
接口：/users/(\d+)/	方法：GET     =>   获取单条数据
接口：/users/(\d+)/	方法：DELETE  =>   删除数据
接口：/users/(\d+)/	方法：PUT     =>   更新数据
接口：/users/(\d+)/	方法：PATCH   =>   局部更新
```



### 6. 搜索条件

在URL中通过参数的形式来传递搜索条件。

```python
https://api.example.com/v1/users
```

```
https://api.example.com/v1/zoos?limit=10				指定返回记录的数量
https://api.example.com/v1/zoos?offset=10				指定返回记录的开始位置
https://api.example.com/v1/zoos?page=2&per_page=100		指定第几页，以及每页的记录数
https://api.example.com/v1/zoos?sortby=name&order=asc	指定返回结果按照哪个属性排序，以及排序顺序
https://api.example.com/v1/zoos?animal_type_id=1		指定筛选条件
```



### 7. 返回数据

针对不同操作，服务器向用户返回的结果结构应该不同。

```python
https://api.example.com/v1/users
https://api.example.com/v1/users/2/
```

| URL           | 方法   | 描述         | 返回数据                                                     |
| ------------- | ------ | ------------ | ------------------------------------------------------------ |
| /users/       | GET    | 列表         | 返回资源对象的列表<br />[ {id:1,name:"武沛齐"},   {id:1,name:"日天"}  ] |
| /users/       | POST   | 添加         | 返回新生成的资源对象<br />{id:1,name:"武沛齐"}               |
| /users/(\d+)/ | GET    | 获取单条数据 | 返回单个资源对象<br />{id:1,name:"武沛齐"}                   |
| /users/(\d+)/ | DELETE | 删除数据     | 返回一个空文档<br />null                                     |
| /users/(\d+)/ | PUT    | 更新数据     | 返回完整的资源对象<br />{id:1,name:"武沛齐"}                 |
| /users/(\d+)/ | PATCH  | 局部更新     | 返回完整的资源对象<br />{id:1,name:"武沛齐"}                 |

一般在实际的开发过程中会对上述返回数据进行补充和完善，例如：每次请求都返回一个字典，其中包含：

- code，表示返回码，用于表示请求执行请求，例如：0表示请求成功，1003表示参数非法，40009数据量太大等。
- data，表示数据
- error，错误信息

```python
{
    code:0,
    data:[ {id:1,name:"武沛齐"},   {id:1,name:"日天"}  ]
}
```

```python
{
    code:41007,
    error:"xxxxx"
}
```





### 8. 状态码

后端API在对请求进行响应时，除了返回数据意外还可以返回状态码，来表示请求状况。

```python
from django.urls import path, include
from app01 import views

urlpatterns = [
    path('users/', views.users),
]
```

```python
from django.http import JsonResponse

def users(request):
    info = {
        "code": 1000,
        "data": {"id":1,"name":"武沛齐"}
    }
    return JsonResponse(info, status=200)
```

![image-20210829161449149](drf.assets/image-20210829161449149.png)



```
200 OK - [GET]：服务器成功返回用户请求的数据
201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。
202 Accepted - [*]：表示一个请求已经进入后台排队（异步任务）
204 NO CONTENT - [DELETE]：用户删除数据成功。
400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作。
401 Unauthorized - [*]：表示用户未认证（令牌、用户名、密码错误）。
403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的。
404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作。
406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。
410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。
422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。
500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。

更多看这里：http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html
```



状态码可以表示一部分的服务端的处理请求，但特别细致的信息无法全都都包括，所以一般在开发中会配合code返回码来进行。

例如：https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Global_Return_Code.html

### 9. 错误处理

错误处理，状态码是4xx时，应返回错误信息，error当做key。

```
{
    error: "Invalid API key"
}
```

在 1.1.7 中中已包含。





了解常用resful规范，那么以后在开发后端API接口时，就要根据上述要求遵循restful规范（非必须，视公司情况灵活变通）。

















### 案例展示

基于django + restful规范来开发一个后台接口示例。

```python
# urls.py

from django.urls import path
from app01 import views

# http://www.xxx.com/api/v1/users/

urlpatterns = [
    path('api/<str:version>/users/', views.users),
    path('api/<str:version>/users/<int:pk>/', views.users),
]
```

```python
# views.py

from django.http import JsonResponse


def users(request, version, pk=None):
    print("版本：", version)
    if not pk:
        if request.method == "GET":
            # 请求用户列表
            info = {
                "code": 0,
                "data": [{"id": 1, "name": "武沛齐"}]
            }
            return JsonResponse(info)
        elif request.method == "POST":
            # 新增用户，读取 request.POST 中提交的数据并添加到数据库中
            info = {
                "code": 0,
                "data": {"id": 1, "name": "武沛齐"}
            }
            return JsonResponse(info)
        else:
            info = {
                "code": 1000,
                "error": "请求错误"
            }
            return JsonResponse(info)

    if request.method == "GET":
        # 获取ID=pk的用户信息，并返回
        info = {
            "code": 0,
            "data": {"id": 1, "name": "武沛齐"}
        }
        return JsonResponse(info)
    elif request.method == "DELETE":
        # 删除id=pk的用户
        info = {
            "code": 0,
            "data": {}
        }
        return JsonResponse(info)
    elif request.method == "PUT":
        # 读取request.POST中的数据 + pk，更新数据库中的用户信息
        info = {
            "code": 0,
            "data": {"id": 1, "name": "武沛齐"}
        }
        return JsonResponse(info)
    elif request.method == "PATCH":
        # 读取request.POST中的数据 + pk，更新数据库中的用户信息
        info = {
            "code": 0,
            "data": {"id": 1, "name": "武沛齐"}
        }
        return JsonResponse(info)
    else:
        info = {
            "code": 1000,
            "error": "请求错误"
        }
        return JsonResponse(info)

```



# 3 Django的FBV和CBV

基于django开发项目时，对于视图可以使用 FBV 和 CBV 两种模式编写。

## FBV，function base views，其实就是编写函数来处理业务请求。

```python
from django.contrib import admin
from django.urls import path
from app01 import views
urlpatterns = [
    path('users/', views.users),
]
```

```python
from django.http import JsonResponse

def users(request,*args, **kwargs):
    if request.method == "GET":
        return JsonResponse({"code":1000,"data":"xxx"})
    elif request.method == 'POST':
        return JsonResponse({"code":1000,"data":"xxx"})
    ...
```

## CBV，class base views，其实就是编写类来处理业务请求。

```python
from django.contrib import admin
from django.urls import path
from app01 import views
urlpatterns = [
    path('users/', views.UserView.as_view()),
]
```

```python
from django.views import View

class UserView(View):
    def get(self, request, *args, **kwargs):
        return JsonResponse({"code": 1000, "data": "xxx"})

    def post(self, request, *args, **kwargs):
        return JsonResponse({"code": 1000, "data": "xxx"})
```



其实，CBV和FBV的底层实现本质上相同的。

![image-20210819114755157](drf.assets/image-20210819114755157.png)



![image-20210819115517407](drf.assets/image-20210819115517407.png)

CBV，其实就是在FBV的基础上进行的功能的扩展，根据请求的方式不同，直接定位到不同的函数中去执行。

如果是基于django编写restful API，很显然使用CBV的方式会更加简洁，因为restful规范中就是根据method不同来执行不同操作。



基于django的CBV和restful规范开发实战案例：

```python
# urls.py

from django.urls import path
from app01 import views

urlpatterns = [
    # http://www.xxx.com/api/v1/users/
    path('api/<str:version>/users/', views.UserView.as_view()),

    # http://www.xxx.com/api/v1/users/2/
    path('api/<str:version>/users/<int:pk>/', views.UserView.as_view()),

]
```

```python
# views.py

from django.views import View
from django.http import JsonResponse


class UserView(View):
    def get(self, request, version, pk=None):
        if not pk:
            # 请求用户列表
            info = {
                "code": 0,
                "data": [
                    {"id": 1, "name": "武沛齐"},
                    {"id": 1, "name": "武沛齐"},
                ]
            }
            return JsonResponse(info)
        else:
            # 获取ID=pk的用户信息，并返回
            info = {
                "code": 0,
                "data": {"id": 1, "name": "武沛齐"}
            }
            return JsonResponse(info)

    def post(self, request, version):
        # 新增用户，读取 request.POST 中提交的数据并添加到数据库中
        info = {
            "code": 0,
            "data": {"id": 1, "name": "武沛齐"}
        }
        return JsonResponse(info)

    def delete(self, request, version, pk):
        # 删除id=pk的用户
        info = {
            "code": 0,
            "data": {}
        }
        return JsonResponse(info)

    def put(self, request, version, pk):
        # 读取request.POST中的数据 + pk，更新数据库中的用户信息
        info = {
            "code": 0,
            "data": {"id": 1, "name": "武沛齐"}
        }
        return JsonResponse(info)

    def patch(self, request, version, pk):
        # 读取request.POST中的数据 + pk，更新数据库中的用户信息
        info = {
            "code": 0,
            "data": {"id": 1, "name": "武沛齐"}
        }
        return JsonResponse(info)

```





从上面的示例看来，基于django框架完全可以开发restful API。







django restframework框架 是在django的基础上又给我们提供了很多方便的功能，让我们可以更便捷基于django开发restful API，来一个简单的实例，快速了解下：

- 基于django
  <img src="drf.assets/image-20210819132015065.png" alt="image-20210819132015065" style="zoom: 25%;" />
- 基于django + django restframework框架
  <img src="drf.assets/image-20210819132209726.png" alt="image-20210819132209726" style="zoom:25%;" />





# 3 DRF 上

全称django restframework（简称drf）本质上其实就是一个别人编写好的app，里面集成了很多编写restful API的功能功能

## 1 简单使用

### 1.1安装

```
pip install djangorestframework==3.12.4
```

```python
版本要求：djangorestframework==3.12.4
	Python (3.5, 3.6, 3.7, 3.8, 3.9)
	Django (2.2, 3.0, 3.1)
    
版本要求：djangorestframework==3.11.2
	Python (3.5, 3.6, 3.7, 3.8)
	Django (1.11, 2.0, 2.1, 2.2, 3.0)
```

### 1.2 配置

**在`settings.py`中添加配置: **

```python
INSTALLED_APPS = [
    ...
    # 注册rest_framework（drf）
    'rest_framework',			
]

# drf相关配置以后编写在这里 
# 下面的配置根据项目需要进行设置
REST_FRAMEWORK = {
    # 配置默认页面大小
     'PAGE_SIZE': 10,
    # 配置默认的分页类
     'DEFAULT_PAGINATION_CLASS': '...',
    # 配置异常处理器
     'EXCEPTION_HANDLER': '...',
    # 配置默认解析器
     'DEFAULT_PARSER_CLASSES': (
         'rest_framework.parsers.JSONParser',
         'rest_framework.parsers.FormParser',
         'rest_framework.parsers.MultiPartParser',
     ),
    # 配置默认限流类
     'DEFAULT_THROTTLE_CLASSES': (
         '...'
    ),
    # 配置默认授权类
     'DEFAULT_PERMISSION_CLASSES': (
        '...',
     ),
    # 配置默认认证类
     'DEFAULT_AUTHENTICATION_CLASSES': (
         '...',
     ),
}
```

### 1.3 URL和视图

```python
# urls.py

from django.urls import path
from app01 import views

urlpatterns = [
    path('users/', views.UserView.as_view()),		
]
```

视图类继承 `APIView`  return时用 `rest_framework.response` 类中的 `Response` 返回`json`数据

```python
# views.py
from rest_framework.views import APIView			# 1导入APIView继承，导入Response作返回数据
from rest_framework.response import Response


class UserView(APIView):						    # 2 创建视图类继承APIView
    def get(self, request, *args, **kwargs):
        return Response({"code": 1000, "data": "xxx"})	# 3 用Response返回json

    def post(self, request, *args, **kwargs):
        return Response({"code": 1000, "data": "xxx"})
```

### 1.4 drf框架与django的CBV的区别

其实drf框架是在django基础进行的扩展，所以上述执行过得底层实现流程（同django的CBV）：

![image-20210819141447988](drf.assets/image-20210819141447988.png)

drf中重写了 `as_view` 和`dispatch`方法，其实就是在原来django的功能基础上添加了一些功能，例如：

- `as_view`，免除了csrf 验证，一般前后端分离不会使用csrf token认证（后期会使用jwt认证）。
- `dispatch`，内部添加了 版本处理、认证、权限、访问频率限制等诸多功能（后期逐一讲解）。











## 2 请求数据request的封装

### 原request对象

以前我们通过django开发项目时，视图中的request是 `django.core.handlers.wsgi.WSGIRequest` 类的对象，其中包含了请求相关的所有数据。

```python
# Django FBV
def index(request):
	request.method	# 查看请求
	request.POST	# 查看post数据
	request.GET		# 查看get数据
	request.body	# 查看请求体

# Django CBV
from django.views import View
class UserView(View):
	def get(self,request):
        request.method
        request.POST
        request.GET
        request.body
```

### drf中request对象

而在使用drf框架时，视图中的request是`rest_framework.request.Request`类的对象，其是又对django的request进行了一次封装，包含了除django原request对象以外，还包含其他后期会使用的其他对象。

```python
from rest_framework.views import APIView
from rest_framework.response import Response


class UserView(APIView):
    def get(self, request, *args, **kwargs):
        # 1 request，不再是django中的request，而是又被封装了一层，内部包含：django的request、认证、解析器等。
        return Response({"code": 1000, "data": "xxx"})

    def post(self, request, *args, **kwargs):
        return Response({"code": 1000, "data": "xxx"})

```

```python
新request对象 = (原request, 其他数据)
```

#### 新request对象源码

```python
# rest_framework.request.Request 类

class Request:
    """
    Wrapper allowing to enhance a standard `HttpRequest` instance.
    Kwargs:
        - request(HttpRequest). The original request instance. （django中的request）
        - parsers(list/tuple). The parsers to use for parsing the
          request content.
        - authenticators(list/tuple). The authenticators used to try
          authenticating the request's user.
    """

    def __init__(self, request, parsers=None, authenticators=None,negotiator=None, parser_context=None):
    	self._request = request
        self.parsers = parsers or ()
        self.authenticators = authenticators or ()
        ...
	
    @property
    def query_params(self):
        """
        More semantically correct name for request.GET.
        """
        return self._request.GET

    @property
    def data(self):
        if not _hasattr(self, '_full_data'):
            self._load_data_and_files()
        return self._full_data
    
	def __getattr__(self, attr):
        try:
            return getattr(self._request, attr) # self._request.method
        except AttributeError:
            return self.__getattribute__(attr)
```

#### drf 的request数据的调用方法

所以，在使用drf框架开发时，视图中的request对象与原来的有些不同，例如：

- request._request 就等于原来的，可以调用原来内的数据，如下1
- request.query_params 本质上就是 request._request.GET，如下2
- request.data 会把用户请求的json字符串进行反序列化成json格式

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from django.views import View
from rest_framework.request import Request


class UserView(APIView):
    def get(self, request, *args, **kwargs):
        # 1 通过对象的嵌套直接找到原request，读取相关值
        request._request.method
        request._request.GET
        request._request.POST
        request._request.body
        
        # 直接读取新request对象中的值，一般此处会对原始的数据进行一些处理，方便开发者在视图中使用。
        request.query_params  # 2 内部本质上就是 request._request.GET
        
        # 举例：
        	"""
        	content-type: url-form-encoded
        	v1=123&v2=456&v3=999
            django一旦读取到这个请求头之后，就会按照 {"v1":123,"v2":456,"v3":999}
            
            content-type: application/json
            {"v1":123,"v2":456}
            request._request.POST
            request._request.body
            
            """    
        request.data # 3 内部读取请求体中的数据，并进行处理，例如：请求者发来JSON格式，他的内部会对json字符串进行反序列化。
        
        # 4 通过 __getattr__ 去访问 request._request 中的值
        request.method
        
        
```



### 底层源码实现

![image-20210819150601089](drf.assets/image-20210819150601089.png)



## 3. 版本管理

在restful规范中要去，后端的API中需要体现版本。

drf框架中支持5种版本的设置。



### 3.1 URL的GET参数传递（*）

#### 使用方法

1. 路由中设置路径 `'api/useres'`,视图选择对应的视图类`.as.view()`
2. 视图类导入并继承`APIViwe`，类下设置变量`versioning`值导入类`QueryParameterVersioning`
3. 用户访问要在路径后加上 `?version=v1`   version键可自己配置  ，v1是用户传入的版本
4. 视图类对应方法中 `request.version`  就可以输出用户输入的版本

<img src="drf.assets/image-20210819154455680.png" alt="image-20210819154455680" style="zoom: 200%;" />

要导入的模块

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.versioning import QueryParameterVersioning,URLPathVersioning,AcceptHeaderVersioning

class User(APIView):
    versioning_class = QueryParameterVersioning

    def get(self, request, *args, **kwargs):
        print(request.version)
        return Response({'code': 1000, 'deta': '6666'})
```



#### 设置方法

```python
# settings.py

REST_FRAMEWORK = {
    "VERSION_PARAM": "v",													   # 对url中自定义版本键
    "DEFAULT_VERSION": "v1",												   # 设置默认的版本
    "ALLOWED_VERSIONS": ["v1", "v2", "v3"],			 							# 设置版本的限制只能有列表中的
    "DEFAULT_VERSIONING_CLASS":"rest_framework.versioning.QueryParameterVersioning" # 全局设置使用版本
}
```

#### 源码执行流程

![image-20210820105543193](drf.assets/image-20210820105543193.png)



### 3.2 URL路径传递（*）

1. 同上区别不大，路由中用re_path做路径
2. 在视图类中的设置是 `versioning_class = URLPathVersioning`
3. 用户要在url路径中传入版本信息

![image-20210819154955480](drf.assets/image-20210819154955480.png)



### 3.3 请求头传递

1. 路由路径无变化
2. 视图类下设置是 `versioning_class = AcceptHeaderVersioning`
3. 用户访问时要添加请求头获取版本，如图

![image-20210819155617845](drf.assets/image-20210819155617845.png)



### 3.4 二级域名传递

较少使用

![image-20210819160202013](drf.assets/image-20210819160202013.png)

在使用二级域名这种模式时需要先做两个配置：

- 域名需解析至IP，本地可以在hosts文件中添加
  ![image-20210829213040611](drf.assets/image-20210829213040611.png)

  ```
  127.0.0.1       v1.wupeiqi.com
  127.0.0.1       v2.wupeiqi.com
  ```

- 在django的settings.py配置文件中添加允许域名访问

  ```
  ALLOWED_HOSTS = ["*"]
  ```



### 3.5 路由的namespace传递

![image-20210819161839318](drf.assets/image-20210819161839318.png)



以上就是drf中支持的5种版本管理的类的使用和配置。





**全局配置**

上述示例中，如果想要应用某种 版本 的形式，需要在每个视图类中定义类变量：

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.versioning import QueryParameterVersioning


class UserView(APIView):
    versioning_class = QueryParameterVersioning
    ...
```

如果你项目比较大，需要些很多的视图类，在每一个类中都写一遍会比较麻烦，所有drf中也支持了全局配置。

```python
# settings.py

REST_FRAMEWORK = {
    "DEFAULT_VERSIONING_CLASS": "rest_framework.versioning.QueryParameterVersioning",  # 处理版本的类的路径
    "VERSION_PARAM": "version",  # URL参数传参时的key，例如：xxxx?version=v1
    "ALLOWED_VERSIONS": ["v1", "v2", "v3"],  # 限制支持的版本，None表示无限制
    "DEFAULT_VERSION": "v1",  # 默认版本
}
```

![image-20210820113538002](drf.assets/image-20210820113538002.png)

访问URL：

````
http://127.0.0.1:8000/api/users/?version=v1
http://127.0.0.1:8000/api/users/?version=v2
http://127.0.0.1:8000/api/users/?version=v3

http://127.0.0.1:8000/api/admin/?version=v1
http://127.0.0.1:8000/api/admin/?version=v2
http://127.0.0.1:8000/api/admin/?version=v3

http://127.0.0.1:8000/api/v1/order/
http://127.0.0.1:8000/api/v2/order/
http://127.0.0.1:8000/api/v3/order/
````



**底层源码实现**

![image-20210820105543193](drf.assets/image-20210820105543193.png)



**反向生成URL**

在每个版本处理的类中还定义了`reverse`方法，他是用来反向生成URL并携带相关的的版本信息用的，例如：

![image-20210820105543193](drf.assets/image-20210820105543193.png)

![image-20210820112152615](drf.assets/image-20210820112152615.png)



## 小结

以后使用drf开发后端API接口时：

1. 创建django程序
2. 安装drf框架
3. 创建一个app专门来处理用户的请求
4. 注册APP
5. 设置版本
6. 编写视图类



## 4. 认证

![image-20210819123735927](drf.assets/image-20210819123735927-165876172284221.png)

在开发后端的API时，不同的功能会有不同的限制，例如：

- 无需认证，就可以访问并获取数据。
- 需认证，用户需先登录，后续发送请求需携带登录时发放的凭证（后期会讲jwt）



### 要使用导入的类

```python
from rest_framework.views import APIView 					#视图类的继承类
from rest_framework.response import Response				# 返回数据用的
from rest_framework.authentication import BaseAuthentication #继承的认证类
from rest_framework.exceptions import AuthenticationFailed   # 抛出异常的类
```





### 认证流程

**1 用户post访问`api/auth/`路径传入username和password**

**2 数据库中查到有此对象就生成一个uuid，保存到此对象内并把这个对象数据返回**

在drf中也给我们提供了 认证组件 ，帮助我们快速实现认证相关的功能，例如：

```python
# models.py

from django.db import models

class UserInfo(models.Model):
    username = models.CharField(verbose_name="用户名", max_length=32)
    password = models.CharField(verbose_name="密码", max_length=64)
    token = models.CharField(verbose_name="TOKEN", max_length=64, null=True, blank=True)
```

![image-20210821170610618](drf.assets/image-20210821170610618.png)

**3 用户经过登陆后拿到uuid后用get访问`api/order/`路径 到指定的视图类中时，要经过认证类才能访问到对应的get方法，如uuid未对上抛出错误，就不会访问到视图类 中的get方法**

**4 视图类`OrderView`中设置变量 `authentication_classes`的值为 处定认证类 `MyAuthentication`  要继承`BaseAuthentication`类，表示此视图在执行内部功能之前需要先经过认证，认证类的内部就是去执行：`authenticate`方法，根据返回值来表示认证结果。**

![image-20210821171152853](drf.assets/image-20210821171152853.png)

**5 在自定的`MyAuthentication`类中定义`authenticate`方法，不通过就抛出异常`AuthenticationFailed`，表示认证失败，内部还会执行 `authenticate_header`方法将返回值设置给响应头 `WWW-Authenticate`**

**6 没有异常就返回含有两个元素的元组，表示认证成功，并且会将元素的第1个元素当前查到的对象赋值给 `request.user`，第2个值token赋值给`request.auth` 。**

```
第1个值，一般是用户对象。
第2个值，一般是token
```

- 返回None，表示继续调用 后续的认证类 进行认证（上述案例未涉及）



### 关于 返回None

接下来说说 “返回None” 是咋回事。

> 在视图类的 `authentication_classes` 中定义认证类时，传入的是一个列表，支持定义多个认证类。
>
> 当出现多个认证类时，drf内部会按照列表的顺序，逐一执行认证类的 `authenticate` 方法，如果 返回元组 或 抛出异常 则会终止后续认证类的执行；如果返回None，则意味着继续执行后续的认证类。
>
> 如果所有的认证类`authenticate`都返回了None，则默认 `request.user="AnonymousUser" 和 request.auth=None`，也可以通过修改配置文件来修改默认值。



### 认证类默认返回设置

```python
REST_FRAMEWORK = {
"UNAUTHENTICATED_USER": lambda: None,
"UNAUTHENTICATED_TOKEN": lambda: None,
}
```



### 返回None的应用场景

> 当某个API，已认证 和 未认证 的用户都可以方法时，比如：
>
> - 已认证用户，访问API返回该用户的视频播放记录列表。
> - 未认证用户，访问API返回最新的的视频列表。
>
> 注意：不同于之前的案例，之前案例是：必须认证成功后才能访问，而此案例则是已认证和未认证均可访问。

图说明：**认证类如判断用户token不存在返回none，但可在视图请求方法中判断`request.user`是否为空返回不同的数据**

![image-20210821214440034](drf.assets/image-20210821214440034.png)





### 关于多个认证类

一般情况下，编写一个认证类足矣。 

当项目中可能存在多种认证方式时，就可以写多个认证类。例如，项目认证支持：

- 在请求中传递token进行验证。
- 请求携带cookie进行验证。
- 请求携带jwt进行验证（后期讲）。
- 请求携带的加密的数据，需用特定算法解密（一般为app开发的接口都是有加密算法）
- ...

此时，就可以编写多个认证类，并按照需要应用在相应的视图中，例如：

![image-20210821220439103](drf.assets/image-20210821220439103.png)

**1 先在`settings.py`中设置认证类默认返回空，不设置会返回匿名用户。**

**2 创建两个自定义认证类，在视图类 `authentication_classes = [ ]`放入创建的认证类**

注意：此示例后续在视图中读取的 `request.user` 的值为None时，表示未认证成功；不为None时，则表示认证成功。



### 全局配置

在每个视图类的类变量 `authentication_classes` 中可以定义，其实在配置文件中也可以进行全局配置，例如：

```python
# settings.py

REST_FRAMEWORK = {
    "UNAUTHENTICATED_USER": lambda: None,										# 认证默认返回none
    "UNAUTHENTICATED_TOKEN": lambda: None,										# 认证默认返回none
    "DEFAULT_AUTHENTICATION_CLASSES":["xxxx.xxxx.xx.类名","xxxx.xxxx.xx.类名",]		# 认证设置的全局配置
}
```



### 底层源码实现

![image-20210822092707803](drf.assets/image-20210822092707803.png)



## 5. 权限

认证，根据用户携带的 token/其他 获取当前用户信息。

权限，读取认证中获取的用户信息，判断当前用户是否有权限访问，例如：普通用户、管理员、超级用户，不同用户具有不同的权限。

### 权限使用示例

**1 用户表**

```python
class UserInfo(models.Model):
    
    role_choices = ((1, "普通用户"), (2, "管理员"), (3, "超级管理员"),)
    role = models.IntegerField(verbose_name="角色", choices=role_choices, default=1)
    
    username = models.CharField(verbose_name="用户名", max_length=32)
    password = models.CharField(verbose_name="密码", max_length=64)
    token = models.CharField(verbose_name="TOKEN", max_length=64, null=True, blank=True)
```

**2 图示**

![](drf.assets/image-20210822100012603.png)

 3 **代码示例**

```python
import uuid
from rest_framework.views import APIView
from rest_framework.request import Request
from rest_framework.response import Response
from rest_framework.authentication import BaseAuthentication
from rest_framework.permissions import BasePermission
from rest_framework.exceptions import AuthenticationFailed

from app01 import models


class AuthView(APIView):
    """ 用户登录认证 """
    authentication_classes = []
    permission_classes = []

    def post(self, request, *args, **kwargs):
        print(request.data)  # {"username": "wupeiqi", "password": "123"}
        username = request.data.get('username')
        password = request.data.get('password')
		# 1 用户登陆认证视图类接收用户username，password，进行数据匹配
        user_object = models.UserInfo.objects.filter(username=username, password=password).first()
        if not user_object:
            return Response({"code": 1000, "data": "用户名或密码错误"})
		# 2 匹配后生成uuid 保存到匹配的对象token字段内
        token = str(uuid.uuid4())
        user_object.token = token
        user_object.save()
		# 3 并返回token及username给用户
        return Response({"code": 0, "data": {"token": token, "name": username}})

# 4 创建认证token类，认证失败抛出异常，成功返回用户对象及token
class TokenAuthentication(BaseAuthentication):
    def authenticate(self, request):
        token = request.query_params.get("token")
        if not token:
            raise AuthenticationFailed({"code": 1002, "data": "认证失败"})
        user_object = models.UserInfo.objects.filter(token=token).first()
        if not user_object:
            raise AuthenticationFailed({"code": 1002, "data": "认证失败"})
        return user_object, token

    def authenticate_header(self, request):
        return 'Bearer realm="API"'

# 5 创建权限类继承BasePermission类
class PermissionA(BasePermission):
    message = {"code": 1003, 'data': "无权访问"} #自定义返回的错误信息
	# 6 在has_pemission方法中判断request.user当前用户对象在.role字段的值是否相等于对应的权限数字返回True或False
    def has_permission(self, request, view):
        if request.user.role == 2:
            return True
        return False
	
    # 暂时先这么写
    def has_object_permission(self, request, view, obj):
        return True

# 7 视图类
class OrderView(APIView):
    authentication_classes = [TokenAuthentication, ] # 7.1 应用上认证类

    permission_classes = [PermissionA,]				# 7.2 应用上权限类，如无法通过验证就无法走到get方法

    def get(self, request, *args, **kwargs):
        print(request.user)
        return Response({"code": 0, "data": {"user": None, 'list': [1, 2, 3]}})


class PayView(APIView):
    authentication_classes = [TokenAuthentication, ]
    permission_classes = [PermissionA, ]

    def get(self, request, *args, **kwargs):
        print(request.user)
        return Response({"code": 0, "data": "数据..."})

```







### 关于多个权限类

当开发过程中需要用户同时具备多个权限（缺一不可）时，可以用多个权限类来实现。

权限组件内部处理机制：按照列表的顺序逐一执行 `has_permission` 方法，如果返回True，则继续执行后续的权限类；如果返回None或False，则抛出权限异常并停止后续权限类的执行。

```python
# models.py

from django.db import models


class Role(models.Model):
    """ 角色表 """
    title = models.CharField(verbose_name="名称", max_length=32)


class UserInfo(models.Model):
    """ 用户表 """
    username = models.CharField(verbose_name="用户名", max_length=32)
    password = models.CharField(verbose_name="密码", max_length=64)
    token = models.CharField(verbose_name="TOKEN", max_length=64, null=True, blank=True)

    roles = models.ManyToManyField(verbose_name="角色", to="Role")
```

![image-20210822103254687](drf.assets/image-20210822103254687.png)

```python
# urls.py

from django.urls import path, re_path, include
from app01 import views

urlpatterns = [
    path('api/auth/', views.AuthView.as_view()),
    path('api/order/', views.OrderView.as_view()),
]

```



```python
# views.py

import uuid
from rest_framework.views import APIView
from rest_framework.request import Request
from rest_framework.response import Response
from rest_framework.authentication import BaseAuthentication
from rest_framework.permissions import BasePermission
from rest_framework.exceptions import AuthenticationFailed

from app01 import models

# 1 先登陆认证
class AuthView(APIView):
    """ 用户登录认证 """

    def post(self, request, *args, **kwargs):
        print(request.data)  # {"username": "wupeiqi", "password": "123"}
        username = request.data.get('username')
        password = request.data.get('password')

        user_object = models.UserInfo.objects.filter(username=username, password=password).first()
        if not user_object:
            return Response({"code": 1000, "data": "用户名或密码错误"})

        token = str(uuid.uuid4())

        user_object.token = token
        user_object.save()

        return Response({"code": 0, "data": {"token": token, "name": username}})

# 创建token认证类
class TokenAuthentication(BaseAuthentication):
    def authenticate(self, request):
        token = request.query_params.get("token")
        if not token:
            raise AuthenticationFailed({"code": 1002, "data": "认证失败"})
        user_object = models.UserInfo.objects.filter(token=token).first()
        if not user_object:
            raise AuthenticationFailed({"code": 1002, "data": "认证失败"})
        return user_object, token

    def authenticate_header(self, request):
        return 'Bearer realm="API"'

# 3 创建权限a类判断当前对象是否员工
class PermissionA(BasePermission):
    message = {"code": 1003, 'data': "无权访问"}

    def has_permission(self, request, view):
        exists = request.user.roles.filter(title="员工").exists()
        if exists:
            return True
        return False

    def has_object_permission(self, request, view, obj):
        return True

# 3 创建权限b类判断当前对象是否主管
class PermissionB(BasePermission):
    message = {"code": 1003, 'data': "无权访问"}

    def has_permission(self, request, view):
        exists = request.user.roles.filter(title="主管").exists()
        if exists:
            return True
        return False

    def has_object_permission(self, request, view, obj):
        return True
# 4 视图类
class OrderView(APIView):
    authentication_classes = [TokenAuthentication, ]   # 4.1 应用上的认证类
    permission_classes = [PermissionA, PermissionA]		# 4.2 应用上2个权限类，都通过才能走get方法

    def get(self, request, *args, **kwargs):
        return Response({"code": 0, "data": {"user": None, 'list': [1, 2, 3]}})


class PayView(APIView):
    authentication_classes = [TokenAuthentication, ]
    permission_classes = [PermissionA, ]			# 4.3 此视图类只应用了一个权限类，过一个类就行

    def get(self, request, *args, **kwargs):
        return Response({"code": 0, "data": "数据..."})
```





### 关于 has_object_permission

当我们使用drf来编写 视图类时，如果是继承 `APIView`，则 `has_object_permission`不会被执行（没用），例如：

```python
from rest_framework.views import APIView

class PayView(APIView):
    authentication_classes = [TokenAuthentication, ]
    permission_classes = [PermissionA, ]

    def get(self, request, *args, **kwargs):
        return Response({"code": 0, "data": "数据..."})
```



但是，当我们后期学习了 视图类的各种骚操作之后，发现视图也可以继承 `GenericAPIView`，此时 **有可能** 会执行 `has_object_permission` 用于判断是否有权限访问某个特定ID的对象

![image-20210822105606505](drf.assets/image-20210822105606505.png)

调用 `self.get_object` 方法时，会按照 `permission_classes`中权限组件的顺序，依次执行他们的 `has_object_permission` 方法。

`self.get_object`其实就根据用户传入的 pk，搜索并获取某个对象的过程。



在之前定义权限类时，类中可以定义两个方法：`has_permission` 和 `has_object_permission` 

- `has_permission` ，在请求进入视图之前就会执行。
- `has_object_permission`，当视图中调用 `self.get_object`时就会被调用（删除、更新、查看某个对象时都会调用），一般用于检查对某个对象是否具有权限进行操作。

```python
class PermissionA(BasePermission):
    message = {"code": 1003, 'data': "无权访问"}

    def has_permission(self, request, view):
        exists = request.user.roles.filter(title="员工").exists()
        if exists:
            return True
        return False

    def has_object_permission(self, request, view, obj):
        return True
```



所以，让我们在编写视图类时，如果是直接获取间接继承了 GenericAPIView，同时内部调用 `get_object`方法，这样在权限中通过 `has_object_permission` 就可以进行权限的处理。





### 全局配置

```python
REST_FRAMEWORK = {
    "DEFAULT_PERMISSION_CLASSES":["xxxx.xxxx.xx.类名","xxxx.xxxx.xx.类名",]
}
```





### 底层源码实现

![image-20210822110404096](drf.assets/image-20210822110404096.png)



## 小结

- 请求的封装
- 版本的处理
  - 过程：选择版本处理类，获取用户传入的版本信息
  - 结果：在 `request.version = 版本`、`request.versioning_scheme=版本处理类的对象`
- 认证组件，在视图执行之前判断用户是否认证成功。
  - 过程：执行所有的认证类中的 `authenticate` 方法
    - 返回None，继续执行后续的认证类（都未认证成功，request.user 和 auth有默认值，也可以全局配置）
    - 返回2个元素的元组，中断
    - 抛出 `AuthenticationFailed`，中断
  - 结果：在 `request.user` 和 `request.auth` 赋值（后续代码可以使用）
- 权限
  - 过程：执行所有的权限类的`has_permission`方法，只有所有都返回True时，才表示具有权限
  - 结果：有权限则可以执行后续的视图，无权限则直接返回 自定义的错误信息





# DRF 中

## 6. 限流

限流，限制用户访问频率，例如：用户1分钟最多访问100次 或者 短信验证码一天每天可以发送50次， 防止盗刷。

- 对于匿名用户，使用用户IP作为唯一标识。
- 对于登录用户，使用用户ID或名称作为唯一标识。

```python
缓存={
	用户标识：[12:33,12:32,12:31,12:30,12,]    1小时/5次   12:34   11:34
{
```

### 使用流程

**1 安装 django-redis缓存模块，用于储存记录**

```
pip3 install django-redis
```

**2 在设置中配置安装的缓存**

```python
# settings.py
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379",						# 访问缓存的ip端口
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
            "PASSWORD": "qwe123",									# 访问的密码
        }
    }
}
```

![image-20210822115201724](drf.assets/image-20210822115201724.png)

**3 路由代码**

```python
from django.urls import path, re_path
from app01 import views

urlpatterns = [
    path('api/order/', views.OrderView.as_view()),
]
```

```python
# views.py

from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import exceptions
from rest_framework import status
from rest_framework.throttling import SimpleRateThrottle
from django.core.cache import cache as default_cache          # 3.1 的导入的缓存


class ThrottledException(exceptions.APIException):			# 3.7 自定的抛出异常类
    status_code = status.HTTP_429_TOO_MANY_REQUESTS			# 状态码，没啥用可直接pass
    default_code = 'throttled'							  # 异常原因，没啥用可直接pass


class MyRateThrottle(SimpleRateThrottle):		 		 # 3 创建缓存类，继承SimpleRateThrottle类
    cache = default_cache  								# 3.1 访问记录存放在django的缓存中（需设置缓存）
    scope = "user"  						    		# 3.2构造缓存中的key
    cache_format = 'throttle_%(scope)s_%(ident)s' 		 # 3.3进行用户唯一标识的拼接

    
    
    THROTTLE_RATES = {"user": "10/m"}			   # 3.4 设置访问频率，例如：1分钟允许访问10次
    											# 其他：'s'秒, 'sec', 'm'分, 'min', 'h'时, 'hour', 'd'天, 'day'
	
    def get_cache_key(self, request, view):			# 3.5此方法用于获取用户唯一标识，登陆的使用用户id，未登陆的用用户ip
        if request.user:
            ident = request.user.pk  								  # 用户ID
        else:
            ident = self.get_ident(request)  						   # 获取请求用户IP（去request中找请求头）  
        return self.cache_format % {'scope': self.scope, 'ident': ident} # throttle_user_11.11.11.11ser_2
    
	
    def throttle_failure(self):										# 3.6此方法当用户超出限制抛出异常	
        wait = self.wait()											# 此方法是父类的方法能获取到还要等待的时间
        detail = {
            "code": 1005,
            "data": "访问频率限制",
            'detail': "需等待{}s才能访问".format(int(wait))
        }
        raise ThrottledException(detail)							# 3.7 创建一个抛出异常的类返回自定的数据


class OrderView(APIView):										 # 3.8 视图类
    throttle_classes = [MyRateThrottle, ]						  # 3.9 视图类中限流类应用方法

    def get(self, request):										# 应用后一分钟只能访问十次
        return Response({"code": 0, "data": "数据..."})
```





### 多个限流类

本质，每个限流的类中都有一个 `allow_request` 方法，此方法内部可以有三种情况：

- 返回True，表示当前限流类允许访问，继续执行后续的限流类。
- 返回False，表示当前限流类不允许访问，继续执行后续的限流类。所有的限流类执行完毕后，读取所有不允许的限流，并计算还需等待的时间。
- 抛出异常，表示当前限流类不允许访问，后续限流类不再执行。



### **全局配置**

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES":["xxx.xxx.xx.限流类", ],
    "DEFAULT_THROTTLE_RATES": {
        "user": "10/m",
        "xx":"100/h"
    }
}
```

### **底层源码实现**

![image-20210822121259284](drf.assets/image-20210822121259284.png)

![image-20210822120127336](drf.assets/image-20210822120127336.png)

### 多限流示例

```python
# settings.py

...
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
            "PASSWORD": "qwe123",
        }
    }
}
```

```python
# urls.py

from django.urls import path, re_path, include
from app01 import views

urlpatterns = [
    path('api/order/', views.OrderView.as_view()),
]
```

```python
# views.py
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import exceptions
from rest_framework import status
from rest_framework.throttling import SimpleRateThrottle
from django.core.cache import cache as default_cache
class ThrottledException(exceptions.APIException):
    status_code = status.HTTP_429_TOO_MANY_REQUESTS
    default_code = 'throttled'
class MyRateThrottle(SimpleRateThrottle):
    cache = default_cache  # 访问记录存放在django的缓存中（需设置缓存）
    scope = "user"  # 构造缓存中的key
    cache_format = 'throttle_%(scope)s_%(ident)s'
    THROTTLE_RATES = {"user": "10/m"}

    def get_cache_key(self, request, view):
        if request.user:
            ident = request.user.pk  # 用户ID
        else:
            ident = self.get_ident(request)  # 获取用户IP
        return self.cache_format % {'scope': self.scope, 'ident': ident}
    def throttle_failure(self):	
        return False		# 1 以上和正常用一个限流一样，如果要用多个在这个方法中就不能抛出异常而是返回False，如果直接抛出异常则不会在走后面的限流类，想全走一遍就return False，直接抛出异常的方法好些

class OrderView(APIView):
    throttle_classes = [MyRateThrottle, xxxx] # 2视图类把多个限流类应用上第一个返回false时就会应用下一个限流类

    def get(self, request):
        return Response({"code": 0, "data": "数据..."})

    def throttled(self, request, wait):	# 3 多个限流类时都返回false后，则要视图中重写此方法返回错误信息
        detail = {
            "code": 1005,
            "data": "访问频率",
            'detail': "需等待{}s才能访问".format(int(wait))
        }
        raise ThrottledException(detail)

```



--------



## 7. Serializer（*）

drf中为我们提供了Serializer，他主要有两大功能：

- 对请求数据校验（底层调用Django的Form和ModelForm）
- 对数据库查询到的对象进行序列化



### 1数据校验

- 数据校验一般是用户post请求增加或者修改数据，传入的数据经过校验在保存到库

#### 基于Serializer

![image-20210823084033952](drf.assets/image-20210823084033952.png)

**1 用户要用post请求发送数据**

**2 在视图类post方法中调用`serializer`类实例化传入参数`data=request.data`**

**3 然后用实例对对象`ser.is_valid()：`判断用户的数据有没有通过校验，进行返回相应数据**,`出现错误在对象ser.errors`

**4 `serializer`类的创建，要继承`serializers.Serializer`类;导入路径如下**

```python
from rest_framework import serializers
```

**5 serializer类的使用与`from`相似，都是创建匹配字段，其中 级别 字段调用choices=对应的模型类choice字段**

**6 email有图中有几种验证方法，导入类或者用钩子方法都可**

**7 `request.data` 不仅可以解析读取用户以raw发送的`json`格式，还可以解析from-data格式的数据**



#### 基于ModelSerializer

**创建方式**

```python
from rest_framework import serializers 
class SubjectSerializer(serializers.ModelSerializer):
    class Meta:
        model = Subject
        fields = '__all__'
```

`上面的代码直接继承了ModelSerializer，通过Meta类的model属性指定要序列化的模型以及fields属性指定需要序列化的模型字段`

1 **创建模型类表**

```python
# models.py

from django.db import models


class Role(models.Model):
    """ 角色表 """
    title = models.CharField(verbose_name="名称", max_length=32)


class Department(models.Model):
    """ 部门表 """
    title = models.CharField(verbose_name="名称", max_length=32)


class UserInfo(models.Model):
    """ 用户表 """
    level_choices = ((1, "普通会员"), (2, "VIP"), (3, "SVIP"),)
    level = models.IntegerField(verbose_name="级别", choices=level_choices, default=1)

    username = models.CharField(verbose_name="用户名", max_length=32)
    password = models.CharField(verbose_name="密码", max_length=64)
    age = models.IntegerField(verbose_name="年龄", default=0)
    email = models.CharField(verbose_name="邮箱", max_length=64)
    token = models.CharField(verbose_name="TOKEN", max_length=64, null=True, blank=True)

    # 外键
    depart = models.ForeignKey(verbose_name="部门", to="Department", on_delete=models.CASCADE)
    
    # 多对多
    roles = models.ManyToManyField(verbose_name="角色", to="Role")

```

![](drf.assets/image-20210823085008103.png)

**2 创建自定义的`ModelSeriaLizer`类 要继承`serializers.ModelSerializer`,导入模块如下**

```python
from rest_framework import serializers
```

**3 在`modelserializer`类中创建Mete类，与modelfrom相同。选择对应的表，在选择展示的字段,`extra_kwargs`字段可添加每个表字段的限制**

**4 在视图类的使用post方法为用户新增数据；`modelserializer`类传入`data=`用户数据`request.data`实例出`ser`对象，用对象`ser.valid()：`进行校验，没有校验成功的错误信息在`ser.errors`**

**5 如果要进行seva保存时如果modelserializer类中新增了字段，需要在保在前去掉`ser.validated_data.pop('字段')`，另如果用户的数据字段不够，需要自己添加在保存如`ser.save(level=1，passwo='xxx')`括号内填添加的字段与内容**

**提示：save方法会返回新生成的数据对象。**





#### 基于ModelSerializer（含FK+M2M）

方法与上面两种都相同就是多了两个字段，外键与多对多字段，验证没什么区别。有区别的在用户提交时要用json提交数据，因为要多对多提交列表，如图

![image-20210823085945420](drf.assets/image-20210823085945420.png)

*提示：save方法会返回新生成的数据对象。*



#### 关于serializzer实例时的参数

```python
data=request.data   # 用户传入的数据去验证
partial=True		# true是用户传入的数据一个就只更新一个；false就用户要把所有要传的都传	
instance=模型类的对象 #用作序列化
many=True			#True是代表传入模型类是多个，false是对象只是一个
```



#### serializer钩子方法

```python
from rest_framework import serializers

# 1创建类继承modelserializer或serializer
class AuthSerializer(serializers.Serializer):
    # 2 要校验的字段写上
    username = serializers.CharField(label='用户名', write_only=True, required=False)
    phone = serializers.CharField(label='手机', write_only=True, required=False)
    password = serializers.CharField(label='密码', write_only=True, min_length=8)
	
    # 3 创建钩子方法，方法名是 validate_字段名
    def validate_username(self,value):
        # 4 在方法内便可自定校验方法了，校验成功返回value，失败抛出异常
        username = self.initial_data.get("username")
        phone = self.initial_data.get("phone")
        if not username and not phone:
            raise ValidationError("用户名或手机为空")
        if username and phone:
            raise ValidationError("提交数据异常")
        return value
```







### 2 序列化

**通过ORM从数据库获取到的 QuerySet 或 对象 均可以被序列化为 json 格式数据。**

```python
# models.py

from django.db import models


class Role(models.Model):
    """ 角色表 """
    title = models.CharField(verbose_name="名称", max_length=32)


class Department(models.Model):
    """ 部门表 """
    title = models.CharField(verbose_name="名称", max_length=32)


class UserInfo(models.Model):
    """ 用户表 """
    level_choices = ((1, "普通会员"), (2, "VIP"), (3, "SVIP"),)
    level = models.IntegerField(verbose_name="级别", choices=level_choices, default=1)

    username = models.CharField(verbose_name="用户名", max_length=32)
    password = models.CharField(verbose_name="密码", max_length=64)
    age = models.IntegerField(verbose_name="年龄", default=0)
    email = models.CharField(verbose_name="邮箱", max_length=64, null=True, blank=True)
    token = models.CharField(verbose_name="TOKEN", max_length=64, null=True, blank=True)

    depart = models.ForeignKey(verbose_name="部门", to="Department", on_delete=models.CASCADE, null=True, blank=True)
    roles = models.ManyToManyField(verbose_name="角色", to="Role")
```



#### 序列化基本字段

![image-20210823160227040](drf.assets/image-20210823160227040.png)

**视图类中拿到表的对象，然后modelserializer类传入参数`instance=`表对象，`many=True`代表传入的对象是多个的，如all取到的对象；如传入的对象只有一个则参数应该为`many=False`**

```python
# 切记， 如果从数据库获取的不是QuerySet对象，而是单一对象，例如：
data_object = modes.UserInfo.objects.filter(id=2).first()
ser = UserModelSerializer(instance=data_object,many=False)
print(ser.data)
```





#### 自定义字段

此方法增加了外键时把数字换成字符串展示及自定展示字段的钩子方法

1 如modelserializer类内新增了字段与模型类相同，则以新增的为准

2 要展示模型类内的外键如部门表时，可以自定一个字段 `xxx=serializers.CharField(source='get_level_display')`或者`xxx=serializers.CharField(source='depart.title')`

3 用钩子方法自定义时，创建字段用`字段=serializers.SerializerMethodFld()`，然后钩子方法命名为

```python
def get_字段名(self,obj):
	return '返回相关数据'
```

![image-20210823161608120](drf.assets/image-20210823161608120.png)













#### 序列化类的嵌套

1 对于外键与多对多的序列化还可以，在角色表的serializer类下重写一个 `部门字段= 部门表的serializer类`

![image-20210823162145013](drf.assets/image-20210823162145013.png)













### 3 数据校验&序列化

**1 对于类的校验与展示可以给重写字段加上`read_only`参数；`"read_only": True`代表用户提交数据时不用提交此字段；服务端序列化时则会返回给用户**

**2 相反字段设置`"read_only": False`时则不会序列化 而需要用户提供输入此字段**

**3 `write_only=True`与上面用法一样，只不过是相反的**

**4 如果是对多对多的字段进行修改增加，多对多是第三张表，save是做不到的，要在serializer类中创建create方法，save内部就会调用创建的create方法， 注，多对多表中的id字段要`"read_only": False`让用户需要提交id**

上述示例均属于单一功能（要么校验，要么序列化），其实当我们编写一个序列化类既可以做数据校验，也可以做序列化，例如：

![image-20210823210822789](drf.assets/image-20210823210822789.png)

![image-20210823211016050](drf.assets/image-20210823211016050.png)

![image-20210823211041662](drf.assets/image-20210823211041662.png)

#### 流程

```python
# models.py

from django.db import models


class Role(models.Model):
    """ 角色表 """
    title = models.CharField(verbose_name="名称", max_length=32)


class Department(models.Model):
    """ 部门表 """
    title = models.CharField(verbose_name="名称", max_length=32)


class UserInfo(models.Model):
    """ 用户表 """
    level_choices = ((1, "普通会员"), (2, "VIP"), (3, "SVIP"),)
    level = models.IntegerField(verbose_name="级别", choices=level_choices, default=1)

    username = models.CharField(verbose_name="用户名", max_length=32)
    password = models.CharField(verbose_name="密码", max_length=64)
    age = models.IntegerField(verbose_name="年龄", default=0)
    email = models.CharField(verbose_name="邮箱", max_length=64, null=True, blank=True)
    token = models.CharField(verbose_name="TOKEN", max_length=64, null=True, blank=True)

    depart = models.ForeignKey(verbose_name="部门", to="Department", on_delete=models.CASCADE, null=True, blank=True)
    roles = models.ManyToManyField(verbose_name="角色", to="Role")

```



```python
# urls.py

from django.urls import path, re_path, include
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view()),
]

```

```python
# views.py

from django.core.validators import EmailValidator
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import serializers

from app01 import models


class DepartModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = models.Department
        fields = ['id', "title"]
        extra_kwargs = {
            "id": {"read_only": False},  # 数据验证
            "title": {"read_only": True}  # 序列化
        }


class RoleModelSerializer(serializers.ModelSerializer):
    class Meta:
        model = models.Role
        fields = ['id', "title"]
        extra_kwargs = {
            "id": {"read_only": False},  # 数据验证
            "title": {"read_only": True}  # 序列化
        }


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(source="get_level_display", read_only=True)

    # Serializer嵌套，不是read_only，一定要自定义create和update，自定义新增和更新的逻辑。
    depart = DepartModelSerializer(many=False)
    roles = RoleModelSerializer(many=True)

    extra = serializers.SerializerMethodField(read_only=True)
    email2 = serializers.EmailField(write_only=True)

    # 数据校验：username、email、email2、部门、角色信息
    class Meta:
        model = models.UserInfo
        fields = [
            "username", "age", "email", "level_text", "depart", "roles", "extra", "email2"
        ]
        extra_kwargs = {
            "age": {"read_only": True},
            "email": {"validators": [EmailValidator, ]},
        }

    def get_extra(self, obj):
        return 666

    def validate_username(self, value):
        return value

    # 新增加数据时
    def create(self, validated_data):							# validated_data == ser对象
        """ 如果有嵌套的Serializer，在进行数据校验时，只有两种选择：
              1. 将嵌套的序列化设置成 read_only
              2. 自定义create和update方法，自定义新建和更新的逻辑
            注意：用户端提交数据的格式。
        """
        depart_id = validated_data.pop('depart')['id']						# 1 拿到部门id

        role_id_list = [ele['id'] for ele in validated_data.pop('roles')]		# 2  拿到角色id列表

        # 新增用户表
        validated_data['depart_id'] = depart_id								# 3 把角色id新增到字典
        user_object = models.UserInfo.objects.create(**validated_data)         # 4 在把角色信息加到用户表

        # 在用户表和角色表的关联表中添加对应关系
        user_object.roles.add(*role_id_list)			# 5 通过新增的角色对象跨表到角色表add添加角色的id

        return user_object							# 6 返回新增的对象


class UserView(APIView):
    """ 用户管理 """

    def get(self, request):
        """ 添加用户 """
        queryset = models.UserInfo.objects.all()
        ser = UserModelSerializer(instance=queryset, many=True)
        return Response({"code": 0, 'data': ser.data})

    def post(self, request):
        """ 添加用户 """
        ser = UserModelSerializer(data=request.data)
        if not ser.is_valid():
            return Response({'code': 1006, 'data': ser.errors})

        ser.validated_data.pop('email2')

        instance = ser.save(age=18, password="123", depart_id=1)

        # 新增之后的一个对象（内部调用UserModelSerializer进行序列化）
        print(instance)
        # ser = UserModelSerializer(instance=instance, many=False)
        # ser.data

        return Response({'code': 0, 'data': ser.data})

```



#### 底层源码实现

序列化的底层源码实现有别于上述其他的组件，序列化器相关类的定义和执行都是在视图中被调用的，所以源码的分析过程可以分为：定义类、序列化、数据校验。

源码1：序列化过程

![image-20210823235237512](drf.assets/image-20210823235237512.png)

![image-20210823235752483](drf.assets/image-20210823235752483.png)

源码2：数据校验过程

![image-20210824001814091](drf.assets/image-20210824001814091.png)

![image-20210824001844381](drf.assets/image-20210824001844381.png)









### read_only 的批量设置

```python
from rest_framework import serializers
from rest_framework.exceptions import ValidationError
from api import models


class TopicSerializer(serializers.ModelSerializer):
    class Meta:
        model = models.Topic
        fields = ['id', "title", "is_hot"]
        # 把要设置字段写入就可
        read_only_fields = ['is_hot'] 
        # 等同于下面
        extra_kwargs = {'is_hot': {'read_only': True}}
        

```







## 8. 视图

### 8.1 APIView

- View，django的
- APIView，drf的，在请求到来时，新增了：免除csrf、请求封装、版本、认证、权限、限流的功能。

```python
class GenericAPIView(APIView):
    pass # 10功能

class GenericViewSet(xxxx.View-2个功能, GenericAPIView):
    pass # 5功能能

class UserView(GenericViewSet):
    def get(self,request):
        pass
```

`APIView`是drf中 “顶层” 的视图类，在他的内部主要实现drf基础的组件的使用，例如：版本、认证、权限、限流等。

```python
# urls.py

from django.urls import path, re_path, include
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view()),
    path('api/users/<int:pk>/', views.UserDetailView.as_view()),
]
```

```python
# views.py

from rest_framework.views import APIView
from rest_framework.response import Response

class UserView(APIView):
    
    # 认证、权限、限流等
    
    def get(self, request):
		# 业务逻辑：查看列表
        return Response({"code": 0, 'data': "..."})

    def post(self, request):
        # 业务逻辑：新建
        return Response({'code': 0, 'data': "..."})
    
class UserDetailView(APIView):
    
	# 认证、权限、限流等
        
    def get(self, request,pk):
		# 业务逻辑：查看某个数据的详细
        return Response({"code": 0, 'data': "..."})

    def put(self, request,pk):
        # 业务逻辑：全部修改
        return Response({'code': 0, 'data': "..."})
    
    def patch(self, request,pk):
        # 业务逻辑：局部修改，可以只传一行数据的一项
        return Response({'code': 0, 'data': "..."})
    
    def delete(self, request,pk):
        # 业务逻辑：删除
        return Response({'code': 0, 'data': "..."})
```



### 8.2 GenericAPIView

`GenericAPIView` 继承APIView，在APIView的基础上又增加了一些功能。例如：`get_queryset`、`get_object`等。

实际在开发中一般不会直接继承它，他更多的是担任 `中间人`的角色，为子类提供公共功能。

```python
# urls.py

from django.urls import path, re_path, include
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view()),
    path('api/users/<int:pk>/', views.UserDetailView.as_view()),
]
```

```python
# views.py

from rest_framework.generics import GenericAPIView
from rest_framework.response import Response

class UserView(GenericAPIView):
    queryset = models.UserInfo.objects.filter(status=True)  # 创建的变量，在视图方法中可用self.get_queryset()获取
    serializer_class = 序列化类							# 创建的变量，在视图方法中可用self.get_serializer()获取
    
    def get(self, request):
        queryset = self.get_queryset()
        ser = self.get_serializer(intance=queryset,many=True)
        print(ser.data)
        return Response({"code": 0, 'data': "..."})    
```



注意：最大的意义，将数据库查询、序列化类提取到类变量中，后期再提供公共的get/post/put/delete等方法，让开发者只定义类变量，自动实现增删改查。



### 8.3 GenericViewSet

![image-20210824092131703](drf.assets/image-20210824092131703.png)

`GenericViewSet`类中没有定义任何代码，他就是继承 `ViewSetMixin` 和 `GenericAPIView`，也就说他的功能就是将继承的两个类的功能继承到一起。

- `GenericAPIView`，将数据库查询、序列化类的定义提取到类变量中，便于后期处理。
- `ViewSetMixin`，将 get/post/put/delete 等方法映射到 list、create、retrieve、update、partial_update、destroy方法中，让视图不再需要两个类。

```python
# urls.py

from django.urls import path, re_path, include
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view({"get":"list","post":"create"})),
    path('api/users/<int:pk>/', views.UserView.as_view({"get":"retrieve","put":"update","patch":"partial_update","delete":"destory"})),
]
```

```python
# views.py

from rest_framework.viewsets import GenericViewSet
from rest_framework.response import Response

    
class UserView(GenericViewSet):
    
	# 认证、权限、限流等
    queryset = models.UserInfo.objects.filter(status=True)
    serializer_class = 序列化类
    
    def list(self, request):
		# 业务逻辑：查看列表
        queryset = self.get_queryset()
        ser = self.get_serializer(intance=queryset,many=True)
        print(ser.data)
        return Response({"code": 0, 'data': "..."})

    def create(self, request):
        # 业务逻辑：新建
        return Response({'code': 0, 'data': "..."})
    
    def retrieve(self, request,pk):
		# 业务逻辑：查看某个数据的详细
        return Response({"code": 0, 'data': "..."})

    def update(self, request,pk):
        # 业务逻辑：全部修改
        return Response({'code': 0, 'data': "..."})
    
    def partial_update(self, request,pk):
        # 业务逻辑：局部修改
        return Response({'code': 0, 'data': "..."})
    
    def destory(self, request,pk):
        # 业务逻辑：删除
        return Response({'code': 0, 'data': "..."})
```



注意：开发中一般也很少直接去继承他，因为他也属于是 `中间人`类，在原来 `GenericAPIView` 基础上又增加了一个映射而已。



### 8.4 五大类

**可以直接继承`ModelViewSet`类，此类继承了5个类**

```python
from rest_framework.viewsets import ModelViewSet

class UserView(ModelViewSet):
    pass
```

在drf的为我们提供好了5个用于做 增、删、改（含局部修改）、查列表、查单个数据的5个类（需结合 `GenericViewSet` 使用）。

```python
# urls.py

from django.urls import path, re_path, include
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view({"get":"list","post":"create"})),
    path('api/users/<int:pk>/', views.UserView.as_view({"get":"retrieve","put":"update","patch":"partial_update","delete":"destroy"})),
]
```

```python
# views.py

from rest_framework.viewsets import GenericViewSet
from rest_framework.mixins import (
    ListModelMixin, CreateModelMixin, RetrieveModelMixin, UpdateModelMixin,
    DestroyModelMixin, ListModelMixin
)

class UserView(CreateModelMixin,RetrieveModelMixin, UpdateModelMixin, DestroyModelMixin,ListModelMixin,GenericViewSet):
    
	# 认证、权限、限流等
    queryset = models.UserInfo.objects.filter(status=True)
    serializer_class = 序列化类
```



在这个5个类中已帮我们写好了 `list`、`create`、`retrieve`、`update`、`partial_update`、`destory` 方法，我们只需要在根据写 类变量：queryset、serializer_class即可。

**示例1：**

![image-20210824230441249](drf.assets/image-20210824230441249.png)

```python
# urls.py

from django.urls import path
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view({"get": "list"})),
    path('api/users/<int:pk>/', views.UserView.as_view({"get": "retrieve"})),
]
```

```python
# views.py

from rest_framework import serializers
from rest_framework.viewsets import GenericViewSet
from rest_framework import mixins
from app01 import models


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["username", "age", "email", "level_text", "extra"]

    def get_extra(self, obj):
        return 666


class UserView(mixins.ListModelMixin, mixins.RetrieveModelMixin, GenericViewSet):
    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer
```



**示例2：**

![image-20210824231043061](drf.assets/image-20210824231043061.png)

```python
# urls.py

from django.urls import path
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view({"get": "list", "post": "create"})),
    path('api/users/<int:pk>/', views.UserView.as_view({"get": "retrieve"})),
]
```

```python
# views.py

from rest_framework import serializers
from rest_framework.viewsets import GenericViewSet
from rest_framework import mixins
from app01 import models


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["username", "age", "email", "level_text", "extra"]

    def get_extra(self, obj):
        return 666


class UserView(mixins.ListModelMixin, mixins.RetrieveModelMixin, mixins.CreateModelMixin, GenericViewSet):
    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")
```





**示例3：**

```python
# urls.py

from django.urls import path
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view(
        {"get": "list", "post": "create"}
    )),
    path('api/users/<int:pk>/', views.UserView.as_view(
        {"get": "retrieve", "put": "update", "patch": "partial_update", "delete": "destroy"}
    )),
]

```

```python
# views.py

from rest_framework import serializers
from rest_framework.viewsets import GenericViewSet
from rest_framework import mixins
from app01 import models


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["username", "age", "email", "level_text", "extra"]

    def get_extra(self, obj):
        return 666


class UserView(mixins.ListModelMixin,
               mixins.RetrieveModelMixin,
               mixins.CreateModelMixin,
               mixins.UpdateModelMixin,
               mixins.DestroyModelMixin,
               GenericViewSet):
    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")
	
	def perform_update(self, serializer):
        serializer.save()
        
    def perform_destroy(self, instance):
        instance.delete()
```



**示例4：**

```python
# urls.py

from django.urls import path
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view(
        {"get": "list", "post": "create"}
    )),
    path('api/users/<int:pk>/', views.UserView.as_view(
        {"get": "retrieve", "put": "update", "patch": "partial_update", "delete": "destroy"}
    )),
]

```

```python
# views.py
from rest_framework import serializers
from rest_framework.viewsets import ModelViewSet
from app01 import models


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["username", "age", "email", "level_text", "extra"]

    def get_extra(self, obj):
        return 666


class UserView(ModelViewSet):
    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")
```



在开发过程中使用 `五大类` 或 `ModelViewSet` 是比较常见的，并且如果他们内部的某些功能不够用，还可以进行重新某些方法进行扩展。



问题：drf中提供了这么多视图，以后那个用的比较多？

- 接口与数据库操作无关，直接继承APIView

- 接口背后需要对数据库进行操作，一般：`ModelViewSet` 或 `CreateModelMixin、ListModelMixin...`

  ```
  - 利用钩子自定义功能。
  - 重写某个写方法，实现更加完善的功能。
  ```

- 根据自己公司的习惯，自定义 ：`ModelViewSet` 或 `CreateModelMixin、ListModelMixin...`









## 9. 条件搜索

如果某个API需要传递一些条件进行搜索，其实就在是URL后面通过GET传参即可，例如：

```
/api/users?age=19&category=12
```

在drf中也有相应组件可以支持条件搜索。

### 9.1 自定义Filter

![image-20210825200814769](drf.assets/image-20210825200814769.png)

```python
# urls.py

from django.urls import path
from app01 import views

urlpatterns = [
    path('api/users/', views.UserView.as_view(
        {"get": "list", "post": "create"}
    )),
    path('api/users/<int:pk>/', views.UserView.as_view(
        {"get": "retrieve", "put": "update", "patch": "partial_update", "delete": "destroy"}
    )),
]
```

```python
# views.py

from rest_framework import serializers
from rest_framework.viewsets import ModelViewSet
from rest_framework.filters import BaseFilterBackend
from app01 import models


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["username", "age", "email", "level_text", "extra"]

    def get_extra(self, obj):
        return 666


class Filter1(BaseFilterBackend):
    def filter_queryset(self, request, queryset, view):
        age = request.query_params.get('age')
        if not age:
            return queryset
        return queryset.filter(age=age)


class Filter2(BaseFilterBackend):
    def filter_queryset(self, request, queryset, view):
        user_id = request.query_params.get('id')
        if not user_id:
            return queryset
        return queryset.filter(id__gt=user_id)


class UserView(ModelViewSet):
    filter_backends = [Filter1, Filter2]

    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")
```



### 9.2 第三方Filter

在drf开发中有一个常用的第三方过滤器：DjangoFilterBackend。

```
pip install django-filter
```

注册app：

```python
INSTALLED_APPS = [
    ...
    'django_filters',
    ...
]
```

#### 视图配置和应用（示例1）

```python
# views.py
from rest_framework import serializers
from rest_framework.viewsets import ModelViewSet
from django_filters.rest_framework import DjangoFilterBackend
from app01 import models


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["username", "age", "email", "level_text", "extra"]

    def get_extra(self, obj):
        return 666


class UserView(ModelViewSet):
    filter_backends = [DjangoFilterBackend, ]     # 1 应用上
    filterset_fields = ["id", "age", "email"]     # 2 配置上，些配置用户用户在url中填入 api/?id=1&age=12 就会过滤

    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")

```



#### 视图配置和应用（示例2）

```python
from rest_framework import serializers
from rest_framework.viewsets import ModelViewSet
from django_filters.rest_framework import DjangoFilterBackend
from django_filters import FilterSet, filters
from app01 import models


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    depart_title = serializers.CharField(
        source="depart.title",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["id", "username", "age", "email", "level_text", "extra", "depart_title"]

    def get_extra(self, obj):
        return 666


class MyFilterSet(FilterSet):			# 3 创建filter 类继承FilterSet
    # 3.1 CharFilter代表是字符串，"depart__title"代表跨表到部门表，"exact"代表等于
    depart = filters.CharFilter(field_name="depart__title", lookup_expr="exact")
    # 3.2 Number代表数字，'gte'代表id大于等于
    min_id = filters.NumberFilter(field_name='id', lookup_expr='gte')  

    class Meta:
        model = models.UserInfo
        fields = ["id","min_id", "depart"]     # id代表支持id等于什么

# 用户url使用  ?min_id=5
class UserView(ModelViewSet):
    filter_backends = [DjangoFilterBackend, ]    # 1 应用上filter
    filterset_class = MyFilterSet				# 2 配置这创建一个类

    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")

```



#### 视图配置和应用（示例3）

```python
from rest_framework import serializers
from rest_framework.viewsets import ModelViewSet
from django_filters.rest_framework import DjangoFilterBackend, OrderingFilter
from django_filters import FilterSet, filters
from app01 import models


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    depart_title = serializers.CharField(
        source="depart.title",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["id", "username", "age", "email", "level_text", "extra", "depart_title"]

    def get_extra(self, obj):
        return 666


class MyFilterSet(FilterSet):
    # /api/users/?min_id=2  -> id>=2 ，大于等于
    min_id = filters.NumberFilter(field_name='id', lookup_expr='gte')

    # /api/users/?name=wupeiqi  -> not ( username=wupeiqi )  ，取反
    name = filters.CharFilter(field_name="username", lookup_expr="exact", exclude=True)

    # /api/users/?depart=xx     -> depart__title like %xx%  ,包含
    depart = filters.CharFilter(field_name="depart__title", lookup_expr="contains")

    # /api/users/?token=true      -> "token" IS NULL
    # /api/users/?token=false     -> "token" IS NOT NULL  ，为空或者不空  
    token = filters.BooleanFilter(field_name="token", lookup_expr="isnull")

    # /api/users/?email=xx     -> email like xx%   ，以什么开头
    email = filters.CharFilter(field_name="email", lookup_expr="startswith")

    # /api/users/?level=2&level=1   -> "level" = 1 OR "level" = 2（必须的是存在的数据，否则报错-->内部有校验机制）
    # level = filters.AllValuesMultipleFilter(field_name="level", lookup_expr="exact")
    level = filters.MultipleChoiceFilter(field_name="level", lookup_expr="exact", choices=models.UserInfo.level_choices)

    # /api/users/?age=18,20     -> age in [18,20]
    age = filters.BaseInFilter(field_name='age', lookup_expr="in")

    # /api/users/?range_id_max=10&range_id_min=1    -> id BETWEEN 1 AND 10
    range_id = filters.NumericRangeFilter(field_name='id', lookup_expr='range')

    # /api/users/?ordering=id     -> order by id asc
    # /api/users/?ordering=-id     -> order by id desc
    # /api/users/?ordering=age     -> order by age asc
    # /api/users/?ordering=-age     -> order by age desc
    ordering = filters.OrderingFilter(fields=["id", "age"])

    # /api/users/?size=1     -> limit 1（自定义搜索）
    size = filters.CharFilter(method='filter_size', distinct=False, required=False)
    
    class Meta:
        model = models.UserInfo
        fields = ["id", "min_id", "name", "depart", "email", "level", "age", 'range_id', "size", "ordering"]

    def filter_size(self, queryset, name, value):
        int_value = int(value)
        return queryset[0:int_value]


class UserView(ModelViewSet):
    filter_backends = [DjangoFilterBackend, ]
    filterset_class = MyFilterSet

    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")

```

#### `lookup_expr`有很多常见选择

```python
'exact': _(''),
'iexact': _(''),

'contains': _('contains'),
'icontains': _('contains'),
'startswith': _('starts with'),
'istartswith': _('starts with'),
'endswith': _('ends with'),  
'iendswith': _('ends with'),
    
'gt': _('is greater than'),
'gte': _('is greater than or equal to'),
'lt': _('is less than'),
'lte': _('is less than or equal to'),

'in': _('is in'),
'range': _('is in range'),
'isnull': _(''),
    
'regex': _('matches regex'),
'iregex': _('matches regex'),
```



#### 全局配置和应用

```python
# settings.py 全局配置

REST_FRAMEWORK = {
    'DEFAULT_FILTER_BACKENDS': ['django_filters.rest_framework.DjangoFilterBackend',]
}
```





### 9.3 内置Filter

drf源码中内置了2个filter，分别是：

#### OrderingFilter，支持排序。

```python
from rest_framework import serializers
from rest_framework.viewsets import ModelViewSet
from app01 import models
from rest_framework.filters import OrderingFilter


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    depart_title = serializers.CharField(
        source="depart.title",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["id", "username", "age", "email", "level_text", "extra", "depart_title"]

    def get_extra(self, obj):
        return 666


class UserView(ModelViewSet):
    filter_backends = [OrderingFilter, ]
    # ?order=id
    # ?order=-id
    # ?order=age
    ordering_fields = ["id", "age"]

    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")
```

#### SearchFilter，支持模糊搜索。

```python
from rest_framework import serializers
from rest_framework.viewsets import ModelViewSet
from app01 import models
from rest_framework.filters import SearchFilter


class UserModelSerializer(serializers.ModelSerializer):
    level_text = serializers.CharField(
        source="get_level_display",
        read_only=True
    )
    depart_title = serializers.CharField(
        source="depart.title",
        read_only=True
    )
    extra = serializers.SerializerMethodField(read_only=True)

    class Meta:
        model = models.UserInfo
        fields = ["id", "username", "age", "email", "level_text", "extra", "depart_title"]

    def get_extra(self, obj):
        return 666


class UserView(ModelViewSet):
    # ?search=武沛%齐
    filter_backends = [SearchFilter, ]
    search_fields = ["id", "username", "age"]

    queryset = models.UserInfo.objects.all()
    serializer_class = UserModelSerializer

    def perform_create(self, serializer):
        """ 序列化：对请求的数据校验成功后，执行保存。"""
        serializer.save(depart_id=1, password="123")

```

```python
"app01_userinfo"."id" LIKE %武沛齐% ESCAPE '\' 
OR 
"app01_userinfo"."username" LIKE %武沛齐% ESCAPE '\' 
OR 
"app01_userinfo"."age" LIKE %武沛齐% ESCAPE '\'
```





## 10. 分页

在查看数据列表的API中，如果 数据量 比较大，肯定不能把所有的数据都展示给用户，而需要通过分页展示。

在drf中为我们提供了一些分页先关类：

```python
BasePagination，分页基类
PageNumberPagination(BasePagination) # 支持 /accounts/?page=4&page_size=100 格式的分页,访问第四页显示100条
LimitOffsetPagination(BasePagination) # 支持 ?offset=100&limit=10 格式的分页,定位到100条后，向后取10条
CursorPagination(BasePagination)	# 支持 上一下 & 下一页 格式的分页（不常用），
```

### 10.1 APIView视图

如果编写视图是直接继承APIView，那么在使用分页时，就必须自己手动 实例化 和 调用相关方法。

#### 1.PageNumberPagination 

**如下方法只能选择第几页，及默认显示几条的设置方法**

![image-20210826165642846](drf.assets/image-20210826165642846.png)

1 导入分页类,并在视图类方法内实例类拿到p对象

```python
from rest_framework.pagination import PageNumberPagination


class xxx(APIViiew):
    def get(self,request,*args,**kwargs):
        
        pager = PageNumberPagination()
        p = pager.paginate_queryset()
```

2  视图方法中`p对象.paginate_queryset(模型类对象，request，self)`，然后把这个对象放到modelserializer类中

3 可在如上图进行配置每页显示多少

**如下方法可以选择第几页及多少条**

![image-20210826165918075](drf.assets/image-20210826165918075.png)







#### 2.LimitOffsetPagination

此类应用方法和上面一致，使用有些不同

![image-20210826170617347](drf.assets/image-20210826170617347.png)



#### 3.CursorPagination

![image-20210826171203863](drf.assets/image-20210826171203863.png)















### 10.2 GenericAPIView派生类

**使用方法与上面用户的url使用都一样，视图中应用有小差别**

如果是使用 `ListModelMixin` 或 `ModelViewSet` ，则只需要配置相关类即可，内部会自动执行相关分页的方法。

#### 1.PageNumberPagination

![image-20210827003534400](drf.assets/image-20210827003534400.png)

#### 2.LimitOffsetPagination

![image-20210827003357244](drf.assets/image-20210827003357244.png)

#### 3.CursorPagination

![image-20210827003146430](drf.assets/image-20210827003146430.png)







#### 全局配置方法

![image-20220731230441841](drf.assets/image-20220731230441841.png)





## 11. 路由

在之前进行drf开发时，对于路由我们一般进行两种配置：

- 视图继承APIView

  ```python
  from django.urls import path
  from app01 import views
  
  urlpatterns = [
      path('api/users/', views.UserView.as_view()),
  ]
  ```

- 视图继承 `ViewSetMixin`（GenericViewSet、ModelViewSet）

  ```python
  from django.urls import path, re_path, include
  from app01 import views
  
  urlpatterns = [
      path('api/users/', views.UserView.as_view({"get":"list","post":"create"})),
      path('api/users/<int:pk>/', views.UserView.as_view({"get":"retrieve","put":"update","patch":"partial_update","delete":"destory"})),
  ]
  ```

  对于这种形式的路由，drf中提供了更简便的方式：

  ```python
  from rest_framework import routers
  from app01 import views
  
  router = routers.SimpleRouter()
  router.register(r'api/users', views.UserView)
  
  urlpatterns = [
      # 其他URL
      # path('xxxx/', xxxx.as_view()),
  ]
  
  urlpatterns += router.urls
  ```

  

  也可以利用include，给URL加前缀：

  ```python
  from django.urls import path, include
  from rest_framework import routers
  from app01 import views
  
  router = routers.SimpleRouter()
  router.register(r'users', views.UserView)
  
  urlpatterns = [
      path('api/', include((router.urls, 'app_name'), namespace='instance_name')),
      # 其他URL
      # path('forgot-password/', ForgotPasswordFormView.as_view()),
  ]
  ```















## 12. 解析器

之前使用 `request.data` 获取请求体中的数据。

这个 `reqeust.data` 的数据怎么来的呢？其实在drf内部是由解析器，根据请求者传入的数据格式 + 请求头来进行处理。

#### 1.JSONParser 

**此解析设置后只能json格式且请求头也json,如图**

![image-20210827081058194](drf.assets/image-20210827081058194.png)



#### 2.FormParser

**此方法只能from-data格式和如下图请求头**

![image-20210827081244795](drf.assets/image-20210827081244795.png)



#### 3.MultiPartParser

**此方法用于有文件，又有文本**

![image-20210827083047327](drf.assets/image-20210827083047327.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="http://127.0.0.1:8000/test/" method="post" enctype="multipart/form-data">
    <input type="text" name="user" />
    <input type="file" name="img">

    <input type="submit" value="提交">

</form>
</body>
</html>
```



#### 4.FileUploadParser

此方法只能二进制文件，请求头要求如下

![image-20210827084403453](drf.assets/image-20210827084403453.png)

解析器不用特别设置，**会有默认的设置**

解析器可以设置多个，默认解析器：

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.parsers import MultiPartParser, JSONParser, FormParser


class UserView(APIView):

    def post(self, request):
        print(request.content_type)
        print(request.data)

        return Response("...")

```

 



































































