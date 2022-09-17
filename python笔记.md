 一 计算机基础和环境搭建

- 计算机基础
- 编程的本质
- Python的介绍
- Python环境的搭建



# 一 计算机基础

1.1 基本概念

- 1. 计算机的组成


  ```
计算机是由多个硬件组合而成，常见的硬件有：CPU、硬盘、内存、网卡、显示器、机箱、电源....

注意事项：机械将零件组合在一起，他们之间是无法进行协作。
  ```

- 操作系统

  ```
  用于协调计算机的各个硬件，让硬件之间进行协同工作，以完成某个目标。
  常见的操作系统分类：
  - windows，优点：生态牛逼、工具多；缺点：略慢、收费。【个人】
  	- xp
  	- win7
  	- win10
  	...
  - linux，优点：资源占用少、免费（很多公司的服务器上安装Linux）；缺点：工具少、告别游戏。【企业的服务器】
  	- centos
  	- ubuntu
  	- redhat
  	...
  - mac，优点：生态还行、工具差不多都有、用户体验和交互； 缺点：不能玩游戏
  ```

- 软件（应用程序）

  ```
  在安装上操作系统之后，我们会在自己电脑上安装一些常用的软件，例如：QQ、杀毒、微信...
  
  问题来了：这些软件是由谁开发的？是由各大公司的程序员开发的。
  
  以后的你肯定是写`软件`，可以把软件理解成为一大堆的代码（一篇文章）。
  ```


1.2 编程语言

软件，是由程序员使用 编程语言 开发出来的一大堆代码的集合。全球的编程语言有2500+多种，常见的编程语言：Java、C#、Python、PHP、C...

作文，是由小学生使用 汉语/英语/法语/日语... 写出来一大堆的文字的集合。



本质上学习编程语言就是学习他的语法，根据语法再去编写相应的软件中的功能。

- Python语言中输出的语法规则

  ```python
  print("我是Alex的二大爷")
  ```

- Golang语言中的输出的语法规则

  ```go
  fmt.Println("我是Alex二大爷")
  ```



1.3 编译器/解释器

编译器/解释器，就是一个`翻译官`，将代码翻译成计算机能够识别的命令。

```
A使用Python开发了一个软件 1000              B使用Golang开发了一个软件 2000

       Python解释器                        Golang编译器

                    操    作    系    统

               CPU    硬盘    网卡    内存    电源 .....
```

<img src="python神功.assets\image-20201021204525830.png" alt="image-20201021204525830" style="zoom:50%;" />

为什么有的叫解释器？有的叫编译器？

- 解释器，实时翻译。拿到1000行代码之后，解释一句交给操作系统一句。
- 编译器，全文翻译。拿到2000行代码之后会将他编译成一个临时文件（计算机能够识别命令），再把文件交给操作系统去读取。



Python、PHP、JavaScript、Ruby...一般称为解释型语言。

C、C++、Go、Java...一般称为编译型语言。



2.学习编程的本质

学编程本质上就是三件事：

- 选择一门编程语言，在自己的电脑上安装此编程语言相关的 编译器/解释器。
- 学习编程语言的语法规则，根据语法规则 + 业务背景 设计并开发你的软件（代码集合）。
- 使用 编译器/解释器 去运行自己写的代码。



## Python的介绍

3.1 语言的分类

- `翻译`的维度

  - 解释型语言，Python、Ruby....
  - 编译型语言，C、C++、Golang

- `高低`的维度

  - 低级编程语言，写出来的代码直接可以被计算机识别。

    ```
    机器语言，101 001 00001 00010 001000100010001，机器码，交给计算机去执行。
    汇编语言，MOV INC ... ，指令，交给计算机去执行。
    ```

  - 高级编程语言，写出来的代码无法直接被计算机识别，但可以通过某中方式将其转换为计算机可以识别的语言。

    ```
    C、C++、Java、Python、Ruby...，这类编程语言在编写代码时几乎是写英语作文。
    交由相关编译器或解释器翻译成机器码，然后再交给计算机去执行。
    ```

注意：现在基本上都使用高级编程语言。

3.2 Python

> Python的创始人为吉多·范罗苏姆（Guido van Rossum）。1989年的圣诞节期间，Guido开始写Python语言的编译器。Python这个名字，来自Guido所挚爱的电视剧Monty Python’s Flying Circus。他希望这个新的叫做Python的语言，能符合他的理想：创造一种C和shell之间，功能全面，易学易用，可拓展的语言。

全球众多编程语言，为何Python可以脱颖而出成为业界炙手可热的编程语言？目前位居TIOBE排行榜第三名并且一直呈上升趋势。

<img src="assets/image-20201021214459011.png" alt="image-20201021214459011" style="zoom:50%;" />



<img src="assets/image-20201021214518950.png" alt="image-20201021214518950" style="zoom:50%;" />



Python如此火爆的原因如下：

- 语法简洁 & 适合小白学习，相比较于其他编程语言Python的学习成本非常低，甚至可以让其他行业的人快速掌握编程技能，通过编程提供工作效率，例如：Excel自动化办公、文件和文件夹的处理等。
- 类库强大，Python自诞生之初就任其自然生长，经过多年的发展，造就其在很多领域都是积累了很多方便的类库，自然也成为了运维自动化、数据分析、机器学习首选编程语言。
- 开发效率极高，结合Python语法精炼和类库齐全的特点，所以在使用Python进行开发时可以用更少的代码完成更多的功能，大大提升开发效率。例如：Python10行代码实现的功能，用其他语言可能需要100+行才能完成。



3.3 Python的解释器种类（了解）

想要学一门编程语言：安装Python解释器、学习python语法并编写代码、使用Python解释器去执行编写好的代码。

Python在全球非常的火，很多公司都会想要来层热度。



由于Python太火了，所有就有很多的公司都开发了Python解释器（用来翻译python代码成为计算机能够识别的命令）。

- CPython【主流】，底层是由C语言开发出来的Python解释器。
- Jython，是由Java语言开发出来的Python解释器，方便与让Python和Java代码做集成。
- IronPython，是基于C#语言开发出来的Python解释器，方便与让Python和C#代码做集成。
- RubyPython，...
- PyPy，是对CPython的优化，他的执行效率提高了。引入编译器的功能，本质上将Python代码进行编译，再去执行编译后的代码。
- ...

注意：常说的Python解释器默认指的就是CPython解释器。

3.4 CPython解释器的版本

CPython的解释器主要有两大版本：

- 2.x，目前最新的Python2.7.18。（2020后不再维护）

  ```
  Being the last of the 2.x series, 2.7 received bugfix support until 2020. Support officially stopped January 1 2020, and 2.7.18 code freeze occurred on January 1 2020, but the final release occurred after that date.
  ```

- 3.x，目前最新的3.9.0版本（授课）。





## 环境搭建

- Python解释器，将程序员编写的python代码翻译成计算机能够识别的指令。
  - 主流CPython
  - 3.9.0版本
- 学习编程本质上的3件事
  - 安装 CPython 3.9.0版本解释器
  - 学习Python语法并写代码
  - 解释器去运行代码



4.1 安装Python解释器

4.1.1 mac系统

- 去Python官网下载Python解释器（3.9.0版本）

  ```
  https://www.python.org/
  ```

- 安装

  ```
  默认Python解释器安装目录： /Library/Frameworks/Python.framework/Versions/3.9
  
  有bin目录下有一个 python3.9 文件，他就是Python解释器的启动文件。
  解释器路径：/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 
  ```

- 写一个简单的Python代码并且让解释器去运行。

  ```python
  name = input("请输入用户名:")
  print("欢迎使用NB系统：",name)
  ```

  将文件保存在：文稿/hello.py【/Users/wupeiqi/Documents/hello.py】

  接下来要让解释器去运行代码文件：

  ```
  - 打开终端
  - 在终端输入：解释器 代码文件
    /Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 /Users/wupeiqi/Documents/hello.py
  ```

- 【补充】系统环境变量

  ```
  - 假设你有30个Python文件要运行
     /Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 /Users/wupeiqi/Documents/hello1.py
     ...
     /Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 /Users/wupeiqi/Documents/hello30.py
  
  - Python解释器的路径每次不用再写这么长。
      - 将  /Library/Frameworks/Python.framework/Versions/3.9/bin 添加到系统的环境变量中。
      - 以后再使用Python解释器去运行python代码时，就可以这样：
      	 python3.9 /Users/wupeiqi/Documents/hello1.py
      	 ...
      	 python3.9 /Users/wupeiqi/Documents/hello2.py
  
  - 如何将 /Library/Frameworks/Python.framework/Versions/3.9/bin 添加到系统的环境变量中 ？
  	- 默认你不用添加，默认Python解释器在安装的过程中已经帮你添加了。
  	- 自己手动想添加：
  		 - 打开用户目录的下的  .bash_profile 文件（.zprofile）
  		 - 在文件中写如下内容
  ```

  ```
  # Setting PATH for Python 3.9
  # The original version is saved in .zprofile.pysave
  PATH="/Library/Frameworks/Python.framework/Versions/3.9/bin:${PATH}"
  export PATH
  ```

4.1.2 windows系统

- Python官网下载Python解释器

  ```
  https://www.python.org/downloads/release/python-390/
  ```

- 在自己电脑上进行安装

  ```
  python解释器安装目录：C:\Python39
  python解释器的路径：C:\Python39\python.exe
  ```

- 编写一个Python代码并交给Python解释器去运行

  ```python
  name = input("请输入用户名")
  print("欢迎使用NB系统",name)
  ```

  并将文件保存在：Y:\hello.py

  怎么让解释器去运行写好的代码文件呢？

  ```
  - 打开终端
  - 在终端输入：解释器路径 代码路径
  ```

- 优化配置（让以后操作Python解释器去运行代码时候更加方便）

  ```
  - 写了30个Python代码，想要使用解释器去运行。
      C:\Python39\python.exe Y:\hello1.py
      C:\Python39\python.exe Y:\hello2.py
      ...
      C:\Python39\python.exe Y:\hello10.py
  
  - 然你以后可以方便的去运行代码，不用再写Python解释器所在的路径。   
      只要你将 C:\Python39 路径添加到系统的环境变量中。以后你在终端就可以：
          python.exe Y:\hello1.py
          
  - 如何将 C:\Python39 添加到环境变量呢？【默认在解释器安装的时已自动添加到环境变量了】
  ```


4.2 安装Pycharm编辑器（mac)

帮助我们快速编写代码，用Pycharm可以大大的提高咱们写代码的效率。 +  用解释器去运行代码。

```python
print("asdfasdf")
```

- 下载Pycharm

  ```
  https://www.jetbrains.com/pycharm/
  ```

- 安装

- 快速使用，写代码+运行代码

- 破解Pycharm（专业版）

4.3 安装Pycharm编辑器（win)

- 下载Pycharm

  ```
  https://www.jetbrains.com/pycharm/download/other.html
  ```

- 安装

- 快速使用：编写代码 + 运行代码

- 破解Pycharm（专业版）

# 二 python基础

## 1 编码

#### 编码简介

编码，文字和二进制之间的一个对照表。

**计算机中所有的数据本质上都是以0和1的组合来存储**。

在计算机中会将中文内存转换成 01010101010... ，最终存储到硬盘上。

在计算机中有这么一个编码的概念（密码本）。

```
    武     ->      01111111 00011010 010110110
    沛     ->      01001111 10010000 001110100
    齐     ->      11111111 00000000 010101010
```

在计算机中有很多种编码。

```
每种编码都有自己的一套密码本，都维护这自己的一套规则，如：
    utf-8编码：
        武     ->      01111111 00011010 010110110
        沛     ->      01001111 10010000 001110100
        齐     ->      11111111 00000000 010101010
    gbk编码：
        武     ->      11111111 00000010
        沛     ->      01001111 01111111
        齐     ->      00110011 10101010
所以，使用的不同的编码保存文件时，硬盘的文件中存储的0/1也是不同的。
```



注意事项：以某个编码的形式进行保存文件，以后就要以这种编码去打开这个文件。否则就会出现乱码。

```
UTF-8编码去保存武沛齐：01111111 00011010 010110110 01001111 10010000 001110100 11111111 00000000 010101010
GBK编码形式去打开：乱码
```

#### 1 ascii编码

ascii规定使用1个字节来表示字母与二进制的对应关系。

```
00000000
00000001    w
00000010    B
00000011    a
...
11111111

2**8 = 256
```





#### 2 gbk-2312编码

gb-2312编码，由国家信息标准委员会制作（1980年）。

gbk编码，对gb2312进行扩展，包含了中日韩等文字（1995年）。

在与二进制做对应关系时，由如下逻辑：

- 单字节表示，用一个字节表示对应关系。2**8 = 256
- 双字节表示，用两个字节表示对应关系。2**16 = 65536中可能性。



#### 3 unicode

unicode也被称为万国码，为全球的每个文字都分配了一个码位（二进制表示）。

- ucs2 

  ```
  用固定的2个字节去表示一个文字。
  
  00000000 00000000     悟
  ...
  
  2**16 = 65535
  ```

- ucs4

  ```
  用固定的4个字节去表示一个文字。
  00000000 00000000 00000000 00000000  无
  ...
  2**32 = 4294967296
  ```

  

```
文字     十六进制            二进制 
 ȧ        0227           1000100111
 ȧ        0227         00000010 00100111                       ucs2
 ȧ        0227         00000000 00000000 00000010 00100111     ucs4
 
 乔       4E54           100111001010100
 乔       4E54         01001110 01010100                       ucs2
 乔       4E54         00000000 00000000 01001110 01010100     ucs4
 
 😆      1F606        11111011000000110
 😆      1F606        00000000 00000001 11110110 00000110      ucs4
```



无论是ucs2和ucs4都有缺点：浪费空间？

```python
文字     十六进制     二进制
A        0041      01000001
A        0041      00000000 01000001
A        0041      00000000 00000000 00000000 01000001
```

unicode的应用：在文件存储和网络传输时，不会直接使用unicode，而在内存中会unicode
	。

#### 4 utf-8编码

包含所有文字和二进制的对应关系，全球应用最为广泛的一种编码（站在巨人的肩膀上功成名就）。

本质上：utf-8是对unicode的压缩，用尽量少的二进制去与文字进行对应。

```
  unicode码位范围            utf-8      
   0000 ~ 007F              用1个字节表示
   0080 ~ 07FF              用2个字节表示
   0800 ~ FFFF              用3个字节表示
  10000 ~ 10FFFF            用4个字节表示
```

具体压缩的流程：

- 第一步：选择转换模板

  ```
    码位范围（十六进制）                转换模板
     0000 ~ 007F              0XXXXXXX
     0080 ~ 07FF              110XXXXX 10XXXXXX
     0800 ~ FFFF              1110XXXX 10XXXXXX 10XXXXXX
    10000 ~ 10FFFF            11110XXX 10XXXXXX 10XXXXXX 10XXXXXX
    
    例如：
        "B"  对应的unicode码位为 0042，那么他应该选择的一个模板。
        "ǣ"  对应的unicode码位为 01E3，则应该选择第二个模板。
        "武" 对应的unicode码位为 6B66，则应该选择第三个模板。
        "沛" 对应的unicode码位为 6C9B，则应该选择第三个模板。
        "齐" 对应的unicode码位为 9F50，则应该选择第三个模板。
         😆  对应的unicode码位为 1F606，则应该选择第四个模板。            
  
  注意：一般中文都使用第三个模板（3个字节），这也就是平时大家说中文在utf-8中会占3个字节的原因了。
  ```

- 第二步：在模板中填入数据

  ```
  - "武"  ->  6B66  ->  110 101101 100110
  - 根据模板去套入数据
  	1110XXXX 10XXXXXX 10XXXXXX
  	1110XXXX 10XXXXXX 10100110
  	1110XXXX 10101101 10100110
  	11100110 10101101 10100110
  在UTF-8编码中 ”武“  11100110 10101101 10100110
  
  - 😆  ->  1F606  ->  11111 011000 000110
  - 根据模板去套入数据
  	11110000 10011111 10011000 10000110
  ```

  

#### 5 Python相关的编码

```
字符串（str）     "alex媳妇叫铁锤"             unicode处理               一般在内存
字节（byte）      b"alexfdsfdsdfskdfsd"      utf-8编码 or gbk编码       一般用于文件或网络处理
```

```python
v1 = "武"

v2 = "武".encode("utf-8")
v2 = "武".encode("gbk")
```

将一个字符串写入到一个文件中。

```python
name = "嫂子热的满身大汗"
data = name.encode("utf-8")

# 打开一个文件
file_object = open("log.txt",mode="wb")
# 在文件中写内容
file_object.write(data)
# 关闭文件
file_object.close()
```

1. 基于Python实现将字符串转换为字节（utf-8编码）

   ```python
   # 字符串类型
   name = "武沛齐"
   
   print(name) # 武沛齐
   # 字符串转换为字节类型
   data = name.encode("utf-8")
   print(data) # b'\xe6\xad\xa6\xe6\xb2\x9b\xe9\xbd\x90'
   
   # 把字节转换为字符串
   old = data.decode("utf-8")
   print(old)
   ```

2. 基于Python实现将字符串转换为字节（gbk编码）

   ```python
   # 字符串类型
   name = "武沛齐"
   print(name) # 武沛齐
   # 字符串转换为字节类型
   data = name.encode("gbk")
   # print(data) # b'\xe6\xad\xa6\xe6\xb2\x9b\xe9\xbd\x90'  utf8，中文3个字节
   print(data) # b'\xce\xe4\xc5\xe6\xc6\xeb'              gbk，中文2个字节
   
   # 把字节转换为字符串
   old = data.decode("gbk")
   print(old)
   ```

   

## 2.进制

计算机中底层所有的数据都是以 `010101`的形式存在（图片、文本、视频等）。

- 二进制

  ```python
  0
  1
  10
  ```

  ![截屏2020-10-25 下午5.36.39](C:\Users\Administrator\Desktop\python笔记\python神功.assets\截屏2020-10-25 下午5.36.39.png)

- 八进制

- 十进制

- 十六进制

<img src="C:\Users\Administrator\Desktop\python笔记\python神功.assets\image-20201025174321969.png" alt="image-20201025174321969" style="zoom: 50%;" />

###  进制转换

<img src="C:\Users\Administrator\Desktop\python笔记\python神功.assets\image-20201025180124802.png" alt="image-20201025180124802" style="zoom:50%;" />

```python
v1 = bin(25) # 十进制转换为二进制
print(v1) # "0b11001"

v2 = oct(23) # 十进制转换为八进制
print(v2) # "0o27"

v3 = hex(28) # 十进制转换为十六进制
print(v3) # "0x1c"
```

```python
i1 = int("0b11001",base=2) # 25

i2 = int("0o27",base=8) # 23 

i3 = int("0x1c",base=16) # 28 
```

## 3. 计算机中的单位

由于计算机中本质上所有的东西以为二进制存储和操作的，为了方便对于二进制值大小的表示，所以就搞了一些单位。

- b（bit），位

  ```
  1，1位
  10，2位
  111，3位
  1001，4位
  ```

- B（byte），字节

  ```
  8位是一个字节。
  
  10010110，1个字节
  10010110 10010110，2个字节
  ```

- KB（kilobyte），千字节

  ```
  1024个字节就是1个千字节。
  
  10010110 11010110  10010111 .. ，1KB
  1KB = 1024B= 1024 * 8 b
  ```

- M（Megabyte），兆

  ```
  1024KB就是1M
  1M= 1024KB = 1024 * 1024 B = 1024 * 1024 * 8 b
  ```

- G（Gigabyte），千兆

  ```
  1024M就是1G
  1 G=  1024 M=  1024 *1024KB =  1024 * 1024 * 1024 B =  1024 * 1024 * 1024 * 8 b
  ```

- T（Terabyte），万亿字节

  ```
  1024个G就是1T
  ```

- ...其他更大单位 PB/EB/ZB/YB/BB/NB/DB 不再赘述。













# 三 常用基本功能

## 1 变量 注释 输入输出

#### 变量

变量，其实就是我们生活中起别名和外号，让变量名指向某个值，格式为： 【变量名 = 值】，以后可以通过变量名来操作其对应的值。

```python
name = "武沛齐"
print(name) # 武沛齐
```

- 全局变量，大写 & 大写下划线连接，例如：`NAME = "武沛齐"` 、`BASE_NAME = 18`
- 局部变量，小写 & 小写下划线连接，例如：`data = [11,22,33]`、`user_parent_id = 9`等。

变量名的规范三个规范（只要有一条就会报错）：

- 变量名只能由 字母、数字、下划线 组成。
- 不能以数字开头
- 不能用Python内置的关键字

两个建议：

- 下划线连接命名（小写）
- 见名知意

#### 注释 

1. 单行注释 #

   ```python
   # 声明一个name变量
   name = "alex"
   age = 19 # 这表示当前用户的年龄
   
   ```

2. 多行注释#  """  """

   ```python
   # 声明一个name变量
   # 声明一个name变量
   # 声明一个name变量
   name = "alex"
   """
   多行注释内容
   多行注释内容
   多行注释内容
   """
   age = 19输入输出
   ```

   



#### 输入输出

input输入

print输出

```python
# download_size 已下的大小
# file_size实际大小
# round  四舍五入几位小数
# 进度条原地打印
percent = "\r{}%".format(int(round(download_size / file_size, 2) * 100))  # \r可把输出在同一行
            print(percent, end="")
```



输入，可以实现程序和用户之间的交互

**特别注意**：用户输入的任何内容本质上都是字符串

```python
# 1. 右边 input("请输入用户名：") 是让用户输入内容。
# 2. 将用户输入的内容赋值给name变量。
name = input("请输入用户名：")
if name == "alex":
  print("登录成功")
else:
  print("登录失败")
```



## 2 条件判断语句

if ：

elif  ：

else：

```
if 条件A:
  A成立，执行此缩进中的所有代码
  ...
elif 条件B:
  B成立，执行此缩进中的所有代码
  ...
elif 条件C:
  C成立，执行此缩进中的所有代码
  ...
else:
  上述ABC都不成立。
```

```python
num = input("请输入数字")
data = int(num)
if data>6:
  print("太大了")
elif data == 6:
  print("刚刚好")
else:
  print("太小了")
```

## 3 循环

break：

用于在while循环中帮你终止循环。

```python
print("开始")
while True:
	print("1")
  break
	print("2")
print("结束")

# 输出
开始
1
结束
```

continue:

在循环中用于 结束本次循环，开始下一次循环

```python
print("开始")
while True:
	print("红旗飘飘，军号响。")
	continue
	print("剑已出鞘，雷鸣电闪。")
	print("从来都是狭路相逢勇者胜。")
print("结束")

# 输出
开始
红旗飘飘，军号响。
红旗飘飘，军号响。
红旗飘飘，军号响。
红旗飘飘，军号响。
...
```

range:

range，帮助我们创建一系列的数字

```python
range(10) # [0,1,2,3,4,5,6,7,8,9]
range(1,10) # [1,2,3,4,5,6,7,8,9]
range(1,10,2) # [1,3,5,7,9]
range(10,1,-1) # [10,9,8,7,6,5,4,3,2]
```

#### while循环：

条件成立一直执行

```python
print("开始")
while True:
	print("1")
    break  #终止循环
```

#### for循环：

- for循环

- range，帮助我们创建一系列的数字

  ```python
  range(10) # [0,1,2,3,4,5,6,7,8,9]
  range(1,10) # [1,2,3,4,5,6,7,8,9]
  range(1,10,2) # [1,3,5,7,9]
  range(10,1,-1) # [10,9,8,7,6,5,4,3,2]
  ```

- For + range

  ```python
  for i in range(10):
      print(i）
  ```


else:

 当while后的条件不成立时，else中的代码

```python
while 条件:
  代码
else:
  代码
```

## 4 运算符

- #### 算数运算符

- 例如：加减乘除

  <img src="C:\Users\Administrator\Desktop\python笔记\python神功.assets\image-20201011165419956.png" alt="image-20201011165419956"  />

  ```python
  print( 9//2 )
  ```

- #### 比较运算符

- 例如：大于、小于

  <img src="C:\Users\Administrator\Desktop\python笔记\python神功.assets\image-20201011165434014.png" alt="image-20201011165434014"  />

  注意：python3中不支持 `<>`

  ```python
  if 1 >2:
    pass
  while 1>2:
    pass
  
  data = 1 == 2
  ```

- #### 赋值运算

- 例如：变量赋值

  <img src="C:\Users\Administrator\Desktop\python笔记\python神功.assets\image-20201011165501909.png" alt="image-20201011165501909"  />

  ```python
  num = 1
  while num < 100:
    print(num)
    # num = num + 1
    num += 1
  ```

- #### 成员运算

- 例如：是否包含

  <img src="C:\Users\Administrator\Desktop\python笔记\python神功.assets\image-20201011165515812.png" alt="image-20201011165515812"  />

  ```python
  v1 = "le" in "alex"  # True/False
  # 让用户输入一段文本，检测文本中是否包含敏感词。
  text = input("请输入内容：")
  if "苍老师" in text:
    print("少儿不宜")
  else:
    print(text)
  ```

- #### 逻辑运算

- 例如：且或非

  <img src="C:\Users\Administrator\Desktop\python笔记\python神功.assets\image-20201011165530169.png" alt="image-20201011165530169"  />

  ```python
  if username == "alex" and pwd == "123":
    pass
  
  data = 1 > 2
  if not data:
    pass
  ```

  

####  运算符优先级

运算符的优先级有很多，常见的没几个，推荐你记住3个即可：

- 算数优先级优先级 大于 比较运算符

  ```python
  if 2 + 10 > 11:
  	print("真")
  else:
  	print("假")
  ```

- 比较运算符优先级 大于 逻辑运算符

  ```python
  if 1>2 and 2<10:
  	print("成立")
  else:
  	print("不成立")
  ```

- 逻辑运算符内部三个优先级 not > and > or

  ```python
  if not 1 and 1>2 or 3 == 8:
  	print("真")
  else:
  	print("假")
  ```

上述这3个优先级从高到低总结：`加减乘除 > 比较 > not and or `。绝招：加括号。

## 5. 其它补充

#### pass 

一般Python的代码块是基于 `:` 和`缩进`来实现，Python中规定代码块中必须要有代码才算完整，在没有代码的情况下为了保证语法的完整性可以用pass代替

#### is 比较

`is` 和 `==`的区别是什么？

- `==`，用于比较两个值是否相等。
- is，用于表示内存地址是否一致。

#### 位运算

计算机底层本质上都是二进制，我们平时在计算机中做的很多操作底层都会转换为二进制的操作，位运算就是对二进制的操作。

- `&`，与（都为1）

  ```python
  a = 60            # 60 = 0011 1100 
  b = 13            # 13 = 0000 1101 
  
  c = a & b         # 12 = 0000 1100
  ```

- `|`，或（只要有一个为1）

  ```python
  a = 60            # 60 = 0011 1100 
  b = 13            # 13 = 0000 1101 
  
  c = a | b         # 61 = 0011 1101 
  ```

- `^`，异或（值不同）

  ```python
  a = 60            # 60 = 0011 1100 
  b = 13            # 13 = 0000 1101 
  
  c = a ^ b         # 49 = 0011 0001 
  ```

- `~`，取反

  ```python
  a = 60            #  60 = 0011 1100 
  
  c = ~a;           # -61 = 1100 0011
  ```

- `<<`，左移动

  ```python
  a = 60            #  60 = 0011 1100
  c = a << 2;       # 240 = 1111 0000
  ```

- `>>`，右移动

  ```python
  a = 60            # 60 = 0011 1101 
  c = a >> 2;       # 15 = 0000 1111
  ```

平时在开发中，二进制的位运算几乎很好少使用，在计算机底层 或 网络协议底层用的会比较多，例如：

- 计算  2**n

  ```python
  2**0    1 << 0   1     1
  2**1    1 << 1   10    2
  2**2    1 << 2   100   4
  2**3    1 << 3   1000  8
  ...
  ```









## 三元运算

简单的条件语句，可以基于三元运算实现，例如：

 `结果 =  条件成立时    if   条件   else   不成立`

```python
num = input("请写入内容")
data = "臭不要脸" if "苍老师" in num else "正经人"
print(data)
```

lambda表达式和三元运算没有任何关系，属于两个独立的知识点。

掌握三元运算之后，以后再编写匿名函数时，就可以处理再稍微复杂点的情况了，例如：

```python
func = lambda x: "大了" if x > 66 else "小了"

v1 = func(1)
print(v1) # "小了"

v2 = func(100)
print(v2) # "大了"
```



## 生成器

生成器是由函数+yield关键字创造出来的写法，在特定情况下，用他可以帮助我们节省内存。

生成器的特点是，记录在函数中的执行位置，下次执行next时，会从上一次的位置基础上再继续向下执行。

 执行生成器函数func，返回的生成器对象。注意：执行生成器函数时，函数内部代码不会执行。

- 用`next()`执行生成器函数，或者循环

##### yield关键字

```python
def func():
    print(111)
    yield 1 # 有yield关键字变成生成器，遇到yield停止运行并返回数据。

    print(222) # 再次执行时接着执行下面的
    yield 2

    print(333)
    yield 3

    print(444) # 这里会报错，没有yield
    
data = func() # 返回的生成器对象

v1 = next(data) # 用next()执行生成器
print(v1)

v2 = next(data)
print(v2)

v3 = next(data)
print(v3)

v4 = next(data)
print(v4) 
```

```python
data = func()

for item in data:
    print(item)
```

#####  yield from 关键字

在生成器部分我们了解了yield关键字，其在python3.3之后有引入了一个yield from。

```python
def foo():
    yield 2
    yield 2
    yield 2


def func():
    yield 1
    yield 1
    yield 1
    yield from foo()
    yield 1
    yield 1


for item in func():
    print(item)
```

















## 内置函数

<img src="assets/image-20201230201618164.png" alt="image-20201230201618164" style="zoom:50%;" />

### 运算相关

- abs，绝对值（把负转正）

  ```python
  v = abs(-10)
  ```

- pow，指数（次方）

  ```python
  v1 = pow(2,5) # 2的5次方  2**5
  print(v1)
  ```

- sum，求和

  ```python
  v1 = sum([-11, 22, 33, 44, 55]) # 可以被迭代-for循环
  print(v1)
  ```

- divmod，求商和余数

  ```
  v1, v2 = divmod(9, 2)
  print(v1, v2)
  ```

- round，小数点后n位（四舍五入）

  ```python
  v1 = round(4.11786, 2)
  print(v1) # 4.12
  ```







### 数字相关

- min，最小值

  ```python
  v1 = min(11, 2, 3, 4, 5, 56)
  print(v1) # 2
  ```

  ```
  v2 = min([11, 22, 33, 44, 55]) # 迭代的类型（for循环）
  print(v2) # 11
  ```

  ```python
  v3 = min([-11, 2, 33, 44, 55], key=lambda x: abs(x))
  print(v3) # 2
  ```

