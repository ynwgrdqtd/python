# 一 权限组件开发

 web程序是通过 url 的切换来查看不同的页面（功能），所以权限指的其实就是URL，对url控制就是对权限的控制。

结论：一个人有多少个权限就取决于他有多少个URL的访问权限。

## 1 创建模型类

- 用户表UserInfo：用户表与职位表多对多关系
- 职位表Role：职位表与权限表多对多关系
- 权限表（url）Permission：权限表ForeignKey外键菜单表
- 菜单表Menu

```python
# mpdels.py
from django.db import models


class Menu(models.Model):
    """
    菜单表
    """
    title = models.CharField(verbose_name='一级菜单名称', max_length=32)
    icon = models.CharField(verbose_name='图标', max_length=32, null=True, blank=True)

    def __str__(self):
        return self.title


class Permission(models.Model):
    """
    权限表
    """
    title = models.CharField(verbose_name='标题', max_length=32)
    url = models.CharField(verbose_name='含正则的URL', max_length=128)

    name = models.CharField(verbose_name='URL别名', max_length=32, unique=True)

    menu = models.ForeignKey(verbose_name='所属菜单', to='Menu', null=True, blank=True, help_text='null表示不是菜单;非null表示是二级菜单',on_delete=models.CASCADE)

    pid = models.ForeignKey(verbose_name='关联的权限', to='Permission', null=True, blank=True, related_name='parents',
                            help_text='对于非菜单权限需要选择一个可以成为菜单的权限，用户做默认展开和选中菜单',on_delete=models.CASCADE)

    def __str__(self):
        return self.title


class Role(models.Model):
    """
    角色
    """
    title = models.CharField(verbose_name='角色名称', max_length=32)
    permissions = models.ManyToManyField(verbose_name='拥有的所有权限', to='Permission', blank=True)

    def __str__(self):
        return self.title


class UserInfo(models.Model):
    """
    用户表
    """
    name = models.CharField(verbose_name='用户名', max_length=32)
    password = models.CharField(verbose_name='密码', max_length=64)
    email = models.CharField(verbose_name='邮箱', max_length=32)
    roles = models.ManyToManyField(verbose_name='拥有的所有角色', to='Role', blank=True)

    def __str__(self):
        return self.name


```

录入相关数据后



## 2 权限信息初始化（写session）

1. 用户登陆后把此用户对应能用哪些url和菜单写入到不同的session中
2. 写session的操作放在专门权限的子`app`中，创建py文件调用
3. session和键名写在settings配置中，以后更改方便

```python
# 业务文件
from django.shortcuts import HttpResponse, render, redirect
from rbac import models
from rbac.service.init_permission import init_permission


def login(request):
    # 1. 用户登录
    if request.method == 'GET':
        return render(request, 'login.html')
    user = request.POST.get('user')
    pwd = request.POST.get('pwd')

    current_user = models.UserInfo.objects.filter(name=user, password=pwd).first()
    if not current_user:
        return render(request, 'login.html', {'msg': '用户名或密码错误'})

    init_permission(current_user, request)								     #  写session写这

    return redirect('/customer/list/')
```

```python
# init_permission.py

from django.conf import settings


def init_permission(current_user, request):
    """
    用户权限的初始化
    :param current_user: 当前用户对象
    :param request: 请求相关所有数据
    :return:
    """
    # 2. 权限信息初始化
    # 根据当前用户信息获取此用户所拥有的所有权限，并放入session。
    # 当前用户所有权限
    permission_queryset = current_user.roles.filter(permissions__isnull=False).values("permissions__id",
                                                                                      "permissions__title",
                                                                                      "permissions__url",
                                                                                      "permissions__name",
                                                                                      "permissions__pid_id",
                                                                                      "permissions__pid__title",
                                                                                      "permissions__pid__url",
                                                                                      "permissions__menu_id",
                                                                                      "permissions__menu__title",
                                                                                      "permissions__menu__icon"
                                                                                      ).distinct()

    # 3. 获取权限+菜单信息
     permission_dict = {}

    menu_dict = {}

    for item in permission_queryset:		# 4. 循环每个字典
        
        permission_dict[item['permissions__name']] = {     
            'id': item['permissions__id'],
            'title': item['permissions__title'],
            'url': item['permissions__url'],
            'pid': item['permissions__pid_id'],
            'p_title': item['permissions__pid__title'],
            'p_url': item['permissions__pid__url'],
        }

        menu_id = item['permissions__menu_id']
        if not menu_id:
            continue
        node = {'id': item['permissions__id'], 'title': item['permissions__title'], 'url':      item['permissions__url']}

        if menu_id in menu_dict:
            menu_dict[menu_id]['children'].append(node)
        else:
            menu_dict[menu_id] = {
                'title': item['permissions__menu__title'],
                'icon': item['permissions__menu__icon'],
                'children': [node, ]
            }

    request.session[settings.PERMISSION_SESSION_KEY] = permission_dict
    request.session[settings.MENU_SESSION_KEY] = menu_dict

```



## 3 创建中间件（session验权限）

1. 在权限子app中写一个中间件，验证用户访问url的权限
2. 写完配置settings中设置中间件

```python
# rbac.py 中间件

import re
from django.utils.deprecation import MiddlewareMixin
from django.shortcuts import HttpResponse
from django.conf import settings


class RbacMiddleware(MiddlewareMixin):
    """
    用户权限信息校验
    """

    def process_request(self, request):
        """
        当用户请求刚进入时候出发执行
        :param request:
        :return:
        """

        """
        1. 获取当前用户请求的URL
        2. 获取当前用户在session中保存的权限列表 ['/customer/list/','/customer/list/(?P<cid>\\d+)/']
        3. 权限信息匹配
        """
        current_url = request.path_info
        for valid_url in settings.VALID_URL_LIST: 											# 1 循环白名单路径
            if re.match(valid_url, current_url):														 					return None													# 白名单中的URL无需权限验证即可访问

        permission_list = request.session.get(settings.PERMISSION_SESSION_KEY)			   # 2 打开用户的session
        if not permission_list:															# 无数据就是未登陆
            return HttpResponse('未获取到用户权限信息，请登录！')												

        flag = False															

        for url in permission_list:														# 3 循环用户的session
            reg = "^%s$" % url												# 把每个url加上开头和结尾的正则表达式
            if re.match(reg, current_url):						# 4 用表达式来验证此次访问的url用户有没有权限访问
                flag = True															 # 验证通过就让它过中间件
                break

        if not flag:																# 5 验证不过不给过中间件
            return HttpResponse('无权访问')

```







