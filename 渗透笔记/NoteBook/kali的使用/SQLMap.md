# 跑数据

## 指定目标


> -u : 指定URL

> -m : 把URL保存在文件中，SQLMap回一个一个进行检测


## 数据库版本号

> --banner | -b : 大多数数据库都有一个返回数据库版本的函数【version() | @@version】


## 用户

> -current-user : 当前用户

> -users : 所有用户

> --is-dba : 当前用户是否为管理员权限

> --privileges : 如果--is-dba是TRUE的话，很可能列举出每个用户的权限

## 系统架构

> --schema : 获取数据库的架构【所有的数据库、数据表、数据字段及各自类型，加上--exclude-sysdbs将不会获取数据库自带的系统内容】

## 跑数据库

> -current-db : 当前数据库

> --dbs : 跑数据库

> -D : 指定数据库

## 跑数据表

> --tables : 跑数据表

> -T : 指定数据表

> --common-tables : 如果--tables没有数据表显示，可用该参数暴力破解数据表【指定字典】

## 跑数据字段

> --columns : 跑数据字段

> -C : 指定字段

> --common-columns : 如果--columns没有数据表显示，可用该参数暴力破解数据字段【指定字典】

## 跑全部数据


> --dump : 枚举数据

> --passwords : 列出并进行破解密码【MD5加密】

> --count : 获取数据个数不会获取其中的内容


## 请求方式

### GET请求


> -u : 默认请求时GET

```
python3 sqlmap.py -u "http://192.168.31.250"
```

### POST请求

> --froms : 自动搜索表单信息

> --data : 把数据以POST方式进行提交

```
python3 sqlmap.py -u "http://192.168.31.250" --data "id=1&ns=1"
```

### COOKIE请求


> --cookie : cookie请求

```
python3 sqlmap.py -u "http://192.168.31.250" –cookie "id=11" –level 2（只有level达到2才会检测cookie）
```

## HTTP请求头设置
### User-agent头


> --user-agent : 指定user-agent请求头

> --random-agent : 选择随机的user-agent请求头

> --mobile : 模拟一个手机的user-agent请求头


### Host头


> --host : 指定Host请求头

### Referer头


> --referer : 指定Referer请求头


### 其他请求头


> --headers : 通过该参数来添加额外的HTTP头


### 请求延迟


> --delay : 每次请求延迟


### 超时设置


> --timeout : 请求多久判为延迟【默认10秒】


### 代理设置

> --proxy : 使用本地端口进行代理【--porxy "http://127.0.0.1:8080" : 】


# 常见的其他指令

## 指定文件


> -r : burp抓取到数据包，在疑似有问题的传参数据后加上"*"

> 如 : username=admin&password=123*

> -p : 需要配合-r，达到指定参数的效果

> python3 sqlmap.py -r 1.txt -p 参数名


## 文件操作


> --file-read : 读取文件

> --file-write : 编辑文件

> --file-dest : 写入文件


## 数据库操作

> --sql-shell : SQL命令执行

> --sql-query : 指定mysql进行查询

> --sql-file : 从文件中执行mysql语句


## 系统操作
要求：
1. 管理员root
2. 有绝对路径
3. PHP自动转义gpc关闭
4. secrue_file_priv为空 
--os-cmd : 执行操作系统命令
--os-shell : 交互式操作系统的shell