- max，最大值

  ```python
  v1 = max(11, 2, 3, 4, 5, 56)
  print(v1)
  
  v2 = max([11, 22, 33, 44, 55])
  print(v2)
  ```

  ```python
  v3 = max([-11, 22, 33, 44, 55], key=lambda x: x * 10)
  print(v3) # 55
  ```

- all，是否全部为True

  ```python
  v1 = all(   [11,22,44,""]   ) # False
  ```

- any，是否存在True

  ```python
  v2 = any([11,22,44,""]) # True
  ```

  

### 进制转换相关

- bin，十进制转二进制
- oct，十进制转八进制
- hex，十进制转十六进制



### unicode码点

- ord，获取字符对应的unicode码点（十进制）

  ```
  v1 = ord("武")
  print(v1, hex(v1))
  ```

- chr，根据码点（十进制）获取对应字符

  ```python
  v1 = chr(27494)
  print(v1)
  ```



### 类型相关

- int

- foat

- str，unicode编码

- bytes，utf-8、gbk编码

  ```python
  v1 = "武沛齐"  # str类型
  
  v2 = v1.encode('utf-8')  # bytes类型
  
  v3 = bytes(v1,encoding="utf-8") # bytes类型
  ```

- bool

- list

- dict

- tuple

- set



### 常用

- len ，获取长度，字符串是数字，字节是字节大小

- print

- input

- open，打开文件

- type，获取数据类型

  ```python
  v1 = "123"
  
  if type(v1) == str:
      pass
  else:
      pass
  ```

- range 

  ```python
  range(10)
  ```

- enumerate，for循环列表时打印出序号

  ```python
  v1 = ["武沛齐", "alex", 'root']
  
  for num, value in enumerate(v1, 1):
      print(num, value)
  ```

- id,获取内存地址

- hash

  ```python
  v1 = hash("武沛齐")
  ```

- help，帮助信息

  - pycharm，不用
  - 终端，使用

- zip，打竖取值

  ```python
  v1 = [11, 22, 33, 44, 55, 66]
  v2 = [55, 66, 77, 88]
  v3 = [10, 20, 30, 40, 50]
      
  result = zip(v1, v2, v3)
  for item in result:
      print(item)
  ```

- callable，是否可执行，后面是否可以加括号。

  ```
  v1 = "武沛齐"
  v2 = lambda x: x
  def v3():
      pass
  
  
  print( callable(v1) ) # False
  print(callable(v2))
  print(callable(v3))
  ```

- sorted，排序

  ```python
  v1 = sorted([11,22,33,44,55])
  ```

  ```python
  info = {
      "wupeiqi": {
          'id': 10,
          'age': 119
      },
      "root": {
          'id': 20,
          'age': 29
      },
      "seven": {
          'id': 9,
          'age': 9
      },
      "admin": {
          'id': 11,
          'age': 139
      },
  }
  
  result = sorted(info.items(), key=lambda x: x[1]['id'])
  print(result)
  ```

  ```python
  data_list = [
      '1-5 编译器和解释器.mp4',
      '1-17 今日作业.mp4',
      '1-9 Python解释器种类.mp4',
      '1-16 今日总结.mp4',
      '1-2 课堂笔记的创建.mp4',
      '1-15 Pycharm使用和破解（win系统）.mp4',
      '1-12 python解释器的安装（mac系统）.mp4',
      '1-13 python解释器的安装（win系统）.mp4',
      '1-8 Python介绍.mp4', '1-7 编程语言的分类.mp4',
      '1-3 常见计算机基本概念.mp4',
      '1-14 Pycharm使用和破解（mac系统）.mp4',
      '1-10 CPython解释器版本.mp4',
      '1-1 今日概要.mp4',
      '1-6 学习编程本质上的三件事.mp4',
      '1-18 作业答案和讲解.mp4',
      '1-4 编程语言.mp4',
      '1-11 环境搭建说明.mp4'
  ]
  result = sorted(data_list, key=lambda x: int(x.split(' ')[0].split("-")[-1]) )
  print(result)
  ```

  



## 推导式

推导式是Python中提供了一个非常方便的功能，可以让我们通过一行代码实现创建list、dict、tuple、set 的同时初始化一些值。

- 列表

  ```python
  num_list = [ i for i in range(10)]
  
  num_list = [ [i,i] for i in range(10)]
  
  num_list = [ [i,i] for i in range(10) if i > 6 ]
  ```

- 集合

  ```python
  num_set = { i for i in range(10)}
  
  num_set = { (i,i,i) for i in range(10)}
  
  num_set = { (i,i,i) for i in range(10) if i>3}
  ```

- 字典

  ```python
  num_dict = { i:i for i in range(10)}
  
  num_dict = { i:(i,11) for i in range(10)}
  
  num_dict = { i:(i,11) for i in range(10) if i>7}
  ```

- 元组，<span style="color:red">不同于其他类型。</span>

  ```python
  # 不会立即执行内部循环去生成数据，而是得到一个生成器。
  data = (i for i in range(10))
  print(data)
  for item in data:
      print(item)
  ```

 看代码写结果（新浪微博面试题）

```python
data_list = [lambda x: x + i for i in range(10)]  # [函数,函数,函数]   i=9

v1 = data_list[0](100)
v2 = data_list[3](100)
print(v1, v2)  # 109 109
```







## 常用方法

| 方法名      | 参数               | 使用方法                      | 描述                                                 |
| ----------- | ------------------ | ----------------------------- | ---------------------------------------------------- |
| eval()      | 字符串             | eval("{"key":"val"}")         | 可以把一些字符串编码成python能执行的对象类型或者方法 |
| locals()    | 空                 | locals()                      | 把当前作用域的所有变量调用合成字典    {变量名：值}   |
| enumerate() | 列表元组字典字符等 | for x,y in enumerate([a,b,c]) | 遍历一个集合对象，遍历同时得到索引及元素。           |



# 四 数据类型

## 1 整形（int）

整型其实就是十进制整数的统称，比如：1、68、999都属于整型。且支持 加/减/乘/除/取余/指数 等操作。

 **定义**

```python
number = 10
age = 99
```

**方法**

无

公共功能

加减乘除

```python
v1 = 4
v2 = 8
v3 = v1 + v2
```

转换

在项目开发和面试题中经常会出现一些 "字符串" 和 布尔值 转换为 整型的情况。

```python
# 布尔值转整型
n1 = int(True)  # True转换为整数 1
n2 = int(False) # False转换为整数 0

# 字符串转整型
v1 = int("186",base=10) # 把字符串看成十进制的值，然后再转换为 十进制整数，结果：v1 = 186
v2 = int("0b1001",base=2) # 把字符串看成二进制的值，然后再转换为 十进制整数，结果：v1 = 9 (0b表示二进制)
v3 = int("0o144",base=8)  # 把字符串看成八进制的值，然后转换为 十进制整数，结果：v1 = 100 (0o表示八进制)
v4 = int("0x59",base=16)  # 把字符串看成十六进制的值，然后转换为 十进制整数，结果：v1 = 89 （0x表示十六进制）

# 浮点型（小数）
v1 = int(8.7) # 8
```

所以，如果以后别人给你一个按 二进制、八进制、十进制、十六进制 规则存储的字符串时，可以轻松的通过int转换为十进制的整数。

其他

1 长整型

- Python3：整型（无限制）
- Python2：整型、长整形

在python2中跟整数相关的数据类型有两种：int(整型)、long（长整型），他们都是整数只不过能表示的值范围不同。

<img src="C:\Users\Administrator\Desktop\python笔记\python神功.assets\image-20201102190227431.png" alt="image-20201102190227431" style="zoom:50%;" />

- int，可表示的范围：-9223372036854775808～9223372036854775807
- long，整数值超出int范围之后自动会转换为long类型（无限制）。

在python3中去除了long只剩下：int（整型），并且 int 长度不在限制。

2 地板除

- Py3：

  ```python
  v1 = 9/2 
  print(v1) # 4.5
  ```

- py2:

  ```python
  v1 = 9/2 
  print(v1) # 4
  ```

  ```python
  from __future__ import division 
  
  v1 = 9/2 
  print(v1) # 4.5
  ```

  



## 2 字符串（str）

字符串，其实就是我们生活中的文本信息。字符串有一个特点，他必须由引号引起来。

字符串，不可变，即：创建好之后内部就无法修改。【独有功能都是新创建一份数据】

### 字符串方法

1.判断字符串是否以 XX 开头？得到一个布尔值

- **startswith（）**

  ```python
  v1 = "学如初出之苗"
  result = v1.startswith("学如")
  print(result) # 值为True
  ```

2.判断字符串是否以 XX 结尾？得到一个布尔值

- **endswith（）**

  ```python
  v1 = "不见其增"
  result = v1.endswith("增")
  print(result) # 值为True
  ```

3.判断字符串是否为十进制数？得到一个布尔值

- **isdecimal()**

  ```python
  v1 = "1238871"
  result = v1.isdecimal()
  print(result) # True
  ```

4.去除字符串两边的 空格、换行符、制表符，得到一个新字符串

注：（）内可去除字符串两边指定的内容

- **strip()**

  ```python
  msg =  "  日有所长 " 
  data = msg.strip()
  print(data) # 将msg两边的空白去掉，得到"日有所长"
  ```

- **lstrip()**

  去除字符串左边的 空格、换行符、制表符或自定内容

- **rstrip()**

  去除字符串右边的 空格、换行符、制表符或自定内容

5.字符串字母变大写小写，得到一个新字符串

- **upper()**   大写
- **lower()**   小写

6.字符串内容替换，得到一个新的字符串

- **replace("查找","替换")**

  ```python
  data = "惰如磨刀之石，不见其增"
  value = data.replace("不见其增","日有所耗")
  print(data)  # "惰如磨刀之石，不见其增"
  print(value) #"惰如磨刀之石，日有所耗"
  ```

  

7.字符串切割，得到一个列表

- **split()**  括号内设要分割的字符

  

8.列表拼接，得到一个新的字符串

- **" ".join( )**   `（）`内放列表  `" "`里面放变字符串后的分隔符，可空

  ```python
  data_list = ["alex","是","大烧饼"]
  v1 = "_".join(data_list) # alex_是_大烧饼
  print(v1)# alex_是_大烧饼
  ```



9.字符串转换为字节类型,及字节转字符

- **encode("utf-8")**   括号内填要以什么编码转换可"gbk"

  ```python
  data = "嫂子"  # unicode，字符串类型
  v1 = data.encode("utf-8")  # utf-8，字节类型
  print(v1)  # b'\xe5\xab\x82 \xe5\xad\x90'
  ```

- **decode("utf-8")**    字节转回字符

  ```python
  s1 = v1.decode("utf-8") # 嫂子
  print(s1)# 嫂子
  ```

  

10.将字符串内容居中、居左、居右展示

```python
v1 = "王老汉"
data = v1.center(21, "-")
print(data) #---------王老汉---------中

data = v1.ljust(21, "-")
print(data) # 王老汉------------------左

data = v1.rjust(21, "-")
print(data) # ------------------王老汉 右
```



11.帮助你在字符串前填充0，应用场景：处理二进制数据

```python
data = "101" 
v1 = data.zfill(8)
print(v1) # "00000101"
```



12.字符串格式化

字符串格式化，使用跟便捷的形式实现字符串的拼接

- format（推荐）

```python
text = "我叫{0}，今年{1}岁".format("武沛齐",18)
text = "我叫{}，今年{}岁".format("武沛齐",18)
```

- f

到Python3.6版本，更便捷

```python
name = "alex"
text = f"我是{name}，我爱大铁锤"
```



### 字符通用的功能

1. 相加：字符串 + 字符串

   ```python
   v1 = "alex" + "大sb"
   print(v1)
   ```

2. 相乘：字符串 * 整数

   ```python
   data = "嫂子" * 3
   print(data) # 嫂子嫂子嫂子
   ```

3. 长度

   ```python
   data = "嫂子满身大汉"
   value = len(data) 
   print(value) # 6
   ```

4. 获取字符串中的字符，索引

   ```python
   a = "一二三四五"
   a[0]#一
   a[-1]#五
   ```

   注意：字符串中是能通过索引取值，无法修改值。【字符串在内部存储时不允许对内部元素修改，想修改只能重新创建。】

   

5. 获取字符串中的子序列，切片

   ```python
   message = "一二三"
   print(message[0:2]) # "一二"
   ```

   注意：字符串中的切片只能读取数据，无法修改数据。【字符串在内部存储时不允许对内部元素修改，想要修改只能重新创建】

   

6. 步长，跳着去字符串的内容

   ```python
   name = "生活不是电影，生活比电影苦"
   
   print( name[ 0:5:2 ] )   # 输出：生不电 【前两个值表示区间范围，最有一个值表示步长】
   print( name[ :8:2 ] )    # 输出：生不电，  【区间范围的前面不写则表示起始范围为0开始】、
   print( name[ 2::3 ] )    # 输出：不电，活电苦 【区间范围的后面不写则表示结束范围为最后】
   print( name[ ::2 ] )     # 输出：生不电，活电苦 【区间范围不写表示整个字符串】
   print( name[ 8:1:-1 ] )  # 输出：活生，影电是不 【倒序】
   ```


7.可用while循环for循环

8.转换 ，一般情况下，只有整型转字符串才有意义。

9.其他，字符串不可被修改













## 3 布尔类型（bool）

布尔类型中共有两个值：True / False

    整数0、空字符串、空列表、空元组、空字典转换为布尔值时均为False
    其他均为True

如果在 `if` 、`while` 条件后面写一个值当做条件时，他会默认转换为布尔类型，然后再做条件判断



## 4 列表类型（list）

列表（list），是一个**有序**且**可变**的容器，在里面可以存放**多个不同类型**的元素。

列表，可变，创建好之后内部元素可以修改【独有功能基本上都是直接操作列表内部，不会创建新的一份数据】

列表属于容器，内部可以存放各种数据，所以他也支持列表的嵌套

#### 定义列表

```python
a = []
a = list()
b = [1,2,3,4]
```

#### 列表方法

1. **append( )**     

   追加，在原列表中尾部追加值。

   ```python
   a = []
   v1 = input("请输入姓名")
   a.append(v1)
   print(a) # ["alex","eric"]
   ```

2. **extend( )**  

   批量追加，将一个列表中的元素逐一添加另外一个列表。

   ```python
   tools = ["搬砖","菜刀","榔头"]
   tools.extend( [11,22,33] ) # weapon中的值逐一追加到tools中
   print(tools) # ["搬砖","菜刀","榔头",11,22,33]
   ```

3. **insert(   )**   括号内第一个值选索引，第二个值内容

   插入，在原列表的指定索引位置插入值

   ```python
   a  = []
   a.insert(0,"廖")
   print(a)
   ```

4. **remove( )**

   在原列表中根据值删除（从左到右找到第一个删除）【慎用，里面没有会报错】

   ```python
   a = ["王宝强","陈羽凡","Alex","贾乃亮","Alex"]
   a.remove("Alex")
   print(a)
   ```

5. **pop()**

   在原列表中根据索引踢出某个元素（根据索引位置删除）

   ```python
   user_list = ["王宝强","陈羽凡","Alex","贾乃亮","Alex"]
                  0       1      2      3       4
   user_list.pop(1)
   print(user_list) #  ["王宝强","Alex","贾乃亮","Alex"]
   ```

6. **clear()**

   清空原列表

   ```python
   user_list = ["王宝强","陈羽凡","Alex","贾乃亮","Alex"]
   user_list.clear()
   print(user_list) # []
   ```

7. 根据值获取索引

   ```python
   b = ["王宝强","陈羽凡","Alex","贾乃亮","Alex"]
   a = b.index("Alex")#4
   ```


8. **reverse()**

   反转原列表

   ```python
   user_list = ["王宝强","陈羽凡","Alex","贾乃亮","Alex"]
   user_list.reverse()
   print(user_list)
   ```

9. **sort()**

   列表元素排序 可字符串和数字排序

    注意：排序时内部元素无法进行比较时，程序会报错（尽量数据类型统一）

   ```python
   # 数字排序
   num_list = [11, 22, 4, 5, 11, 99, 88]
   print(num_list)
   num_list.sort()  # 让num_list从小到大排序
   num_list.sort(reverse=True)  # # 让num_list从大到小排序
   print(num_list)
   ```

#### 列表的通用功能

1. 相加，两个列表相加获取生成一个新的列表。

2. 相乘，列表*整型 将列表中的元素再创建N份并生成一个新的列表。

3. 运算符in包含
   由于列表内部是由多个元素组成，可以通过in来判断元素是否在列表中。

   ```python
   user_list = ["狗子","二蛋","沙雕","alex"] 
   result = "alex" in user_list
   ```

   ```python
   # 案例：敏感词替换
   text = input("请输入文本内容：") # 按时打发第三方科技爱普生豆腐啊；了深刻的房价破阿偶打飞机
   forbidden_list = ["草","欧美","日韩"]
   for item in forbidden_list:
       text = text.replace(item,"**")
   print(text)
   ```

   注意：**列表检查元素是否存在时，是采用逐一比较的方式，效率会比较低。**

4. **len( )**  获取长度

   ```python
   user_list = ["范德彪","刘华强",'尼古拉斯赵四']
   print( len(user_list) )
   ```

5. 索引，一个元素的操作

   索引读

   ```python
   user_list = ["范德彪","刘华强",'尼古拉斯赵四']
   print( user_list[0] )
   print( user_list[2] )
   print( user_list[3] ) # 报错
   ```

   索引改

   ```python
   user_list = ["范德彪","刘华强",'尼古拉斯赵四']
   user_list[0] = "武沛齐"
   print(user_list) # ["武沛齐","刘华强",'尼古拉斯赵四']
   ```

   索引删

   ```python
   user_list = ["范德彪","刘华强",'尼古拉斯赵四']
   del user_list[1]
   
   user_list.remove("刘华强")
   ele = user_list.pop(1)
   ```

   注意：超出索引范围会报错。
   提示：由于字符串是不可变类型，所以他只有索引读的功能，而列表可以进行 读、改、删

6. 切片，多个元素的操作（很少用）

   切片读

   ```python
   user_list = ["范德彪","刘华强",'尼古拉斯赵四']
   print( user_list[0:2] ) # ["范德彪","刘华强"]
   ```

   切片改

   ```python
   user_list = ["范德彪", "刘华强", '尼古拉斯赵四']
   user_list[0:2] = [11, 22, 33, 44]
   print(user_list) # 输出 [11, 22, 33, 44, '尼古拉斯赵四']
   ```

   切片删

   ```python
   user_list = ["范德彪", "刘华强", '尼古拉斯赵四']
   del user_list[1:]
   print(user_list) # 输出 ['范德彪']
   ```

7. 步长

   ```python
   user_list = ["范德彪","刘华强",'尼古拉斯赵四',"宋小宝","刘能"]
   #              0        1        2          3       4
   print( user_list[1:4:2] )
   print( user_list[0::2] )
   print( user_list[1::2] )
   print( user_list[4:1:-1] )
   ```

   实现列表的翻转

   ```python
   user_list = ["范德彪","刘华强",'尼古拉斯赵四',"宋小宝","刘能"]
   new_data = user_list[::-1]
   print(new_data)
   ```

8. for循环

   切记，循环的过程中对数据进行删除会踩坑【面试题】。

   ```python
   # 正确方式，倒着删除。
   user_list = ["刘的话", "范德彪", "刘华强", '刘尼古拉斯赵四', "宋小宝", "刘能"]
   for index in range(len(user_list) - 1, -1, -1):
       item = user_list[index]
       if item.startswith("刘"):
           user_list.remove(item)
   print(user_list)
   ```

####  转换列表类型   list( )

- int、bool无法转换成列表

- str，tuple，set类型都能转

  



## 5  元组类型（tuple）

元组（tuple），是一个**有序**且**不可变**的容器，在里面可以存放**多个不同类型**的元素。

由于元组和列表都可以充当`容器`，他们内部可以放很多元素，并且也支持元素内的各种嵌套。

#### 定义元组

注意：建议在元组的最后多加一个逗号，用于标识他是一个元组。

```python
a = (1,)
a = tuple()
```

#### 元组的通用功能

1. 相加，两个列表相加获取生成一个新的列表。

   ```python
   data = ("赵四","刘能") + ("宋晓峰","范德彪")
   print(data) # ("赵四","刘能","宋晓峰","范德彪")
   ```

2. 相乘，列表*整型 将列表中的元素再创建N份并生成一个新的列表。

   ```python
   data = ("赵四","刘能") * 2
   print(data) # ("赵四","刘能","赵四","刘能")
   ```

3. 获取长度   **len（）**

   ```python
   user_list = ("范德彪","刘华强",'尼古拉斯赵四',)
   print( len(user_list) )
   ```

4. 索引

   ```python
   user_list = ("范德彪","刘华强",'尼古拉斯赵四',)
   print( user_list[0] 
   ```

5. 切片

   ```python
   user_list = ("范德彪","刘华强",'尼古拉斯赵四',)
   print( user_list[0:2] )
   ```

6. 步长

   倒转元组可第三位填-1

   ```python
   user_list = ("范德彪","刘华强",'尼古拉斯赵四',"宋小宝","刘能")
   data = user_list[::-1]
   ```

7. for循环


#### 转换

其他类型转换为元组，使用`tuple(其他类型)`，目前只有字符串和列表可以转换为元组。



## 6 字典类型（dict）

字典是 无序、键不重复 且 元素只能是键值对的可变的一个容器（键子孙元素都必须是可哈希）。

无序（在Python3.6+字典就是有序了，之前的字典都是无序。）

字典中对键值得要求：

- 键：必须可哈希。 目前为止学到的可哈希的类型：int/bool/str/tuple；不可哈希的类型：list/set/dict。（集合）
- 值：任意类型。

#### 定义字典

```python
v1 = {}
v2 = dict()
```

#### 字典方法

1. **get（）**

   获取值，括号内输入键获取字典内此键的值

```python
info = { 
    "age":12, 
    "status":True, 
    "name":"武沛齐",
    "data":None
}
data1 = info.get("name")
```

2. **keys()**

   获取字典所有的键

   注意：在Python2中 字典.values()直接获取到的是列表，

   而Python3中返回的是高仿列表，这个高仿的列表可以被循环显示。

```python
info = {"age":12, "status":True, "name":"wupeiqi","email":"xx@live.com"}
data = info.keys()# ['age', 'status', 'name', 'email']
```

3. **values()**

   获取字典所有的值

```python
info = {"age":12, "status":True, "name":"wupeiqi","email":"xx@live.com"}
data = info.values()# [12, True, 'wupeiqi', 'xx@live.com']
```

4. **items( )**

   获取字典内所有的键值

```python
info = {"age":12, "status":True, "name":"wupeiqi","email":"xx@live.com"}
data = info.items()
# 输出[ ('age', 12),  ('status', True),  ('name', 'wupeiqi'),  ('email', 'xx@live.com')  ]
```

5. **setdefault("键名", 值)**

   给字典内添加值，键重复会覆盖上一个值

```python
data = {"name": "武沛齐","email": 'xxx@live.com'}
data.setdefault("age", 18)
# {'name': '武沛齐', 'email': 'xxx@live.com', 'age': 18}
```

6. **update( {"age":14,"name":"武沛齐"} )**

   把一个字典添加到另一个字典，原字典没有此键就直接添加，有就更新值

```python
info = {"age":12, "status":True}
info.update( {"age":14,"name":"武沛齐"} )  
# 输出：{"age":14, "status":True,"name":"武沛齐"}
```

7. **pop("键")**

   移除指定键值对，可以返回一个移除键的值

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   data = info.pop("age")
   print(info) # {"status":True,"name":"武沛齐"}
   print(data) # 12
   ```

8. **popitem()** 

   按照顺序移除字典内的键值（后进先出），并返回一个移除的键值

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   data = info.popitem() # ("name","武沛齐" )
   print(info) # {"age":12, "status":True}
   print(data) # ("name","武沛齐")
   ```

   - py3.6后，popitem移除最后的值。
   - py3.6之前，popitem随机删除。

#### 字典通用功能

1. 求`并集`（Python3.9新加入）

   ```python
   v1 = {"k1": 1, "k2": 2}
   v2 = {"k2": 22, "k3": 33}
   v3 = v1 | v2
   print(v3) # {'k1': 1, 'k2': 22, 'k3': 33}
   ```

2. **len（）**长度

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   data = len(info)
   print(data) # 输出：3
   ```

3. **in** 是否包含

   ```python
   info = { "age":12,  "status":True,"name":"武沛齐" }
   v1 = "age" in info
   print(v1)
   v2 = "age" in info.keys()
   print(v2)
   ```

   

4. 索引（键）
   字典不同于元组和列表，字典的索引是`键`，而列表和元组则是 `0、1、2等数值` 。

   ```python
   info = { "age":12,  "status":True, "name":"武沛齐"}
   print( info["age"] )  	    # 输出：12
   print( info["name"] )		# 输出：武沛齐
   print( info["status"] )	    # 输出：True
   print( info["xxxx"] )   	# 报错，通过键为索引去获取之后时，键不存在会报错（以后项目开发 建议使用get方法根据键去获取值）
   
   value = info.get("xxxxx") # None
   ```

5. 根据键 修改值 和 添加值 和 删除键值对

   字典内添加值

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   info["gender"] = "男"
   print(info) # 输出： {"age":12, "status":True,"name":"武沛齐","gender":"男"}
   ```

   字典内修改值

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   info["age"] = "18" 
   print(info) # 输出： {"age":"18", "status":True,"name":"武沛齐"}
   ```

   字典内删除值

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   del info["age"]  # 删除info字典中键为age的那个键值对（键不存在则报错）
   print(info) # 输出： {"status":True,"name":"武沛齐"}
   ```

   

6. for循环
   由于字典也属于是容器，内部可以包含多个键值对，可以通过循环对其中的：键、值、键值进行循环；

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   for item in info:
   	print(item)  # 所有键
   ```

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   for item in info.keys():
   	print(item)# 所有键
   ```

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   for item in info.values():
   	print(item)#所有值
   ```

   ```python
   info = {"age":12, "status":True,"name":"武沛齐"}
   for key,value in info.items():
   	print(key,value)#所有键值
   ```

#### 字典的转换

想要转换为字典.

```python
v = dict( [ ("k1", "v1"), ["k2", "v2"] ] )
print(v) # { "k1":"v1", "k2":"v2" }
```

字典转其他类型，默认转发成的是键

```python
info = { "age":12, "status":True, "name":"武沛齐" }

v1 = list(info)        # ["age","status","name"]键

v2 = list(info.keys()) # ["age","status","name"]键

v3 = list(info.values()) # [12,True,"武沛齐"]值

v4 = list(info.items()) # [ ("age",12), ("status",True), ("name","武沛齐") ]键值
```



#### 对字典的key进行排序

```python
menu_dict = {1："",2:""}
key_list = sorted(menu_dict)
```



#### 创建有序字典

```python
from collections import OrderedDict

ordered_dict = OrderedDict()
```







## 7 集合类型（set）

集合，是 无序、不重复、元素必须可哈希、可变的一个容器（子孙元素都必须是可哈希）。

因存储原理，集合的元素必须是可哈希的值，即：内部通过通过哈希函数把值转换成一个数字。

总结：集合的元素只能是 int、bool、str、tuple 。

#### 定义集合

**注意**：定义空集合时，只能使用`v = set()`，不能使用 `v={}`（这样是定义一个空字典）。

```python
v = set()
```

#### 集合方法

1. **add( )**

   添加元素

   ```python
   data = {"刘嘉玲", '关之琳', "王祖贤"}
   data.add("郑裕玲")
   ```

2. **discard()**

   删除元素

   ```python
   data = {"刘嘉玲", '关之琳', "王祖贤","张曼⽟", "李若彤"}
   data.discard("关之琳") 
   ```

3. **s1.intersection(s2)**  或 **s1 & s2 **

   交集，两个集合内都存在的值

   ```python
   s1 = {"刘能", "赵四", "⽪⻓⼭"}
   s2 = {"刘科⻓", "冯乡⻓", "⽪⻓⼭"}
   
   s4 = s1.intersection(s2) # 取两个集合的交集 
   print(s4) # {"⽪⻓⼭"}
   
   s3 = s1 & s2   			  # 取两个集合的交集
   print(s3)
   ```

4. **s1.union(s2)**   **s1 | s2**

   并集，两个集合内都不存在的值

   ```python
   s1 = {"刘能", "赵四", "⽪⻓⼭"}
   s2 = {"刘科⻓", "冯乡⻓", "⽪⻓⼭"}
   s4 = s1.union(s2) 		# 取两个集合的并集  {"刘能", "赵四","刘科⻓", "冯乡⻓", }
   s3 = s1 | s2   			# 取两个集合的并集
   ```

5. **s1.difference(s2)**      **s2 - s1**  

   差集，左集合有右集合没的值

   ```python
   s1 = {"刘能", "赵四", "⽪⻓⼭"}
   s2 = {"刘科⻓", "冯乡⻓", "⽪⻓⼭"}
   s4 = s1.difference(s2) 		# 差集，s1中有且s2中没有的值 {"刘能", "赵四"}
   s6 = s2.difference(s1)   	# 差集，s2中有且s1中没有的值 {"刘科⻓", "冯乡⻓"}
   s3 = s1 - s2   			   # 差集，s1中有且s2中没有的值
   s5 = s2 - s1   			   # 差集，s2中有且s1中没有的值
   ```

#### 集合能用功能

1. 减，计算差集

2. &，计算交集

3. |，计算并集
4. 长度  **len（）**

5. for循环


#### 转换集合类型 set（）

其他类型如果想要转换为集合类型，可以通过set进行转换，并且如果数据有重复自动剔除。

提示：str/list/tuple/dict都可以转换为集合。







## 8 浮点类型（ float，浮点型）

浮点型，一般在开发中用于表示小数。

```python
v1 = 3.14
v2 = 9.89
```

关于浮点型的其他知识点如下：

- 在类型转换时需要，在浮点型转换为整型时，会将小数部分去掉。

  ```python
  v1 = 3.14 
  data = int(v1)
  print(data) # 3
  ```

- 想要保留小数点后N位

  ```python
  v1 = 3.1415926
  result = round(v1,3)
  print(result) # 3.142
  ```

- 浮点型的坑（所有语言中）

  底层原理视频：https://www.bilibili.com/video/BV1354y1B7o1/


  在项目中如果遇到精确的小数计算应该怎么办？

  ```python
import decimal