## 4 一二级菜单

使用inclusion_tag渲染，二级菜单功能有进入时自动展开一级菜单并默认选中进入的二级菜单

1. 在权限子`app`中创建父模板
2. 创建菜单函数子模板渲染至父模板
3. 导入 `Library` 并实例对象，对象`.`调用`inclusion_tag`方法，参数传入子模板路径，然后当成装饰器
4. 在父模板中调用装饰过后`inclusion_tag`方法

```python
# rbac.py 子模板函数
import re
from django.template import Library
from django.conf import settings
from collections import OrderedDict

register = Library()									# 1 实例化对象


@register.inclusion_tag('rbac/static_menu.html')         
def static_menu(request):
    """
    创建一级菜单
    :return:
    """
    menu_list = request.session[settings.MENU_SESSION_KEY]
    return {'menu_list': menu_list}


@register.inclusion_tag('rbac/multi_menu.html')    # 2 用inclusion_tag把子模板装饰进来
def multi_menu(request):
    """
    创建二级菜单
    :return:
    """
    menu_dict = request.session[settings.MENU_SESSION_KEY]		# 3 读取到session

    												
    key_list = sorted(menu_dict)							# 4 对字典的key进行排序,循环时菜单才有顺序

    
    ordered_dict = OrderedDict()							# 5 创建空的有序字典等下装排完顺序的字典

    for key in key_list:								# 6 循环顺序的键
        val = menu_dict[key]							# 循环取的是一级菜单
        val['class'] = 'hide'							# 7 对一级菜单先加上hide默认先隐藏二级菜单

        for per in val['children']:						# 8 循环二级菜单		
            regex = "^%s$" % (per['url'],)
            if re.match(regex, request.path_info):	   # 9 取二级菜单的url与当前访问的url作比较 
                per['class'] = 'active'				  # 10 成立就对当前标签加上active，默认选中	
                val['class'] = ''					 # 11 在把一级标签设置class属性为空，变成可以显示子标签
        ordered_dict[key] = val						# 12 数据配置好后传入子模板

    return {'menu_dict': ordered_dict}
```

```html
<!-- static_menu.html 一级菜单子模板 -->

<div class="static-menu">
    {% for item in menu_list %}
        <a href="{{ item.url }}">
            <span class="icon-wrap"><i class="fa {{ item.icon }}"></i></span> {{ item.title }}</a>
    {% endfor %}
</div>
```

```html
<!-- multi-menu.html 二级菜单子模板 -->

<div class="multi-menu">
    {% for item in menu_dict.values %}				<!-- 1 循环传入的字典值 -->
        <div class="item">									<!-- 2 展示一级图标 				展示一级标题-->
            <div class="title"><span class="icon-wrap"><i class="fa {{ item.icon }}"></i></span> {{ item.title }}			</div>
            <!-- 3 创建二级标签的div,class属性用一级传入的 -->
            <div class="body {{ item.class }}">
                <!-- 4 循环传入的二级字典值 -->
                {% for per in item.children %}
                
                    <a class="{{ per.class }}" href="{{ per.url }}">{{ per.title }}</a>
                {% endfor %}
            </div>

        </div>
    {% endfor %}
</div>
```

```html
<!-- 父模板 -->

{% load static  %}
{% load rbac %}
<!DOCTYPE html>
<html lang="en">
<head>
  
</head>
<body>


	<!-- 父模板中引用，并传入参数 -->
    {% multi_menu request %}

   
</body>
</html>
```



## 5 非菜单项默认选中

1. 模型类菜单项加一pid字段，外键自绑定
2. 当菜单为主菜单时pid为空，否则pid为是菜单项的主键
3. 在中间件中判断访问的权限是否为菜单下的子菜单，并把权限`id or pid` 保存在request中
4. 在inclusion_tag二级菜单中进行业务处理,取request中的pid做判断进行菜单的默认选中渲染

![image-20220610201009965](crm.assets/image-20220610201009965.png)

![image-20220610201230060](crm.assets/image-20220610201230060.png)

![image-20220610201840929](crm.assets/image-20220610201840929.png)

```python
# rbac.py 子模板函数
import re
from django.template import Library
from django.conf import settings
from collections import OrderedDict

register = Library()


@register.inclusion_tag('rbac/static_menu.html')
def static_menu(request):
    """
    创建一级菜单
    :return:
    """
    menu_list = request.session[settings.MENU_SESSION_KEY]
    return {'menu_list': menu_list}


@register.inclusion_tag('rbac/multi_menu.html')
def multi_menu(request):
    """
    创建二级菜单
    :return:
    """
    menu_dict = request.session[settings.MENU_SESSION_KEY]

    # 对字典的key进行排序
    key_list = sorted(menu_dict)

    # 空的有序字典
    ordered_dict = OrderedDict()

    for key in key_list:
        val = menu_dict[key]
        val['class'] = 'hide'

        for per in val['children']:

            if per['id'] == request.current_selected_permission:    # 判断当前的菜单id是否和当前访问的权限pid相等
                per['class'] = 'active'							 # 相等就让二级菜单选中
                val['class'] = ''
        ordered_dict[key] = val

    return {'menu_dict': ordered_dict}


@register.inclusion_tag('rbac/breadcrumb.html')
def breadcrumb(request):
    return {'record_list': request.breadcrumb}


@register.filter
def has_permission(request, name):
    """
    判断是否有权限
    :param request:
    :param name:
    :return:
    """
    if name in request.session[settings.PERMISSION_SESSION_KEY]:
        return True

```









## 6 路径导航

1 在中间件中传入导航条信息

