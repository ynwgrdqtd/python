# 1 HTML

```html
HTTP协议：
    请求协议：
      请求首行   请求方式  URL路径？数据
      请求头
      空行
      请求体
      
    GET和POST
      响应首行
      响应头
      响应体
      
标签：
  按格式： 
      闭合标签：<h1>内容</h1>
      自闭合标签：<img src=''>
  
  <标签名 属性1=“属性值1” 属性2=“属性值2”……>内容部分</标签名>
  <标签名 属性1=“属性值1” 属性2=“属性值2”…… />
  
  <a><b>yuan</a></b>
  
  按功能分类：
       块级标签 （block）:
            独占一行
            比如  p , h1-h6 ，div，ul，li
       内联标签 （inline）:   
            按内容占位置  
            
            b，strong，i，em del，span
            a，img，input

            
        基本嵌套原则：
            块级可以嵌套块级和内联
            内联只可以嵌套内联
            

客户端（浏览器）向服务端发送请求形式：
    
    1、地址栏请求    get请求
    2、超链接标签    get请求
    3、form表单      get、post请求
    4、ajax    
    
    
    
Content_Type : multipart/form-data  发送文件
Content_Type : application/x-www-form-urlencoded      例如  "a=1&b=2&c=3"
Content_Type : json      例如  {"a":1,"b":2}
```

### 1 最简单的web应用程序

```python 
import socket

sock=socket.socket()
sock.bind(("127.0.0.1",8800))
sock.listen(5)

while 1:
    print("server is working...")
    conn,addr=sock.accept()
    recv_data=conn.recv(1024)
    conn.send(b"HTTP/1.1 200 OK\r\n\r\nwelcome to web world!")
    conn.close()

sock.close()
```

### 2 HTTP协议

#### 1.2.1 、简介

HTTP协议是Hyper Text Transfer Protocol（超文本传输协议）的缩写,是用于万维网（WWW:World Wide Web ）服务器与本地浏览器之间传输超文本的传送协议。HTTP是一个属于应用层的面向对象的协议，由于其简捷、快速的方式，适用于分布式超媒体信息系统。它于1990年提出，经过几年的使用与发展，得到不断地完善和扩展。HTTP协议工作于客户端-服务端架构为上。浏览器作为HTTP客户端通过URL向HTTP服务端即WEB服务器发送所有请求。Web服务器根据接收到的请求后，向客户端发送响应信息。

<img src="web.assets/1588750-20190118162356278-1999323050.png" />

#### 1.2.2、 http协议特性

(1) 基于TCP/IP协议

http协议是基于TCP/IP协议之上的应用层协议。

(2) 基于请求－响应模式

HTTP协议规定,请求从客户端发出,最后服务器端响应该请求并 返回。换句话说,肯定是先从客户端开始建立通信的,服务器端在没有 接收到请求之前不会发送响应

<img src="web.assets/1588750-20190118162456025-57507097.png"  />

(3) 无状态保存

HTTP是一种不保存状态,即无状态(stateless)协议。HTTP协议 自身不对请求和响应之间的通信状态进行保存。也就是说在HTTP这个 级别,协议对于发送过的请求或响应都不做持久化处理。

使用HTTP协议,每当有新的请求发送时,就会有对应的新响应产 生。协议本身并不保留之前一切的请求或响应报文的信息。这是为了更快地处理大量事务,确保协议的可伸缩性,而特意把HTTP协议设计成 如此简单的。

可是,随着Web的不断发展,因无状态而导致业务处理变得棘手 的情况增多了。比如,用户登录到一家购物网站,即使他跳转到该站的 其他页面后,也需要能继续保持登录状态。针对这个实例,网站为了能 够掌握是谁送出的请求,需要保存用户的状态。HTTP/1.1虽然是无状态协议,但为了实现期望的保持状态功能, 于是引入了Cookie技术。有了Cookie再用HTTP协议通信,就可以管 理状态了。有关Cookie的详细内容稍后讲解。

<img src="web.assets/1588750-20190118162508678-1256775662.png" />

(4) 无连接

无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。

#### 1.3.3、http请求协议与响应协议

http协议包含由浏览器发送数据到服务器需要遵循的请求协议与服务器发送数据到浏览器需要遵循的请求协议。用于HTTP协议交互的信被为HTTP报文。请求端(客户端)的HTTP报文 做请求报文,响应端(服务器端)的 做响应报文。HTTP报文本身是由多行数据构成的字文本。

(1) 请求协议

<img src="web.assets/1588750-20190118162757959-1733737382.png"  />

> 请求方式: get与post请求
>
> - GET提交的数据会放在URL之后，以?分割URL和传输数据，参数之间以&相连，如EditBook?name=test1&id=123456. POST方法是把提交的数据放在HTTP包的请求体中.
> - GET提交的数据大小有限制（因为浏览器对URL的长度有限制），而POST方法提交的数据没有限制

(2) 响应协议

#### <img src="web.assets/1588750-20190118162740806-776466524.png" />

响应状态码：状态码的职责是当客户端向服务器端发送请求时, 返回的请求结果。借助状态码,用户可以知道服务器端是正常理了请求,还是出现了 错误。

<img src="web.assets/1588750-20190118162555828-580941844.png"  />

### 2.HTML概述

了解了web相关基本概念以后，我们开始正式接触网页开发，网页开发的基础是HTML，所以，本章内容主要分两部分，一是介绍HTML的相关概念、发展历史，二是 创建HTML网页文档和认识HTML的基本结构。我们学会如何新建一个 HTML 页面和熟记HTML文档的基本结构和主要标签。

> * HTML，即超文本标记语言（HyperText Markup Language ]），由SGML (标准通用标记语言) 发展而来，也叫web页面。扩展名是 .html 或是 .htm 。
>
> * HTML，是一种用来制作网页的标准标记语言。超文本，指的就是超出普通文本范畴的文档，可以包含文本、图片、视频、音频、链接等元素。
>
> * HTML 不是一种编程语言，而是一种写给网页浏览器、具有描述性的标记语言。

自1990年以来HTML就一直被用作WWW（World Wide Web的缩写，也可简写WEB，中文叫做万维网）的信息表示语言，使用HTML语言描述的文件，需要通过网页浏览器显示出效果。用户在访问网页时，是把服务器的HTML文档**下载** 到本地客户设备中，然后通过本地客户设备的浏览器将文档按顺序解释渲染成对应的网页效果。