v1 = decimal.Decimal("0.1")
v2 = decimal.Decimal("0.2")
v3 = v1 + v2
print(v3) # 0.3
  ```

  







## 9.其他

#### None类型

Python的数据类型中有一个特殊的值None，意味着这个值啥都不是 或 表示空。 相当于其他语言中 `null`作用一样。





##  类型转换

- int，整型定义时，必须是数字且无引号，例如：5、8、9

- str，字符串定义时，必须用双引号括起来，例如：”中国”、”武沛齐”、”666”

- bool，布尔值定义时，只能写True和False

- 不同的数据类型都有不同的功能，例如：整型可以加减乘除 而 字符串只能加(拼接)和乘法。
  如果想要做转换可遵循一个基本规则：想转换什么类型就让他包裹一些。

  例如：str(666) = "666"是将整型转换为字符串、int(“888”)是将字符串转 888。


三句话搞定类型转换：

- 其他所有类型转换为布尔类型时，除了 空字符串、0以为其他都是True。

- 字符串转整形时，只有那种 "988" 格式的字符串才可以转换为整形，其他都报错。

- 想要转换为那种类型，就用这类型的英文包裹一下就行。 

  ```
  str(...)
  int(...)
  bool(...)
  list(...)
  tuple(....)
  set(......)
  ```

  

### int()字符转数字

``` python
int("666")
int("alex是sb") 报错
# 布尔类型转换为整形
int(True)  转换完等于 1
int(False) 转换完等于 0
```

### str()转换为字符串

```python
# 整形转字符串
str(345)
str(666) + str(9) 结果为："6669"
# 布尔类型转换为字符串
str(True)  "True"
str(False) "False"
```

### 转换为布尔类型

```python
# 整形转布尔
bool(1) True
bool(2) True
bool(0) False
bool(-10) True
# 字符串转布尔
bool("alex") True
bool("砂玻帮你") True
bool("") False
bool(" ") True
```





















































# 五 函数

函数，可以当做是一大堆功能代码的集合。

什么时候会用到函数呢？一般在项目开发中有会有两种应用场景：

- 有重复代码，用函数增加代码的重用性。
- 代码太长，用函数增强代码的可读性。

利用函数编程称为：函数式编程。

## 1 定义函数

- 函数名的规范。（同变量名规范）
- 函数的注释，说明函数的作用。

```python
# 定义名字叫info的函数
def info():
     """ 用于数据加密和xxx """
    print("第一行")
    print("第二行")
    print("第n行...")
    
info() #执行
```

## 2. 函数的参数

### 2.1 参数

在定义函数时，如果在括号中添加`变量`，我们称它为函数的形式参数：

- 形参：定义函数时的叫形参

```python
def func(a1,a2,a3): # 形参
    print(a1+a2+a3)
```

- 实参： 执行函数并传入的参数叫实参

```python
func(9,2,103)
```

- 位置传参：按顺序传的

```python
def add(n1,n2):
    print(n1+n2)
   
add(1,22)
```

- 关键字传参 :位置和关键混合时，关键字传参要在后面

```python
def add(n1,n2):
    print(n1+n2)
    
add(n1=1,n2=22)
```



### 2.2 默认参数

定义函数时设定的默认参数，未传参时使用默认参，传参了就覆盖默认参

注意：函数执行传参时，传递的是内存地址。Python在创建函数（未执行）时，如果发现函数的参数中有默认值，则在函数内部会创建一块区域并维护这个默认值。和传入的参数2个内存地址是不一样的，如果默认参数是可变的列表，容易有坑

```python
def func(a1, a2, a3=10):
    print(a1 + a2 + a3) 
    	
# 位置传参
func(8, 19)
func(1, 2, 99)
# 关键字传参（位置和关键混合时，关键字传参要在后面）
func(12, 9, a3=90)
func(12, a2=9, a3=90)
func(a1=12, a2=9, a3=90)
```

默认参数面试坑

```python
# 内存中创建空间存储 [1, 2, 10, 20, 40] 地址：1010101010
def func(a1, a2=[1, 2]):
    a2.append(a1)
    return a2

# a1=10
# a2 -> 1010101010
# v1 -> 1010101010
v1 = func(10)


# a1=20
# a2 -> 1010101010
# v2 -> 1010101010
v2 = func(20)

# a1=30
# a2 -> 11111111111   [11,22,30]
# v3 -> 11111111111
v3 = func(30, [11, 22])

# a1=40
# a2 -> 1010101010
# v4 -> 1010101010
v4 = func(40)

print(v1) # [1, 2, 10, 20, 40]
print(v2) # [1, 2, 10, 20, 40]
print(v3) # [11,22,30]
print(v4) # [1, 2, 10, 20, 40] 
```



### 2.3 动态参数

动态参数，定义函数时在形参位置用 `*或**` 可以接任意个参数。

- `*`元组类型，只能按照位置传参

```python
def func(*args):
    print(args) # 元组类型 (22,)   (22,33,99,) ()

# 只能按照位置传参
func(22)
func(22,33)
func(22,33,99)
func()
```

- `**`字典类型，只能按关键字传参

```python
def func(**kwargs):
    print(kwargs) # 字典类型 {"n1":"武沛齐"}    {"n1":"武沛齐","age":"18","email":"xxxx"}  {}
    
# 只能按关键字传参
func(n1="武沛齐")
func(n1="武沛齐",age=18)
func(n1="武沛齐",age=18,email="xx@live.com")
```

- `*,**`位置参数传参在前，关键字传参在后

```python
def func(*args,**kwargs):
    print(args,kwargs) 

func(22,33,99) # (22, 33, 99) {}
func(n1="武沛齐",age=18) # () {'n1': '武沛齐', 'age': 18}
func(22,33,99,n1="武沛齐",age=18) # (22, 33, 99) {'n1': '武沛齐', 'age': 18}
func() # () {}
```

注意事项（不重要，听过一遍即可）

```python
# 1. ** 必须放在 * 的后面
def func1(*args, **kwargs):
    print(args, **kwargs)


# 2. 参数和动态参数混合时，动态参数只能放在最后。
def func2(a1, a2, a3, *args, **kwargs):
    print(a1, a2, a3, args, **kwargs)


# 3. 默认值参数和动态参数同时存在
def func3(a1, a2, a3, a4=10, *args, a5=20, **kwargs):
    print(a1, a2, a3, a4, a5, args, kwargs)


func3(11, 22, 33, 44, 55, 66, 77, a5=10, a10=123)
```

在定义函数时可以用 `*和**`，其实在执行函数时，也可以用。

- 形参固定，实参用`*和**`:   会把列表或者字典的实参打散

```python
def func(a1,a2):
    print(a1,a2)
    
func( 11, 22 )
func( a1=1, a2=2 )

func( *[11,22] )
func( **{"a1":11,"a2":22} )
```

- 形参用`*和**`，实参也用 `*和**`

```python
def func(*args,**kwargs):
    print(args,kwargs)
    
func( 11, 22 ) # (11, 22) {}
func( 11, 22, name="武沛齐", age=18 ) # (11, 22) {'name': '武沛齐', 'age': 18}


func( [11,22,33], {"k1":1,"k2":2} ) # ([11, 22, 33], {'k1': 1, 'k2': 2}) {}


func( *[11,22,33], **{"k1":1,"k2":2} ) # (11, 22, 33) {'k1': 1, 'k2': 2}

# 值得注意：按照这个方式将数据传递给args和kwargs时，数据是会重新拷贝一份的（可理解为内部循环每个元素并设置到args和kwargs中）。
```



## 3. 函数返回值

`return:完成某个结果并希望的到结果,基于return控制让函数终止执行`

注意：函数的返回值是内存地址

- 返回值可以是任意类型，如果函数中没写return，则默认返回None
- 当在函数中`未写返回值` 或 `return` 或 `return None` ，执行函数获取的返回值都是None。
- return后面的值如果有逗号，则默认会将返回值转换成元组再返回。

```python
def func():
    return 1,2,3

value = func()
print(value) # (1,2,3)
```

- 函数一旦遇到return就会立即退出函数（终止函数中的所有代码）



##  4 函数和函数名

函数名其实就是一个变量，这个变量只不过代指的函数而已。

注意：函数必须先定义才能被调用执行（解释型语言）。

注意：由于函数名被重新定义之后，就会变量新被定义的值，所以大家在自定义函数时，不要与python内置的函数同名，否则会覆盖内置函数的功能

### 1 函数做元素

既然函数就相当于是一个变量，那么在列表等元素中是可以把函数当做元素

函数同时也可被哈希，所以函数名通知也可以当做 集合的元素、字典的键。

### 2 函数名赋值

将函数名赋值给其他变量，函数名其实就个变量，代指某函数；如果将函数名赋值给另外一个变量，则此变量也会代指该函数

```python
def func(a1,a2):
    print(a1,a2)
xxxxx = func

# 此时，xxxxx和func都代指上面的那个函数，所以都可以被执行。
func(1,1)
xxxxx(2,2)
```

对函数名重新赋值，如果将函数名修改为其他值，函数名便不再代指函数

```python
def func(a1,a2):
    print(a1,a2)

# 执行func函数
func(11,22)

# func重新赋值成一个字符串
func = "武沛齐"

print(func)
```





### 3 函数名做参数和返回值

函数名其实就一个变量，代指某个函数，所以，他和其他的数据类型一样，也可以当做函数的参数和返回值

- 参数

  ```python
  def plus(num):
      return num + 100
  
  def handler(func):
      res = func(10) # 110
      msg = "执行func，并获取到的结果为:{}".format(res)
      print(msg) # 执行func，并获取到的结果为:110
     
  # 执行handler函数，将plus作为参数传递给handler的形式参数func
  handler(plus)
  ```

- 返回值

  ```python
  def plus(num):
      return num + 100
  
  def handler():
  	print("执行handler函数")
      return plus
      
  result = handler()
  data = result(20) # 120
  print(data)
  ```



## 5 作用域

作用域，可以理解为一块空间，这块空间的数据是可以共享的。通俗点来说，作用域就类似于一个房子，房子中的东西归里面的所有人共享，其他房子的人无法获取。

### **1 函数为作用域**

Python以函数为作用域，所以在函数内创建的所有数据，可以此函数中被使用，无法在其他函数中被使用。

### **2  全局和局部**

Python中以函数为作用域，函数的作用域其实是一个局部作用域。

```python
# 全局变量（变量名大写）
COUNTRY = "中国"
CITY_LIST = ["北京","上海","深圳"]

def download():
    # 局部变量
    url = "http://www.xxx.com"
    ...
    
def upload():
    file_name = "rose.zip"
    ...
    
```

`COUNTRY`和`CITY_LIST`是在全局作用域中，全局作用域中创建的变量称之为【全局变量】，可以在全局作用域中被使用，也可以在其局部作用域中被使用。

`download`和`upload`函数内部维护的就是一个局部作用域，在各自函数内部创建变量称之为【局部变量】，且局部变量只能在此作用域中被使用。局部作用域中想使用某个变量时，寻找的顺序为：`优先在局部作用域中寻找，如果没有则去上级作用域中寻找`。

注意：全局变量一般都是大写。

### **3 global关键字**

默认情况下，在局部作用域对全局变量只能进行：读取和修改内部元素（可变类型），无法对全局变量进行重新赋值。

如果想要在局部作用域中对全局变量重新赋值，则可以基于 `global`关键字实现

```python
COUNTRY = "中国"
CITY_LIST = ["北京","上海","深圳"]

def download():
    url = "http://www.xxx.com"
	
    global CITY_LIST
    CITY_LIST =  ["河北","河南","山西"]
    print(CITY_LIST)
    
    global COUNTRY
    COUNTRY = "中华人民共和国"
    print(COUNTRY)

def upload():
    file_name = "rose.zip"
    print(COUNTRY)
    print(CITY_LIST)
    
download()
upload()
```



## 6 函数嵌套

### 1 函数在作用域中

函数也是定义在作用域中的数据，在执行函数时候，也同样遵循：优先在自己作用域中寻找，没有则向上一接作用域寻找

三句话搞定作用域：

- 优先在自己的作用域找，自己没有就去上级作用域。
- 在作用域中寻找值时，要确保此次此刻值是什么。
- 分析函数的执行，并确定函数`作用域链`。（函数嵌套）

### 2.闭包

闭包，简而言之就是将数据封装在一个包（区域）中，使用时再去里面取。

闭包应用场景1：封装数据防止污染全局。

```python
def func(age):
    name = "武沛齐"

    def f1():
        print(name, age)

    def f2():
        print(name, age)

    def f3():
        print(name, age)

    f1()
    f2()
    f3()

func(123)
```

闭包应用场景2：封装数据封到一个包里，使用时在取。

### 3.装饰器

装饰器，在不修改原函数内容的前提下，通过@函数可以实现在函数前后自定义执行一些功能（批量操作会更有意义）。

```python
def outer(origin):
    def inner(*args, **kwargs):
        print("before 110")
        res = origin(*args, **kwargs)  # 调用原来的func函数
        print("after")
        return res

    return inner


@outer  # func1 = outer(func1)
def func1(a1):
    print("我是func1函数")
    value = (11, 22, 33, 44)
    return value


@outer  # func2 = outer(func2)
def func2(a1, a2):
    print("我是func2函数")
    value = (11, 22, 33, 44)
    return value


@outer  # func3 = outer(func3)
def func3(a1):
    print("我是func3函数")
    value = (11, 22, 33, 44)
    return value


func1(1)
func2(11, a2=22)
func3(999)
```



- 实现原理：基于@语法和函数闭包，将原函数封装在闭包中，然后将函数赋值为一个新的函数（内层函数），执行函数时再在内层函数中执行闭包中的原函数。

- 实现效果：可以在不改变原函数内部代码 和 调用方式的前提下，实现在函数执行和执行扩展功能。

- 适用场景：多个函数系统统一在 执行前后自定义一些功能。

- 装饰器示例

  ```python
  def outer(origin):
      def inner(*args, **kwargs):
  		# 执行前
          res = origin(*args, **kwargs)  # 调用原来的func函数
          # 执行后
          return res
      return inner
  
  
  @outer
  def func():
      pass
  
  func()
  ```

  **重要补充：functools**

你会发现装饰器实际上就是将原函数更改为其他的函数，然后再此函数中再去调用原函数。

```python
def auth(func):
    def inner(*args, **kwargs):
        return func(*args, **kwargs)
    return inner

@auth
def handler():
    pass

handler()
print(handler.__name__) # inner
```

其实，一般情况下大家不用functools也可以实现装饰器的基本功能，但后期在项目开发时，不加functools会出错（内部会读取`__name__`，且`__name__`重名的话就报错），所以在此大家就要规范起来自己的写法。

```python
import functools


def auth(func):
    @functools.wraps(func)
    def inner(*args, **kwargs):
        """巴巴里吧"""
        res = func(*args, **kwargs)  # 执行原函数
        return res

    return inner
```



## 7 匿名函数

匿名函数，则是基于lambda表达式实现定义一个可以没有名字的函数

```python
f1 = lambda x:x+100

res = f1(100)
print(res)
```

基于Lambda定义的函数格式为：`lambda 参数:函数体`

- 参数，支持任意参数。

  ```python
  lambda x: 函数体
  lambda x1,x2: 函数体
  lambda *args, **kwargs: 函数体
  ```

- 函数体，只能支持单行的代码。

  ```python
  def xxx(x):
      return x + 100
      
  lambda x: x + 100
  ```

- 返回值，默认将函数体单行代码执行的结果返回给函数的执行这。

  ```python
  func = lambda x: x + 100
  
  v1 = func(10)
  print(v1) # 110
  ```

匿名函数适用于简单的业务处理，可以快速并简单的创建函数。





## 判断是否是函数

```python
from types import FunctionType
def key_or_func():
    pass


结果 =  isinstance(key_or_func, FunctionType)
```



## exec()执行字符串代码

`exec()能够动态地执行复杂的Python代码。比如一个写在txt文件中的代码，可以在Python程序中读取后，用exec()执行。`

### 参数

`object：`必选参数，表示需要被指定的python代码，它必须是字符串或code对象。如果object是一个字符串，该字符串会被先解析为一组python语句，然后再执行。如果object是一个code对象，那么它只是被简单的执行

`globals：`可选参数，表示全局命名空间（存放全局变量），如果被提供，则必须是一个字典对象。

`locals：`可选参数，表示当前局部命名空间（存放局部变量），如果被提供，可以是任何映射对象。如果该参数被忽略，那么它将会取与globals相同的值。

### 返回

None













# 六 模块

## 1. 自定义模块

### 1.1 模块和包

在Python中一般对文件和文件的称呼（很多开发者的平时开发中也有人都称为模块）

- 一个py文件，模块（module）。
- 含多个py文件的文件夹，包（package）。

注意：在包（文件夹）中有一个默认内容为空的`__init__.py`的文件，一般用于描述当前包的信息（在导入他下面的模块时，也会自动加载）。

- py2必须有，如果没有导入包就会失败。
- py3可有可无。

### 1.2 导入

当定义好一个模块或包之后，如果想要使用其中定义的功能，必须要先导入，然后再能使用。

导入，其实就是将模块或包加载的内存中，以后再去内存中去拿就行。

关于导如时的路径：

>  在Python内部默认设置了一些路径，导入模块或包时，都会按照指定顺序逐一去特定的路径查找。

##### 查看导入查找的路径

```python
import sys
print(sys.path)
```

想要导入任意的模块和包，都必须写在如下路径下，才能被找到。

##### 添加指定路径

```python
import sys
sys.path.append("路径A")

import xxxxx  # 导入路径A下的一个xxxxx.py文件
```

- 关于导入的方式：
  - 第一类：import xxxx（开发中，一般多用于导入sys.path目录下的一个py文件）
  - 第二类：from xxx import xxx 【常用】，一般适用于多层嵌套和导入模块中某个成员的情况。
  - 提示：基于from模式也可以支持 `from many import *`，即：导入一个模块中所有的成员（可能会重名，所以用的少）。



##### 以字符串方式导入模块

```python
# auto_luffy.urls.py
urlpatterns = [666,]
```

```python
from django.utils.module_loading import import_string		# 1 导入import_string模块方法

ROOT_URLCONF = 'auto_luffy.urls'			
md = import_string(ROOT_URLCONF)						# 2 使用此方法
print(md.urlpatterns)
# >>>	[666,]
```







### 1.3 导入别名

如果项目中导入 成员/模块/包 有重名，那么后导入的会覆盖之前导入，为了避免这种情况的发生，Python支持重命名

```python
from xxx.xxx import xx as xo
import x1.x2 as pg
```

```python
import commons.page as pg

v1 = pg.pagination()
```



### 1.4主文件

执行py文件时，内部`__name__=="__main__"`，导入模块时，被导入的模块 `__name__="模块名"`

- 执行一个py文件时

  ```
  __name__ = "__main__"
  ```

- 导入一个py文件时

  ```python
  __name__ = "模块名"
  ```

主文件，其实就是在程序执行的入口文件，例如：

```python
├── commons
│   ├── __init__.py
│   ├── convert.py
│   ├── page.py
│   ├── tencent
│   │   ├── __init__.py
│   │   ├── sms.py
│   │   └── wechat.py
│   └── utils.py
├── many.py
└── run.py
```

我们通常是执行 run.py 去运行程序，其他的py文件都是一些功能代码。当我们去执行一个文件时，文件内部的 `__name__`变量的值为 `__main__`，所以，主文件经常会看到：

```python
import many
from commons import page
from commons import utils


def start():
    v1 = many.show()
    v2 = page.pagination()
    v3 = utils.encrypt()


if __name__ == '__main__':
    start()
```

只有是以主文件的形式运行此脚本时start函数才会执行，被导入时则不会被执行。





##  2 第三方模块

### 1 pip安装模块（最常用）

pip其实是一个第三方模块包管理工具，默认安装Python解释器时自动会安装，默认目录：

```
MAC系统，即：Python安装路径的bin目录下
	/Library/Frameworks/Python.framework/Versions/3.9/bin/pip3
	/Library/Frameworks/Python.framework/Versions/3.9/bin/pip3.9
	
Windows系统，即：Python安装路径的scripts目录下
	C:\Python39\Scripts\pip3.exe
	C:\Python39\Scripts\pip3.9.exe
```

提示：为了方便在终端运行pip管理工具，我们也会把它所在的路径添加到系统环境变量中。

使用pip去安装第三方模块也非常简单，只需要在自己终端执行：`pip install 模块名称` 即可。

```
pip3 install requests
```

默认安装的是最新的版本，如果想要指定版本：

```python
pip3 install 模块名称==版本

例如：
pip3 install django==2.2
```

pip默认是去 `https://pypi.org` 去下载第三方模块（本质上就是别人写好的py代码），国外的网站速度会比较慢，为了加速可以使用国内的豆瓣源。

- 一次性使用

  ```
  pip3.9 install 模块名称  -i  https://pypi.douban.com/simple/
  ```

- 永久使用

  - 配置

    ```
    # 在终端执行如下命令
    pip3.9 config set global.index-url https://pypi.douban.com/simple/
    
    # 执行完成后，提示在我的本地文件中写入了豆瓣源，以后再通过pip去安装第三方模块时，就会默认使用豆瓣源了。
    # 自己以后也可以打开文件直接修改源地址。
    Writing to /Users/wupeiqi/.config/pip/pip.conf
    ```

  - 使用

    ```
    pip3.9 install 模块名称
    ```



写在最后，也还有其他的源可供选择（豆瓣应用广泛）。

```
阿里云：http://mirrors.aliyun.com/pypi/simple/
中国科技大学：https://pypi.mirrors.ustc.edu.cn/simple/ 
清华大学：https://pypi.tuna.tsinghua.edu.cn/simple/
中国科学技术大学：http://pypi.mirrors.ustc.edu.cn/simple/
```

如果你的电脑上某个写情况没有找到pip，也可以自己手动安装：

- 下载 `get-pip.py` 文件，到任意目录

  ```
  地址：https://bootstrap.pypa.io/get-pip.py
  ```

- 打开终端进入目录，用Python解释器去运行已下载的 `get-pip.py`文件即刻安装成功。
  <img src="python神功.assets\image-20210102191829546.png" alt="image-20210102191829546" style="zoom:200%;" />



### xlrd，操作xlsx文件

#### 读

##### 1.1 获取工作簿对象

引入模块，获得工作簿对象。

```python
import xlrd  #引入模块
 
workbook=xlrd.open_workbook("DataSource/Economics.xls")  #打开文件，获取excel文件的workbook（工作簿）对象
```

##### 1.2 获取工作表对象

一个工作簿里面可以含有多个工作表，当我们获取“工作簿对象”后，可以接着来获取工作表对象，可以通过“索引”的方式获得，也可以通过“表名”的方式获得。

```python
'''对workbook对象进行操作'''
names=workbook.sheet_names() #获取所有sheet的名字
sheet0_name=workbook.sheet_names()[0]  #通过sheet索引获取sheet名称

worksheet=workbook.sheet_by_index(0) #通过sheet索引获得sheet对象

worksheet=workbook.sheet_by_name("各省市") #通过sheet名获得sheet对象
```

##### 1.3 获取工作表的基本信息

在获得“表对象”之后，我们可以获取关于工作表的基本信息。包括表名、行数与列数。

```python
'''对sheet对象进行操作'''
name=worksheet.name  #获取表的姓名
 
nrows=worksheet.nrows  #获取该表总行数
 
ncols=worksheet.ncols  #获取该表总列数
```

##### 1.4 按行或列方式获得工作表的数据

有了行数和列数，循环打印出表的全部内容也变得轻而易举。

```python
worksheet.row_values(0)  #以列表形式读出，列表中的每一项是str类型
 
col_data=worksheet.col_values(0)  #获取第一列的内容
```

##### 1.5 获取某一个单元格的数据

 我们还可以将查询精确地定位到某一个单元格。在xlrd模块中，工作表的行和列都是从0开始计数的。

```python
cell_value1=worksheet.cell_value(0,0) #通过坐标读取表格中的数据
 
cell_value1=worksheet.cell(0,0).value
```

#### 写

##### 2.1 创建工作簿

```sql
import xlwt  # 导入xlwt模块
 
book=xlwt.Workbook(encoding="utf-8",style_compression=0) #创建一个Workbook对象，相当于创建了一个Excel文件
'''
Workbook类初始化时有encoding和style_compression参数
encoding:设置字符编码，一般要这样设置：w = Workbook(encoding='utf-8')，就可以在excel中输出中文了。默认是ascii。
style_compression:表示是否压缩，不常用。
'''
```

##### 2.2 创建工作表

创建完工作簿之后，可以在相应的工作簿中，创建工作表。

```python
 # 创建一个sheet对象，一个sheet对象对应Excel文件中的一张表格。
sheet = book.add_sheet('test01', cell_overwrite_ok=True)
# 其中的test是这张表的名字,cell_overwrite_ok，表示是否可以覆盖单元格，其实是Worksheet实例化的一个参数，默认值是False
```

##### 2.3 按单元格的方式向工作表中添加数据

```python
# 向表test中添加数据
sheet.write(0, 0, '各省市')  # 其中的'0-行, 0-列'指定表中的单元，'各省市'是向该单元写入的内容
sheet.write(0, 1, '工资性收入')
```

##### 2.4 按行或列方式向工作表中添加数据

为了验证这个功能，我们在工作簿中，再创建一个工作表，上个工作表叫“test01”，那么这个工作表命名为“test02”，都隶属于同一个工作簿。在下面代码中test02是表名，sheet2才是可供操作的工作表对象。

```python
#添加第二个表
sheet2=book.add_sheet("test02",cell_overwrite_ok=True)
 
 
Province=['北京市', '天津市', '河北省', '山西省', '内蒙古自治区', '辽宁省',
          '吉林省', '黑龙江省', '上海市', '江苏省', '浙江省', '安徽省', '福建省',
          '江西省', '山东省', '河南省', '湖北省', '湖南省', '广东省', '广西壮族自治区',
          '海南省', '重庆市', '四川省', '贵州省', '云南省', '西藏自治区', '陕西省', '甘肃省',
          '青海省', '宁夏回族自治区', '新疆维吾尔自治区']
 
Income=['5047.4', '3247.9', '1514.7', '1374.3', '590.7', '1499.5', '605.1', '654.9',
        '6686.0', '3104.8', '3575.1', '1184.1', '1855.5', '1441.3', '1671.5', '1022.7',
        '1199.2', '1449.6', '2906.2', '972.3', '555.7', '1309.9', '1219.5', '715.5', '441.8',
        '568.4', '848.3', '637.4', '653.3', '823.1', '254.1']
 
Project=['各省市', '工资性收入', '家庭经营纯收入', '财产性收入', '转移性收入', '食品', '衣着',
         '居住', '家庭设备及服务', '交通和通讯', '文教、娱乐用品及服务', '医疗保健', '其他商品及服务']
 
#填入第一列
for i in range(0, len(Province)):
    sheet2.write(i+1, 0, Province[i])
 
#填入第二列
for i in range(0,len(Income)):
    sheet2.write(i+1,1,Income[i])
 
#填入第一行
for i in range(0,len(Project)):
    sheet2.write(0,i,Project[i])
```

##### 2.5 保存创建的文件

```python
# 最后，将以上操作保存到指定的Excel文件中
book.save('DataSource\\test1.xls')  
```







## 3.内置模块（一）

### 1 os文件相关

详见文件操作

### 2 shutil文件解压相关相关

详见文件操作

### 3 random  随机抽取元素

```python
import random
```

#### 1. 获取范围内的随机整数

```python
v = random.randint(10, 20)
print(v)
```

#### 2. 获取范围内的随机小数

```python
v = random.uniform(1, 10)
print(v)
```

#### 3. 随机抽取一个元素

```python
v = random.choice([11, 22, 33, 44, 55])
print(v)
```

#### 4. 随机抽取多个元素

```python
v = random.sample([11, 22, 33, 44, 55], 3)
print(v)
```

#### 5. 打乱顺序

```python
data = [1, 2, 3, 4, 5, 6, 7, 8, 9]
random.shuffle(data)
print(data)
```

#### 6.随机0.xxxxx数

```python
text = random.random()
print(text) # 0.30696537105563704
```





### 4 hashlib md5加密

```python
import hashlib

hash_object = hashlib.md5()
hash_object.update("456789".encode('utf-8'))
result = hash_object.hexdigest()
print(result)
```

```python
import hashlib

hash_object = hashlib.md5("iajfsdunjaksdjfasdfasdf".encode('utf-8'))
hash_object.update(54984984".encode('utf-8'))
result = hash_object.hexdigest()
print(result)
```



### 5  json

json模块，是python内部的一个模块，可以将python的数据格式 转换为json格式的数据，也可以将json格式的数据转换为python的数据格式。

json格式，是一个数据格式（本质上就是个字符串，常用语网络数据传输）

#### 1 核心功能

json格式的作用

```
跨语言数据传输，例如：
	A系统用Python开发，有列表类型和字典类型等。
	B系统用Java开发，有数组、map等的类型。

	语言不同，基础数据类型格式都不同。
	
	为了方便数据传输，大家约定一个格式：json格式，每种语言都是将自己数据类型转换为json格式，也可以将json格式的数据转换为自己的数据类型。
```



![image-20210104123415566](assets/image-20210104123415566.png)

Python数据类型与json格式的相互转换：

- 数据类型 -> json ，一般称为：序列化

  ```python
  import json
  
  data = [
      {"id": 1, "name": "武沛齐", "age": 18},
      {"id": 2, "name": "alex", "age": 18},
  ]
  
  res = json.dumps(data)
  print(res) # '[{"id": 1, "name": "\u6b66\u6c9b\u9f50", "age": 18}, {"id": 2, "name": "alex", "age": 18}]'
  
  res = json.dumps(data, ensure_ascii=False)
  print(res) # '[{"id": 1, "name": "武沛齐", "age": 18}, {"id": 2, "name": "alex", "age": 18}]'
  ```

- json格式 -> 数据类型，一般称为：反序列化

  ```python
  import json
  
  data_string = '[{"id": 1, "name": "武沛齐", "age": 18}, {"id": 2, "name": "alex", "age": 18}]'
  
  data_list = json.loads(data_string)
  
  print(data_list)
  ```



#### 2 类型要求

python的数据类型转换为 json 格式，对数据类型是有要求的，默认只支持：

```
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
```

其他类型如果想要支持，需要自定义`JSONEncoder `才能实现【目前只需要了解大概意思即可】，例如：

```python
import json
from decimal import Decimal
from datetime import datetime

data = [
    {"id": 1, "name": "武沛齐", "age": 18, 'size': Decimal("18.99"), 'ctime': datetime.now()},
    {"id": 2, "name": "alex", "age": 18, 'size': Decimal("9.99"), 'ctime': datetime.now()},
]


class MyJSONEncoder(json.JSONEncoder):
    def default(self, o):
        if type(o) == Decimal:
            return str(o)
        elif type(o) == datetime:
            return o.strftime("%Y-%M-%d")
        return super().default(o)


res = json.dumps(data, cls=MyJSONEncoder)
print(res)
```



#### 3 其他功能

json模块中常用的是：

- `json.dumps`，序列化生成一个字符串。

- `json.loads`，发序列化生成python数据类型。

- `json.dump`，将数据序列化并写入文件（不常用）

  ```python
  import json
  
  data = [
      {"id": 1, "name": "武沛齐", "age": 18},
      {"id": 2, "name": "alex", "age": 18},
  ]
  
  file_object = open('xxx.json', mode='w', encoding='utf-8')
  
  json.dump(data, file_object)
  
  file_object.close()
  ```

- `json.load`，读取文件中的数据并反序列化为python的数据类型（不常用）

  ```python
  import json
  
  file_object = open('xxx.json', mode='r', encoding='utf-8')
  
  data = json.load(file_object)
  print(data)
  
  file_object.close()
  ```

  

