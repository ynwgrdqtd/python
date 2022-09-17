

## 1 安装 & 配置 & 启动

MySQL现在的版本主要分为：

- 5.x 版本，现在互联网企业中的主流版本，包括：头条、美图、百度、腾讯等互联网公司主流的版本。
- 8.x 版本，新增了一些了窗口函数、持久化配置、隐藏索引等其他功能。

所以，我们课程会以常用大版本中最新的版本为例来讲解，即：5.7.31 （依然有很多企业在用5.6.x，但新项目基本上都是5.7.x了）。

### 1.1 win系统

#### **第1步：下载安装**

https://downloads.mysql.com/archives/community/

#### **第2步：解压至任意文件夹：解压就是安装了**

#### **第3步：创建配置文件**

在MySQL的安装目录下创建 `my.ini` 的文件，作为MySQL的配置文件。

配置内容

```
[mysqld]

# 端口
port=3306
# 安装路径，就是解压路径,
basedir=C:\\Program Files\\mysql-5.7.31-winx64
# 初始化路径，安装路径加一个设置的初始文件夹data
datadir=C:\\Program Files\\mysql-5.7.31-winx64\\data
```

注意，设置文件后缀显示，不然怕找不到

其实，MySQL的配置文件可以放在很多的目录，下图是配置文件的优先级：

![image-20210510150530193](mysql.assets/image-20210510150530193.png)



强烈，建议大家还是把配置文件放在MySQL安装目录下，这样以后电脑上想要安装多个版本的MySQL时，配置文件可以相互独立不影响。

注意：如果你电脑的上述其他目录存在MySQL配置文件，建议删除，否则可能会影响MySQL的启动。

#### 第4步：初始化

```
>>> "C:\Program Files\mysql-5.7.31-winx64\bin\mysqld.exe"  --initialize-insecure
    "D:\mysql\mysql-5.7.31-winx64\mysql-5.7.31-winx64\bin\mysqld.exe"  --initialize-insecure
```

初始化命令在执行时，会自动读取配置文件并执行初始化，此过程主要会做两件事：

- 自动创建data目录，以后我们的数据都会存放在这个目录。
- 同时创建建必备一些的数据，例如默认账户 root （无密码），用于登录MySQL并通过指令操作MySQL。

![image-20210510151829891](mysql.assets/image-20210510151829891.png)



在windowns安装过程中如果有报错 （ msvcr120.dll不存在 ），请下载并安装下面的两个补丁：

- vcredist：https://www.microsoft.com/zh-cn/download/confirmation.aspx?id=40784  （主要）
  <img src="mysql.assets/image-20210508115414183.png" alt="image-20210508115414183" style="zoom:33%;" />

- dirctx：https://www.microsoft.com/zh-CN/download/details.aspx?id=35
  <img src="mysql.assets/image-20210508115521913.png" alt="image-20210508115521913" style="zoom: 33%;" />







#### 第5步：启动

启动MySQL常见的有两种方式：

- 终端临时启动

  ```sql
   "C:\Program Files\mysql-5.7.31-winx64\bin\mysqld.exe"
  ```

  注意：此时程序会挂起，内部就是可以接收客户端发来的MySQL指令，关闭窗口或Ctrl+c 就可以停止运行。

  这种启动方式每次开机或想要开启都需要手动执行一遍命令比较麻烦。

- 制作windows服务，基于windows服务管理。

  mysql57：设置的名称

  ```sql
  >>>"C:\Program Files\mysql-5.7.31-winx64\bin\mysqld.exe" --install mysql57
  ```

  创建好服务之后，可以通过命令 启动和关闭服务，例如：

  ```sql
   net start mysql57  --启动
   net stop mysql57  --关闭
  ```

```sql
  
也可以在window的服务管理中点击按钮启动和关闭服务。
  
任务管理器>服务>找到名称
  
以后不再想要使用window服务了，也可以将制作的这个MySQL服务删除。
"C:\Program Files\mysql-5.7.31-winx64\bin\mysqld.exe" --remove mysql57  
```


#### 第6步：测试连接MySQL

安装并启动MySQL之后，就可以连接MySQL来测试是否已正确安装并启动成功。
以后在开发时，肯定是要用Python代码来连接MySQL并且进行数据操作（后面讲）。
在安装MySQL时，其实也自动安装了一个工具（客户端），让我们快速实现连接MySQL并发送指令。

```sql
连接命令
"路径\mysql.exe" -h 127.0.0.1 -P 3306 -u root -p 
注意：如把bin目录加入环境变量，每次在运行命令时，就不用再重新输入绝对路径了。
上述过程如果操作完成之后，证明你的安装和启动过程就搞定了。

```

### 1.2 mac系统

mac系统和win不同，MySQL为他提供了非常方便的一站式安装程序，只要点击、next就可以安装、初始化完成。



#### 第1步：安装和初始化

https://downloads.mysql.com/archives/community/

<img src="mysql.assets/image-20210508103830229.png" alt="image-20210508103830229"  />

<img src="mysql.assets/image-20210508165414794.png" alt="image-20210508165414794" style="zoom:50%;" />



<img src="mysql.assets/image-20210508171059416.png" alt="image-20210508171059416" style="zoom:50%;" />



这个基于dmg文件的安装过程，其实包含了：

- 安装，默认安装在了 `/usr/local/mysql-5.7.31-macos10.14-x86_64/`目录。
- 初始化，在安装目录下创建data目录用于存放数据； 初始化模块数据库以及账户相关等，例如： 账cd

![image-20210510103342842](mysql.assets/image-20210510103342842.png)



#### 第2步：创建配置文件

建议在MySQL安装目录下创建 `etc/my.cnf` 作为MySQL的配置文件。

![image-20210510161700478](mysql.assets/image-20210510161700478.png)



MySQL的配置文件按照优先级，会在以下目录中寻找：

![image-20210510161845843](mysql.assets/image-20210510161845843.png)



为了避免多个版本共存时，配置文件混乱的问题，建议大家还是把配置文件放在当前MySQL的安装目录下。



#### 第3步：启动

在Mac系统中启动MySQL常见的有2种方式：

- 安装目录中自带 `mysql.server` 脚本（建议）

  ```python
  sudo /usr/local/mysql/support-files/mysql.server start
  # 输入电脑密码
  
  sudo mysql.server start
  # 输入电脑密码
  ```


  sudo /usr/local/mysql/support-files/mysql.server stop


  ![image-20210510162854578](mysql.assets/image-20210510162854578.png)


  为了避免每次执行命令都需要些路径，可以将路径 `/usr/local/mysql/support-files`加入到环境变量中。

![image-20210510165107737](mysql.assets/image-20210510165107737.png)

  操作完成之后，再在终端执行下命令：`source ~/.zprofile` 让设置的环境变量立即生效。

  注意：mac系统的版本如果比较老，会显示空白的 `zprofile` 文件，此就要去打开   `bash_profile` 文件。


  这样设置好之后，以后就可以使用下面的命令去启动和关闭MySQL了。


sudo mysql.server start
sudo mysql.server stop




- 系统偏好设置（不推荐）

<img src="mysql.assets/image-20210510104009559.png" alt="image-20210510104009559" style="zoom: 33%;" />





第一种`mysql.server`脚本的形式，内部是使用 `mysqld_safe`运行，可以守护我们的MySQL进程，如意外挂掉可自动重启。



#### 第4步：测试连接MySQL

安装并启动MySQL之后，就可以连接MySQL来测试是否已正确安装并启动成功。

![image-20210510153336093](mysql.assets/image-20210510153336093.png)

以后在开发时，肯定是要用Python代码来连接MySQL并且进行数据操作（后面讲）。

在安装MySQL时，其实也自动安装了一个工具（客户端），让我们快速实现连接MySQL并发送指令。

![image-20210510171029083](mysql.assets/image-20210510171029083.png)

![image-20210510171004699](mysql.assets/image-20210510171004699.png)

注意：`/usr/local/mysql/bin`也可以加入到环境变量。

至此，在Mac系统中关于MySQL的安装和配置就完成了。





### 1.3 关于密码



#### 1. 设置和修改root密码

在windows系统中模块默认 root 账户是没有密码的，如果想要为账户设定密码，可以在利用root账户登录成功之后，执行：

![image-20210530001548192](mysql.assets/image-20210530001548192.png)

```python
set password = password("666");
```



#### 2. 忘记root密码

如果你忘记了MySQL账户的密码。

- 修改配置文件，在 [mysqld] 节点下添加 `skip-grant-tables=1`

  ```
  [mysqld]
  ...
  skip-grant-tables=1
  ...
  ```

- 重启MySQL，再次登录时，不需要密码直接可以进去了

  - windows重启

    ```
    net stop mysql57
    net start mysql57
    ```

  - mac重启

    ```
    sudo mysql.server restart
    ```

  重启后，无序密码就可以进入。

  ```
  >>> mysql -u root -p
  ```

- 进入数据库后执行修改密码命令

  ```
  use mysql;
  update user set authentication_string = password('新密码'),password_last_changed=now() where user='root';
  ```

- 退出并再次修改配置文件，删除 [mysqld] 节点下的 `skip-grant-tables=1`

  ```
  [mysqld]
  ...
  # skip-grant-tables=1
  ...
  ```

- 再次重启，以后就可以使用新密码登录了。



## 2. 数据库 

内置客户端操作指令

当连接上MySQL之后，执行如下指令（一般称为SQL语句），就可以对MySQL的数据进行操作。

### 1 连接mysql

```
"路径\mysql.exe -h 127.0.0.1 -P 3308 -u root -p 
```

### 2 查看所有的数据库：

 ````
show databases;
 ````

### 3 创建数据库

```
创建数据库:  create database 数据库名 default charset 编码 collate 排序规则;

create database 数据库名 DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
```

```python
create database day25db;
create database student DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
```

### 4 删除数据库

```
drop database 数据库名;
```

### 5 进入数据库

```
use 数据库名;
```

### 6 查看所有表

- 先进入到数据库下在执行

```
show tables;
```

### 7 退出

```
exit;
```

### 8 导入导出数据库

```sql
mysqldump -h IP -u 用户名 -p -d 数据库名 > 导出的文件名

参数解析：
-h:表示host地址
-u:表示user用户
-p:表示password密码
-d:表示不导出数据
（1）-p 后面不能加password，只能单独输入数据库名称
（2）mysqldump是在cmd下的命令，不能再mysql下面，即不能进入mysql的（如果进入了mysql，得exit退出mysql后才可以的。）
```

#### 1 导出

导出数据库结构和数据（此时不用加-d），如下导出库dbtest中所有表结构和数据

```sql
mysqldump -h 127.0.0.1 -u root -p student1 > D:\pythonapp\student1.sql
```

只导出数据库表结构（此时要加-d），如下导出库dbtest中的users表结构没有数据

```sql
mysqldump -h 192.168.182.134 -u root -p -d dbtest > C:\Users\Administrator\Desktop\users2.sql
```

导出某张表结构和数据（此时不用加-d），如下导出库dbtest中的users表结构和数据

```
mysqldump -h 192.168.182.134 -u root -p dbtest users > C:\Users\Administrator\Desktop\users2.sql
```