网页本身是一种文本文件，通过在文本文件中添加各种各样的标记标签，可以告诉[浏览器](http://baike.baidu.com/view/7718.htm)如何显示标记中的代表的内容，如：HTML中有的标签可以告诉浏览器要把字体放大，就像word一样，也有的标签可以告诉浏览器显示指定的图片，还有的标签可以告诉浏览器把内容居中或者倾斜等等。

每一个HTML标签代表的意义都不一样。同样，他们在浏览器中表现出来的外观也是不一样的。

### 3.HTML标准结构

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

</body>
</html>

```

> 1、`<!DOCTYPE html>` 告诉浏览器使用什么样的`html`或者`xhtml`来解析`html`文档
>
> 2、`<html></html>`是文档的开始标记和结束标记。此元素告诉浏览器其自身是一个 `HTML `文档，在它们之间是文档的头部`<head>`和主体`<body>`。	
>
> 3、`<head></head>`元素出现在文档的开头部分。`<head>与</head>`之间的内容不会在浏览器的文档窗口显示，但是其间的元素有特殊重要的意义。
>
> 4、`<title></title>`定义网页标题，在浏览器标题栏显示。
>
> 5、`<body></body>`之间的文本是可见的网页主体内容
>
> 6、`<meta charset="UTF-8"> `  声明编码方式用`utf8`

### 4.标签的语法

```html
<标签名 属性1=“属性值1” 属性2=“属性值2”……>内容部分</标签名>
<标签名 属性1=“属性值1” 属性2=“属性值2”…… />
```

> 1、HTML标签是由尖括号包围的特定关键词
>
> 2、标签分为闭合和自闭合两种标签
>
> 3、HTML不区分大小写
>
> 4、标签可以有若干个属性,也可以不带属性,比如<head>就不带任何属性
>
> 5、标签可以嵌套,但是不可以交叉嵌套
>
> 6、在很早以前HTML4的时候，HTML的标签是大写的，但在后面的发展中，人们发现HTML仍然存在很多不足，标签不区分大小写和标签可以胡乱嵌套都在其中，于是1998 年语法更为完的XML（ The Extensible Markup Lanxguage 可扩展标记语言 ）成为推荐标准，意在替代HTML。和HTML一样，XML同样来源于SGML，但当时已有成千上万的站点，因此直接使用XML作为网页开发技术根本就不可能。因此，后面W3C就在HTML4.0的基础上，参照XML的语法规则对HTML进行扩展，形成了XHTML （ The Extensible HyperText Markup Language ，可扩展超文本标记语言 ）的1.0版本。所以，XHTML是实现 HTML 到 XML的 过渡。



### 5.基本标签

| 标签名   | 标签                           | 描述                                   |
| -------- | ------------------------------ | -------------------------------------- |
| 标题标签 | <h1>标题</h1>    <h6>标题</h6> | 占一行，1代表文本最大，6最小，块级标签 |
| 段落标签 | <p>大家好，我是段落1。</p>     | 块级占一行                             |
| 换行标签 | <br/>                          | 换行                                   |
|          |                                |                                        |
|          |                                |                                        |

#### 文本格式化标签

HTML提供了一系列的用于格式化文本的标签，可以让我们输出不同外观的元素，比如粗体和斜体字。如果需要在网页中，需要让某些文本内容展示的效果丰富点，可以使用以下的标签来进行格式化。

```html
<b>定义粗体文本</b><br />
<strong>定义粗体文本方式2</strong><br />
<em>定义斜体字</em><br />
<i>定义斜体字方式2</i><br />
<del>定义删除文本</del><br />
```

* 特殊符号

```html
&reg; &nbsp; &copy;
```

* div和span标签

````html
<div>只是一个块级元素，并无实际的意义。主要通过CSS样式为其赋予不同的表现.
<span>表示了内联行(行内元素),并无实际的意义,主要通过CSS样式为其赋予不同的表现
````


块级元素与行内元素的区别所谓块元素，是以另起一行开始渲染的元素，行内元素则不需另起一行。如果单独在网页中插入这两个元素，不会对页面产生任何的影响。这两个元素是专门为定义CSS样式而生的。

### 6.超链接标签

#### 6.1、超链接基本使用

```html
<a href="http://www.baidu.com">百度</a>
<a href="02%20基本标签.html">本地资源</a>

<a href="http://www.baidu.com" target="_blanks" title="访问百度链接">百度</a>
<a href="#">click</a>
```

超链接是浏览者和服务器的交互的主要手段，也叫超级链接或a链接，是网页中指向一个目标的连接关系，这个目标可以是网页、网页中的具体位置、图片、邮件地址、文件、应用程序等。

超链接是网页中最重要的元素之一。一个网站的各个网页就是通过超链接关联起来的，用户通过点击超链接可以从一个网页跳转到另一个网页。

几乎可以在所有的网页中找到链接。点击链接可以从一张页面跳转到另一张页面。例如,在阅读某个网站时，遇到一个不认识的英文，你只要在这个单词上单击一下，即可跳转到它的翻译页面中，看完单词的解释后点一下返回按钮，又可继续阅读，这就是超链接的常见用途。还有经常到购物网站中去，我们都是在百度搜索，然后点击对应的搜索项进入到对应的购物网站的，这也是超链接的作用。超链接的属性：

| 属性   | 值                                                           | 描述                                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| href   | 网络链接 [ 例如: http://www.baidu.com ]     本地链接 [ 例如：F:\html\index.html ] | 规定链接的跳转目标                                           |
| title  | <a href="http://www.baidu.com" title="国内最著名的搜索引擎网站">百度</a> | 链接的提示信息                                               |
| target | _blank [ 在新建窗口中打开网页 ]                                                                                       _self  [ 默认值，覆盖自身窗口打开网页 ]                                                                                  _parent [ 在父级框架中打开网页 ]                                                                                                           _top  [ 在顶级框架中打开网页 ] framename [  在指定的框架中打开网页] | 与前面四项固定值不同，framename是泛指，并不是这个值，这点将在后面框架部分内容中详细介绍，这里可以暂时先略过 |

> 1、href是超链接最重要的属性，规定了用户点击链接以后的跳转目标，这个目标可以是 网络连接，也可以是本地连接。
>
> 2、网络链接指的是依靠网络来进行关联的地址，一般在地址前面是以 http://或者https://这样开头的，如果没有网络，则用户点击了超链接也无法访问对应的目标。
>
> 3、本地链接指的是本地计算机的地址，一般在地址前面是以 file:///开头或直接以 C:/、D:/、E:/开头的，不需要经过网络。
>
> 4、如果href的值留空，则默认是跳转到当前页面，也就是刷新当前页面。

#### 6.2、锚点

锚点( anchor )是超链接的一种应用，也叫命名锚记，锚点可以像一个定位器一样，可以实现页面内的链接跳转，运用相当普遍。例如，我们有一个网页，由于内容太多，导致页面很长，而且里面的内容，可以分为N个部分。这样的话，我们就可以在网页的顶部设置一些锚点，这样便可以方便浏览者点击相应的锚点，到达本页内相应的位置，而不必在一个很长的网页里自行寻找。又例如，我们页面中，有个链接需要跳转到另一个页面的中间或者脚部去，这时候也可以运用上锚点技术来解决这个问题。

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
    <title>锚点的使用</title>
  </head>
  <body>
  <a href="#i1">第一章</a>
  <a href="#i2">第二章</a>
  <a href="#i3">第三章</a>

   <div id="i1">
      <p>第一章内容</p>
  </div>
   <div id="i2">
      <p>第二章内容</p>
  </div>
  <div id="i3">
     <p> 第三章内容</p>
  </div>
  </body>
</html>
```

### 7.img标签

在HTML中，图像由<img>标签定义的，它可以用来加载图片到html网页中显示。网页开发过程中，有三种图片格式被广泛应用到web里，分别是 jpg、png、gif。

img标签的属性：

```go
/*
src属性：
    指定图像的URL地址，是英文source的简写，表示引入资源。
    src的值可以是本地计算机存储的图片的地址，也可以是网络上外部网站的图片的地址。
    如果src的值不正确，那么浏览器就无法正确的图片，而是显示一张裂图。
alt属性：指定图像无法显示时的替换文本。
width属性： 指定引入图片的显示宽度。
height属性：指定引入图片的显示高度。
border属性：指定引入图片的边框宽度，默认为0。
title属性：悬浮图片上的提示文字
*/
```

点击图片跳转可以配合a标签使用

```html
<a><img src="" alt=""></a>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<img src="https://img2.baidu.com/it/u=1613029778,1507777131&fm=26&fmt=auto&gp=0.jpg" title="美女" alt="美女图片">

<a href="http://www.baidu.com"><img src="u=1613029778,1507777131&fm=26&fmt=auto&gp=0.webp" alt=""></a>
</body>
</html>
```

### 8.列表标签

ul 无序

ol 有充

```html
  <ul type="square">
      <li>item1</li>
      <li>item2</li>
      <li>item3</li>
  </ul>

  <ol start="100">
      <li>item1</li>
      <li>item2</li>
      <li>item3</li>
  </ol>
```

### 9.表格标签

#### 9.1、table结构

在HTML中使用table来定义表格。网页的表格和办公软件里面的xls一样，都是有行有列的。HTML使用tr标签定义行，使用td标签定义列。

语法：

```html
<table border="1">
  <tr>
    <td>单元格的内容</td>
    ……
  </tr>
  ……
</table>

```

```html
<table border="1" align="center" cellpadding="10px" cellspacing="5px">
    <thead>
        <tr>
            <!--        table data-->
            <th>姓名</th>
            <th>年龄</th>
            <th>部门</th>
         </tr>
    </thead>

    <tbody>
         <tr>
            <td>张三</td>
            <td>23</td>
            <td rowspan="3">销售部门</td>
        </tr>

        <tr>
            <td>李四</td>
            <td>23</td>

        </tr>
        <tr>
            <td>王五</td>
            <td>23</td>
        </tr>

    </tbody>
</table>

```



> 1、`<table>`和`</table>`表示一个表格的开始和结束。一组`<table>...</table>`表示一个表格。
>
> 2、border用于设置整个表格的边框宽度，默认为0，表示不显示边框。
>
> 3、`<tr>`和`</tr>`表示表格中的一行的开始和结束。一组`<tr>...</tr>`，一个表格可以有多行。通过计算table标签中包含多少对tr子标签即可知道一个表格有多少行。
>
> 4、`<td>`和`</td>`表示表格中的一个单元格的开始和结束。通过计算一个tr里面包含了多少对td自标签即可知道一个表格有多少列，多少的单元格了。

#### 9.2、table属性

| 属性                                                         | 值                             | 描述                               |
| ------------------------------------------------------------ | ------------------------------ | ---------------------------------- |
| [width](http://www.w3school.com.cn/tags/att_table_width.asp) | px、%                          | 规定表格的宽度。                   |
| height                                                       | px、%                          | 规定表格的高度。                   |
| [align](http://www.w3school.com.cn/tags/att_table_align.asp) | left、center、right            | 规定表格相对周围元素的对齐方式。   |
| [bgcolor](http://www.w3school.com.cn/tags/att_table_bgcolor.asp) | rgb(x,x,x)、#xxxxxx、colorname | 规定表格的背景颜色。               |
| background                                                   | url                            | 规定表格的背景图片。               |
| [border](http://www.w3school.com.cn/tags/att_table_border.asp) | px                             | 规定表格边框的宽度。               |
| [cellpadding](http://www.w3school.com.cn/tags/att_table_cellpadding.asp) | px、%                          | 规定单元格边框与其内容之间的空白。 |
| [cellspacing](http://www.w3school.com.cn/tags/att_table_cellspacing.asp) | px、%                          | 规定单元格之间的空隙。             |

#### 9.3、td属性

表格中除了行元素以外，还有单元格，单元格的属性和行的属性类似。td和th都是单元格。

| 属性                                                         | 值                             | 描述                           |
| ------------------------------------------------------------ | ------------------------------ | ------------------------------ |
| height                                                       | px、%                          | 规定单元格的高度。             |
| width                                                        | px、%                          | 规定单元格的宽度。             |
| [align](http://www.w3school.com.cn/tags/att_table_align.asp) | left、center、right            | 规定单元格内容的对齐方式。     |
| valign                                                       | top、middle、bottom            | 规定单元格内容的垂直对齐方式。 |
| [bgcolor](http://www.w3school.com.cn/tags/att_table_bgcolor.asp) | rgb(x,x,x)、#xxxxxx、colorname | 规定单元格的背景颜色。         |
| background                                                   | url                            | 规定单元格的背景图片。         |
| rowspan                                                      | number                         | 规定单元格合并的行数           |
| colspan                                                      | number                         | 规定单元格合并的列数           |

### 10.表单标签

表单主要是用来收集客户端提供的相关信息，提供了用户数据录入的方式，有多选、单选、单行文本、下拉列表等输入框，便于网站管理员收集用户的数据，是Web浏览器和Web服务器之间实现信息交流和数据传递的桥梁.

表单被form标签包含，内部使用不同的表单元素来呈现不同的方式来供用户输入或选择。当用户输入好数据后，就可以把表单数据提交到服务器端。

一个表单元素有三个基本组成部分：

* 表单标签，包含了表单处理程序所在的URL以及数据提交到服务器的方法等表单信息。 

* 表单域，包含了文本框、密码框、隐藏域、多行文本框、复选框、单选框、下拉选择框和文件上传框等表单控件。

* 表单按钮，包括提交按钮、复位按钮和一般按钮，用于将数据传送到服务器上的CGI脚本或者取消输入，还可以用表单按钮来控制其他定义了处理脚本的处理工作。

在HTML中创建表单用form标签。每个表单都可以包含一到多个表单域或按钮。form标签属性：

| 属性    | 值                                                           | 描述                          |
| ------- | ------------------------------------------------------------ | ----------------------------- |
| action  | 访问服务器地址                                               | 服务器端表单处理程序的URL地址 |
| method  | post、get[默认值]                                            | 表单数据的提交方法            |
| target  | 参考超链接的target属性                                       | 表单数据提交时URL的打开方式   |
| enctype | application/x-www-form-urlencoded[默认值]    multipart/form-data [用于文件上传]                                                        text/plain [用于纯文本数据发送] | 表单提交数据时的编码方式      |

| 属性  | 值                             | 描述                       |
| ----- | ------------------------------ | -------------------------- |
| type  | password（密码），text（文本） | 输入时的格式               |
| name  | 自定                           | 设置的键，上传服务时传上去 |
| value | 自定                           | 设置的值，上传服务时传上去 |

```html
<form>表标签
<input>输入标签
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h3>注册用户</h3>

<form action="http://127.0.0.1:8888" method="post" enctype="application/x-www-form-urlencoded">

<p>
    <label for="user">姓名：</label>
    <input type="text" name="user" placeholder="用户名" id="user"></p>





<p>密码：<input type="password" name="pwd"></p>


<p>爱好：
    篮球<input checked="checked" type="checkbox" name="hobby" value="basketball">
    足球<input type="checkbox" name="hobby" value="football">
    双色球<input type="checkbox" name="hobby" value="shuangseqiu">
</p>
<p>
    性别：
    男<input type="radio" name="gender" value="1">
    女<input type="radio" name="gender" value="2">
    其它<input type="radio" name="gender" value="3">
</p>

<p>
    生日： <input type="date" name="birth">
</p>

<p>
    籍贯：
    <select name="province" multiple="multiple" size="3">
        <option value="hubei">湖北省</option>
        <option value="hebei">河北省</option>
        <option value="dongbei" selected="selected">东北省</option>
    </select>
</p>

<p>
    <textarea name="info" cols="50" rows="10" placeholder="个人简介"></textarea>
</p>

<p>
    <input type="button" value="按钮">
    <input type="reset" value="reset">
    <input type="submit">
    <button>提交数据</button>
</p>

</form>


</body>
</html>
```

![image-20210415213029670](web.assets/image-20210415213029670.png)























# 2 css

CSS就是Cascading Style Sheet的缩写，中文译作“层叠样式表”或者是“级联样式表”，是用于控制网页外观处理并允许将网页的表现与内容分离的一种标记性语言，CSS不需要编译,可以直接由浏览器执行(属于浏览器解释型语言)，是Web网页开发技术的重要组成部分。

那么接下来，继续看下，使用CSS有什么好处吧。

*  使用CSS样式可以有效地对页面进行布局，更加灵活多样。

*  使用CSS样式可以对页面字体、颜色、背景和其他效果实现精确控制，同时对它们的修改和控制变得更加快捷，更加强大。

*  站点中所有的网页风格都使用一个CSS文件进行统一控制，达到一改全改。还可以快速切换主题，我们可以把HTML比作是骨架，CSS是衣服。同一个HTML骨架结构，不同CSS样式，所得到的美化布局效果不同。

*  CSS可以支持多种设备,比如手机,PDA,打印机,电视机,游戏机等。

*  CSS可以将网页的表现与结构分离，使页面载入得更快,更利于维护，这也是我们的最终目的。

CSS基本语法:

<img src="web.assets/QQ截图20210222154121.png" style="zoom:50%;" />

> CSS的基本语法由选择器、属性、属性的值组成，如果选择符有多个属性，由分号隔开。
>
> 注意，这里的代码都是英文格式，例如花括号、冒号和分号。

### 1、CSS的引入方式

CSS样式有三种不同的使用方式，分别是行内样式，嵌入样式以及链接式。我们需要根据不同的场合不同的需求来使用不同的样式。

#### 行内样式

行内样式，就是写在元素的style属性中的样式，这种样式仅限于元素内部起作用。当个别元素需要应用特殊样式时就可以使用内联样式。但不推荐大量使用内联样式，因为那样不利于后期维护。

```html
<div style="color: white;background-color: #369;text-align: center">行内设置</div>
```

#### 嵌入式

嵌入式，是把CSS样式写在HTML文档内部head标签中的style标签里。浏览器加载HTML的同时就已经加载了CSS样式了。当单个文档需要特殊，单独的样式时，可以使用内部样式表。

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
     <title>title</title>
      <meta charset="utf8">

      <style>
          div{
              color: white;
              background-color: #369;
              text-align: center
          }
      </style>
  </head>
  <body>
  
  <div> 嵌入式</div>

  </body>
</html>
```

#### 链接式

链接式，就是把CSS样式写在HTML文档的外部，一个后缀为 .css 的外部样式表中，然后使用时在head标签中，使用link标签的href属性引入文件即可。当CSS样式需要应用在很多页面时，外部样式表是最理想的选择。在使用外部样式表的情况下，我们可以通过改变一个文件来改变这所有页面的外观。

common.css

````css
div{
      color: white;
      background-color: #369;
      text-align: center
}
````

html文件

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
     <title>title</title>
      <meta charset="utf8">

      <link rel="stylesheet" href="common.css">
  </head>
  <body>

  <div>链接式</div>
  
  </body>
</html>
```

### 2、CSS的选择器

#### 基本选择器

<img src="web.assets/QQ截图20210222164901.png" style="zoom:70%;" />

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
           #i1{
               color: red;
           }
           .c1{
               color: red;
           }
           .c2{
               font-size: 32px;
           }

    </style>


</head>
<body>

<div id="i1">item1</div>
<div id="i2">item2</div>
<div id="i3">item3</div>

<div class="c1 c2">item4</div>
<div class="c1">item5</div>
<div class="c1">item6</div>

</body>
</html>
```

#### 组合选择器

##### 后代子代选择器，后代空格隔开，子代>隔开

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>


    <style>
        /*后代选择器*/
        .c1 .c2{
            color: red;
        }

       
        .c3 .c5{
            color: red;
        }
        
          .c3 .c4 .c5{
            color: red;
        }
        
		 /*子代选择器*/
        .c3 > .c5{
            color: red;
        }

      
        
    </style>


</head>
<body>

<!--后代选择器-->
<div class="c1">
    <div class="c2">item1</div>
</div>
<div class="c2">item2</div>

<!--子代选择器-->
<div class="c3">
    <div class="c4">
        <div class="c5">item3</div>
    </div>
     <div class="c5">item4</div>
</div>

</body>
</html>
```

##### 与或选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        /*与选择器*/
        p.c1{
            color: red;
        }
         /*或选择器*/
        p.c1,#i1{
            color: red;
        }


    </style>


</head>
<body>

<!--与选择器-->
<div class="c1">item1</div>
<p class="c1">item2</p>
<div>item3</div>
<p id="i1">item4</p>


</body>
</html>
```

##### 兄弟选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        /*毗邻选择器*/
       #i1 + div.c1{
           color: red;
       }

       #i1 + div.c2{
           color: red;
       }

        /*兄弟选择器*/
        #i1 ~ div.c2{
           color: red;
        }
        #i1 ~ div{
           color: red;
        }


    </style>


</head>
<body>
    
<p id="i1">item0</p>
<div class="c1">item1</div>
<div class="c2">item2</div>
<div class="c3">item3</div>
<div class="c4">item4</div>


</body>
</html>
```

#### 属性选择器

```css
E[att]          匹配所有具有att属性的E元素，不考虑它的值。（注意：E在此处可以省略。
                比如“[cheacked]”。以下同。）   p[title] { color:#f00; }
                
E[att=val]      匹配所有att属性等于“val”的E元素   div[class=”error”] { color:#f00; }
 
E[att~=val]     匹配所有att属性具有多个空格分隔的值、其中一个值等于“val”的E元素
                td[class~=”name”] { color:#f00; }
 
E[attr^=val]    匹配属性值以指定值开头的每个元素                    
                div[class^="test"]{background:#ffff00;}
 
E[attr$=val]    匹配属性值以指定值结尾的每个元素    div[class$="test"]{background:#ffff00;}
 
E[attr*=val]    匹配属性值中包含指定值的每个元素    div[class*="test"]{background:#ffff00;}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        /*属性选择器*/
        [type="text"]{
            border: 1px solid red;
        }

        [index]{
            font-size: 32px;
            font-style: italic;
        }

        [href*="png"]{
            color: red;
        }

    </style>


</head>
<body>


<input type="text">
<input type="password">

<div index="1">1</div>
<div index="2">2</div>
<div index="3">3</div>

<ul>
    <li><a href="1.png">item1</a></li>
    <li><a href="2.jpg">item2</a></li>
    <li><a href="3.jpg">item3</a></li>
    <li><a href="4.png">item4</a></li>
    <li><a href="5.gif">item5</a></li>
</ul>

</body>
</html>
```

#### 伪类选择器

##### anchor伪类：专用于控制链接的显示效果

| [:link](https://www.w3school.com.cn/cssref/selector_link.asp) | a:link    | 选择所有未被访问的链接。     |
| ------------------------------------------------------------ | --------- | ---------------------------- |
| [:visited](https://www.w3school.com.cn/cssref/selector_visited.asp) | a:visited | 选择所有已被访问的链接。     |
| [:active](https://www.w3school.com.cn/cssref/selector_active.asp) | a:active  | 选择活动链接。               |
| [:hover](https://www.w3school.com.cn/cssref/selector_hover.asp) | a:hover   | 选择鼠标指针位于其上的链接。 |

```html
    <style>
           a:link{
               color: red;
           }
           a:visited{
               color: coral;
           }
           a:hover{
               color: blue;
           }
           a:active{
               color: rebeccapurple;
           }

    </style>

```

##### before after伪类 

before/after伪类相当于在元素内部插入两个额外的标签，其最适合也是最推荐的应用就是`图形生成`。在一些精致的UI实现上，可以简化HTML代码，提高可读性和可维护性。

| [:first-child](https://www.w3school.com.cn/cssref/selector_first-child.asp) | p:first-child | 选择属于父元素的第一个子元素的每个 <p> 元素。 |
| ------------------------------------------------------------ | ------------- | --------------------------------------------- |
| [:last-child](https://www.w3school.com.cn/cssref/selector_last-child.asp) | p:last-child  | 选择属于其父元素最后一个子元素每个 <p> 元素。 |
| [:before](https://www.w3school.com.cn/cssref/selector_before.asp) | p:before      | 在每个 <p> 元素的内容之前插入内容。           |
| [:after](https://www.w3school.com.cn/cssref/selector_after.asp) | p:after       | 在每个 <p> 元素的内容之后插入内容。           |

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>

        .c1 p:first-child{
            color: red;
        }

        .c1 div:last-child{
            color: red;
        }

        p#i1:after{
            content:"hello";
            color:red;
            display: block;
        }

    </style>


</head>
<body>

<div class="c1">
    <p>item1</p>
    <p>item1</p>
    <div>item1</div>
    <p>item1</p>
</div>

<p id="i1">p标签</p>

</body>
</html>
```

#### 样式继承

CSS的样式表继承指的是，特定的CSS属性向下传递到子孙元素。总的来说，一个HTML文档就是一个家族，然后html元素有两个子元素，相当于它的儿子，分别是head和body，然后body和head各自还会有自己的儿子，最终形成了一张以下的家族谱。

<img src="web.assets/QQ截图20210224153345.png" style="zoom:67%;" />



在上图中，可以看到，body的子元素有三个，h1、p和ul，ul也有几个子元素，p也有1个子元素，那么li和a就都是body的后代元素。有时可能我们在body里面设置了一些属性，结果，body下面所有的后代元素都可能享受到，这就是样式继承。就像一句俗语一样，“龙生龙，凤生凤，老鼠的儿子会打洞”。样式继承，可以给我们的网页布局带来很多的便利，让我们的代码变得更加简洁，但是，如果不了解，或者使用不当，也有可能会给我们带来很多不必要的麻烦。

因此，如果了解了哪些样式是会继承到后代元素的，那么就可以避免这些问题的发生了。

| 文本相关属性       |                     |                 |              |
| ------------------ | ------------------- | --------------- | ------------ |
| font-family        | font-size           | letter-spacing  | line-height  |
| font-style         | font-variant        | text-align      | text-indent  |
| font-weight        | font                | text-transform  | word-spacing |
| color              | direction           |                 |              |
| 列表相关属性       |                     |                 |              |
| list-style-image   | list-style-position | list-style-type | list-style   |
| 表格和其他相关属性 |                     |                 |              |
| border-collapse    | border-spacing      | caption-side    | empty-cells  |
| cursor             |                     |                 |              |

#### 选择器优先级

##### 继承

继承是CSS的一个主要特征，它是依赖于祖先-后代的关系的。继承是一种机制，它允许样式不仅可以应用于某个特定的元素，还可以应用于它的后代。例如一个BODY定义了的颜色值也会应用到段落的文本中。

```
body{color:red;}    <p>helloyuan</p>
```

这段文字都继承了由body {color:red;}样式定义的颜色。然而CSS继承性的权重是非常低的，是比普通元素的权重还要低的0。

```
p{color:green}
```

发现只需要给加个颜色值就能覆盖掉它继承的样式颜色。由此可见：任何显示申明的规则都可以覆盖其继承样式。 此外，继承是CSS重要的一部分，我们甚至不用去考虑它为什么能够这样，但CSS继承也是有限制的。有一些属性不能被继承，如：border, margin, padding, background等。

##### 优先级

所谓CSS优先级，即是指CSS样式在浏览器中被解析的先后顺序。样式表中的特殊性描述了不同规则的相对权重。

```css
/*
!important > 行内样式>ID选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性

1 内联样式表的权值最高               style=""           1000；

2 统计选择符中的ID属性个数。         #id                100

3 统计选择符中的CLASS属性个数。      .class             10

4 统计选择符中的HTML标签名个数。     标签名              1

按这些规则将数字符串逐位相加，就得到最终的权重，然后在比较取舍时按照从左到右的顺序逐位比较。
*/
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
            .c1{
                color: red;
            }
            #i1{
                color: coral;
            }
            div{
                color: greenyellow;
            }

            /*.c2 .c3 .c4 span{*/
            /*    color: orange;*/
            /*}*/

            .c2 .c4 span{
                color: blue;
            }

            .c2 .c3 .c5{
                color: rebeccapurple;
            }

            .c2 .c4 .c5{
                color: darkcyan;
            }

    </style>

</head>
<body>


<div class="c1" id="i1">item1</div>


<div class="c2">
    <div class="c3">
        <div class="c4">
            <span class="c5">item2</span>
        </div>
    </div>
</div>


</body>
</html>
```

> 1、有!important声明的规则高于一切。
>
> 2、如果!important声明冲突，则比较优先权。
>
> 3、如果优先权一样，则按照在源码中出现的顺序决定，后来者居上。
>
> 4、由继承而得到的样式没有specificity的计算，它低于一切其它规则(比如全局选择符*定义的规则)。
>
> 5、用数字表示只是说明思想，一万个class也不如一个id权值高

### 3、CSS的属性操作

#### 1 文本属性

##### font-style（字体样式风格）

```html
属性值：
normal：设置字体样式为正体。默认值。 
italic：设置字体样式为斜体。这是选择字体库中的斜体字。
oblique：设置字体样式为斜体。人为的使文字倾斜，而不是去使用字体库的斜体字。

```

##### font-weight（字体粗细）

```go
/*
属性值：
normal：设置字体为正常字体。相当于数字值400
bold：设置字体为粗体。相当于数字值700。
bolder：设置字体为比父级元素字体更粗的字体。
lighter：设置字体为比父级元素字体更细的字体。
number：用数字表示字体粗细。从小到大，越来约粗，取值范围：100、200、300、400、500、600、700、800、900。
注意：
font-weight的常用值有两个normal和bold，其他的值在浏览器中的支持并不好。
*/
```

##### font-size（字体大小）

```go
/*
font-size的值有很多，有xx-small、x-small、small、medium、large、x-large、xx-large、smaller和larger，也可以设置值为具体的数值加上对应的计算单位来表示字体的大小。字体单位有像素（ px ）、字符（ em，默认1em等于16px，2em等于32px，根据不同浏览器的默认字体大小而决定 ）、百分比（ % ），磅[点]（ pt ）。
字体不指定大小时，主流浏览器默认是15像素到16像素。旧版本的谷歌浏览器，字体最小只能设置成12像素，新版已经修复。*/
```

##### font-family（字体族）

```go
/*
font-family可以指定元素使用的字体系列或字体族。当我们使用font-family指定字体族的时候，可以指定多种字体,作为候补。指定多个字体的时候，需要使用逗号隔开。
如果css中没有声明当前内容使用的字体族的时候，默认：
	中文：  宋体 [ win7以后默认是 微软雅黑 ]
	英文：  Arial
*/
```

##### color（字体颜色）

```go
// 可以使用color来表示字体的颜色，颜色值最常用的有三种形式，英文单词，十六进制，RGB十进制。更高级的有 RGBA、HSL、HSLA，不过低版本的浏览器并不支持。
```

````
 <style>
        .c1{
            color: red;
        }
        .c1{
            color: #369;
        }
        .c1{
            color: RGB(0,0,255);
        }
</style>

````

> 另外要注意，使用十六进制表示颜色值的时候，如果字符的格式类似于“AAAAAA”的这种，六个字符一样的；又或者是“AABBCC”，这种，一二，三四，五六 位置上的数字一样的，我们可以使用简写来表达。

##### text-align（文本对齐方式）

```go
text-align属性可以设置文本内容的水平对齐方式。属性值常用的有
左对齐left、居中对齐center、右对齐right。justify 实现两端对齐文本效果。

```

##### line-height（字体行高）

```go
// 字体行高即字体最底端与字体内部顶端之间的距离。值可以是normal、px、number、%。
```

<img src="web.assets/QQ截图20210224150648.png" style="zoom:67%;" />

> 行高 = 字体大小 + 上半行距 + 下半行距

##### vertical-align

vertical-align 属性设置元素的垂直对齐方式。

```html
<img src="" alt=""><span>yuan</span>
```

##### text-decoration

```go
// 使用text-decoration可以设置文本内容的装饰线条，正常的文本是没有线条的，常用的值有none，underline，overline，line-through四种。
```

#### 2 背景属性

##### background-color（背景颜色）

页面的背景颜色有四种属性值表示，分别是transparent（透明），RGB十进制颜色表示，十六进制颜色表示和颜色单词表示。

属性使用：

```go
/*
background-color: transparent;   // 透明 
background-color: rgb(255,0,0); //  红色背景 
background-color: #ff0000;  //  红色背景
background-color: red;    // 红色背景 
*/
```

##### background-image（背景图片）

background-image可以引入一张图片作为元素的背景图像。默认情况下，background-image放置在元素的左上角，并在垂直和水平方向重复平铺。

语法：

```go
// background-image: url('图片地址')
```

> 当同时定义了背景颜色和背景图像时，背景图像覆盖在背景颜色之上。 所以当背景图片没有被加载到，或者不能完全铺满元素时，就会显示背景颜色。

##### background-repeat（背景平铺方式）

CSS中，当使用图像作为背景了以后，都是默认把整个页面平铺满的，但是有时候在很多场合下面，页面并不需要这种默认的效果，而可能需要背景图像只显示一次，或者只按照指定方式进行平铺的时候，可以使用background-repeat来进行设置。

background-repeat专门用于设置背景图像的平铺方式，一般有四个值，默认是repeat（平铺），no-repeat（不平铺），repeat-x（X轴平铺），repeat-y（Y轴平铺）。

##### background-position（背景定位）

CSS中支持元素对背景图像的定位摆放功能，就是利用background-position属性来实现，以页面中元素的左上角为原点（0，0），把元素的内部区域当成一个坐标轴（上边框为X轴，越往左X的值越大，左边框为Y轴，越往下Y轴的值就越大，反之亦然），然后计算出背景图片的左上角与圆点的距离（x轴和y轴的距离），然后把背景图片放入到指定的位置上，对背景图片的位置进行精确的控制和摆放。

​	background-position的值分成两个，使用空格隔开，前面一个是背景图片左上角的x轴坐标，后面一个是背景图片左上角的y轴坐标。两个值都可以是正、负值。

语法：

```go
// background-position: x轴坐标 y轴坐标
```

> 背景定位的值除了是具体的数值以外，还可以是左（left）、中（center）、右（right）

##### background（背景样式缩写）

和字体属性一样，多个不同背景样式属性也是可以同时缩写的，不过不需要像字体那样按照一定的顺序，背景样式的缩写属性的顺序是不固定的，可以任意编排。

语法：

```go
// background: 背景颜色  背景图片  背景平铺方式  背景定位;
```

#### 3 边框属性

##### border-style（边框风格）

定义边框的风格，值可以有

```go
/*
none：没有边框，当border的值为none的时候，系统将会忽略[border-color]
hidden：隐藏边框，低版本浏览器不支持。
dotted：点状边框。
dashed：虚线边框。
solid：实线边框。
double：双实线边框，两条单线与其间隔的和等于border-width值。
*/
```

border-style的值可以缩写的：

```go
/*
只有一个值的时候表示同时控制上下左右的边框风格。
只有两个值的时候表示分别控制上下、左右的边框风格。
有三个值的时候表示分别控制上、左右、下的边框风格。
有四个只的时候表示分别控制上、右、下、左的边框风格。
*/
```

border-style还可以单独指定不同方向：

```go
/*
border-top-style		设置上边的边框风格
border-bottom-style	     设置下边的边框风格
border-left-style		设置左边的边框风格
border-right-style		设置右边的边框风格
*/
```

##### border-width（边框宽度）

使用border-width可以定义边框的厚度，值可以是medium，thin，thick和指定数值的宽度。 同时，border-width也可以进行缩写：

```go
/*
只有一个值的时候表示同时控制上下左右的边框宽度。
只有两个值的时候表示分别控制上下、左右的边框宽度。
有三个值的时候表示分别控制上、左右、下的边框宽度。
有四个只的时候表示分别控制上、右、下、左的边框宽度。
*/
```

border-width也可以单独指定不同方向：

```go
/*
border-top-width		设置上边的边框宽度
border-bottom-width	    设置下边的边框宽度
border-left-width		设置左边的边框宽度
border-right-width		设置右边的边框宽度
*/
```

##### border-color（边框颜色）

定义边框的颜色，值表示的方式可以是十六进制，RGB十进制和单词表示法。

 同上，border-color的缩写：

```go
/*
只有一个值的时候表示同时控制上下左右的边框颜色。
只有两个值的时候表示分别控制上下、左右的边框颜色。
有三个值的时候表示分别控制上、左右、下的边框颜色。
有四个只的时候表示分别控制上、右、下、左的边框颜色。
*/
```

border-color也可以单独指定不同方向：

```css
/*
border-top-color		设置上边的边框颜色
border-bottom-color	设置下边的边框颜色
border-left-color		设置左边的边框颜色
border-right-color		设置右边的边框颜色
*/
```

##### 边框样式缩写

还可以把边框风格，边框宽度，边框颜色进行组合在一起，进行缩写：语法：

```go
// border: 边框宽度 边框样式 边框颜色;
```

> 注意，border的缩写值可以不按照顺序来进行书写。这样的缩写可以同时控制4个方向的边框样式。	

#### 4 列表属性

CSS中提供了一些列表属性可以用来：

​	(1)、设置不同的列表项标记为有序列表

​	(2)、设置不同的列表项标记为无序列表

​	(3)、设置列表项标记为图像

* list-style-type（系统提供的列表项目符号）

* list-style-image（自定义的列表项目符号）

```css
 li { list-style-image:url('qq.gif'); }
```

#### 5 dispaly属性

display可以指定元素的显示模式，它可以把行内元素修改成块状元素，也可以把别的模式的元素改成行内元素。diisplay常用的值有四个。

语法：

```css
/*
display: block;		 	// 声明当前元素的显示模式为块状元素
display: inline;		// 声明当前元素的显示模式为行内元素
display: inline-block; 	 // 声明当前元素的显示模式为行内块状元素
display: none;			// 声明当前元素的显示模式为隐藏 把列表的标签隐藏
*/
```

#### 6 盒子模型（重点）

盒模型是CSS的核心知识点之一，它指定元素如何显示以及如何相互交互。HTML页面上的每个元素都可以看成一个个方盒子，这些盒子由元素的content（内容）、padding（内边距）、border（边框）、margin（外边距）组成。

![](web.assets/QQ截图20210227143245.png)

##### padding（内边距及其缩写）

内边距，也叫“内补白”，表示页面中元素的边框与内容的距离。内边距的值不能是负值，相当于table标签的cellpadding属性。

内边距可以设置多个值：

```go
/*
当padding只有一个值的时候表示同时控制上下左右的内边距。
当padding只有两个值的时候表示分别控制上下、左右的内边距。
当padding有三个值的时候表示分别控制上、左右、下的内边距。
当padding有四个只的时候表示分别控制上、右、下、左的内边距。
*/
```

内边距也可以进行单独设置：

```css
/*
padding-top 			设置上边的外边距
padding -bottom 		设置下边的外边距
padding -left			设置左边的外边距
padding -right			设置右边的外边距
*/
```

##### margin（外边距及其缩写）

外边距，也叫“外补白”，表示页面中元素与元素之间的距离。外边距越大，两者的距离就越远，反之，如果外边距越小，则元素之间的距离就越近，外边距的值可以是正数，也可以是负值。

margin也可以像padding一样设置多个值和单独方向设置，用法一样。

> 1、在网页的开发过程中，需要让一个元素相对于父级元素作水平居中时，可以借助margin的特性来实现。
>
> ​      使用margin让元素自身居中：  margin: 0 auto;
>
> 2、浏览器的默认边距清零

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
       .c1{
           width: 100%;
           height: 600px;
           border: 1px solid red;

       }

       .c2{
           width: 50%;
           height: 40px;
           background-color: rebeccapurple;
           margin: 10px auto;
       }
    </style>
</head>
<body>

<div class="c1">
    <div class="c2"></div>
    <div class="c2"></div>
</div>
</body>
</html>
```

边距案例：

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
        <meta charset="utf8">
        <style>

            *{
                margin: 0;
                padding: 0;
            }

            .c1{
                width: 80%;

                margin: 100px auto;

            }

            .c1 .J_categoryList{
                list-style: none;

            }
            .c1 .J_categoryList li{
                display: inline-block;
                margin: 10px;

            }
            .c1 .J_categoryList li a{
                font-size: 16px;
                color: #333;
                padding: 20px;
                border: 1px solid rebeccapurple;
                text-decoration: none;
            }

        </style>
  </head>
  <body>
<div class="c1">
      <ul class="J_categoryList">
          <li><a href=""><span>红米</span></a></li>
          <li><a href=""><span>电视</span></a></li>
          <li><a href=""><span>笔记本</span></a></li>
          <li><a href=""><span>家电</span></a></li>
          <li><a href=""><span>小米手机</span></a></li>
      </ul>
</div>
  </body>
</html>
```

#### 7 float属性（重点）

##### 流动布局

流动模型（Flow），即文档流，浏览器打开HTML网页时，从上往下，从左往右，逐一加载。

在正常情况下，HTML元素都会根据文档流来分布网页内容的。

文档流有2大特征：

① 块状元素会随着浏览器读取文档的顺序，自上而下垂直分布，一行一个的形式占据页面位置。

② 行内元素会随着浏览器区队文档的顺序，从左往右水平分布，一行多个的形式占据页面位置。行内元素摆放满一行以后才会到下一行继续排列。

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
    <title></title>
    <style>
    div{ border: 1px solid #f00; margin: 4px; }
    .d3{ width: 100px; }
    </style>
  </head>
  <body>
    <div>d1</div>
    <div>d2</div>
    <div class="d3">
      <span>span1</span>
      <a>a1</a>
      <a>a2</a>
      <span>span2</span>
    </div>
  </body>
</html>
```

##### 浮动模型

要学习浮动模型的布局模式，就要了解CSS提供的浮动属性（float）。浮动属性是网页布局中最常用的属性之一，通过浮动属性不但可以很好的实现页面布局，而且还可以依靠它来制作导航栏等页面功能。

简单浮动：

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
    <title>简单浮动</title>
    <style>

        .c1{
            width: 200px;
            height: 200px;
            background-color: indianred;
            float: left;
        }

        .c2{
            width: 300px;
            height: 200px;
            background-color: orange;
            float: left;

        }

        .c3{
            width: 400px;
            height: 200px;
            background-color: lightblue;
            float: left;
        }
        

    </style>
  </head>
  <body>

   <div class="c1"></div>
   <div class="c2"></div>
   <div class="c3"></div>

  </body>
</html>
```

##### 字围效果

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
    <title>字围效果</title>
    <style>

        .c1{
            width: 200px;
            height: 200px;
            background-color: indianred;

        }

        .c2{
            width: 300px;
            height: 200px;
            background-color: orange;
            float: left;

        }

        .c3{
            width: 400px;
            height: 400px;
            background-color: lightblue;

        }
        
    </style>
  </head>
  <body>

   <div class="c1">111</div>
   <div class="c2">222</div>
   <div class="c3">333</div>>

  </body>
</html>
```

案例：

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
    <title>字围案例</title>
    <meta charset="utf8">
    <style>

        .c1{
            width: 500px;
        }

        img{
            float: left;
            width: 300px;
            height: 200px;
        }

      
    </style>
  </head>
  <body>
    <div class="c1">
           <img src="" alt="">
           <span class="text">
           </span>
    </div>

  </body>
</html>
```

> 当一个元素被设置浮动后，将具有以下特性：
>
> 1. 任何申明为float 的元素都会自动被设置为一个行内块状元素，具有行内块状元素的特性。 
> 2. 假如某个元素A是浮动的，如果A元素上一个元素也是浮动的，那么A元素会跟随在上一个元素的后边(如果一行放不下这两个元素，那么A元素会被挤到下一行)；如果A元素上一个元素是标准流中的元素，那么A的相对垂直位置不会改变，也就是说A的顶部总是和上一个元素的底部对齐。
> 3. 在标准浏览器中如果浮动元素a脱离了文档流，那么排在浮动元素a后的元素将会往回排列占据浮动元素a本来所处的位置，使页面布局产生变化。
> 4. 如果水平方向上没有足够的空间容纳浮动元素，则转向下一行。
> 5. 字围效果：文字内容会围绕在浮动元素周围。
> 6. 浮动元素只能浮动至左侧或者右侧。
> 7. 浮动元素只能影响排在其后面元素的布局，却无法影响出现在浮动元素之前的元素。

##### 清除浮动

网页布局中，最常用的布局便是浮动模型。但是浮动了以后就会破坏原有的文档流，使页面产生不必要的改动，所以我们一般在浮动了以后，达到目的了，就紧接着清除浮动。

在主流浏览器（如Firefox）下，如果没有设置height，元素的高度默认为auto，且其内容中有浮动元素时，在这种情况下元素的高度不能自动伸长以适应内容的高度，使得内容溢出到容器外面而影响（甚至破坏）布局的情况，叫“浮动溢出”，为了防止这个现象的出现而进行的CSS处理操作，CSS里面叫“清除浮动”。

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
    <title></title>
    <meta charset="utf8">
    <style>

        .box{
            border: 1px solid red;
        }

        .c1{
            width: 200px;
            height: 200px;
            background-color: #336699;
            float: left;
        }

         .c2{
            width: 200px;
            height: 200px;
            background-color: orange;
            float: right;
        }

         .footer{
             width: 100%;
             height: 60px;
             background-color: yellowgreen;

         }
    </style>
  </head>
  <body>
    <div class="box">
        <div class="c1"></div>
        <div class="c2"></div>
    </div>
   <div class="footer"></div>

  </body>
</html>
```

![](web.assets/QQ截图20210226151828.png)

clear是css中专用于清除浮动的，常用的属性值有以下几个：

| 值    | 描述                             |
| ----- | -------------------------------- |
| left  | 在左侧不允许浮动元素。           |
| right | 在右侧不允许浮动元素。           |
| both  | 在左右两侧均不允许浮动元素。     |
| none  | 默认值。允许浮动元素出现在两侧。 |

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
    <title>简单浮动</title>
    <style>

        .c1{
            width: 200px;
            height: 200px;
            background-color: indianred;
            float: left;
            /*float: right;*/
        }

        .c2{
            width: 300px;
            height: 200px;
            background-color: orange;
            float: left;
            clear: left;
            /*clear: both;*/
        }

        .c3{
            width: 400px;
            height: 200px;
            background-color: lightblue;
            float: left;

        }

    </style>
  </head>
  <body>

   <div class="c1"></div>
   <div class="c2"></div>
   <div class="c3"></div>

  </body>
</html>
```

清除浮动解决父级塌陷问题：

````css
  .clearfix:after {                         /*在类名为“clearfix”的元素内最后面加入内容*/
            content: ".";                    /*内容为“.”就是一个英文的句号而已。也可以不写。*/
            display: block;                  /*加入的这个元素转换为块级元素。*/
            clear: both;                     /*清除左右两边浮动。*/
            visibility: hidden;              /*可见度设为隐藏。注意它和display:none;是有区别的。*/
                                              /* visibility:hidden;仍然占据空间，只是看不到而已；*/
            line-height: 0;                  /*行高为0；*/
            height: 0;                       /*高度为0；*/
            font-size:0;                     /*字体大小为0；*/
        }
 

整段代码就相当于在浮动元素后面跟了个宽高为0的空div，然后设定它clear:both来达到清除浮动的效果。
之所以用它，是因为，你不必在html文件中写入大量无意义的空标签，又能清除浮动。
<div class="head clearfix"></div>


````

> 此外，还给父元素加上溢出隐藏属性（overflow: hidden;）来进行清除浮动。

#### 8 position属性

就像photoshop中的图层功能会把一整张图片分层一个个图层一样，网页布局中的每一个元素也可以看成是一个个类似图层的层模型。层布局模型就是把网页中的每一个元素看成是一层一层的，然后通过定位属性position对元素进行定位摆放，最终实现网页的布局。

定位属性position有4个值，分别是静态定位（static）、相对定位（relative）、绝对定位（absolute）和固定定位（fixed）。默认就是static。所以我们略过。

元素设置了定位以后，还要依靠4个方位属性来进行定位摆放。

方位属性：

```css
/*
top：让元素相对于指定目标的顶部偏移指定的距离。
  例如： top：10px; 表示距离顶部10像素

right：让元素相对于指定目标的右边偏移指定的距离。
  例如： right：10px; 表示距离顶部10像素

bottom：让元素相对于指定目标的底部偏移指定的距离。
  例如： bottom：10px; 表示距离顶部10像素

left：让元素相对于指定目标的左边偏移指定的距离。
  例如： left：10px; 表示距离顶部10像素
*/
```

##### 相对定位（relative）

相对定位就是在正常文档流中，元素相对于自身位置使用left、right、top、bottom属性进行定位偏移。

```css
      .c1{
            width: 200px;
            height: 200px;
            background-color: indianred;

        }

        .c2{
            width: 200px;
            height: 200px;
            background-color: orange;
            position: relative;
            left: 200px;
            top: 200px;


        }

        .c3{
            width: 200px;
            height: 200px;
            background-color: lightblue;


        }
```

##### 绝对定位（absolute）

绝对定位就是将元素脱离文档流，然后使用left、right、top、bottom属性相对于其最接近的一个具有定位属性的父级元素进行绝对定位，如果不存在这样的父级元素，则默认是相对于body元素进行绝对定位。

轮播图案例：

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
        <meta charset="utf8">
        <style>

            *{
                margin: 0;
                padding: 0;
            }

            .lunbo{
                width: 590px;
                height: 470px;
                border: 1px solid rebeccapurple;
                margin: 100px auto;
                position: relative;
            }

            .lunbo ul{
                list-style: none;
            }

            .lunbo .img li{
                position: absolute;
                top: 0;
                left: 0;
            }

            .lunbo .btn li{

                font-size: 25px;
                width: 40px;
                height: 40px;
                background-color: gray;
                text-align: center;
                line-height: 40px;
                border-bottom-right-radius: 50%;
                border-top-right-radius: 50%;
                color: white;

                position: absolute;
                top: 50%;
                margin-top: -20px;

            }

            .lunbo .left_btn{
                left: 0;
            }

            .lunbo .right_btn{
                right: 0;
            }
        </style>
  </head>
  <body>


  <div class="lunbo">
      <ul class="img">
          <li><a href=""><img src="imgs/1.jpg" alt=""></a></li>
          <li><a href=""><img src="imgs/2.jpg" alt=""></a></li>
          <li><a href=""><img src="imgs/3.jpg" alt=""></a></li>
          <li><a href=""><img src="imgs/4.jpg" alt=""></a></li>
          <li><a href=""><img src="imgs/5.jpg" alt=""></a></li>
      </ul>
      <ul class="btn">
          <li class="left_btn"> < </li>
          <li class="right_btn"> > </li>
      </ul>
  </div>
  </body>
</html>
```

###### 固定定位（fixed）

固定定位与绝对定位有点相似，但是固定定位是使用left、right、top、bottom属性相对于整个浏览器的窗口进行定位，而不再相对于某个HTML页面元素了，所以当元素使用了固定定位以后，就算页面的滚动条滚动了，固定定位的元素也不会变化位置。也就是说固定定位是相对于窗口的定位，不受文档流的影响了。

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
      <meta charset="utf8">
    <style>

        body{
            margin: 0;
        }

        .c1{
            width: 100%;
            height: 2000px;
            background-color: lightgray;
        }

        .c2{
            width: 200px;
            height: 60px;
            background-color: yellowgreen;
            text-align: center;
            line-height: 60px;
            position: fixed;
            right: 20px;
            bottom: 20px;
        }
        
    </style>
  </head>
  <body>

   <div class="c1"></div>
   <div class="c2">返回顶部</div>

  </body>
</html>
```







# 3 JavaScript

### 1.1、JavaScript 的历史

JavaScript 因为互联网而生，紧随着浏览器的出现而问世。回顾它的历史，就要从浏览器的历史讲起。

1990年底，欧洲核能研究组织（CERN）科学家Tim Berners-Lee，在全世界最大的电脑网络——互联网的基础上，发明了万维网（World Wide Web），从此可以在网上浏览网页文件。最早的网页只能在操作系统的终端里浏览，也就是说只能使用命令行操作，网页都是在字符窗口中显示，这当然非常不方便。

1992年底，美国国家超级电脑应用中心（NCSA）开始开发一个独立的浏览器，叫做Mosaic。这是人类历史上第一个浏览器，从此网页可以在图形界面的窗口浏览。

1994年10月，NCSA的一个主要程序员Marc Andreessen联合风险投资家Jim Clark，成立了Mosaic通信公司（Mosaic Communications），不久后改名为Netscape。这家公司的方向，就是在Mosaic的基础上，开发面向普通用户的新一代的浏览器Netscape Navigator。

1994年12月，Navigator发布了1.0版，市场份额一举超过90%。

Netscape 公司很快发现，Navigator浏览器需要一种可以嵌入网页的脚本语言，用来控制浏览器行为。当时，网速很慢而且上网费很贵，有些操作不宜在服务器端完成。比如，如果用户忘记填写“用户名”，就点了“发送”按钮，到服务器再发现这一点就有点太晚了，最好能在用户发出数据之前，就告诉用户“请填写用户名”。这就需要在网页中嵌入小程序，让浏览器检查每一栏是否都填写了。

管理层对这种浏览器脚本语言的设想是：功能不需要太强，语法较为简单，容易学习和部署。那一年，正逢Sun公司的Java语言问世，市场推广活动非常成功。Netscape公司决定与Sun公司合作，浏览器支持嵌入Java小程序（后来称为Java applet）。但是，浏览器脚本语言是否就选用Java，则存在争论。后来，还是决定不使用Java，因为网页小程序不需要Java这么“重”的语法。但是，同时也决定脚本语言的语法要接近Java，并且可以支持Java程序。这些设想直接排除了使用现存语言，比如Perl、Python和TCL。

1995年，Netscape公司雇佣了程序员Brendan Eich开发这种网页脚本语言。Brendan Eich有很强的函数式编程背景，希望以Scheme语言（函数式语言鼻祖LISP语言的一种方言）为蓝本，实现这种新语言。

1995年5月，Brendan Eich只用了10天，就设计完成了这种语言的第一版。为了保持简单，这种脚本语言缺少一些关键的功能，比如块级作用域、模块、子类型（subtyping）等等，但是可以利用现有功能找出解决办法。这种功能的不足，直接导致了后来JavaScript的一个显著特点：对于其他语言，你需要学习语言的各种功能，而对于JavaScript，你常常需要学习各种解决问题的模式。而且由于来源多样，从一开始就注定，JavaScript的编程风格是函数式编程和面向对象编程的一种混合体。

Netscape 公司的这种浏览器脚本语言，最初名字叫做 Mocha，1995年9月改为LiveScript。12月，Netscape公司与Sun公司（Java语言的发明者和所有者）达成协议，后者允许将这种语言叫做JavaScript。这样一来，Netscape公司可以借助Java语言的声势，而Sun公司则将自己的影响力扩展到了浏览器。

之所以起这个名字，并不是因为JavaScript本身与Java语言有多么深的关系（事实上，两者关系并不深），而是因为Netscape公司已经决定，使用Java语言开发网络应用程序，JavaScript可以像胶水一样，将各个部分连接起来。当然，后来的历史是Java语言的浏览器插件失败了，JavaScript反而发扬光大。

1995年12月4日，Netscape 公司与 Sun 公司联合发布了 JavaScript 语言。当时的意图是将 JavaScript 作为 Java 的补充，用来操作网页。

1996年3月，Navigator 2.0 浏览器正式内置了 JavaScript 脚本语言。

#### 1.2、JavaScript与ECMAScript的关系

1996年8月，微软模仿JavaScript开发了一种相近的语言，取名为JScript（JavaScript是Netscape的注册商标，微软不能用），首先内置于IE 3.0。Netscape公司面临丧失浏览器脚本语言的主导权的局面。

1996年11月，Netscape公司决定将JavaScript提交给国际标准化组织ECMA（European Computer Manufacturers Association），希望JavaScript能够成为国际标准，以此抵抗微软。ECMA的39号技术委员会（Technical Committee 39）负责制定和审核这个标准，成员由业内的大公司派出的工程师组成，目前共25个人。该委员会定期开会，所有的邮件讨论和会议记录，都是公开的。

1997年7月，ECMA组织发布262号标准文件（ECMA-262）的第一版，规定了浏览器脚本语言的标准，并将这种语言称为ECMAScript。这个版本就是ECMAScript 1.0版。之所以不叫JavaScript，一方面是由于商标的关系，Java是Sun公司的商标，根据一份授权协议，只有Netscape公司可以合法地使用JavaScript这个名字，且JavaScript已经被Netscape公司注册为商标，另一方面也是想体现这门语言的制定者是ECMA，不是Netscape，这样有利于保证这门语言的开放性和中立性。因此，ECMAScript和JavaScript的关系是，前者是后者的规格，后者是前者的一种实现。在日常场合，这两个词是可以互换的。

ECMAScript只用来标准化JavaScript这种语言的基本语法结构，与部署环境相关的标准都由其他标准规定，比如DOM的标准就是由W3C组织（World Wide Web Consortium）制定的。

> 一个完整的JavaScript包含三个部分：ECMAScript（标准语法），DOM以及BOM！

ECMA-262标准后来也被另一个国际标准化组织ISO（International Organization for Standardization）批准，标准号是ISO-16262。

#### 1.3、JavaScript与Java的关系

JavaScript和Java是两种不一样的语言，但是它们之间存在联系。

JavaScript的基本语法和对象体系，是模仿Java而设计的。但是，JavaScript没有采用Java的静态类型。正是因为JavaScript与Java有很大的相似性，所以这门语言才从一开始的LiveScript改名为JavaScript。基本上，JavaScript这个名字的原意是“很像Java的脚本语言”。

在JavaScript语言中，函数是一种独立的数据类型，以及采用基于原型对象（prototype）的继承链。这是它与Java语法最大的两点区别。JavaScript语法要比Java自由得多。

另外，Java语言需要编译，而JavaScript语言则是运行时由解释器直接执行。

总之，JavaScript的原始设计目标是一种小型的、简单的动态语言，与Java有足够的相似性，使得使用者（尤其是Java程序员）可以快速上手。

#### 1.4、JavaScript的版本

1997年7月，ECMAScript 1.0发布。

1998年6月，ECMAScript 2.0版发布。

1999年12月，ECMAScript 3.0版发布，成为JavaScript的通行标准，得到了广泛支持。

2007年10月，ECMAScript 4.0版草案发布，对3.0版做了大幅升级，预计次年8月发布正式版本。草案发布后，由于4.0版的目标过于激进，各方对于是否通过这个标准，发生了严重分歧。以Yahoo、Microsoft、Google为首的大公司，反对JavaScript的大幅升级，主张小幅改动；以JavaScript创造者Brendan Eich为首的Mozilla公司，则坚持当前的草案。

2008年7月，由于对于下一个版本应该包括哪些功能，各方分歧太大，争论过于激进，ECMA开会决定，中止ECMAScript 4.0的开发（即废除了这个版本），将其中涉及现有功能改善的一小部分，发布为ECMAScript 3.1，而将其他激进的设想扩大范围，放入以后的版本，由于会议的气氛，该版本的项目代号起名为Harmony（和谐）。会后不久，ECMAScript 3.1就改名为ECMAScript 5。

2009年12月，ECMAScript 5.0版正式发布。Harmony项目则一分为二，一些较为可行的设想定名为JavaScript.next继续开发，后来演变成ECMAScript 6；一些不是很成熟的设想，则被视为JavaScript.next.next，在更远的将来再考虑推出。TC39的总体考虑是，ECMAScript 5与ECMAScript 3基本保持兼容，较大的语法修正和新功能加入，将由JavaScript.next完成。当时，JavaScript.next指的是ECMAScript 6。第六版发布以后，将指ECMAScript 7。TC39预计，ECMAScript 5会在2013年的年中成为JavaScript开发的主流标准，并在此后五年中一直保持这个位置。

2011年6月，ECMAscript 5.1版发布，并且成为ISO国际标准（ISO/IEC 16262:2011）。到了2012年底，所有主要浏览器都支持ECMAScript 5.1版的全部功能。

2013年3月，ECMAScript 6草案冻结，不再添加新功能。新的功能设想将被放到ECMAScript 7。

2013年12月，ECMAScript 6草案发布。然后是12个月的讨论期，听取各方反馈。

2015年6月，ECMAScript 6正式发布，并且更名为“ECMAScript 2015”。这是因为TC39委员会计划，以后每年发布一个ECMAScirpt的版本，下一个版本在2016年发布，称为“ECMAScript 2016”。

除了ECMAScript的版本，很长一段时间中，Netscape公司（以及继承它的Mozilla基金会）在内部依然使用自己的版本号。这导致了JavaScript有自己不同于ECMAScript的版本号。1996年3月，Navigator 2.0内置了JavaScript 1.0。JavaScript 1.1版对应ECMAScript 1.0，但是直到JavaScript 1.4版才完全兼容ECMAScript 1.0。JavaScript 1.5版完全兼容ECMAScript 3.0。目前的JavaScript 1.8版完全兼容ECMAScript 5。

[参考链接](https://javascript.ruanyifeng.com/introduction/history.html)

### 2、JS的引入方式

```html
1 直接编写
    <script>
        console.log('hello yuan')
    </script>
2 导入文件
    <script src="hello.js"></script>
```

### 3、ECMAScript基本语法

js是一门弱类型的编程语言,属于基于对象和基于原型的脚本语言.

* 变量

```js
格式:
	    // 方式1 先声明再赋值
	    var 变量名;   // 声明的变量如果没有进行赋值,或者没有被定义的变量,值默认是undefined
      变量名 = 变量值;
	    // 方式2 声明并赋值
      var 变量名 = 变量值;
      // 方式3 一行可以声明多个变量.并且可以是不同类型
      var name="yuan", age=20, job="lecturer";
		// 全局变量就是直接赋值
		a = '66'
     
```

> 1、声明变量时 可以不用var. 如果不用var 那么它是全局变量
>
> 2、变量命名,首字符只能是字母,下划线,$美元符 三选一，余下的字符可以是下划线、美元符号或任何字母或数字字符且区分大小写

*  注释

```js
// 单行注释

 /*
   多行注释
 */
```

* 语句分隔符

```js
var a = 1   // 分号和换行符作为语句分隔符号
var b = 2;
console.log(a,b)
```

### 4、ECMAScript 基本数据类型

<img src="web.assets/image-20210301140011992.png" alt="image-20210301140011992" style="zoom:67%;" />

#### 4.4.1、数字类型

JavaScript 没有整型和浮点型，只有一种数字类型，即number类型。

```js
var x = 10;
var y = 3.14;
console.log(x,typeof x);  // 10 "number"
console.log(y,typeof y);  // 3.14 "number"
```

#### 4.4.2、字符串

字符串创建(两种方式)

* 变量 = “字符串”
* 字串对象名称 = new String (字符串)

```js
var str1="hello world";
var str1= new String("hello word");
```

```js
// 字符串对象的操作
var str = "hello"; // 这就是字符串对象
console.log(str);

// 字符串对象内置属性
// length 计算字符串的长度
console.log( str.length );

// 字符串对象内置方法
// toUpperCase();  字母大写转换
// toLowerCase();  字母小写转换

console.log( str.toUpperCase() );
console.log( str.toLowerCase() );

// indexOf 获取指定字符在字符串中第一次出现的索引位置
// 字符串也有下标,也可以使用中括号来提取字符串的指定字符
console.log(str[1]); // e
console.log( str.indexOf("e") ); // 1

// 切片,当前方法支持使用负数代表倒数下标
// slice(开始下标)   从开始位置切到最后
// slice(开始下标,结束下标)  从开始下标切到指定位置之前
var str = "helloworld";
var ret = str.slice(3,6); // 开区间,不包含结束下标的内容
console.log(ret); // low
var ret = str.slice(5);
console.log(ret); // world
var ret = str.slice(2,-1);
console.log(ret); // lloworl
var ret = str.slice(-4,-1);
console.log(ret); // orl
var ret = str.slice(-1,-4);
console.log(ret); // orl

// split   正则分割,经常用于把字符串转换成数组
var str = "广东-深圳-南山";
var ret = str.split("-");
console.log( ret );

// substr  截取
var str = "hello world";
var ret = str.substr(0,3);
console.log(ret); // hel

// trim    移除字符串首尾空白
var password = "    ge llo   ";
var ret = password.trim();
console.log(password.length); // 13
console.log(ret.length);  // 6

```

#### 4.4.3、布尔值

> 1、Boolean类型仅有两个值：true和false，也代表1和0，实际运算中true=1,false=0
> 2、布尔值也可以看作on/off、yes/no、1/0对应true/false;
> 3、Boolean值主要用于JavaScript的控制语句

```js
console.log(true);
console.log(false);
console.log(typeof true);
console.log(true === 1);
console.log(true == 1);
console.log(true + 1);
console.log(false + 1);
```

#### 4.4.4、空值（Undefined和Null）

* undefined类型

undefined类型只有一个值，即 undefined。

（1）当声明的变量未初始化时，该变量的默认值是 undefined。

（2）当函数无明确返回值时，返回的也是值 undefined;

* null类型

另一种只有一个值的类型是 null，它只有一个专用值 null，即它的字面量。值 undefined 实际上是从值 null 派生来的，因此 ECMAScript 把它们定义为相等的。

尽管这两个值相等，但它们的含义不同。undefined 是声明了变量但未对其初始化时赋予该变量的值，null 则用于表示尚未存在的对象。如果函数或方法要返回的是对象，那么找不到该对象时，返回的通常是 null。

#### 4.4.5、类型转换

js中,类型转换有2种.一种就是强制转换,一种就是自动转换.

> 因为js是一门弱类型的脚本语言,所以变量会在运算符的运行要求,有时候根据运算符的要求,进行自动转换的.

* 强制转换

```js
// 1. 转换数据为数值类型
// parseInt     把数据转换成整数
// parseFloat   把数据转换成小数
// Number       把数据转换成数值
var box1 = "一共100件"; // 转换会失败
var box1 = "100件";     // 转换会成功
var ret = parseInt(box1);
console.log(box1);
console.log(ret);
//
var box2 = "3.14";
console.log(parseFloat(box2) ); // 3.14
//
var box3 = "3.14";   // 使用Number转换的数据里面必须是纯数字!!!!否则都会转换失败
// var box3 = "3.1.4";  // 转换失败!
console.log( Number(box3) );

// 对于转换数值,如果转换失败的话,则结果为 NaN ,是 Not a Number ,但是NaN的类型也是number类型

// 2. 转换数据为字符串
// 变量.toString()
// String(数据)
var box4 = 3.14;
var ret = box4.toString();
console.log(ret);
//
ret = String(box4);
console.log(ret);

// 3. 转换数据成布尔类型
// Boolean()

var box5 = "";
console.log( Boolean(box5) ); // false
var box6 = -1;
console.log( Boolean(box6) ); // true
var box7 = 0;
console.log( Boolean(box7) ); // false;
var box8 = "false";
console.log( Boolean(box8) ); // true
var box9 = [];
console.log( Boolean(box9) ); // true
var box10 = {};
console.log( Boolean(box10) ); // true
var box11 = "0";
console.log( Boolean(box11) ); // true
var box12 = null;
console.log( Boolean(box12) ); // false
var box13 = undefined;
console.log( Boolean(box13) ); // false
```

* 自动转换

```js
// 所谓的自动转换,其实弱类型中的变量会根据当前代码的需要,进行类型的自动隐式转化
var box1 = 1 + true;
// true 转换成数值,是1, false转换成数值,是0
console.log(box1); // 2

var box2 = 1 + "200";
console.log(box2); // 1200 原因是,程序中+的含义有2种,第一: 两边数值相加, 第二: 两边字符串拼接.但是在js中运算符的优先级中, 字符串拼接的优先级要高于数值的加减乘除,所以解析器优先使用了+号作为了字符串的拼接符号了,因为程序就需要+号两边都是字符串才能完成运算操作,因此1变成字符串最终的结果就是 "1" +"200"

var box3 = 1 - "200";
console.log(box3); // -199;因为-号中表示的就是左边的数值减去右边的数值,因此程序就会要求"200"是数值,因此内部偷偷的转换了一下
```

#### 4.4.6、原始值和引用值

根据数据类型不同，有的变量储存在栈中，有的储存在堆中。具体区别如下：

原始变量及他们的值储存在栈中，当把一个原始变量传递给另一个原始变量时，是把一个栈房间的东西复制到另一个栈房间，且这两个原始变量互不影响。

引用值是把 引用变量的名称储存在栈中，但是把其实际对象储存在堆中，且存在一个指针由变量名指向储存在堆中的实际对象，当把引用对象传递给另一个变量时，复制的其实是指向实际对象的指针， 此时 两者指向的 是同一个数据，若通过方法改变其中一个变量的值，则访问另一个变量时，其值也会随之加以改变；但若不是通过方法 而是通过 重新赋值 此时 相当于 重新开了一个房间 该值的原指针改变 ，则另外一个 值不会随他的改变而改变。

```js
// 初始值类型
var a = "yuan";
var b = a;
a = "alvin";
console.log(a);//alvin
console.log(b);//yuan

// 对象类型
var arr1=[1,2];
arr2 = arr1;
arr1.push(3);
console.log(arr1)// [1,2,3]
console.log(arr2);//[1,2,3]

arr1=[4,5];
console.log(arr1);//[4,5]
console.log(arr2);//[1,2,3]
```

### 5、运算符

* 运算符

```js
/*
//算术运算符
   +   数值相加
   -   数值相减
   *   数值相乘
   /   数值相除
   %   数值求余
   **  数值求幂
   a++ 数值后自增1   a=a+1
   ++a 数值前自增1   a=a+1
   b-- 数值后自减1   b=b-1
   --b 数值前自减1   b=b-1
   
//赋值运算符
   =
   +=
   -=
   *=
   /=
   %=
   **=

//比较运算符,比较的结果要么是true, 要么是false
	>   大于
	<   小于
	>=  大于或者等于
	<=  小于或者等于
	!=  不等于[计算数值]
	==  等于[计算]

  !== 不全等[不仅判断数值,还会判断类型是否一致]
	=== 全等[不仅判断数值,还会判断类型是否一致]

//逻辑运算符
  &&   并且  and    两边的运算结果为true,最终结果才是true
  ||   或者  or     两边的运算结果为false,最终结果才是false
  !    非    not    运算符的结果如果是true,则最终结果是false ,反之亦然.
 
  //逻辑运算符进阶用法:
     1. 实现短路
        var a = false || 2      >>> a = 2
        var a = true && "hehe"  >>>  a = "hehe"
     
     2. 快速布尔化[把数据快速转换成布尔类型]
        var a = 100
        !!a  >>> true

//条件运算符[三目运算符]
	 条件?true:false
	 例如:
	      var age = 12;
        var ret = age>=18?"成年":"未成年"; // 相当于 python中的"成年" if age >= 18 else "未成年"
        console.log(ret);
 */
```

### 6、流程控制语句

编程语言的流程控制分为三种：

- 顺序结构(从上向下顺序执行)
- 分支结构
- 循环结构

之前我们学习的方式就是顺序执行，即代码的执行从上到下，一行行分别执行。

例如：

```js
console.log("星期一");
console.log("星期二");
console.log("星期三");

```

#### 6.1、分支结构

* if 分支语句

```js
 if(条件){
     // 条件为true时,执行的代码
   }
   
   if(条件){
     // 条件为true时,执行的代码
   }else{
     // 条件为false时,执行的代码
   }
   
   if(条件1){
     // 条件1为true时,执行的代码
   }else if(条件2){
     // 条件2为true时,执行的代码
   
   }....
   
   }else{
     // 上述条件都不成立的时候,执行的代码
   }
```

* switch语句

```js
switch(条件){
      case 结果1:
           满足条件执行的结果是结果1时,执行这里的代码..
           break;
      case 结果2:
      	   满足条件执行的结果是结果2时,执行这里的代码..
      	   break;
      .....
      default:
           条件和上述所有结果都不相等时,则执行这里的代码
   }
```

> 1、switch比if else更为简洁
>
> 2、执行效率更高。switch…case会生成一个跳转表来指示实际的case分支的地址，而这个跳转表的索引号与switch变量的值是相等的。从而，switch…case不用像if…else那样遍历条件分支直到命中条件，而只需访问对应索引号的表项从而到达定位分支的目的。
>
> 3、到底使用哪一个选择语句，代码环境有关，如果是范围取值，则使用if else语句更为快捷；如果是确定取值，则使用switch是更优方案。

#### 6.2、循环语句

* while循环

```js
   while(循环的条件){
      // 循环条件为true的时候,会执行这里的代码
   }
  
```

循环案例：

```js
 var count = 0
 while (count<10){
     console.log(count);
     count++;
 }
```

* for循环

```js
   
   // 循环三要素
   for(1.声明循环的开始; 2.条件; 4. 循环的计数){
      // 3. 循环条件为true的时候,会执行这里的代码
   }
   
   for(循环的成员下标 in 被循环的数据){
      // 当被循环的数据一直没有执行到最后下标,都会不断执行这里的代码
   }   
```

循环案例：

```js
// 方式1
for (var i = 0;i<10;i++){
	console.log(i)
}

// 方式2
var arr = [111,222,333]
for (var i in arr){
    console.log(i,arr[i])
}

```

* 退出循环（break和continue）

```js
 for (var i = 0;i<100;i++){
           if (i===88){
               continue  // 退出当次循环
               // break  // 退出当前整个循环
           }
           console.log(i)
       }
```

> 作业：
>
> （1）计算1+2+3+...+100=？
>
> （2）求20的阶乘值

### 7、数组对象

* 创建数组

```js
创建方式1:
var arrname = [元素0,元素1,….];          // var arr=[1,2,3];

创建方式2:
var arrname = new Array(元素0,元素1,….); // var test=new Array(100,"a",true);
```

* 数组方法

```js
var arr = ["A","B","C","D"];
// 内置属性
console.log( arr.length );
// 获取指定下标的成员
// console.log( arr[3] ); // D
console.log( arr[arr.length-1] ); // 最后一个成员

// (1) pop()  出栈,删除最后一个成员作为返回值
var arr = [1,2,3,4,5];
var ret = arr.pop();
console.log(arr); // [1, 2, 3, 4]
console.log(ret); // 5


// (2) push() 入栈,给数组后面追加成员
var arr = [1,2,3,4,5];
arr.push("a");
console.log(arr); // [1, 2, 3, 4, 5, "a"]


// (3) shift是将数组的第一个元素删除
var arr = [1,2,3,4,5];
arr.shift()
console.log(arr); // [2, 3, 4, 5]

// (4) unshift是将value值插入到数组的开始
var arr = [1,2,3,4,5];
arr.unshift("yuan")
console.log(arr); // ["yuan",1,2, 3, 4, 5]


// (5) reverse() 反转排列
var arr = [1,2,3,4,5];
arr.reverse();
console.log(arr); // [5, 4, 3, 2, 1]

// (6) slice(开始下标,结束下标)  切片,开区间


// (7) sort() 排序
var arr = [3,4,1,2,5,10];
console.log( arr ); // [3, 4, 1, 2, 5, 10]
arr.sort();
//
// // 这是字符的排序,不是数值的排序
console.log(arr);   //  [1, 10, 2, 3, 4, 5]

// 数值升序
var arr = [3,4,1,2,5,10];
arr.sort(function(a,b){
    return a-b;
});
console.log(arr);  // [1, 2, 3, 4, 5, 10]

// 数值降序
var arr = [3,4,1,2,5,10];
arr.sort(function(a,b){
    return b-a;
});
console.log(arr); // [10, 5, 4, 3, 2, 1]

// (8) splice(操作位置的下标,删除操作的成员长度,"替换或者添加的成员1","替换或者添加的成员2")  添加/删除指定的成员   "万能函数"
var arr1 = [1,2,3];
arr1.splice(1,1);
console.log(arr1); // 删除指定的1个成员  [1, 3]

var arr2 = ["a","b","c","d"];
arr2.splice(2,0,"w","x","w"); // 添加
console.log(arr2); // ["a", "b", "w", "x", "w", "c", "d"]

var arr3 = ["a","b","c"];
arr3.splice(1,1,"w");
console.log(arr3); // ["a", "w", "c"]

// (9) concat() 把2个或者多个数组合并
var arr1 = [1,2,3];
var arr2 = [4,5,7];
var ret = arr1.concat(arr2);
console.log( ret );


// (10) join()  把数组的每一个成员按照指定的符号进行拼接成字符串
var str = "广东-深圳-南山";
var arr = str.split("-");
console.log( arr ); // ["广东", "深圳", "南山"];

var arr1 = ["广东", "深圳", "南山"];
var str1 = arr1.join("-");
console.log( str1 ); // 广东-深圳-南山


// (11) find()  高阶函数, 返回符合条件的第一个成员
var arr = [4,6,5,7];
var func = (num)=>{
    if(num%2===0){
        return num;
    }
};
var ret = arr.find(func);
console.log( ret ); // 4

// (12)  filter() 高阶函数, 对数组的每一个成员进行过滤,返回符合条件的结果
var arr = [4,6,5,7];
function func(num){  // 也可以使用匿名函数或者箭头函数
    if(num%2===0){
        return num;
    }
}
var ret = arr.filter(func);  // 所有的函数名都可以作为参数传递到另一个函数中被执行
console.log( ret );

// (13) map() 对数组的每一个成员进行处理,返回处理后的每一个成员
var arr = [1,2,3,4,5];
var ret = arr.map((num)=>{
    return num**3;
});
console.log( ret  ); // [1, 8, 27, 64, 125]

// (14) 其它方法
// includes   查询指定数据是否在数组中存在!
// indexOf()  查询指定数据在数组中第一次出现的位置
// isArray()  判断变量的值是否是数组
       
```

* 遍历数组

```js
 var arr = [12,23,34]
 for (var i in arr){
       console.log(i,arr[i])
 }
```

### 8、Object对象

#### 8.1、object对象的基本操作

 Object 的实例不具备多少功能，但对于在应用程序中存储和传输数据而言，它们确实是非常理想的选择。
`创建 Object 实例的方式有两种。`

```js
var person = new Object();
person.name = "alvin";
person.age = 18;
```

`另一种方式是使用对象字面量表示法。`对象字面量是对象定义的一种简写形式，目的在于简化创建包含大量属性的对象的过程。下面这个例子就使用了对象字面量语法定义了与前面那个例子中相同的person 对象：

```js
var person = {
                name : "alvin",
                age : 18
             }; 
```

* object可以通过. 和 []来访问。

```js
console.log(person["age"]);
console.log(person.age)
```

* object可以通过for循环遍历

```js
 for (var attr in person){
           console.log(attr,person[attr]);
      }
```

#### 8.2、json序列化和反序列化

`JSON`：JavaScript 对象表示法（JavaScript Object Notation），是一种轻量级的数据交换格式。易于人阅读和编写。

```js
# json是一种数据格式, 语法一般是{}或者[]包含起来
# 内部成员以英文逗号隔开,最后一个成员不能使用逗号!
# 可以是键值对,也可以是列表成员
# json中的成员如果是键值对,则键名必须是字符串.而json中的字符串必须使用双引号圈起来
# json数据也可以保存到文件中,一般以".json"结尾.
# 前端项目中,一般使用json作为配置文件.

{
   "name": "xiaoming",
	 "age":12
}

[1,2,3,4]

{
   "name": "xiaoming",
	 "age":22,
   "sex": true,
   "son": {
      "name":"xiaohuihui",
      "age": 2
   },
   "lve": ["篮球","唱","跳"]
}
```

js中也支持序列化和反序列化的方法：

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script>
    // js对象,因为这种声明的对象格式很像json,所以也叫json对象
    var data = {
        name: "xiaoming",
        age: 22,
        say: function(){
            alert(123);
        }
    };

    // 把json对象转换成json字符串
    var ret = JSON.stringify(data);
    console.log(ret ); // {"name":"xiaoming","age":22}

    // 把json字符串转换成json对象
    var str = `{"name":"xiaoming","age":22}`;
    var ret = JSON.parse(str);
    console.log(ret);
</script>
</body>
</html>
```

### 9、Date对象

* 创建Date对象

```js
//方法1：不指定参数
var nowd1=new Date();
console.log(nowd1.toLocaleString( ));//获取当前本地时间的时间格式



//方法2：参数为日期字符串
var d2=new Date("2004/3/20 11:12");
console.log(d2.toLocaleString( ));
var d3=new Date("04/03/20 11:12");
console.log(d3.toLocaleString( ));




//方法3：参数为毫秒数，时间戳
var d4=new Date(5000);
console.log(d4.toLocaleString( ));
console.log(d4.toUTCString());

//方法4：参数为年月日小时分钟秒毫秒
var d5=new Date(2004,2,20,11,12,0,300);
console.log(d5.toLocaleString( ));//毫秒并不直接显示
```

* 获取时间信息

```java
获取日期和时间
getDate()                 获取日
getDay ()                 获取星期
getMonth ()               获取月（0-11）
getFullYear ()            获取完整年份
getYear ()                获取年
getHours ()               获取小时
getMinutes ()             获取分钟
getSeconds ()             获取秒
getMilliseconds ()        获取毫秒
getTime ()                返回累计毫秒数(从1970/1/1午夜)
```

* 日期和时间的转换

```java
日期和时间的转换:
// 返回国际标准时间字符串
toUTCString()
// 返回本地格式时间字符串
toLocalString()
// 返回累计毫秒数(从1970/1/1午夜到本地时间) 时间戳
Date.parse(x)
// 返回累计毫秒数(从1970/1/1午夜到国际时间)
Date.UTC(x)

```

练习：以`2021年03月2日 14:1:43 星期二`格式化输出当前时间

```js
 function getCurrentDate(){
            //1. 创建Date对象
            var date = new Date(); //没有填入任何参数那么就是当前时间
            //2. 获得当前年份
            var year = date.getFullYear();
            //3. 获得当前月份 js中月份是从0到11.
            var month = date.getMonth()+1;
            //4. 获得当前日
            var day = date.getDate();
            //5. 获得当前小时
            var hour = date.getHours();
            //6. 获得当前分钟
            var min = date.getMinutes();
            //7. 获得当前秒
            var sec = date.getSeconds();
            //8. 获得当前星期
            var week = date.getDay(); //没有getWeek
            // 2014年06月18日 15:40:30 星期三
            return year+"年"+changeNum(month)+"月"+day+"日 "+hour+":"+min+":"+sec+" "+parseWeek(week);
        }

//解决 自动补齐成两位数字的方法
function changeNum(num){
    if(num < 10){
        return "0"+num;
    }else{
        return num;
    }
}
//将数字 0~6 转换成 星期日到星期六
function parseWeek(week){
    var arr = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
    //             0      1      2      3 .............
    return arr[week];
}

console.log(getCurrentDate());
```

### 10、Math对象

```js
 //  Number对象的内置方法
 //  toFixed(x) 保留小数位
 var num = 100.3;
 var ret = num.toFixed(2);
 console.log(num);  // 100.3
 console.log(ret);  // 100.30

// Math对象的内置方法
// abs(x)  返回数值的绝对值
// var num = -10;
console.log( Math.abs(num) ); // 10

// ceil(x)  向上取整
var num = 10.3;
console.log( Math.ceil(num) ); // 11

// floor(x) 向下取整
var num = 10.3;
console.log( Math.floor(num) ); // 10

// max(x,y,z,...,n)
console.log( Math.max(3,56,3) ); // 56
// min(x,y,z,...,n)

// pow(x,y)
console.log(Math.pow(3, 2)); // 相等于 3**2
console.log( 3**2 ); // 使用这个,上面废弃

// random()  生成0-1随机数
console.log( Math.random() );

// 生成0-10之间的数值
console.log( Math.random() * 10 );

// round(x) 四舍五入
// 生成0-10之间的整数
console.log( Math.round( Math.random() * 10 ) );
```

* 练习：获取1-100的随机整数，包括1和100

```js
var num=Math.random();
num=num*100;
num=Math.round(num);
console.log(num)
```

### 11、Function 对象

函数在程序中代表的就是一段具有功能性的代码，可以让我们的程序编程更加具有结构性和提升程序的复用性,也能让代码变得更加灵活强大

### 11.1、声明函数

```js
// 函数的定义方式1
function 函数名 (参数){
    函数体;
    return 返回值;
}
功能说明：
    可以使用变量、常量或表达式作为函数调用的参数
    函数由关键字function定义
    函数名的定义规则与标识符一致，大小写是敏感的
    返回值必须使用return
    
//  函数的定义方式2
    
用 Function 类直接创建函数的语法如下：
var 函数名 = new Function("参数1","参数n","function_body");

虽然由于字符串的关系，第二种形式写起来有些困难，但有助于理解函数只不过是一种引用类型，它们的行为与用 Function 类明确创建的函数行为是相同的。    
   
```

### 11.2、函数调用

```js
    //f(); --->OK
    function f(){
        console.log("hello")

    }
    f() //----->OK

```

>不同于python，js代码在运行时，会分为两大部分———预编译 和 执行阶段。
>
>- 预编译：会先检测代码的语法错误，进行变量、函数的声明。
>- 执行阶段：变量的赋值、函数的调用等，都属于执行阶段。

### 11.3、函数参数

（1） 参数基本使用

```js
// 位置参数
function add(a,b){
    console.log(a);
    console.log(b);
}
add(1,2)
add(1,2,3)
add(1)

// 默认参数
function stu_info(name,gender="male"){
    console.log("姓名："+name+" 性别："+gender)
}

stu_info("yuan")
```

（2）函数中的arguments对象

```js
function add(a,b){

        console.log(a+b);//3
        console.log(arguments.length);//2
        console.log(arguments);//[1,2]

    }
add(1,2)

// arguments的应用1 
function add2(){
    var result=0;
    for (var num in arguments){
        result+=arguments[num]
    }
    console.log(result)

}

add2(1,2,3,4,5)

// arguments的应用2

function f(a,b,c){
    if (arguments.length!=3){
        throw new Error("function f called with "+arguments.length+" arguments,but it just need 3 arguments")
    }
    else {
        alert("success!")
    }
}

f(1,2,3,4,5)

```

### 11.4、函数返回值

在函数体内，使用 return 语句可以设置函数的返回值。一旦执行 return 语句，将停止函数的运行，并运算和返回 return 后面的表达式的值。如果函数不包含 return 语句，则执行完函数体内每条语句后，返回 undefined 值。

```js
function add(x,y) {
          return x+y
      }

var ret = add(2,5);
console.log(ret)
```

> 1、在函数体内可以包含多条 return 语句，但是仅能执行一条 return 语句
>
> 2、函数的参数没有限制，但是返回值只能是一个；如果要输出多个值，可以通过数组或对象进行设计。

### 11.5、匿名函数

匿名函数，即没有变量名的函数。在实际开发中使用的频率非常高！也是学好JS的重点。

```js
      // 匿名函数赋值变量
       var foo = function () {
           console.log("这是一个匿名函数！")
       };

      // 匿名函数的自执行
      (function (x,y) {
           console.log(x+y);
       })(2,3)


     // 匿名函数作为一个高阶函数使用
     function bar() {

        return function () {
            console.log("inner函数！")
        }
    }

    bar()()
        
```

> 使用匿名函数表达式时，函数的调用语句，必须放在函数声明语句之后！

### 11.6、函数作用域

作用域是JavaScript最重要的概念之一，想要学好JavaScript就需要理解JavaScript作用域和作用域链的工作原理。

任何程序设计语言都有作用域的概念，简单的说，作用域就是变量可访问范围，即作用域控制着变量与函数的可见性和生命周期。在JavaScript中，变量的作用域有全局作用域和局部作用域两种。

```js
// 局部变量,是在函数内部声明,它的生命周期在当前函数被调用的时候, 当函数调用完毕以后,则内存中自动销毁当前变量
// 全局变量,是在函数外部声明,它的生命周期在当前文件中被声明以后就保存在内存中,直到当前文件执行完毕以后,才会被内存销毁掉
```

首先熟悉下var

```js
    var name = "yuan"; // 声明一个全局变量 name并赋值”yuan“
    name = "张三";  // 对已经存在的变量name重新赋值 ”张三“
    console.log(name);

    age = 18   // 之前不存在age变量，这里等同于var age = 19 即声明全局变量age并赋值为18

    var  gender = "male"
    var  gender = "female" // 原内存释放与新内存开辟，指针指向新开辟的内存
    console.log(gender)
```

  作用域案例：

```js
 var num = 10; // 在函数外部声明的变量, 全局变量
    function func(){
        // num = 20; // 函数内部直接使用变量,则默认调用了全局的变量,
        //var num = 20; // 函数内部使用var 或者 let声明的变量则是局部变量
                  // 函数内部直接使用变量,则默认调用了全局的变量,
                  // 使用变量的时候,解释器会在当前花括号范围值搜索是否有关键字var 或者 let 声明了变量,如果没有,则一层一层往外查找最近的声明
                  // 如果最终查找不到,则直接报错! 变量名 is not define!
        console.log("函数内部num：",num)
    }
func();
console.log("全局num：",num);
```

### 11.7、JS的预编译

js运行三个阶段：

1. 语法分析
2. 预编译
3. 解释执行

语法分析就是JS引擎去检查你的代码是否有语法错误，解释执行就是执行你的代码。最重要最需要理解的就是第二个环节预编译，简单理解就是在内存中开辟一些空间，存放一些变量与函数 。

预编译可分为全局预编译和局部预编译。

> 1. 在js脚本加载之后，会先通篇检查是否存在低级错误；
> 2. 在语法检测完之后，便进行全局预编译；
> 3. 在全局预编译之后，就解释一行，执行一行；
> 4. 当执行到函数调用那一行前一刻，会先进行函数预编译，再往下执行。

**全局预编译的3个步骤：**

1. 创建GO对象（Global Object）全局对象，即window对象。
2. 找变量声明，将变量名作为GO属性名，值为undefined
3. 查找函数声明，作为GO属性，值赋予函数体

**局部预编译的4个步骤：**

1. 创建AO对象（Activation Object）执行期上下文。
2. 找形参和变量**声明**，将变量和形参名作为AO属性名，值为undefined
3. 将实参值和形参统一。
4. 在函数体里面找函数声明，值赋予函数体。

> GO对象是全局预编译，所以它优先于AO对象所创建和执行

案例分析：

```js 
  <script>
        var a = 10;
        console.log(a);

        function foo(a) {
          console.log(a);
          var a = 100;
          console.log(a);
          function a() {}
          console.log(a);
          var b = function(){};
          console.log(b);
          function d() {}
        }
        var c = function (){
        console.log("匿名函数C");
        };
        console.log(c);
        foo(20);

  </script>

```

##### 全局预编译

```js
    GO/window = {
        a: undefined,
        c: undefined，
        foo: function(a) {
            console.log(a);
            var a = 123;
            console.log(a);
            function a() {}
            console.log(a);
            var b = function() {}
            console.log(b);
            function d() {}
        }
    }
```

##### 解释执行代码（直到执行调用函数foo(20)语句）

````
GO/window = {
        a: 10,
        c: function (){
            console.log("I at C function");
        }
        test: function(a) {
            console.log(a);
            var a = 123;
            console.log(a);
            function a() {}
            console.log(a);
            var b = function() {}
            console.log(b);
            function d() {}
        }
    }
````

##### 调用函数foo(20)前发生布局预编译

```js
// 局部预编译前两步：
AO = {
        a:undefined,
        b:undefined,
    }

// 局部预编译第三步：
AO = {
            a:20,
            b:undefined,
        }
// 局部预编译第四步：
AO = {
        a:function a() {},
        b:undefined
        d:function d() {}
    }
```

预编译总结：

1. 函数声明整体提升-(具体点说，无论函数调用和声明的位置是前是后，系统总会把函数声明移到调用前面）
2. 变量 声明提升-(具体点说，无论变量调用和声明的位置是前是后，系统总会把声明移到调用前，注意仅仅只是声明，所以值是undefined）

面试题：

```js
var num3 = 10;
function func3(){
    console.log(num3); 
    var num3 = 20;       
}
func3();
console.log(num3); 


 /*

        // 全局编译

        GO{
           num3:undefined,
           func3: function (){
            console.log(num3);
            var num3 = 20;
        }

        // 全局执行
        var num3 = 10;
        GO{
           num3:10,
           func3: function (){
            console.log(num3);
            var num3 = 20;
        }


        // 局部编译
        func3.AO{
           num3:undefined,
        }


        // 局部执行

        func3.AO{
           num3:20,
        }

        // 全局执行

        GO.num3 = 10
        }

*/
```







# 4 JavaScript(2)

### 1、BOM对象

BOM:Broswer object model,即浏览器提供我们开发者在javascript用于操作浏览器的对象。

#### 1、window对象

##### 1 窗口方法

```js
// BOM  Browser object model 浏览器对象模型

// js中最大的一个对象.整个浏览器窗口出现的所有东西都是window对象的内容.
console.log( window );

// alert()  弹出一个警告框
window.alert("hello");

//confirm  弹出一个确认框,点击确认,返回true, 点击取消,返回false
var ret = confirm("您确认要删除当前文件么?");
console.log( ret  );

// 弹出一个消息输入框,当点击确认以后,则返回可以接收到用户在输入框填写的内容.如果点击取消,则返回null
var ret = prompt("请输入一个内容","默认值");
console.log( ret );

// close() 关闭当前浏览器窗口
window.close();

//打开一个新的浏览器窗口
window.open("http://www.baidu.com","_blank","width=800px,height=500px,left=200px,top=200px";
            
```

##### 2 定时方法

setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。由 setInterval() 返回的 ID 值可用作 clearInterval() 方法的参数。而setTimeout是在指定的毫秒数后调用code一次。

```js
// 设置循环定时器
var ID = window.setInterval(code,millisec)   // 每millisec毫秒执行一次code  （赛特 英特喔）
// 取消循环定时器
window.clearInterval(ID);  // （咳李额 英特喔）

// 设置单次定时器
var ID = window.setTimeout(code,millisec) // millisec毫秒后执行code一次 （赛特 台拿（啊）特）
// 取消单次定时器
window.clearTimeout(ID);                                              // （咳李额 台拿（啊）特 ）

```

其中，code为要调用的函数或要执行的代码串。millisec周期性执行或调用 code 之间的时间间隔，以毫秒计。

显示时间案例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<input id="ID1" type="text" >
<button onclick="begin()">开始</button>
<button onclick="end()">停止</button>

<script>
    function showTime(){
           var nowd2=new Date().toLocaleString();
           var temp=document.getElementById("ID1");
           temp.value=nowd2;

    }
    var ID;
    function begin(){
        if (ID==undefined){
             showTime();
             ID=setInterval(showTime,1000);
        }
    }
    function end(){
        clearInterval(ID);
        ID=undefined;
    }

</script>

</body>
</html>
```

#### 2、Location ( 地址栏)对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<button onclick="func1()">查看Location对象</button>
<button onclick="func2()">跳转到百度</button>
<button onclick="func3()">F5</button>
<script>
    function func1(){
        console.log( location );
    }
    // 地址栏对象控制和操作地址栏
    // 所谓的地址就是当前页面所在地址
    // 地址结构:
    // 协议://域名:端口/路径/文件名?查询字符串#锚点
    console.log( `协议=>${location.protocol}` );
    console.log( `端口=>${location.port}` );
    console.log( `域名=>${location.hostname}` );
    console.log( `域名:端口=>${location.host}` );
    console.log( `路径=>${location.pathname}` );
    console.log( `查询字符串=>${location.search}` );
    console.log(`完整的地址信息=>${location.href}`);

    function func2(){
        // location.href="http://www.baidu.com"; // 页面跳转
        location.assign("http://www.baidu.com"); // 页面跳转
    }

    function func3(){
        location.reload(); // 刷新页面
    }
</script>
</body>
</html>
```

#### 3、本地存储对象

使用存储对象的过程中, 对象数据会根据域名端口进行保存的,所以 js不能获取当前页面以外其他域名端口保存到本地的数据。也就是说,我们存储对象获取数据只能是自己当前端口或者域名下曾经设置过的数据,一旦端口或者域名改变,则无法获取原来的数据。

```js
localStorage    本地永久存储
  localStorage.setItem("变量名","变量值");   保存一个数据到存储对象
  localStorage.变量名 = 变量值               保存一个数据到存储对象

  localStorage.getItem("变量名")   获取存储对象中保存的指定变量对应的数据
  localStorage.变量名              获取存储对象中保存的指定变量对应的数据

  localStorage.removeItem("变量名")   从存储对象中删除一个指定变量对应的数据
  localStorage.clear()               从存储对象中删除所有数据

sessionStorage  本地会话存储
  sessionStorage.setItem("变量名","变量值");   保存一个数据到存储对象
  sessionStorage.变量名 = 变量值               保存一个数据到存储对象

  sessionStorage.getItem("变量名")   获取存储对象中保存的指定变量对应的数据
  sessionStorage.变量名              获取存储对象中保存的指定变量对应的数据

  sessionStorage.removeItem("变量名")   从存储对象中删除一个指定变量对应的数据
  sessionStorage.clear()               从存储对象中删除所有数据
```

练习：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<button onclick="func1()">设置一个数据</button>
<button onclick="func2()">查看一个数据</button>
<script>
    function func1(){
        localStorage.setItem("name","yuan");
    }

    function func2(){
        var ret = localStorage.getItem("name");
        console.log(ret);
    }
</script>
</body>
</html>
```

> localStorage和sessionStorage的区别：
>
> 1、localStorage和sessionStorage一样都是用来存储客户端临时信息的对象。
>
> 2、他们均只能存储字符串类型的对象（虽然规范中可以存储其他原生类型的对象，但是目前为止没有浏览器对其进行实现）。
>
> 3、localStorage生命周期是永久，这意味着除非用户显示在浏览器提供的UI上清除localStorage信息，否则这些信息将永远存在。sessionStorage生命周期为当前窗口或标签页，一旦窗口或标签页被永久关闭了，那么所有通过sessionStorage存储的数据也就被清空了。
>
> 4、不同浏览器无法共享localStorage或sessionStorage中的信息。相同浏览器的不同页面间可以共享相同的 localStorage（页面属于相同域名和端口），但是不同页面或标签页间无法共享sessionStorage的信息。这里需要注意的是，页面及标 签页仅指顶级窗口，如果一个标签页包含多个iframe标签且他们属于同源页面，那么他们之间是可以共享sessionStorage的。

### 2、DOM对象(JS核心)

DOM  document Object Model 文档对象模型

```js
// 整个html文档,会保存一个文档对象document
// console.log( document ); // 获取当前文档的对象
```

#### 1、查找标签

##### 1 直接查找标签

```js
document.getElementsByTagName("标签名")
document.getElementById("id值")
document.getElementsByClassName("类名")
```

> 1、方法的返回值是dom对象还是数组
>
> 2、document对象可以是任意dom对象，将查询范围限制在当前dom对象

##### 2 导航查找标签

```js
elementNode.parentElement           // 父节点标签元素
elementNode.children                // 所有子标签
elementNode.firstElementChild       // 第一个子标签元素
elementNode.lastElementChild        // 最后一个子标签元素
elementNode.nextElementSibling     // 下一个兄弟标签元素
elementNode.previousElementSibling  // 上一个兄弟标签元素
```

##### 3 CSS选择器查找

```JS
document.querySelector("css选择器")  //根据css选择符来获取查找到的第一个元素，返回标签对象（dom对象）
document.querySelectorAll("css选择器"); // 根据css选择符来获取查找到的所有元素,返回数组
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>


<div id="i1">DIV1</div>

<div class="c1">DIV</div>
<div class="c1">DIV</div>
<div class="c1">DIV</div>


<div class="outer">
    <div class="c1">item</div>
</div>


<div class="c2">
    <div class="c3">
        <ul class="c4">
            <li class="c5" id="i2">111</li>
            <li>222</li>
            <li>333</li>
        </ul>
    </div>
</div>

<script>

   // 直接查找

   var ele = document.getElementById("i1");  // ele就是一个dom对象
   console.log(ele);

   var eles = document.getElementsByClassName("c1"); // eles是一个数组 [dom1,dom2,...]
   console.log(eles);

   var eles2 = document.getElementsByTagName("div"); // eles2是一个数组 [dom1,dom2,...]
   console.log(eles2);

   var outer = document.getElementsByClassName("outer")[0];
   var te = outer.getElementsByClassName("c1");
   console.log(te);

   // 导航查找

    var c5 = document.getElementsByClassName("c5")[0];
    console.log(c5);  // c5是一个DOM对象

    console.log(c5.parentElement.lastElementChild);  // 返回值是dom对象
    console.log(c5.parentElement.children);  // 返回值是dom对象数组
    console.log(c5.nextElementSibling.nextElementSibling);
    console.log(c5.parentElement.children);

    // css选择器

    var dom = document.querySelector(".c2 .c3 .c5");
    console.log(":::",dom);

    var doms = document.querySelectorAll("ul li");
    console.log(":::",doms);
    
</script>

</body>
</html>
```

#### 2、绑定事件

##### 1 静态绑定 ：直接把事件写在标签元素中。

```html
<div id="div" onclick="foo(this)">click</div>

<script>
    function foo(self){           // 形参不能是this;
        console.log("foo函数");
        console.log(self);   
    }
</script>


```

##### 2 动态绑定：在js中通过代码获取元素对象,然后给这个对象进行后续绑定。

```html
<p id="i1">试一试!</p>

<script>

    var ele=document.getElementById("i1");

    ele.onclick=function(){
        console.log("ok");
        console.log(this);    // this直接用
    };

</script>
```

> 一个元素本身可以绑定多个不同的事件, 但是如果多次绑定同一个事件,则后面的事件代码会覆盖前面的事件代码

##### 3 多个标签绑定事件

```html
<ul>
    <li>111</li>
    <li>222</li>
    <li>333</li>
    <li>444</li>
    <li>555</li>
</ul>


<script>

    var eles = document.querySelectorAll("ul li");
    for(var i=0;i<eles.length;i++){
        eles[i].onclick = function (){
            console.log(this.innerHTML)
            // console.log(eles[i].innerHTML)  // 结果？
        }
    }

</script>
```

#### 3、操作标签

```html
<标签名 属性1=“属性值1” 属性2=“属性值2”……>文本</标签名>
```

##### 1 文本操作

```html
<div class="c1"><span>click</span></div>

<script>

    var ele =document.querySelector(".c1");

    ele.onclick = function (){
        // 查看标签文本
        console.log(this.innerHTML)
        console.log(this.innerText)
    }

    ele.ondblclick = function (){
        // 设置标签文本
        this.innerHTML = "<a href='#'>yuan</a>"
        //this.innerText = "<a href='#'>yuan</a>"
    }

</script>
```

##### 2 value操作

像input标签，select标签以及textarea标签是没有文本的，但是显示内容由value属性决定

```html
    <input type="text" id="i1" value="yuan">                               
    <textarea name="" id="i2" cols="30" rows="10">123</textarea>
    <select  id="i3">
        <option value="hebei">河北省</option>
        <option value="hubei">湖北省</option>
        <option value="guangdong">广东省</option>
    </select>

<script>

    // input标签
    var ele1 =document.getElementById("i1");
    console.log(ele1.value);
    ele1.onmouseover = function (){                        // onmouseover鼠标悬浮事件
        this.value = "alvin"
    }

    // textarea标签
    var ele2 =document.getElementById("i2");
    console.log(ele2.value);
    ele2.onmouseover = function (){
        this.innerText = "welcome to JS world！"
        this.value = "welcome to JS world！"
    }
    // select标签
    var ele3 =document.getElementById("i3");
    console.log(ele3.value);
    ele3.value= "hubei"

</script>
```

##### 3 css样式操作

```html
<p id="i1">Hello world!</p>

<script>
    var ele = document.getElementById("i1");
    ele.onclick = function (){
        this.style.color = "red"
    }
</script>
```

##### 4 属性操作

```
elementNode.setAttribute("属性名","属性值")    
elementNode.getAttribute("属性名")       
elementNode.removeAttribute("属性名");
```

> 并不是所有属性都可以像value那样操作。

##### 5 class属性操作

可以设置多个class样式，然后通过事件触发增加样式或者减少样式

```js
elementNode.className()
elementNode.classList.add('a1')        //class属性值里面添加一个class的值。a1：添加的值
elementNode.classList.remove('a1')     //class属性值里面删除一个class的值。a1：添加的值
```

案例：tab切换

<img src="web.assets/image-20210303144706023.png" alt="image-20210303144706023" style="zoom:50%;" />

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        *{
            margin: 0;
            padding: 0;
        }

        .tab{
            width: 800px;
            height: 300px;
            /*border: 1px solid red;*/
            margin: 200px auto;
        }

        .tab ul{
            list-style: none;
        }

        .tab-title{
            background-color: #f7f7f7;
            border: 1px solid #eee;
            border-bottom: 1px solid #e4393c;
        }

        .tab .tab-title li{
            display: inline-block;
            padding: 10px 25px;
            font-size: 14px;
        }

        li.current {
            background-color: #e4393c;
            color: #fff;
            cursor: default;
        }

        .hide{
            display: none;
        }


    </style>
</head>
<body>


<div class="tab">
    <ul class="tab-title">
        <li class="current" index="0">商品介绍</li>
        <li class="" index="1">规格与包装</li>
        <li class="" index="2">售后保障</li>
        <li class="" index="3">商品评价</li>
    </ul>

    <ul class="tab-content">
        <li>商品介绍...</li>
        <li class="hide">规格与包装...</li>
        <li class="hide">售后保障...</li>
        <li class="hide">商品评价...</li>
    </ul>
</div>


<script>
     var titles = document.querySelectorAll(".tab-title li");
     var contents = document.querySelectorAll(".tab-content li");
     
     for (var i = 0;i<titles.length;i++){
         
         titles[i].onclick = function () {
             // (1) 触发事件标签拥有current样式
             for (var j = 0;j<titles.length;j++){
                 titles[j].classList.remove("current")
             }

             console.log(this);
             this.classList.add("current");

             // (2) 显示点击title对应的详情内容
             var index = this.getAttribute("index");
             // console.log(this.getAttribute("index"));
             // console.log(contents[index]);


             for (var z = 0;z<contents.length;z++){
                 contents[z].classList.add("hide");
             }

             contents[index].classList.remove("hide");
             
         }
         
     } 

</script>

</body>
</html>
```

##### 6 节点操作

```js
// 创建节点：
document.createElement("标签名")
// 插入节点
somenode.appendChild(newnode)             // 追加一个子节点（作为最后的子节点）
somenode.insertBefore(newnode,某个节点)   // 把增加的节点放到某个节点的前边
// 删除节点
somenode.removeChild()：获得要删除的元素，通过父元素调用删除
//替换节点
somenode.replaceChild(newnode, 某个节点);
```

案例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>


<button class="add_btn">添加节点</button>
<button class="del_btn">删除节点</button>
<button class="replace_btn">替换节点</button>
<div class="c1">
    <h3>hello JS!</h3>
    <h3 class="c2">hello world</h3>
</div>


<script>

    var add_btn = document.querySelector(".add_btn");
    var del_btn = document.querySelector(".del_btn");
    var replace_btn = document.querySelector(".replace_btn");

    var c1 = document.querySelector(".c1");
    var c2 = document.querySelector(".c2");
    
    add_btn.onclick = function () {
        // 创建节点

        var ele = document.createElement("img");  // <img>
        ele.src = "https://img2.baidu.com/it/u=1613029778,1507777131&fm=26&fmt=auto&gp=0.jpg"
        console.log(ele);


        // 添加节点
        // c1.appendChild(ele);

        c1.insertBefore(ele, c2)

    };


    del_btn.onclick = function () {
        // 删除子节点
        c1.removeChild(c2);
    };


    replace_btn.onclick = function () {

        // 创建替换节点

        var ele = document.createElement("img");  // <img>
        ele.src = "https://img2.baidu.com/it/u=1613029778,1507777131&fm=26&fmt=auto&gp=0.jpg"
        console.log(ele);

        // 替换节点
        c1.replaceChild(ele, c2);

    }
</script>

</body>
</html>
```

#### 4、常用事件

##### this调用的对象本身

```js
创建了标签，事件触发函数，并传入了一个对象本身当实参
<button onclick="del_tr(this)">删除</button>  
var del_tr = function (a){
    a.value;                 // 直接通形参调用button标签对象

}
```



##### 1 onload事件

保留事件，等页面加载完在执行函数内的代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>


    <script>
       window.onload = function (){
            ele = document.getElementById("i1")
            console.log(ele.innerHTML);
       }
    </script>
    
</head>
<body>

<div id="i1">yuan</div>

</body>
</html>
```

##### 2 onsubmit事件

提交事件，提交表单先执行函数内的代码做判断

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

</head>
<body>

<form action="" id="i1">
     用户名：<input type="text">
     密码：  <input type="password">
    <input type="submit">
</form>


<script>

     var ele = document.getElementById("i1");
     var user = document.querySelector("#i1 [type=text]")
     var pwd = document.querySelector("#i1 [type=password]")
     ele.onsubmit = function (e){
           console.log(user.value);
           console.log(pwd.value);
	
            return false;    // 终止事件执行
           // e.preventDefault() // 阻止元素默认行为
     }

</script>
</body>
</html>
```

##### 3 onchange事件

当文本内容发生变化时触发函数内代码，例如select标签下的省变化时做相应的操作

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

</head>
<body>

<select name="provonce" id="s1">
    <option value="hebei">请选择省份</option>
    <option value="hubei">湖北省</option>
    <option value="hunan">湖南省</option>
    <option value="hebei">河北省</option>
</select>

<select name="provonce" id="s2">
    <option value="hebei">请选择城市</option>

</select>

<script>

   var  data={"hunan":["长沙","岳阳","张家界"],"hubei":["武汉","襄阳","荆州"],"hebei":["石家庄","保定","张家口"]};
   console.log(data);
   var ele =  document.getElementById("s1");
   var ele2 =  document.getElementById("s2");
   ele.onchange=function () {
       console.log(this.value);
       var citys = data[this.value];
       console.log(citys);
       // 清空操作
       ele2.options.length=1;
       // 创建标签
       for (var i=0;i<citys.length;i++){
           var option =  document.createElement("option"); // </option></option>
           option.innerHTML=citys[i];
           ele2.appendChild(option)
       }
   }

</script>


</body>
</html>
```

##### 4 onmouse事件

onmouseover：鼠标悬浮到某对象内执行函数内操作

onmouseleave：鼠标离开某对象后执行函数内操作

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #container{
            width: 300px;
        }
        #title{
            cursor: pointer;
            background: #ccc;
        }
       #list{
           display: none;
           background:#fff;
       }

        #list div{
            line-height: 50px;
        }
        #list  .item1{
            background-color: green;
        }

         #list  .item2{
            background-color: rebeccapurple;
        }

         #list  .item3{
            background-color: lemonchiffon;
        }


    </style>
</head>
<body>
<div id="container">
        <div id="title">使用了mouseout事件↓</div>
        <div id="list">
                <div class="item1">第一行</div>
                <div class="item2">第二行</div>
                <div class="item3">第三行</div>
        </div>
</div>
<script>

// 1.不论鼠标指针离开被选元素还是任何子元素，都会触发 mouseout 事件。

// 2.只有在鼠标指针离开被选元素时，才会触发 mouseleave 事件。

   var container=document.getElementById("container");
   var title=document.getElementById("title");
   var list=document.getElementById("list");
   title.onmouseover=function(){
       list.style.display="block";
   };

   container.onmouseleave=function(){  // 改为onmouseout试一下
       list.style.display="none";
   };

/*

因为mouseout事件是会冒泡的，也就是onmouseout事件可能被同时绑定到了container的子元素title和list
上，所以鼠标移出每个子元素时也都会触发我们的list.style.display="none";

*/
</script>
</body>
</html>
```

##### 5 onkey事件

onkeydown：按下键盘执行事件

onkeyup：松开键盘执行



```html
<input type="text" id="t1"/>

<script type="text/javascript">

    var ele=document.getElementById("t1");

     ele.onkeydown=function(e){
        console.log("onkeydown",e.keycode)  // 获取用户键盘输入的字符号，是数字显示
    };

     ele.onkeyup=function(e){
        console.log("onkeyup",e.key)  // 获取用户输入的字符和数字
    };
</script>
```

##### 6 onblur和onfocus事件

onblur：获取用户进入到了输入框后执行事件

onfocus：用户离开输入框后执行事件

```html
<input type="text" class="c1">


<script>

    var ele = document.querySelector(".c1");

    // 获取焦点事件
    ele.onfocus = function () {
        console.log("in")
    };

    // 失去焦点事件
    ele.onblur = function () {
        console.log("out")
    }

</script>
```

##### 7 冒泡事件

指触发子标签事件时会触发父标签事件

```html
<div class="c1">
    <div class="c2"></div>
</div>


<script>

    var ele1 = document.querySelector(".c1");
    ele1.onclick = function () {
        alert("c1区域")
    };

    var ele2 = document.querySelector(".c2");
    ele2.onclick = function (event) {
        alert("c2区域");
        
        // 如何阻止事件冒泡
        event.stopPropagation();
    }

</script>
```











# 5 jQuery

### 1、jQuery介绍

* jQuery是什么

jQuery是一个快速、简洁的JavaScript框架，是继Prototype之后又一个优秀的JavaScript代码库（*或JavaScript框架*）。jQuery设计的宗旨是“write Less，Do More”，即倡导写更少的代码，做更多的事情。它封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML文档操作、事件处理、动画设计和Ajax交互。

jQuery的核心特性可以总结为：具有独特的链式语法和短小清晰的多功能接口；具有高效灵活的css选择器，并且可对CSS选择器进行扩展；拥有便捷的插件扩展机制和丰富的插件。jQuery兼容各种主流浏览器，如IE 6.0+、FF 1.5+、Safari 2.0+、Opera 9.0+等

* jQuery的版本

目前在市场上, 1.x , 2.x, 3.x 功能的完善在1.x, 2.x的时候是属于删除旧代码,去除对于旧的浏览器兼容代码。3.x的时候增加es的新特性以及调整核心代码的结构

jQuery的引入

根本上jquery就是一个写好的js文件,所以想要使用jQuery的语法必须先引入到本地

```html
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.js"></script>
```

* jQuery对象和dom对象的关系

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<!--    远程导入-->
    <!--    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.6.0/jquery.js"></script>-->
<!--本地导入-->
    <script src="jquery3.6.js"></script>

</head>
<body>

<ul class="c1">
    <li>123</li>
    <li>234</li>
    <li>345</li>
</ul>

<script>

       // $(".c1 li").css("color","red");
       console.log($(".c1 li"));   // dom集合对象  [dom1,dom2,...]

       // 如何将jQury对象转换为Dom对象
       console.log($(".c1 li")[1].innerHTML);

       // 如何将Dom对象转换为jQuery对象;
       var ele = document.querySelector(".c1 li");
       // console.log(ele);
       // ele.style.color = "red";
      $(ele).css("color","orange")  // [ele]

</script>
</body>
</html>
```

### 2、jQuery的选择器

#### 2.1、直接查找

##### 基本选择器 

```go
/*
#id         # id选择符 
element     # 元素选择符
.class      # claw43ss选择符  
selector1, selector2, selectorN   # 同时获取多个元素的选择符 
 
$("#id")   
$(".class")  
$("element")  
$(".class,p,div")
*/
```

##### 组合选择器  

```js
/*
  ancestor descendant  // 包含选择符 
  parent > child       // 父子选择符 
  prev + next          // 下一个兄弟选择符 
  prev ~ siblings      // 兄弟选择符 

$(".outer div")  
$(".outer>div")  
$(".outer+div")  
$(".outer~div")
*/
```

##### 属性选择器

```js
/*
[attribute=value]    // 获取拥有指定数据attribute,并且置为value的元素 
$('[type="checked"]')  
$('[class*="xxx"]')  
*/
```

##### 表单选择器

```js
/*
$("[type='text']")----->$(":text")         注意只适用于input标签  : $("input:checked")
同样适用表单的以下属性
:enabled
:disabled
:checked
:selected
*/
```

##### 筛选器

```js
/*

  // 筛选器
  :first               //  从已经获取的元素集合中提取第一个元素
  :even                //  从已经获取的元素集合中提取下标为偶数的元素 
  :odd                 //  从已经获取的元素集合中提取下标为奇数的元素
  :eq(index)           //  从已经获取的元素集合中提取指定下标index对应的元素
  :gt(index)           //  从已经获取的元素集合中提取下标大于index对应的元素
  :last                //  从已经获取的元素集合中提取最后一个元素
  :lt(index)           //  从已经获取的元素集合中提取下标小于index对应的元素
  :first-child         //  从已经获取的所有元素中提取他们的第一个子元素
  :last-child          //  从已经获取的所有元素中提取他们的最后一个子元素
  :nth-child           //  从已经获取的所有元素中提取他们的指定下标的子元素
  // 筛选器方法
  $().first()          //  从已经获取的元素集合中提取第一个元素
  $().last()           //  从已经获取的元素集合中提取最后一个元素
  $().eq()             //  从已经获取的元素集合中提取指定下标index对应的元素

  */
```

#### 2.2、导航查找

```js
/* 
// 查找子代标签：         
 $("div").children(".test")     
 $("div").find(".test")  
                               
 // 向下查找兄弟标签 
$(".test").next()               
$(".test").nextAll()     
$(".test").nextUntil() 
                           
// 向上查找兄弟标签  
$("div").prev()                  
$("div").prevAll()       
$("div").prevUntil() 

// 查找所有兄弟标签  
$("div").siblings()  
              
// 查找父标签：         
$(".test").parent()              
$(".test").parents()     
$(".test").parentUntil() 

*/
```

### 3、jQuery的绑定事件

```js
/*
三种用法:
  1. on 和 off
  	 // 绑定事件
  	 $().on("事件名",匿名函数)
  	 
  	 // 解绑事件,给指定元素解除事件的绑定
  	 $().off("事件名")
  
  2. 直接通过事件名来进行调用
  	 $().事件名(匿名函数)
  	
  3. 组合事件,模拟事件
  	 $().ready(匿名函数)   // 入口函数
  	 $().hover(mouseover, mouseout)   // 是onmouseover和 onmouseout的组合
  	 $().trigger(事件名)  // 用于让js自动触发指定元素身上已经绑定的事件
  	 
*/
```

`mouseover` ：jquery鼠标悬浮时执函数

```js
$(".num li").mouseover(function () {
   
})
```

```js
$(".num li").mouseover(function () {
    i = $(this).index();
    $(".outer .img li").eq(i).stop().fadeIn(100).siblings().stop().fadeOut(1000);
    $(".outer .num li").eq(i).addClass("c1").siblings().removeClass("c1");

})
```



案例1：绑定取消事件

```html
<p>限制每次一个按钮只能投票3次</p>
<button id="zan">点下赞(<span>10</span>)</button>
<script>
    let zan = 0;
    $("#zan").click(function(){
        $("#zan span").text(function(){
            zan++;
            let ret = parseInt($(this).text())+1;
            if(zan >= 3){
                $("#zan").off("click"); // 事件解绑
            }
            return ret;
        });
    })

</script>
```

案例2：模拟事件触发

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="js/jquery-1.11.0.js"></script>
    <style>
    input[type=file]{
        display: none;
    }
    .upload{
        width: 180px;
        height: 44px;
        border-radius: 5px;
        color: #fff;
        text-align: center;
        line-height: 44px;
        background-color: #000000;
        border: none;
        outline: none;
        cursor: pointer;
    }
    </style>
</head>
<body>
    <input type="file" name="avatar">
    <button class="upload">上传文件</button>
    <script>
    $(".upload").on("click", function(){
       $("input[type=file]").trigger("click"); // 模拟事件的触发
    });
    </script>
</body>
</html>
```

### 4、jQuery的操作标签

#### 1 文本操作

```js
/*
$("选择符").html()     // 读取指定元素的内容,如果$()函数获取了有多个元素,则提取第一个元素
$("选择符").html(内容) // 修改内容,如果$()函数获取了多个元素, 则批量修改内容

$("选择符").text()     // 效果同上,但是获取的内容是纯文本,不包含html代码
$("选择符").text(内容)  // 效果同上,但是修改的内容中如果有html文本,在直接转成实体字符,而不是html代码
*/
```

#### 2 value操作

```
$().val()
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script src="jquery3.6.js"></script>
    <script>

    $(function () {


        $("#i1").blur(function () {

            // 获取jquery对象的value属性值
            console.log(this.value);
            console.log($(this).val());

            // 设置value属性值
            $(this).val("hello world")

        });
        

        $("#i3").change(function () {
            console.log(this.value);
            console.log($(this).val());

            $(this).val("guangdong");

        });

        console.log($("#i2").val());
        console.log($("#i2").val("hello pig!"))

    })

    </script>
</head>
<body>


<input type="text" id="i1">

<select  id="i3">
    <option value="hebei">河北省</option>
    <option value="hubei">湖北省</option>
    <option value="guangdong">广东省</option>
</select>

<p> <textarea name="" id="i2" cols="30" rows="10">123</textarea></p>



</body>
</html>
```

#### 3 属性操作

```java
/*
//读取属性值
	$("选择符").attr("属性名");   // 获取非表单元素的属性值,只会提取第一个元素的属性值
	$("选择符").prop("属性名");   // 表单元素的属性,只会提取第一个元素的属性值

//操作属性
  $("选择符").attr("属性名","属性值");  // 修改非表单元素的属性值,如果元素有多个,则全部修改
  $("选择符").prop("属性名","属性值");  // 修改表单元素的属性值,如果元素有多个,则全部修改
  
  $("选择符").attr({'属性名1':'属性值1','属性名2':'属性值2',.....})
  $("选择符").prop({'属性名1':'属性值1','属性名2':'属性值2',.....})
*/
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script src="jquery3.6.js"></script>
   
</head>
<body>

<button class="select_all">全选</button>
<button class="cancel">取消</button>
<button class="reverse">反选</button>
<hr>
<table border="1">
    <tr>
        <td>选择</td>
        <td>姓名</td>
        <td>年龄</td>
    </tr>
    
    <tr>
        <td><input type="checkbox"></td>
        <td>张三</td>
        <td>23</td>
    </tr>
    <tr>
        <td><input type="checkbox"></td>
        <td>李四</td>
        <td>23</td>
    </tr>
    <tr>
        <td><input type="checkbox"></td>
        <td>王五</td>
        <td>23</td>
    </tr>
</table>

<script>
    
    $(".select_all").click(function () {
        $("table input:checkbox").prop("checked",true);

    });
    $(".cancel").click(function () {
       $("table input:checkbox").prop("checked",false);
    });

    $(".reverse").click(function () {
       $("table input:checkbox").each(function () {
           $(this).prop("checked",!$(this).prop("checked"))

       })

   });

</script>

</body>
</html>
```

#### 4 css样式操作

```js
/*
获取样式
$().css("样式属性");   // 获取元素的指定样式属性的值,如果有多个元素,只得到第一个元素的值

操作样式
$().css("样式属性","样式值").css("样式属性","样式值");
$().css({"样式属性1":"样式值1","样式属性2":"样式值2",....})

$().css("样式属性":function(){
  
  // 其他代码操作 
  return "样式值";
});
*/
```

#### 5 class 属性操作

```js
$().addClass("class1  class2 ... ...")   // 给获取到的所有元素添加指定class样式
$().removeClass() // 给获取到的所有元素删除指定class样式
$().toggleClass() // 给获取到的所有元素进行判断,如果拥有指定class样式的则删除,如果没有指定样式则添加
```

tab切换案例jQuery版本：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>

        *{
            margin: 0;
            padding: 0;
        }

        .tab{
            width: 800px;
            height: 300px;
            /*border: 1px solid rebeccapurple;*/
            margin: 200px auto;
        }

        .tab ul{
            list-style: none;
        }

        .tab ul li{
            display: inline-block;
        }

        .tab_title {
            background-color: #f7f7f7;
            border: 1px solid #eee;
            border-bottom: 1px solid #e4393c;
        }

        .tab .tab_title li{
            padding: 10px 25px;
            font-size: 14px;
        }

        .tab .tab_title li.current{
            background-color: #e4393c;
            color: #fff;
            cursor: default;
        }

        .tab_con li.hide{
            display: none;
        }

    </style>

    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.js"></script>
</head>
<body>

<div class="tab">
    <ul class="tab_title">
        <li class="current">商品介绍</li>
        <li>规格与包装</li>
        <li>售后保障</li>
        <li>商品评论</li>
    </ul>

    <ul class="tab_con">
        <li>商品介绍...</li>
        <li class="hide">规格与包装...</li>
        <li class="hide">售后保障...</li>
        <li class="hide">商品评论...</li>
    </ul>
</div>

<script>


    // jQuery

    $(".tab_title li").click(function (){
           // current样式
           $(this).addClass("current").siblings().removeClass('current');
           // hide样式
           $(".tab_con li").eq($(this).index()).removeClass("hide").siblings().addClass("hide")
    })

</script>

</body>
</html>
```

#### 6 节点操作

```js
/*
//创建一个jquery标签对象
    $("<p>")

//内部插入

    $("").append(content|fn)      // $("p").append("<b>Hello</b>");
    $("").appendTo(content)       // $("p").appendTo("div");
    $("").prepend(content|fn)     // $("p").prepend("<b>Hello</b>");
    $("").prependTo(content)      // $("p").prependTo("#foo");

//外部插入

    $("").after(content|fn)       // ("p").after("<b>Hello</b>");
    $("").before(content|fn)      // $("p").before("<b>Hello</b>");
    $("").insertAfter(content)    // $("p").insertAfter("#foo");
    $("").insertBefore(content)   // $("p").insertBefore("#foo");

//替换
    $("").replaceWith(content|fn) // $("p").replaceWith("<b>Paragraph. </b>");

//删除

    $("").empty()
    $("").remove([expr])

//复制
    $("").clone([Even[,deepEven]])
*/
```

案例1：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="jquery3.6.js"></script>
</head>
<body>


<button class="add_btn">添加节点</button>
<button class="del_btn">删除节点</button>
<button class="replace_btn">替换节点</button>
<div class="c1">
    <h3>hello JS!</h3>
    <h3 class="c2">hello world</h3>

</div>


<script>
     
    $(".add_btn").click(function () {
        // 创建jquery对象

        // var $img = $("<img>");
        // $img.attr("src","https://img1.baidu.com/it/u=3210260546,3888404253&fm=26&fmt=auto&gp=0.jpg")

        // 节点添加

        // $(".c1").append($img);
        // $img.appendTo(".c1")

        // $(".c1").prepend($img);
        // $(".c2").before($img);
        // 支持字符串操作
        $(".c1").append("<img src ='https://img1.baidu.com/it/u=3210260546,3888404253&fm=26&fmt=auto&gp=0.jpg'>")


    });


    $(".del_btn").click(function () {

          $(".c2").remove();
          // $(".c2").empty();

    });


    $(".replace_btn").click(function () {
        // alert(123);
        // var $img = $("<img>");
        // $img.attr("src","https://img1.baidu.com/it/u=3210260546,3888404253&fm=26&fmt=auto&gp=0.jpg")
        // $(".c2").replaceWith($img);
        $(".c2").replaceWith("<img src ='https://img1.baidu.com/it/u=3210260546,3888404253&fm=26&fmt=auto&gp=0.jpg'>");

    })
    
</script>

</body>
</html>
```

案例2：clone案例

```html
<div class="outer">
    <div class="item">
        <input type="button" value="+" class="add">
        <input type="text">
    </div>

</div>

<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.js"></script>
<script>

   $(".add").click(function () {

       var $clone=$(this).parent().clone()
       $clone.children(".add").attr({"value":"-","class":"rem"})
       $(".outer").append($clone);
   });

    $('.rem').click(function () {
        $(this).parent().remove()
    });

    // 事件委派
    $(".outer").on("click",".item .rem",function () {
        $(this).parent().remove()
    })


</script>
```

#### 7 css尺寸

```js
/*
$("").height([val|fn])
$("").width([val|fn])
$("").innerHeight()
$("").innerWidth()
$("").outerHeight([soptions])
$("").outerWidth([options])
*/
```

#### 8 css位置

```js
/*
$("").offset([coordinates])  // 获取匹配元素在当前视口的相对偏移。
$("").position()             // 获取匹配元素相对父元素的偏移，position()函数无法用于设置操作。
$("").scrollTop([val])       // 获取匹配元素相对滚动条顶部的偏移。
*/
```

案例1：返回顶部

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
        }
        .content{
            height: 2000px;
            background-color: lightgray;
        }

        .return_top{
            width: 120px;
            height: 50px;
            background-color: lightseagreen;
            color: white;
            text-align: center;
            line-height: 50px;

            position: fixed;
            bottom: 20px;
            right: 20px;
        }

        .hide{
            display: none;
        }
    </style>

    <script src="jquery3.6.js"></script>
</head>
<body>


<div class="content">
    <h3>文章...</h3>
</div>

<div class="return_top hide">返回顶部</div>


<script>

    console.log($(window).scrollTop());
    $(".return_top").click(function () {

        $(window).scrollTop(0)
        
    });

    $(window).scroll(function () {
        console.log($(this).scrollTop());
        var v =$(this).scrollTop();
        if (v > 100){
            $(".return_top").removeClass("hide");
        }else {
            $(".return_top").addClass("hide");
        }

    })
</script>


</body>
</html>
```

案例2：位置偏移

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box{
            width: 200px;
            height: 200px;
            background-color: orange;

        }

        .parent_box{
             width: 800px;
             height: 500px;
             margin: 200px auto;
             border: 1px solid rebeccapurple;
        }
    </style>
</head>
<body>

<button class="btn1">offset</button>
<div class="parent_box">
    <div class="box"></div>
</div>


<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.js"></script>
<script>

    var $offset=$(".box").offset();
    var $left=$offset.left;
    var $top=$offset.top;

    console.log("$offset","top:"+$top+" left:"+$left)

    var $position=$(".box").position();
    var $left=$position.left;
    var $top=$position.top;

    console.log("$position","top:"+$top+" left:"+$left);


    $(".btn1").click(function () {
        $(".box").offset({left:50,top:50})
    });


</script>


</body>
</html>
```

### 5、jQuery的动画

#### 5.1、基本方法

```js
/*
//基本
	show([s,[e],[fn]])   显示元素
        hide([s,[e],[fn]])   隐藏元素

//滑动
	slideDown([s],[e],[fn])  向下滑动 
	slideUp([s,[e],[fn]])    向上滑动

//淡入淡出
	fadeIn([s],[e],[fn])     淡入
	fadeOut([s],[e],[fn])    淡出
	fadeTo([[s],opacity,[e],[fn]])  让元素的透明度调整到指定数值

//自定义
	animate(p,[s],[e],[fn])   自定义动画 
	stop([c],[j])             暂停上一个动画效果,开始当前触发的动画效果
	
*/
```

案例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>


        .c1{
            width: 250px;
            height: 250px;
            background-color: black;
        }

        .hide{
            display: none;
        }
    </style>

    <script src="jquery3.6.js"></script>
</head>
<body>


<p>
    <button class="show01">显示</button>
    <button class="hide01">隐藏</button>
</p>
<p>
    <button class="show02">显示</button>
    <button class="hide02">隐藏</button>
</p>
<p>
    <button class="show03">显示</button>
    <button class="hide03">隐藏</button>
</p>

<p>
    <button class="show04">显示</button>
    <button class="hide04">隐藏</button>
</p>
<hr>

<div class="c1"></div>


<script>
    // 自己实现的隐藏与显示

    $(".show01").click(function () {
        $(".c1").removeClass("hide")
    });
    $(".hide01").click(function () {
        $(".c1").addClass("hide")
    });

    // (1) show与hide方法

    $(".show02").click(function () {

        $(".c1").show(1000,function () {
            alert("显示成功")
        });

    });
    $(".hide02").click(function () {

        $(".c1").hide(1000,function () {
            alert("隐藏成功")
        })

    });

     // (2) slideDown与slideUp

     $(".show03").click(function () {

        $(".c1").slideDown(1000,function () {
            alert("显示成功")
        });

     });
     $(".hide03").click(function () {

        $(".c1").slideUp(1000,function () {
            alert("隐藏成功")
        })

    });

      // (3) fadeIn与fadeOut

     $(".show04").click(function () {

        $(".c1").fadeIn(1000,function () {
            alert("显示成功")
        });

     });
     $(".hide04").click(function () {

        $(".c1").fadeOut(1000,function () {
            alert("隐藏成功")
        })

    });
</script>

</body>
</html>
```

#### 5.2、自定义动画

```js
$(".box").animate(动画最终效果,动画完成的时间,动画完成以后的回调函数)
```

```js
 $(".animate").click(function () {

        $(".c1").animate({
            "border-radius":"50%",
            "top":340,
            "left":200
        },1000,function () {
            $(".c1").animate({
                "border-radius":"0",
                "top":240,
                "left":120
            },1000,function () {

                $(".animate").trigger("click")
            })
        })
        
    })

```

### 6、扩展方法 (插件机制)

* jQuery.extend(object)

```html
扩展jQuery对象本身。

用来在jQuery命名空间上增加新函数。 

在jQuery命名空间上增加两个函数:


<script>
    jQuery.extend({
      min: function(a, b) { return a < b ? a : b; },
      max: function(a, b) { return a > b ? a : b; }
});

    jQuery.min(2,3); // => 2
    jQuery.max(4,5); // => 5
</script>

```

* jQuery.fn.extend(object)

```html
扩展 jQuery 元素集来提供新的方法（通常用来制作插件）

增加两个插件方法：

<body>

<input type="checkbox">
<input type="checkbox">
<input type="checkbox">

<script src="jquery.min.js"></script>
<script>
    jQuery.fn.extend({
      check: function() {
         $(this).attr("checked",true);
      },
      uncheck: function() {
         $(this).attr("checked",false);
      }
    });

    $(":checkbox").check()
</script>

</body>
```







# 6 ES6语言

基于javascrip提高开发效率的语言

### 1  Let和Const 声明

```
const定义常量（实际指的是变量和的内存地址），不可变只能在其声明或定义的代码块内有效
注：若区块中存在let或者const命令，则这个区块对这些变量和常量在一开始就行成封闭作用域，只要在声明之前使用就会报错（可能会出现暂时性死区）
不能重复声明，否则报错
建议：在默认情况下用const,而只有在你知道变量值需要被修改的情况使用let
```

**let：**1 声明变量，没有变量提升

```javascript
var a;
console.log(a); 				//打印为空
a = 2;
// -----------------------------对比
console.log(a); 			//会报错    初始化前无法访问“a”
let a = 10;
console.log(b);
```

2.是一个块作用域

```javascript
if(1===1){
   let b = 10;
 }
console.log(b);        // 报错  b 未定义
```

3.不能重复声明

```javascript
let a = 1;
let a = 3;
console.log(a);    // 报错 标识符“a”已被声明
```



**const  **：1 声明常量  一旦被声明 无法修改

```javascript
 //作用1： for循环是个经典例子
        const arr = [];

        for (let i = 0; i < 10; i++) {
            arr[i] = function() {
                return i;
            }
        }
        console.log(arr[5]()); //5
```

作用2:不会污染全局变量



### 2  模板字符串格式化

```javascript
  <script>
        // 模板字符串：使用tab键上面的反引号``,插入变量时使用${变量名}
        const oBox = document.querySelector('.box');
        let id = 1,name = '小马哥';

        let htmlStr = `<ul>
            <li>
                <p id=${id}>${name}</p>
            </li>
        </ul>`;

        oBox.innerHTML = htmlStr;
    </script>
```



### 3 函数

#### 1 参数默认值设置

```javascript
// es5的写法
function add(a, b) {
a = a || 10;
b = b || 20;
return a + b;
}
// es6
console.log(add());
function add(a, b = 20) {
return a + b;
}
console.log(add(30));

// 默认的表达式也可以是一个函数
function add(a, b = getVal(5)) {
return a + b;
}

function getVal(val) {
return val + 5;
}
console.log(add(10));
```



####  2 剩余参数运算符 ...

放在形参中，由三个点...自定参数名如： `...keys`,相当python的`args`，可以把实参多个参数打包成数组

```javascript
函数(...arr){
    arr = [10, 20, 50, 30, 90, 100, 40];
}	

执行函数(10, 20, 50, 30, 90, 100, 40)
```

```javascript
        function pick(obj, ...keys) {
            // ...keys 解决了arguments 的问题
            let result = Object.create(null);               // 1 声明一个空对象
            for (let i = 0; i < keys.length; i++) {         // 2循环
                result[keys[i]] = obj[keys[i]]              // 封装新对象返回
            }
            return result;
        }

        let book = {
            title: 'es6的教程',
            author: '小马哥',
            year: 2019
        }

        let bookData = pick(book, 'year', 'author');
        console.log(bookData);                  //   结果 {"year": 2019, "author": "小马哥"}
```

#### 3.扩展参数运算符 ...

将一个数组分割，并将各个项作为分离的参数传给函数,与剩余相反

```javascript
const arr = [10, 20, 50, 30, 90, 100, 40];
console.log(Math.max(...arr));
```



#### 4 箭头函数  =>

用来定义函数，用=>来定义  `function(){}`  等于与   `()=>{}`

```javascript
// 使用示例
//旧
let add = function (a, b) { return a + b } 
//新
let add = (a, b) => {return a + b }			
let add = (val1, val2) => val1 + val2;						// 直接返回时不用加{}
let fn = ()=> 'hello world' + 123;						  // 无参数时
let getObj = id => { return { id: id, name:'小马哥'}}		// 一个参数时
let getObj = id => ({id:id,name:"小马哥"});			   // 一个参数时

let fn = (											 // 闭包
    () => {
        return () => {console.log('hello es6 2');}
    }
         )();
fn();
```



5  `=>` 的`this`指向

**this：是指在对象内的当前对象**

**箭头函数没有this指向，箭头函数内部this值只能通过查找作用域链来确定,一旦使用箭头函数，当前就不存在作用域链**

 **使用箭头函数的注意事项：**

```
1:使用箭头函数 函数内部没有arguments
2.箭头函数不能使用new关键字来实例化对象
因为function函数 也是一个对象，但是箭头函数不是一个对象，它其实就是一个语法糖 表达式
```

```javascript
如多层函数时，使用function的函数时this就指向此function的同级作为作用域。使用=>的函数时会穿过此层一直向上
```

```javascript
 let PageHandle = {
            id: 123,
            init: function () {
                document.addEventListener('click', (event) => {
                    console.log(this);                          // this.doSomeThings 不是函数
                    this.doSomeThings(event.type);             // 使用=>后 作用域会往上找到function调用者的作用域
                }, false)
            },
            doSomeThings: function (type) {
                console.log(`事件类型:${type},当前id:${this.id}`);
            }
        }
        PageHandle.init();
```









# 7 vue.js

## 1 vue的使用

基于vue.js框架来编写项目需要以下几个步骤：

### 1 导入vue.js包（CDN）

```html
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>

<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>

# 当然，也可以将文件下载下来再通过本地导入。
```

### 2 应用

在script标签中new一个Vue对象，这个对象`el`的值就用在指定区域标签的id中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- 1.引入vue.js文件 -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>

<!-- 2.指定区域，该区域的内容希望由vue.js来接管。 -->
<div id="app">
    <h1>欢迎学习Vue.js</h1>
    <div>我叫{{name}}，微信{{wechat}}</div>
    
    <input type="button" value="点我" v-on:click="clickMe">
</div>


<script>
	// 3.创建Vue对象，并关联指定HTML区域。
    var app = new Vue({
        el: '#app',
        data: {
            name: '武沛齐',
            wechat: 'wupeiqi888'
        },
        methods: {
            clickMe: function () {
                // 获取值this.name
                // 修改值this.name = "xx"
                this.name = "alex";
                this.wechat = "wupeiqi666";
            }
        }
    })
</script>
</body>
</html>
```

### 3 Vue对象说明

**el:'自定id名，在标签id属性中使用此名就代表使用'**

 **data :{变量键:变量值}**

 **methods: {变量函数名：`function () {函数}`    }**

**components：{组件，组件名:组件}**









## 2.vue常见指令

### 2.1 插值表达式 （文本）

**说明：****用`{{}}`号就可在其中调用变量，{{}}内可作数字与字符串相加及其它，另可用表达式**

一般在显示文本内容的标签中使用。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <div>我叫{{name}}，我喜欢{{hobby}}，邮箱:{{dataInfo.email}}</div>
    <ul>
        <li>{{'李杰'}}</li>
        <li>{{'李杰' + "土鳖"}}</li>
        <li>{{ base + 1 + 1 }}</li>
        <li>{{ 1===1 ?"李杰":"alex"}}</li>
    </ul>
    <ul>
        <li>{{ condition?"李杰":"alex"}}</li>
    </ul>
    <input type="button" value="点我" v-on:click="clickMe">
</div>


<script>
    var app = new Vue({
        el: '#app',
        data: {
            name: '武沛齐',
            hobby: '篮球',
            dataInfo: {
                id: 1,
                email: "xxx.com"
            },
            condition: false,
            base: 1
        },
        methods: {
            clickMe: function () {
                this.name = "苑日天";
                this.condition = true;
                this.dataInfo.email = "wupeiqi@live.com";
                this.base += 100;
            }
        }
    })
</script>
</body>
</html>
```





### 2.2 v-bind指令（单向，属性）

**使用说明：一般用于对标签中的属性进行操作。v-bind:属性="值变量"，例：**

```html
<!--imageUrl,cls 是变量-->
<img alt="" v-bind:src="imageUrl" v-bind:class="cls">
```



**注意：v-bind属于单向绑定（ JS修改->HTML修改 )，js内容修改了页面会修改，页面修改并不影响js内数据。**

**可简写，简写的格式:`:属性名=xxx`，**例如：

```html
<h1 v-bind:class="v1"></h1>
<h1 :class="v1"></h1>
<img :src="xx" />
```

1 **常规使用在调用变量当属性值**

2   **调用变量中的true flase 来判断使用的属性值   `v-bind:class="{属性值1:变量，属性值2:变量}"`**

**3 属性值中调用变量中的对象，对象内键是属性值，值是true,flase**

**4 属性值可用数组类似于列表[变量1，变量2]，调用多个变量中的属性值**

**5 在数组中不可使用三元表达式**

**6 属性style也可用花括号动态使用属性值** `<h3 v-bind:style="{ color:变量,fontSize:变量+'px'}">222</h3>`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- 导入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <style>
        .ig {
            border: 2px solid red;
        }

        .info {
            color: red;
        }

        .danger {
            font-size: 10px;
        }
    </style>
</head>
<body>
<div id="app">
    <img src='xx.png' class='c1'/>
	<!-- 1 -->
    <img alt="" v-bind:src="imageUrl" v-bind:class="cls">
	<!-- 2 -->
    <h1 v-bind:class="{info:v1,danger:v2}">你好呀111</h1>
    <!--3-->
    <h1 v-bind:class="clsDict">你好呀</h1>
	<!--4-->
    <h2 v-bind:class="[a1,a2]"></h2>
    <!--5-->
    <h2 v-bind:class="[1===1?a1:'y',a2]">111</h2>
	<!--6-->
    <h3 v-bind:style="{ color:clr,fontSize:size+'px'}">222</h3>
    <h3 style="color: red;font-size: 19px">333</h3>

    <input type="button" value="点我" v-on:click="clickMe">
</div>


<script>
    var app = new Vue({
        el: '#app',
        data: {
            imageUrl: 'https://hcdn2.luffycity.com/media/frontend/public_class/PY1@2x_1566529821.1110113.png',
            cls: "ig",
            v1: true,
            v2: true,
            clsDict: {
                info: false,
                danger: false
            },
            a1: "info",
            a2: "danger",
            clr: "red",
            size: "19",
        },
        methods:{
            clickMe:function () {
                this.v1 = false;
            }
        }
    })
</script>
</body>
</html>
```



### 2.3 v-model指令(双向，交互)

**一般用于在交互的表中中使用，例如：input、select、textarea等。【双向绑定】**

**1 在input标签中 使用 v-model="变量"，在变量中默认为空，输入值后变量同步修改**

**2 在提交键中可添加点击函数   `<input type="button" value="注 册" v-on:click="函数变量"/>` **

**3 变量如果是对象（类似字典）可以用  `对象.键`  调用**

```html
<!DOCTYPE html> 
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <div>
        <!-- 1-->
        用户名：<input type="text" v-model="user">
    </div>
    <div>
        密码：<input type="password" v-model="pwd">
    </div>
    <div>
        性别：
        <input type="radio" v-model="sex" value="1">男
        <input type="radio" v-model="sex" value="2">女
    </div>
    <div>
        爱好：
        <input type="checkbox" v-model="hobby" value="11">篮球
        <input type="checkbox" v-model="hobby" value="22">足球
        <input type="checkbox" v-model="hobby" value="33">评判求
    </div>
    <div>
        城市：
        <select v-model="city">
            <option value="sh">上海</option>
            <option value="bj">北京</option>
            <option value="sz">深圳</option>
        </select>
    </div>
    <div>
        擅长领域：
        <select v-model="company" multiple>
            <option value="11">技术</option>
            <option value="22">销售</option>
            <option value="33">运营</option>
        </select>
    </div>
    <div>
        其他：<textarea v-model="more"></textarea>
    </div>
	  <!-- 2 -->
    <input type="button" value="注 册" v-on:click="clickMe"/>
</div>


<script>
    var app = new Vue({
        el: '#app',
        data: {
            user: "",
            pwd: "",
            sex: "2",
            hobby: ["22"],
            city: "sz",
            company: ["22", "33"],
            more: '...'
        },
        methods: {
            clickMe: function () {
                console.log(this.user, this.pwd, this.sex, this.hobby, this.city, this.company, this.more);
            },
        }
    })
</script>
</body>
</html>



```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <div>
        <!--3-->
        用户名：<input type="text" v-model="info.user">
    </div>
    <div>
        密码：<input type="password" v-model="info.pwd">
    </div>
    <div>
        性别：
        <input type="radio" v-model="info.sex" value="1">男
        <input type="radio" v-model="info.sex" value="2">女
    </div>
    <div>
        爱好：
        <input type="checkbox" v-model="info.hobby" value="11">篮球
        <input type="checkbox" v-model="info.hobby" value="22">足球
        <input type="checkbox" v-model="info.hobby" value="33">评判求
    </div>
    <div>
        城市：
        <select v-model="info.city">
            <option value="sh">上海</option>
            <option value="bj">北京</option>
            <option value="sz">深圳</option>
        </select>
    </div>
    <div>
        擅长领域：
        <select v-model="info.company" multiple>
            <option value="11">技术</option>
            <option value="22">销售</option>
            <option value="33">运营</option>
        </select>
    </div>
    <div>
        其他：<textarea v-model="info.more"></textarea>
    </div>

    <input type="button" value="注 册" v-on:click="clickMe"/>
</div>


<script>
    var app = new Vue({
        el: '#app',
        data: {
            info: {
                user: "",
                pwd: "",
                sex: "2",
                hobby: ["22"],
                city: "sz",
                company: ["22", "33"],
                more: '...'
            }
        },
        methods: {
            clickMe: function () {
                console.log(this.info);
            },
        }
    })
</script>
</body>
</html>
```





### 2.4 v-for指令（循环标签）

用户数据进行循环并展示。

#### 示例1：循环数组

```html
<div id="app">
    <ul>
        <li v-for="item in dataList">{{ item }}</li>
    </ul>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            dataList: ["郭德纲", "于谦", "三哥"],
        }
    })
</script>
```



#### 示例2：循环数组与序号

 第一个值，第二个序号

```html
<div id="app">
    <ul>
        <li v-for="(item,idx) in dataList">{{idx}} - {{ item }}</li>
    </ul>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            dataList: ["郭德纲", "于谦", "三哥"],
        }
    })
</script>
```



#### 示例3：循环对象值键 

第一个值，第二个键

```html
<div id="app">
    <ul>
        <li v-for="(value,key) in dataDict">{{key}} - {{ value }}</li>
    </ul>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            dataDict: {
                id: 1,
                age: 18,
                name: "xxx"
            }
        }
    })
</script>
```



#### 示例4：循环数组中的对象

```html
<div id="app">
    <ul>
        <li v-for="(item,idx) in cityList">{{item.id}} - {{ item.text }}</li>
    </ul>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            cityList: [
                {id: 11, text: "上海"},
                {id: 12, text: "北京"},
                {id: 13, text: "深圳"},
            ]
        }
    })
</script>
```



#### 示例5：嵌套循环

```
<ul>
	<li> <span>id 11</span>  <span>text 上海</span> </li>
	。。
	。。
</ul>
```



```html
<div id="app">
    <ul>
        <li v-for="(item,idx) in cityList">
        	<span v-for="(v,k) in item">{{k}} {{v}}</span>
        </li>
    </ul>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            cityList: [
                {id: 11, text: "上海"},
                {id: 12, text: "北京"},
                {id: 13, text: "深圳"},
            ]
        }
    })
</script>
```





### 2.5 v-on指令（事件）

**注意：事件可以简写为 `<div @click="函数变量">点击</div>`事件触发后调用函数执行**

#### 1 事件相关的指令：

```python
v-on:click		# 点击
v-on:dblclick    # 双击
v-on:mouseover，  # 鼠标进入
v-on:mouseout，	# 鼠标移出
v-on:change      # 更改了
v-on:focus

```

#### 示例1

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <ul>
        <li v-on:click="clickMe">点击</li>
        <li @click="clickMe">点击</li>
        <li v-on:dblclick="doSomething('双击')">双击</li>
        <li v-on:mouseover="doSomething('进入')" v-on:mouseout="doSomething('离开')">进入&离开</li>
    </ul>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {},
        methods: {
            clickMe: function () {
                alert("点击了")
            },
            doSomething: function (msg) {
                console.log(msg);
            }
        }
    })
</script>
</body>
</html>
```



#### 示例2：数据管理

数据的管理包括对数据：展示、动态添加、删除、修改。

##### 数据列表展示

使用了标签循环

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <style>
        .penal {
            border: 1px solid #dddddd;
            margin: 20px 0 0 0;
            padding: 10px;
            border-bottom: 0;
            background-color: #d9d9d9;
        }

        .table {
            width: 100%;
            border-collapse: collapse;
            border-spacing: 0;
        }

        .table > tbody > tr > td, .table > tbody > tr > th, .table > tfoot > tr > td, .table > tfoot > tr > th, .table > thead > tr > td, .table > thead > tr > th {
            padding: 8px;
            vertical-align: top;
            border: 1px solid #ddd;
            text-align: left;
        }
    </style>
</head>
<body>

<div id="app">
    <h3 class="penal">数据列表</h3>
    <table class="table">
        <thead>
        <tr>
            <td>姓名</td>
            <td>年龄</td>
        </tr>
        </thead>
        <tbody>
        <tr v-for="item in dataList">
            <td>{{item.name}}</td>
            <td>{{item.age}}</td>
        </tr>
        </tbody>
    </table>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            dataList: [
                {"name": "武沛齐", "age": 19},
                {"name": "alex", "age": 89},
            ]
        }
    })
</script>
</body>
</html>
```

##### 数据添加

**1 用户点击执行函数把用户输入的值获取到一个对象中，在把对象添加到表单数组中**

**`要添加处.push(要添加的值)`:添加的方法**

```javascript
addUser: function () {
                let row = {name: this.user, age: this.age};
                this.dataList.push(row);
                this.user = "";
                this.age = ""
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <style>
        .penal {
            border: 1px solid #dddddd;
            margin: 20px 0 0 0;
            padding: 10px;
            border-bottom: 0;
            background-color: #d9d9d9;
        }

        .table {
            width: 100%;
            border-collapse: collapse;
            border-spacing: 0;
        }

        .table > tbody > tr > td, .table > tbody > tr > th, .table > tfoot > tr > td, .table > tfoot > tr > th, .table > thead > tr > td, .table > thead > tr > th {
            padding: 8px;
            vertical-align: top;
            border: 1px solid #ddd;
            text-align: left;
        }
    </style>
</head>
<body>

<div id="app">
    <h3 class="penal">表单区域</h3>
    <div>
        <div>
            <label>姓名</label>
            <input type="text" v-model="user">
        </div>
        <div>
            <label>年龄</label>
            <input type="text" v-model="age">
            <input type="button" value="新建" @click="addUser">
        </div>
    </div>

    <h3 class="penal">数据列表</h3>
    <table class="table">
        <thead>
        <tr>
            <td>姓名</td>
            <td>年龄</td>
        </tr>
        </thead>
        <tbody>
        <tr v-for="item in dataList">
            <td>{{item.name}}</td>
            <td>{{item.age}}</td>
        </tr>
        </tbody>
    </table>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            user: "",
            age: "",
            dataList: [
                {name: "武沛齐", age: 19},
                {name: "alex", age: 89},
            ]
        },
        methods: {
            addUser: function () {
                let row = {name: this.user, age: this.age};
                this.dataList.push(row);
                this.user = "";
                this.age = "";
            }
        }
    })
</script>
</body>
</html>
```

##### 删除数据

**`this.dataList.splice(idx, 1);`：splice删除方法，第一值是要删除的序号，第二个是删除几个**

**函数的参数可以在事件调用函数中传入**

**还有种方法，函数内默认有个`event`，值传入方法如下`"deleteRow"`：调用函数，传值方法 `data-自定变量名="值"`，**

**另变量要加上`v-bind:data-idx="值"`，不然传入的就是字符串，`v-bind`可简化成`：`**

```html
<tr v-for="(item,idx) in dataList">
	<td>{{item.name}}</td>
	<td>{{item.age}}</td>
     <td>
         <input type="button" value="删除" @click="deleteRow" :data-idx="idx"/>  <!--传入idx变量-->
      </td>
```

函数内

```javascript
deleteRow: function (event) {
                // 根据索引删除dataList中的值
                let idx = event.target.dataset.idx;    // 调用变量
                this.dataList.splice(idx, 1);
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <style>
        .penal {
            border: 1px solid #dddddd;
            margin: 20px 0 0 0;
            padding: 10px;
            border-bottom: 0;
            background-color: #d9d9d9;
        }

        .table {
            width: 100%;
            border-collapse: collapse;
            border-spacing: 0;
        }

        .table > tbody > tr > td, .table > tbody > tr > th, .table > tfoot > tr > td, .table > tfoot > tr > th, .table > thead > tr > td, .table > thead > tr > th {
            padding: 8px;
            vertical-align: top;
            border: 1px solid #ddd;
            text-align: left;
        }
    </style>
</head>
<body>

<div id="app">
    <h3 class="penal">表单区域</h3>
    <div>
        <div>
            <label>姓名</label>
            <input type="text" v-model="user">
        </div>
        <div>
            <label>年龄</label>
            <input type="text" v-model="age">
            <input type="button" value="新建" @click="addUser">
        </div>
    </div>

    <h3 class="penal">数据列表</h3>
    <table class="table">
        <thead>
        <tr>
            <td>姓名</td>
            <td>年龄</td>
            <td>操作</td>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(item,idx) in dataList">
            <td>{{item.name}}</td>
            <td>{{item.age}}</td>
            <td>
                <input type="button" value="删除" @click="deleteRow" :data-idx="idx"/>
            </td>
        </tr>
        </tbody>
    </table>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            user: "",
            age: "",
            dataList: [
                {name: "武沛齐", age: 19},
                {name: "alex", age: 89},
            ]
        },
        methods: {
            addUser: function () {
                let row = {name: this.user, age: this.age};
                this.dataList.push(row);
                this.user = "";
                this.age = "";
            },
            deleteRow: function (event) {
                // 根据索引删除dataList中的值
                let idx = event.target.dataset.idx;
                this.dataList.splice(idx, 1);
            }
        }
    })
</script>
</body>
</html>

```

##### 编辑修改数据

**修改函数：点击表单时执行函数传入当前数据序号，在函数内获取到数据并赋值输入框内，序号则赋值给一个变量在添加中调用**

**添加函数：添加函数中先判断有没有传入序号值，有就执行修改，空就执行添加。在结尾要把框内值清空，并把提交键换回默认添加**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <style>
        .penal {
            border: 1px solid #dddddd;
            margin: 20px 0 0 0;
            padding: 10px;
            border-bottom: 0;
            background-color: #d9d9d9;
        }

        .table {
            width: 100%;
            border-collapse: collapse;
            border-spacing: 0;
        }

        .table > tbody > tr > td, .table > tbody > tr > th, .table > tfoot > tr > td, .table > tfoot > tr > th, .table > thead > tr > td, .table > thead > tr > th {
            padding: 8px;
            vertical-align: top;
            border: 1px solid #ddd;
            text-align: left;
        }
    </style>
</head>
<body>

<div id="app">
    <h3 class="penal">表单区域</h3>
    <div>
        <div>
            <label>姓名</label>
            <input type="text" v-model="user">
        </div>
        <div>
            <label>年龄</label>
            <input type="text" v-model="age">
            <input type="button" :value="title" @click="addUser">
        </div>
    </div>

    <h3 class="penal">数据列表</h3>
    <table class="table">
        <thead>
        <tr>
            <td>姓名</td>
            <td>年龄</td>
            <td>操作</td>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(item,idx) in dataList">
            <td>{{item.name}}</td>
            <td>{{item.age}}</td>
            <td>
                <input type="button" value="删除" @click="deleteRow" :data-idx="idx"/>
                <input type="button" value="编辑" @click="editRow" :data-idx="idx"/>
            </td>
        </tr>
        </tbody>
    </table>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            editIndex: undefined,
            title: "新建",
            user: "",
            age: "",
            dataList: [
                {name: "武沛齐", age: 19},
                {name: "alex", age: 89},
            ]
        },
        methods: {
            addUser: function () {
                if (this.editIndex) {
                    // 修改
                    this.dataList[this.editIndex].name = this.user;
                    this.dataList[this.editIndex].age = this.age;
                } else {
                    let row = {name: this.user, age: this.age};
                    this.dataList.push(row);
                }
                this.user = "";
                this.age = "";
                this.editIndex = undefined;
                this.title = "新建";
            },
            deleteRow: function (event) {
                // 根据索引删除dataList中的值
                let idx = event.target.dataset.idx;
                this.dataList.splice(idx, 1);
            },
            editRow: function (event) {
                let idx = event.target.dataset.idx;
                // let name = this.dataList[idx].name;
                // let age = this.dataList[idx].age;
                // let {id, name} = {id: 1, name: "武沛齐"};
                // console.log(id, name);
                let {name, age} = this.dataList[idx];
                this.user = name;
                this.age = age;
                this.title = "编辑";
                this.editIndex = idx;
            }
        }
    })
</script>
</body>
</html>
```



### 2.6 v-if指令（条件判断 ）

**1 在标签中 `v-if="变量"`为true时此标签才会显示**

**2 在标签中 `v-if="变量==="xxx"`可作判断**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <!--1-->
    <a v-if="isLogin">{{user}}</a>
    <a v-else>登录</a>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            isLogin: false,
            user: "武沛齐"
        }
    })