### 6 time时间处理

- UTC/GMT：世界时间

- 本地时间：本地时区的时间。

```python
import time
```

#### 1  获取当前时间戳（自1970-1-1 00:00）

```python
v1 = time.time()
print(v1)
```

#### 2  时区

```python
v2 = time.timezone
```

#### 3 停止n秒，再执行后续的代码。

```python
time.sleep(5)
```



### 7  datetime 时间处理

```python
from datetime import datetime, timezone, timedelta
```

```python
from datetime import datetime
from datetime import timedelta
from datetime import timezone
 
SHA_TZ = timezone(
    timedelta(hours=8),
    name='Asia/Shanghai',
)
 
# 协调世界时
utc_now = datetime.utcnow().replace(tzinfo=timezone.utc)
print("UTC:")
print(utc_now, utc_now.time()) #2022-07-24 17:29:04.117146+00:00 17:29:04.117146
print(utc_now.date(), utc_now.tzname())	# 2022-07-24 UTC
 
# 北京时间
beijing_now = utc_now.astimezone(SHA_TZ)
print("Beijing:")
print(beijing_now.strftime('%H_%M_%S'))
print(beijing_now, beijing_now.time())	# 2022-07-25 01:29:04.117146+08:00 01:29:04.117146
print(beijing_now.date(), beijing_now.tzname())#2022-07-25 Asia/Shanghai
 
# 系统默认时区
local_now = utc_now.astimezone()
print("Default:")
print(local_now, local_now.time())#2022-07-25 01:29:04.117146+08:00 01:29:04.117146
print(local_now.date(), local_now.tzname())#2022-07-25 中国标准时间
```



#### 1 当前本地时间

```python
v1 = datetime.now()
print(v1)
```

#### 2 当前东7区时间

```python
tz = timezone(timedelta(hours=7))
v2 = datetime.now(tz)
print(v2)
```

#### 3  当前UTC时间

```python
v3 = datetime.utcnow()
print(v3)
```

#### 4  字符串格式的时间  转换为datetime格式时间

```python
text = "2021-11-11"
v1 = datetime.strptime(text,'%Y-%m-%d') # %Y 年，%m，月份，%d，天。
print(v1)
```

#### 5 datetime格式 转换为字符串格式

```python
v1 = datetime.now()
val = v1.strftime("%Y-%m-%d %H:%M:%S")
print(val)
```

#### 6 时间戳格式 转换为datetime格式

```python
ctime = time.time() # 11213245345.123
v1 = datetime.fromtimestamp(ctime)
print(v1)
```

#### 7  datetime格式 转换为时间戳格式

```python
v1 = datetime.now()
val = v1.timestamp()
print(val)
```







### 8 re 正则表达式

##### 1. 字符相关

- `wupeiqi` 匹配文本中的wupeiqi

  ```python
  import re
  
  text = "你好wupeiqi,阿斯顿发wupeiqasd 阿士大夫能接受的wupeiqiff"
  data_list = re.findall("wupeiqi", text)
  print(data_list) # ['wupeiqi', 'wupeiqi'] 可用于计算字符串中某个字符出现的次数
  ```

- `[abc]` 匹配a或b或c 字符。

  ```python
  import re
  
  text = "你2b好wupeiqi,阿斯顿发awupeiqasd 阿士大夫a能接受的wffbbupqaceiqiff"
  data_list = re.findall("[abc]", text)
  print(data_list) # ['b', 'a', 'a', 'a', 'b', 'b', 'c']
  ```

  ```python
  import re
  
  text = "你2b好wupeiqi,阿斯顿发awupeiqasd 阿士大夫a能接受的wffbbupqcceiqiff"
  data_list = re.findall("q[abc]", text)
  print(data_list) # ['qa', 'qc']
  ```

- `[^abc]` 匹配除了abc意外的其他字符。

  ```python
  import re
  
  text = "你wffbbupceiqiff"
  data_list = re.findall("[^abc]", text)
  print(data_list)  # ['你', 'w', 'f', 'f', 'u', 'p', 'e', 'i', 'q', 'i', 'f', 'f']
  ```

- `[a-z]`  匹配a~z的任意字符（ [0-9]也可以 ）。

  ```python
  import re
  
  text = "alexrootrootadmin"
  data_list = re.findall("t[a-z]", text)
  print(data_list)  # ['tr', 'ta']
  ```

  - `.`  代指除换行符以外的任意字符。


  ```python
import re

text = "alexraotrootadmin"
data_list = re.findall("r.o", text)
print(data_list) # ['rao', 'roo']
  ```

  ```python
import re

text = "alexraotrootadmin"
data_list = re.findall("r.+o", text) # 贪婪匹配
print(data_list) # ['raotroo']
  ```

  ```python
import re

text = "alexraotrootadmin"
data_list = re.findall("r.+?o", text) # 非贪婪匹配
print(data_list) # ['rao']
  ```

- `\w` 代指字母或数字或下划线（汉字）。

  ```python
  import re
  
  text = "北京武沛alex齐北  京武沛alex齐"
  data_list = re.findall("武\w+x", text)
  print(data_list) # ['武沛alex', '武沛alex']
  ```

- `\d` 代指数字

  ```python
  import re
  
  text = "root-ad32min-add3-admd1in"
  data_list = re.findall("d\d", text)
  print(data_list) # ['d3', 'd3', 'd1']
  ```

  ```python
  import re
  
  text = "root-ad32min-add3-admd1in"
  data_list = re.findall("d\d+", text)
  print(data_list) # ['d32', 'd3', 'd1']
  ```

- `\s` 代指任意的空白符，包括空格、制表符等。

  ```python
  import re
  
  text = "root admin add admin"
  data_list = re.findall("a\w+\s\w+", text)
  print(data_list) # ['admin add']
  ```

  

##### 2. 数量相关

- `*` 重复0次或更多次

  ```python
  import re
  
  text = "他是大B个，确实是个大2B。"
  data_list = re.findall("大2*B", text)
  print(data_list) # ['大B', '大2B']
  ```

- `+` 重复1次或更多次

  ```python
  import re
  
  text = "他是大B个，确实是个大2B，大3B，大66666B。"
  data_list = re.findall("大\d+B", text)
  print(data_list) # ['大2B', '大3B', '大66666B']
  ```

- `?` 重复0次或1次

  ```python
  import re
  
  text = "他是大B个，确实是个大2B，大3B，大66666B。"
  data_list = re.findall("大\d?B", text)
  print(data_list) # ['大B', '大2B', '大3B']
  ```

- `{n}` 重复n次

  ```python
  import re
  
  text = "楼主太牛逼了，在线想要 442662578@qq.com和xxxxx@live.com谢谢楼主，手机号也可15131255789，搞起来呀"
  data_list = re.findall("151312\d{5}", text)
  print(data_list) # ['15131255789']
  ```

- `{n,}` 重复n次或更多次

  ```python
  import re
  
  text = "楼主太牛逼了，在线想要 442662578@qq.com和xxxxx@live.com谢谢楼主，手机号也可15131255789，搞起来呀"
  data_list = re.findall("\d{9,}", text)
  print(data_list) # ['442662578', '15131255789']
  
  ```

- `{n,m}` 重复n到m次

  ```python
  import re
  
  text = "楼主太牛逼了，在线想要 442662578@qq.com和xxxxx@live.com谢谢楼主，手机号也可15131255789，搞起来呀"
  data_list = re.findall("\d{10,15}", text)
  print(data_list) # ['15131255789']
  ```



##### 3. 括号（分组）

- 提取数据区域

  ```python
  import re
  
  text = "楼主太牛逼了，在线想要 442662578@qq.com和xxxxx@live.com谢谢楼主，手机号也可15131255789，搞起来呀"
  data_list = re.findall("15131(2\d{5})", text)
  print(data_list)  # ['255789']
  ```

  ```python
  import re
  
  text = "楼主太牛逼了，在线想要 442662578@qq.com和xxxxx@live.com谢谢楼主，手机号也可15131255789，搞起来15131266666呀"
  data_list = re.findall("15(13)1(2\d{5})", text)
  print(data_list)  # [ ('13', '255789')   ]
  ```

  

  ```python
  import re
  
  text = "楼主太牛逼了，在线想要 442662578@qq.com和xxxxx@live.com谢谢楼主，手机号也可15131255789，搞起来呀"
  data_list = re.findall("(15131(2\d{5}))", text)
  print(data_list)  # [('15131255789', '255789')]
  ```

  

- 获取指定区域 + 或条件

  ```python
  import re
  
  text = "楼主15131root太牛15131alex逼了，在线想要 442662578@qq.com和xxxxx@live.com谢谢楼主，手机号也可15131255789，搞起来呀"
  data_list = re.findall("15131(2\d{5}|r\w+太)", text)
  print(data_list)  # ['root太', '255789']
  ```

  ```python
  import re
  
  text = "楼主15131root太牛15131alex逼了，在线想要 442662578@qq.com和xxxxx@live.com谢谢楼主，手机号也可15131255789，搞起来呀"
  data_list = re.findall("(15131(2\d{5}|r\w+太))", text)
  print(data_list)  # [('15131root太', 'root太'), ('15131255789', '255789')]
  ```



##### 4. 起始和结束

上述示例中都是去一段文本中提取数据，只要文本中存在即可。

但，如果要求用户输入的内容必须是指定的内容开头和结尾，比就需要用到如下两个字符。

- `^` 开始
- `$` 结束

```python
import re

text = "啊442662578@qq.com我靠"
email_list = re.findall("^\w+@\w+.\w+$", text, re.ASCII)
print(email_list) # []
```

```python
import re

text = "442662578@qq.com"
email_list = re.findall("^\w+@\w+.\w+$", text, re.ASCII)
print(email_list) # ['442662578@qq.com']
```



这种一般用于对用户输入数据格式的校验比较多，例如：

```python
import re

text = input("请输入邮箱：")
email = re.findall("^\w+@\w+.\w+$", text, re.ASCII)
if not email:
    print("邮箱格式错误")
else:
    print(email)
```



##### 5. 特殊字符

由于正则表达式中 `*  .  \ { } ( ) ` 等都具有特殊的含义，所以如果想要在正则中匹配这种指定的字符，需要转义，例如：

```python
import re

text = "我是你{5}爸爸"
data = re.findall("你{5}爸", text)
print(data) # []
```

```python
import re

text = "我是你{5}爸爸"
data = re.findall("你\{5\}爸", text)
print(data)
```

#### re 的方法

- findall，获取匹配到的所有数据

  ```python
  import re
  
  text = "dsf130429191912015219k13042919591219521Xkk"
  data_list = re.findall("(\d{6})(\d{4})(\d{2})(\d{2})(\d{3})([0-9]|X)", text)
  print(data_list) # [('130429', '1919', '12', '01', '521', '9'), ('130429', '1959', '12', '19', '521', 'X')]
  ```

- match，从起始位置开始匹配，匹配成功返回一个对象，未匹配成功返回None

  ```python
  import re
  
  text = "大小逗2B最逗3B欢乐"
  data = re.match("逗\dB", text)
  print(data) # None
  ```

  ```python
  import re
  
  text = "逗2B最逗3B欢乐"
  data = re.match("逗\dB", text)
  if data:
      content = data.group() # "逗2B"
      print(content)
  ```

- search，浏览整个字符串去匹配第一个，未匹配成功返回None

  ```python
  import re
  
  text = "大小逗2B最逗3B欢乐"
  data = re.search("逗\dB", text)
  if data:
      print(data.group())  # "逗2B"
  ```

- sub，替换匹配成功的位置

  ```python
  import re
  
  text = "逗2B最逗3B欢乐"
  data = re.sub("\dB", "沙雕", text)
  print(data) # 逗沙雕最逗沙雕欢乐
  ```

  ```python
  import re
  
  text = "逗2B最逗3B欢乐"
  data = re.sub("\dB", "沙雕", text, 1)
  print(data) # 逗沙雕最逗3B欢乐
  ```

- split，根据匹配成功的位置分割

  ```python
  import re
  
  text = "逗2B最逗3B欢乐"
  data = re.split("\dB", text)
  print(data) # ['逗', '最逗', '欢乐']
  ```

  ```python
  import re
  
  text = "逗2B最逗3B欢乐"
  data = re.split("\dB", text, 1)
  print(data) # ['逗', '最逗3B欢乐']
  ```

- finditer：获取的迭代器

  ![image-20220327124106675](python神功.assets/image-20220327124106675.png)

  ```python
  import re
  
  text = "逗2B最逗3B欢乐"
  data = re.finditer("\dB", text)
  for item in data:
      print(item.group())# group()括号内可以填分组名
  ```

  ```python
  import re
  
  text = "逗2B最逗3B欢乐"
  data = re.finditer("(?P<xx>\dB)", text)  # 命名分组
  for item in data:
      print(item.groupdict())
  ```

  ```python
  text = "dsf130429191912015219k13042919591219521Xkk"
  data_list = re.finditer("\d{6}(?P<year>\d{4})(?P<month>\d{2})(?P<day>\d{2})\d{3}[\d|X]", text)
  for item in data_list:
      info_dict = item.groupdict()
      print(info_dict)
  ```

  compile:正则分组

  ```python
  obj = re.compile(
      r'<div class="source">.*?_play_web@2x.png"/>(?P<movie>.*?)</a>.*?<span class="rating_nums">(?P<score>.*?)</span>.*?年份:(?P<years>.*?)</div>',
      re.S)
  
  a1 = requests.get(url=url, headers=ko).text# 获取的文本
  a2 = obj.finditer(a1) # 直接通过obj变量调用获取内容。
  ```

  





### 9  copy拷贝

#### 1 浅拷贝

- 不可变类型，不拷贝。

  ```python
  import copy
  
  v1 = "武沛齐"
  print(id(v1)) # 140652260947312
  
  v2 = copy.copy(v1) 
  print(id(v2)) # 140652260947312
  ```

  按理说拷贝v1之后，v2的内存地址应该不同，但由于python内部优化机制，内存地址是相同的，因为对不可变类型而言，如果以后修改值，会重新创建一份数据，不会影响原数据，所以，不拷贝也无妨。

- 可变类型，只拷贝第一层。

  ```python
  import copy
  
  v1 = ["武沛齐", "root", [44, 55]]
  print(id(v1))  # 140405837216896
  print(id(v1[2]))  # 140405837214592
  
  v2 = copy.copy(v1)
  print(id(v2))  # 140405837214784
  print(id(v2[2]))  # 140405837214592
  ```

  ![image-20210106151332792](assets/image-20210106151332792.png)

#### 2 深拷贝

- 不可变类型，不拷贝

  ```python
  import copy
  
  v1 = "武沛齐"
  print(id(v1))  # 140188538697072
  
  v2 = copy.deepcopy(v1)
  print(id(v2))  # 140188538697072
  ```

  特殊的元组：

  - 元组元素中无可变类型，不拷贝

    ```python
    import copy
    
    v1 = ("武沛齐", "root")
    print(id(v1))  # 140243298961984
    
    v2 = copy.deepcopy(v1)
    print(id(v2))  # 140243298961984
    ```

  - 元素元素中有可变类型，找到所有【可变类型】或【含有可变类型的元组】   均拷贝一份

    ```python
    import copy
    
    v1 = ("武沛齐", "root", [11, [44, 55], (11, 22), (11, [], 22), 33])
    v2 = copy.deepcopy(v1)
    
    print(id(v1))  # 140391475456384
    print(id(v2))  # 140391475456640
    
    print(id(v1[2]))  # 140352552779008
    print(id(v2[2]))  # 140352552920448
    
    print(id(v1[2][1]))  # 140642999940480
    print(id(v2[2][1]))  # 140643000088832
    
    print(id(v1[2][2]))  # 140467039914560
    print(id(v2[2][2]))  # 140467039914560
    
    print(id(v1[2][3]))  # 140675479841152
    print(id(v2[2][3]))  # 140675480454784
    ```

- 可变类型，找到所有层级的 【可变类型】或【含有可变类型的元组】   均拷贝一份

  ```python
  import copy
  
  v1 = ["武沛齐", "root", [11, [44, 55], (11, 22), (11, [], 22), 33]]
  v2 = copy.deepcopy(v1)
  
  print(id(v1))  # 140391475456384
  print(id(v2))  # 140391475456640
  
  print(id(v1[2]))  # 140352552779008
  print(id(v2[2]))  # 140352552920448
  
  print(id(v1[2][1]))  # 140642999940480
  print(id(v2[2][1]))  # 140643000088832
  
  print(id(v1[2][2]))  # 140467039914560
  print(id(v2[2][2]))  # 140467039914560
  
  print(id(v1[2][3]))  # 140675479841152
  print(id(v2[2][3]))  # 140675480454784
  ```

  ```python
  import copy
  
  v1 = ["武沛齐", "root", [44, 55]]
  v2 = copy.deepcopy(v1)
  
  print(id(v1))  # 140405837216896
  print(id(v2))  # 140405837214784
  
  
  print(id(v1[2]))  # 140563140392256
  print(id(v2[2]))  # 140563140535744
  ```

  ![image-20210106152704591](assets/image-20210106152704591.png)

  





## 项目开发规范

现阶段，我们在开发一些程序时（终端运行），应该遵循一些结构的规范，让你的系统更加专业。



### 2.1 单文件应用

当基于python开发简单应用时（一个py文件就能搞定），需要注意如下几点。

```python
"""
文件注释
"""

import re
import random

import requests
from openpyxl import load_workbook

DB = "XXX"


def do_something():
    """ 函数注释 """

    # TODO 待完成时，下一期实现xxx功能
    for i in range(10):
        pass


def run():
    """ 函数注释 """

    # 对功能代码进行注释
    text = input(">>>")
    print(text)


if __name__ == '__main__':
    run()
```



<img src="assets/image-20210105160728297.png" alt="image-20210105160728297" style="zoom:50%;" />





### 2.2 单可执行文件

新创建一个项目，假设名字叫 【crm】，可以创建如下文件和文件夹来存放代码和数据。

```python
crm
├── app.py        文件，程序的主文件（尽量精简）
├── config.py     文件，配置文件（放相关配置信息，代码中读取配置信息，如果想要修改配置，即可以在此修改，不用再去代码中逐一修改了）
├── db            文件夹，存放数据
├── files         文件夹，存放文件
├── src           包，业务处理的代码
└── utils         包，公共功能
```

示例程序见附件：crm.zip

![image-20210105163335127](assets/image-20210105163335127.png)



### 2.3 多可执行文件

新创建项目，假设名称叫【killer】，可以创建如下文件和文件夹来存放代码和数据。

```
killer
├── bin					文件夹，存放多个主文件（可运行）
│   ├── app1.py
│   └── app2.py
├── config              包，配置文件
│   ├── __init__.py
│   └── settings.py
├── db                  文件夹，存放数据
├── files               文件夹，存放文件
├── src                 包，业务代码
│   └── __init__.py
└── utils               包，公共功能
    └── __init__.py
```

















# 七 文件操作

### 1.读文件

**读文本文件**

- **open( )**   打开文件    (文件路径，`r`只读模式`t`文本，utf-8编码打开)
- **read()**    读取文件内容，并赋值给data
- **close()**   关闭文件

```python
file_object = open('info.txt', mode='rt', encoding='utf-8')

data = file_object.read()

file_object.close()

print(data)#打印文本
```

**读图片等非文本内容文件**

- **open( )**   打开文件    (文件路径，`r`只读模式`b`二进制文件，utf-8编码打开)
- **read()**    读取文件内容，并赋值给data
- **close()**   关闭文件

```python
file_object = open('a1.png', mode='rb')
data = file_object.read()
file_object.close()
print(data) # \x91\xf6\xf2\x83\x8aQFfv\x8b7\xcc\xed\xc3}\x7fT\x9d{.3.\xf1{\xe8\...
```

**常见功能**

- **read（）**，读所有【常用】r模式（）内可设读多少字符，rb模式可设读多少字节

- **readline（）**，读一行

- **readlines（）**，读所有行，每行作为列表的一个元素

- **循环文本**，读大文件（readline加强版）【常见】直接循环打开的文本内容

  ```python
  f = open('info.txt', mode='r', encoding='utf-8')
  for line in f:
      print(line.strip())
  f.close()
  ```

  

### 2.写文件

**写文本文件**

- **open( ) **           打开文件
- **wt**                   要求写入的内容需要是文本类型
- **write( )**           写入内容
- close( )             文件关闭

```python
file_object = open("t1.txt", mode='wt', encoding='utf-8')

file_object.write("武沛齐")

file_object.close()
```

写非文本文件把`wt`换成`wb`

**常见功能**

- **write( )**，写  ,不是写到了硬盘，而是写在缓冲区，系统会将缓冲区的内容刷到硬盘

- **flush( )**，刷到硬盘,马上刷到硬盘

  ```python
  f = open('info.txt', mode='a',encoding='utf-8')
  while True:
  	f.write("武沛齐")
      f.flush()
  f.close(
  ```

- **seek(  )**,移动光标位置（字节）,括号内选择到指定字节的位置,utf-8中文会占3个字节

  ```python
  f = open('info.txt', mode='r+', encoding='utf-8')
  f.seek(3)
  f.write("武沛齐")
  f.close()
  ```

  注意：在a模式下，调用write在文件中写入内容时，永远只能将内容写入到尾部，不会写到光标的位置。

- **tell()**  ,获取当前光标位置，utf-8中文会占3个字节

  ```python
  f = open('info.txt', mode='r', encoding='utf-8')
  p1 = f.tell()
  print(p1)  # 0
  f.read(3)  # 读3个字符 3*3=9字节
  p2 = f.tell()
  print(p2)  # 9
  f.close()
  ```

  

### 3.文件打开模式

关于文件的打开模式常见应用有：

- 只读：`r`、`rt`、`rb` （用）默认光标位置：起始位置

  - 存在，读
  - 不存在，报错

- 只写：`w`、`wt`、`wb`（用）起始位置（清空文件）

  - 存在，清空再写
  - 不存在，创建再写

- 只写：`x`、`xt`、`xb`起始位置（新文件）

  - 存在，报错
  - 不存在，创建再写。

- 只写：`a`、`at`、`ab`【尾部追加】（用）默认光标位置：末尾

  - 存在，尾部追加。
  - 不存在，创建再写。

### 4.上下文管理

with上下文管理，它可以自动实现关闭文件

```python
with open("xxxx.txt", mode='rb') as file_object:
    data = file_object.read()
    print(data)
```

在Python 2.7 后，with又支持同时对多个文件的上下文进行管理，即：

```python
with open("xxxx.txt", mode='rb') as f1, open("xxxx.txt", mode='rb') as f2:
    pass
```

### 5 .csv文件相关

**逗号分隔值**（Comma-Separated Values，**CSV**，有时也称为**字符分隔值**，因为分隔字符也可以不是逗号），其文件以纯文本形式存储表格数据（数字和文本）。

### 6 .ini格式文件

ini文件是Initialization File的缩写，平时用于存储软件的的配置文件。例如：MySQL数据库的配置文件。

```ini
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
log-bin=py-mysql-bin
character-set-server=utf8
collation-server=utf8_general_ci
log-error=/var/log/mysqld.log
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0

[mysqld_safe]
log-error=/var/log/mariadb/mariadb.log
pid-file=/var/run/mariadb/mariadb.pid

[client]
default-character-set=utf8
```

这种格式是可以直接使用open来出来，考虑到自己处理比较麻烦，所以Python为我们提供了更为方便的方式。

```python
import configparser

config = configparser.ConfigParser()
config.read('files/my.ini', encoding='utf-8')
# config.read('/Users/wupeiqi/PycharmProjects/luffyCourse/day09/files/my.ini', encoding='utf-8')

# 1.获取所有的节点
"""
result = config.sections()
print(result)  # ['mysqld', 'mysqld_safe', 'client']
"""

# 2.获取节点下的键值
"""
result = config.items("mysqld_safe")
print(result)  # [('log-error', '/var/log/mariadb/mariadb.log'), ('pid-file', '/var/run/mariadb/mariadb.pid')]

for key, value in config.items("mysqld_safe"):
    print(key, value)
"""

# 3.获取某个节点下的键对应的值
"""
result = config.get("mysqld","collation-server")
print(result)
"""

# 4.其他

# 4.1 是否存在节点
# v1 = config.has_section("client")
# print(v1)

# 4.2 添加一个节点
# config.add_section("group")
# config.set('group','name','wupeiqi')
# config.set('client','name','wupeiqi')
# config.write(open('files/new.ini', mode='w', encoding='utf-8'))

# 4.3 删除
# config.remove_section('client')
# config.remove_option("mysqld", "datadir")
# config.write(open('files/new.ini', mode='w', encoding='utf-8'))
```

- 读取所有节点

  ```python
  import configparser
  
  config = configparser.ConfigParser()
  config.read('/Users/wupeiqi/PycharmProjects/luffyCourse/day09/files/my.conf', encoding='utf-8')
  # config.read('my.conf', encoding='utf-8')
  ret = config.sections()
  print(ret) 
  
  >>输出
  ['mysqld', 'mysqld_safe', 'client']
  ```

- 读取节点下的键值

  ```python
  import configparser
  
  config = configparser.ConfigParser()
  config.read('/Users/wupeiqi/PycharmProjects/luffyCourse/day09/files/my.conf', encoding='utf-8')
  # config.read('my.conf', encoding='utf-8')
  item_list = config.items("mysqld_safe")
  print(item_list) 
  
  >>输出
  [('log-error', '/var/log/mariadb/mariadb.log'), ('pid-file', '/var/run/mariadb/mariadb.pid')]
  ```

- 读取节点下值（根据 节点+键 ）

  ```python
  import configparser
  
  config = configparser.ConfigParser()
  config.read('/Users/wupeiqi/PycharmProjects/luffyCourse/day09/files/my.conf', encoding='utf-8')
  
  value = config.get('mysqld', 'log-bin')
  print(value)
  
  >>输出
  py-mysql-bin
  ```

- 检查、删除、添加节点

  ```python
  import configparser
  
  config = configparser.ConfigParser()
  config.read('/Users/wupeiqi/PycharmProjects/luffyCourse/day09/files/my.conf', encoding='utf-8')
  # config.read('my.conf', encoding='utf-8')
  
  
  # 检查
  has_sec = config.has_section('mysqld')
  print(has_sec)
  
  # 添加节点
  config.add_section("SEC_1")
  # 节点中设置键值
  config.set('SEC_1', 'k10', "123")
  config.set('SEC_1', 'name', "哈哈哈哈哈")
  
  config.add_section("SEC_2")
  config.set('SEC_2', 'k10', "123")
  # 内容写入新文件
  config.write(open('/Users/wupeiqi/PycharmProjects/luffyCourse/day09/files/xxoo.conf', 'w'))
  
  
  # 删除节点
  config.remove_section("SEC_2")
  # 删除节点中的键值
  config.remove_option('SEC_1', 'k10')
  config.write(open('/Users/wupeiqi/PycharmProjects/luffyCourse/day09/files/new.conf', 'w'))7 .XML格式文件
  ```

### 7 .XML格式文件