导出某张表结构（此时要加-d），如下导出库dbtest中的users表结构

```
mysqldump -h 192.168.182.134 -u root -p -d dbtest users > C:\Users\Administrator\Desktop\users2.sql
```

#### 2 导入

一：已经建好数据库，导入数据库文件
（1）首先登录并进入数据库：

```
本地访问：
mysql -h localhost -u root -p

远程访问：
mysql -h 192.168.182.120 -uroot -p
 
参数解析：
-h:表示host地址，本地直接使用localhost，远程需要使用ip地址
-u:表示user用户
-p:表示password密码
```

2.登录成功后执行导入命令source+文件路径：

```
source C:\Users\Administrator\Desktop\users2.sql
```

二：没有数据库，需要先创建数据库

```sql
mysql -h localhost -u root -p（进入mysql下面）

create database dbtest; (创建数据库)

show databases;(查看数据库列表)

use dbtest;(进入dbtest数据库下面)

show tables;(刚创建的数据库dbtest下面空没有表)

source C:\Users\Administrator\Desktop\users2.sql（导入数据库表）

show tables;(查看dbtest数据库下面的所有表,就可以看到表了)

desc users;(查看表结构设计)

select * from users;(查询所有的数据)

exit;(或者ctrl + c)退出mysql
```









## 3 数据表 

其实在数据库中创建数据库 和 创建Excel非常类似，需要指定： `表名`、`列名称`、`类类型（整型、字符串或其他)`。

### 1 创建表

![image-20210511102323966](mysql.assets/image-20210511102323966.png)

```sql
create table 表名(
    列名  类型 约束,
    列名  类型 约束,
   列名  类型 约束
)default charset=utf8;
```

```sql
   create table tb5(
        id int not null auto_increment primary key,	-- 不允许为空 & 自增 & 主键
        name varchar(16) not null unique,   		-- 不允许为空 ,不能重复
        email varchar(32) null,      		-- 允许为空（默认）
        age int default 3            		-- 插入数据时，如果不给age列设置值，默认值：3
    )default charset=utf8;
```

### 1.1表结构约束

##### 1 允许空&不允许空

```sql
null      -- 允许
not null  -- 不允许
```

##### 2 自增 

用于主键 int 格式，默认步长1步，自增1，可以修改

![image-20220317223728909](mysql.assets/image-20220317223728909.png)

```sql
auto_increment
```

##### 3 主键

`innodb`引擎必须有主键，值不能重复，不设置主键会默认值不为空列帮你设一个

```sql
primary key

create table '表'(
id int primary key    		 -- 单一主键
)

create table '表'(
	id int,
	ip char,
	primary key(id,ip)      -- 联合主键
)
```

##### 4 设默认值

可以结合不允许空使用

```sql
default 3
default '男'
```

##### 5 唯一

单列唯一和，多列唯一

```sql
unique
```

```sql
create table '表'(
	id int unique,          -- id单独唯一
	ip char(15),
	port int,
	unique(ip,port)         -- ip和端口联合唯一
)
```

##### 7 外键（表关系）

```sql
foreign key
```

###### 1 初始外键

创建表时加外键：不要设置删除和更新同步，影响表以后的扩展

```sql
constraint '外键名' foreign key ('外键列') references '主键表'('主键列')
```

```sql
# 先创建一个部门表
create table depart(
	id int not null auto_increment primary key,
    title varchar(16) not null
)default charset=utf8;


create table info(
	id int not null auto_increment primary key,
    name varchar(16) not null,
    email varchar(32) not null,
    age int,
    depart_id int not null,
    constraint fk_info_depart foreign key (depart_id) references depart(id)   -- 创建外键
    on delete cascade                                                         -- 删除同步
    on update cascade 														  -- 更新同步
)default charset=utf8;
```

###### 2 添加外键

如果表结构已创建好了，额外想要增加外键：

```sql
-- 选要修改的   表    添加个外键      设键名         要设的列名                    要关联的列名
alter table info add constraint fk_info_depart foreign key info(depart_id) references depart(id);
```

###### 3 删除外键：

```sql
-- 选要修改的  表   选择要删除的       外键名
alter table info drop foreign key fk_info_depart;
```

多对一：主表不重复，外键表重复的。比如一个老师有多个学生

一对一：主表不重复，外键表也不重复的，在外键上在加一个唯一约束。比如一个家庭老师教一个学生

多对多：表1有很多重复的关联表2，表2也重复的关联表1，这时用第3张表来存

```sql
create table boy(
	id int not null auto_increment primary key,
    name varchar(16) not null
)default charset=utf8;

create table girl(
	id int not null auto_increment primary key,
    name varchar(16) not null
)default charset=utf8;


create table boy_girl(
	id int not null auto_increment primary key,
    boy_id int not null,
    girl_id int not null,
    constraint fk_boy_girl_boy foreign key boy_girl(boy_id) references boy(id),
    constraint fk_boy_girl_girl foreign key boy_girl(girl_id) references girl(id)
)default charset=utf8;
```

如果表结构已创建好了，额外想要增加外键：

```sql
alter table boy_girl add constraint fk_boy_girl_boy foreign key boy_girl(boy_id) references boy(id);

alter table boy_girl add constraint fk_boy_girl_girl foreign key boy_girl(girl_id) references girl(id);
```

删除外键：

```sql
alter table info drop foreign key fk_boy_girl_boy;
alter table info drop foreign key fk_boy_girl_girl;
```

在以后项目开发时，设计表结构及其关系的是一个非常重要的技能。一般项目开始开发的步骤：

- 需求调研
- 设计数据库表结构（根据需求）
- 项目开发（写代码）

大量的工作应该放在前2个步骤，前期的设计完成之后，后续的功能代码开发就比较简单了。









### 1.2 表结构类型

##### 1 数字

- `int[(m)][unsigned][zerofill]`
- 数字类型括号内设定的值是显示宽度，默认最长，不用设置，没用的

```sql
int				表示有符号，取值范围：-2147483648 ～ 2147483647
int unsigned	表示无符号，取值范围：0 ～ 4294967295
int(5)zerofill	仅用于显示，当不满足5位时，按照左边补0，例如：00002；满足时，正常显示。
```

- `tinyint[(m)] [unsigned] [zerofill]`

```sql
tinyint unsigned 有符号，取值范围：-128 ～ 127.
tinyint zerofill 无符号，取值范围：0 ～ 255
```

- `bigint[(m)][unsigned][zerofill]`

```sql
bigint unsigned 有符号，取值范围：-9223372036854775808 ～ 9223372036854775807
bigint zerofill 无符号，取值范围：0  ～  18446744073709551615
```

- `decimal[(m[,d])] [unsigned] [zerofill]`

```sql
准确的小数值，m是数字总个数（负号不算），d是小数点后个数。 m最大值为65，d最大值为30。
decimal(8,2)
```

- `FLOAT[(M,D)] [UNSIGNED] [ZEROFILL]`

  ```sql
  FLOAT(6,1)  单精度浮点数，非准确小数值，m是数字总个数，d是小数点后个数。
  ```

- `DOUBLE[(M,D)] [UNSIGNED] [ZEROFILL]`

  ```sql
  DOUBLE(6,3)  双精度浮点数（非准确小数值），m是数字总个数，d是小数点后个数。
  ```

##### 2 字符串

`char(m)`

```sql
定长字符串，m代表字符串的长度，最多可容纳255个字符。

定长的体现：即使内容长度小于m，也会占用m长度。例如：char(5)，数据是：yes，底层也会占用5个字符；如果超出m长度限制（默认MySQL是严格模式，所以会报错）。
    如果在配置文件中加入如下配置，
        sql-mode="NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
    保存并重启，此时MySQL则是非严格模式，此时超过长度则自动截断（不报错）。。

注意：默认底层存储是固定的长度（不够则用空格补齐），但是查询数据时，会自动将空白去除。 如果想要保留空白，在sql-mode中加入 PAD_CHAR_TO_FULL_LENGTH 即可。
查看模式sql-mode，执行命令：show variables  like 'sql_mode';

一般适用于：固定长度的内容。

create table L3(
    id int not null primary key auto_increment,
    name varchar(5),
    depart char(3)
)default charset=utf8;

insert into L3(name,depart) values("alexsb","sbalex");
```

`varchar(m)`

```sql
变长字符串，m代表字符串的长度，最多可容纳65535个字节。

变长的体现：内容小于m时，会按照真实数据长度存储；如果超出m长度限制（（默认MySQL是严格模式，所以会报错）。
    如果在配置文件中加入如下配置，
        sql-mode="NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
    保存并重启，此时MySQL则是非严格模式，此时超过长度则自动截断（不报错）。

例如：
create table L3(
    id int not null primary key auto_increment,
    name varchar(5),
    depart char(3)
)default charset=utf8;
```

`text`

```
text数据类型用于保存变长的大字符串，可以组多到65535 (2**16 − 1)个字符。

一般情况下，长文本会用text类型。例如：文章、新闻等。
```

```sql
create table L4(
	id int not null primary key auto_increment,
    title varchar(128),
	content text
)default charset=utf8;
```

`mediumtext`

```
A TEXT column with a maximum length of 16,777,215 (2**24 − 1) characters.
```

`longtext`

```
A TEXT column with a maximum length of 4,294,967,295 or 4GB (2**32 − 1)
```

##### 3 时间

`datetime` 

```sql
datetime
YYYY-MM-DD HH:MM:SS（1000-01-01 00:00:00/9999-12-31 23:59:59）
对于DATETIME，不做任何改变，原样输入和输出。
```

`timestamp`

```sql
timestamp
YYYY-MM-DD HH:MM:SS（1970-01-01 00:00:00/2037年）
对于TIMESTAMP，它把客户端插入的时间从当前时区转化为UTC（世界标准时间）进行存储，查询时，将其又转化为客户端当前时区进行返回。
```

```sql
mysql> create table L5(
    -> id int not null primary key auto_increment,
    -> dt datetime,
    -> tt timestamp
    -> )default charset=utf8;
Query OK, 0 rows affected (0.03 sec)

mysql> insert into L5(dt,tt) values("2025-11-11 11:11:44", "2025-11-11 11:11:44");

mysql> select * from L5;
+----+---------------------+---------------------+
| id | dt                  | tt                  |
+----+---------------------+---------------------+
|  1 | 2025-11-11 11:11:44 | 2025-11-11 11:11:44 |
+----+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | CST    | 
| time_zone        | SYSTEM |
+------------------+--------+
2 rows in set (0.00 sec)
-- “CST”指的是MySQL所在主机的系统时间，是中国标准时间的缩写，China Standard Time UT+8:00

mysql> set time_zone='+0:00';
Query OK, 0 rows affected (0.00 sec)

mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | CST    |
| time_zone        | +00:00 |
+------------------+--------+
2 rows in set (0.01 sec)

mysql> select * from L5;
+----+---------------------+---------------------+
| id | dt                  | tt                  |
+----+---------------------+---------------------+
|  1 | 2025-11-11 11:11:44 | 2025-11-11 03:11:44 |
+----+---------------------+---------------------+
1 row in set (0.00 sec)
```

 `date`