```python
# 中间件
import re
from django.utils.deprecation import MiddlewareMixin
from django.shortcuts import HttpResponse
from django.conf import settings


class RbacMiddleware(MiddlewareMixin):
    """
    用户权限信息校验
    """

    def process_request(self, request):
        """
        当用户请求刚进入时候出发执行
        :param request:
        :return:
        """

        """
        1. 获取当前用户请求的URL
        2. 获取当前用户在session中保存的权限列表 ['/customer/list/','/customer/list/(?P<cid>\\d+)/']
        3. 权限信息匹配
        """
        current_url = request.path_info
        for valid_url in settings.VALID_URL_LIST:
            if re.match(valid_url, current_url):
                # 白名单中的URL无需权限验证即可访问
                return None

        permission_dict = request.session.get(settings.PERMISSION_SESSION_KEY)
        print(permission_dict)
        if not permission_dict:
            return HttpResponse('未获取到用户权限信息，请登录！')

        flag = False
		# 1 先创建一个首页
        url_record = [
            {'title': '首页', 'url': '#'}
        ]

        for item in permission_dict.values():
            reg = "^%s$" % item['url']
            if re.match(reg, current_url):
                flag = True
                request.current_selected_permission = item['pid'] or item['id']
                
                # 2 判断pid是否为空，空代表就是一级导航菜单
                if not item['pid']:
                    # 一级菜单就传回一个本身的title等,class: active是让访问的导航条应该为不可点击状态
                    url_record.extend([{'title': item['title'], 'url': item['url'], 'class': 'active'}])
                else:
                    # 二级菜单就先返回一级菜单参数在跟上当前访问的url
                    url_record.extend([
                        {'title': item['p_title'], 'url': item['p_url']},
                        {'title': item['title'], 'url': item['url'], 'class': 'active'},
                    ])
                 # 3 把数据传入到 request.breadcrumb 中
                request.breadcrumb = url_record
                break

        if not flag:
            return HttpResponse('无权访问')

```



2 使用inclusion_tag渲染

```python
# rbac.py

from django.template import Library

register = Library()

@register.inclusion_tag('rbac/breadcrumb.html')   # 1 创建装饰器
def breadcrumb(request):
    return {'record_list': request.breadcrumb}   # 2 把 request.breadcrumb 传到子模板breadcrumb.html
```

```html
<!-- 子模板breadcrumb.html -->
<div>
    <ol class="breadcrumb no-radius no-margin" style="border-bottom: 1px solid #ddd;">
        
        <!-- 3 循环传入的数据 -->
        
        
        {% for item in record_list %}
        	 
            {% if item.class %}
        		<!-- 4  判断有class属性，有属性的都是最后一个的子标签，传入active不可点击，也不用a标签了 -->
                <li class="active">{{ item.title }}</li>
        
            {% else %}
        
        		<!-- 4  判断无class属性，要加上标签可点击 -->
                <li><a href="{{ item.url }}">{{ item.title }}</a></li>
            {% endif %}
        {% endfor %}
    </ol>
</div>
```

然后就父模板调用

![image-20220610214150981](crm.assets/image-20220610214150981.png)







## 7 权限控制粒度到按钮

简单说就是无权限的按钮不给用户显示

1. 在模板中判断用户有无权限，有就渲染展示。无就不渲染
2. 在中间件中判断权限后数据已全部传到session中
3. 判断此次url是否在session的权限列表中
4. 在models中的权限表中增加一个url的别名字段，不能空，唯一
5. 在用户初始化时把别名当成字典的key传入到session中

![image-20220610215833516](crm.assets/image-20220610215833516.png)

6 filter的使用,返回True,False，只能传两个参数

```python
# rbac.py

from django.template import Library

register = Library()								# 1 实例对象

@register.filter									# 2 生成register.filter装饰器
def has_permission(request, name):
    """
    判断是否有权限
    :param request:
    :param name:
    :return:
    """
    # 3 判断传入的按钮别名in用户权限中字典中，字典的键是url别名
    if name in request.session[settings.PERMISSION_SESSION_KEY]:   
        return True

```

要做按钮控制的子HTML模板中

```html
{% extends 'layout.html' %}   <!-- 继承父模板  -->                                                
{% load rbac %}				<!-- 1 导入rbac.py -->  
{% block content %}

    <div class="luffy-container">
        
        <!-- 3 引用filter函数返回的布尔值做判断 ，True就显示下面的按钮-->  
         <!-- 调用方式: request| 第一个实参位置用|分割 接着中间就是函数名 第二个实参 :"payment_add" --> 
        <!-- payment_add:是下面标签url的别名 --> 
        {% if request|has_permission:"payment_add" %}
            <div style="margin: 5px 0;">
                <a class="btn btn-success" href="/payment/add/">
                    <i class="fa fa-plus-square" aria-hidden="true"></i> 添加缴费记录
                </a>
            </div>
        {% endif %}
        <table class="table table-bordered table-hover">
            <thead>
            <tr>
                <th>ID</th>
                <th>客户姓名</th>
                <th>金额</th>
                <th>付费时间</th>
				<!--  此外也一样做判断，手动对每个需要的按钮加上判断渲染 -->  
                {% if request|has_permission:"payment_del" or request|has_permission:"payment_edit" %}
                    <th>选项</th>
                {% endif %}
                
            </tr>
            </thead>
            <tbody>
            {% for row in data_list %}
                <tr>
                    <td>{{ row.id }}</td>
                    <td>{{ row.customer.name }}</td>
                    <td>{{ row.money }}</td>
                    <td>{{ row.create_time|date:"Y-m-d H:i:s" }}</td>
                    {% if request|has_permission:"payment_del" or request|has_permission:"payment_edit" %}
                        <td>
                            {% if request|has_permission:"payment_edit" %}
                                <a style="color: #333333;" href="/payment/edit/{{ row.id }}/">
                                    <i class="fa fa-edit" aria-hidden="true"></i></a>
                            {% endif %}
                            {% if request|has_permission:"payment_del" %}
                                <a style="color: #d9534f;" href="/payment/del/{{ row.id }}/"><i
                                        class="fa fa-trash-o"></i></a>
                            {% endif %}
                        </td>
                    {% endif %}

                </tr>
            {% endfor %}
            </tbody>
        </table>
    </div>
{% endblock %}
```



## 8 url参数打包到下一个url参数中

用作默认选中某菜单，点击了其他url时返回后继续默认选中原菜单

**思路**

1. 在模板中把request和name别名，传入到函数，如路游正则含有id，则还要传入pk
2. 函数中`request.GET`取到url携带的参数，打包成一个参数，与name别名反向出的url进行拼接返回
3. 打包参数时要用到django的QueryDict模块把参数转义，不然参数分分割

一 、把原参数携带到新的url中并访问

