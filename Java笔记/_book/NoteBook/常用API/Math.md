## Math

| 方法                         | 说明                                           | 案例                                                         |
| ---------------------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| Math.abs(int a)              | 返回参数的绝对值                               | System.out.println(Math.abs(12));<br>System.out.println(Math.abs(-1)); |
| Math.ceil(double a)          | 返回大于或等于参数的最小double值，等于一个整数 | System.out.println(Math.ceil(12.34));<br>System.out.println(Math.ceil(12.56)); |
| Math.floor(double a)         | 返回小于或等于参数的最小double值，等于一个整数 | System.out.println(Math.floor(12.34));<br/>System.out.println(Math.floor(12.56)); |
| Math.round(float a)          | 按照四舍五入返回最接近参数的int                | System.out.println(Math.round(12.34L));<br/>System.out.println(Math.round(12.56L)); |
| Math.max(int a, int b)       | 返回两个int数中最大的那个                      | System.out.println(Math.max(1, 3));                          |
| Math.min(int a, int b)       | 返回两个int数中最小的那个                      | System.out.println(Math.min(1, 2));                          |
| Math.pow(double a, double b) | 返回a的b次幂的值                               | System.out.println(Math.pow(2.0, 3.0));                      |
| Math.random()                | 返回值为double的正值                           | System.out.println(Math.random());<br>System.out.println((int)(Math.random()*100) + 1) // 1-100的随机数 |