```sql
  date
  年月日 YYYY-MM-DD（1000-01-01/9999-12-31）
```

`time`

```sql
time
时分秒 HH:MM:SS（'-838:59:59'/'838:59:59'）
```

主键一般用于表示当前这条数据的ID编号（类似于人的身份证），需要我们自己来维护一个不重复的值，比较繁琐。所以，在数据库中一般会将主键和自增结合。

##### 4 枚举类型（设值只选一个，男&女）

`enum()`例如性别表，只能选其中一个

```sql
create table '表名'(
	id int,
	sex enum('男','女') default '男'                    -- 创建表格式，默认为男
)


insert into '表名' values(1,'男'),(2,'女')  -- 插入数据sex列只能男或女
```

5 集合类型（设值可多选，兴趣）

`set()`

```sql
create table '表名'(
	id int,
	sex enum('游戏','学习','运动')                     -- 创建表格式
)


insert into '表名' values(1,'学习,运动'),(2,'游戏,学习')  -- 插入数据能多选
```



### 2 删除表

```
drop table 表名;
```

### 3 清空表

```sql
delete from 表名;                   -- 无条件清空表   这个一般用于删除数据行
delete from 表名 where id= 1;       -- 有条件删除数据


truncate table 表名;                -- 清空表用这个合适（速度快、无法回滚撤销等）
```

### 4 修改表

##### 1 添加列 

```sql
alter table 表名 add 列名 类型;
alter table 表名 add 列名 类型 DEFAULT 默认值;
alter table 表名 add 列名 类型 not null default 默认值;
alter table 表名 add 列名 类型 not null primary key auto_increment;
```

##### 2 删除列

```sql
alter table 表名 drop column 列名;
```

##### 3  修改列 类型

```sql
alter table 表名 modify column 列名 类型;
alter table registry modify column phone varchar(64) not null;
```

##### 4 修改列 类型 + 名称

```sql
alter table 表名 change 原列名 新列名 新类型;
```

```sql
alter table  tb change id nid int not null;
alter table  tb change id id int not null default 5;
alter table  tb change id id int not null primary key auto_increment;
alter table  tb change id id int; -- 允许为空，删除默认值，删除自增。
```

##### 5 修改列 默认值

```sql
ALTER TABLE 表名 ALTER 列名 SET DEFAULT 1000;
```

##### 6 删除列 默认值

```sql
ALTER TABLE 表名 ALTER 列名 DROP DEFAULT;
```

##### 7 添加主键

```sql
alter table 表名 add primary key(列名);
```

##### 8 删除主键

```sql
alter table 表名 drop primary key;
```

#### 5 查询表结构

```sql
desc 表名
```

#### 6 查询建表时指令

```sql
show create table 表名
```









## 4 数据行 

当数据库和数据表创建完成之后，就需要对数据表中的内容进行：增、删、改、查了。

![image-20210511102323966](mysql.assets/image-20210511102323966-16456162972781.png)

#### 1 新**增**数据

```sql
insert into 表名 (列名,列名,列名) values(对应列的值,对应列的值,对应列的值);
# 插入另一个表的所有数据
insert into 表名 select * from score;
```

```sql
insert into tb1(name,password) values('武沛齐','123123');
insert into tb1(name,password) values('武沛齐','123123'),('alex','123');

insert into tb1 values('武沛齐','123123'),('alex','123'); -- 如果表中只有2列
insert into registry(name,user,password,phone,time) values('qdq明','116796','0103','13640891308','2022-03-08 16:20:00')
```

#### 2 删除数据

```sql
delete from 表名;
delete from 表名 where 条件;
```

```sql
delete from tb1;
delete from tb1 where name="wupeiqi";
delete from tb1 where name="wupeiqi" and password="123";
delete from tb1 where id>9;
```

```sql
delete from xl where xl = ' 02025005拆装（换）档位按键总成 ';
```



#### 3 修**改**数据

```sql
update 表名 set 列名=值;
update 表名 set 列名=值 where 条件;
```

```sql
update xl set xl='03043601更换遥控器电子/电池' where xl = '03043601更换遥控器电子/电池 02011310拆装（换）右前轮胎（条） ';
```



```sql
update tb1 set name="wupeiqi";
update tb1 set name="wupeiqi" where id=1;

update tb1 set age=age+1;  -- 整型
update tb1 set age=age+1 where id=2;

update L3 set name=concat(name,"db");
update L3 set name=concat(name,"123")  where id=2;  -- concat一个函数，可以拼接字符串
```

#### 4 查询数据

```sql
select * from 表名;
select 列名,列名,列名 from 表名;
select 列名,列名 as 别名,列名 from 表名;
select * from 表名 where 条件;
```

```sql
select * from tb1;                          -- 查询所有列
select id,name,age from tb1;
select id,name as N,age, from tb1;          -- 查询对应需求列
select id,name as N,age, 111 from tb1;

select * from oooo where id1 = 1714875;
select * from tb1 where id > 1;
select * from tb1 where id != 1;
select * from tb1 where name="wupeiqi" and password="123";
```

##### 1 去重

DISTINCT：把显示的内容去重

```sql
select distinct '列' from '表';
```

##### 2 四则运算

+-*/：把显示的int列内容加运算

```sql
select '列'*15 fron '表';
```

##### 3 字符连接

`CONCAT`:多列自定义连接显示

```sql
select concat('列1','列2') from '表';                      -- 打印显示就会连在一起
select concat('列1','自定义字符','列2') from '表';           -- 还可以自定义显示
```



##  5 查询SQL语句

这一部分的SQL语句都是围绕着对 表中的数据进行操作的。

#### 1 条件

根据条件搜索结果。

```sql
where 
```

![image-20210517184600205](mysql.assets/image-20210517184600205.png)

```sql
select * from info where age > 30;
select * from info where id > 1;
select * from info where id = 1;
select * from info where id >= 1;
select * from info where id != 1;
select * from info where id between 2 and 4;   -- id大于等于2、且小于等于4

select * from info where name = '武沛齐' and age = 19;
select * from info where name = 'alex' or age = 49;
select * from info where (name = '李杰' or email="pyyu@live.com")  and age=49;

select * from info where id in (1,4,6); -- 在1，4，6的
select * from info where id not in (1,4,6); -- 不在1.4.6的
select * from info where id in (select id from depart); -- 存在depar表id的
# select * from info where id in (1,2,3);

# exists select * from depart where id=5，去查数据是否存在，如果存在显示，如果不存在不查
select * from info where exists (select * from depart where id=5);
select * from info where not exists (select * from depart where id=5);

# 2次条件
select * from (select * from info where id>2) as T where age > 10;
```

```sql
select * from info where info.id > 10; -- 2个表时用表名.键名
select * from info where id > 10;
```



#### 2  通配符(模糊搜索)

```sql
like "%沛%"
```

一般用于模糊搜索。`%`和`_`  百分号指1到多的字符，下划线一个代指一个字符

```sql
select * from info where name like "%沛%";
select * from info where name like "%沛";
select * from info where email like "%@live.com";
select * from info where name like "武%齐";
select * from info where name like "k%y";
select * from info where email like "wupeiqi%";


select * from info where email like "_@live.com";
select * from info where email like "_upeiqi@live.com";
select * from info where email like "__peiqi@live.com";
select * from info where email like "__peiqi_live.co_";
```

注意：数量少，数据量大的搜索。



#### 3 映射(自定义列)

对列的显示操作

##### 3.1自定义列名临时显示

```sql
# 获取 id name 列并把name列名临时显示NM
select id, name as NM from info;
```

##### 3.2临时新增列

```sql
# 123是新增临时列，列名内容都是123
select id, name as NM, 123  from info;

注意：少些select * ,自己需求。

select 
	id,
	name,
	666 as num,
	( select max(id) from depart ) as mid, -- max/min/sum
	( select min(id) from depart) as nid, -- max/min/sum
	age
from info;

+----+--------+-----+------+------+------+
| id | name   | num | mid  | nid  | age  |
+----+--------+-----+------+------+------+
|  1 | 武沛齐 | 666 |    3 |    1 |   19 |
|  2 | 于超   | 666 |    3 |    1 |   49 |
|  3 | alex   | 666 |    3 |    1 |    9 |
|  4 | tony   | 666 |    3 |    1 |   29 |
|  5 | kelly  | 666 |    3 |    1 |   99 |
|  6 | james  | 666 |    3 |    1 |   49 |
|  7 | 李杰   | 666 |    3 |    1 |   49 |
+----+--------+-----+------+------+------+
```

##### 3.3表关联方法

```sql
select 
	id,
	name,
	( select title from depart where depart.id=info.depart_id) as x1
from info;

# 注意：效率很低

select 
	id,
	name,
	( select title from depart where depart.id=info.depart_id) as x1,
	( select title from depart where depart.id=info.id) as x2
from info;
```

##### 3.4条件显示方法

```sql
case 列名 when 条件 then 成立就显示 else 不成立显示这个 end 要显示的列名
```

```sql
select 
	id,
	name,
	case depart_id when 1 then "第1部门" end v1
from info;
select 
	id,
	name,
	case depart_id when 1 then "第1部门" else "其他" end v2
from info;

select 
	id,
	name,
	case depart_id when 1 then "第1部门" end v1,
	case depart_id when 1 then "第1部门" else "其他" end v2,
	case depart_id when 1 then "第1部门" when 2 then "第2部门" else "其他" end v3,
	case when age<18 then "少年" end v4,
	case when age<18 then "少年" else "油腻男" end v5,
	case when age<18 then "少年" when age<30 then "青年" else "油腻男" end v6
from info;
```

#### 4 排序

倒序

```sql
order by 列 desc -- 倒序
```

顺序

```sql
order by 列 asc  -- 顺序
```

```sql
select * from info order by age desc; -- 倒序
select * from info order by age asc;  -- 顺序

select * from info order by age asc,id desc; -- 优先按照age从小到大；如果age相同则按照id从大到小。

# 先条件过后在排序
select * from info where id>10 order by age asc,id desc;
select * from info where id>6 or name like "%y" order by age asc,id desc;
```



#### 5 取部分数据

```sql
select * from info limit 5;   										-- 获取5条数据
```

```sql
select * from info order by id desc limit 3;						-- 先排序，再获取前3条数据
select * from info where id > 4 order by id desc limit 3;			-- 条件后，先排序，再获取前3条数据
```

从xx位置开始取

```sql
select * from info limit 3 offset 2;	                            -- 从位置2开始，向后获取3行数据
```

```sql
 -- 数据库表中：1000条数据。
select * from info limit 10 offset 0;    --  第一页：
select * from info limit 10 offset 10;   --  第二页：
```







#### 6 分组（聚合,去重）

聚合语句

```sql
group by '列名'   -- 对 age列去重分组
```

聚合后条件

```sql
having '条件'

select depart_id,count(id) from info group by depart_id having count(id) > 2; -- 对各个部门`depart_id`有分组后在设置条件大于2
```



```sql
max(id)      -- age列统计后id列取             最大的
min(id)      -- age列统计后id列取             最小的
count(id)    -- age列相同的有几个             统计
sum(id)      -- age列统计相同有几个后id相加的   和
avg(id)      -- age列统计相同有几个后id        平均值

select age,max(id),min(id),count(id),sum(id),avg(id) from info group by age;

```

