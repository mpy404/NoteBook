- 通过$_SERVER获取的数据未经过任何处理，直接插入数据库，从而形成head注入，获取数据之后就会插入数据库，所以不会有回显，显错注入无效，只能盲注或报错注入
- 常见的容易出Head注入的地方

### Cookie

```
$_Cookie['id'] 获取用户的cookie信息，无任何过滤
```

### user_agent

```php
$_SERVER['HTTP_USER_ADENT']  获取用户相关信息、包括用户浏览器、操作系统等信息
```

### referer

```php
$_SERVER['HTTP_REFERER']  获取Referer请求头数据
```

### x-forwarded-for

```php
$_SERVER['REMOTE_ADDR']   获取浏览网页的用户IP
```

### host

```php
$_SERVER['HTTP_HOST']  请求头信息中的Host内容，获取当前域名
```

- 案例

```mysql
这是一个MySQL插入语句：
insert into ugaent ('useragent', 'username') values ($agent, $user);
因为 $agent 是直接通过 $_SERVER['HTTP_USER_ADENT'] 获取，没有任何防护
'' or updatexml(1,concat(ox7e, (select database())),1),1)#    
后面的 ,1 是因为前面插入了两个数据，这里也需要两个数据来保持一致
```