```python
# rbac.py
from django.urls import reverse
from django.http import QueryDict
from django.template import Library

register = Library()


@register.simple_tag
def memory_url(request, name, *args, **kwargs):
 	"""
	1 反向生成url
	name:url别名
	args,kwargs:正则url中携带的id
	"""  
    basic_url = reverse(name, args=args, kwargs=kwargs)     
	

    # 2 当前URL中无参数就直接返回url，不用在拼接
    if not request.GET:
        return basic_url
    
	# 3 创建一个QueryDict用来打包参数防转义
    query_dict = QueryDict(mutable=True)
    query_dict['_filter'] = request.GET.urlencode()  # mid=2&age=99
	
    # 4 把打包的参数编码后和url拼接返回给模板
    return "%s?%s" % (basic_url, query_dict.urlencode())


```

```html
 {% load rbac %}

<a style="color: #333333;" href="{% memory_url request 'rbac:menu_edit' pk=row.id %}">
     <!-- 5 模板中引入模块调用函数，传入了request，name别名，pk ,生成了携带了参数的url -->
```

二 、从新url中在重定向回原url

```python
# rbac.py
from django.urls import reverse
from django.template import Library

register = Library()


@register.simple_tag
def memory_reverse(request, name, *args, **kwargs):			# 1 反向解析name中的url
    url = reverse(name, args=args, kwargs=kwargs)
    origin_params = request.GET.get('_filter')				# 2 取出原url中打包的参数
    if origin_params:									  # 3 有打包参数就与url拼接
        url = "%s?%s" % (url, origin_params,)

    return url
```









## formset

![image-20220618225321721](crm.assets/image-20220618225321721.png)

使用方法

1 先创建一个forms类

```python
# rbac.forms.menu.py

from django import forms


class MultiAddPermissionForm(forms.Form):
    title = forms.CharField(
        widget=forms.TextInput(attrs={'class': "form-control"})
    )
    url = forms.CharField(
        widget=forms.TextInput(attrs={'class': "form-control"})
    )
    name = forms.CharField(
        widget=forms.TextInput(attrs={'class': "form-control"})
    )
    menu_id = forms.ChoiceField(
        choices=[(None, '-----')],
        widget=forms.Select(attrs={'class': "form-control"}),
        required=False,

    )

    pid_id = forms.ChoiceField(
        choices=[(None, '-----')],
        widget=forms.Select(attrs={'class': "form-control"}),
        required=False,
    )

    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.fields['menu_id'].choices += models.Menu.objects.values_list('id', 'title')
        self.fields['pid_id'].choices += models.Permission.objects.filter(pid__isnull=True).exclude(
            menu__isnull=True).values_list('id', 'title')
```

2 导入1创建的类和导入`formset_factory`

```python
from rbac.forms.menu import  MultiAddPermissionForm			# 1 导入创建的forms类
from django.forms import formset_factory	


def multi_permissions(request):
   
    # 2 使用formset_factory(),传入创建的forms类“MultiAddPermissionForm”。extra=0代表生成多少个表单，0就代表0个
    generate_formset_class = formset_factory(MultiAddPermissionForm, extra=0)
    
   
    if request.method == 'POST' and post_type == 'generate':
         # 3 实例化2的类传入用户输入的信息，就可进行判断或者传入模板	
    	formset = generate_formset_class(data=request.POST)
        if formset.is_valid():
            return return render( request,'rbac/multi_permissions.html',{'generate_formset':formset })
    
```

`rbac/multi_permissions.html`

```html
 	        <form method="post" action="?type=generate">
            {% csrf_token %}								<!-- 在form表单统一传入  csrf_token-->
            {{ generate_formset.management_form }}<!-- 4 还要导入一个传入的generate_formset.management_form-->
            <div class="panel panel-default">
                <!-- Default panel contents -->
                <div class="panel-heading">
                    <i class="fa fa-th-list" aria-hidden="true"></i> 待新建权限列表
                    <button href="#" class="right btn btn-primary btn-xs"
                            style="padding: 2px 8px;margin: -3px;">
                        <i class="fa fa-save" aria-hidden="true"></i>
                        新建
                    </button>


                </div>

                <!-- Table -->
                <table class="table">
                    <thead>
                    <tr>
                        <th>序号</th>
                        <th>名称</th>
                        <th>URL</th>
                        <th>别名</th>
                        <th>菜单</th>
                        <th>父权限</th>
                    </tr>
                    </thead>
                    <tbody>
                    {% for form in generate_formset %}			<!-- 5 循环生成input框和错误信息-->
                        <tr>
                            <td>{{ forloop.counter }}</td>
                            {% for field in  form %}
                                <td>{{ field }}<span style="color: red;">{{ field.errors.0 }}</span></td>
                            {% endfor %}
                        </tr>
                    {% endfor %}

                    </tbody>
                </table>
            </div>
        </form>

```

注：有个唯一错误unique，formset不能捕捉，要使用异常捕获把错误信息传入对应的`formset.errors`中





## 获取项目中所有的url

```python
import re
from collections import OrderedDict
from django.conf import settings
from django.utils.module_loading import import_string
from django.urls import URLResolver, URLPattern



def check_url_exclude(url):
    """
    排除一些特定的URL
    :param url:
    :return:
    """
    for regex in settings.AUTO_DISCOVER_EXCLUDE:    					# 8 循环放在配置文件中的路径
        if re.match(regex, url):									  # 用正则判断是否相同返回true
            return True


def recursion_urls(pre_namespace, pre_url, urlpatterns, url_ordered_dict):
    """
    递归的去获取URL
    None, '/', md.urlpatterns, url_ordered_dict
    :param pre_namespace: namespace前缀，以后用户拼接name
    :param pre_url: url前缀，以后用于拼接url
    :param urlpatterns: 路由关系列表
    :param url_ordered_dict: 用于保存递归中获取的所有路由
    :return:
    """
    for item in urlpatterns:												# 3 循环传入的所有url路游
        # 8 判断当前url对象是否URLPattern对象的子孙类   RLPattern是非路由分发，将路由添加到url_ordered_dict
        if isinstance(item, URLPattern):  
            if not item.name:								# 9 判断当前循环的url有没有name别名，没有就跳过此url
                continue

            if pre_namespace:  								# 10 此处获取name别名，判断有namespace就拼接name别名
                name = "%s:%s" % (pre_namespace, item.name)  			   # name = rbac:login
            else:
                name = item.name										# name = login
                
            url = pre_url + item.regex  						# 11 获取url拼接  /rbac/user/edit/(?P<pk>\d+)/
            url = url.replace('^', '').replace('$', '')			 # 获取的url在把正则用的符号给去掉

            if check_url_exclude(url):  						# 12 排除白名单的url,是白名单的url就跳过此url
                continue

            url_ordered_dict[name] = {'name': name, 'url': url}	 # 13 把拼接过的name别名当字典的键，name别名及url当值

            
         # 4 判断当前url对象是否URLResolver对象的子孙类   URLResolver是的路由分发的祖宗类，进行递归操作
        elif isinstance(item, URLResolver):  

            if pre_namespace:				# 5 判断有父的namespace同子namespace拼接
                if item.namespace:			# 5.1 判断此url有namespace，同上层的拼接
                    namespace = "%s:%s" % (pre_namespace, item.namespace,)  #   namespace= rbac:rbbc
                else:
                    namespace = item.namespace
            else:						   # 6 else 判断无父的namespace
                if item.namespace:			# 6.1 判断此url有namespace，直接返回 namespace
                    namespace = item.namespace
                else:

                    namespace = None		# 6.2 判断无urlnamespace，返回 None
                    
            # 7 递归去获取下层的url拼接
            recursion_urls(namespace, pre_url + item.regex.pattern, item.url_patterns, url_ordered_dict)





def get_all_url_dict():
    """
    获取项目中所有的URL（必须有name别名）
    :return:
    """
    url_ordered_dict = OrderedDict()													# 1 创建有序字典	

    md = import_string(settings.ROOT_URLCONF)  				# 2 以字符串导入方式导入模块 from luff.. import urls
    
    
    # 递归去获取所有的路由，传入上层namespace第一次无上层为None，路径，url路由列表，及存储用的有序字典
    recursion_urls(None, '/', md.urlpatterns, url_ordered_dict)  

    return url_ordered_dict
```