[可扩展标记语言](https://baike.baidu.com/item/可扩展标记语言/2885849)，是一种简单的数据存储语言，XML 被设计用来传输和存储数据。

  - 存储，可用来存放配置文件，例如：java的配置文件。

- 传输，网络传输时以这种格式存在，例如：早期ajax传输的数据、soap协议等。

  ```xml
  <data>
      <country name="Liechtenstein">
          <rank updated="yes">2</rank>
          <year>2023</year>
          <gdppc>141100</gdppc>
          <neighbor direction="E" name="Austria" />
          <neighbor direction="W" name="Switzerland" />
      </country>
      <country name="Singapore">
          <rank updated="yes">5</rank>
          <year>2026</year>
          <gdppc>59900</gdppc>
          <neighbor direction="N" name="Malaysia" />
      </country>
      <country name="Panama">
          <rank updated="yes">69</rank>
          <year>2026</year>
          <gdppc>13600</gdppc>
          <neighbor direction="W" name="Costa Rica" />
          <neighbor direction="E" name="Colombia" />
      </country>
  </data>
  ```

```
  
注意：在Python开发中用的相对来比较少，大家作为了解即可（后期课程在讲解微信支付、微信公众号消息处理 时会用到基于xml传输数据）。
  
例如：https://developers.weixin.qq.com/doc/offiaccount/Message_Management/Receiving_standard_messages.html
  
#### 1 读取文件和内容
  
  ```python
  from xml.etree import ElementTree as ET
  
  # ET去打开xml文件
  tree = ET.parse("files/xo.xml")
  
  # 获取根标签
  root = tree.getroot()
  
  print(root) # <Element 'data' at 0x7f94e02763b0>
```

  ```python
from xml.etree import ElementTree as ET

content = """
<data>
    <country name="Liechtenstein">
        <rank updated="yes">2</rank>
        <year>2023</year>
        <gdppc>141100</gdppc>
        <neighbor direction="E" name="Austria" />
        <neighbor direction="W" name="Switzerland" />
    </country>
     <country name="Panama">
        <rank updated="yes">69</rank>
        <year>2026</year>
        <gdppc>13600</gdppc>
        <neighbor direction="W" name="Costa Rica" />
        <neighbor direction="E" name="Colombia" />
    </country>
</data>
"""

root = ET.XML(content)
print(root)  # <Element 'data' at 0x7fdaa019cea0>
  ```

**2 读取节点数据**

  ```python
from xml.etree import ElementTree as ET

content = """
<data>
    <country name="Liechtenstein" id="999" >
        <rank>2</rank>
        <year>2023</year>
        <gdppc>141100</gdppc>
        <neighbor direction="E" name="Austria" />
        <neighbor direction="W" name="Switzerland" />
    </country>
     <country name="Panama">
        <rank>69</rank>
        <year>2026</year>
        <gdppc>13600</gdppc>
        <neighbor direction="W" name="Costa Rica" />
        <neighbor direction="E" name="Colombia" />
    </country>
</data>
"""

# 获取根标签 data
root = ET.XML(content)

country_object = root.find("country")
print(country_object.tag, country_object.attrib)
gdppc_object = country_object.find("gdppc")
print(gdppc_object.tag,gdppc_object.attrib,gdppc_object.text)
  ```

  ```python
from xml.etree import ElementTree as ET

content = """
<data>
    <country name="Liechtenstein">
        <rank>2</rank>
        <year>2023</year>
        <gdppc>141100</gdppc>
        <neighbor direction="E" name="Austria" />
        <neighbor direction="W" name="Switzerland" />
    </country>
     <country name="Panama">
        <rank>69</rank>
        <year>2026</year>
        <gdppc>13600</gdppc>
        <neighbor direction="W" name="Costa Rica" />
        <neighbor direction="E" name="Colombia" />
    </country>
</data>
"""

# 获取根标签 data
root = ET.XML(content)

# 获取data标签的孩子标签
for child in root:
    # child.tag = conntry
    # child.attrib = {"name":"Liechtenstein"}
    print(child.tag, child.attrib)
    for node in child:
        print(node.tag, node.attrib, node.text)
  ```

  ```python
from xml.etree import ElementTree as ET

content = """
<data>
    <country name="Liechtenstein">
        <rank>2</rank>
        <year>2023</year>
        <gdppc>141100</gdppc>
        <neighbor direction="E" name="Austria" />
        <neighbor direction="W" name="Switzerland" />
    </country>
     <country name="Panama">
        <rank>69</rank>
        <year>2026</year>
        <gdppc>13600</gdppc>
        <neighbor direction="W" name="Costa Rica" />
        <neighbor direction="E" name="Colombia" />
    </country>
</data>
"""

root = ET.XML(content)

for child in root.iter('year'):
    print(child.tag, child.text)
  ```

  ```python
from xml.etree import ElementTree as ET

content = """
<data>
    <country name="Liechtenstein">
        <rank>2</rank>
        <year>2023</year>
        <gdppc>141100</gdppc>
        <neighbor direction="E" name="Austria" />
        <neighbor direction="W" name="Switzerland" />
    </country>
     <country name="Panama">
        <rank>69</rank>
        <year>2026</year>
        <gdppc>13600</gdppc>
        <neighbor direction="W" name="Costa Rica" />
        <neighbor direction="E" name="Colombia" />
    </country>
</data>
"""

root = ET.XML(content)
v1 = root.findall('country')
print(v1)

v2 = root.find('country').find('rank')
print(v2.text)
  ```



**3 修改和删除节点**

  ```python
from xml.etree import ElementTree as ET

content = """
<data>
    <country name="Liechtenstein">
        <rank>2</rank>
        <year>2023</year>
        <gdppc>141100</gdppc>
        <neighbor direction="E" name="Austria" />
        <neighbor direction="W" name="Switzerland" />
    </country>
     <country name="Panama">
        <rank>69</rank>
        <year>2026</year>
        <gdppc>13600</gdppc>
        <neighbor direction="W" name="Costa Rica" />
        <neighbor direction="E" name="Colombia" />
    </country>
</data>
"""

root = ET.XML(content)

# 修改节点内容和属性
rank = root.find('country').find('rank')
print(rank.text)
rank.text = "999"
rank.set('update', '2020-11-11')
print(rank.text, rank.attrib)
############ 保存文件 ############
tree = ET.ElementTree(root)
tree.write("new.xml", encoding='utf-8')


# 删除节点
root.remove( root.find('country') )
print(root.findall('country'))

############ 保存文件 ############
tree = ET.ElementTree(root)
tree.write("newnew.xml", encoding='utf-8')
  ```



**4 构建文档**

  ```xml
<home>
    <son name="儿1">
        <grandson name="儿11"></grandson>
        <grandson name="儿12"></grandson>
    </son>
    <son name="儿2"></son>
</home>
  ```



  ```python
from xml.etree import ElementTree as ET

# 创建根标签
root = ET.Element("home")

# 创建节点大儿子
son1 = ET.Element('son', {'name': '儿1'})
# 创建小儿子
son2 = ET.Element('son', {"name": '儿2'})

# 在大儿子中创建两个孙子
grandson1 = ET.Element('grandson', {'name': '儿11'})
grandson2 = ET.Element('grandson', {'name': '儿12'})
son1.append(grandson1)
son1.append(grandson2)

# 把儿子添加到根节点中
root.append(son1)
root.append(son2)

tree = ET.ElementTree(root)
tree.write('oooo.xml', encoding='utf-8', short_empty_elements=False)
  ```



  ```xml
<famliy>
    <son name="儿1">
        <grandson name="儿11"></grandson>
        <grandson name="儿12"></grandson>
    </son>
    <son name="儿2"></son>
</famliy>
  ```

  ```python
from xml.etree import ElementTree as ET

# 创建根节点
root = ET.Element("famliy")


# 创建大儿子
son1 = root.makeelement('son', {'name': '儿1'})
# 创建小儿子
son2 = root.makeelement('son', {"name": '儿2'})

# 在大儿子中创建两个孙子
grandson1 = son1.makeelement('grandson', {'name': '儿11'})
grandson2 = son1.makeelement('grandson', {'name': '儿12'})

son1.append(grandson1)
son1.append(grandson2)


# 把儿子添加到根节点中
root.append(son1)
root.append(son2)

tree = ET.ElementTree(root)
tree.write('oooo.xml',encoding='utf-8')
  ```





  ```xml
<famliy>
	<son name="儿1">
    	<age name="儿11">孙子</age>
    </son>
	<son name="儿2"></son>
</famliy>
  ```

  ```python
from xml.etree import ElementTree as ET


# 创建根节点
root = ET.Element("famliy")


# 创建节点大儿子
son1 = ET.SubElement(root, "son", attrib={'name': '儿1'})
# 创建小儿子
son2 = ET.SubElement(root, "son", attrib={"name": "儿2"})

# 在大儿子中创建一个孙子
grandson1 = ET.SubElement(son1, "age", attrib={'name': '儿11'})
grandson1.text = '孙子'


et = ET.ElementTree(root)  #生成文档对象
et.write("test.xml", encoding="utf-8")
  ```



  ```xml
<user><![CDATA[你好呀]]</user>
  ```

  ```python
from xml.etree import ElementTree as ET

# 创建根节点
root = ET.Element("user")
root.text = "<![CDATA[你好呀]]"

et = ET.ElementTree(root)  # 生成文档对象
et.write("test.xml", encoding="tf-8")
  ```

### 8 Excel格式文件

Python内部未提供处理Excel文件的功能，想要在Python中操作Excel需要按照第三方的模块。

```
pip install openpyxl
```

#### 1 读Excel

##### 1导入模块

```python
from openpyxl import load_workbook
```

##### 2 打开.xlsx文件: **load_workbook(文件路径)**

```python
wb = load_workbook("files/p1.xlsx")
```

##### 3 sheet相关操作

1.获取excel文件中的所有sheet名称：**sheetnames**

```python
print(wb.sheetnames) # ['数据导出', '用户列表', 'Sheet1', 'Sheet2']
```

2.选择sheet，基于sheet名称

```python
sheet = wb["数据导出"]
```

3.选择sheet，基于索引位置:**worksheets[0]**

```python
sheet = wb.worksheets[0]
```

4 循环所有的sheet

```python
for name in wb.sheetnames:#获取excel文件中的所有sheet名称
    sheet = wb[name]
    cell = sheet.cell(1, 1)
    print(cell.value)
    

```

##### 4 读sheet中单元格的数据

1.获取第N行第N列的单元格(位置是从1开始）

```python
cell = sheet.cell(1, 1)#行，列
print(cell.value)#单元格内的值
print(cell.style)
print(cell.font)
print(cell.alignment)
```

2.获取某个单元格

```python
c1 = sheet["A2"]
print(c1.value)
```

3.第N行所有的单元格

```python
for cell in sheet[1]:
    print(cell.value)
```

4.所有行的数据（获取某一列数据）

```python
for row in sheet.rows:
    print(row[0].value, row[1].value)
```

5.获取所有列的数据

```python
for col in sheet.columns:
    print(col[1].value)
```

6 获取工作表属性

得到工作表对象后，可以获取工作表的相应属性，包括“表名”、“行数”、“列数”

```python
name=worksheet.title  #获取表名

#获取该表相应的行数和列数
rows=worksheet.max_row
columns=worksheet.max_column
print(rows,columns)  #32 13
```



#### 2 写Excel

流程：导模块，打开.xlsx文件，打开sheet表, 找到单元格，修改，保存

##### 原Excel文件基础上写内容。写入方式

```python
cell = sheet.cell(1, 1)        # 找到单元格，并修改单元格的内容
cell.value = "新的开始"
wb.save("files/p2.xlsx")       # 将excel文件保存到p2.xlsx文件中
```

```python
sheet["B3"] = "Alex"          #找到单元格，并修改单元格的内容
wb.save("p2.xlsx")            # 将excel文件保存到p2.xlsx文件中
```

##### 获取某些单元格，修改值

```python
cell_list = sheet["B2":"C3"]  #获取sheet下B2到C3位置的单元格，2行.4个单元格
for row in cell_list:         #循环行
    for cell in row:          #循环行的值
        cell.value = "新的值"  #修改单元格值
wb.save("p2.xlsx")            #保存
```

##### 新创建Excel文件写内容。

```python
from openpyxl import workbook    #导入模块
wb = workbook.Workbook()         # 创建excel且默认会创建一个sheet（名称为Sheet）
sheet = wb.worksheets[0]         # 或 sheet = wb["Sheet"]，打开sheet
cell = sheet.cell(1, 1)          # 找到单元格，并修改单元格的内容
cell.value = "新的开始"
wb.save("files/p2.xlsx")         # 将excel文件保存到p2.xlsx文件中
```



#### 3 其他

##### 1 对齐方式

```python
horizontal，水平方向对齐方式："general", "left", "center", "right", "fill", "justify", "centerContinuous", "distributed"
vertical，垂直方向对齐方式："top", "center", "bottom", "justify", "distributed"
text_rotation，旋转角度。
wrap_text，是否自动换行。
```

```python
cell = sheet.cell(1, 1)

cell.alignment = Alignment(horizontal='center', vertical='distributed', text_rotation=45, wrap_text=True)
wb.save("p2.xlsx")
```

##### 2 边框

```python
# side的style有如下：dashDot','dashDotDot', 'dashed','dotted','double','hair', 'medium', 'mediumDashDot', 'mediumDashDotDot','mediumDashed', 'slantDashDot', 'thick', 'thin'
```

```python
cell = sheet.cell(9, 2)  

cell.border = Border(
    top=Side(style="thin", color="FFB6C1"), 
    bottom=Side(style="dashed", color="FFB6C1"),
    left=Side(style="dashed", color="FFB6C1"),
    right=Side(style="dashed", color="9932CC"),
    diagonal=Side(style="thin", color="483D8B"),  # 对角线
    diagonalUp=True,  # 左下 ~ 右上
    diagonalDown=True  # 左上 ~ 右下
)

wb.save("p2.xlsx")
```

```py
from openpyxl import load_workbook
from openpyxl.styles import Border, Side, colors

excel_address = r"E:\Coding\E_PythonWriting\Excel\openpyxl示例_7.xlsx"
wb = load_workbook(excel_address)
sht = wb.worksheets[0]

sht["D5"] = "测试"

border_set = Border(left=Side(style='thick', color=colors.RED),
                    right=Side(style='medium', color=colors.BLACK),
                    top=Side(style='double', color=colors.BLUE),
                    bottom=Side(style='dotted', color=colors.BLACK))

sht["D5"].border = border_set

wb.save(excel_address)
```



##### 3 字体

```python
cell = sheet.cell(5, 1)
#                      主题		大小		颜色				下划线			加粗
cell.font = Font(name="微软雅黑", size=45, color="ff0000", underline="single",bold=True)
wb.save("p2.xlsx")
```

##### 4 背景色

```python
cell = sheet.cell(5, 3)
cell.fill = PatternFill("solid", fgColor="99ccff")
wb.save("p2.xlsx")
```

##### 5 渐变背景色

```python
cell = sheet.cell(5, 5)
cell.fill = GradientFill("linear", stop=("FFFFFF", "99ccff", "000000"))
wb.save("p2.xlsx")
```

##### 6 宽高(索引从1开始)

```python
sheet.row_dimensions[1].height = 50
sheet.column_dimensions["E"].width = 100
wb.save("p2.xlsx")
```

##### 7 合并单元格

```python
sheet.merge_cells("B2:D8")
sheet.merge_cells(start_row=15, start_column=3, end_row=18, end_column=8)
wb.save("p2.xlsx")


sheet.unmerge_cells("B2:D8")
wb.save("p2.xlsx")
```

##### 8 写入公式

```python
sheet = wb.worksheets[3]
sheet["D1"] = "合计"
sheet["D2"] = "=B2*C2"
sheet["D3"] = "=SUM(B3,C3)"
sheet.move_range("B1:D3",cols=10, translate=True) # 自动翻译公式
wb.save("p2.xlsx")
```

##### 9 删除

```python
# idx，要删除的索引位置
# amount，从索引位置开始要删除的个数（默认为1）
sheet.delete_rows(idx=1, amount=20)
sheet.delete_cols(idx=1, amount=3)
wb.save("p2.xlsx")
```

##### 10 插入

```python
sheet.insert_rows(idx=5, amount=10)  # 第5行开始插入10行
sheet.insert_cols(idx=3, amount=2)   # 第三列前插入2列
wb.save("p2.xlsx")
```

##### 11 循环写内容

```python
sheet = wb["Sheet"]
cell_range = sheet['A1:C2']
for row in cell_range:
    for cell in row:
        cell.value = "xx"

for row in sheet.iter_rows(min_row=5, min_col=1, max_col=7, max_row=10):
    for cell in row:
        cell.value = "oo"
wb.save("p2.xlsx")
```

##### 12 移动

```python
# 将H2:J10范围的数据，向右移动15个位置、向上移动1个位置
sheet.move_range("H2:J10",rows=1, cols=15)
wb.save("p2.xlsx")

```

##### 13 打印区域

```python
sheet.print_area = "A1:D200"
wb.save("p2.xlsx")


# 打印时，每个页面的固定表头

sheet.print_title_cols = "A:D"
sheet.print_title_rows = "1:3"
wb.save("p2.xlsx")

```



##### 14 行高列宽

```py
import openpyxl
wb=openpyxl.Workbook()
sheet=wb.active

# 设置行高
sheet['A1']='行高被设置为 100'
sheet.row_dimensions[1].height=100

# 设置列宽
sheet['B2']='列宽被设置为 50'
sheet.column_dimensions['B'].width=50

wb.save('dimensions.xlsx')
```



##### 15 自动换行

```py
from openpyxl.styles import Alignment
# row=行 ， column=列 ，value =值 									true自动换行
sheet.cell(row=1, column=1, value=value).alignment = Alignment(wrapText=True)

```



##### 16 水平居中

```py
import openpyxl
from openpyxl.styles import Alignment

wb = openpyxl.Workbook()        # 创建一个excel文件
sheet = wb.active               # 获得一个的工作表
sheet.title = "边框控制"

# 纵向靠左  水平居中
align = Alignment(horizontal='left', vertical='center', wrap_text=True,wrapText=True)

sheet['A1'].alignment = align
sheet.cell(1, 1, "靠左，水平居中")

wb.save("./data/文字对齐方式.xlsx")
```







### 9 压缩文件

基于Python内置的shutil模块可以实现对压缩文件的操作。

- 1	压缩文件

```python
import shutil
# base_name，压缩后的压缩包文件
# format，压缩的格式，例如："zip", "tar", "gztar", "bztar", or "xztar".
# root_dir，要压缩的文件夹路径
shutil.make_archive(base_name=r'datafile',format='zip',root_dir=r'files')
```

- 2 解压文件

```python
# filename，要解压的压缩包文件
# extract_dir，解压的路径
# format，压缩文件格式
shutil.unpack_archive(filename=r'datafile.zip', extract_dir=r'xxxxxx/xo', format='zip')
```

### 10 路径相关

#### 1  转义

windows路径使用的是\，linux路径使用的是/。

特别的，在windows系统中如果有这样的一个路径 `D:\nxxx\txxx\x1`，程序会报错。因为在路径中存在特殊符 `\n`（换行符）和`\t`（制表符），Python解释器无法自动区分。

所以，在windows中编写路径时，一般有两种方式：

- 加转义符，例如：`"D:\\nxxx\\txxx\\x1"`
- 路径前加r，例如：`r"D:\\nxxx\\txxx\\x1"`

#### 2 程序当前路径

项目中如果使用了相对路径，那么一定要注意当前所在的位置。

例如：在`/Users/wupeiqi/PycharmProjects/CodeRepository/`路径下编写 `demo.py`文件

```python
with open("a1.txt", mode='w', encoding='utf-8') as f:
    f.write("你好呀")
```

用以下两种方式去运行：

- 方式1，文件会创建在 `/Users/wupeiqi/PycharmProjects/CodeRepository/` 目录下。

  ```python
  cd /Users/wupeiqi/PycharmProjects/CodeRepository/
  python demo.py
  ```

- 方式2，文件会创建在 `/Users/wupeiqi`目录下。

  ```
  cd /Users/wupeiqi
  python /Users/wupeiqi/PycharmProjects/CodeRepository/demo.py
  ```



```python
import os
base_dir = os.path.dirname(os.path.abspath(__file__)) # 获取绝对路径的上层路径
file_path = os.path.join(base_dir, 'files', 'info.txt') # 路径拼接
print(file_path)
if os.path.exists(file_path): # 判断路径是否存在
    file_object = open(file_path, mode='r', encoding='utf-8')
    data = file_object.read()
    file_object.close()

    print(data)
else:
    print('文件路径不存在')
```

#### 3 文件和路径相关

- 用到的模块

```python
import os
import shutil
```

##### 1. 获取当前脚本绝对路径

```python
abs_path = os.path.abspath(__file__)
```

##### 2. 获取当前文件的上级目录

```python
base_path = os.path.dirname(os.path.abspath(__file__))
```

##### 3. 路径拼接

```python
p1 = os.path.join(base_path, 'xx')
p2 = os.path.join(base_path, 'xx', 'oo', 'a1.png')
```

#####  4. 判断路径是否存在

```python
exists = os.path.exists(p1)
```

#####  5. 创建文件夹

```python
os.makedirs(路径)
```

```python
# 判断文件夹不存在在创建
path = os.path.join(base_path, 'xx', 'oo', 'uuuu')
if not os.path.exists(path):
    os.makedirs(path)
```

##### 6. 是否是文件夹

```python
file_path = os.path.join(base_path, 'xx', 'oo', 'uuuu.png')
is_dir = os.path.isdir(file_path)
print(is_dir) # False
```

##### 7. 删除文件或文件夹

```python
# 文件
os.remove("文件路径")
# 文件夹
path = os.path.join(base_path, 'xx')
shutil.rmtree(path)
```

##### 8. 拷贝文件夹

```python
# 第一个文件夹位置。第二个要拷贝的位置
shutil.copytree("/Users/wupeiqi/Desktop/图/csdn/","/Users/wupeiqi/PycharmProjects/CodeRepository/files")
```

##### 9.拷贝文件

```python
# 拷贝的文件夹
shutil.copy("/Users/wupeiqi/Desktop/图/csdn/WX20201123-112406@2x.png","/Users/wupeiqi/PycharmProjects/CodeRepository/")
# 拷贝覆盖
shutil.copy("/Users/wupeiqi/Desktop/图/csdn/WX20201123-112406@2x.png","/Users/wupeiqi/PycharmProjects/CodeRepository/x.png")
```

##### 10.文件或文件夹重命名

```python
shutil.move("/Users/wupeiqi/PycharmProjects/CodeRepository/x.png","/Users/wupeiqi/PycharmProjects/CodeRepository/xxxx.png")
shutil.move("/Users/wupeiqi/PycharmProjects/CodeRepository/files","/Users/wupeiqi/PycharmProjects/CodeRepository/images")
```

##### 11.查看目录下所有的文件

```python
data = os.listdir("/Users/wupeiqi/PycharmProjects/luffyCourse/day14/commons")
print(data)
```

##### 12.查看目录下所有的文件（含子孙文件）

```python
data = os.walk("/Users/wupeiqi/Documents/视频教程/路飞Python/mp4")
for path, folder_list, file_list in data:
    for file_name in file_list:
        file_abs_path = os.path.join(path, file_name)
        ext = file_abs_path.rsplit(".",1)[-1]
        if ext == "mp4":
            print(file_abs_path)
```

##### 13 .获取文件大小

```python
file_size = os.stat(file_path).st_size#获取文件大小
client.sendall(str(file_size).encode('utf-8'))#把大小转字符串在以字节模式发送

```























































# 八 面向对向

## 1 定义类

- 定义类，在类中定义方法，在方法中去实现具体的功能。

- 实例化类并返回一个对象，通过对象去调用并执行方法。

  创建类：class 类名（）

```python
class Message:#创建类
    
     def __init__(self, content): #初始化方法
        self.data = content

    def send_email(self, email, content):
        data = "给{}发邮件，内容是：{}".format(email,content)
        print(data)

msg_object = Message() # 实例化一个对象 msg_object，创建了一个一块区域。
msg_object.send_email("wupeiqi@live.com","注册成功")
```

注意：1.类名称首字母大写&驼峰式命名；2.py3之后默认类都继承object；3.在类种编写的函数称为方法；4.每个方法的第一个参数是self。

## 2 对象和self

在每个类中都可以定义个特殊的：`__init__ 初始化方法 `，在实例化类创建对象时自动执行，即：`对象=类()`

```python
class Message:

    def __init__(self, content):#content 实例化类时传进来的参数
        self.data = content

    def send_email(self, email):
        data = "给{}发邮件，内容是：{}".format(email, self.data)
        print(data)

    def send_wechat(self, vid):
        data = "给{}发微信，内容是：{}".format(vid, self.data)
        print(data)

# 对象 = 类名() # 自动执行类中的 __init__ 方法。

# 1. 根据类型创建一个对象，内存的一块 区域 。
# 2. 执行__init__方法，模块会将创建的那块区域的内存地址当self参数传递进去。    往区域中(data="注册成功")
a  = Message("注册成功")

a .send_email("wupeiqi@live.com") # 给wupeiqi@live.com发邮件，内容是：注册成功
a .send_wechat("武沛齐") # 给武沛齐发微信，内容是：注册成功
```



- 对象，让我们可以在它的内部先封装一部分数据，以后想要使用时，再去里面获取。
- self，类中的方法需要由这个类的对象来触发并执行（ 对象.方法名 ），且在执行时会自动将对象当做参数传递给self，以供方法中获取对象中已封装的值。

- 注意：除了self默认参数以外，方法中的参数的定义和执行与函数是相同。

- 面向对象的思想：将一些数据封装到对象中，在执行方法时，再去对象中获取。

- 函数式的思想：函数内部需要的数据均通过参数的形式传递。

- self，本质上就是一个参数。这个参数是Python内部会提供，其实本质上就是调用当前方法的那个对象。
- 对象，基于类实例化出来”一块内存“，默认里面没有数据；经过类的 `__init__`方法，可以在内存中初始化一些数据。



### 对象嵌套

在基于面向对象进行编程时，对象之间可以存在各种各样的关系，例如：组合、关联、依赖等（Java中的称呼），用大白话来说就是各种嵌套。

情景一：

```python
class Student(object):
    """ 学生类 """

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def message(self):
        data = "我是一名学生，我叫:{},我今年{}岁".format(self.name, self.age)
        print(data)

s1 = Student("武沛齐", 19)
s2 = Student("Alex", 19)
s3 = Student("日天", 19)



class Classes(object):
    """ 班级类 """

    def __init__(self, title):
        self.title = title
        self.student_list = []

    def add_student(self, stu_object):
        self.student_list.append(stu_object)

    def add_students(self, stu_object_list):
        for stu in stu_object_list:
            self.add_student(stu)

    def show_members(self):
        for item in self.student_list:
            # print(item)
            item.message()

c1 = Classes("三年二班")
c1.add_student(s1)
c1.add_students([s2, s3])

print(c1.title)
print(c1.student_list)
```



情景二：

```python
class Student(object):
    """ 学生类 """

    def __init__(self, name, age, class_object):
        self.name = name
        self.age = age
        self.class_object = class_object

    def message(self):
        data = "我是一名{}班的学生，我叫:{},我今年{}岁".format(self.class_object.title, self.name, self.age)
        print(data)


class Classes(object):
    """ 班级类 """

    def __init__(self, title):
        self.title = title


c1 = Classes("Python全栈")
c2 = Classes("Linux云计算")

user_object_list = [
    Student("武沛齐", 19, c1),
    Student("Alex", 19, c1),
    Student("日天", 19, c2)
]

for obj in user_object_list:
    print(obj.name,obj.age, obj.class_object.title)

```

![image-20210127215951115](python神功.assets/image-20210127215951115.png)











## 3 成员

#### 常用成员

在编写面向对象相关代码时，最常见成员有：

- 实例变量，属于对象，只能通过对象调用。
- 绑定方法，属于类，通过对象调用 或 通过类调用。

```python
class Person:

    def __init__(self, n1, n2):
        # 实例变量
        self.name = n1
        self.age = n2
	
    # 绑定方法
    def show(self):
        msg = "我叫{}，今年{}岁。".format(self.name, self.age)
        print(msg)
```

```python
p1 = Person("武沛齐",20)# 初始化，实例化了Person类的对象叫p1,并传入了参数变成实例变量
p1.show()# 执行绑定方法，p1对象内带有实例变量传给此方法
# 或
p1 = Person("武沛齐",20)
Person.show(p1)

```

#### 所有成员

##### 变量

- 实例变量，属于对象，每个对象中各自维护自己的数据。

- 类变量，属于类，可以被所有对象共享，一般用于给对象提供公共数据（类似于全局变量）。

  ![](python神功.assets/image-20210127111042911.png)

##### 方法

- 初始方法：`__init__ 初始化方法 `

- 绑定方法，默认有一个self参数，由对象进行调用（此时self就等于调用方法的这个对象）【对象&类均可调用】

- 类方法，默认有一个cls参数，用类或对象都可以调用（此时cls就等于调用方法的这个类）【对象&类均可调用】

- 静态方法，无默认参数，用类和对象都可以调用。【对象&类均可调用】

  ```python
  class Foo(object):
  
      def __init__(self, name,age):
          self.name = name
          self.age = age
  
      def f1(self):
          print("绑定方法", self.name)
  
      @classmethod
      def f2(cls):
          print("类方法", cls)
  
      @staticmethod
      def f3():
          print("静态方法")
          
  # 绑定方法（对象）
  obj = Foo("武沛齐",20)
  obj.f1() # Foo.f1(obj)
  
  
  # 类方法
  Foo.f2()  # cls就是当前调用这个方法的类。（类）
  obj.f2()  # cls就是当前调用这个方法的对象的类。
  
  
  # 静态方法
  Foo.f3()  # 类执行执行方法（类）
  obj.f3()  # 对象执行执行方法
  ```

  

##### 属性

属性其实是由绑定方法 + 特殊装饰器 **@property**  组合创造出来的，让我们以后在调用方法时可以不加括号

```python
class Foo(object):

    def __init__(self, name):
        self.name = name

    def f1(self):
        return 123

    @property  #添加装饰器 
    def f2(self):
        return 123


obj = Foo("武沛齐")

v1 = obj.f1()
print(v1)

v2 = obj.f2#执行时不用加括号
print(v2)
```

关于属性的编写有两种方式：

- 方式一，基于装饰器，不同的装饰器会有不同的执行调用方法

  ```python
  class C(object):
      
      @property
      def x(self):
          pass
      
      @x.setter
      def x(self, value):
          pass
      
      @x.deleter
      def x(self):
  		pass
          
  obj = C()
  
  obj.x
  obj.x = 123
  del obj.x
  ```

- 方式二，基于定义变量

  ```python
  class C(object):
      
      def getx(self): 
  		pass
      
      def setx(self, value): 
  		pass
          
      def delx(self): 
  		pass
          
      x = property(getx, setx, delx, "I'm the 'x' property.")
      
  obj = C()
  
  obj.x
  obj.x = 123
  del obj.x
  ```

  由于属性和实例变量的调用方式相同，所以在编写时需要注意：属性名称 不要 与实例变量 重名。

  如果真的想要在名称上创建一些关系，可以让实例变量加上一个下划线。

  ```python
  class Foo(object):
  
      def __init__(self, name, age):
          self._name = name
          self.age = age
  
      @property
      def name(self):
          return "{}-{}".format(self._name, self.age)
  
  
  obj = Foo("武沛齐", 123)
  print(obj._name)
  print(obj.name)
  ```




#### 特殊成员

在Python的类中存在一些特殊的方法，这些方法都是 `__方法__` 格式，这种方法在内部均有特殊的含义，接下来我们来讲一些常见的特殊成员：

- `__init__`，初始化方法,在空对象中创建数据

  ```python
  class Foo(object):
      def __init__(self, name):
          self.name = name
  
  
  obj = Foo("武沛齐")
  ```

- `__new__`，构造方法

  ```python
  class Foo(object):
      def __init__(self, name):
          print("第二步：初始化对象，在空对象中创建数据")
          self.name = name
  
      def __new__(cls, *args, **kwargs):
          print("第一步：先创建空对象并返回")
          return object.__new__(cls)
  
  
  obj = Foo("武沛齐")
  ```

- `__call__`对象加括号执行就会执行call方法

  ```python
  class Foo(object):
      def __call__(self, *args, **kwargs):
          print("执行call方法")
  
  
  obj = Foo()
  obj()
  ```

- `__str__ `      str（对象）就会执行这个方法

  ```python
  class Foo(object):
  
      def __str__(self):
          return "哈哈哈哈"
  
  
  obj = Foo()
  data = str(obj)
  print(data)
  ```

- `__dict__`       执行  对象.此方法就会换实例变量变成一个字典

  ```python
  class Foo(object):
      def __init__(self, name, age):
          self.name = name
          self.age = age
  
  
  obj = Foo("武沛齐",19)
  print(obj.__dict__)
  ```

- `__getitem__`、`__setitem__`、`__delitem__`     对应的字典执行方式就会执行到对应的方法

  ```python
  class Foo(object):
  
      def __getitem__(self, item):
          pass
  
      def __setitem__(self, key, value):
          pass
  
      def __delitem__(self, key):
          pass
  
  
  obj = Foo("武沛齐", 19)
  
  obj["x1"]          #__getitem__
  obj['x2'] = 123   #__setitem__
  del obj['x3']    #__delitem__
  ```

- `__enter__`、`__exit__`       上下文管理方法

  ```python
  class Foo(object):
  
      def __enter__(self):
          print("进入了")
          return 666
  
      def __exit__(self, exc_type, exc_val, exc_tb):
          print("出去了")
  
  
  obj = Foo()
  with obj as data:
      print(data)
  ```

  ```python
  超前知识：数据连接，每次对远程的数据进行操作时候都必须经历。
  1.连接 = 连接数据库
  2.操作数据库
  3.关闭连接
  ```

  ```python
  class SqlHelper(object):
  
      def __enter__(self):
          self.连接 = 连接数据库
          return 连接
  
      def __exit__(self, exc_type, exc_val, exc_tb):
          self.连接.关闭
  
          
          
  with SqlHelper() as 连接:
      连接.操作..
      
      
  with SqlHelper() as 连接:
      连接.操作...
  ```

  ```python
  # 面试题（补充代码，实现如下功能）
  
  class Context:
       def __enter__(self):#执行前
              reture self
          
       def __exit__(self, exc_type, exc_val, exc_tb):#执行后
          pass
      
       def do_something(self):
          print('内部执行')
  
  
  with Context() as ctx:
      print('内部执行')
      ctx.do_something()
  
  ```

  上下文管理的语法。

- `__add__` 等。

  ```python
  class Foo(object):
      def __init__(self, name):
          self.name = name
  
      def __add__(self, other):
          return "{}-{}".format(self.name, other.name)
  
  
  v1 = Foo("alex")
  v2 = Foo("sb")
  
  # 对象+值，内部会去执行 对象.__add__方法，并将+后面的值当做参数传递过去。
  v3 = v1 + v2
  print(v3)
  ```

- `__iter__`

  - 迭代器

    ```python
    # 迭代器类型的定义：
        1.当类中定义了 __iter__ 和 __next__ 两个方法。
        2.__iter__ 方法需要返回对象本身，即：self
        3. __next__ 方法，返回下一个数据，如果没有数据了，则需要抛出一个StopIteration的异常。
    	官方文档：https://docs.python.org/3/library/stdtypes.html#iterator-types
            
    # 创建 迭代器类型 ：
    	class IT(object):
            def __init__(self):
                self.counter = 0
    
            def __iter__(self):
                return self
    
            def __next__(self):
                self.counter += 1
                if self.counter == 3:
                    raise StopIteration()
                return self.counter
    
    # 根据类实例化创建一个迭代器对象：
        obj1 = IT()
        
        # v1 = obj1.__next__()
        # v2 = obj1.__next__()
        # v3 = obj1.__next__() # 抛出异常
        
        v1 = next(obj1) # obj1.__next__()
        print(v1)
    
        v2 = next(obj1)
        print(v2)
    
        v3 = next(obj1)
        print(v3)
    
    
        obj2 = IT()
        for item in obj2:  # 首先会执行迭代器对象的__iter__方法并获取返回值，一直去反复的执行 next(对象) 
            print(item)
            
    迭代器对象支持通过next取值，如果取值结束则自动抛出StopIteration。
    for循环内部在循环时，先执行__iter__方法，获取一个迭代器对象，然后不断执行的next取值（有异常StopIteration则终止循环）。
    ```

  - 生成器

    ```python
    # 创建生成器函数
        def func():
            yield 1
            yield 2
        
    # 创建生成器对象（内部是根据生成器类generator创建的对象），生成器类的内部也声明了：__iter__、__next__ 方法。
        obj1 = func()
        
        v1 = next(obj1)
        print(v1)
    
        v2 = next(obj1)
        print(v2)
    
        v3 = next(obj1)
        print(v3)
    
    
        obj2 = func()
        for item in obj2:
            print(item)
    
    如果按照迭代器的规定来看，其实生成器类也是一种特殊的迭代器类（生成器也是一个中特殊的迭代器）。
    ```

  - 可迭代对象

    ```python
    # 如果一个类中有__iter__方法且返回一个迭代器对象 ；则我们称以这个类创建的对象为可迭代对象。
    
    class Foo(object):
        
        def __iter__(self):
            return 迭代器对象(生成器对象)
        
    obj = Foo() # obj是 可迭代对象。
    
    # 可迭代对象是可以使用for来进行循环，在循环的内部其实是先执行 __iter__ 方法，获取其迭代器对象，然后再在内部执行这个迭代器对象的next功能，逐步取值。
    for item in obj:
        pass
    ```

    ```python
    class IT(object):
        def __init__(self):
            self.counter = 0
    
        def __iter__(self):
            return self
    
        def __next__(self):
            self.counter += 1
            if self.counter == 3:
                raise StopIteration()
            return self.counter
    
    
    class Foo(object):
        def __iter__(self):
            return IT()
    
    
    obj = Foo() # 可迭代对象
    
    
    for item in obj: # 循环可迭代对象时，内部先执行obj.__iter__并获取迭代器对象；不断地执行迭代器对象的next方法。
        print(item)
    ```

    ```python
    # 基于可迭代对象&迭代器实现：自定义range
    class IterRange(object):
        def __init__(self, num):
            self.num = num
            self.counter = -1
    
        def __iter__(self):
            return self
    
        def __next__(self):
            self.counter += 1
            if self.counter == self.num:
                raise StopIteration()
            return self.counter
    
    
    class Xrange(object):
        def __init__(self, max_num):
            self.max_num = max_num
    
        def __iter__(self):
            return IterRange(self.max_num)
    
    
    obj = Xrange(100)
    
    for item in obj:
        print(item)
    ```

    

    ```python
    class Foo(object):
        def __iter__(self):
            yield 1
            yield 2
    
    
    obj = Foo()
    for item in obj:
        print(item)
    ```

    ```python
    # 基于可迭代对象&生成器 实现：自定义range
    
    class Xrange(object):
        def __init__(self, max_num):
            self.max_num = max_num
    
        def __iter__(self):
            counter = 0
            while counter < self.max_num:
                yield counter
                counter += 1
    
    
    obj = Xrange(100)
    for item in obj:
        print(item)
    ```

    常见的数据类型：

    ```python
    v1 = list([11,22,33,44])
    
    v1是一个可迭代对象，因为在列表中声明了一个 __iter__ 方法并且返回一个迭代器对象。
    ```

    ```python
    from collections.abc import Iterator, Iterable
    
    v1 = [11, 22, 33]
    print( isinstance(v1, Iterator) )  # false，判断是否是迭代器；判断依据是__iter__ 和 __next__。
    v2 = v1.__iter__()
    print( isinstance(v2, Iterator) )  # True
    
    
    
    v1 = [11, 22, 33]
    print( isinstance(v1, Iterable) )  # True，判断依据是是否有 __iter__且返回迭代器对象。
    
    v2 = v1.__iter__()
    print( isinstance(v2, Iterable) )  # True，判断依据是是否有 __iter__且返回迭代器对象。
    ```

    

    





#### 成员修饰符 公有、私有

Python中成员的修饰符就是指的是：公有、私有。

- 公有，在任何地方都可以调用这个成员。
- 私有，只有在类的内部才可以调用改成员（成员是以两个下划线开头，则表示该成员为私有）。

```python
class Foo(object):

    def get_age(self):
        print("公有的get_age")

    def __get_data(self):
        print("私有的__get_data方法")

    def proxy(self):
        print("公有的proxy")
        self.__get_data()

obj = Foo()
obj.get_age()

obj.proxy()
```

特别提醒：父类中的私有成员，子类无法继承。

```python
class Base(object):

    def __data(self):
        print("base.__data")

    def num(self):
        print("base.num")


class Foo(Base):

    def func(self):
        self.num()
        self.__data() # # 不允许执行父类中的私有方法


obj = Foo()
obj.func()

```

写在最后，按理说私有成员是无法被外部调用，但如果用一些特殊的语法也可以（Flask源码中有这种写法，大家写代码不推荐这样写）。

```python
class Foo(object):

    def __init__(self):
        self.__num = 123
        self.age = 19

    def __msg(self):
        print(1234)


obj = Foo()
print(obj.age)#加一个下划线和类名，在加上私有方法就能在外部调用
print(obj._Foo__num) # 
obj._Foo__msg()
```



成员是否可以作为独立的功能暴露给外部，让外部调用并使用。

- 可以，公有。
- 不可以，内部其他放的一个辅助，私有。













## 4 三大特性

面向对象编程在很多语言中都存在，这种编程方式有三大特性：封装、继承、多态。

### 封装

封装主要体现在两个方面：

- 将同一类工具方法封装到了一个类中
- 将数据封装到了对象中，在实例化一个对象时，可以通过`__init__`初始化方法在对象中封装一些数据，便于以后使用。

###  继承

在面向对象中也有这样的理念，即：子类可以继承父类中的方法和类变量（不是拷贝一份，父类的还是属于父类，子类可以继承而已）

- 有2种称呼   **父类子类**  或  **基类派生类** 选择一个称呼就要统一
- 优先在自己的类中找，自己没有才去父类。
- 执行对象.方法时，优先去当前对象所关联的类中找，没有的话才去她的父类中查找。
- Python支持多继承：先继承左边、再继承右边的。
- self到底是谁？去self对应的那个类中去获取成员，没有就按照继承关系向上查找 。

####  mro和c3算法

- **mro()**

如果类中存在继承关系，在可以通过`mro()`获取当前类的继承关系（找成员的顺序）。

```python
class C(object):
    pass
class B(object):
    pass
class A(B, C):
    pass
print( A.mro() )   # [<class '__main__.A'>, <class '__main__.B'>, <class '__main__.C'>, <class 'object'>]
print( A.__mro__ ) # (<class '__main__.A'>, <class '__main__.B'>, <class '__main__.C'>, <class 'object'>)
```

- **c3算法**

一句话搞定继承关系

如果用正经的C3算法规则去分析一个类继承关系有点繁琐，尤其是遇到一个复杂的类也要分析很久。

<span style="color:red">**从左到右，深度优先，大小钻石，留住顶端**</span>，基于这句话可以更快的找到继承关系。

![image-20210129142756667](python神功.assets/image-20210129142756667.png)

```
简写为：A -> B -> D -> G -> H -> K -> C -> E -> F -> M -> N -> P -> object
```















### 多态

多态，按字面翻译其实就是多种形态。

- Python中多态，由于Python对数据类型没有任何限制，所以他天生支持多态。
- 在程序设计中，鸭子类型（duck typing）是动态类型的一种风格。在鸭子类型中，关注点在于对象的行为，能作什么；而不是关注对象所属的类型，例如：一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟可以被称为鸭子。

### 小结：

- 封装，将方法封装到类中 或 将数据封装到对象中，便于以后使用。

- 继承，将类中的公共的方法提取到基类中去实现。

- 多态，Python默认支持多态（这种方式称之为鸭子类型），最简单的基础下面的这段代码即可。

  ```python
  def func(arg):
      v1 = arg.copy() # 浅拷贝
      print(v1)
      
  func("武沛齐")
  func([11,22,33,44])
  ```


- 面向对象的应用场景

1. 数据封装。
2. 封装数据 + 方法再对数据进行加工处理。
3. 创建同一类的数据且同类数据可以具有相同的功能（方法）。
4. 补充：在Python3中编写类时，默认都会继-object（即使不写也会自动继承）。

```python
class Foo:
    pass

class Foo(object):
    pass
```

这一点在Python2是不同的：

- 继承object，新式类
- 不继承object，经典类



## 5 面向对象相关内置函数

- classmethod：类方法的装饰器，类方法，默认有一个cls参数

  ```python
   @classmethod
      def f2(cls):
          print("类方法", cls)
  ```

  

- staticmethod：静态方法的装饰器,无默认参数

  ```python
  @staticmethod
      def f3():
          print("静态方法")
  ```

  

- property :属性，装饰在绑定方法上，调用此方法时不用加（）号

- callable，是否可在后面加括号执行。

  - 函数

    ```python
    def func():
        pass
    
    print( callable(func) ) # True
    ```

  - 类

    ```python
    class Foo(object):
        pass
    
    print( callable(Foo) ) # True
    ```

  - 类中具有`__call__`方法的对象

    ```python
    class Foo(object):
    	pass
    
    obj = Foo()
    print( callable(obj) ) # False
    ```

    ```python
    class Foo(object):
    
        def __call__(self, *args, **kwargs):
            pass
        
    obj = Foo()
    print( callable(obj) ) # True
    ```

  所以当你以后在见到下面的情况时，首先就要想到handler可以是：函数、类、具有call方法的对象 这三种，到底具体是什么，需要根据代码的调用关系才能分析出来。

  ```python
  def do_something(handler):
      handler()
  ```

- super，按照mro继承关系向上找成员。

  ```python
  class Top(object):
      def message(self, num):
          print("Top.message", num)
          
  class Base(Top):
      pass
  
  class Foo(Base):
  
      def message(self, num):
          print("Foo.message", num)
          super().message(num + 100)
  
  
  obj = Foo()
  obj.message(1)
  
  >>> Foo.message 1
  >>> Top.message 101
  ```

  ```python
  class Base(object):
  
      def message(self, num):
          print("Base.message", num)
          super().message(1000)
  
  
  class Bar(object):
  
      def message(self, num):
          print("Bar.message", num)
  
  
  class Foo(Base, Bar):
      pass
  
  
  obj = Foo()
  obj.message(1)
  
  >>> Base.message 1
  >>> Bar.message 1000
  ```

  

  **应用场景**

  假设有一个类，他原来已实现了某些功能，但我们想在他的基础上再扩展点功能，重新写一遍？比较麻烦，此时可以用super。

  ```python
  info = dict() # {}
  info['name'] = "武沛齐"
  info["age"] = 18
  
  value = info.get("age")
  
  print(value)
  ```

  ```python
  class MyDict(dict):
  
      def get(self, k):
          print("自定义功能")
          return super().get(k)
  
  
  info = MyDict()
  info['name'] = "武沛齐" # __setitem__
  info["age"] = 18       # __setitem__
  print(info)
  
  value = info.get("age")
  
  print(value)
  ```

  ![image-20210131150707551](../../../碧锋/python/模块3/day19 面向对象高级和应用/笔记/assets/image-20210131150707551.png)

  

- type，获取一个对象的类型。

  ```python
  v1 = "武沛齐"
  result = type(v1)
  print(result) # <class 'str'>
  ```

  ```python
  v2 = "武沛齐"
  print( type(v2) == str )  # True
  
  v3 = [11, 22, 33] # list(...)
  print( type(v3) == list )  # True
  ```

  ```python
  class Foo(object):
      pass
  
  v4 = Foo()
  
  print( type(v4) == Foo )  # True
  ```

- isinstance，判断对象是否是某个类的实例。

  ```python
  class Top(object):
      pass
  
  
  class Base(Top):
      pass
  
  
  class Foo(Base):
      pass
  
  
  v1 = Foo()
  
  print( isinstance(v1, Foo) )   # True，对象v1是Foo类的实例
  print( isinstance(v1, Base) )  # True，对象v1的Base子类的实例。
  print( isinstance(v1, Top) )   # True，对象v1的Top子类的实例。
  ```

  ```python
  class Animal(object):
      def run(self):
          pass
  
  class Dog(Animal):
      pass
  
  class Cat(Animal):
      pass
  
  data_list = [
      "alex",
      Dog(),
      Cat(),
  	"root"
  ]
  
  for item in data_list:
      if type(item) == Cat:
          item.run()
      elif type(item) == Dog:
          item.run()
      else:
          pass
      
  for item in data_list:
      if isinstance(item, Animal):
          item.run()
      else:
          pass
  ```

  

- issubclass，判断类是否是某个类的子孙类。

  ```python
  class Top(object):
      pass
  
  
  class Base(Top):
      pass
  
  
  class Foo(Base):
      pass
  
  
  print(issubclass(Foo, Base))  # True
  print(issubclass(Foo, Top))   # True
  ```

  



## 6 异常处理 

- **异常处理基本格式**

```python
try:
    # 逻辑代码
except Exception as e:
    # try中的代码如果有异常，则此代码块中的代码会执行。
```

```python
try:
    # 逻辑代码
except Exception as e:
    # try中的代码如果有异常，则此代码块中的代码会执行。
finally:
    # try中的代码无论是否报错，finally中的代码都会执行，一般用于释放资源。

print("end")

"""
try:
    file_object = open("xxx.log")
    # ....
except Exception as e:
    # 异常处理
finally:
    file_object.close()  # try中没异常，最后执行finally关闭文件；try有异常，执行except中的逻辑，最后再执行finally关闭文件。
"""    
```

- **异常细分**

之前只是简单的捕获了异常，出现异常则统一提示信息即可。如果想要对异常进行更加细致的异常处理，则可以这样来做：

```python
import requests
from requests import exceptions

while True:
    url = input("请输入要下载网页地址：")
    try:
        res = requests.get(url=url)
        print(res)    
    except exceptions.MissingSchema as e:
        print("URL架构不存在")
    except exceptions.InvalidSchema as e:
        print("URL架构错误")
    except exceptions.InvalidURL as e:
        print("URL地址格式错误")
    except exceptions.ConnectionError as e:
        print("网络连接错误")
    except Exception as e:
        print("代码出现错误", e)
        
# 提示：如果想要写的简单一点，其实只写一个Exception捕获错误就可以了。
```



如果想要对错误进行细分的处理，例如：发生Key错误和发生Value错误分开处理。

基本格式：

```python
try:
    # 逻辑代码
    pass

except KeyError as e:
    # 小兵，只捕获try代码中发现了键不存在的异常，例如：去字典 info_dict["n1"] 中获取数据时，键不存在。
    print("KeyError")

except ValueError as e:
    # 小兵，只捕获try代码中发现了值相关错误，例如：把字符串转整型 int("无诶器")
    print("ValueError")

except Exception as e:
    # 王者，处理上面except捕获不了的错误（可以捕获所有的错误）。
    print("Exception")
```

Python中内置了很多细分的错误，供你选择。

```python
常见异常：
"""
AttributeError 试图访问一个对象没有的树形，比如foo.x，但是foo没有属性x
IOError 输入/输出异常；基本上是无法打开文件
ImportError 无法引入模块或包；基本上是路径问题或名称错误
IndentationError 语法错误（的子类） ；代码没有正确对齐
IndexError 下标索引超出序列边界，比如当x只有三个元素，却试图访问n x[5]
KeyError 试图访问字典里不存在的键 inf['xx']
KeyboardInterrupt Ctrl+C被按下
NameError 使用一个还未被赋予对象的变量
SyntaxError Python代码非法，代码不能编译(个人认为这是语法错误，写错了）
TypeError 传入对象类型与要求的不符合
UnboundLocalError 试图访问一个还未被设置的局部变量，基本上是由于另有一个同名的全局变量，
导致你以为正在访问它
ValueError 传入一个调用者不期望的值，即使值的类型是正确的
"""
更多异常：
"""
ArithmeticError
AssertionError
AttributeError
BaseException
BufferError
BytesWarning
DeprecationWarning
EnvironmentError
EOFError
Exception
FloatingPointError
FutureWarning
GeneratorExit
ImportError
ImportWarning
IndentationError
IndexError
IOError
KeyboardInterrupt
KeyError
LookupError
MemoryError
NameError
NotImplementedError
OSError
OverflowError
PendingDeprecationWarning
ReferenceError
RuntimeError
RuntimeWarning
StandardError
StopIteration
SyntaxError
SyntaxWarning
SystemError
SystemExit
TabError
TypeError
UnboundLocalError
UnicodeDecodeError
UnicodeEncodeError
UnicodeError
UnicodeTranslateError
UnicodeWarning
UserWarning
ValueError
Warning
ZeroDivisionError
"""
```



- #### 自定义异常&抛出异常

如果想要触发，则需要使用：`raise MyException()`类实现。

你可以用`raise`语句来引发一个异常,返回类名。异常/错误对象必须有一个名字，且它们应是Error或`Exception``类的子类`

```python
class MyException(Exception):
    pass


try:
    # 。。。
    raise MyException()
    # 。。。
except MyException as e:
    print("MyException异常被触发了", e)
except Exception as e:
    print("Exception", e)
```

```python
class MyException(Exception):
    def __init__(self, msg, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.msg = msg


try:
    raise MyException("xxx失败了")
except MyException as e:
    print("MyException异常被触发了", e.msg)
except Exception as e:
    print("Exception", e)
```

```python
class MyException(Exception):
    title = "请求错误"


try:
    raise MyException()
except MyException as e:
    print("MyException异常被触发了", e.title)
except Exception as e:
    print("Exception", e)
```

```python
class ShortInputException(Exception):
    '''自定义的异常类'''
    def __init__(self, length, atleast):
        #super().__init__()
        self.length = length
        self.atleast = atleast

def main():
    try:
        s = input('请输入 --> ')
        if len(s) < 3:
            # raise引发一个你定义的异常
            raise ShortInputException(len(s), 3)
    except ShortInputException as result:#x这个变量被绑定到了错误的实例
        print('ShortInputException: 输入的长度是 %d,长度至少应是 %d'% (result.length, result.atleast))
    else:
        print('没有异常发生.')

main()
```



- **特殊的finally**

```python
try:
    # 逻辑代码
except Exception as e:
    # try中的代码如果有异常，则此代码块中的代码会执行。
finally:
    # try中的代码无论是否报错，finally中的代码都会执行，一般用于释放资源。

print("end")
```

当在函数或方法中定义异常处理的代码时，要特别注意finally和return。

```python
def func():
    try:
        return 123
    except Exception as e:
        pass
    finally:
        print(666)
        
func()
```

在try或except中即使定义了return，也会执行最后的finally块中的代码。

## 7 反射

反射，提供了一种更加灵活的方式让你可以实现去 对象 中操作成员（以字符串的形式去 `对象` 中进行成员的操作）。

Python中提供了4个内置函数来支持反射：

- **getattr，**去对象中获取成员

  ```
  v1 = getattr(对象,"成员名称")
  v2 = getattr(对象,"成员名称", 不存在时的默认值)
  ```

- **setattr**，去对象中设置成员

  ```
  setattr(对象,"成员名称",值)
  ```

- **hasattr**，对象中是否包含成员

  ```
  v1 = hasattr(对象,"成员名称") # True/False
  ```

- **delattr**，删除对象中的成员

  ```
  delattr(对象,"成员名称")
  ```

以后如果再遇到 对象.成员 这种编写方式时，均可以基于反射来实现。



```python
class Person(object):
    
    def __init__(self,name,wx):
        self.name = name
        self.wx = wx
	
    def show(self):
        message = "姓名{}，微信：{}".format(self.name,self.wx)
        
        
user_object = Person("武沛齐","wupeiqi666")


# 对象.成员 的格式去获取数据
user_object.name
user_object.wx
user_object.show()

# 对象.成员 的格式无设置数据
user_object.name = "吴培期"
```

```python
user = Person("武沛齐","wupeiqi666")

# getattr 获取成员
getattr(user,"name") # user.name
getattr(user,"wx")   # user.wx


method = getattr(user,"show") # user.show
method()
# 或
getattr(user,"show")()

# setattr 设置成员
setattr(user, "name", "吴培期") # user.name = "吴培期"
```

由于反射支持以字符串的形式去对象中操作成员【等价于 对象.成员 】，所以，基于反射也可以对类、模块中的成员进行操作。

简单粗暴：只要看到 xx.oo 都可以用反射实现。

```python
class Person(object):
    title = "武沛齐"

v1 = Person.title
print(v1)
v2 = getattr(Person,"title")
print(v2)
```

```python
import re

v1 = re.match("\w+","dfjksdufjksd")
print(v1)

func = getattr(re,"match")
v2 = func("\w+","dfjksdufjksd")
print(v2)
```

#### import_module + 反射

在Python中如果想要导入一个模块，可以通过import语法导入；企业也可以通过字符串的形式导入

```python
# 导入模块
import random

v1 = random.randint(1,100)
```

```python
# 导入模块
from importlib import import_module

m = import_module("random")

v1 = m.randint(1,100)
```

示例二：

```python
# 导入模块exceptions
from requests import exceptions as m
```

```python
# 导入模块exceptions
from importlib import import_module
m = import_module("requests.exceptions")
```

示例三：

```python
# 导入模块exceptions，获取exceptions中的InvalidURL类。
from requests.exceptions import InvalidURL
```

```python
# 错误方式
from importlib import import_module
m = import_module("requests.exceptions.InvalidURL") # 报错，import_module只能导入到模块级别。
```

```python
# 导入模块
from importlib import import_module
m = import_module("requests.exceptions")
# 去模块中获取类
cls = m.InvalidURL
```



在很多项目的源码中都会有 `import_module` 和 `getattr` 配合实现根据字符串的形式导入模块并获取成员，例如：

```python
from importlib import import_module

path = "openpyxl.utils.exceptions.InvalidFileException"

module_path,class_name = path.rsplit(".",maxsplit=1) # "openpyxl.utils.exceptions"   "InvalidFileException"

module_object = import_module(module_path)

cls = getattr(module_object,class_name)

print(cls)
```



我们在开发中也可以基于这个来进行开发，提高代码的可扩展性，例如：请在项目中实现一个发送 短信、微信 的功能。



## 元类

### 一、元类介绍

一切源自于一句话：python中一切皆为对象。让我们先定义一个类，然后逐步分析

```python
class StanfordTeacher(object):
    school='Stanford'

    def __init__(self,name,age):
        self.name=name
        self.age=age

    def say(self):
        print('%s says welcome to the Stanford to learn Python' %self.name)

```

所有的对象都是实例化或者说调用类而得到的（调用类的过程称为类的实例化），比如对象t1是调用类StanfordTeacher得到的

```py
t1=StanfordTeacher('lili',18)
print(type(t1)) #查看对象t1的类是<class '__main__.StanfordTeacher'>
```

**如果一切皆为对象，那么类StanfordTeacher本质也是一个对象，既然所有的对象都是调用类得到的**

**那么StanfordTeacher必然也是调用了一个类得到的，这个类称为元类**

```python
print(type(StanfordTeacher))
# 结果为<class 'type'>，证明是调用了type这个元类而产生的StanfordTeacher，即默认的元类为type

```

### 二、class关键字创建类的流程分析

用class关键字定义的类本身也是一个对象，负责产生该对象的类称之为元类（元类可以简称为类的类），内置的元类为`typeclass`关键字在帮我们创建类时，必然帮我们调用了元类`StanfordTeacher` = type(参数 1，参数2，参数3)，那调用type时传入的参数是什么呢？必然是类的关键组成部分，一个类有三大组成部分：

```
参数1、类名 class_name=‘StanfordTeacher’

参数2、基类 class_bases=(object,)

参数3、类的名称空间 class_dic，类的名称空间是执行类体代码而得到的
```

调用type时会依次传入以上三个参数—type( ‘StanfordTeacher’，（object,），{…} )

综上，class关键字帮我们创建一个类应该细分为以下四个过程：

1、拿到类名 'StanfordTeache

2、拿到他的基类们；

3、执行类体代码，拿到类的名称空间；

4、调用元类返回对象(返回的对象就是我们需要的“类”) ：`StanfordTeache = type( class_name, class_bases, class_dict )`

### 三、自定义元类

一个类没有声明自己的元类，默认他的元类就是type，除了使用内置元类type，我们也可以通过继承type来自定义元类，这样我们用 class 关键字生成的元类使用的就是我们自定义的元类

```python
class 类名( 继承的类名, … , metaclass = 自定义的元类名(默认为 type) ) :
```

**由 class 关键字创建一个类的四个步骤，只有最后一步调用元类生成类是无法修改的；比如：传入的类名必须首字母大写，不大写就报错, 为了实现这样的需求，元类显然是不能满足的**

**需求：**
传入的类名必须首字母大写，不大写就报错；类中必须有文档注释，并且文档注释不能为空

**步骤分析：**
1、需求分析-----People类，满足类名首字母必须大写；

2、首先需要自定义元类 Mymeta, 这样 class 类名(metaclass = Mymeta)就会对 类名首字母判断

3、使用 class 关键字创建类，相当于 类名 = Mymeta ( ‘类名’ , (需要继承的基类们，) , { 类体代码执行后的名称空间 } )

4、调用 Mymeta 类—发生"三件事":

 生成一个空对象，调用_ _ init _ _ 方法初始化对象，这个对象当做返回值

5、由于 Mymeta 类传入了三个参数，所以需要在 _ _ init _ _ 方法，要传入这三个参数以及空对象

6、在 _ _ init _ _ 方法中 对传入的参数进行 需求的自定义

```python
""" 自定义元类 """
class Mymeta(type): #只有继承了type类才能称之为一个元类，否则就是一个普通的自定义类
    def __init__(self,class_name,class_bases,class_dic):
        # self.class_name = class_name
        # self.class_bases = class_bases
        # self.class_dic = class_dic
        super(Mymeta, self).__init__(class_name, class_bases, class_dic)  # 重用父类的功能

        
        if not class_name.istitle():
            raise TypeError('类名%s请修改为首字母大写' %class_name)

        if '__doc__' not in class_dic or len(class_dic['__doc__'].strip(' \n')) == 0:
            raise TypeError('类中必须有文档注释，并且文档注释不能为空')

```



### 四、 _ _ new _ _ 方法

**调用一个类会发生"三件事"，其中第一件就是–产生一个空对象，那么这个空对象是怎么产生的呢？**

在调用类的时候，会首先自动触发 _ _ new _ _方法，执行里面的代码，在触发 init 方法





### 总结：类的产生与调用

1、对象 ( ) -----> 调用 类. _ _ call _ _

2、类 ( ) -----> 调用自定义元类. _ _ call _ _

3、自定义元类 ( ) -----> 调用type元类. _ _ call _ _

#### 类的产生：

People = Mymeta （ 参数 1，2，3）—>自定义元类加括号调用 Mymeta ( ) -----> 调用type元类. _ _ call _ _方法

type元类. _ _ call _ _方法做了三件事：

1、type元类. _ _ call _ _方法 调用自定义元类 Mymeta 内的 new 方法，造出一个空对象；

2、type元类. _ _ call _ _方法 调用自定义元类 Mymeta 内的 init 方法，初始化这个对象；

3、type元类. _ _ call _ _方法 会返回这个初始化好的对象；

#### 类的调用：

obj = People（参数…）—> People 类加括号调用 -----> 调用自定义元类 Mymeta . _ _ call _ _方法

自定义元类 Mymeta . _ _ call _ _方法做了三件事：

1、 Mymeta . _ _ call _ _方法 调用自定义元类 People 类内的 new 方法，造出一个空对象；

2、 Mymeta . _ _ call _ _方法 调用自定义元类People 类内的 init 方法，初始化这个对象；

3、 Mymeta . _ _ call _ _方法 会返回这个初始化好的对象；

### **生成一个对象的完整代码**

```python
class Mymeta(type):

    def __new__(cls, *args, **kwargs):
        print('type 调用了 Mymeta 的 new 方法--生成一个空对象，即 People 类')
        "这里调用的是 type 的 new 方法,传入参数需要注意全部传会 type 元类"
        return super().__new__(cls, *args, **kwargs)


    def __init__(self, class_name, class_bases, class_dic):
        print('初始化这个对象--- People 类，给 People 类添加额外的功能')
        super(Mymeta, self).__init__(class_name, class_bases, class_dic)  # 重用父类的功能
        # 自定义的类的功能
        if not class_name.istitle():
            raise TypeError('类名%s请修改为首字母大写' % class_name)

        if '__doc__' not in class_dic or len(class_dic['__doc__'].strip(' \n')) == 0:
            raise TypeError('类中必须有文档注释，并且文档注释不能为空')


    # 传入 Mymeta的参数：People, 以及传入People的参数
    def __call__(self, *args, **kwargs):
        """
        self---<class '__main__.People'>
        :param args: (1,)
        :param kwargs: {'y': 2}
        :return: 返回最终初始化好的代码
        """
        print('调用了 Mymeta 的 call 方法')
        # 调用 People 类里的 __new__方法，生成空对象
        People_obj = self.__new__(self, *args, **kwargs)
        # 调用 People 类里的 __init__方法，初始化空对象,注意：第一个传入的参数是生成好的空对象
        self.__init__(People_obj, *args, **kwargs)
        # 给 People 类生成的对象 obj 添加额外的功能
        print("给 People 类生成的对象 obj 添加额外的功能")
        People_obj.__dict__["新增一个属性"] = None
        # 返回初始化好的对象
        return People_obj


class People(metaclass=Mymeta):
    """People 类的注释"""

    # 产生 People 类真正的对象
    def __new__(cls, *args, **kwargs):
        # 在这里就可以定制功能
        print('生成 People 类的空对象')
        print('传入的位置参数', args)
        print('传入的位置参数', kwargs)
        # 调用所继承的父类的__new__方法，这里就是 object 类,一定要传入 cls(当前这个类)
        "这里要区别于自定义元类的 new 方法，自定义元类调用的是 type 的 new 方法,传入参数是不一样的"
        return super().__new__(cls)


    def __init__(self, x, y=None):
        print("初始化 People 类的对象")
        self.x = x
        self.y = y
        print("初始化 People 类的对象结束")


# 调用People 类生成对象---> People()= Mymeta.__call__()
obj = People(1, y=2)
print('最终的对象字典：', obj.__dict__)


```









# 九 网络编程

Python中内置了一个socket模块，可以快速实现网络之间进行传输数据

## 1 客户端服务端案例

#### 消息上传

- 服务端，放在左边云服务器中（有固定IP）

```python
import socket

# 1.监听本机的IP和端口
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.bind(('123.206.15.88', 8001)) #bind:设置自己ip端口 。IP,端口
sock.listen(5) # 支持排队等待5人

while True:
    # 2.等待客户端来连接，停在这等人连接
    conn, addr = sock.accept() # conn：用户, addr：用户的ip

    # 3.等待，连接者发送消息（阻塞）
    client_data = conn.recv(1024) # recv：读取数据
    
    #用户断开连接会发送一个空，空的话断开
    if not client_data:
            break
    #先转换接收的字节类型在打印
    print(client_data.decode('utf-8')) # decode：字节转成字符串类型

    # 4.给连接者回复消息
    conn.sendall("hello world".encode('utf-8'))#sendall：发送数据，encode：字符串转字节

    # 5.关闭连接
    conn.close()

# 6.停止服务端程序
```

- 客户端，放在用户电脑上

```python
import socket

# 1. 向指定IP发送连接请求
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(('127.0.0.1', 8001))#connect：连接指定ip


# 2.连接成功后，获取系统登录信息
message = client.recv(1024)#recv：读取对方发送的数据
print(message.decode("utf-8"))#decode：转成字符串类型

while True:
    content = input("请输入(q/Q退出)：")
    if content.upper() == 'Q':
        break
    client.sendall(content.encode("utf-8"))#sendall：发送数据。encode：转字节类型

    # 3. 等待，消息的回复
    reply = client.recv(1024)
    print(reply.decode("utf-8"))

# 关闭连接，关闭连接时会向服务端发送空数据。
client.close()
```

#### 文件上传

- 服务端

  ```python
  import socket
  
  sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
  sock.bind(('127.0.0.1', 8001))  # 127.0.0.1 或 查看自己局域网本地IP地址
  sock.listen(5)
  
  conn, addr = sock.accept()
  
  # 接收文件大小
  data = conn.recv(1024)
  total_file_size = int(data.decode('utf-8'))
  
  # 接收文件内容
  file_object = open('xxx.png', mode='wb')
  recv_size = 0
  while True:
      # 每次最多接收1024字节
      data = conn.recv(1024)
      file_object.write(data)
      file_object.flush()
  
      recv_size += len(data)
      # 上传完成
      if recv_size == total_file_size:
          break
  
  # 接收完毕，关闭连接
  conn.close()
  sock.close()
  
  ```

- 客户端

  ```python
  import time
  import os
  import socket
  
  client = socket.socket()
  client.connect(('127.0.0.1', 8001))
  
  file_path = input("请输入要上传的文件：")
  
  # 先发送文件大小
  file_size = os.stat(file_path).st_size#获取文件大小
  client.sendall(str(file_size).encode('utf-8'))#把大小转字符串在以字节模式发送
  
  print("准备...")
  time.sleep(2)
  print("开始上传..")
  file_object = open(file_path, mode='rb')
  read_size = 0
  while True:
      chunk = file_object.read(1024) # 每次读取1024字节
      client.sendall(chunk)
      read_size += len(chunk)
      if read_size == file_size:
          break
  
  client.close()
  ```

  小结：发送前先获取文件大小发送给接收方用于判断是否接收完



##  2 B/S和C/S架构

平时在开发或与人沟通时，经常会有人提到b/s和c/s架构，他们是啥意思呢？

- C/S架构，是Client和Server的简称。开发这种架构的程序意味着你即需要开发客户端也需要开发服务端。

  ```python
  例如：你电脑的上QQ、百度网盘、钉钉、QQ音乐 等安装在电脑上的软件。
  
  服务端：互联网公司会开发一个程序放在他们的服务器上，用于给客户端提供数据支持。
  客户端：大家在电脑安装的相关程序，内部会连接服务端进行收发数据并提供 交互和展示的功能。
  ```

- B/S架构，是Browser和Server的简称。开发这种架构的程序意味着你开发服务端即可，客户端用用户电脑上的浏览器来代替。

  ```
  例如：淘宝、京东等网站。
  
  服务端：互联网公司开发一个网站，放在他们的服务器上。
  客户端：不需要开发，用现成的浏览器即可。
  ```

简而言之，B/S架构就是开发网站；C/S架构就是开发安装在电脑的软件。

## 3 	OSI 7层模型

假设，你在浏览器上输入了一些关键字，内部通过DNS找到对应的IP后，再发送数据时内部会做如下的事：

- 应用层：规定数据的格式。

  ```python
  "GET /s?wd=你好 HTTP/1.1\r\nHost:www.baidu.com\r\n\r\n"
  ```

- 表示层：对应用层数据的编码、压缩（解压缩）、分块、加密（解密）等任务。

  ```python
  "GET /s?wd=你好 HTTP/1.1\r\nHost:www.baidu.com\r\n\r\n你好".encode('utf-8')
  ```

- 会话层：负责与目标建立、中断连接。

  ```
  在发送数据之前，需要会先发送 “连接” 的请求，与远程建立连接后，再发送数据。当然，发送完毕之后，也涉及中断连接的操作。
  ```

- 传输层：建立端口到端口的通信，其实就确定双方的端口信息。

  ```
  数据："GET /s?wd=你好 HTTP/1.1\r\nHost:www.baidu.com\r\n\r\n你好".encode('utf-8')
  端口：
  	- 目标：80
  	- 本地：6784
  ```

- 网络层：标记目标IP信息（IP协议层）

  ```
  数据："GET /s?wd=你好 HTTP/1.1\r\nHost:www.baidu.com\r\n\r\n你好".encode('utf-8')
  端口：
  	- 目标：80
  	- 本地：6784
  IP：
  	- 目标IP：110.242.68.3（百度）
  	- 本地IP：192.168.10.1
  ```

- 数据链路层：对数据进行分组并设置源和目标mac地址

  ```
  数据："POST /s?wd=你好 HTTP/1.1\r\nHost:www.baidu.com\r\n\r\n你好".encode('utf-8')
  端口：
  	- 目标：80
  	- 本地：6784
  IP：
  	- 目标IP：110.242.68.3（百度）
  	- 本地IP：192.168.10.1
  MAC：
  	- 目标MAC：FF-FF-FF-FF-FF-FF 
  	- 本机MAC：11-9d-d8-1a-dd-cd
  ```

- 物理层：将二进制数据在物理媒体上传输。

  ```
  通过网线将二进制数据发送出去
  ```

## 4  UDP和TCP协议

协议，其实就是规定 连接、收发数据的一些规定。

在OSI的 传输层 除了定义端口信息以外，常见的还可以指定UDP或TCP的协议，协议不同连接和传输数据的细节也会不同。

- UDP（User Data Protocol）用户数据报协议， 是⼀个⽆连接的简单的⾯向数据报的传输层协议。 UDP不提供可靠性， 它只是把应⽤程序传给IP层的数据报发送出去， 但是并不能保证它们能到达⽬的地。 由于UDP在传输数据报前不⽤在客户和服务器之间建⽴⼀个连接， 且没有超时重发等机制， 故⽽传输速度很快。

  ```
  常见的有：语音通话、视频通话、实时游戏画面 等。
  ```

- TCP（Transmission Control Protocol，传输控制协议）是面向连接的协议，也就是说，在收发数据前，必须和对方建立可靠的连接，然后再进行收发数据。

  ```
  常见有：网站、手机APP数据获取等。
  ```

  UDP和TCP的区别

  ```python
  UDP，速度快但无法保证数据的准确性。
  TCP，需要先创建可靠连接，在进行收发数据（ack）。
  ```

UDP示例如下：

- 服务端

  ```python
  import socket
  
  server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)#创建连接
  server.bind(('127.0.0.1', 8002))#填自己本地的ip
  
  while True:
      data, (host, port) = server.recvfrom(1024) # 阻塞等待连接
      print(data, host, port)
      server.sendto("好的".encode('utf-8'), (host, port))
  ```

- 客户端

  ```python
  import socket
  
  client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
  while True:
      text = input("请输入要发送的内容：")
      if text.upper() == 'Q':
          break
      client.sendto(text.encode(('utf-8'), ('127.0.0.1', 8002))
      data, (host, port) = client.recvfrom(1024)
      print(data.decode('utf-8'))
  
  client.close()
  ```

  TCP示例如下：

  - 服务端

    ```python
    import socket
    
    # 1.监听本机的IP和端口
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.bind(('127.0.0.1', 8001))
    sock.listen(5)
    
    while True:
        # 2.等待，有人来连接（阻塞）
        conn, addr = sock.accept()          #conn:连接对象
    
        # 3.等待，连接者发送消息（阻塞）
        client_data = conn.recv(1024)       #recv：读取数据，（）号内填指定接收的字节大小
        print(client_data)
    
        # 4.给连接者回复消息
        conn.sendall(b"hello world")        #sendall：发送数据
    
        # 5.关闭连接
        conn.close()
    
    # 6.停止服务端程序
    sock.close()
    ```

  - 客户端

    ```python
    import socket
    
    # 1. 向指定IP发送连接请求
    client = socket.socket()
    client.connect(('127.0.0.1', 8001))
    
    # 2. 连接成功之后，发送消息
    client.sendall(b'hello')
    
    # 3. 等待，消息的回复（阻塞）
    reply = client.recv(1024)
    print(reply)
    
    # 4. 关闭连接
    client.close()
    ```

  网络中的双方想要基于TCP连接进行通信，必须要经过：

  - 创建连接，客户端和服务端要进行三次握手。

  ```
        客户端                                                服务端
  
    1.  SYN-SENT    --> <seq=100><CTL=SYN>               --> SYN-RECEIVED
  
    2.  ESTABLISHED <-- <seq=300><ack=101><CTL=SYN,ACK>  <-- SYN-RECEIVED
  
    3.  ESTABLISHED --> <seq=101><ack=301><CTL=ACK>       --> ESTABLISHED
  
        
  At this point, both the client and server have received an acknowledgment of the connection. The steps 1, 2 establish the connection parameter (sequence number) for one direction and it is acknowledged. The steps 2, 3 establish the connection parameter (sequence number) for the other direction and it is acknowledged. With these, a full-duplex communication is established.
  ```

  - 传输数据

    ```
    在收发数据的过程中，只有有数据的传送就会有应答（ack），如果没有ack，那么内部会尝试重复发送。
    ```

  - 关闭连接，客户端和服务端要进行4次挥手。

    ```
           TCP A                                                TCP B
    
      1.  FIN-WAIT-1  --> <seq=100><ack=300><CTL=FIN,ACK>  --> CLOSE-WAIT
    
      2.  FIN-WAIT-2  <-- <seq=300><ack=101><CTL=ACK>      <-- CLOSE-WAIT
    
      3.  TIME-WAIT   <-- <seq=300><ack=101><CTL=FIN,ACK>  <-- LAST-ACK
    
      4.  TIME-WAIT   --> <seq=101><ack=301><CTL=ACK>      --> CLOSED
    ```

    

## 5 粘包

两台电脑在进行收发数据时，其实不是直接将数据传输给对方。

- 对于发送者，执行 `sendall/send` 发送消息时，是将数据先发送至自己网卡的 写缓冲区 ，再由缓冲区将数据发送给到对方网卡的读缓冲区。
- 对于接受者，执行 `recv` 接收消息时，是从自己网卡的读缓冲区获取数据。

所以，如果发送者连续快速的发送了2条信息，接收者在读取时会认为这是1条信息，即：<span style='color:red;'>**2个数据包粘在了一起

**如何解决粘包的问题？**

> 每次发送的消息时，都将消息划分为 头部（固定字节长度） 和 数据 两部分。例如：头部，用4个字节表示后面数据的长度。
>
> - 发送数据，先发送数据的长度，再发送数据（或拼接起来再发送）。
> - 接收数据，先读4个字节就可以知道自己这个数据包中的数据长度，再根据长度读取到数据。
>
> 对于头部需要一个数字并固定为4个字节，这个功能可以借助python的struct包来实现：

```python
import struct
# i 表示4个字节的int
# 199 表示字节大小为199
v1 = struct.pack('i', 199)# 把199转成固定4字节
print(v1)  # b'\xc7\x00\x00\x00'
 
v2 = struct.unpack('i', v1) # 4个字节转换为数字
print(v2) # 199
```

服务端

```python
import socket
import struct
 
client = socket.socket()
client.connect(('127.0.0.1', 8001))
 
# 第一条数据
data1 = '惰如磨刀之石'.encode('utf-8')
 
len1 = struct.pack('i', len(data1))# 获取要发送数据的字节长度
 
client.sendall(len1)# 先发送数据字节长度
client.sendall(data)# 发送数据
 
# 第二条数据
data2 = '不见其损，日有所耗'.encode('utf-8')
len2 = struct.pack('i', len(data2))
 
client.sendall(len2)
client.sendall(data2)
 
client.close()
```

客户端

```python
import socket
import struct
#创建连接，等待连接
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.bind(('127.0.0.1', 8001))
sock.listen(5)
conn, addr = sock.accept()
 
# 固定读取4字节
header1 = conn.recv(4)
data_length1 = struct.unpack('i', header1)[0]
 
has_recv_len = 0
data1 = b""
while True:
   length = data_length1 - has_recv_len
   if length > 1024:
       lth = 1024
 else:
       lth = length
 chunk = conn.recv(lth) 
# 可能一次收不完，自己可以计算长度再次使用recv收取，只到收完为止。 接收最大字节1024*8 = 8196
   data1 += chunk
   has_recv_len += len(chunk)
   if has_recv_len == data_length1:
       break
print(data1.decode('utf-8'))# 惰如磨刀之石
 
# 固定读取4字节
header2 = conn.recv(4)
data_length2 = struct.unpack('i', header2)[0] # 数据字节长度
 
data2 = conn.recv(data_length2) # 读取数据
print(data2.decode('utf-8')) # 不见其损，日有所耗
 
conn.close()
sock.close()
```



## 6  阻塞和非阻塞

默认情况下我们编写的网络编程的代码都是阻塞的（等待）

- socket服务端（接收者）

```python
import socket
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

sock.setblocking(False) # 加上就变为了非阻塞

sock.bind(('127.0.0.1', 8001))
sock.listen(5)

# 非阻塞
conn, addr = sock.accept()

# 非阻塞
client_data = conn.recv(1024)
print(client_data.decode('utf-8'))

conn.close()
sock.close()

```

- socket客户端（发送者）

```python
import socket
client = socket.socket()

client.setblocking(False) # 加上就变为了非阻塞

# 非阻塞
client.connect(('127.0.0.1', 8001))

client.sendall('alex正在吃翔'.encode('utf-8'))

client.close()
```

如果代码变成了非阻塞，程序运行时一旦遇到 `accept`、`recv`、`connect` 就会抛出 BlockingIOError 的异常。

这不是代码编写的有错误，而是原来的IO阻塞变为非阻塞之后，由于没有接收到相关的IO请求抛出的固定错误。

非阻塞的代码一般与IO多路复用结合，可以迸发出更大的作用。

## 7 IO多路复用

- I/O多路复用指：通过一种机制，可以**监视多个描述符**，一旦某个描述符就绪（一般是读就绪或者写就绪），能够通知程序进行相应的读写操作。

- IO多路复用 + 非阻塞，可以实现让TCP的服务端同时处理多个客户端的请求

```python
import select
import socket
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setblocking(False)  # 加上就变为了非阻塞
server.bind(('127.0.0.1', 8001))
server.listen(5)

inputs = [server, ] # socket对象列表 

while True:
    r, w, e = select.select(inputs, [], [], 0.05) # 检测是否有新连接，有连接 r 就有变化
    for sock in r:
        if sock == server: 
            conn, addr = sock.accept() # 接收新连接。
            print("有新连接")
            inputs.append(conn) # 把连接加入到对象列表
        else:
            data = sock.recv(1024)
            if data:
                # 收到消息在此操作，收到的是空就关闭这个对象的连接
                print("收到消息：", data)
            else:
                print("关闭连接")
                inputs.remove(sock) # 删除列表中的连接对象
	# 没有连接可以在这干点其他事 20s

# 优点：1. 干点那其他的事。2. 让服务端支持多个客户端同时来连接。
```

- IO多路复用 + 非阻塞，可以实现让TCP的客户端同时发送多个请求，例如：去某个网站发送下载图片的请求。

```python
import socket
import select
import uuid
client_list = []  # socket对象列表

for i in range(5): # 创建了5个连接对象
    client = socket.socket()
    client.setblocking(False) # 变非堵塞

    try:
        # 连接百度，虽然有异常BlockingIOError，但向还是正常发送连接的请求
        client.connect(('47.98.134.86', 80))
    except BlockingIOError as e:
        pass

    client_list.append(client) #把连接对象加入到列表

recv_list = []  # 放已连接成功，且已经把下载图片的请求发过去的socket
while True:
    # w = [第一个socket对象,]
    # r = [socket对象,]
    r, w, e = select.select(recv_list, client_list, [], 0.1)
    for sock in w:
        # 连接成功，发送数据
        # 下载图片的请求
        sock.sendall(b"GET /nginx-logo.png HTTP/1.1\r\nHost:47.98.134.86\r\n\r\n")
        recv_list.append(sock) # 把发送请求加入到列表
        client_list.remove(sock)# 删除列表中的连接对象

    for sock in r:
        # 数据发送成功后，接收的返回值
        data = sock.recv(8196)

        recv_list.remove(sock) # 删除列表中的消息对象

    if not recv_list and not client_list: # 都空时结束循环	
        break
        
# 优点：1. 可以伪造除并发的现象。
```

基于 IO多路复用 + 非阻塞的特性，无论编写socket的服务端和客户端都可以提升性能。其中

- IO多路复用，监测socket对象是否有变化（是否连接成功？是否有数据到来等）。
- 非阻塞，socket的connect、recv过程不再等待。

注意：IO多路复用只能用来监听 IO对象 是否发生变化，常见的有：文件是否可读写、电脑终端设备输入和输出、网络请求（常见）。



在Linux操作系统化中 IO多路复用 有三种模式，分别是：select，poll，epoll。（windows 只支持select模式）

> 监测socket对象是否新连接到来 or 新数据到来。

```
select
 
select最早于1983年出现在4.2BSD中，它通过一个select()系统调用来监视多个文件描述符的数组，当select()返回后，该数组中就绪的文件描述符便会被内核修改标志位，使得进程可以获得这些文件描述符从而进行后续的读写操作。
select目前几乎在所有的平台上支持，其良好跨平台支持也是它的一个优点，事实上从现在看来，这也是它所剩不多的优点之一。
select的一个缺点在于单个进程能够监视的文件描述符的数量存在最大限制，在Linux上一般为1024，不过可以通过修改宏定义甚至重新编译内核的方式提升这一限制。
另外，select()所维护的存储大量文件描述符的数据结构，随着文件描述符数量的增大，其复制的开销也线性增长。同时，由于网络响应时间的延迟使得大量TCP连接处于非活跃状态，但调用select()会对所有socket进行一次线性扫描，所以这也浪费了一定的开销。
 
poll
 
poll在1986年诞生于System V Release 3，它和select在本质上没有多大差别，但是poll没有最大文件描述符数量的限制。
poll和select同样存在一个缺点就是，包含大量文件描述符的数组被整体复制于用户态和内核的地址空间之间，而不论这些文件描述符是否就绪，它的开销随着文件描述符数量的增加而线性增大。
另外，select()和poll()将就绪的文件描述符告诉进程后，如果进程没有对其进行IO操作，那么下次调用select()和poll()的时候将再次报告这些文件描述符，所以它们一般不会丢失就绪的消息，这种方式称为水平触发（Level Triggered）。
 
epoll
 
直到Linux2.6才出现了由内核直接支持的实现方法，那就是epoll，它几乎具备了之前所说的一切优点，被公认为Linux2.6下性能最好的多路I/O就绪通知方法。
epoll可以同时支持水平触发和边缘触发（Edge Triggered，只告诉进程哪些文件描述符刚刚变为就绪状态，它只说一遍，如果我们没有采取行动，那么它将不会再次告知，这种方式称为边缘触发），理论上边缘触发的性能要更高一些，但是代码实现相当复杂。
epoll同样只告知那些就绪的文件描述符，而且当我们调用epoll_wait()获得就绪文件描述符时，返回的不是实际的描述符，而是一个代表就绪描述符数量的值，你只需要去epoll指定的一个数组中依次取得相应数量的文件描述符即可，这里也使用了内存映射（mmap）技术，这样便彻底省掉了这些文件描述符在系统调用时复制的开销。
另一个本质的改进在于epoll采用基于事件的就绪通知方式。在select/poll中，进程只有在调用一定的方法后，内核才对所有监视的文件描述符进行扫描，而epoll事先通过epoll_ctl()来注册一个文件描述符，一旦基于某个文件描述符就绪时，内核会采用类似callback的回调机制，迅速激活这个文件描述符，当进程调用epoll_wait()时便得到通知。
```



## 查看本机ip

ipconfig

![image-20210221190426551](assets/image-20210221190426551.png)











# 十 并发编程

**并发编程**，提升代码执行的效率。原来代码执行需要20分钟，学习并发编程后可以加快到1分钟执行完毕。

## 1 进程和线程

```
串行的代码示例就是一个程序，在使用python xx.py 运行时，内部就创建一个进程（主进程），在进程中创建了一个线程（主线程），由线程逐行运行代码。
```

```
线程，是计算机中可以被cpu调度的最小单元(真正在工作）。
进程，是计算机资源分配的最小单元（进程为线程提供资源）。
一个进程中可以有多个线程,同一个进程中的线程可以共享此进程中的资源。
通过 进程 和 线程 都可以将 串行 的程序变为并发
```

### 1.1多线程

- 一个**工厂**，创建一个**车间**，这个车间中创建 **3个工人**，并行处理任务。
- 一个**程序**，创建一个**进程**，这个进程中创建 **3个线程**，并行处理任务。

```python
import threading      # 导入多线程模块
def func(a1,a2,a3):   # 创建一个函数
    pass
t = threaing.Thread(target=func,args=(11,22,33)) # （）号内第一个是函数，第二个是函数的参数
t.start()  # start：执行多线程的函数
```

```python
import time
import requests
import threading
url_list = [
    ("东北F4模仿秀.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0300f570000bvbmace0gvch7lo53oog"),
    ("卡特扣篮.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0200f3e0000bv52fpn5t6p007e34q1g"),
    ("罗斯mvp.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0200f240000buuer5aa4tij4gv6ajqg")
]  
def task(file_name, video_url):
    res = requests.get(video_url)
    with open(file_name, mode='wb') as f:
        f.write(res.content)
    print(time.time())

for name, url in url_list:
    # 创建线程，让每个线程都去执行task函数（参数不同）
    t = threading.Thread(target=task, args=(name, url))
    t.start()
```

### 1.2 多进程

- 一个**工厂**，创建 **三个车间**，每个车间 **一个工人（共3人）**，并行处理任务。
- 一个**程序**，创建 **三个进程**，每个进程 **一个线程（共3人）**，并行处理任务。

```python
import multiprocessing
# 进程创建之后，在进程中还会创建一个线程。
t = multiprocessing.Process(target=函数名, args=(name, url)) # target=函数名  args= 函数参数
t.start() # start执行进程参数
```

```python
import requests
import multiprocessing
url_list = [
    ("东北F4模仿秀.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0300f570000bvbmace0gvch7lo53oog"),
    ("卡特扣篮.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0200f3e0000bv52fpn5t6p007e34q1g"),
    ("罗斯mvp.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0200f240000buuer5aa4tij4gv6ajqg")
]

def task(file_name, video_url):
    res = requests.get(video_url)
    with open(file_name, mode='wb') as f:
        f.write(res.content)

if __name__ == '__main__':
    for name, url in url_list:
        t = multiprocessing.Process(target=task, args=(name, url))
        t.start()
```

### 1.3 GIL锁

- GIL， 全局解释器锁（Global Interpreter Lock），是CPython解释器特有一个玩意，让一个进程中同一个时刻只能有一个线程可以被CPU调用。

- 如果程序想利用 计算机的多核优势，让CPU同时处理一些任务，适合用多进程开发（即使资源开销大）。

- 如果程序不利用 计算机的多核优势，适合用多线程开发

- 常见的程序开发中，计算操作需要使用CPU多核优势，IO操作不需要利用CPU的多核优势，所以，就有这一句话：

  计算密集型，用多进程，例如：大量的数据计算【累加计算示例】。

  IO密集型，用多线程，例如：文件读写、网络数据传输【下载抖音视频示例】

 累加计算示例（计算密集型）：

- 串行处理

  ```python
  import time
  start = time.time()
  result = 0
  for i in range(100000000):
      result += i
  print(result)
  end = time.time()
  print("耗时：", end - start) # 耗时： 9.522780179977417
  ```

- 多进程处理

  ```python
  import time
  import multiprocessing # 导入多进程模块
  
  def task(start, end, queue):
      result = 0
      for i in range(start, end):
          result += i
      queue.put(result)
  
  
  if __name__ == '__main__':
      queue = multiprocessing.Queue() # 创建一个GIL锁
      start_time = time.time()
  
      p1 = multiprocessing.Process(target=task, args=(0, 50000000, queue)) # 把函数放到进程
      p1.start() #执行进程函数
  
      p2 = multiprocessing.Process(target=task, args=(50000000, 100000000, queue))
      p2.start()
  
      v1 = queue.get(block=True) #阻塞
      v2 = queue.get(block=True) #阻塞
      print(v1 + v2)
  
      end_time = time.time()
  
      print("耗时:", end_time - start_time) # 耗时: 2.6232550144195557
  ```

  

- 当然，在程序开发中 多线程 和 多进程 是可以结合使用，例如：创建2个进程（建议与CPU个数相同），每个进程中创建3个线程。

```python
import multiprocessing
import threading

def thread_task(): # 实际执行的函数
    pass

def task(start, end): 
    t1 = threading.Thread(target=thread_task) # 函数内在创建线程
    t1.start()
    t2 = threading.Thread(target=thread_task)
    t2.start()
    t3 = threading.Thread(target=thread_task)
    t3.start()
    
if __name__ == '__main__':
    p1 = multiprocessing.Process(target=task, args=(0, 50000000)) # 创建进程
    p1.start() #执行进程函数
    p2 = multiprocessing.Process(target=task, args=(50000000, 100000000)) # 创建进程
    p2.start()
```

## 2. 多线程开发

```python
import threading
def task(arg):
	pass

t = threading.Thread(target=task,args=('xxx',)) # 创建一个Thread对象（线程），并封装线程被CPU调度时应该执行的任务和相关参数。
t.start() # 线程准备就绪（等待CPU调度），代码继续向下执行。

print("继续执行...") # 主线程执行完所有代码，不结束（等待子线程）
```

线程的常见方法：

- `t.start()`，当前线程准备就绪（等待CPU调度，具体时间是由CPU来决定）。

  ```python
  import threading
  loop = 10000000
  number = 0
  
  def _add(count):
      global number
      for i in range(count):
          number += 1
  
  t = threading.Thread(target=_add,args=(loop,))
  t.start()
  
  print(number)
  ```

- `t.join()`，等待当前线程的任务执行完毕后再向下继续执行。

  ```python
  import threading
  
  number = 0
  
  def _add():
      global number
      for i in range(10000000):
          number += 1
  
  t = threading.Thread(target=_add)
  t.start() # 执行子线程
  
  t.join() # 主线程等待中...,等待子线程完成任务
  
  print(number)
  ```

  ```python
  import threading
  
  number = 0
  
  
  def _add():
      global number
      for i in range(10000000):
          number += 1
  
  
  def _sub():
      global number
      for i in range(10000000):
          number -= 1
  
  
  t1 = threading.Thread(target=_add)
  t2 = threading.Thread(target=_sub)
  t1.start()
  t1.join()  # t1线程执行完毕,才继续往后走
  t2.start()
  t2.join()  # t2线程执行完毕,才继续往后走
  
  print(number) # 结果0
  
  ```

  ```python
  import threading
  
  loop = 10000000
  number = 0
  
  
  def _add(count):
      global number
      for i in range(count):
          number += 1
  
  
  def _sub(count):
      global number
      for i in range(count):
          number -= 1
  
  
  t1 = threading.Thread(target=_add, args=(loop,))
  t2 = threading.Thread(target=_sub, args=(loop,))
  t1.start()
  t2.start()
  
  t1.join()  # t1线程执行完毕,才继续往后走
  t2.join()  # t2线程执行完毕,才继续往后走
  
  print(number) # 结果不确定
  ```

- `t.setDaemon(布尔值)` ，守护线程（必须放在start之前）

  - `t.setDaemon(True)`，设置为守护线程，主线程执行完毕后，子线程也自动关闭。
  - `t.setDaemon(False)`，设置为非守护线程，主线程等待子线程，子线程执行完毕后，主线程才结束。（默认）

  ```python
  import threading
  import time
  
  def task(arg):
      time.sleep(5)
      print('任务')
  
  t = threading.Thread(target=task, args=(11,))
  t.setDaemon(True) # True/False
  t.start()
  
  print('END')
  ```

- 线程名称的设置和获取

  ```python
  import threading
  
  
  def task(arg):
      # 获取当前执行此代码的线程
      name = threading.current_thread().getName()
      print(name)
  
  
  for i in range(10):
      t = threading.Thread(target=task, args=(11,))
      t.setName('日魔-{}'.format(i))
      t.start()
  ```

- 自定义线程类，直接将线程需要做的事写到run方法中。

  ```python
  import threading
  
  
  class MyThread(threading.Thread):
      def run(self):
          print('执行此线程', self._args)
  
  
  t = MyThread(args=(100,))
  t.start() #start：执行线程
  ```

  ```python
  import requests
  import threading
  
  
  class DouYinThread(threading.Thread):
      def run(self):
          file_name, video_url = self._args
          res = requests.get(video_url)
          with open(file_name, mode='wb') as f:
              f.write(res.content)
  
  
  url_list = [
      ("东北F4模仿秀.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0300f570000bvbmace0gvch7lo53oog"),
      ("卡特扣篮.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0200f3e0000bv52fpn5t6p007e34q1g"),
      ("罗斯mvp.mp4", "https://aweme.snssdk.com/aweme/v1/playwm/?video_id=v0200f240000buuer5aa4tij4gv6ajqg")
  ]
  for item in url_list:
      t = DouYinThread(args=(item[0], item[1]))
      t.start()
  
  ```

  

## 3. 线程安全

一个进程中可以有多个线程，且线程共享所有进程中的资源。

多个线程同时去操作一个"东西"，**可能**会存在数据混乱的情况，例如：

- 示例1

  ```python
  import threading
  
  loop = 10000000
  number = 0
  
  
  def _add(count):
      global number
      for i in range(count):
          number += 1
  
  
  def _sub(count):
      global number
      for i in range(count):
          number -= 1
  
  
  t1 = threading.Thread(target=_add, args=(loop,))
  t2 = threading.Thread(target=_sub, args=(loop,))
  t1.start()
  t2.start()
  
  t1.join()  # t1线程执行完毕,才继续往后走
  t2.join()  # t2线程执行完毕,才继续往后走
  
  print(number)
  ```

  ```python
  import threading
  
  lock_object = threading.RLock()
  
  loop = 10000000
  number = 0
  
  
  def _add(count):
      lock_object.acquire() # 加锁
      global number
      for i in range(count):
          number += 1
      lock_object.release() # 释放锁
  
  
  def _sub(count):
      lock_object.acquire() # 申请锁（等待）
      global number
      for i in range(count):
          number -= 1
      lock_object.release() # 释放锁
  
  
  t1 = threading.Thread(target=_add, args=(loop,))
  t2 = threading.Thread(target=_sub, args=(loop,))
  t1.start()
  t2.start()
  
  t1.join()  # t1线程执行完毕,才继续往后走
  t2.join()  # t2线程执行完毕,才继续往后走
  
  print(number)
  
  ```

  

- 示例2：

  ```python
  import threading
  
  num = 0
  
  def task():
      global num
      for i in range(1000000):
          num += 1
      print(num)
  
  
  for i in range(2):
      t = threading.Thread(target=task)
      t.start()
  ```

  ```python
  import threading
  
  num = 0
  lock_object = threading.RLock()
  
  
  def task():
      print("开始")
      lock_object.acquire()  # 第1个抵达的线程进入并上锁，其他线程就需要再此等待。
      global num
      for i in range(1000000):
          num += 1
      lock_object.release()  # 线程出去，并解开锁，其他线程就可以进入并执行了
      print(num)
  
  
  for i in range(2):
      t = threading.Thread(target=task)
      t.start()
  ```

  ```python
  import threading
  
  num = 0
  lock_object = threading.RLock()
  
  
  def task():
      print("开始")
      with lock_object: # 基于上下文管理，内部自动执行 acquire 和 release
          global num
          for i in range(1000000):
              num += 1
      print(num)
  
  
  for i in range(2):
      t = threading.Thread(target=task)
      t.start()
  ```

  



在开发的过程中要注意有些操作默认都是 线程安全的（内部集成了锁的机制），我们在使用的时无需再通过锁再处理，例如：

```python
import threading

data_list = []

lock_object = threading.RLock()


def task():
    print("开始")
    for i in range(1000000):
        data_list.append(i)
    print(len(data_list))


for i in range(2):
    t = threading.Thread(target=task)
    t.start()
```

![image-20210225102151570](assets/image-20210225102151570-16432883702691.png)

所以，要多注意看一些开发文档中是否标明线程安全。



## 4. 线程锁

在程序中如果想要自己手动加锁，一般有两种：Lock 和 RLock。

- import threading #线程锁模块

- lock_object = threading.Lock() # 创建线程锁

- lock_object.acquire() # 申请线程锁

- lock_object.release() #放锁

- Lock，同步锁。

  ```python
  import threading
  
  num = 0
  lock_object = threading.Lock()
  
  
  def task():
      print("开始")
      lock_object.acquire()  # 第1个抵达的线程进入并上锁，其他线程就需要再此等待。
      global num
      for i in range(1000000):
          num += 1
      lock_object.release()  # 线程出去，并解开锁，其他线程就可以进入并执行了
      
      print(num)
  
  
  for i in range(2):
      t = threading.Thread(target=task)
      t.start()
  
  ```

- RLock，递归锁。

  ```python
  import threading
  
  num = 0
  lock_object = threading.RLock()
  
  
  def task():
      print("开始")
      lock_object.acquire()  # 第1个抵达的线程进入并上锁，其他线程就需要再此等待。
      global num
      for i in range(1000000):
          num += 1
      lock_object.release()  # 线程出去，并解开锁，其他线程就可以进入并执行了
      print(num)
  
  
  for i in range(2):
      t = threading.Thread(target=task)
      t.start()
  ```

  

RLock支持多次申请锁和多次释放；Lock不支持。例如：

```python
import threading
import time

lock_object = threading.RLock()


def task():
    print("开始")
    lock_object.acquire()
    lock_object.acquire()
    print(123)
    lock_object.release()
    lock_object.release()


for i in range(3):
    t = threading.Thread(target=task)
    t.start()
```

```python
import threading
lock = threading.RLock()

# 程序员A开发了一个函数，函数可以被其他开发者调用，内部需要基于锁保证数据安全。
def func():
	with lock:
		pass
        
# 程序员B开发了一个函数，可以直接调用这个函数。
def run():
    print("其他功能")
    func() # 调用程序员A写的func函数，内部用到了锁。
    print("其他功能")
    
# 程序员C开发了一个函数，自己需要加锁，同时也需要调用func函数。
def process():
    with lock:
		print("其他功能")
        func() # ----------------> 此时就会出现多次锁的情况，只有RLock支持（Lock不支持）。
		print("其他功能")
```



## 5.死锁

死锁，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象。

```python
import threading

num = 0
lock_object = threading.Lock()


def task():
    print("开始")
    lock_object.acquire()  # 第1个抵达的线程进入并上锁，其他线程就需要再此等待。
    lock_object.acquire()  # 第1个抵达的线程进入并上锁，其他线程就需要再此等待。
    global num
    for i in range(1000000):
        num += 1
    lock_object.release()  # 线程出去，并解开锁，其他线程就可以进入并执行了
    lock_object.release()  # 线程出去，并解开锁，其他线程就可以进入并执行了
    
    print(num)


for i in range(2):
    t = threading.Thread(target=task)
    t.start()


```

```python
import threading
import time 

lock_1 = threading.Lock()
lock_2 = threading.Lock()


def task1():
    lock_1.acquire()
    time.sleep(1)
    lock_2.acquire()
    print(11)
    lock_2.release()
    print(111)
    lock_1.release()
    print(1111)


def task2():
    lock_2.acquire()
    time.sleep(1)
    lock_1.acquire()
    print(22)
    lock_1.release()
    print(222)
    lock_2.release()
    print(2222)


t1 = threading.Thread(target=task1)
t1.start()

t2 = threading.Thread(target=task2)
t2.start()
```



## 6.线程池

Python3中官方才正式提供线程池。

线程不是开的越多越好，开的多了可能会导致系统的性能更低了，例如：如下的代码是不推荐在项目开发中编写。



**不建议**：无限制的创建线程。

```python
import threading


def task(video_url):
    pass

url_list = ["www.xxxx-{}.com".format(i) for i in range(30000)]

for url in url_list:
    t = threading.Thread(target=task, args=(url,))
    t.start()

# 这种每次都创建一个线程去操作，创建任务的太多，线程就会特别多，可能效率反倒降低了。
```

**建议**：使用线程池

示例1：

```python
import time
from concurrent.futures import ThreadPoolExecutor

# pool = ThreadPoolExecutor(100)
# pool.submit(函数名,参数1，参数2，参数...)


def task(video_url,num):
    print("开始执行任务", video_url)
    time.sleep(5)

# 创建线程池，最多维护10个线程。
pool = ThreadPoolExecutor(10)

url_list = ["www.xxxx-{}.com".format(i) for i in range(300)]

for url in url_list:
    # 在线程池中提交一个任务，线程池中如果有空闲线程，则分配一个线程去执行，执行完毕后再将线程交还给线程池；如果没有空闲线程，则等待。
    pool.submit(task, url,2)
    
print("END")
```



示例2：等待线程池的任务执行完毕。

```python
import time
from concurrent.futures import ThreadPoolExecutor


def task(video_url):
    print("开始执行任务", video_url)
    time.sleep(5)


# 创建线程池，最多维护10个线程。
pool = ThreadPoolExecutor(10)

url_list = ["www.xxxx-{}.com".format(i) for i in range(300)]
for url in url_list:
    # 在线程池中提交一个任务，线程池中如果有空闲线程，则分配一个线程去执行，执行完毕后再将线程交还给线程池；如果没有空闲线程，则等待。
    pool.submit(task, url)

print("执行中...")
 pool.shutdown(True)  # 等待线程池中的任务执行完毕后，在继续执行
print('继续往下走')
```



示例3：任务执行完任务，再干点其他事。

```python
import time
import random
from concurrent.futures import ThreadPoolExecutor, Future


def task(video_url):
    print("开始执行任务", video_url)
    time.sleep(2)
    return random.randint(0, 10)


def done(response):
    print("任务执行后的返回值", response.result())


# 创建线程池，最多维护10个线程。
pool = ThreadPoolExecutor(10)

url_list = ["www.xxxx-{}.com".format(i) for i in range(15)]

for url in url_list:
    # 在线程池中提交一个任务，线程池中如果有空闲线程，则分配一个线程去执行，执行完毕后再将线程交还给线程池；如果没有空闲线程，则等待。
    future = pool.submit(task, url)
    future.add_done_callback(done) # 是子主线程执行
    
# 可以做分工，例如：task专门下载，done专门将下载的数据写入本地文件。
```



示例4：最终统一获取结果。

```python
import time
import random
from concurrent.futures import ThreadPoolExecutor,Future


def task(video_url):
    print("开始执行任务", video_url)
    time.sleep(2)
    return random.randint(0, 10)


# 创建线程池，最多维护10个线程。
pool = ThreadPoolExecutor(10)

future_list = []

url_list = ["www.xxxx-{}.com".format(i) for i in range(15)]
for url in url_list:
    # 在线程池中提交一个任务，线程池中如果有空闲线程，则分配一个线程去执行，执行完毕后再将线程交还给线程池；如果没有空闲线程，则等待。
    future = pool.submit(task, url)
    future_list.append(future)
    
pool.shutdown(True)
for fu in future_list:
    print(fu.result())
```

## 7.单例模式（扩展）



面向对象 + 多线程相关的一个面试题（以后项目和源码中会用到）。



之前写一个类，每次执行 `类()` 都会实例化一个类的对象。

```python
class Foo:
    pass

obj1 = Foo()

obj2 = Foo()
print(obj1,obj2)
```



以后开发会遇到单例模式，每次实例化类的对象时，都是最开始创建的那个对象，不再重复创建对象。



- 简单的实现单例模式

  ```python
  class Singleton:
      instance = None
  
      def __init__(self, name):
          self.name = name
          
      def __new__(cls, *args, **kwargs):
          # 返回空对象
          if cls.instance:
              return cls.instance
          cls.instance = object.__new__(cls)
          return cls.instance
  
  obj1 = Singleton('alex')
  obj2 = Singleton('SB')
  
  print(obj1,obj2)
  ```

- 多线程执行单例模式，有BUG

  ```python
  import threading
  import time
  
  
  class Singleton:
      instance = None
  
      def __init__(self, name):
          self.name = name
  
      def __new__(cls, *args, **kwargs):
          if cls.instance:
              return cls.instance
          time.sleep(0.1)
          cls.instance = object.__new__(cls)
          return cls.instance
  
  
  def task():
      obj = Singleton('x')
      print(obj)
  
  
  for i in range(10):
      t = threading.Thread(target=task)
      t.start()
  
  ```

- 加锁解决BUG

  ```python
  import threading
  import time
  class Singleton:
      instance = None
      lock = threading.RLock()
  
      def __init__(self, name):
          self.name = name
          
      def __new__(cls, *args, **kwargs):
          with cls.lock:
              if cls.instance:
                  return cls.instance
              time.sleep(0.1)
              cls.instance = object.__new__(cls)
          return cls.instance
  
  def task():
      obj = Singleton('x')
      print(obj)
  
  for i in range(10):
      t = threading.Thread(target=task)
      t.start()
  ```

- 加判断，提升性能

  ```python
  import threading
  import time
  class Singleton:
      instance = None
      lock = threading.RLock()
  
      def __init__(self, name):
          self.name = name
          
      def __new__(cls, *args, **kwargs):
  
          if cls.instance:
              return cls.instance
          with cls.lock:
              if cls.instance:
                  return cls.instance
              time.sleep(0.1)
              cls.instance = object.__new__(cls)
          return cls.instance
  
  def task():
      obj = Singleton('x')
      print(obj)
  
  for i in range(10):
      t = threading.Thread(target=task)
      t.start()
  
  # 执行1000行代码
  
  data = Singleton('asdfasdf')
  print(data)
  ```



## 1 多进程开发

### 1.1 进程介绍

进程是计算机中资源分配的最小单元；一个进程中可以有多个线程，同一个进程中的线程共享资源；

进程与进程之间则是相互隔离。

Python中通过多进程可以利用CPU的多核优势，计算密集型操作适用于多进程。

- 执行进程要在`if __name__ == '__main__':`下

```python
import multiprocessing

def task():
	pass

if __name__ == '__main__':
    p1 = multiprocessing.Process(target=task)
    p1.start()
```

```python
from multiprocessing import Process

def task(arg):
	pass

def run():
    p = multiprocessing.Process(target=task, args=('xxx',))
    p.start()

if __name__ == '__main__':
    run()
```

关于在Python中基于multiprocessiong模块操作的进程：

- fork:可以拷贝主进程所有包括进程锁文件对象
- pawn，forkserver：只能以参数形式手动传

> - *fork*，【“拷贝”几乎所有资源】【支持文件对象/线程锁等传参】【unix】【任意位置开始】【快】
>
>   The parent process uses [`os.fork()`](https://docs.python.org/3/library/os.html#os.fork) to fork the Python interpreter. The child process, when it begins, is effectively identical to the parent process. All resources of the parent are inherited by the child process. Note that safely forking a multithreaded process is problematic.Available on Unix only. The default on Unix.
>
> - *spawn*，【run参数传必备资源】【不支持文件对象/线程锁等传参】【unix、win】【main代码块开始】【慢】
>
>   The parent process starts a fresh python interpreter process. The child process will only inherit those resources necessary to run the process object’s [`run()`](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Process.run) method. In particular, unnecessary file descriptors and handles from the parent process will not be inherited. Starting a process using this method is rather slow compared to using *fork* or *forkserver*.Available on Unix and Windows. The default on Windows and macOS.
>
> - *forkserver*，【run参数传必备资源】【不支持文件对象/线程锁等传参】【部分unix】【main代码块开始】
>
>   When the program starts and selects the *forkserver* start method, a server process is started. From then on, whenever a new process is needed, the parent process connects to the server and requests that it fork a new process. The fork server process is single threaded so it is safe for it to use [`os.fork()`](https://docs.python.org/3/library/os.html#os.fork). No unnecessary resources are inherited.Available on Unix platforms which support passing file descriptors over Unix pipes.

```python
import multiprocessing
multiprocessing.set_start_method("spawn")
```

案例

```python
import multiprocessing
import threading
import time

def func():
    print("来了")
    with lock:
        print(666)
        time.sleep(1)

def task():
    # 拷贝的锁也是被申请走的状态
    # 被谁申请走了? 被子进程中的主线程申请走了
    for i in range(10):
        t = threading.Thread(target=func)
        t.start()
    time.sleep(2)
    lock.release()


if __name__ == '__main__':
    multiprocessing.set_start_method("fork")
    name = []
    lock = threading.RLock()
    lock.acquire()
    # print(lock)
    # lock.acquire() # 申请锁
    # print(lock)
    # lock.release()
    # print(lock)
    # lock.acquire()  # 申请锁
    # print(lock)

    p1 = multiprocessing.Process(target=task)
    p1.start()
```

### 1.2 常见功能

进程的常见方法：

- `p.start()`，当前进程准备就绪，等待被CPU调度（工作单元其实是进程中的线程）。

- `p.join()`，等待当前进程的任务执行完毕后再向下继续执行。

  ```python
  import time
  from multiprocessing import Process
  
  
  def task(arg):
      time.sleep(2)
      print("执行中...")
  
  
  if __name__ == '__main__':
      multiprocessing.set_start_method("spawn")
      p = Process(target=task, args=('xxx',))
      p.start()
      p.join()
  
      print("继续执行...")
  ```

- `p.daemon = 布尔值`，守护进程（必须放在start之前）

  - `p.daemon =True`，设置为守护进程，主进程执行完毕后，子进程也自动关闭。
  - `p.daemon =False`，设置为非守护进程，主进程等待子进程，子进程执行完毕后，主进程才结束。

  ```python
  import time
  from multiprocessing import Process
  
  
  def task(arg):
      time.sleep(2)
      print("执行中...")
  
  
  if __name__ == '__main__':
      multiprocessing.set_start_method("spawn")
      p = Process(target=task, args=('xxx',))
      p.daemon = True
      p.start()
  
      print("继续执行...")
  
  ```

- 进程的名称的设置和获取

  ```python
  import os
  import time
  import threading
  import multiprocessing
  
  
  def func():
      time.sleep(3)
  
  
  def task(arg):
      for i in range(10):
          t = threading.Thread(target=func)
          t.start()
      print(os.getpid(), os.getppid())
      print("线程个数", len(threading.enumerate()))
      time.sleep(2)
      print("当前进程的名称：", multiprocessing.current_process().name)
  
  
  if __name__ == '__main__':
      print(os.getpid())
      multiprocessing.set_start_method("spawn")
      p = multiprocessing.Process(target=task, args=('xxx',))
      p.name = "哈哈哈哈"
      p.start()
  
      print("继续执行...")
  
  ```

- 自定义进程类，直接将线程需要做的事写到run方法中。

  ```python
  import multiprocessing
  
  
  class MyProcess(multiprocessing.Process):
      def run(self):
          print('执行此进程', self._args)
  
  
  if __name__ == '__main__':
      multiprocessing.set_start_method("spawn")
      p = MyProcess(args=('xxx',))
      p.start()
      print("继续执行...")
  
  ```

- CPU个数，程序一般创建多少个进程？（利用CPU多核优势）。

  ```python
  import multiprocessing
  multiprocessing.cpu_count()
  ```

  ```python
  import multiprocessing
  
  if __name__ == '__main__':
      count = multiprocessing.cpu_count()
      for i in range(count - 1):
          p = multiprocessing.Process(target=xxxx)
          p.start()
  ```

## 2.进程间数据的共享

进程是资源分配的最小单元，每个进程中都维护自己独立的数据，不共享。

如果想要让他们之间进行共享，则可以借助一些特殊的东西来实现。

### 2.1 共享

**Shared memory**

Data can be stored in a shared memory map using [`Value`](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Value) or [`Array`](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Array). For example, the following code

```
    'c': ctypes.c_char,  'u': ctypes.c_wchar,
    'b': ctypes.c_byte,  'B': ctypes.c_ubyte, 
    'h': ctypes.c_short, 'H': ctypes.c_ushort,
    'i': ctypes.c_int,   'I': ctypes.c_uint,  （其u表示无符号）
    'l': ctypes.c_long,  'L': ctypes.c_ulong, 
    'f': ctypes.c_float, 'd': ctypes.c_double
```

```python
from multiprocessing import Process, Value, Array


def func(n, m1, m2):
    n.value = 888
    m1.value = 'a'.encode('utf-8')
    m2.value = "武"


if __name__ == '__main__':
    num = Value('i', 666)
    v1 = Value('c')
    v2 = Value('u')

    p = Process(target=func, args=(num, v1, v2))
    p.start()
    p.join()

    print(num.value)  # 888
    print(v1.value)  # a
    print(v2.value)  # 武
```

```python
from multiprocessing import Process, Value, Array


def f(data_array):
    data_array[0] = 666


if __name__ == '__main__':
    arr = Array('i', [11, 22, 33, 44]) # 数组：元素类型必须是int; 只能是这么几个数据。

    p = Process(target=f, args=(arr,))
    p.start()
    p.join()

    print(arr[:])
```

**Server process**

A manager object returned by `Manager()` controls a server process which holds Python objects and allows other processes to manipulate them using proxies.

```python
from multiprocessing import Process, Manager

def f(d, l):
    d[1] = '1'
    d['2'] = 2
    d[0.25] = None
    l.append(666)

if __name__ == '__main__':
    with Manager() as manager:
        d = manager.dict()
        l = manager.list()

        p = Process(target=f, args=(d, l))
        p.start()
        p.join()

        print(d)
        print(l)
```

### 2.2 交换

[`multiprocessing`](https://docs.python.org/3/library/multiprocessing.html#module-multiprocessing) supports two types of communication channel between processes

**Queues**

![image-20210302110643327](assets/image-20210302110643327.png)

The [`Queue`](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Queue) class is a near clone of [`queue.Queue`](https://docs.python.org/3/library/queue.html#queue.Queue). For example

```python
import multiprocessing


def task(q):
    for i in range(10):
        q.put(i)


if __name__ == '__main__':
    queue = multiprocessing.Queue()
    
    p = multiprocessing.Process(target=task, args=(queue,))
    p.start()
    p.join()

    print("主进程")
    print(queue.get())
    print(queue.get())
    print(queue.get())
    print(queue.get())
    print(queue.get())
```

**Pipes**

![image-20210302110821720](assets/image-20210302110821720.png)

The [`Pipe()`](https://docs.python.org/3/library/multiprocessing.html#multiprocessing.Pipe) function returns a pair of connection objects connected by a pipe which by default is duplex (two-way). For example:

```python
import time
import multiprocessing


def task(conn):
    time.sleep(1)
    conn.send([111, 22, 33, 44])
    data = conn.recv() # 阻塞
    print("子进程接收:", data)
    time.sleep(2)


if __name__ == '__main__':
    parent_conn, child_conn = multiprocessing.Pipe()

    p = multiprocessing.Process(target=task, args=(child_conn,))
    p.start()

    info = parent_conn.recv() # 阻塞
    print("主进程接收：", info)
    parent_conn.send(666)
```

## 3. 进程锁

如果多个进程抢占式去做某些操作时候，为了防止操作出问题，可以通过进程锁来避免。

- import multiprocessing #进程锁模块

- lock = multiprocessing.RLock() # 创建进程RLock锁

- lock.acquire() #申请锁

- lock.release()#放锁

```python
import time
import multiprocessing
import os


def task(lock):
    print("开始")
    lock.acquire()
    # 假设文件中保存的内容就是一个值：10
    with open('f1.txt', mode='r', encoding='utf-8') as f:
        current_num = int(f.read())

    print(os.getpid(), "排队抢票了")
    time.sleep(0.5)
    current_num -= 1

    with open('f1.txt', mode='w', encoding='utf-8') as f:
        f.write(str(current_num))
    lock.release()


if __name__ == '__main__':
    multiprocessing.set_start_method("spawn")
    lock = multiprocessing.RLock()

    process_list = []
    for i in range(10):
        p = multiprocessing.Process(target=task, args=(lock,))
        p.start()
        process_list.append(p)

    # spawn模式，需要特殊处理。
    for item in process_list:
        item.join()
```



## 4. 进程池

- `from concurrent.futures import ProcessPoolExecutor` 导入进程池模块
- `pool = ProcessPoolExecutor(4)`  生成进程池4个

- `pool.submit(task, i)`  执行进程池，第一参数是函数名，第二是函数的参数



```python
import time
from concurrent.futures import ProcessPoolExecutor, ThreadPoolExecutor


def task(num):
    print("执行", num)
    time.sleep(2)


if __name__ == '__main__':
    # 修改模式
    pool = ProcessPoolExecutor(4)
    for i in range(10):
            pool.submit(task, i)
	print(1)
	print(2)

```

```python
import time
from concurrent.futures import ProcessPoolExecutor


def task(num):
    print("执行", num)
    time.sleep(2)


if __name__ == '__main__':

    pool = ProcessPoolExecutor(4)
    for i in range(10):
        pool.submit(task, i)
	# 等待进程池中的任务都执行完毕后，再继续往后执行。
    pool.shutdown(True)
    print(1)

```

```python
import time
from concurrent.futures import ProcessPoolExecutor
import multiprocessing

def task(num):
    print("执行", num)
    time.sleep(2)
    return num


def done(res):
    print(multiprocessing.current_process())
    time.sleep(1)
    print(res.result())
    time.sleep(1)


if __name__ == '__main__':

    pool = ProcessPoolExecutor(4)
    for i in range(50):
        fur = pool.submit(task, i)
        fur.add_done_callback(done) # done的调用由主进程处理（与线程池不同）
        
    print(multiprocessing.current_process())
    pool.shutdown(True)

```



注意：如果在进程池中要使用进程锁，则需要基于Manager中的Lock和RLock来实现。

```python
import time
import multiprocessing
from concurrent.futures.process import ProcessPoolExecutor


def task(lock):
    print("开始")
    # lock.acquire()
    # lock.relase()
    with lock:
        # 假设文件中保存的内容就是一个值：10
        with open('f1.txt', mode='r', encoding='utf-8') as f:
            current_num = int(f.read())

        print("排队抢票了")
        time.sleep(1)
        current_num -= 1

        with open('f1.txt', mode='w', encoding='utf-8') as f:
            f.write(str(current_num))


if __name__ == '__main__':
    pool = ProcessPoolExecutor()
    # lock_object = multiprocessing.RLock() # 不能使用
    manager = multiprocessing.Manager()
    lock_object = manager.RLock() # Lock
    for i in range(10):
        pool.submit(task, lock_object)
```

**案例：计算每天用户访问情况。**

![image-20210326132114601](assets/image-20210326132114601.png)



- 示例

  ```python
  import os
  import time
  from concurrent.futures import ProcessPoolExecutor
  def task(file_name):
      ip_set = set()
      total_count = 0
      ip_count = 0
      file_path = os.path.join("files", file_name)
      file_object = open(file_path, mode='r', encoding='utf-8')
      for line in file_object:
          if not line.strip():
              continue
          user_ip = line.split(" - -", maxsplit=1)[0].split(",")[0]
          total_count += 1
          if user_ip in ip_set:
              continue
          ip_count += 1
          ip_set.add(user_ip)
      time.sleep(1)
      return {"total": total_count, 'ip': ip_count}
  
  def outer(info, file_name):
      def done(res, *args, **kwargs):
          info[file_name] = res.result() # res.result()第三方包要求的固定写法，不加就是字典类型
      return done
  
  def run():
      # 根据目录读取文件并初始化字典
      """
          1.读取目录下所有的文件，每个进程处理一个文件。
      """
      info = {}
      pool = ProcessPoolExecutor(4) # 创建进程池
      for file_name in os.listdir("files"): # 循环files文件夹目录下的文件
          fur = pool.submit(task, file_name) # 执行进程
          fur.add_done_callback(  outer(info, file_name)  ) # 回调函数：主进程
      pool.shutdown(True)
      for k, v in info.items():
          print(k, v)
  
  if __name__ == '__main__':
      run()
  ```


## 5. 协程

计算机中提供了：线程、进程 用于实现并发编程（真实存在）。

协程（Coroutine），是程序员通过代码搞出来的一个东西（非真实存在）。

```
协程也可以被称为微线程，是一种用户态内的上下文切换技术。
简而言之，其实就是通过一个线程实现代码块相互切换执行（来回跳着执行）。
```

> 不要让用户手动去切换，而是遇到IO操作时能自动切换。
>
> Python在3.4之后推出了asyncio模块 + Python3.5推出async、async语法 ，内部基于协程并且遇到IO请求自动化切换。

#### **协程、线程、进程的区别？**

```python
线程，是计算机中可以被cpu调度的最小单元。
进程，是计算机资源分配的最小单元（进程为线程提供资源）。
一个进程中可以有多个线程,同一个进程中的线程可以共享此进程中的资源。

由于CPython中GIL的存在：
	- 线程，适用于IO密集型操作。
    - 进程，适用于计算密集型操作。

协程，协程也可以被称为微线程，是一种用户态内的上下文切换技术，在开发中结合遇到IO自动切换，就可以通过一个线程实现并发操作。


所以，在处理IO操作时，协程比线程更加节省开销（协程的开发难度大一些）。
```

#### `asyncio`模块

**asyncio 是用来编写 并发 代码的库，使用 async/await 语法。**

- *协程函数*: 定义形式为 [`async def`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#async-def) 的函数;
- *协程对象*: 调用 *协程函数* 所返回的对象。

通过 async/await 语法来声明 [协程](https://docs.python.org/zh-cn/3/glossary.html#term-coroutine) 是编写 asyncio 应用的推荐方式。 例如，以下代码段会打印 "hello"，等待 1 秒，再打印 "world"

```python
>>> import asyncio

>>> async def main():
...     print('hello')
...     await asyncio.sleep(1)
...     print('world')

>>> asyncio.run(main())
hello
world
```

注意：简单地调用一个协程并不会使其被调度执行,用async生成的函数加括号是一个对象

```python
>>> main()
<coroutine object main at 0x1053bb7c8>
```



#### asyncio.run()

要真正运行一个协程，asyncio 提供了三种主要机制:

- `asyncio.run()` 函数用来运行最高层级的入口点 "main()" 函数 (参见上面的示例。)

- 等待一个协程。以下代码段会在等待 1 秒后打印 "hello"，然后 *再次* 等待 2 秒后打印 "world":

  ```python
  import asyncio
  import time
  
  async def say_after(delay, what):
      await asyncio.sleep(delay)
      print(what)
  
  async def main():
      print(f"started at {time.strftime('%X')}")
  
      await say_after(1, 'hello')
      await say_after(2, 'world')
  
      print(f"finished at {time.strftime('%X')}")
  
  asyncio.run(main())
  ```

  预期的输出:

  ```
  started at 17:13:52
  hello
  world
  finished at 17:13:55
  ```



#### `asyncio.create_task()`

- `asyncio.create_task()` 函数用来并发运行作为 asyncio [`任务`](https://docs.python.org/zh-cn/3/library/asyncio-task.html#asyncio.Task) 的多个协程。

  让我们修改以上示例main函数，*并发* 运行两个 `say_after` 协程:

  ```python
  async def main():
      task1 = asyncio.create_task(
          say_after(1, 'hello'))
  
      task2 = asyncio.create_task(
          say_after(2, 'world'))
  
      print(f"started at {time.strftime('%X')}")
  
      # 等到两个任务都完成（应该大约需要 2 秒。）
      await task1
      await task2
  
      print(f"finished at {time.strftime('%X')}")
  ```

  注意，预期的输出显示代码段的运行时间比之前快了 1 秒:

  ```
  started at 17:14:32
  hello
  world
  finished at 17:14:34
  ```



## 































































- 文章

  ```python
  https://pythonav.com/wiki/detail/6/91/
  https://zhuanlan.zhihu.com/p/137057192
  ```

- 视频

  ```
  https://www.bilibili.com/video/BV1NA411g7yf
  ```

  

# 其它

## 1 导出项目依赖包

到指正项目目录下输入命令

```python
pip freeze > ./requirements.txt
```



