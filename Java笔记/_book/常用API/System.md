## System

| 方法                       | 说明                                            | 案例                                                         |
| -------------------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| System.exit(int num)       | 退出java虚拟机<br>int后面的额变量标识退出字符码 | System.exit(0);                                              |
| System.currentTimeMillis() | 返回从1970.1.1与现在的时间差（毫秒）            | System.out.println(System.currentTimeMillis() * 1.0 / 1000 / 60 / 60 / 24 / 365); |

```java
long start = System.currentTimeMillis();
for (int i = 0; i < 10000; i ++){
    System.out.println(i);
}
long end = System.currentTimeMillis();
System.out.println("共消耗 ： " + (end - start) + "毫秒");
```