接下来就在业务函数中，调用get_all_url_dict获取到url别名







































知识点

![image-20220618224848732](crm.assets/image-20220618224848732.png)

![image-20220618224703955](crm.assets/image-20220618224703955.png)











































# 二 stark 组件开发

介绍：
　　stark组件，是一个帮助开发者快速实现数据库表的增删改查+的组件。
目标：
　　10s 中完成一张表的增删改查。







## 1 前戏

### 1 .1 django项目启动时，自定义执行某个py文件

1. 在配置中配置上app

![](crm.assets/image-20220620182552178.png)

2.在任意app的apps.py中的Config类中定义ready方法，并调用autodiscover_modules

```python
   from django.apps import AppConfig
    from django.utils.module_loading import autodiscover_modules


    class App01Config(AppConfig):
    name = 'app01'

    def ready(self):
        autodiscover_modules('xxxx')


# 3 django在启动时，就会去已注册的所有app的目录下找 xxxx.py 并自动导入。


如果执行两次，是因为django内部自动重启导致：
    python manage.py runserver 120.0.0.1:8001 --noreload

提示：
    如果xxxx.py执行的代码向 “某个神奇的地方” 放入了一些值。之后的路由加载时，可以去“某个神奇的地方”读取到原来设置的值。
```



### 1.2 单例模式

```python
单，一个。
例，实例、对象。

通过利用Python模块导入的特性：在Python中，如果已经导入过的文件再次被重新导入时候，python不会再重新解释一遍，而是选择从内存中直接将原来导入的值拿来用。
xxxx.py
    class AdminSite(object):
        pass
    site = AdminSite() # 为AdminSite类创建了一个对象（实例）
app.py
    import utils
    print(utils.site)

    import utils
    print(utils.site)


提示：
    如果以后存在一个单例模式的对象，可以先在此对象中放入一个值，然后再在其他的文件中导入该对象，通过对象再次讲值获取到。
```





### 1.3 django路由分发的本质：include

```python
方式一：
    from django.conf.urls import url,include

    urlpatterns = [
        url(r'^web/', include("app01.urls")),
    ]

方式二：
    include函数主要返回有三个元素的元组。
    from django.conf.urls import url,include
    from app01 import urls
    urlpatterns = [
        url(r'^web/', (urls, app_name, namespace)), # 第一个参数是urls文件对象，通过此对象可以获取urls.patterns获取分发的路由。
    ]


    在源码内部，读取路由时：
        如有第一个参数有：urls.patterns 属性，那么子路由就从该属性中后去。
        如果第一个参数无：urls.patterns 属性，那么子路由就是第一个参数。

方式三：
    urlpatterns = [
        url(r'^web/', ([
            url(r'^index/', views.index),
            url(r'^home/', views.home),
        ], app_name, namespace)), # 第一个参数是urls文件对象，通过此对象可以获取urls.patterns获取分发的路由。
    ]
```







## 2 知识点

### 2.1 通过模型类获取到表的app名及表名称

应用在生成url路径及url的name别名的生成

```python
# model :是某个表的模型类
app名 = model._meta.app_label
表名 = model._meta.model_name
```

### 2.2通过模型类获取到字段备注

```python
   # model_calss = 模型类对象，行数据
   # key = 字段
   
   verbose_name = model_calss._meta.get_field(key).verbose_name
```



### 2.3判断值是否函数，或者是否的对象的子对象

```python
from types import FunctionType

def key_or_func():
    pass

结果 = isinstance(key_or_func, FunctionType) # True
```



### 2.4 把性别0，1等的转成中文

数据库存入的男女经常用0，1储存表示

```python
# obj:一条数据的对象   field：字段名称
结果 = obj.get_field_display
```

项目用的闭包方法

```python
def get_choice_text(title, field):
    """
    对于Stark组件中定义列时，choice如果想要显示中文信息，调用此方法即可。
    :param title: 希望页面显示的表头
    :param field: 字段名称
    :return:
    """

    def inner(self, obj=None, is_header=None):
        if is_header:
            return title
        method = "get_%s_display" % field
        return getattr(obj, method)()

    return inner


# 调用
get_choice_text('性别', 'gender'),     # 传入模板表格的标题，和字段，get_choice_text内就会return回一个闭包函数
```





### 2.5 Q查询的

```python
	search_list = ['name__contains', 'email__contains']
     search_value = request.GET.get('q', '')  # 读取用户搜索内容
     conn = Q()  # 创建Q对象
     conn.connector = 'OR'
     if search_value:
         for item in search_list:
             conn.children.append((item, search_value))  # 把筛选配置与筛选内容以元组append Q对象内。在把这个对象放在 filter内

     
     queryset = self.model_class.objects.filter(conn).order_by(*order_list) # 查找

```





