# XSS跨站

- xss就是用户输入的传参会被当做前端代码执行

1. XSS可以做什么

   - 获取cookie   (不能跨域名，跨端口，跨IP)   获取cookie的代码只会在一个站点上获取，其他站点上的cookie无法获取
   - 获取内网IP
   - 获取浏览器保存的明文密码
   - 截取网页屏幕
   - 网页上的键盘记录

2. XSS种类

   - 反射性xss   你提交的数据支队本次访问产生了影响
   - 存储型xss   提交的数据存入了数据库，别人访问这个页面的时候就会自动获取数据
   - DOM型xss    基于文档对象模型Document Object Model的一种漏洞,DOM是一个与平台、编程无关的接口,允许脚本动态的访问和更新文档内容结构样式(原本不应该出现xss的地方，但是经过JavaScript的操作之后产生了xss)

3. 除法XSS的3种方法

   1. 标签触发

   ```javascript
   <script>alert(123)</script>
   <hr />
   <h1>123</h1>
   ```

   2. 伪协议

   >     不同于网络上真实存在的协议如：http://  https://  ftp://

   >     伪协议只有关联应用能够用 如：php://   tencent://(关联qq)

   >     javascript: 声明url的主体是任意javascript代码  如：javascript:alert(1)

   >     js容错率高   哪里能用执行哪里    单引号(')可以闭合双引号(")

   3. 事件触发方法

   >     <img src = "C:/Users/30352/Desktop/a" onerror = alert(1)>             这是在路径不正确的情况下弹框测试

   >     <img src = 'a' onerror = alert(1)//'>          这是在图片名字上进行篡改然后弹框

   >     <input name="keyword" value="" '="">           这是在value里面单独写一个'搞的鬼

   >     <input name="keyword" value="" oninput="alert(1)"//'">    这是在value里面进行双引号闭合(浏览器的特性)

   >     <input name="keyword" value="" onfocus="alert(1) autofocus"//'">

   >     *-+<input name="keyword" value="" onmouseover="alert(1)"//'">

   >     等等诸如此类

## 反射

- 你提交的数据成功实现了XSS，但是仅仅只是对你这次访问产生了影响，是非持久性攻击

## 存储

- 提交的数据存入了数据库，别人访问这个页面的时候就会继续执行恶意代码

## DOM

- js中会把+变成p  也就是<scri+t>  =>  <script>
 - dom的操作

1. Document的操作 => js操作
   1. document.cookie
   2. document.body
   3. document.domain          返回当前文档的域名
   4. document.lastModified    (判断页面是否是动态还是静态,动态页面打印出来的数据是会不断变化的,而静态是不会发生改变的)
   5. document.referrer        返回载入当前文档的文档url
   6. document.title           返回当前文档的标题
   7. document.url             返回当前文档的url
2. Document对象方法
   1. document.write()         打印数据    -->   js语句    会解析某些编码(native编码)
      document.write('<script>alert(1)</script>') 把里面的js语句转化成native编码才可以
      document.write('\u003c\u0073\u0063\u0072\u0069\u0070\u0074\u003e\u0061\u006c\u0065\u0072\u0074\u0028\u0031\u0029\u003c\u002f\u0073\u0063\u0072\u0069\u0070\u0074\u003e')    就可以弹窗了
      在做xss时候 被拦截了那么是不是可以通过js代码的解码功能进行绕过

- document.write()



- innerHTML



- eval()