</script>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1 v-if="v1">阿里无人区</h1>

    
    <h1 v-if="v2">去西藏</h1>
    <h1 v-else>去新疆</h1>

    <!--2-->
    <div v-if="v3 === '北京'">
        <h1>天安门</h1>
    </div>
    <div v-else-if="v3 === '新疆'">
        <h1>乌鲁木齐</h1>
    </div>
    <div v-else-if="v3 ==='西藏'">
        <h1>拉萨</h1>
    </div>
    <div v-else>
        <h1>大理</h1>
    </div>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            v1: true,
            v2: true,
            v3: "新疆"
        }
    })
</script>
</body>
</html>
```



### 2.7 v-show指令 （条件判断）

**根据条件显示或隐藏（标签都会渲染到页面）。**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1 v-show="v1">可可西里</h1>
    <h1 v-show="!v1">罗布泊</h1>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            v1: false,
        }
    })
</script>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <style>
        label {
            width: 60px;
            display: inline-block;
            text-align: right;
            margin-right: 8px;
        }
    </style>
</head>
<body>
<div id="app">
    <input type="button" value="密码登录" @click="isSms=false"/>
    <input type="button" value="短信登录" @click="isSms=true"/>
    
    <div v-show="isSms">
        <p>
            <label>手机号</label>
            <input type="text" placeholder="手机号">
        </p>
        <p>
            <label>验证码</label>
            <input type="text" placeholder="验证码">
        </p>
    </div>
    <div v-show="!isSms">
        <p>
            <label>用户名</label>
            <input type="text" placeholder="用户名">
        </p>
        <p>
            <label>密码</label>
            <input type="password" placeholder="密码">
        </p>
    </div>

</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            isSms: false,
        }
    })
</script>
</body>
</html>
```









