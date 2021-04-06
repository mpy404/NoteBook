# 代码分析

```
<?php
    $id = base64_decode($_GET['id']);
    $con = mysqli_connect("localhostt", "root", "root");
    mysql_select_db("sql", $con);
    $sql = "select * from users where id = $id";
    $result = mysql_query($sql);
    while($row = mysqli_fetch_array($result)){
        echo "ID : " . $row['id'] . "<br>";
        echo "Name : " . $row['username'] . "<br>";
        echo "PassWd : " . $row['passwd'] . "<br>";
        echo "<hr>";
    }
    mysql_close($con);
    echo "now use" . $sql . "<hr>";
?>
```

 - 程序获取GET传参的ID，利用`base64_decode()`函数对参数进行base64解码，然后将解码后的$id拼接到select查询语句中进行查询，通过while循环将查询结果输出到页面
 - 由于代码没有对解码后SQL语句无任何过滤，当访问`id=1 union select 1,2,3#`【访问时，先进性base64加密】，此时的SQL语句为`select * from users where id=1`和`union select 1,2,3#`
 - 可以尝试绕过WAF【对传参进行base64编码】