对相同年龄`age`的人分组,统计相同年龄人各有几个

```sql
select age,count(id) from info group by age;
```

对各个部门`depart_id`有几个人分组

```sql
select depart_id,count(id) from info group by depart_id;
```

```sql
select count(id) from info;  -- 统计id列有几个
select max(id) from info;    -- 取id列最大的
```

```sql
(select max(id) from info group by age) -- 对年龄相同的id取最大的，然后给当判断
+---------+
| max(id) |
+---------+
|       3 |
|       1 |
|       4 |
|       7 |
|       5 |
+---------+、
# 然后取有13457的所有列

select * from info where id in (select max(id) from info group by age);
```

```sql
select age,count(id) from info group by age having count(id) > 2;
select age,count(id) from info where id > 4 group by age having count(id) > 2;  -- 聚合条件放在having后面
```

```sql
到目前为止SQL执行顺序：
    where               -- 条件筛选
    group by            -- 分组聚合
    having              -- 分组聚合后的条件            
    order by            -- 排序
    limit               -- 取值（设定的是前多少条）
```



```sql
select age,count(id) from info where id > 2 group by age having count(id) > 1 order by age desc limit 1;


select age,count(id) from info -- 要查询的表info
where id > 2                   -- 条件 id>2
group by age                   -- 根据age分组
having count(id) > 1           -- 对分组后的数据再根据聚合条件过滤 count(id)>1
order by age desc              -- 根据age从大到小排序
limit 1                         -- 获取第1条
```



#### 7 左右连表

多个表可以连接起来进行查询。

格式，使用一个就行，左右表调转功能一样：

```sql
left outer join     -- 左边是主表右是从表
right outer join    -- 右是主左是从

主表 left outer join 从表 on 主表.x = 从表.id 、
从表 right outer join 主表 on 主表.x = 从表.id 

select * from info left outer join depart on info.depart_id = depart.id;
```

多表连接

```sql
select * from '表1'
		left outer join '表2' on info.depart_id = depart.id 
		left outer join '表3' on xx.xxx = xxx.xx
```



#### 8 联合（两表列连接）

- 取不同的表 对应多少列上下连接，格式可以不一样， 列数需相同
- 关键字`union`  会 自动去重    ；   `union all` 不去重

```sql
select id from depart 
union                            -- 自动去重  
select id from info;
```

```sql
select id from depart 
union all                       -- 保留所有      
select id from info;
```

#### 9 SQ L执行优先顺序

```sql
到目前为止SQL执行顺序：
    join                -- 连接，，选连接才能做其它
    on                  -- 连接条件
    where               -- 条件筛选
    group by            -- 分组聚合
    having              -- 分组聚合后的条件            
    order by            -- 排序，顺序或倒序
    limit               -- 取值（设定的是前多少条）
```





## 6 索引

在数据库中索引最核心的作用是：**加速查找**。  例如：在含有300w条数据的表中查询，无索引需要700秒，而利用索引可能仅需1秒。

在开发过程中：查询手机号、邮箱、用户名等。会被搜索的列 创建索引，以提高程序的响应速度。

### 1 索引原理

为什么加上索引之后速度能有这么大的提升呢？ 因为索引的底层是基于B+Tree的数据结构存储的。

![image-20210526160040895](mysql.assets/image-20210526160040895.png)

![image-20210526155746811](mysql.assets/image-20210526155746811.png)

![image-20210526160519425](mysql.assets/image-20210526160519425.png)

很明显，如果有了索引结构的查询效率比表中逐行查询的速度要快很多且数据量越大越明显。

B+Tree结构连接：https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html

数据库的索引是基于上述B+Tree的数据结构实现，但在创建数据库表时，如果指定不同的引擎，底层使用的B+Tree结构的原理有些不同。

- myisam引擎，非聚簇索引（数据 和 索引结构 分开存储）

- innodb引擎，聚簇索引（数据 和 主键索引结构存储在一起）




#### 1.1.1 非聚簇索引（mysiam引擎）

```sql
create table 表名(
    id int not null auto_increment primary key, 
    name varchar(32) not null,
    age int
)engine=myisam default charset=utf8;
```


![image-20210526160040895](mysql.assets/image-20210526160040895.png)

![image-20210526155746811](mysql.assets/image-20210526155746811-16464872177692.png)

![image-20210526155118552](mysql.assets/image-20210526155118552.png)



#### 1.1.2 聚簇索引（innodb引擎）

不设置默认是innodb引擎

```sql
create table 表名(
    id int not null auto_increment primary key, 
    name varchar(32) not null,
    age int
)engine=innodb default charset=utf8;
```


![image-20210526160040895](mysql.assets/image-20210526160040895.png)

![image-20210526155746811](mysql.assets/image-20210526155746811-16464872177692.png)

![image-20210526160519425](mysql.assets/image-20210526160519425-16464872177693.png)

![image-20210526155250801](mysql.assets/image-20210526155250801.png)

在MySQL文件存储中的体现：

```
root@192 userdb # pwd
/usr/local/mysql/data/userdb
root@192 userdb # ls -l
total 1412928
-rw-r-----  1 _mysql  _mysql       8684 May 15 22:51 big.frm，表结构。
-rw-r-----  1 _mysql  _mysql  717225984 May 15 22:51 big.ibd，数据和索引结构。
-rw-r-----  1 _mysql  _mysql       8588 May 16 11:38 goods.frm
-rw-r-----  1 _mysql  _mysql      98304 May 16 11:39 goods.ibd
-rw-r-----  1 _mysql  _mysql       8586 May 26 10:57 t2.frm，表结构
-rw-r-----  1 _mysql  _mysql          0 May 26 10:57 t2.MYD，数据
-rw-r-----  1 _mysql  _mysql       1024 May 26 10:57 t2.MYI，索引结构
```



上述 聚簇索引 和 非聚簇索引 底层均利用了B+Tree结构结构，只不过内部数据存储有些不同罢了。

在企业开发中一般都会使用 innodb 引擎（内部支持事务、行级锁、外键等特点），在MySQL5.5版本之后默认引擎也是innodb。

```sql
mysql> show create table users \G;
*************************** 1. row ***************************
       Table: users
Create Table: CREATE TABLE `users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(32) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL,
  `ctime` datetime DEFAULT NULL,
  `age` int(11) DEFAULT '5',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8
1 row in set (0.00 sec)

ERROR:
No query specified

mysql> show index from users \G;
*************************** 1. row ***************************
        Table: users
   Non_unique: 0
     Key_name: PRIMARY
 Seq_in_index: 1
  Column_name: id
    Collation: A
  Cardinality: 3
     Sub_part: NULL
       Packed: NULL
         Null:
   Index_type: BTREE   -- 虽然显示BTree，但底层数据结构基于B+Tree。
      Comment:
Index_comment:
1 row in set (0.00 sec)

ERROR:
No query specified

mysql>
```

innodb引擎，一般创建的索引：聚簇索引。

### 1.2 常见索引

在innodb引擎下，索引底层都是基于B+Tree数据结构存储（聚簇索引）。

![image-20210526160040895](mysql.assets/image-20210526160040895.png)

在开发过程中常见的索引类型有：

- 主键索引：加速查找、不能为空、不能重复。 + 联合主键索引
- 唯一索引：加速查找、不能重复。  + 联合唯一索引
- 普通索引：加速查找。 + 联合索引



#### 1.2.1 主键和联合主键索引

创建表时加索引

```sql
# 原本方式
create table 表名(
    id int not null auto_increment primary key,   
    name varchar(32) not null
);

create table 表名(
    id int not null auto_increment,
    name varchar(32) not null,
    primary key(id)  -- 也可以这样
);

create table 表名(
    id int not null auto_increment,
    name varchar(32) not null,
    primary key(列1,列2)  -- 联合主键方式       
);
```

新增主键索引

```sql
alter table 表名 add primary key(列名);
```

删除主键索引

```sql
alter table 表名 drop primary key;
```

注意：删除索引时列有自增属性会报错，因为自增列必须定义为主键。

```sql
-- 用修改列的方法也和删除差不多
alter table 表 change 原列名 新列名 int not null;
```





#### 1.2.2 唯一和联合唯一索引

创建表时加唯一索引

```sql
create table 表名(
    id int not null auto_increment primary key,
    name varchar(32) not null,
    email varchar(64) not null,
    unique ix_name (name),    -- unique创建一个唯一索引，ix_name是自定义的索引名，（）内是列名
    unique ix_email (email),
);

create table 表名(
    id int not null auto_increment,
    name varchar(32) not null,
    unique (列1,列2)               -- 如果有多列，称为联合唯一索引。
);
```

添加唯一索引

```sql
create unique index 索引名 on 表名(列名);
```

删除唯一索引

```sql
drop unique index 索引名 on 表名;
```



#### 1.2.3 索引和联合索引

添加索引

```sql
create table 表名(
    id int not null auto_increment primary key,
    name varchar(32) not null,
    email varchar(64) not null,
    index ix_email (email),
    index ix_name (name),     -- 单索引
);