### 2.6 字符串查找字段对象

通过字符串找到字段的对象

```python
# model_class ：表模型类
# 'gender' ;模型类中的字段名
field_object = model_class._meta.get_field('gender')
```



### 2.7可迭代对象

类的对象的默认不可循环，在一个类中定义了__iter__方法且该方法返回一个迭代器，那么就称该类实例化的对象为可迭代对象（对象可以被循环）。

```python
class SearchGroupRow(object):
    def __init__(self, queryset_or_tuple):
        """

        :param queryset_or_tuple: 组合搜索关联获取到的数据
        """
        self.queryset_or_tuple = queryset_or_tuple

    def __iter__(self):
        # return iter([11, 22, 33])
        yield 1
        yield 2
        yield 3


row = SearchGroupRow([11, 22, 33])

for item in row:
    print(item)

```



















# 三 `crm` 业务

## 流程

### 一  创建项目

1 把rbac及stark组件app复制到crm项目中
2 在设置中把三个app加到apps中
3 进行迁移



### 二  校区管理

1 创建一个校区表，迁移，然后进行增删改查
2 在stark 中引入校区表使用stark功能生成url，默认生成 改删 并把编辑和删除的按键生成一列
知识点：子模板继承父模板，父模板所使用查找的是在设置中apps,按app的设置顺序去每个app的文件中查找;
注意: apps设置中把rbac放在stark后面，不然模板报错，因为，列表界面继承的父模板rbac中也有同名的,会优先使用到rbac中的模板



### 三 部门管理

1 创建表，迁移，同样 用stark生成增删改查



### 四 用户基本管理

1 创建用户表，继承rbac的UserInfo的用户表，迁移，同样 在业务stark文件中用stark生成增删改查，设置列表页面默认显示的列

2 对用户新增时默认展示的框的顺序不喜欢时进行设置 ，创建新的modelform类，继承starkmodelform类，在类中的fields字段中设置要展示的列字段，设置的顺序就是页面中显示的顺序就相同，然后在stark中的 用户表的handler  UserInfoHandler类下创建一个model_form_class字段=刚自定义的modelform类

![image-20220711221409437](crm.assets/image-20220711221409437.png)



3 在用户表新增界面增加确认密码，编辑界面不展示密码; 实现：需要在v1.py的默认handler类内get_model_class方法中添加一个默认参数is_add=False

![image-20220711221612388](crm.assets/image-20220711221612388.png)



然后在对应的添加方法中调用get_model_class方法时传入参数is_add=True,编辑的参数传入False。创建两个自定义的modelform类，一个类加一个确认密码字段，一个类中减去密码字段。![image-20220711222555435](crm.assets/image-20220711222555435.png)



在表的handler自定义类中创建get_model_class钩子方法，在方法中进行判断返回哪个类。

![image-20220711221926734](crm.assets/image-20220711221926734.png)

其他：新增界面的密码与确认密码中添加一个密码不一致的异常 ; modelform类中用钩子方法对密码进行一个md5加密;

```python
# luffy_crm-5\web\utils\md5.py
import hashlib	
# 1 创建一个md5加密方法
def gen_md5(origin): 					
    """
    md5加密
    :param origin:
    :return:
    """
    ha = hashlib.md5(b'jk3usodfjwkrsdf')
    ha.update(origin.encode('utf-8'))
    return ha.hexdigest()

```

```python
# luffy_crm/web/stark.py
from django.core.exceptions import ValidationError		# 1 导入错误
from stark.service.v1 import site, StarkHandler, get_choice_text, StarkModelForm 
# 2 导入创建的md5
from web.utils.md5 import gen_md5
class UserInfoAddModelForm(StarkModelForm):				# 2 创建编辑页面的ModelForm类，继承了默认的类
    confirm_password = forms.CharField(label='确认密码')

    class Meta:
        model = models.UserInfo
        fields = ['name', 'password', 'confirm_password', 'nickname', 'gender', 'phone', 'email', 'depart', 					'roles']

    def clean_confirm_password(self):		   	 # 3 创建钩子方法 
        password = self.cleaned_data['password']  # 3.1 读取密码与确认密码
        confirm_password = self.cleaned_data['confirm_password']
        if password != confirm_password:		# 3.2 对比两个密码不相等抛出错误
            raise ValidationError('密码输入不一致')
        return confirm_password					# 3.3 相等就返回原密码
    
    
	# 3 在ModelForm类中创建clean方法
    def clean(self):
        password = self.cleaned_data['password']
        self.cleaned_data['password'] = gen_md5(password)
        # 3.1 读取原密码返回加密后的密码
        return self.cleaned_data
```

### 五  用户重置密码

#### 1 新增一列重置密码到列表页面

![image-20220711233335970](crm.assets/image-20220711233335970.png)

#### 2 生成重置密码的url路由，视图函数，name别名，在反向name别名生成url给 重置密码a标签 的href

```python
# luffy_crm\stark\service\v1.py
class StarkHandler(object):               
    def reverse_commons_url(self, name, *args, **kwargs):   # 反向生成url的方法
        name = "%s:%s" % (self.site.namespace, name,)
        base_url = reverse(name, args=args, kwargs=kwargs)
        if not self.request.GET:
            add_url = base_url
        else:
            param = self.request.GET.urlencode()
            new_query_dict = QueryDict(mutable=True)
            new_query_dict['_filter'] = param
            add_url = "%s?%s" % (base_url, new_query_dict.urlencode())
        return add_url
```

`luffy_crm\web\stark.py`

![](crm.assets/image-20220711235104919.png)

#### 3  创建重置密码的模板及视图函数

![image-20220712003155974](crm.assets/image-20220712003155974.png)

`luffy_crm\web\stark.py`

```py
# 自定义的重置密码Form类，继承了StarkForm类
class ResetPasswordForm(StarkForm):
    password = forms.CharField(label='密码', widget=forms.PasswordInput)
    confirm_password = forms.CharField(label='确认密码', widget=forms.PasswordInput)

    def clean_confirm_password(self):
        password = self.cleaned_data['password']
        confirm_password = self.cleaned_data['confirm_password']
        if password != confirm_password:
            raise ValidationError('密码输入不一致')
        return confirm_password

    def clean(self):
        password = self.cleaned_data['password']
        self.cleaned_data['password'] = gen_md5(password)
        return self.cleaned_data

```

`luffy_crm\web\stark.py  \ class UserInfoHandler`

