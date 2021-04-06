
查询出所有的表

```
select * from all_tables 
```

查询出当前用户的表

```
select * from user_tables 
```

查询出所有的字段

```
select*from all_tab_columns 
```

查询出当前用户的字段

```
select*from user_tab_columns  
```

查版本

```
select*from v$version 
```

查询第一行

```
select * from all_tables where rownum=1
```

查询多行，参考实现limit的功能的	

实现limit的功能

  1. rownum输出

 ```
 select * from all_tables where rownum=1; // 输出一行;
 select * from all_tables where rownum<3; // 输出两行
 select * from all_tables where rownum<n; // 输出n-1行
 ```

  2. 查询结果去掉没用的

 ```
select password from admin where password<>'asd123';
 select password from admin where password<>'asd123' and password<>'zxc12312ws';
 ```

  3. 基于行数别名的子查询

 ```
查询admin表中的username字段，并在字段前面加上行号，想要利用行号就必须得取个别名，不然会和外面查询的rownum冲突 : 
select rownum as rr, username from admin;
select username from (select rownum as rr, username from admin) where rr = 1;
想要改变行数只需要改变行号就可以了 : 
select username from (select rownum as rr, username from admin) where rr = 2;
 ```