create table 表名(
    id int not null auto_increment primary key,
    name varchar(32) not null,
    email varchar(64) not null,
    index ix_email (name,email)     -- 如果有多列，称为联合索引。
);
```

添加索引

```sql
create index 索引名 on 表名(列名);
```

删除索引

```sql
drop index 索引名 on 表名;
```

在项目开发的设计表结构的环节，需要根据业务需求的特点来决定是否创建相应的索引。

#### 案例：博客系统

![image-20210531164453161](mysql.assets/image-20210531164453161.png)

- 每张表id列都创建 自增 + 主键。
- 用户表
  - 用户名 + 密码 创建联合索引。
  - 手机号，创建唯一索引。
  - 邮箱，创建唯一索引。
- 推荐表
  - user_id和article_id创建联合唯一索引。

### 1.3 操作表

在表中创建索引后，查询时一定要命中索引。

![image-20210526170700985](mysql.assets/image-20210526170700985.png)



![image-20210526155746811](mysql.assets/image-20210526155746811-16464885280154.png)

在数据库的表中创建索引之后优缺点如下：

- 优点：查找速度快、约束（唯一、主键、联合唯一）
- 缺点：插入、删除、更新速度比较慢，因为每次操作都需要调整整个B+Tree的数据结构关系。

所以，在表中不要无节制的去创建索引啊。。。



在开发中，我们会对表中经常被搜索的列创建索引，从而提高程序的响应速度。

![image-20210526170718219](mysql.assets/image-20210526170718219.png)

```sql
CREATE TABLE `big` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    `name` varchar(32) DEFAULT NULL,
    `email` varchar(64) DEFAULT NULL,
    `password` varchar(64) DEFAULT NULL,
    `age` int(11) DEFAULT NULL,
    PRIMARY KEY (`id`),                       -- 主键索引
    UNIQUE KEY `big_unique_email` (`email`),  -- 唯一索引
    index `ix_name_pwd` (`name`,`password`)     -- 联合索引
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```



一般情况下，我们针对只要通过索引列去搜搜都可以 `命中` 索引（通过索引结构加速查找）。

```sql
select * from big where id = 5;
select * from big where id > 5;
select * from big where email = "wupeiqi@live.com";
select * from big where name = "武沛齐";
select * from big where name = "kelly" and password="ffsijfs";
...
```



但是，还是会有一些特殊的情况，让我们无法命中索引（即使创建了索引），这也是需要大家在开发中要注意的。

![image-20210526170718219](mysql.assets/image-20210526170718219.png)

- 类型不一致

  ```sql
  select * from big where name = 123;		-- 未命中
  select * from big where email = 123;	-- 未命中
  
  特殊的主键：
  	select * from big where id = "123";	-- 命中
  ```

- 使用不等于

  ```sql
  select * from big where name != "武沛齐";				-- 未命中
  select * from big where email != "wupeiqi@live.com";  -- 未命中
  
  特殊的主键：
  	select * from big where id != 123;	-- 命中
  ```

- or，当or条件中有未建立索引的列才失效。

  ```sql
  select * from big where id = 123 or password="xx";			-- 未命中
  select * from big where name = "wupeiqi" or password="xx";	-- 未命中
  特别的：
  	select * from big where id = 10 or password="xx" and name="xx"; -- 命中
  ```

- 排序，当根据索引排序时候，选择的映射如果不是索引，则不走索引。

  ```sql
  select * from big order by name asc;     -- 未命中
  select * from big order by name desc;    -- 未命中
  
  特别的主键：
  	select * from big order by id desc;  -- 命中
  ```

- like，模糊匹配时。匹配符在最后才命中

  ```sql
  select * from big where name like "%u-12-19999";	-- 未命中
  select * from big where name like "_u-12-19999";	-- 未命中
  select * from big where name like "wu-%-10";		-- 未命中
  
  特别的：
  	select * from big where name like "wu-1111-%";	-- 命中
  	select * from big where name like "wuw-%";		-- 命中
  ```

- 使用函数

  ```sql
  select * from big where reverse(name) = "wupeiqi";  -- 未命中
  
  特别的：
  	select * from big where name = reverse("wupeiqi");  -- 命中
  ```

- 最左前缀，如果是联合索引，要遵循最左前缀原则。

  ```sql
  如果联合索引为：(name,password)
      name and password       -- 命中
      name                 	-- 命中
      password                -- 未命中
      name or password       	-- 未命中
  ```

  



### 1.4 执行计划

MySQL中提供了执行计划，让你能够预判SQL的执行（只能给到一定的参考，不一定完全能预判准确）。

```
explain + SQL语句;
```

![image-20210527074105599](mysql.assets/image-20210527074105599.png)

其中比较重要的是 type，他他SQL性能比较重要的标志，性能从低到高依次：`all < index < range < index_merge < ref_or_null < ref < eq_ref < system/const` 

- ALL，全表扫描，数据表从头到尾找一遍。(一般未命中索引，都是会执行权标扫描)

  ```sql
  select * from big;
  
  特别的：如果有limit，则找到之后就不在继续向下扫描.
  	select * from big limit 1;
  ```

- INDEX，全索引扫描，对索引从头到尾找一遍

  ```sql
  explain select id from big;
  explain select name from big;
  ```

- RANGE，对索引列进行范围查找

  ```sql
  explain select * from big where id > 10;
  explain select * from big where id in (11,22,33);
  explain select * from big where id between 10 and 20;
  explain select * from big where name > "wupeiqi" ;
  ```

- INDEX_MERGE，合并索引，使用多个单列索引搜索

  ```sql
  explain select * from big where id = 10 or name="武沛齐";
  ```

- REF，根据 索引 直接去查找（非键）。

  ```sql
  select *  from big where name = '武沛齐';
  ```

- EQ_REF，连表操作时常见。

  ```sql
  explain select big.name,users.id from big left join users on big.age = users.id;
  ```

- CONST，常量，表最多有一个匹配行,因为仅有一行,在这行的列值可被优化器剩余部分认为是常数,const表很快。

  ```sql
  explain select * from big where id=11;					-- 主键
  explain select * from big where email="w-11-0@qq.com";	-- 唯一索引
  ```

- SYSTEM，系统，表仅有一行(=系统表)。这是const联接类型的一个特例。

  ```sql
   explain select * from (select * from big where id=1 limit 1) as A;
  ```



其他列：

```
id，查询顺序标识

z，查询类型
    SIMPLE          简单查询
    PRIMARY         最外层查询
    SUBQUERY        映射为子查询
    DERIVED         子查询
    UNION           联合
    UNION RESULT    使用联合的结果
    ...
    
table，正在访问的表名

partitions，涉及的分区（MySQL支持将数据划分到不同的idb文件中，详单与数据的拆分）。 一个特别大的文件拆分成多个小文件（分区）。

possible_keys，查询涉及到的字段上若存在索引，则该索引将被列出，即：可能使用的索引。
key，显示MySQL在查询中实际使用的索引，若没有使用索引，显示为NULL。例如：有索引但未命中，则possible_keys显示、key则显示NULL。

key_len，表示索引字段的最大可能长度。(类型字节长度 + 变长2 + 可空1)，例如：key_len=195，类型varchar(64)，195=64*3+2+1

ref，连表时显示的关联信息。例如：A和B连表，显示连表的字段信息。

rows，估计读取的数据行数（只是预估值）
	explain select * from big where password ="025dfdeb-d803-425d-9834-445758885d1c";
	explain select * from big where password ="025dfdeb-d803-425d-9834-445758885d1c" limit 1;
filtered，返回结果的行占需要读到的行的百分比。
	explain select * from big where id=1;  -- 100，只读了一个1行，返回结果也是1行。
	explain select * from big where password="27d8ba90-edd0-4a2f-9aaf-99c9d607c3b3";  -- 10，读取了10行，返回了1行。
	注意：密码27d8ba90-edd0-4a2f-9aaf-99c9d607c3b3在第10行
	
extra，该列包含MySQL解决查询的详细信息。
    “Using index”
    此值表示mysql将使用覆盖索引，以避免访问表。不要把覆盖索引和index访问类型弄混了。
    “Using where”
    这意味着mysql服务器将在存储引擎检索行后再进行过滤，许多where条件里涉及索引中的列，当（并且如果）它读取索引时，就能被存储引擎检验，因此不是所有带where子句的查询都会显示“Using where”。有时“Using where”的出现就是一个暗示：查询可受益于不同的索引。
    “Using temporary”
    这意味着mysql在对查询结果排序时会使用一个临时表。
    “Using filesort”
    这意味着mysql会对结果使用一个外部索引排序，而不是按索引次序从表里读取行。mysql有两种文件排序算法，这两种排序方式都可以在内存或者磁盘上完成，explain不会告诉你mysql将使用哪一种文件排序，也不会告诉你排序会在内存里还是磁盘上完成。
    “Range checked for each record(index map: N)”
    这个意味着没有好用的索引，新的索引将在联接的每一行上重新估算，N是显示在possible_keys列中索引的位图，并且是冗余的。
```

上述索引相关的内容讲的比较多，大家在开发过程中重点应该掌握的是：

- 根据情况创建合适的索引（加速查找）。
- 有索引，则查询时要命中索引。





## 7 函数

MySQL中提供了很多函数，为我们的SQL操作提供便利，例如：

```sql
-- 反转字符
reverse(列名)
-- 合并列
concat(列名，列名)
-- 显示当前时间
NOW()
-- 设置时间格式
DATE_FORMAT( NOW(),'%Y-%m-%d %H:%i:%s')
```



```sql
mysql> select * from d1;
+----+-----------+
| id | name      |
+----+-----------+
|  1 | 武沛齐    |
|  3 | xxx       |
|  4 | pyyu      |
+----+-----------+
3 rows in set (0.00 sec)

mysql> select count(id), max(id),min(id),avg(id) from d1;
+-----------+---------+---------+---------+
| count(id) | max(id) | min(id) | avg(id) |
+-----------+---------+---------+---------+
|         3 |       4 |       1 |  2.6667 |
+-----------+---------+---------+---------+
1 row in set (0.00 sec)

mysql>
mysql>
mysql> select id,reverse(name) from d1;  -- reverse反转字符
+----+---------------+
| id | reverse(name) |
+----+---------------+
|  1 | 齐沛武        |
|  3 | xxx           |
|  4 | uyyp          |
+----+---------------+
3 rows in set (0.00 sec)

mysql> select id, reverse(name),concat(name,name), NOW(), DATE_FORMAT( NOW(),'%Y-%m-%d %H:%i:%s')  from d1;
+----+---------------+--------------------+---------------------+-----------------------------------------+
| id | reverse(name) | concat(name,name)  | NOW()               | DATE_FORMAT( NOW(),'%Y-%m-%d %H:%i:%s') |
+----+---------------+--------------------+---------------------+-----------------------------------------+
|  1 | 齐沛武        | 武沛齐武沛齐       | 2021-05-27 09:18:07 | 2021-05-27 09:18:07                     |
|  3 | xxx           | xxxxxx             | 2021-05-27 09:18:07 | 2021-05-27 09:18:07                     |
|  4 | uyyp          | pyyupyyu           | 2021-05-27 09:18:07 | 2021-05-27 09:18:07                     |
+----+---------------+--------------------+---------------------+-----------------------------------------+
3 rows in set (0.00 sec)

mysql> select concat("alex","sb");
+---------------------+
| concat("alex","sb") |
+---------------------+
| alexsb              |
+---------------------+
1 row in set (0.00 sec)

mysql> select sleep(1);
+----------+
| sleep(1) |
+----------+
|        0 |
+----------+
1 row in set (1.00 sec)
```



### 1 部分函数列表

```sql
CHAR_LENGTH(str)
    返回值为字符串str 的长度，长度的单位为字符。一个多字节字符算作一个单字符。
    对于一个包含五个二字节字符集, LENGTH()返回值为 10, 而CHAR_LENGTH()的返回值为5。

CONCAT(str1,str2,...)
    字符串拼接
    如有任何一个参数为NULL ，则返回值为 NULL。