```python
def reset_password(self, request, pk):
    """
    重置密码的视图函数
    :param request:
    :param pk:
    :return:
    """
    userinfo_object = models.UserInfo.objects.filter(id=pk).first() # 1 判断点击的用户存在就不往下走
    if not userinfo_object:
        return HttpResponse('用户不存在，无法进行密码重置！')
    if request.method == 'GET':									# 2 get请示直接返回重置密码页面
        form = ResetPasswordForm()
        return render(request, 'stark/change.html', {'form': form})
    form = ResetPasswor dForm(data=request.POST)					# 3 接收传入的值
    if form.is_valid():											
        userinfo_object.password = form.cleaned_data['password'] # 3.1 判断无问题就更新密码
        userinfo_object.save()
        return redirect(self.reverse_list_url())				# 3.2 然后重定向回列表页面
    return render(request, 'stark/change.html', {'form': form})
```



### 六 用户管理丰富

在模型类handler中添加模糊搜索及组合搜索

```python
from stark.service.v1 import site, StarkHandler, get_choice_text, StarkModelForm, StarkForm, Option

class UserInfoHandler(StarkHandler):

    list_display = ['nickname', get_choice_text('性别', 'gender'), 'phone', 'email', 'depart', display_reset_pwd]
	# 1 模糊搜索 ，以账号及姓名进行搜索
    search_list = ['nickname__contains', 'name__contains']
	# 2 组合搜索，field=要组合搜索的字段
    search_group = [
        Option(field='gender'),
        Option(field='depart'),
    ]

    
        return patterns

```

### 七 课程管理

1 创建一个课程类，迁移

2 在stark.py中创建课程类的handler类，并使用site对象调用

3 当stark中的模型handler类多了后，把所有的handler类放到其它文件中，然后stark.py导入这些模型类，只做对象调用，达到简洁

![image-20220712214258008](crm.assets/image-20220712214258008.png)



### 八 班级管理

#### 1 创建班级类，并迁移

![image-20220712214636044](crm.assets/image-20220712214636044.png)

#### 2创建班级类handler

![image-20220712214908431](crm.assets/image-20220712214908431.png)

#### 3 引用班级类handler

![image-20220712215014853](crm.assets/image-20220712215014853.png)

#### 4 把班级和第几期两个字段在页面中显示成1列

![image-20220712215349857](crm.assets/image-20220712215349857.png)

![image-20220712215427122](crm.assets/image-20220712215427122.png)

#### 5 开班日期的格式显示改成年月日

![image-20220712215903893](crm.assets/image-20220712215903893.png)

​	在v1中创建函数

![image-20220712220040578](crm.assets/image-20220712220040578.png)

在模型handler类中调用函数

![image-20220712220140470](crm.assets/image-20220712220140470.png)

效果

![image-20220712220245161](crm.assets/image-20220712220245161.png)

#### 6 对多对多的任课老师显示

原

![](crm.assets/image-20220712220720723.png)

修改后

![image-20220712220657787](crm.assets/image-20220712220657787.png)

在v1中创建一个函数

![image-20220712220839693](crm.assets/image-20220712220839693.png)

进行调用

![image-20220712220935886](crm.assets/image-20220712220935886.png)

7 基于limit_choice_to 关联 FK或M2M进行筛选

在模型类字段中添加limit_choice_to条件就可

![image-20220712221926094](crm.assets/image-20220712221926094.png)

原

![image-20220712222020970](crm.assets/image-20220712222020970.png)

修改后

![image-20220712222040889](crm.assets/image-20220712222040889.png)



#### 7 用户输入的时间格式的设置

**模型handler中的设置**

`luffy_crm-10\web\views\class_list.py`

```python
from stark.service.v1 import StarkHandler, get_datetime_text, get_m2m_text, StarkModelForm
from stark.forms.widgets import DateTimePickerInput
from web import models

class ClassListModelForm(StarkModelForm):      # 1 自定义一个modelform类，继承StarkModelForm类
    class Meta:
        model = models.ClassList
        fields = '__all__'
        widgets = {
            'start_date': DateTimePickerInput,  # 2 对2个时间字段进行input的自定制
            'graduate_date': DateTimePickerInput,
        }


class ClassListHandler(StarkHandler):

    def display_course(self, obj=None, is_header=None):
        if is_header:
            return '班级'
        return "%s %s期" % (obj.course.name, obj.semester,)

    list_display = ['school', display_course, 'price', get_datetime_text('开班日期', 'start_date'), 'class_teacher',
                    get_m2m_text('任课老师', 'tech_teachers')]

    model_form_class = ClassListModelForm  	 # 3 在handler中使用自定义的modelform
```

`stark.forms.widgets`

```python
from django import forms


class DateTimePickerInput(forms.TextInput):
    template_name = 'stark/forms/widgets/datetime_picker.html'  # 4 上面调用此类返回出指定的html样式路径

```

`stark/forms/widgets/datetime_picker.html`

此时间输入格式来自bootstrap，需要设置`css，js`

```html
<div class="input-group date form_date">
    <input readonly class="form-control" type="{{ widget.type }}" name="{{ widget.name }}"{% if widget.value != None %}
           value="{{ widget.value|stringformat:'s' }}"{% endif %}{% include "django/forms/widgets/attrs.html" %} />
    <span class="input-group-addon"><span class="glyphicon glyphicon-calendar"></span></span>
</div>
```

把时间格式要引入的css,js等在stark的父模板中引用，以后哪个字段需要时间格式便可直接引用

在父模板顶部引入css

![image-20220712230412508](crm.assets/image-20220712230412508.png)

在父模板底部引入js

![image-20220712230454353](crm.assets/image-20220712230454353.png)



### 九 公户基本管理

#### 1把一张模型表创建两个handler类生成公户和私户

传入不同的前缀生成不一样的url路径

![image-20220713213116203](crm.assets/image-20220713213116203.png)

#### 2 把表中的课程顾问添加limit_choices_to，属于到销售部去

#### 3生成了公户私户后，把私户的添加页中才有课程顾问的选择，并且添加了有课程顾问的的用户只在私户显示，反之只在公户

把此类拿走放到钩子方法中在调用

![image-20220713213838875](crm.assets/image-20220713213838875.png)

​		把拿来的对象放到此方法中当默认![](crm.assets/image-20220713214043911.png)

这样同刚才其实没什么变化，但却多了钩子方法