### 2.8 axios  （网络请求）

**axios，他是一个HTTP 库，可以发送Http请求。**

1 要引用 `<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`

2  `method:请求`，`params:参数`，`data:请求体`，`headers:请求头`

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
    axios({
        method: "post",
        url: 'https://api.luf...ord/login/',
        params: {
			v1:123,
            v2:456
        },
        data: {
            name:"武沛齐",
            pwd:"123"
        },
        headers: {
            "Content-Type": "application/json"
        }
    }).then(function (res) {
        console.log(res.data);
    }).catch(function (error) {
		console.log(error);
    })
</script>
```







### 案例：用户登录

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--1 引用vue及axios-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <style>
        label {
            width: 60px;
            display: inline-block;
            text-align: right;
            margin-right: 8px;
        }
    </style>
</head>
<body>
<div id="app">
    <!--2 点击密码短信登陆进行变量修改-->
    <input type="button" value="密码登录" @click="isSms=false"/>
    <input type="button" value="短信登录" @click="isSms=true"/>
	<!--3.1 判断是否显示界面-->
    <div v-show="isSms">
        <p>
            <label>手机号</label>
            <input type="text" placeholder="手机号" v-model="sms.mobile">
        </p>
        <p>
            <label>验证码</label>
            <input type="text" placeholder="验证码" v-model="sms.code">
        </p>
    </div>
    <div v-show="!isSms">
        <p>
            <label>用户名</label>
            <input type="text" placeholder="用户名" v-model="info.username">
        </p>
        <p>
            <label>密码</label>
            <input type="password" placeholder="密码" v-model="info.password">
        </p>
    </div>

    <input type="button" value="登 录" @click="loginForm"/>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            isSms: false,
            info: {
                username: "",
                password: "",
            },
            sms: {
                mobile: "",
                code: ""
            }
        },
        methods: {
            loginForm: function () {
                // 1.获取用户输入的值
                let dataDict = this.isSms ? this.sms : this.info;

                let url;
                // 2 判断用户选的什么创建对应url
                if (this.isSms) {
                    url = "https://api.luffycity.com/api/v1/auth/mobile/login/?loginWay=mobile";
                } else {
                    url = "https://api.luffycity.com/api/v1/auth/password/login/?loginWay=password";
                }

                // 3.想某个地址发送网络请求 axios
                // https://api.luffycity.com/api/v1/auth/password/login/?loginWay=password
                // {"username":"alex123","password":"999"}

                // https://api.luffycity.com/api/v1/auth/mobile/login/?loginWay=mobile
                // {"mobile":"18630087660","code":"123123"}
                axios({
                    method: "post",
                    url: url,
                    data: dataDict,
                    headers: {
                        "Content-Type": "application/json"
                    }
                }).then(function (res) {       // 4 发送请求后获取返回数据，判断数据是否成功
                    if (res.data.code === -1) {
                        alert(res.data.msg);
                        return;
                    }
                    // 5 登录成功后跳转
                    window.location.href = "https://www.luffycity.com"
                }).catch(function (error) {
                    alert("请求异常，请重新操作。")  // 6 异常显示异常
                })
            }
        }
    })
</script>
</body>
</html>
```