CONCAT_WS(separator,str1,str2,...)
    字符串拼接（自定义连接符）
    CONCAT_WS()不会忽略任何空字符串。 (然而会忽略所有的 NULL）。

CONV(N,from_base,to_base)
    进制转换
    例如：
        SELECT CONV('a',16,2); 表示将 a 由16进制转换为2进制字符串表示

FORMAT(X,D)
    将数字X 的格式写为'#,###,###.##',以四舍五入的方式保留小数点后 D 位， 并将结果以字符串的形式返回。若  D 为 0, 则返回结果不带有小数点，或不含小数部分。
    例如：
        SELECT FORMAT(12332.1,4); 结果为： '12,332.1000'
INSERT(str,pos,len,newstr)
    在str的指定位置插入字符串
        pos：要替换位置其实位置
        len：替换的长度
        newstr：新字符串
    特别的：
        如果pos超过原字符串长度，则返回原字符串
        如果len超过原字符串长度，则由新字符串完全替换
INSTR(str,substr)
    返回字符串 str 中子字符串的第一个出现位置。

LEFT(str,len)
    返回字符串str 从开始的len位置的子序列字符。

LOWER(str)
    变小写

UPPER(str)
    变大写

LTRIM(str)
    返回字符串 str ，其引导空格字符被删除。
RTRIM(str)
    返回字符串 str ，结尾空格字符被删去。
SUBSTRING(str,pos,len)
    获取字符串子序列

LOCATE(substr,str,pos)
    获取子序列索引位置

REPEAT(str,count)
    返回一个由重复的字符串str 组成的字符串，字符串str的数目等于count 。
    若 count <= 0,则返回一个空字符串。
    若str 或 count 为 NULL，则返回 NULL 。
REPLACE(str,from_str,to_str)
    返回字符串str 以及所有被字符串to_str替代的字符串from_str 。
REVERSE(str)
    返回字符串 str ，顺序和字符顺序相反。
RIGHT(str,len)
    从字符串str 开始，返回从后边开始len个字符组成的子序列

SPACE(N)
    返回一个由N空格组成的字符串。

SUBSTRING(str,pos) , SUBSTRING(str FROM pos) SUBSTRING(str,pos,len) , SUBSTRING(str FROM pos FOR len)
    不带有len 参数的格式从字符串str返回一个子字符串，起始于位置 pos。带有len参数的格式从字符串str返回一个长度同len字符相同的子字符串，起始于位置 pos。 使用 FROM的格式为标准 SQL 语法。也可能对pos使用一个负值。假若这样，则子字符串的位置起始于字符串结尾的pos 字符，而不是字符串的开头位置。在以下格式的函数中可以对pos 使用一个负值。

    mysql> SELECT SUBSTRING('Quadratically',5);
        -> 'ratically'

    mysql> SELECT SUBSTRING('foobarbar' FROM 4);
        -> 'barbar'

    mysql> SELECT SUBSTRING('Quadratically',5,6);
        -> 'ratica'

    mysql> SELECT SUBSTRING('Sakila', -3);
        -> 'ila'

    mysql> SELECT SUBSTRING('Sakila', -5, 3);
        -> 'aki'

    mysql> SELECT SUBSTRING('Sakila' FROM -4 FOR 2);
        -> 'ki'

TRIM([{BOTH | LEADING | TRAILING} [remstr] FROM] str) TRIM(remstr FROM] str)
    返回字符串 str ， 其中所有remstr 前缀和/或后缀都已被删除。若分类符BOTH、LEADIN或TRAILING中没有一个是给定的,则假设为BOTH 。 remstr 为可选项，在未指定情况下，可删除空格。

    mysql> SELECT TRIM('  bar   ');
            -> 'bar'

    mysql> SELECT TRIM(LEADING 'x' FROM 'xxxbarxxx');
            -> 'barxxx'

    mysql> SELECT TRIM(BOTH 'x' FROM 'xxxbarxxx');
            -> 'bar'

    mysql> SELECT TRIM(TRAILING 'xyz' FROM 'barxxyz');
            -> 'barx'   
```

更多函数：https://dev.mysql.com/doc/refman/5.7/en/functions.html



当然，MySQL中也支持让你去自定义函数。

### 2 创建函数

```sql
delimiter $$
create function f1(
    i1 int,
    i2 int)
returns int
BEGIN
    declare num int;
    declare maxId int;
    select max(id) from big into maxId;
    
    set num = i1 + i2 + maxId;
    return(num);
END $$
delimiter ;
```

### 3 执行函数

```sql
select f1(11,22);

select f1(11,id),name from d1;
```

### 4 删除函数

```sql
drop function f1;
```



## 8 存储过程

存储过程，是一个存储在MySQL中的SQL语句集合，当主动去调用存储过程时，其中内部的SQL语句会按照逻辑执行。

![image-20210531174813902](mysql.assets/image-20210531174813902.png)

### 1 创建存储过程

```sql
delimiter $$
create procedure p1()
BEGIN
    select * from d1;
END $$
delimiter ;
```

### 2 执行存储过程

```sql
call p1();
```

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import pymysql

conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='root123', db='userdb')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
# 执行存储过程
cursor.callproc('p1')
result = cursor.fetchall()

cursor.close()
conn.close()

print(result)
```

### 3 删除存储过程

```sql
drop procedure proc_name;
```



### 4 参数类型

存储过程的参数可以有如下三种：

- in，仅用于传入参数用
- out，仅用于返回值用
- inout，既可以传入又可以当作返回值

```sql
delimiter $$
create procedure p2(
    in i1 int,
    in i2 int,
    inout i3 int,
    out r1 int
)
BEGIN
    DECLARE temp1 int;
    DECLARE temp2 int default 0;
    
    set temp1 = 1;

    set r1 = i1 + i2 + temp1 + temp2;
    
    set i3 = i3 + 100;

end $$
delimiter ;
```

```sql
set @t1 =4;
set @t2 = 0;
CALL p2 (1, 2 ,@t1, @t2);
SELECT @t1,@t2;
```

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import pymysql

conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='root123', db='userdb')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)

# 执行存储过程
cursor.callproc('p2',args=(1, 22, 3, 4))

# 获取执行完存储的参数
cursor.execute("select @_p2_0,@_p2_1,@_p2_2,@_p2_3")
result = cursor.fetchall()
# {"@_p2_0":11 }

cursor.close()
conn.close()

print(result)
```



### 5 返回值 & 结果集

```sql
delimiter $$
create procedure p3(
    in n1 int,
    inout n2 int,
    out n3 int
)
begin
    set n2 = n1 + 100;
    set n3 = n2 + n1 + 100;
    select * from d1;
end $$
delimiter ;
```

```sql
set @t1 =4;
set @t2 = 0;
CALL p3 (1,@t1, @t2);
SELECT @t1,@t2;
```

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import pymysql

conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='root123', db='userdb')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
# 执行存储过程
cursor.callproc('p3',args=(22, 3, 4))
table = cursor.fetchall() # 得到执行存储过中的结果集

# 获取执行完存储的参数
cursor.execute("select @_p3_0,@_p3_1,@_p3_2")
rets = cursor.fetchall()

cursor.close()
conn.close()

print(table)
print(rets)
```



### 6 事务 & 异常

事务，成功都成功，失败都失败。

```sql
delimiter $$
create PROCEDURE p4(
    OUT p_return_code tinyint
)
BEGIN 
  DECLARE exit handler for sqlexception 
  BEGIN 
    -- ERROR 
    set p_return_code = 1; 
    rollback; 
  END; 
 
  DECLARE exit handler for sqlwarning 
  BEGIN 
    -- WARNING 
    set p_return_code = 2; 
    rollback; 
  END; 
 
  START TRANSACTION;  -- 开启事务
    delete from d1;
    insert into tb(name)values('seven');
  COMMIT;  -- 提交事务
 
  -- SUCCESS 
  set p_return_code = 0; 
 
  END $$
delimiter ; 
```

```sql
set @ret =100;
CALL p4(@ret);
SELECT @ret;
```

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import pymysql

conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='root123', db='userdb')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
# 执行存储过程
cursor.callproc('p4',args=(100))

# 获取执行完存储的参数
cursor.execute("select @_p4_0")
rets = cursor.fetchall()

cursor.close()
conn.close()

print(table)
print(rets)
```



### 7 游标

```sql
delimiter $$
create procedure p5()
begin 
    declare sid int;
    declare sname varchar(50); 
    declare done int default false;


    declare my_cursor CURSOR FOR select id,name from d1;
    
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;
    
    open my_cursor;
        xxoo: LOOP
            fetch my_cursor into sid,sname;
            IF done then 
                leave xxoo;
            END IF;
            insert into t1(name) values(sname);
        end loop xxoo;
    close my_cursor;
end $$
delimiter ; 
```

```sql
call p5();
```



## 9 视图

视图其实是一个虚拟表（非真实存在），其本质是【根据SQL语句获取动态的数据集，并为其命名】，用户使用时只需使用【名称】即可获取结果集，并可以将其当作表来使用。注意：基于视图只能查询，针对视图不能执行 增加、修改、删除。 如果源表发生变化，视图表也会发生变化。

```sql
SELECT
    *
FROM
    (SELECT nid,name FROM tb1 WHERE nid > 2) AS A
WHERE
    A.name > 'alex';
```

### 1 创建视图

```sql
create view v1 as select id,name from d1 where id > 1;
```

### 2 使用视图

```sql
select * from v1;

-- select * from (select id,name from d1 where id > 1) as v1;
```

### 3 删除视图

```sql
drop view v1;
```

### 4 修改视图

```sql
alter view v1 as SQL语句
```





## 10 触发器

![image-20210531181738177](mysql.assets/image-20210531181738177.png)

#### 1 添加触发器

对某个表进行【增/删/改】操作的前后如果希望触发某个特定的行为时，可以使用触发器。

```sql
# 插入前
CREATE TRIGGER tri_before_insert_tb1 BEFORE INSERT ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 插入后
CREATE TRIGGER tri_after_insert_tb1 AFTER INSERT ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 删除前
CREATE TRIGGER tri_before_delete_tb1 BEFORE DELETE ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 删除后
CREATE TRIGGER tri_after_delete_tb1 AFTER DELETE ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 更新前
CREATE TRIGGER tri_before_update_tb1 BEFORE UPDATE ON tb1 FOR EACH ROW
BEGIN
    ...
END

# 更新后
CREATE TRIGGER tri_after_update_tb1 AFTER UPDATE ON tb1 FOR EACH ROW
BEGIN
    ...
END
```

#### 2 删除触发器

```sql
DROP TRIGGER tri_after_insert_tb1;
```

#### 3 示例

- 在 t1 表中插入数据之前，先在 t2 表中插入一行数据。

  ```sql
  delimiter $$
  CREATE TRIGGER tri_before_insert_t1 BEFORE INSERT ON t1 FOR EACH ROW
  BEGIN
  	-- NEW.id  NEW.name  NEW.email
  	-- INSERT INTO t2 (name) VALUES();
  	IF NEW.name = 'alex' THEN
          INSERT INTO t2 (name) VALUES(NEW.id);
      END IF;
  
  END $$
  delimiter ;
  ```

  

  

  ```
  insert into t1(id,name,email)values(1,"alex","xxx@qq.com")
  ```

- 在t1表中删除数据之后，再在t2表中插入一行数据。

  ```sql
  delimiter $$
  CREATE TRIGGER tri_after_insert_t1 AFTER DELETE ON t1 FOR EACH ROW
  BEGIN
  
  IF OLD.name = 'alex' THEN
      INSERT INTO t2 (name) VALUES(OLD.id);
  END IF;
  
  END $$
  delimiter ;
  ```

特别的：NEW表示新数据，OLD表示原来的数据。



































## 11 Pymysql

无论通过何种方式去连接MySQL，本质上发送的 **指令** 都是相同的，只是连接的方式和操作形式不同而已。

当连接上MySQL之后，执行如下指令，就可以对MySQL的数据进行操作。（同上述过程）

想要使用Python操作MySQL需要安装第三方模块：

```python
pip3 install pymysql
```

安装完成后，就可以编写代码：

```python
import pymysql

