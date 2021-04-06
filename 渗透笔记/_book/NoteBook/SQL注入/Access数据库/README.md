<font size=4 color="red">
注入本质
</font>

> 把用户输入的数据当做代码执行

<font size=4 color="red">
注入条件
</font>

> 第一：用户能够控制输入

> 第二：原本要执行的代码，拼接了用户输入的数据然后进行执行

# Access注入

- Access没有系统自带库
  - 在每个查询语句后面都要带表名
    - 第一种方法是靠强猜一些常用的表名（admin、users、job、news）
    - 第二种方法是利用exists(select * from 常见的表名)，如果有数据会无回显，没有就会报错，通过burp加载字典来查看表名