## 3 组件开发

在开发过程中，我们可以将页面中 某一部分 的功能编写成一个组件，然后再在页面上进行引用。

- 有利于划分功能模块的开发（HTML、CSS、JavaScript等相关代码都集成到组件中）。
- 有利于重用

### 3.1 局部组件（要挂载）

**局部组件创建后要放在在vue的 components内**

```javascript
1 创建一个组件 
const Demo{
	data ：创建一个函数，return出数据
	template：`此处html标签，此处内调用变量只能在此data内调用 `
	methods:{函数名:函数}
}
2 在vue的 components内放入组件名
3 在html中使用组件名的标签
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1>=======当前页面=======</h1>
    {{name}}

    <h1>=======引入子组件=======</h1>
    <Demo></Demo>
    <Demo></Demo>
    <Bb></Bb>
    <Bb></Bb>
    <hr/>
    <Bb></Bb>
</div>
<script>
    //创建子组件
    const Demo = {
        data:function() {
            return {
                msg: '哈哈哈哈哈'
            }
        },
        template: `
            <div>
                <h1>{{msg}}</h1>
                <input type="text" v-model="msg"/>
                <input type="button" @click="showMeg" value="点我呀">
            </div>
        `,
        methods: {
            showMeg: function () {
                alert(this.msg);
            }
        }
    }

    //创建子组件
    const Bili = {
        // 组件中的data是一个方法，并返回值（与Vue对象创建不同）
        data:function() {
            return {
                dataList: [
                    {"id": 1, "title": "路飞学城倒闭了"},
                    {"id": 2, "title": "老板和保洁阿姨跑了"},
                ]
            }
        },
        template: `
            <div>
                <h1>数据列表</h1>
                <table border="1">
                    <thead>
                    <tr>
                        <th>ID</th>
                        <th>标题</th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr v-for="item in dataList">
                        <td>{{item.id}}</td>
                        <td>{{item.title}}</td>
                    </tr>
                    </tbody>
                </table>
            </div>
        `
    }

    var app = new Vue({
        el: '#app',
        data: {
            name: "武沛齐",
        },
        components: {
            Demo,
            Bb: Bili
        },
        methods: {}
    })
</script>
</body>
</html>

```