![image-20220713214220952](crm.assets/image-20220713214220952.png)

然后在公户的模型类handler中自定义类设置 课程顾问为空；这样公户就会走自定筛选过的类

![image-20220713214903944](crm.assets/image-20220713214903944.png)



#### 5 然后公户的添加界面就要去掉课程顾问的选择

![image-20220713215431334](crm.assets/image-20220713215431334.png)



#### 6 公户中查看跟进记录

公户只能查看，私户才能添加

1 创建跟进记录类，迁移

![image-20220713215915270](crm.assets/image-20220713215915270.png)

2 在公户页面添加一列查看跟进记录

![image-20220713220139766](crm.assets/image-20220713220139766.png)

3 给跟进记录生成url路由，因为只有一个查看，所以不需要生成4个url，直接在公户中添加一个额外的跟进记录url便可

![image-20220713220852273](crm.assets/image-20220713220852273.png)

4 函数获取到用户的pk进行对应的模板渲染展示

![image-20220713221411388](crm.assets/image-20220713221411388.png)



#### 7 申请到私户

添加批量添加到私户，先在公户第一列添加多选框

![image-20220713222526649](crm.assets/image-20220713222526649.png)

添加一个申请到私户功能

![image-20220713223133761](crm.assets/image-20220713223133761.png)

以上未对申请的私户数量进行限制，现在进行优化添加限制

![image-20220713224222055](crm.assets/image-20220713224222055.png)

如果有人同时并发进行操作会出现问题，所以要加上锁

![image-20220713225331164](crm.assets/image-20220713225331164.png)





### 十 用户登陆

1 简单写一个登陆页面及路由，注销路由，主界面路由

2 把登陆的密码进行md5加密在与数据库密码对比。

3 登陆成功后用此用户id作添加私户到此用户



### 十一 私户基本管理

#### 1 把私户主页显示的人员只显示当前登陆人的人员

![image-20220716134749285](crm.assets/image-20220716134749285.png)

#### 2 把主页展示的列设置全面些

![image-20220716134939072](crm.assets/image-20220716134939072.png)

#### 3 把私户添加页的选择课程顾问去掉，默认用当前登陆用户

去掉课程顾问方法

![image-20220716135143720](crm.assets/image-20220716135143720.png)

默认用当前登陆用户，重写save方法，把课程顾问id修改成当前登陆者

![image-20220716135555313](crm.assets/image-20220716135555313.png)





#### 4 把私户的踢除到公户

1 批量操作页面新增移除到公户选项

2 读取用户批量选择的用户id与当前登陆用户的id进行查找，然后更新课程顾问为空

![image-20220716140054501](crm.assets/image-20220716140054501.png)

![image-20220716140356933](crm.assets/image-20220716140356933.png)





#### 5 私户跟进记录管理

1 在私户handler生成查看跟进记录的列显示，先把url去掉

![image-20220716140957418](crm.assets/image-20220716140957418.png)

2 创建一个跟进记录的handler，自定url路由，修改url要携带查看对应客户的id，避免操作到非当前用户的客户，查找表时从当前登陆的用户跨表到要查的跟进记录。非本用户的跟进便不可操作

![image-20220716142541962](crm.assets/image-20220716142541962.png)

3 在私户查看跟进记录中应用上url

![image-20220716143201316](crm.assets/image-20220716143201316.png)



#### 6 私户跟进记录界面展示

1 默认渲染的是表格模式不友好，可以给starkhandler在添加一个钩子变量，设置自定义使用哪个模板

![image-20220716164632552](crm.assets/image-20220716164632552.png)

在列表返回模板中使用一个默认为空的变量 or 默认使用模板路径

![image-20220716164421520](crm.assets/image-20220716164421520.png)



3 在跟进的handler中使用此变量设置自定的模板路径便可更换模板

![image-20220716164825862](crm.assets/image-20220716164825862.png)

4 然后写一个模板



#### 7 跟进记录添加页面的展示

把输入框选择用户和课程顾问的选项去掉，课程顾问默认用当前登陆的，用户在点进来时携带id了

1 把添加按钮调用的生成添加按钮加上参数

![image-20220716170443866](crm.assets/image-20220716170443866.png)

2 添加按钮原方法也加

![image-20220716170829599](crm.assets/image-20220716170829599.png)

3 去掉添加界面多余显示

自定义modelform

![image-20220716171017810](crm.assets/image-20220716171017810.png)



4 保存时等给内容加上用户id和当前登陆id

重写save

![image-20220716171222807](crm.assets/image-20220716171222807.png)



5 还有个报错点，反向生成url也加个参数

![image-20220716171355733](crm.assets/image-20220716171355733.png)

![image-20220716171435713](crm.assets/image-20220716171435713.png)









## 知识点

### `modelform`生成的input框的自定制

```python
# 1 自定义modelfrom类
from django import forms

class DateTimePickerInput(forms.TextInput):
    # 4.1 在类下添加template_name字段，并返回一个html模板，模板内容会传到生成的界面上
    template_name = 'stark/forms/widgets/datetime_picker.html'	

    
class ClassListModelForm(forms.ModelForm):
    class Meta:
        model = models.ClassList			# 2 选择模型类
        fields = '__all__'					# 3 选择显示全字段
        widgets = {							# 4 进行字段页面input框的设置{'字段名':定制类}
            'start_date': DateTimePickerInput,
            'graduate_date': DateTimePickerInput,
        }

```





### 模型类字字段的`limit_choices_to`筛选

```python
# 创建一个模型类
# 在字段内添加 limit_choices_to 限制内容字典形式
# {'表_字段':'符合筛选的内容'}
class Customer(models.Model): 
     consultant = models.ForeignKey(verbose_name="课程顾问", to='UserInfo', related_name='consultant',
                                   null=True, blank=True,
                                   limit_choices_to={'depart__title': '销售部'})
```



### `django`数据库加`transaction.atomic()`锁

```py
from django.db import transaction 	 # 1导包

 with transaction.atomic():  		# 2 创建事务
        						  # 3 查询的数据加上.select_for_update()，此条查询便上锁
 	queryset = models.Customer.objects.filter(id__in=pk_list, status=2,consultant__isnull=True).select_for_update()
    
     if len(origin_queryset) == len(pk_list):
          models.Customer.objects.filter(id__in=pk_list, status=2,		# 4 查询的结果进行了判断在保存
                                               consultant__isnull=True).update(consultant_id=current_user_id)
```