# 连接MySQL：pymysql.connect创建连接 host=ip，port=端口，user=用户名，passwd=密码，charset=编码，db=数据库名
conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='666', charset="utf8", db='blog')
cursor = conn.cursor()  # 创建游标

# 发送指令
cursor.execute("这里放指令") # 发送
conn.commit()


# 查询
cursor.execute("这里放指令") # 发送
data = cursor.fetchone()  # 接收一行
print(data)


# 关闭连接
cursor.close()
conn.close()
```

## 12 事务

`事务，解决批量操作同时成功或失败的问题。`

innodb引擎中支持事务，myisam不支持

例如：李杰 给 武沛齐 转账 100，那就会涉及2个步骤。

- 李杰账户 减100
- 武沛齐账户 加 100

这两个步骤必须同时完成才算完成，并且如果第一个完成、第二步失败，还是回滚到初始状态。

事务，就是来解决这种情况的。  大白话：要成功都成功；要失败都失败。



### 事务的的四大特性（ACID）

- 原子性（Atomicity）

  ```
  原子性是指事务包含的所有操作不可分割，要么全部成功，要么全部失败回滚。
  ```

- 一致性（Consistency）

  ```
  执行的前后数据的完整性保持一致。
  ```

- 隔离性（Isolation）

  ```
  一个事务执行的过程中,不应该受到其他事务的干扰。
  ```

- 持久性（Durability）

  ```
  事务一旦结束,数据就持久到数据库
  ```



### MySQL客户端事务指令

 **开启事务**

```sql
begin;            -- 或
start transaction;
```

开启事务后做执行操作，操作都完成后在执行提交事务

**提交（结束）事务**

```sql
commit; 
```

**事务回滚（回到原来的状态）**

```sql
rollback;
```

**示例**

```sql
mysql> select * from users;
+----+---------+---------+
| id | name    | amount  |
+----+---------+---------+
|  1 | wupeiqi |    5    |
|  2 |  alex   |    6    |
+----+---------+---------+
3 rows in set (0.00 sec)

mysql> begin;  -- 开启事务 start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> update users set amount=amount-2 where id=1;   -- 执行操作
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update users set amount=amount+2 where id=2;   -- 执行操作
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> commit;  -- 提交事务  rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from users;
+----+---------+---------+
| id | name    | amount  |
+----+---------+---------+
|  1 | wupeiqi |    3    |
|  2 |  ale x  |    8    |
+----+---------+---------+
3 rows in set (0.00 sec)
```

```sql
mysql> select * from users;
+----+---------+---------+
| id | name    | amount  |
+----+---------+---------+
|  1 | wupeiqi |    3    |
|  2 |  ale x  |    8    |
+----+---------+---------+
3 rows in set (0.00 sec)

mysql> begin; -- 开启事务
Query OK, 0 rows affected (0.00 sec)

mysql> update users set amount=amount-2 where id=1; -- 执行操作（此时数据库中的值已修改）
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> rollback; -- 事务回滚（回到原来的状态）
Query OK, 0 rows affected (0.00 sec)

mysql> select * from users;
+----+---------+---------+
| id | name    | amount  |
+----+---------+---------+
|  1 | wupeiqi |    3    |
|  2 |  ale x  |    8    |
+----+---------+---------+
3 rows in set (0.00 sec)
```



### Python事务代码

```python
import pymysql

conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='root123', charset="utf8", db='userdb')
cursor = conn.cursor()

# 开启事务
conn.begin()

try:
    cursor.execute("update users set amount=1 where id=1")
    cursor.execute("update tran set amount=2 where id=2")
    
except Exception as e:
    print("回滚")
    conn.rollback()
else:
    print("提交")
    conn.commit()

cursor.close()
conn.close()
```





## 13 锁

`锁，解决并发处理的问题。`

MySQL中自带了锁的功能，可以帮助我们实现开发过程中遇到的同时处理数据的情况。对于数据库中的锁，从锁的范围来讲有：

- 表级锁，即A操作表时，其他人对整个表都不能操作，等待A操作完之后，才能继续。
- 行级锁，即A操作表时，其他人对指定的行数据不能操作，其他行可以操作，等待A操作完之后，才能继续。

```sql
MYISAM支持表锁，不支持行锁；
InnoDB引擎支持行锁和表锁。

即：在MYISAM下如果要加锁，无论怎么加都会是表锁。
    在InnoDB引擎支持下如果是基于索引查询的数据则是行级锁，否则就是表锁。
所以，一般情况下我们会选择使用innodb引擎，并且在 搜索 时也会使用索引（命中索引）。
```

接下来的操作就基于innodb引擎来操作：

```sql
CREATE TABLE `L1` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `count` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8;
```

![image-20210528134811202](mysql.assets/image-20210528134811202.png)



在innodb引擎中，update、insert、delete的行为内部都会先申请锁（排它锁），申请到之后才执行相关操作，最后再释放锁。

```
所以，当多个人同时像数据库执行：insert、update、delete等操作时，内部加锁后会排队逐一执行。
```

而select则默认不会申请锁。

```
select * from xxx;
```

如果，你想要让select去申请锁，则需要配合 事务 + 特殊语法来实现。

- `for update`，排它锁，加锁之后，其他不可以读写。

  ```sql
  begin; 
  	select * from L1 where name="武沛齐" for update;    -- name列不是索引（表锁）
  commit;
  ```

  ```sql
  begin; -- 或者 start transaction;
  	select * from L1 where id=1 for update;			  -- id列是索引（行锁）
  commit;
  ```

- `lock in share mode` ，共享锁，加锁之后，其他可读但不可写。

  ```sql
  begin; 
  	select * from L1 where name="武沛齐" lock in share mode;    -- 假设name列不是索引（表锁）
  commit;
  ```

  ```sql
  begin; -- 或者 start transaction;
  	select * from L1 where id=1 lock in share mode;           -- id列是索引（行锁）
  commit;
  ```



###  排它锁 

排它锁（ `for update`），加锁之后，其他事务不可以读写。

应用场景：总共100件商品，每次购买一件需要让商品个数减1 。

```sql
A: 访问页面查看商品剩余 100
B: 访问页面查看商品剩余 100

此时 A、B 同时下单，那么他们同时执行SQL：
	update goods set count=count-1 where id=3
由于Innodb引擎内部会加锁，所以他们两个即使同一时刻执行，内部也会排序逐步执行。


但是，当商品剩余 1个时，就需要注意了。
A: 访问页面查看商品剩余 1
B: 访问页面查看商品剩余 1

此时 A、B 同时下单，那么他们同时执行SQL：
	update goods set count=count-1 where id=3
这样剩余数量就会出现 -1，很显然这是不正确的，所以应该怎么办呢？


这种情况下，可以利用 排它锁，在更新之前先查询剩余数量，只有数量 >0 才可以购买，所以，下单时应该执行：
	begin; -- start transaction;
	select count from goods where id=3 for update;
	-- 获取个数进行判断
	if 个数>0:
		update goods set count=count-1 where id=3;
	else:
		-- 已售罄
	commit;
```

基于Python代码示例：

```python
import pymysql
import threading


def task():
    conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='root123', charset="utf8", db='userdb')
    cursor = conn.cursor(pymysql.cursors.DictCursor)  # 获取游标，获取的数据是字典
    # cursor = conn.cursor()
	
    # 开启事务
    conn.begin()

    cursor.execute("select id,age from tran where id=2 for update")
    # fetchall      ( {"id":1,"age":10},{"id":2,"age":10}, )   ((1,10),(2,10))
    # {"id":1,"age":10}   (1,10)
    result = cursor.fetchone()
    current_age = result['age']
    
    if current_age > 0:
        cursor.execute("update tran set age=age-1 where id=2")
    else:
        print("已售罄")

    conn.commit()

    cursor.close()
    conn.close()


def run():
    for i in range(5):
        t = threading.Thread(target=task)
        t.start()


if __name__ == '__main__':
    run()

```



### 共享锁

共享锁（ `lock in share mode`），可以读，但不允许写。

加锁之后，后续其他事物可以可以进行读，但不允许写（update、delete、insert），因为写的默认也会加锁。



**Locking Read Examples**

Suppose that you want to insert a new row into a table `child`, and make sure that the child row has a parent row in table `parent`. Your application code can ensure referential integrity throughout this sequence of operations.

First, use a consistent read to query the table `PARENT` and verify that the parent row exists. Can you safely insert the child row to table `CHILD`? No, because some other session could delete the parent row in the moment between your `SELECT` and your `INSERT`, without you being aware of it.

To avoid this potential issue, perform the [`SELECT`](https://dev.mysql.com/doc/refman/5.7/en/select.html) using `LOCK IN SHARE MODE`:

```sql
SELECT * FROM parent WHERE NAME = 'Jones' LOCK IN SHARE MODE;
```

After the `LOCK IN SHARE MODE` query returns the parent `'Jones'`, you can safely add the child record to the `CHILD` table and commit the transaction. Any transaction that tries to acquire an exclusive lock in the applicable row in the `PARENT` table waits until you are finished, that is, until the data in all tables is in a consistent state.



## 14 数据库连接池

![image-20210531211656410](mysql.assets/image-20210531211656410.png)

`数据库连接池，解决多个人请求连接数据库的问题。`

过多线程时使用线程池

```
pip3.9 install pymysql
pip3.9 install dbutils
```

```python
import threading
import pymysql
from dbutils.pooled_db import PooledDB

MYSQL_DB_POOL = PooledDB(
    creator=pymysql,  # 使用链接数据库的模块
    maxconnections=5,  # 连接池允许的最大连接数，0和None表示不限制连接数
    mincached=2,  # 初始化时，链接池中至少创建的空闲的链接，0表示不创建
    maxcached=3,  # 链接池中最多闲置的链接，0和None不限制
    blocking=True,  # 连接池中如果没有可用连接后，是否阻塞等待。True，等待；False，不等待然后报错
    setsession=[],  # 开始会话前执行的命令列表。如：["set datestyle to ...", "set time zone ..."]
    ping=0,
    # ping MySQL服务端，检查是否服务可用。
    # 如：0 = None = never, 1 = default = whenever it is requested, 
    # 2 = when a cursor is created, 4 = when a query is executed, 7 = always
    host='127.0.0.1',
    port=3306,
    user='root',
    password='root123',
    database='userdb',
    charset='utf8'
)


def task():
    # 去连接池获取一个连接
    conn = MYSQL_DB_POOL.connection()
    cursor = conn.cursor(pymysql.cursors.DictCursor)
    
    cursor.execute('select sleep(2)')
    result = cursor.fetchall()
    print(result)

    cursor.close()
    # 将连接交换给连接池
    conn.close()

def run():
    for i in range(10):
        t = threading.Thread(target=task)
        t.start()


if __name__ == '__main__':
    run()

```



## 15 SQL工具类

`SQL工具类，解决连接数据库代码重复的问题`。

基于数据库连接池开发一个公共的SQL操作类，方便以后操作数据库。

#### 1 单例和方法

```sql
# db.py
import pymysql
from dbutils.pooled_db import PooledDB