### 3.2 全局组件（创建就可用）

**全局组件创建后直接就能调用**

**创建方法**

```javascript
Vue.component('组件名', {
    data:返回函数,
    template:`界面展示的html`
    
})
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1>=======当前页面=======</h1>
    {{name}}

    <h1>=======引入子组件=======</h1>
    <Demo></Demo>
    <Demo></Demo>
    <Bili></Bili>
    <Bili></Bili>
</div>
<script>
    //创建子组件
    Vue.component('Demo', {
        data: function () {
            return {
                msg: '哈哈哈哈哈'
            }
        },
        template: `
            <div>
                <h1>{{msg}}</h1>
                <input type="text" v-model="msg"/>
                <input type="button" @click="showMeg" value="点我呀">
            </div>
        `,
        methods: {
            showMeg: function () {
                alert(this.msg);
            }
        }
    });

    //创建子组件
    Vue.component('Bili', {
        // 组件中的data是一个方法，并返回值（与Vue对象创建不同）
        data: function () {
            return {
                dataList: [
                    {"id": 1, "title": "路飞学城倒闭了"},
                    {"id": 2, "title": "老板和保洁阿姨跑了"},
                ]
            }
        },
        template: `
            <div>
                <h1>数据列表</h1>
                <table border="1">
                    <thead>
                    <tr>
                        <th>ID</th>
                        <th>标题</th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr v-for="item in dataList">
                        <td>{{item.id}}</td>
                        <td>{{item.title}}</td>
                    </tr>
                    </tbody>
                </table>
            </div>
        `
    });

    var app = new Vue({
        el: '#app',
        data: {
            name: "武沛齐",
        },
        methods: {}
    })
</script>
</body>
</html>
```







## 4.vue-router组件

vue + **vue-router**组件 可以实现 SPA（single Page Application），即：**单页面应用**。

单页面应用，简而言之就是项目只有一个页面。

一个页面如何呈现多种界面的效果呢？

- 基于vue开发多个组件，例如：活动组件、课程组件、咨询组件
- 在页面上 vue-router 用来管理这些组件，用户点击某个按钮，就显示特定的组件（数据基于Ajax获取）。

### 4.0 组件和属性（待添加）

### 4.1 下载和引用

官方地址：https://router.vuejs.org/zh/

下载地址：https://unpkg.com/vue-router@4

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <!--  vue-router.js 依赖 vue.js -->
    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
    
</head>
<body>
	...
</body>
</html>
```

注意：后期用脚手架开发时，可以直接使用npm下载和引用。



### 4.2 快速上手

#### 案例：路飞学城（第1版）

![image-20220124174657691](web前端.assets/image-20220124174657691-6441034.png)

`created：`此函数在触发当前组件时会第一个触发，所以用来发送请求，拿到数据后赋值给`data：{}`

`mounted:`此函数要dom对象生成后才调用，执行会慢点

使用顺序（个人感觉）：

1.  创建组件   
2.  `new` 一个 `VueRouter`对象作路径与组件的对应关系 
3.  在页面中使用router对象名作标签，属性to=路径，点击对应标签便调用对应组件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .container {
            width: 1100px;
            margin: 0 auto;
        }

        .menu {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .menu a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }

        .course-list {
            display: flex;
            flex-wrap: wrap;
            justify-content: flex-start;
        }

        .course-list .item {
            width: 248px;
            padding: 10px;
            border: 1px solid #dddddd;
            margin-right: 5px;
            margin-top: 10px;
        }

        .course-list .item img {
            width: 100%;
            height: 120px;
        }
    </style>

    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
    <script src="axios.min.js"></script>
</head>
<body>
<div id="app">
    <div class="menu">
        <div class="container">
            <router-link to="/">路飞学城</router-link>
            <router-link to="/home">首页</router-link>
            <router-link to="/course">课程</router-link>
            <router-link to="/news">资讯</router-link>
        </div>
    </div>
    <div class="container">
        <router-view></router-view>
    </div>

</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用路飞学城"
            }
        },
        template: `<h2>{{title}}</h2>`
    }
    const Course = {
        data: function () {
            return {
                courseList: []
            }
        },
        created: function () {
            /* 组件创建完成之后自动触发【此时组件的对象已创建，但还未将页面先关的DOM创建并显示在页面上】
                 - 可以去操作组件对象，例如：this.courseList = [11,22,33]
                 - 不可以去操作DOM，例如：document.getElementById （未创建）
             */
            axios({
                method: "get",
                url: 'https://api.luffycity.com/api/v1/course/actual/?limit=5&offset=0',
                headers: {
                    "Content-Type": "application/json"
                }
            }).then((res) => {
                this.courseList = res.data.data.result;
            })

        },
        mounted: function () {
            /* DOM对象已在页面上生成，此时就可以 */
        },
        template: `
            <div class="course-list">
                <div class="item" v-for="item in courseList">
                    <img :src="item.cover" alt="">
                    <a>{{item.name}}</a>
                </div>
            </div>`
    }
    const News = {
        data: function () {
            return {
                dataList: []
            }
        },
        created: function () {
            /* 组件创建完成之后自动触发【此时组件的对象已创建，但还未将页面先关的DOM创建并显示在页面上】
                 - 可以去操作组件对象，例如：this.courseList = [11,22,33]
                 - 不可以去操作DOM，例如：document.getElementById （未创建）
             */
            axios({
                method: "get",
                url: 'https://api.luffycity.com/api/v1/course/actual/?limit=5&offset=10',
                headers: {
                    "Content-Type": "application/json"
                }
            }).then((res) => {
                this.dataList = res.data.data.result;
            })

        },
        template: `<ul><li v-for="item in dataList">{{item.name}}</li></ul>`
    }

    const router = new VueRouter({
        routes: [
            {path: '/', component: Home},
            {path: '/home', component: Home},
            {path: '/course', component: Course},
            {path: '/news', component: News}
        ],
        //mode: 'history'
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```



















### 4.3 路由和传值

当某个组件可以根据某些参数值的不同，展示不同效果时，需要用到动态路由。

例如：访问网站看到课程列表，点击某个课程，就可以跳转到课程详细页面（根据课程ID不同展示不同数据）。



#### 1 定义路由

1. `path:`路径，`:id`是动态传入的值
2. `component:`组件名
3. `name:`别名，代指路径

```javascript
const router = new VueRouter({
    routes: [
        { path: '/', component: Home},
        { path: '/course', component: Course, name: "Course"}
        { path: '/detail/:id', component: Detail, name: "Detail"}
    ],
})
```

####  2 HTML展示

**说明：**

1. 要想动态就要在标签属性`to="/xxx"`改成`v-bind:to`简写 `:to={path=xxx}`
2. 路径可用name别名
3. `params:{id:3}` 的值代表的是路径`xx/id`在路径/后面的值
4. `query:{size:19,page:2}`代表的是路径？号后面的参数

```html
<div>
    <!--1 固定的路径-->
    <router-link to="/">首页</router-link>
    <router-link to="/course">课程</router-link>
    <!--1.1 固定的路径 固定传值-->
    <router-link to="/detail/123">课程</router-link>
    
    <!--2 动态的路径 获取到路由中的变量-->
    <router-link :to="{path:'/course'}">课程</router-link>
    <!--2.1动态的路径 固定参数-->
    <router-link :to="{path:'/course?size=19&page=2'}">课程</router-link>
    <!--2.2 动态的路径 动态参数-->
    <router-link :to="{path:'/course', query:{size:19,page:2}">课程</router-link>
    
    <!--3 路径也可用name别名-->
    <router-link :to="{name:'Course'}">课程</router-link>
    <router-link :to="{name:'Course', query:{size:19,page:2} }">课程</router-link>

    <router-link :to="{path:'/detail/22',query:{size:123}}">Linux</router-link>
    <!--4 动态的路径 动态的传值 动态的参数-->
    <router-link :to="{name:'Detail',params:{id:3}, query:{size:29}}">网络安全</router-link>
</div>

<h1>内容区域</h1>
<router-view></router-view>
```

#### 3 组件获取URL传值和GET参数

1. `this.$route.params`  获取路径/后面的值，此方法固定的
2. `this.$route.query ` 获取路径？号后面的参数，此方法固定的

```javascript
 const Detail = {
     data: function () {
         return {
             title: "详细页面",
             paramDict: null,
             queryDict: null,

         }
     },
     created: function () {
         // 获取到html路径中的值
         this.paramDict = this.$route.params;
         this.queryDict = this.$route.query;
         // 发送axios请求
     },
     template: `<div><h2>{{title}}</h2><div>当前请求的数据 {{paramDict}}  {{queryDict}}</div></div>`
 }
```





#### 案例：路飞学城（第2版）

点击课程，查看课程详细页面。

