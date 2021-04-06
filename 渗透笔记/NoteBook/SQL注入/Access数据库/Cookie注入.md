## Cookie注入

- 什么是Cookie
  - Cookie就是代表身份的一串字符串，网站根据Cookie来识别你是谁，如果你获取了管理员的Cookie，无需密码就可以登录管理员帐号
- 什么是Cookie注入
  - 开发的偷懒，无论什么数据都用$_REQUEST来获取，这就有可能忽略了对Cookie传参的检测，也可以通过这个绕过waf
    - 注意：php5.4以上的版本就不会接受Cookie传参了

### 流程

1. 尝试cookie传入参数和值是否可以运行
2. 猜字段数（order by）
3. 猜表名
4. 猜字段（字段名）

### 方法

#### 插件修改

- EditThisCookie
  - 通过“+”来添加cookie字段（可能get传参有waf拦截）
  - 修改数据来进行注入

#### JS修改

- document.cookie="参数"+escape("值")

#### sqlmap跑

>python3 sqlmap.py -u "http://127.0.0.1/1.asp" --cookie "id=1" --level 2