class DBHelper(object):

    def __init__(self):
        # TODO 此处配置，可以去配置文件中读取。
        self.pool = PooledDB(
            creator=pymysql,  # 使用链接数据库的模块
            maxconnections=5,  # 连接池允许的最大连接数，0和None表示不限制连接数
            mincached=2,  # 初始化时，链接池中至少创建的空闲的链接，0表示不创建
            maxcached=3,  # 链接池中最多闲置的链接，0和None不限制
            blocking=True,  # 连接池中如果没有可用连接后，是否阻塞等待。True，等待；False，不等待然后报错
            setsession=[],  # 开始会话前执行的命令列表。如：["set datestyle to ...", "set time zone ..."]
            ping=0,
            # ping MySQL服务端，检查是否服务可用。# 如：0 = None = never, 1 = default = whenever it is requested, 2 = when a cursor is created, 4 = when a query is executed, 7 = always
            host='127.0.0.1',
            port=3306,
            user='root',
            password='root123',
            database='userdb',
            charset='utf8'
        )

    def get_conn_cursor(self):
        conn = self.pool.connection()
        cursor = conn.cursor(pymysql.cursors.DictCursor)
        return conn, cursor

    def close_conn_cursor(self, *args):
        for item in args:
            item.close()

    def exec(self, sql, **kwargs):
        conn, cursor = self.get_conn_cursor()

        cursor.execute(sql, kwargs)
        conn.commit()

        self.close_conn_cursor(conn, cursor)

    def fetch_one(self, sql, **kwargs):
        conn, cursor = self.get_conn_cursor()

        cursor.execute(sql, kwargs)
        result = cursor.fetchone()

        self.close_conn_cursor(conn, cursor)
        return result

    def fetch_all(self, sql, **kwargs):
        conn, cursor = self.get_conn_cursor()

        cursor.execute(sql, kwargs)
        result = cursor.fetchall()

        self.close_conn_cursor(conn, cursor)

        return result


db = DBHelper()

```

```sql
from db import db

db.exec("insert into d1(name) values(%(name)s)", name="武沛齐666")

ret = db.fetch_one("select * from d1")
print(ret)

    ret = db.fetch_one("select * from d1 where id=%(nid)s", nid=3)
    print(ret)

ret = db.fetch_all("select * from d1")
print(ret)

ret = db.fetch_all("select * from d1 where id>%(nid)s", nid=2)
print(ret)

```



#### 2 上下文管理

如果你想要让他也支持 with 上下文管理。

```
with 获取连接：
	执行SQL（执行完毕后，自动将连接交还给连接池）

```



```python
 	# db_context.py
import threading
import pymysql
from dbutils.pooled_db import PooledDB

POOL = PooledDB(
    creator=pymysql,  # 使用链接数据库的模块
    maxconnections=5,  # 连接池允许的最大连接数，0和None表示不限制连接数
    mincached=2,  # 初始化时，链接池中至少创建的空闲的链接，0表示不创建
    maxcached=3,  # 链接池中最多闲置的链接，0和None不限制
    blocking=True,  # 连接池中如果没有可用连接后，是否阻塞等待。True，等待；False，不等待然后报错
    setsession=[],  # 开始会话前执行的命令列表。如：["set datestyle to ...", "set time zone ..."]
    ping=0,
    host='127.0.0.1',
    port=3306,
    user='root',
    password='root123',
    database='userdb',
    charset='utf8'
)


class Connect(object):
    def __init__(self):
        self.conn = conn = POOL.connection()
        self.cursor = conn.cursor(pymysql.cursors.DictCursor)

    def __enter__(self):
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.cursor.close()
        self.conn.close()

    def exec(self, sql, **kwargs):
        self.cursor.execute(sql, kwargs)
        self.conn.commit()

    def fetch_one(self, sql, **kwargs):
        self.cursor.execute(sql, kwargs)
        result = self.cursor.fetchone()
        return result

    def fetch_all(self, sql, **kwargs):
        self.cursor.execute(sql, kwargs)
        result = self.cursor.fetchall()
        return result

```

```python
from db_context import Connect

with Connect() as obj:
    # print(obj.conn)
    # print(obj.cursor)
    ret = obj.fetch_one("select * from d1")
    print(ret)

    ret = obj.fetch_one("select * from d1 where id=%(id)s", id=3)
    print(ret)

```



## 16 授权

之前我们无论是基于Python代码 or 自带客户端 去连接MySQL时，均使用的是 **root** 账户，拥有对MySQL数据库操作的所有权限。

如果有多个程序的数据库都放在同一个MySQL中，如果程序都用root账户就存在风险了。

**这种情况怎么办呢？**

在MySQL中支持创建账户，并给账户分配权限，例如：只拥有数据库A操作的权限、只拥有数据库B中某些表的权限、只拥有数据库B中某些表的读权限等。



### 1 用户管理

在MySQL的默认数据库 `mysql` 中的 `user` 表中存储着所有的账户信息（含账户、权限等）。

```sql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| day26              |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
10 rows in set (0.00 sec)
# 表mysql=.user下放着用户账户，user=账号名 authentication_string=密码  host=指定连接的ip,localhost是本机

mysql> select user,authentication_string,host from  mysql.user; 
+----------------------------------+-------------------------------------------+-------------------------------+
| user                             | authentication_string                     | host                          |
+----------------------------------+-------------------------------------------+-------------------------------+
| root                             | *FAAFFE644E901CFAFAEC7562415E5FAEC243B8B2 | localhost                     |
| mysql.session                    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | localhost                     |
| mysql.sys                        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | localhost                     |
+----------------------------------+-------------------------------------------+-------------------------------+
3 rows in set (0.00 sec)
```



创建和删除用户

```
create user '用户名'@'连接者的IP地址' identified by '密码';
```

```sql
# 账户名和密码可用'引号'也可不用，但是用了通配符就要加，尽量统一都加
# 创建账户
create user wupeiqi1@127.0.0.1 identified by 'root123';

# 删除账户
drop user wupeiqi1@127.0.0.1;

# 百分号%代表0-9
create user wupeiqi2@'127.0.0.%' identified by 'root123';
drop user wupeiqi2@'127.0.0.%';

create user wupeiqi3@'%' identified by 'root123';
drop user wupeiqi3@'%';

create user 'wupeiqi4'@'%' identified by 'root123';
drop user 'wupeiqi4'@'%';
```

修改用户

```
rename user '用户名'@'IP地址' to '新用户名'@'IP地址';
```

```sql
rename user wupeiqi1@127.0.0.1 to wupeiqi1@localhost;

rename user 'wupeiqi1'@'127.0.0.1' to 'wupeiqi1'@'localhost';
```

修改密码

```
set password for '用户名'@'IP地址' = Password('新密码')
```

```sql
set password for 'wupeiqi4'@'%' = Password('123123');
```

### 2 授权管理

创建好用户之后，就可以为用户进行授权了。

授权

```
grant 权限 on 数据库.表 to   '用户'@'IP地址'
```

```sql
grant all privileges on *.* TO 'luffy'@'127.0.0.1';         -- 用户wupeiqi拥有所有数据库的所有权限
grant all privileges on day26.* TO 'wupeiqi'@'localhost';     -- 用户wupeiqi拥有数据库day26的所有权限
grant all privileges on day26.info TO 'wupeiqi'@'localhost';  -- 用户wupeiqi拥有数据库day26中info表的所有权限

grant select on day26.info TO 'wupeiqi'@'localhost';          -- 用户wupeiqi拥有数据库day26中info表的查询权限
grant select,insert on day26.* TO 'wupeiqi'@'localhost';      -- 用户wupeiqi拥有数据库day26所有表的查询和插入权限

grant all privileges on day26db.* To 'wupeiqi4'@'%';


注意：flush privileges;   -- 将数据读取到内存中，从而立即生效。
```

对于权限

```
all privileges  除grant外的所有权限
select          仅查权限
select,insert   查和插入权限
...
usage                   无访问权限
alter                   使用alter table
alter routine           使用alter procedure和drop procedure
create                  使用create table
create routine          使用create procedure
create temporary tables 使用create temporary tables
create user             使用create user、drop user、rename user和revoke  all privileges
create view             使用create view
delete                  使用delete
drop                    使用drop table
execute                 使用call和存储过程
file                    使用select into outfile 和 load data infile
grant option            使用grant 和 revoke
index                   使用index
insert                  使用insert
lock tables             使用lock table
process                 使用show full processlist
select                  使用select
show databases          使用show databases
show view               使用show view
update                  使用update
reload                  使用flush
shutdown                使用mysqladmin shutdown(关闭MySQL)
super                   􏱂􏰈使用change master、kill、logs、purge、master和set global。还允许mysqladmin􏵗􏵘􏲊􏲋调试登陆
replication client      服务器位置的访问
replication slave       由复制从属使用
```

对于数据库和表

```
数据库名.*            数据库中的所有
数据库名.表名          指定数据库中的某张表
数据库名.存储过程名     指定数据库中的存储过程
*.*                  所有数据库
```

查看授权

```
show grants for '用户'@'IP地址'
```

```sql
show grants for 'wupeiqi'@'localhost';
show grants for 'wupeiqi4'@'%';
```

取消授权

```
revoke 权限 on 数据库.表 from '用户'@'IP地址'
```

```sql
revoke ALL PRIVILEGES on day26.* from 'wupeiqi'@'localhost';

revoke ALL PRIVILEGES on day26db.* from 'wupeiqi4'@'%';
注意：flush privileges;   -- 将数据读取到内存中，从而立即生效。
```




一般情况下，在很多的 正规 公司，数据库都是由 DBA 来统一进行管理，DBA为每个项目的数据库创建用户，并赋予相关的权限。





##  其他

### `navicat`可视化`mysql`

navicat，是一个桌面应用，让我们可以更加方便的管理MySQL数据库。

- mac系统：https://www.macdo.cn/17030.html
- win系统：
  - 链接: https://pan.baidu.com/s/13cjbrBquz9vjVqKgWoCQ1w  密码: qstp
  - 链接: https://pan.baidu.com/s/1JULIIwQA5s0qN98KP8UXHA  密码: p18f

###  关于`SQL`注入

假如，你开发了一个用户认证的系统，应该用户登录成功后才能正确的返回相应的用户结果。 

如果用户在输入user时，输入了：   ` ' or 1=1 --   `    ，这样即使用户输入的密码不存在，也会可以通过验证。

**为什么呢？**

因为在SQL拼接时，拼接后的结果是：

```
select * from users where name='' or 1=1 -- ' and password='123'
```

注意：在MySQL中 `--` 表示注释。



**那么，在Python开发中 如何来避免SQL注入呢？**

切记，SQL语句不要在使用python的字符串格式化，而是使用pymysql的execute方法。	

```sql
import pymysql

# 输入用户名和密码
user = input("请输入用户名：")
pwd = input("请输入密码：")

conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='root123', charset="utf8", db='userdb')
cursor = conn.cursor()

cursor.execute("select * from users where name=%s and password=%s", [user, pwd])
# 或
cursor.execute("select * from users where name=%(n1)s and password=%(n2)s", {"n1": user, 'n2': pwd})

result = cursor.fetchone()
print(result)

cursor.close()
conn.close()
```









### 其他指令

```sql
\c  -- 终结指令
```