>执行流程说明
>
>1 创建组件，new 一个VueRouter对象进行路径对应组件，使用route对象名创建标签如 
>
>`<router-link to="/course">课程</router-link>`，属性to对应路径，点击标签会调用组件，先执行组件内`created:`的函数
>
>然后把组件的`template:`中的html渲染到页面`<router-view></router-view>`的标签内
>
>标签内循环数据生成页面，然后把页面中每个`to=`新的组件url，传入动态的参数到url中，在调用下一个组件时就能对不同参数展示不同的数据
>
>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .container {
            width: 1100px;
            margin: 0 auto;
        }

        .menu {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .menu a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }

        .course-list {
            display: flex;
            flex-wrap: wrap;
            justify-content: flex-start;
        }

        .course-list .item {
            width: 248px;
            padding: 10px;
            border: 1px solid #dddddd;
            margin-right: 5px;
            margin-top: 10px;
        }

        .course-list .item img {
            width: 100%;
            height: 120px;
        }
    </style>

    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
    <script src="axios.min.js"></script>
</head>
<body>
<div id="app">
    <div class="menu">
        <div class="container">
            <router-link to="/">路飞学城</router-link>
            <router-link to="/home">首页</router-link>
            <router-link to="/course">课程</router-link>
            <router-link to="/news">资讯</router-link>
        </div>
    </div>
    <div class="container">
         <router-view></router-view>
    </div>

</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用路飞学城"
            }
        },
        template: `<h2>{{title}}</h2>`
    }
    const Course = {
        data: function () {
            return {
                courseList: []
            }
        },
        created: function () {
            /* 组件创建完成之后自动触发【此时组件的对象已创建，但还未将页面先关的DOM创建并显示在页面上】
                 - 可以去操作组件对象，例如：this.courseList = [11,22,33]
                 - 不可以去操作DOM，例如：document.getElementById （未创建）
             */
            axios({
                method: "get",
                url: 'https://api.luffycity.com/api/v1/course/actual/?limit=5&offset=0',
                headers: {
                    "Content-Type": "application/json"
                }
            }).then((res) => {
                this.courseList = res.data.data.result;
            })

        },
        mounted: function () {
            /* DOM对象已在页面上生成，此时就可以 */
        },
        template: `
            <div class="course-list">

                <div class="item" v-for="item in courseList">
                    <router-link :to="{name:'Detail',params:{id:item.id}}">
                        <img :src="item.cover" alt="">
                        <a>{{item.name}}</a>
                     </router-link>
                </div>

            </div>`
    }
    const News = {
        data: function () {
            return {
                dataList: []
            }
        },
        created: function () {
            /* 组件创建完成之后自动触发【此时组件的对象已创建，但还未将页面先关的DOM创建并显示在页面上】
                 - 可以去操作组件对象，例如：this.courseList = [11,22,33]
                 - 不可以去操作DOM，例如：document.getElementById （未创建）
             */
            axios({
                method: "get",
                url: 'https://api.luffycity.com/api/v1/course/actual/?limit=5&offset=10',
                headers: {
                    "Content-Type": "application/json"
                }
            }).then((res) => {
                this.dataList = res.data.data.result;
            })

        },
        template: `<ul><li v-for="item in dataList">{{item.name}}</li></ul>`
    }

    const Detail = {
        data: function () {
            return {
                title: "详细页面",
                courseId: null
            }
        },
        created: function () {
            this.courseId = this.$route.params.id;
            // 此处可以根据课程ID，发送ajax请求获取课程详细信息
        },
        template: `<div><h2>课程详细页面</h2><div>当前课程ID为：{{courseId}}</div></div>`
    }

    const router = new VueRouter({
        routes: [
            {path: '/', component: Home},
            {path: '/home', component: Home},
            {path: '/course', component: Course},
            {path: '/news', component: News},
            {path: '/detail/:id', component: Detail, name: 'Detail'}
        ],
        //mode: 'history'
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```







### 4.5 无法刷新

上述编写案例是没有问题，但如果在开发中会涉及到 同一个路由的跳转（默认不会重新加载页面，数据无法获取）。

例如：在详细页面再出现一个课程推荐，即：在课程详细，点击推荐的课程后跳转到课程详细页面（课程ID不同），此时课程的ID还是原来加载的ID，无法获取推荐课程的ID。

**如何解决呢？**

在课程详细的组件中设置watch属性即可，watch会监测`$route` 值，一旦发生变化，就执行相应的函数。

```javascript
const Detail = {
    data: function () {
        return {
            title: "详细页面",
            courseId: null,

        }
    },
    created: function () {
        this.courseId = this.$route.params.id;
        this.getCourseDetail();
    },
    watch: {
        $route:function(to, from) {  		 // to参数代指变化的route，from参数代指未变化
            this.courseId = to.params.id;
            // this.getCourseDetail();
        }
    },
    methods: {
        getCourseDetail: function () {
            // 根据this.courseId获取课程详细信息
        }
    },
    template: `<div><h2>{{title}}</h2><div>当前请求的数据 {{paramDict}}  {{queryDict}}</div></div>`
}
```



#### 案例：路飞学城（第3版）

> 在详细页面实现推荐课程

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .container {
            width: 1100px;
            margin: 0 auto;
        }

        .menu {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .menu a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }

        .course-list {
            display: flex;
            flex-wrap: wrap;
            justify-content: flex-start;
        }

        .course-list .item {
            width: 248px;
            padding: 10px;
            border: 1px solid #dddddd;
            margin-right: 5px;
            margin-top: 10px;
        }

        .course-list .item img {
            width: 100%;
            height: 120px;
        }
    </style>

    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
    <script src="axios.min.js"></script>
</head>
<body>
<div id="app">
    <div class="menu">
        <div class="container">
            <router-link to="/">路飞学城</router-link>
            <router-link to="/home">首页</router-link>
            <router-link to="/course">课程</router-link>
            <router-link to="/news">资讯</router-link>
        </div>
    </div>
    <div class="container">
        <router-view></router-view>
    </div>

</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用路飞学城"
            }
        },
        template: `<h2>{{title}}</h2>`
    }
    const Course = {
        data: function () {
            return {
                courseList: []
            }
        },
        created: function () {
            /* 组件创建完成之后自动触发【此时组件的对象已创建，但还未将页面先关的DOM创建并显示在页面上】
                 - 可以去操作组件对象，例如：this.courseList = [11,22,33]
                 - 不可以去操作DOM，例如：document.getElementById （未创建）
             */
            axios({
                method: "get",
                url: 'https://api.luffycity.com/api/v1/course/actual/?limit=5&offset=10',
                headers: {
                    "Content-Type": "application/json"
                }
            }).then((res) => {
                this.courseList = res.data.data.result;
            })

        },
        mounted: function () {
            /* DOM对象已在页面上生成，此时就可以 */
        },
        template: `
            <div class="course-list">

                <div class="item" v-for="item in courseList">
                    <router-link :to="{name:'Detail',params:{id:item.id}}">
                        <img :src="item.cover" alt="">
                        <a>{{item.name}}</a>
                     </router-link>
                </div>

            </div>`
    }
    const News = {
        data: function () {
            return {
                dataList: []
            }
        },
        created: function () {
            /* 组件创建完成之后自动触发【此时组件的对象已创建，但还未将页面先关的DOM创建并显示在页面上】
                 - 可以去操作组件对象，例如：this.courseList = [11,22,33]
                 - 不可以去操作DOM，例如：document.getElementById （未创建）
             */
            axios({
                method: "get",
                url: 'https://api.luffycity.com/api/v1/course/actual/?limit=5&offset=10',
                headers: {
                    "Content-Type": "application/json"
                }
            }).then((res) => {
                this.dataList = res.data.data.result;
            })

        },
        template: `<ul><li v-for="item in dataList">{{item.name}}</li></ul>`
    }

    const Detail = {
        data: function () {
            return {
                title: "详细页面",
                courseId: null,
                hotCourseList: [
                    {id: 1000, title: "python全栈开发"},
                    {id: 2000, title: "异步编程"},
                ],
            }
        },
        created: function () {
            this.courseId = this.$route.params.id;
            // 此处可以根据课程ID，发送ajax请求获取课程详细信息
            this.getCourseDetail();
        },
        watch: {
            $route: function (to, from) {
                this.courseId = to.params.id;
                this.getCourseDetail();
            }
        },
        methods: {
            getCourseDetail: function () {
                // 根据this.courseId获取课程详细信息
            }
        },
        template: `
                <div>
                    <h2>课程详细页面</h2>
                    <div>当前课程ID为：{{courseId}}</div>
                    <h3>课程推荐</h3>
                    <ul>
                        <li v-for="item in hotCourseList">
                            <router-link :to="{name:'Detail', params:{id:item.id}}">{{item.title}}</router-link>
                        </li>
                    </ul>
                </div>`
    }

    const router = new VueRouter({
        routes: [
            {path: '/', component: Home},
            {path: '/home', component: Home},
            {path: '/course', component: Course},
            {path: '/news', component: News},
            {path: '/detail:id', component: Detail, name: 'Detail'}
        ],
        //mode: 'history'
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```



### 4.6 路由嵌套

![image-20220124210012187](E:/LBF/笔记/课件（vue+drf+业务）/第2部分：vue/assets/image-20220124210012187-6447697.png)

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/pins/',
      component: Pins,
      children: [
        {
          // 当 /pins/hot 匹配成功，
          // Hot组件 会被渲染在 Pins 的 <router-view> 中
          path: 'hot',
          component: Hot
        },
        {
          // 当 /pins/following 匹配成功，
          // Following组件 会被渲染在 Pins 的 <router-view> 中
          path: 'following',
          component: Following
        }
      ]
    }
  ]
})
```



#### 案例：路飞学城（第4版）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .container {
            width: 1100px;
            margin: 0 auto;
        }

        .menu {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .menu a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }

        .course-list {
            display: flex;
            flex-wrap: wrap;
            justify-content: flex-start;
        }

        .course-list .item {
            width: 248px;
            padding: 10px;
            border: 1px solid #dddddd;
            margin-right: 5px;
            margin-top: 10px;
        }

        .course-list .item img {
            width: 100%;
            height: 120px;
        }
    </style>

    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
    <script src="axios.min.js"></script>
</head>
<body>
<div id="app">
    <div class="menu">
        <div class="container">
            <router-link to="/">路飞学城</router-link>
            <router-link to="/pins">沸点</router-link>
            <router-link to="/home">首页</router-link>
            <router-link to="/course">课程</router-link>
            <router-link to="/news">资讯</router-link>
        </div>
    </div>
    <div class="container">
        <router-view></router-view>
    </div>

</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用路飞学城"
            }
        },
        template: `<h2>{{title}}</h2>`
    }
    const Course = {
        data: function () {
            return {
                courseList: []
            }
        },
        created: function () {
            /* 组件创建完成之后自动触发【此时组件的对象已创建，但还未将页面先关的DOM创建并显示在页面上】
                 - 可以去操作组件对象，例如：this.courseList = [11,22,33]
                 - 不可以去操作DOM，例如：document.getElementById （未创建）
             */
            axios({
                method: "get",
                url: 'https://api.luffycity.com/api/v1/course/actual/?limit=5&offset=0',
                headers: {
                    "Content-Type": "application/json"
                }
            }).then((res) => {
                this.courseList = res.data.data.result;
            })

        },
        mounted: function () {
            /* DOM对象已在页面上生成，此时就可以 */
        },
        template: `
            <div class="course-list">

                <div class="item" v-for="item in courseList">
                    <router-link :to="{name:'Detail',params:{id:item.id}}">
                        <img :src="item.cover" alt="">
                        <a>{{item.name}}</a>
                     </router-link>
                </div>

            </div>`
    }
    const News = {
        data: function () {
            return {
                dataList: []
            }
        },
        created: function () {
            /* 组件创建完成之后自动触发【此时组件的对象已创建，但还未将页面先关的DOM创建并显示在页面上】
                 - 可以去操作组件对象，例如：this.courseList = [11,22,33]
                 - 不可以去操作DOM，例如：document.getElementById （未创建）
             */
            axios({
                method: "get",
                url: 'https://api.luffycity.com/api/v1/course/actual/?limit=5&offset=10',
                headers: {
                    "Content-Type": "application/json"
                }
            }).then((res) => {
                this.dataList = res.data.data.result;
            })

        },
        template: `<ul><li v-for="item in dataList">{{item.name}}</li></ul>`
    }
    const Detail = {
        data: function () {
            return {
                title: "详细页面",
                courseId: null,
                hotCourseList: [
                    {id: 1000, title: "python全栈开发"},
                    {id: 2000, title: "异步编程"},
                ],
            }
        },
        created: function () {
            this.courseId = this.$route.params.id;
            // 此处可以根据课程ID，发送ajax请求获取课程详细信息
            this.getCourseDetail();
        },
        watch: {
            $route: function (to, from) {
                this.courseId = to.params.id;
                this.getCourseDetail();
            }
        },
        methods: {
            getCourseDetail: function () {
                // 根据this.courseId获取课程详细信息
            }
        },
        template: `
                <div>
                    <h2>课程详细页面</h2>
                    <div>当前课程ID为：{{courseId}}</div>
                    <h3>课程推荐</h3>
                    <ul>
                        <li v-for="item in hotCourseList">
                            <router-link :to="{name:'Detail', params:{id:item.id}}">{{item.title}}</router-link>
                        </li>
                    </ul>
                </div>`
    }

    const Pins = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <h2>沸点专区</h2>
                <router-link :to="{name:'Hot'}">热点</router-link>
                <router-link :to="{name:'Following'}">关注</router-link>
                <router-view></router-view>
            </div>
         `
    };

    const Hot = {template: `<div><h2>Hot页面</h2></div>`};
    const Following = {template: `<div><h2>Following页面</h2></div>`};

    const router = new VueRouter({
        routes: [
            {path: '/', component: Home},
            {path: '/home', component: Home},
            {path: '/course', component: Course},
            {path: '/news', component: News},
            {path: '/detail:id', component: Detail, name: 'Detail'},
            {
                path: '/pins',
                component: Pins,
                name: 'Pins',
                children: [
                    {
                        // 当 /pins/hot 匹配成功，
                        // Hot组件 会被渲染在 Pins 的 <router-view> 中
                        path: 'hot',
                        component: Hot,
                        name:'Hot'
                    },
                    {
                        // 当 /pins/following 匹配成功，
                        // Following组件 会被渲染在 Pins 的 <router-view> 中
                        path: 'following',
                        component: Following,
                        name:'Following'
                    }
                ]
            }
        ],
        //mode: 'history'
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```





#### 案例：后台分类菜单

![image-20220124222144176](E:/LBF/笔记/课件（vue+drf+业务）/第2部分：vue/assets/image-20220124222144176-6449265.png)



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .header {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .header a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }

        .body .left-menu {
            width: 180px;
            border: 1px solid #dddddd;
            border-bottom: 0;
            position: absolute;
            left: 1px;
            top: 50px;
            bottom: 0;
            overflow: auto;
            background-color: #f3f5f7;
        }

        .body .left-menu .head {
            border-bottom: 1px solid #dddddd;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            padding: 15px;
        }

        .body .left-menu a {
            display: block;
            padding: 10px;
            border-bottom: 1px solid #dddddd;
        }

        .body .right-body {
            position: absolute;
            left: 183px;
            top: 50px;
            right: 0;
            bottom: 0;
            overflow: auto;
            padding: 10px;

        }
    </style>

    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
    <script src="axios.min.js"></script>
</head>
<body>
<div id="app">
    <div class="header">
        <router-link to="/">Logo</router-link>
        <router-link to="/home">首页</router-link>
        <router-link to="/task">任务宝</router-link>
        <router-link to="/message">消息宝</router-link>
    </div>
    <div class="body">
        <router-view></router-view>
    </div>

</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用xx系统"
            }
        },
        template: `<h2>{{title}}</h2>`
    };

    const Task = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <div class="left-menu">
                    <div class="head">任务宝</div>
                    <router-link :to="{name:'Fans'}">粉丝</router-link>
                    <router-link :to="{name:'Spread'}">推广码</router-link>
                    <router-link :to="{name:'Statistics'}">数据统计</router-link>
                </div>
                <div class="right-body">
                    <router-view></router-view>
                </div>

            </div>`
    };

    const Fans = {template: `<h3>粉丝页面</h3>`};
    const Spread = {template: `<h3>推广码页面</h3>`};
    const Statistics = {template: `<h3>数据统计页面</h3>`};

    const Message = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <div class="left-menu">
                    <div class="head">消息宝</div>
                    <router-link :to="{name:'Sop'}">SOP</router-link>
                    <router-link :to="{name:'Send'}">推送管理</router-link>
                </div>
                <div class="right-body">
                    <router-view></router-view>
                </div>

            </div>`
    };

    const Sop = {template: `<h3>SOP页面</h3>`};
    const Send = {template: `<h3>推送管理页面</h3>`};

    const router = new VueRouter({
        routes: [
            {path: '/', component: Home},
            {path: '/home', component: Home},
            {
                path: '/task',
                component: Task,
                name: 'Task',
                children: [
                    {
                        path: '',
                        // component: Fans,
                        // redirect:'/task/fans'
                        redirect: {name: 'Fans'}
                    },
                    {
                        path: 'fans',
                        component: Fans,
                        name: 'Fans'
                    },
                    {
                        path: 'spread',
                        component: Spread,
                        name: 'Spread'
                    },
                    {
                        path: 'statistics',
                        component: Statistics,
                        name: 'Statistics'
                    }
                ]
            },
            {
                path: '/message',
                component: Message,
                name: 'Message',
                children: [
                    {
                        path: 'sop',
                        component: Sop,
                        name: 'Sop'
                    },
                    {
                        path: 'send',
                        component: Send,
                        name: 'Send'
                    }
                ]
            }
        ]
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```



### 4.7 编程式导航

除了使用 `<router-link>` 创建 a 标签来定义导航链接，我们还可以借助 router 的实例方法，通过编写代码来实现。

想要导航到不同的 URL，则使用 `router.push` 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。

- router.push

  ```javascript
  // 字符串
  router.push('home')
  
  // 对象
  router.push({ path: 'home' })
  
  // 命名的路由
  router.push({ name: 'user', params: { userId: '123' }}) //
  
  // 带查询参数，变成 /register?plan=private
  router.push({ path: 'register', query: { plan: 'private' }})
  ```

- router.replace

  ```javascript
  // 字符串
  router.replace('home')
  
  // 对象
  router.replace({ path: 'home' })
  
  // 命名的路由
  router.replace({ name: 'user', params: { userId: '123' }})
  
  // 带查询参数，变成 /register?plan=private
  router.replace({ path: 'register', query: { plan: 'private' }})
  
  # 跟 router.push 很像，唯一的不同就是，它不会向 history 添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录。
  ```

- router.go  这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步

  ```javascript
  // 在浏览器记录中前进一步，等同于 history.forward()
  router.go(1)
  
  // 后退一步记录，等同于 history.back()
  router.go(-1)
  
  // 前进 3 步记录
  router.go(3)
  
  // 如果 history 记录不够用，那就默默地失败呗
  router.go(-100)
  router.go(100)
  ```

  

#### 案例：登录跳转（含顶部）

![image-20220124230751442](E:/LBF/笔记/课件（vue+drf+业务）/第2部分：vue/assets/image-20220124230751442-6449299.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .header {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .header a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }


    </style>
    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
</head>
<body>
<div id="app">
    <div class="header">
        <router-link to="/">Logo</router-link>
        <router-link to="/home">首页</router-link>
        <router-link to="/task">任务宝</router-link>
        <router-link to="/message">消息宝</router-link>

        <div style="float: right;">
            <router-link to="/login">登录</router-link>
        </div>
    </div>
    <div class="body">
        <router-view></router-view>
    </div>

</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用xx系统"
            }
        },
        template: `<h2>{{title}}</h2>`
    };

    const Task = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <h2>任务宝页面</h2>
            </div>`
    };

    const Message = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <h2>消息宝页面</h2>
            </div>`
    };

    const Login = {
        data: function () {
            return {
                user: '',
                pwd: ''
            }
        },
        methods: {
            doLogin: function () {
                if (this.user.length > 0 && this.pwd.length > 0) {
                    this.$router.push({name: 'Task'});
                    // this.$router.replace({name: 'Task'});
                }
            }
        },
        template: `
            <div style="width: 500px;margin: 100px auto">
                <input type="text" placeholder="用户名" v-model="user"/>
                <input type="text" placeholder="密码" v-model="pwd" />
                <input type="button" value="提 交"  @click="doLogin" />
            </div>
         `
    };
    const router = new VueRouter({
        routes: [
            {path: '/', component: Home},
            {path: '/home', component: Home},
            {path: '/login', component: Login, name: 'Login'},
            {path: '/task', component: Task, name: 'Task'},
            {path: '/message', component: Message, name: 'Message'}
        ]
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```

#### 

#### 案例：登录跳转（不含顶部）

![image-20220124234015248](E:/LBF/笔记/课件（vue+drf+业务）/第2部分：vue/assets/image-20220124234015248-6451139.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .header {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .header a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }

        .body .left-menu {
            width: 180px;
            border: 1px solid #dddddd;
            border-bottom: 0;
            position: absolute;
            left: 1px;
            top: 50px;
            bottom: 0;
            overflow: auto;
            background-color: #f3f5f7;
        }

        .body .left-menu .head {
            border-bottom: 1px solid #dddddd;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            padding: 15px;
        }

        .body .left-menu a {
            display: block;
            padding: 10px;
            border-bottom: 1px solid #dddddd;
        }

        .body .right-body {
            position: absolute;
            left: 183px;
            top: 50px;
            right: 0;
            bottom: 0;
            overflow: auto;
            padding: 10px;

        }
    </style>
    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
</head>
<body>
<div id="app">
    <router-view></router-view>
</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用xx系统"
            }
        },
        template: `
            <div>
                <div class="header">
                    <router-link to="/">Logo</router-link>
                    <router-link to="/home">首页</router-link>
                    <router-link :to="{name:'Task'}">任务宝</router-link>
                    <router-link :to="{name:'Message'}">消息宝</router-link>

                    <div style="float: right;">
                        <router-link to="/login">登录</router-link>
                    </div>
                </div>
                <div class="body">
                    <router-view></router-view>
                </div>

            </div>
        `
    };

    const Index = {template: '<h3>这是个首页呀...</h3>'}

    const Task = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <div class="left-menu">
                    <div class="head">任务宝</div>
                    <router-link :to="{name:'Fans'}">粉丝</router-link>
                    <router-link :to="{name:'Spread'}">推广码</router-link>
                    <router-link :to="{name:'Statistics'}">数据统计</router-link>
                </div>
                <div class="right-body">
                    <router-view></router-view>
                </div>

            </div>`
    };

    const Fans = {template: `<h3>粉丝页面</h3>`};
    const Spread = {template: `<h3>推广码页面</h3>`};
    const Statistics = {template: `<h3>数据统计页面</h3>`};

    const Message = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <div class="left-menu">
                    <div class="head">消息宝</div>
                    <router-link :to="{name:'Sop'}">SOP</router-link>
                    <router-link :to="{name:'Send'}">推送管理</router-link>
                </div>
                <div class="right-body">
                    <router-view></router-view>
                </div>

            </div>`
    };

    const Sop = {template: `<h3>SOP页面</h3>`};
    const Send = {template: `<h3>推送管理页面</h3>`};
    const Login = {
        data: function () {
            return {
                user: '',
                pwd: ''
            }
        },
        methods: {
            doLogin: function () {
                if (this.user.length > 0 && this.pwd.length > 0) {
                    this.$router.push({name: 'Index'});
                    // this.$router.replace({name: 'Task'});
                }
            }
        },
        template: `
            <div style="width: 500px;margin: 100px auto">
                <input type="text" placeholder="用户名" v-model="user"/>
                <input type="text" placeholder="密码" v-model="pwd" />
                <input type="button" value="提 交"  @click="doLogin" />
            </div>
         `
    };



    const router = new VueRouter({
        routes: [
            {
                path: '/',
                // component: Home,
                redirect: '/login'
            },
            {path: '/login', component: Login, name: 'Login'},
            {
                path: '/home',
                component: Home,
                children: [
                    {
                        path: '',
                        component: Index,
                        name: "Index"
                    },
                    {
                        path: 'task',
                        component: Task,
                        name: 'Task',
                        children: [
                            {
                                path: 'fans',
                                component: Fans,
                                name: 'Fans'
                            },
                            {
                                path: 'spread',
                                component: Spread,
                                name: 'Spread'
                            },
                            {
                                path: 'statistics',
                                component: Statistics,
                                name: 'Statistics'
                            }
                        ]
                    },
                    {
                        path: 'message',
                        component: Message,
                        name: 'Message',
                        children: [
                            {
                                path: 'sop',
                                component: Sop,
                                name: 'Sop'
                            },
                            {
                                path: 'send',
                                component: Send,
                                name: 'Send'
                            }
                        ]
                    }
                ],
            },

        ]
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```

### 

### 4.8 导航守卫

在基于vue-router实现访问跳转时，都会执行一个钩子。

```javascript
const router = new VueRouter({ ... })

router.beforeEach((to, from, next) => {
	// to: Route: 即将要进入的目标 路由对象
	// from: Route: 当前导航正要离开的路由
    // next() 继续向后执行
    // next(false) 中断导航，保持当前所在的页面。
    // next('/')   next({path:'/'}) next({name:'Login'})  跳转到指定页面
})
```

注意：可以基于他实现未登录跳转登录页面。



#### 案例：登录拦截（全局）

> 未登录时，访问后台管理页面，自动跳转到登录页面。

![image-20220125000302331](E:/LBF/笔记/课件（vue+drf+业务）/第2部分：vue/assets/image-20220125000302331-6451838.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .header {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .header a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }

        .body .left-menu {
            width: 180px;
            border: 1px solid #dddddd;
            border-bottom: 0;
            position: absolute;
            left: 1px;
            top: 50px;
            bottom: 0;
            overflow: auto;
            background-color: #f3f5f7;
        }

        .body .left-menu .head {
            border-bottom: 1px solid #dddddd;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            padding: 15px;
        }

        .body .left-menu a {
            display: block;
            padding: 10px;
            border-bottom: 1px solid #dddddd;
        }

        .body .right-body {
            position: absolute;
            left: 183px;
            top: 50px;
            right: 0;
            bottom: 0;
            overflow: auto;
            padding: 10px;

        }
    </style>
    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
</head>
<body>
<div id="app">
    <router-view></router-view>
</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用xx系统"
            }
        },
        methods: {
            doLogout: function () {
                sessionStorage.clear();
                this.$router.push({name: "Login"});
            }
        },
        template: `
            <div>
                <div class="header">
                    <router-link to="/">Logo</router-link>
                    <router-link to="/home">首页</router-link>
                    <router-link :to="{name:'Task'}">任务宝</router-link>
                    <router-link :to="{name:'Message'}">消息宝</router-link>

                    <div style="float: right;">
                        <a @click="doLogout">注销</a>
                    </div>
                </div>
                <div class="body">
                    <router-view></router-view>
                </div>

            </div>
        `
    };

    const Index = {template: '<h3>这是个首页呀...</h3>'}

    const Task = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <div class="left-menu">
                    <div class="head">任务宝</div>
                    <router-link :to="{name:'Fans'}">粉丝</router-link>
                    <router-link :to="{name:'Spread'}">推广码</router-link>
                    <router-link :to="{name:'Statistics'}">数据统计</router-link>
                </div>
                <div class="right-body">
                    <router-view></router-view>
                </div>

            </div>`
    };

    const Fans = {template: `<h3>粉丝页面</h3>`};
    const Spread = {template: `<h3>推广码页面</h3>`};
    const Statistics = {template: `<h3>数据统计页面</h3>`};

    const Message = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <div class="left-menu">
                    <div class="head">消息宝</div>
                    <router-link :to="{name:'Sop'}">SOP</router-link>
                    <router-link :to="{name:'Send'}">推送管理</router-link>
                </div>
                <div class="right-body">
                    <router-view></router-view>
                </div>

            </div>`
    };

    const Sop = {template: `<h3>SOP页面</h3>`};
    const Send = {template: `<h3>推送管理页面</h3>`};
    const Login = {
        data: function () {
            return {
                user: '',
                pwd: ''
            }
        },
        methods: {
            doLogin: function () {
                if (this.user.length > 0 && this.pwd.length > 0) {
                    sessionStorage.setItem("isLogin", true);
                    this.$router.push({name: 'Index'});
                }
            }
        },
        template: `
            <div style="width: 500px;margin: 100px auto">
                <input type="text" placeholder="用户名" v-model="user"/>
                <input type="text" placeholder="密码" v-model="pwd" />
                <input type="button" value="提 交"  @click="doLogin" />
            </div>
         `
    };
    const router = new VueRouter({
        routes: [
            {
                path: '/',
                component: Home,
                redirect: '/home'
            },
            {
                path: '/home',
                component: Home,
                name: "Home",
                children: [
                    {
                        path: '',
                        component: Index,
                        name: "Index"
                    },
                    {
                        path: 'task',
                        component: Task,
                        name: 'Task',
                        children: [
                            {
                                path: 'fans',
                                component: Fans,
                                name: 'Fans'
                            },
                            {
                                path: 'spread',
                                component: Spread,
                                name: 'Spread'
                            },
                            {
                                path: 'statistics',
                                component: Statistics,
                                name: 'Statistics'
                            }
                        ]
                    },
                    {
                        path: 'message',
                        component: Message,
                        name: 'Message',
                        children: [
                            {
                                path: 'sop',
                                component: Sop,
                                name: 'Sop'
                            },
                            {
                                path: 'send',
                                component: Send,
                                name: 'Send'
                            }
                        ]
                    }
                ],
            },
            {path: '/login', component: Login, name: 'Login'},
        ]
    })

    router.beforeEach((to, from, next) => {
        // 如果已登录，则可以继续访问目标地址
        if (sessionStorage.getItem('isLogin')) {
            next();
            return;
        }
        // 未登录，访问登录页面
        if (to.name === "Login") {
            next();
            return;
        }
        // 未登录，跳转登录页面
        // next(false); 保持当前所在页面，不跳转
        next({name: 'Login'});
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```



#### 案例：登录拦截（路由）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        body {
            margin: 0;
        }

        .header {
            height: 48px;
            background-color: #499ef3;
            line-height: 48px;

        }

        .header a {
            color: white;
            text-decoration: none;
            padding: 0 10px;
        }

        .body .left-menu {
            width: 180px;
            border: 1px solid #dddddd;
            border-bottom: 0;
            position: absolute;
            left: 1px;
            top: 50px;
            bottom: 0;
            overflow: auto;
            background-color: #f3f5f7;
        }

        .body .left-menu .head {
            border-bottom: 1px solid #dddddd;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            padding: 15px;
        }

        .body .left-menu a {
            display: block;
            padding: 10px;
            border-bottom: 1px solid #dddddd;
        }

        .body .right-body {
            position: absolute;
            left: 183px;
            top: 50px;
            right: 0;
            bottom: 0;
            overflow: auto;
            padding: 10px;

        }
    </style>
    <script src="vue.js"></script>
    <script src="vue-router.js"></script>
</head>
<body>
<div id="app">
    <router-view></router-view>
</div>

<script>

    const Home = {
        data: function () {
            return {
                title: "欢迎使用xx系统"
            }
        },
        methods: {
            doLogout: function () {
                sessionStorage.clear();
                this.$router.push({name: "Login"});
            }
        },
        template: `
            <div>
                <div class="header">
                    <router-link to="/">Logo</router-link>
                    <router-link to="/home">首页</router-link>
                    <router-link :to="{name:'Task'}">任务宝</router-link>
                    <router-link :to="{name:'Message'}">消息宝</router-link>

                    <div style="float: right;">
                        <a @click="doLogout">注销</a>
                    </div>
                </div>
                <div class="body">
                    <router-view></router-view>
                </div>

            </div>
        `
    };

    const Index = {template: '<h3>这是个首页呀...</h3>'}

    const Task = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <div class="left-menu">
                    <div class="head">任务宝</div>
                    <router-link :to="{name:'Fans'}">粉丝</router-link>
                    <router-link :to="{name:'Spread'}">推广码</router-link>
                    <router-link :to="{name:'Statistics'}">数据统计</router-link>
                </div>
                <div class="right-body">
                    <router-view></router-view>
                </div>

            </div>`
    };

    const Fans = {template: `<h3>粉丝页面</h3>`};
    const Spread = {template: `<h3>推广码页面</h3>`};
    const Statistics = {template: `<h3>数据统计页面</h3>`};

    const Message = {
        data: function () {
            return {}
        },
        template: `
            <div>
                <div class="left-menu">
                    <div class="head">消息宝</div>
                    <router-link :to="{name:'Sop'}">SOP</router-link>
                    <router-link :to="{name:'Send'}">推送管理</router-link>
                </div>
                <div class="right-body">
                    <router-view></router-view>
                </div>

            </div>`
    };

    const Sop = {template: `<h3>SOP页面</h3>`};
    const Send = {template: `<h3>推送管理页面</h3>`};
    const Login = {
        data: function () {
            return {
                user: '',
                pwd: ''
            }
        },
        methods: {
            doLogin: function () {
                if (this.user.length > 0 && this.pwd.length > 0) {
                    sessionStorage.setItem("isLogin", true);
                    this.$router.push({name: 'Index'});
                }
            }
        },
        template: `
            <div style="width: 500px;margin: 100px auto">
                <input type="text" placeholder="用户名" v-model="user"/>
                <input type="text" placeholder="密码" v-model="pwd" />
                <input type="button" value="提 交"  @click="doLogin" />
            </div>
         `
    };
    const router = new VueRouter({
        routes: [
            {
                path: '/',
                component: Home,
                redirect: '/home'
            },
            {
                path: '/home',
                component: Home,
                name: "Home",
                children: [
                    {
                        path: '',
                        component: Index,
                        name: "Index"
                    },
                    {
                        path: 'task',
                        component: Task,
                        name: 'Task',
                        children: [
                            {
                                path: 'fans',
                                component: Fans,
                                name: 'Fans'
                            },
                            {
                                path: 'spread',
                                component: Spread,
                                name: 'Spread'
                            },
                            {
                                path: 'statistics',
                                component: Statistics,
                                name: 'Statistics'
                            }
                        ]
                    },
                    {
                        path: 'message',
                        component: Message,
                        name: 'Message',
                        children: [
                            {
                                path: 'sop',
                                component: Sop,
                                name: 'Sop'
                            },
                            {
                                path: 'send',
                                component: Send,
                                name: 'Send'
                            }
                        ]
                    }
                ],
                beforeEnter: (to, from, next) => {
                    if (sessionStorage.getItem('isLogin')) {
                        next();
                        return;
                    }
                    // 未登录，跳转登录页面
                    // next(false); 保持当前所在页面，不跳转
                    next({name: 'Login'});
                }
            },
            {path: '/login', component: Login, name: 'Login'},
        ]
    })

    var app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router: router
    })
</script>
</body>
</html>
```





- cookie

- localStorage

  ```
  setItem (key, value)
  getItem (key)
  removeItem (key)
  clear ()
  key (index)
  ```

- sessionStorage





## 5.脚手架

基于vue+vue-router单文件开发，可以完成小规模的页面的开发，但如果项目大+组件多+依赖多，开发起来就非常不方便。

此时，脚手架（vue cli - Vue Command Line Interface ）是一个基于 Vue.js 进行快速开发的完整系统。

```
官方的说法：
Vue CLI 致力于将 Vue 生态中的工具基础标准化。它确保了各种构建工具能够基于智能的默认配置即可平稳衔接，这样你可以专注在撰写应用上，而不必花好几天去纠结配置的问题。
```

```
通俗的说法：
他帮助我们构内置了很多组件来帮助我们更便捷的的开发vue.js项目。
```



### 5.1 安装

- 第一步：安装node.js

  ```
  Vue CLI 4.x+ 需要 Node.js v8.9 或更高版本 (推荐 v10 以上)。
  
  https://nodejs.org/en/download/
  ```

  

  注意：sudo命令是linux系统的命令，w系统减去此命令

  ```
  =======如果想要更新node.js的版本=======
  
  1.先查看本机node.js版本：
  	 node -v
  	
  2.清除node.js的cache：
  	sudo npm cache clean -f
  
  3.安装 n 工具，这个工具是专门用来管理node.js版本的，别怀疑这个工具的名字，是他是他就是他，他的名字就是 "n"
  	sudo npm install -g n
  
  4.安装最新版本的node.js
  	sudo n stable
  
  5.再次查看本机的node.js版本：
          node -v
  ```

- 第二步：关于npm

  ```
  安装上node之后，自带了npm包管理工具，类似于Python中的pip。
  
  如果想要更新npm到最新版，可以执行命令：
  	sudo npm install npm@latest -g
  ```

  

- 第三步：npm淘宝源，以后基于npm安装包就会快了（相当于豆瓣的pip源）

  ```
      npm config set registry https://registry.npm.taobao.org
  ```

- 第四步：全局安装vue-cli

  ```
  # 安装（最新版）
  sudo npm install -g @vue/cli
  
  # 安装（指定版本）
  sudo npm install -g @vue/cli@4.5.14
  
  # 卸载
  sudo npm uninstall -g @vue/cli
  ```

  



### 5.2 创建项目

```
cd /Users/wupeiqi/WebstormProjects
vue create mysite
```



提示：babel是一个将ES6语法转化成ES5的工具，eslint是做语法检查。



a few moments later...



按照提示执行如下命令，脚手架就会给我们大家一个Web服务去运行编写的vue项目（便于开发测试）。

```
cd mysite
npm run serve
```







### 5.3 编译部署

项目创建完，脚手架会默认会生成如下文件（包含项目依赖、配置文件、默认代码）。	

![image-20220310111119113](web前端.assets/image-20220310111119113.png)

如果以后项目开发完毕，想要进行项目部署，是不需要这些文件的，执行命令：

```
cd 项目目录
npm run build
```



![](web前端.assets/image-20220310111348156-16628722229292.png)

build会将项目中的依赖和代码自动编译成HTML、CSS、JavaScript代码，后续只需要将此代码上传至服务器部署即可。



### 5.4 目录结构

```
- babel.config.js      babel是ES6转换ES5的组件，这是他所需的配置文件（一般不需要动）。
- package.json         项目所需的包的版本信息。
- package-lock.json    保存项目所需的包细节以及包的依赖等信息。
- node-modules         项目安装依赖包的文件保存的地方。例如：npm install axios 
                       axios包会保存在此目录、信息也会写在 package.json、package-lock.json中   
- src
	- main.js          项目的启动 npm run serve ，用户访问时程序的入门。
	- App.vue		   主组件
	- components       子组件
	- assets           静态文件（自己的静态文件，会被压缩和合并）
- public		      【此目录下的文件直接被复制到dist/目录下，一般放不动的数据，引入第三方】
	- index.html       主HTML文件（模板引擎）
	- favicon.icon     图标
- README.md            项目说明文档
```

把项目发给他人时不要发`node-modules`文件夹，内存太大，有了`package.json` 及`package-lock.json`  后，只要执行如下指令会自动下载依赖包

```
cd 项目
npm install
```

本质上，其实就是将原来的代码做了拆分来进行开发，开发完毕之后再编译整合起来。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>

<div id="app">
    <h1>欢迎学习Vue.js</h1>
    <div>我叫{{name}}，微信{{wechat}}</div>
</div>

<script>
    
    
    var app = new Vue({
        el: '#app',
        data: {
            name: '武沛齐',
            wechat: 'wupeiqi888'
        },
        methods: {
            clickMe: function () {
                this.name = "alex";
                this.wechat = "wupeiqi666";
            }
        }
    })
</script>
</body>
</html>
```





### 5.5 快速上手

#### 5.5.1 axios组件

安装：

```
cd 项目目录
npm install axios
npm install vue-axios
```

导入：

**use:把两个变量引入到Vue这个对象里**

```javascript
// main.js
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)
```

使用：

```
Vue.axios.get(api).then((response) => {
  console.log(response.data)
})

this.axios.get(api).then((response) => {
  console.log(response.data)
})

this.$http.get(api).then((response) => {
  console.log(response.data)
})
```



#### 5.5.2 vue-router组件

安装：

```
cd 项目目录
npm install vue-router@3 
```

引入：

```javascript
// router/index.js

import Vue from 'vue'
import VueRouter from 'vue-router'


import Home from '../components/Home'


Vue.use(VueRouter)

const router = new VueRouter({
    routes: [
        {
            path: '/home',
            name: "Home",
            component: Home
        },
    ]
})

export default router
```

```javascript
// main.js
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'


import App from './App.vue'

// 导入router文件
import router from "./router"


Vue.use(VueAxios, axios)

Vue.config.productionTip = true


new Vue({
    router: router,
    render: h => h(App),
}).$mount('#app')
```

使用：App.vue

```
<router-link to="/home">点我</router-link>
<router-view></router-view>
```



#### 5.5.3 案例：路飞学城

基于vue-cli快速开发：路飞学城（第一版）



### 5.6 线上部署

- 第一步：编译

  ```
  npm run build
  ```

- 第二步：将编译后的代码dist文件上传到服务器（阿里云、腾讯云）

  ![image-20220312123432759](web前端.assets/image-20220312123432759.png)

- 第三步：安装nginx + 配置 + 启动

  ```
  yum install nginx
  ```


  vim /etc/nginx/nginx.conf

  ```
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 4096;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80;
        listen       [::]:80;
        server_name  _;
        # 项目目录
        root         /data/mysite;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
    }


}
  ```

  ```
>>>systemctl start nginx
  ```

- 第四步：访问
  ![image-20220312123724185](web前端.assets/image-20220312123724185.png)













## 6.vuex

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

说人话：将组件中需要共享的数据交给vuex来帮我们进行管理，例如：用户登录状态、加入购物车。

![image-20220314001612334](web前端.assets/image-20220314001612334.png)



### 6.1 案例：登录

创建项目

```
vue create vxdemo
```

安装router

```dc
npm install vue-router@3
```

安装vuex

```
npm install vuex@3
```



- main.js

  ```javascript
  import Vue from 'vue'
  import App from './App.vue'
  import router from "./router"
  import store from "./store"
  
  Vue.config.productionTip = false
  
  new Vue({
      router: router,
      store: store,
      render: h => h(App),
  }).$mount('#app')
  ```

- App.vue

  ```vue
      <template>
          <div id="app">
              <div class="menu">
                  <div class="container">
                      <router-link to="/home">首页</router-link>
                      <router-link to="/course">课程</router-link>
  
                      <div style="float: right">
                          <a v-if="this.$store.state.isLogin">
                              {{this.$store.state.userInfo.username}}
                          </a>
                          <router-link v-else to="/login">登录</router-link>
  
                      </div>
                  </div>
              </div>
              <div class="container">
                  <router-view></router-view>
              </div>
          </div>
      </template>
      <script>
          export default {
              name: 'App',
              data() {
                  return {}
              },
              components: {},
          }
      </script>
  
      <style>
          body {
              margin: 0;
          }
          .container {
              width: 1100px;
              margin: 0 auto;
          }
          .menu {
              height: 48px;
              background-color: #499ef3;
              line-height: 48px;
  
          }
          .menu a {
              color: white;
              text-decoration: none;
              padding: 0 10px;
          }
      </style>
  ```

- store/index.js

  ```javascript
  import Vue from 'vue'
  import Vuex from 'vuex'
  
  Vue.use(Vuex)
  
  
  export default new Vuex.Store({
      state: {
          isLogin: false, //是否登录
          userInfo: null //用户信息
      },
      mutations: {
          login: function (state, info) {
              state.userInfo = info;
              state.isLogin = true;
          },
  
      },
      actions: {}
  })
  
  ```

- router/index.js

  ```javascript
  // router/index.js
  
  import Vue from 'vue'
  import VueRouter from 'vue-router'
  
  
  import Home from '../components/Home'
  import Course from '../components/Course'
  import Login from '../components/Login'
  
  
  Vue.use(VueRouter)
  
  const router = new VueRouter({
      routes: [
          {
              path: '/home',
              name: "Home",
              component: Home
          },
          {
              path: '/course',
              name: "Course",
              component: Course
          },
          {
              path: '/login',
              name: "Login",
              component: Login
          },
      ]
  })
  
  export default router
  ```

- components/Login.vue

  ```html
  <template>
      <div>
          <input type="text" v-model="info.username" placeholder="用户名">
          <input type="password" v-model="info.password" placeholder="密码">
          <input type="button" value="登录" @click="doLogin"/>
      </div>
  </template>
  
  <script>
      export default {
          name: "Login",
          data() {
              return {
                  info: {
                      username: "",
                      password: ""
                  }
              }
          },
          methods: {
              doLogin: function () {
                  // 1.用户登录
                  this.$store.commit('login', this.info);
                  // 2.登录成功修改状态
                  this.$router.push({name: 'Home'});
              }
          }
      }
  </script>
  
  <style scoped>
  
  </style>
  ```



### 6.2 关于computed属性

在vue的组件中有一个computed属性（计算属性），监听关联的数据，如果发生变化则重新计算并显示。

```html
<template>
    <div>
        <h1>主页 {{v1}} {{ v2}}</h1>
        
        <div>总数：{{totalData}}</div>
        <input type="button" value="点我" @click="addData"/>
    </div>
</template>

<script>
    export default {
        name: "Home",
        data() {
            return {
                v1: 123,
                v2: 456
            }
        },
        computed: {
            totalData: {
                get() {
                    let data = this.v1 + this.v2;
                    return data + 1000;
                },
                set(value) {
                    this.v1 = value;
                }
            }
        },
        methods: {
            addData() {
                this.totalData = 999;
                // this.v2 = 1000;
            }
        }
    }
</script>

<style scoped>

</style>
```



所以，上述案例也可以用computed属性来实现，例如：App.vue改成：

```html
<template>
    <div id="app">
        <div class="menu">
            <div class="container">
                <router-link to="/home">首页</router-link>
                <router-link to="/course">课程</router-link>

                <div style="float: right">
                    <a v-if="userState">
                        {{userName}}
                    </a>
                    <router-link v-else to="/login">登录</router-link>

                </div>
            </div>
        </div>
        <div class="container">
            <router-view></router-view>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'App',
        data() {
            return {}
        },
        computed: {
            userState: {
                get() {
                    return this.$store.state.isLogin;
                }
            },
            userName() {
                return this.$store.state.userInfo.username;
            },

        },
        components: {},
    }
</script>

<style>
    body {
        margin: 0;
    }

    .container {
        width: 1100px;
        margin: 0 auto;
    }

    .menu {
        height: 48px;
        background-color: #499ef3;
        line-height: 48px;

    }

    .menu a {
        color: white;
        text-decoration: none;
        padding: 0 10px;
    }


</style>
```





### 6.3 案例：购物车

![image-20220314001612334](web前端.assets/image-20220314001612334.png)







### 6.4 关于Action

Action 类似于 mutation，不同在于：

- Action 提交的是 mutation，而不是直接变更状态。
- Action 可以包含任意异步操作。

代码示例：

```javascript
const store = createStore({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count+=1;
    }
  },
  actions: {
    increment (context) {
        // 触发mutations
      	context.commit('increment')
    }
  }
})
```

在组件中如果要触发，则应该执行：

```javascript
this.$store.dispatch('increment')
```



这就有点像脱裤子放屁，意义何在呢？ 当有异步操作时，应该使用action、而不是mutation，例如：

```javascript
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)


export default new Vuex.Store({
    state: {
        isLogin: false, //是否登录
        userInfo: null, //用户信息
        carNumber: 0,
        xxxxx: 10
    },
    mutations: {
        login: function (state, info) {
            state.userInfo = info;
            state.isLogin = true;
        },
        addCar: function (state) {
            state.carNumber += 1;
        },
        fetchAsync: function (state) {
            // ajax
            setTimeout(function () {
                state.xxxxx += 1;
            }, 1000);
        }

    },
    actions: {}
})

```

```
this.$store.commit("fetchAsync");
```

从效果上看是没有问题的，但是通过开发者工具就会发现，监测到的state的数据不准确。

![image-20220314005748980](web前端.assets/image-20220314005748980.png)



所以，这种情况可以选择用Action。

```javascript
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)


export default new Vuex.Store({
    state: {
        isLogin: false, //是否登录
        userInfo: null, //用户信息
        carNumber: 0,
        xxxxx: 10
    },
    mutations: {
        login: function (state, info) {
            state.userInfo = info;
            state.isLogin = true;
        },
        addCar: function (state) {
            state.carNumber += 1;
        },
        fetchAsync: function (state,data) {
            state.xxxxx += 1;
            console.log(data);
        }

    },
    actions: {
        fetchAsync: function (context,data) {
            setTimeout(function () {
                context.commit("fetchAsync",data);
            }, 1000);
        }
    }
})

```

再触发时，调用：

```
this.$store.dispatch('fetchAsync',{ amount: 10})
```







## 7.flex布局

在CSS3中flex可以非常便捷的可以帮助我们实现对页面的布局。

- 传统的页面布局，基于div+float来实现。
- flex可以快速实现页面的布局（很方便）。



关于flex布局你必须要了解的有一下几点：

```html
<div class="menu" 样式>
    <div class="item" 样式>112</div>
    <div class="item">113</div>
</div>
```

### 7.1 容器

#### 7.1.1 flex布局

在容器元素上应用

```
<div class="menu">
    <div class="item">112</div>
    <div class="item">113</div>
</div>

<style>
    .menu{
        border: 1px solid red;
        width: 500px;
        display: flex;         // 表示flex布局
    }
</style>
```



#### 7.1.2 元素的方向（主轴和副轴）

```
<div class="menu">
    <div class="item">112</div>
    <div class="item">113</div>
</div>
<style>
    .menu{
        border: 1px solid red;
        width: 500px;
        
        display: flex;         // 表示flex布局
        flex-direction: row;   // 主轴是横向，副轴是纵向。
    }
</style>
```



#### 7.1.3 元素排列方式

```
justify-content，主轴上的元素的排列方式
align-items，副轴上的元素的排列方式。
```

示例1： 

```
<div class="menu">
    <div class="item">11</div>
    <div class="item">112</div>
    <div class="item">112</div>
</div>
<style>
    .menu {
        width: 500px;
        border: 1px solid red;
        display: flex;

        flex-direction: row;
        justify-content: flex-start;     /* 主轴=横向，横向从左开始 */
        justify-content: flex-end;       /* 主轴=横向，横向从右开始 */
        justify-content: space-between;   /* 主轴=横向，左右定格，中间元素等分空白 */
        justify-content: space-around;   /* 主轴=横向，所有元素等分空白 */
        justify-content: space-evenly;   /* 主轴=横向，元素间距一样 */
    }

    .item {
        border: 1px solid green;
        padding: 5px 50px;
        height: 50px;
        width: 40px;
    }
</style>
```

示例2：

```
<div class="menu">
    <div class="item">11</div>
    <div class="item">112</div>
    <div class="item">112</div>
</div>
<style>
    .menu {
        width: 500px;
        height: 300px;
        border: 1px solid red;
        display: flex;

        flex-direction: row;
        justify-content: flex-start;     /* 主轴=横向，横向从左开始 */
        justify-content: flex-end;       /* 主轴=横向，横向从右开始 */
        justify-content: space-between;   /* 主轴=横向，左右定格，中间元素等分空白 */
        justify-content: space-around;   /* 主轴=横向，所有元素等分空白 */
        justify-content: space-evenly;   /* 主轴=横向，元素间距一样 */

        align-items: center;             /* 副轴=纵向，元素居中*/
        align-items: flex-start;         /* 副轴=纵向，元素顶部*/
        align-items: flex-end;           /* 副轴=纵向，元素底部*/
    }

    .item {
        border: 1px solid green;
        padding: 5px 50px;
        height: 50px;
        width: 40px;
    }
</style>
```



#### 7.1.4 换行

- `flex-wrap: nowrap;` 元素超过容器，不换行
- `flex-wrap: wrap;` 元素超过容器，换行



示例1：不换行



```
<div class="menu">
    <div class="item">11</div>
    <div class="item">112</div>
    <div class="item">112</div>
    <div class="item">112</div>
    <div class="item">112</div>
</div>
<style>
    .menu {
        width: 500px;
        height: 200px;
        border: 1px solid red;
        display: flex;

        flex-direction: row;
        justify-content: space-evenly;   /* 主轴=横向，元素间距一样 */
        align-items: flex-start;         /* 副轴=纵向，元素顶部*/

        flex-wrap: nowrap;

    }

    .item {
        border: 1px solid green;
        padding: 5px 50px;
        height: 50px;
        width: 40px;
    }
</style>
```



示例2：换行

```
<div class="menu">
    <div class="item">111</div>
    <div class="item">112</div>
    <div class="item">112</div>
    <div class="item">112</div>
    <div class="item">112</div>

</div>

<style>
    body{
        margin: 0;
    }
    .menu {
        width: 500px;
        height: 200px;
        border: 1px solid red;
        display: flex;

        flex-direction: row;
        justify-content: space-evenly;   /* 主轴=横向，元素间距一样 */
        align-items: flex-start;         /* 副轴=纵向，元素顶部*/

        flex-wrap: wrap;

    }

    .item {
        border: 1px solid green;
        padding: 5px 50px;
        height: 50px;
        width: 40px;
    }
</style>
```



#### 7.1.5 多行对齐方式

**align-content**用于控制多行元素的对齐方式，如果元素只有一行则不会起作用；默认stretch，即在元素没设置高度，或高度为auto情况下让元素填满整个容器。

```
flex-start | flex-end | center | space-between | space-around | space-evenly | stretch(默认);
```



### 7.2 元素

#### 7.2.1 顺序

order，默认0，用于决定项目排列顺序，数值越小，项目排列越靠前。



```
<div class="father">
    <div class="son" style="order: 2">11</div>
    <div class="son" style="order: 0">22</div>
    <div class="son" style="order: 1">33</div>
</div>

<style scoped>
    .father {
        border: 1px solid red;
        width: 500px;
        height: 300px;
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
    }

    .father .son {
        border: 1px solid saddlebrown;
        width: 20px;
        height: 18px;
    }
</style>
```



#### 7.2.2 剩余空间

flex-grow，默认0，用于决定项目在有剩余空间的情况下是否放大，默认不放大；



```
<div class="father">
    <div class="son">11</div>
    <div class="son" style="flex-grow: 1">22</div>
    <div class="son" style="flex-grow: 1">33</div>
</div>
```













### 案例：flex页面布局



```html
<template>
    <div>
        <div class="row1">
            <div class="company"></div>
            <div class="pic"></div>
            <div class="pic"></div>
            <div class="pic"></div>
        </div>
        <div class="row2">
            <div class="title">
                <div>手机</div>
                <div>查看更多</div>
            </div>
            <div class="pic-list">
                <div class="big"></div>
                <div class="right-list">
                    <div class="group">
                        <div class="phone"></div>
                        <div class="phone"></div>
                        <div class="phone"></div>
                        <div class="phone"></div>
                    </div>
                    <div class="group">
                        <div class="phone"></div>
                        <div class="phone"></div>
                        <div class="phone"></div>
                        <div class="phone"></div>
                    </div>

                </div>
            </div>
        </div>

        <div class="course-list">
            <div class="item"></div>
            <div class="item"></div>
            <div class="item"></div>
            <div class="item"></div>
            <div class="item"></div>

        </div>
    </div>
</template>

<script>
    export default {
        name: "Mi"
    }
</script>

<style scoped>
    .row1 {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    .row1 .company {
        width: 210px;
        height: 180px;
        background-color: saddlebrown;
    }

    .row1 .pic {
        width: 266px;
        height: 180px;
        background-color: cadetblue;
    }

    .row2 .title {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    .row2 .pic-list {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    .row2 .pic-list .big {
        background-color: aquamarine;
        height: 610px;
        width: 210px;
        margin-right: 20px;
    }

    .row2 .pic-list .right-list {
        /*background-color: antiquewhite;*/
        flex-grow: 1;
    }

    .row2 .pic-list .right-list .group {


        display: flex;
        flex-direction: row;
        justify-content: space-between;
        flex-wrap: wrap;
    }

    .row2 .pic-list .right-list .phone {
        margin-bottom: 10px;
        border: 1px solid red;
        width: 200px;
        height: 300px;
    }

    .course-list {
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
    }

    .course-list .item {
        width: 24%;
        height: 100px;
        background-color: skyblue;
        margin-top: 15px;
    }
	
	// 如果最后一个元素，是第3个，右边距=一个位置 + 所有空白位置/3（有三个空白位置）
    .course-list .item:last-child:nth-child(4n - 1) {
        margin-right: calc(24% + 4% / 3);
    }

	// 如果最后一个元素，是第2个，右边距=两个位置 + 所有空白位置/3*2（有三个空白位置）
    .course-list .item:last-child:nth-child(4n - 2) {
        margin-right: calc(48% + 8% / 3);
    }
</style>
```



至此，结合以上的知识点，我们就可以来开发一个项目，但很多的页面按钮、标签、提示框等都需要自己手动，太费劲。

所以，接下来就要给大家的来聊一个UI框架 - ElementUI，他的内部提供了很多方便的样式和组件，可以加速我们开发。





## 8.ElementUI

Element，是 饿了吗 团队开发一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的组件库（也支持vue3.x）。

在他的基础上来开发，可以大大提升开发进度。

![image-20220312130559702](web前端.assets/image-20220312130559702.png)



想要在项目中进行使用element-ui需要提前安装并引入。



### 8.1 引入

**方式1：**完整引入

- 安装

  ```
  cd 项目目录
  npm install element-ui
  ```

- 引入

  ```javascript
  import Vue from 'vue';
  import ElementUI from 'element-ui';
  import 'element-ui/lib/theme-chalk/index.css';
  import App from './App.vue';
  
  Vue.use(ElementUI);
  
  new Vue({
      render: h => h(App),
  }).$mount('#app')
  
  ```

- 在组件中使用

  ```html
  <el-button type="success">哈哈哈</el-button>
  ```



**方式2**：局部引入

- 安装

  ```
  cd 项目目录
  npm install element-ui
  ```

- 引入

  ```javascript
  import Vue from 'vue';
  import { Button, Select } from 'element-ui';
  import 'element-ui/lib/theme-chalk/index.css';
  import App from './App.vue';
  
  
  Vue.use(Button)
  Vue.use(Select)
  
  new Vue({
      render: h => h(App),
  }).$mount('#app')
  
  ```

- 在组件中使用

  ```html
  <el-button type="success">哈哈哈</el-button>
  ```

  完整组件名称：https://element.eleme.cn/#/zh-CN/component/quickstart



### 8.2 组件的使用

参见官方文档，在后续的项目开发中来应用并使用。

















































































# 其它

## BootStrap样式

![](web.assets/image-20210304172121361-1621326379092.png)

Bootstrap是Twitter推出的一个用于前端开发的开源工具包。它由Twitter的设计师Mark Otto和Jacob Thornton合作开发，是一个CSS/HTML框架。目前，Bootstrap最新版本为4.4。 注意，Bootstrap有三个大版本分别是 v2、v3和v4，我们这里学习最常用的v3。

使用Bootstrap的好处：

​     Bootstrap简单灵活，可用于架构流行的用户界面，具有 友好的学习曲线，卓越的兼容性，响应式设计，12列栅格系统，样式向导文档，自定义JQuery插件，完整的类库，基于Less等特性。

下载

* bootstap英文官方: https://getbootstrap.com/

* bootstrap中文官网：http://www.bootcss.com/

* 下载地址: http://v3.bootcss.com/getting-started/#download

> 注意： Bootstrap提供了三种不同的方式供我们下载，我们不需要使用Bootstrap的源码 和 sass项目，只需要下载生产环境的Bootstrap即可。		





## Font Awesome图标

一个css图标的网

```
http://www.fontawesome.com.cn/faicons/
```

使用方法

```html
{% load static %}         			 1 模板顶部先引入静态文件夹

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <link rel="stylesheet" href="{% static 'plugins/bootstrap/css/bootstrap.css' %} "/>
    2 head头部引入css文件
    <link rel="stylesheet" href="{% static 'plugins/font-awesome/css/font-awesome.css' %} "/>
</head>
<body>
    
    
<div class="multi-menu">
    {% for item in menu_dict.values %}
        <div class="item">						3 创建一个i标签class属性= "图标名称"图标名称官网找
            <div class="title"><span class="icon-wrap"><i class="fa fa-user-circle-o"></i></span> {{ item.title }}</div>
            <div class="body {{ item.class }}">
                {% for per in item.children %}
                    <a class="{{ per.class }}" href="{{ per.url }}">{{ per.title }}</a>
                {% endfor %}
            </div>

        </div>
    {% endfor %}
    </div>
    
</body>
    
</html>
```



![image-20220609101908126](web.assets/image-20220609101908126.png)



















# 





