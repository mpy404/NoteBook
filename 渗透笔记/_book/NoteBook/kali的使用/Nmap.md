# Nmap
<!--TB - top bottom（自上而下）-->
<!--BT - bottom top（自下而上）-->
<!--RL - right left（从右到左）-->
<!--LR - left right（从左到右）-->

## 常见扫描方式

1. 无任何附加参数

> nmap 192.168.31.177
> > 如果是超级用户，无参数扫描相当于是sS扫描<br>
> > 其他用户相当于sT扫描【TCP 完整扫描】

2. 指定端口

> nmap -p 8080 192.168.30.177

3. 系统探测

> nmap -O 192.168.30.177<br>
> nmap -A 192.168.30.177

4. 主机发现

> nmap -sn 192.168.30.177 【只是用ping扫描来发现】

5. 跳过主机发现

> nmap -Pn 192.168.30.177 【穿透防火墙】

6. 扫描和版本号侦测

> nmap -sV 192.168.30.177 【侦测开放的端口来判断开放的服务，并检测对应的版本】

7. UDP扫描

> nmap -sU 192.168.30.177

8. TCP扫描

> nmap -sT 192.168.30.177

9. STCP扫

【通过STCP协议进行扫描主机】
> nmap -PY 192.168.30.177


10. 漏洞扫描

> nmap --script=vuln 192.168.30.177 【使用vuln脚本扫描漏洞】

11. IPV6扫描

> nmap -6 192.168.30.177

12. 路由跟踪
<br/>
【帮助用户了解网络情况，可以查出本地计算机到目标之间所经过的网络节点并可以查看到通过各个节点的时间】

> nmap 192.168.30.177 -traceroute

13. 保存输出

> 标准输出 【txt格式的】
>
> > nmap -oN test.txt

> XML输出【XML格式的】
>
> > nmap -oX test.xml








## 端口扫描

### 端口状态
```mermaid
graph LR
A[端口状态]-->Opend
Opend-->端口开放
A-->Closed
Closed-->端口关闭
A-->Filtered
Filtered-->端口过滤,数据被防火墙拦截
A-->UnFiltered
UnFiltered-->未被过滤,但不能识别端口当前的状态
A-->B[Openfiltered开放或者被过滤]
B-->发生在UDP,IP,FIN,NULL和Xmas扫描中
A-->C[CloseFiltered关闭或者被过滤]
C-->发生在IP,ID,idle扫描
```


```mermaid
graph LR
S[端口扫描]-->S1[-p:指定端口扫描]
S1-->指定一个端口进行扫描
指定一个端口进行扫描-->A[nmap -p 80 192.168.31.12]
S1-->指定多个端口进行扫描
指定多个端口进行扫描-->B[nmap -p 80,88,135 192.168.31.123]
S1-->指定一段端口进行扫描
指定一段端口进行扫描-->C[nmap -p 1-1000 192.168.31.123]
S1-->D[--top-ports默认1000开放最高的TCP端口]
D-->D1[nmap --top-ports 1000 192.168.31.123];
```






## ARP 扫描

```mermaid
graph LR;
S[ARP Ping扫描]-->-PR
-PR-->通常在局域网中扫描,使用地址解析协议,本地局域网不会禁止ARP请求;
```

## ICMP扫描

```mermaid
graph LR;
S[ICMP Ping Types扫描] --> -PE 
-PE--> 使用ICMP扫描方式
使用ICMP扫描方式--> A[通过发送ICMP Echo数据包来探测数据是否存活,在内网中能达到穿透防火墙的效果];
S-->-PP
-PP--> 使用时间戳Ping扫描
使用时间戳Ping扫描--> A;
S-->-PM
-PM--> 使用ICMP地址掩码ping扫描
使用ICMP地址掩码ping扫描--> A;

```

## TCP扫描

```mermaid
graph LR;

SYN扫描 --> -sS 
-sS--> 半开放扫描,速度较快,隐蔽性好
半开放扫描,速度较快,隐蔽性好--> A[nmap -sS 192.168.30.123];
连接扫描 --> -sT
-sT--> 扫描速度快,准确性高,但容易被防火墙发现
扫描速度快,准确性高,但容易被防火墙发现--> B[nmap -sT 192.168.30.123];
ACK扫描 --> -sA
-sA-->A1[用于发现防火墙规则,确定它们是有状态的还是无状态的,哪些端口是被过滤的]
A1-->C[nmap -sA 192.168.30.123];
A11[TCP SYN Ping扫描] --> -PS
-PS--> B11[当防火墙阻止TCP ACK和ICMP Echo请求时可以通过SYNping扫描来判断主机是否存活];
A12[TCP ACK Ping扫描] --> -PA
-PA--> B12[很多防火墙会封锁SYN报文,通过ACKping扫描来判断目标主机是否存活];

```

## UDP扫描

```mermaid
graph LR;
UDP扫描 --> -sU
-sU--> 扫描存在于UDP端口的程序,速度较慢
扫描存在于UDP端口的程序,速度较慢--> A[nmap -sU 192.168.30.123];
UDPping扫描 --> -PU
-PU--> A1[Nmap会发送一个空UDP包到目标主机];
A1 -->主机响应范围一个ICMP端口不可达则主机存货;
A1 --> 主句不存货则返回各种ICMP错误信息;
```

## Ping扫描

```mermaid
graph LR;
Ping扫描 --> -sP 
-sP --> 使用平扫描,然后回显并作出响应的主机,获取目标主机信息而不会被轻易发现
无ping扫描 --> -P0 
-P0 --> A[同于防火墙进制ping的情况下启动高强度扫描,可用于穿透防火墙同时避免防火墙发现]
无ping扫描 --> -Pn
-Pn--> A
```

## 其他扫描

### 域名扫描

```mermaid
graph LR;
列表扫描 --> -sL 
-sL --> 累出指定网络上的每台主机,默认使用域名解析获取他们的名字;
进制反向域名解析 --> -n 
-n --> 不对目标进行反向域名解析;
反向域名解析 --> -R
-R--> 对目标地址进行反向域名解析;
系统域名解析器 --> A1["--system-dns"]
A1--> A[通过直接发行查询到主机上自带配置的域名服务解析域名];
启动IPV6扫描 --> -6;
```

### 指纹识别

```mermaid
graph LR;
端口服务版本探测 --> -sV
-sV--> 通过端口对应处响应的服务器,识别出相对应的版本;
全端口服务探测 --> B1[--allports]
B1-->B[启用全端口版本扫描,会跳过9100 TCP段];
系统and版本探测 --> -A
-A--> A1[打开操作系统探测,版本探测,脚本扫描,路径跟踪] 
A1--> A[nmap -A 192.168.30.123];
获取详细版本信息 --> C1[--version-trace]
C1--> C[获取详细版本信息,对获取目标主机的额外信息有帮助];
系统探测 --> 操作系统探测
操作系统探测--> D1[-O] 
D1-->D[windows和linux有区别];
操作系统探测 --> E1["--osscan-limit"]
E1--> E[对C段目标进行探测,需要配合-A和-O];
系统探测 --> 探测系统识别
探测系统识别--> F1["--osscan-guess"]
F1-->F[当无法准确识别系统时可以利用这两个参数进行猜测系统];
探测系统识别 --> G["--fuzzy"]
G-->F;
RCP扫描 --> -sR
-sR--> 扫描是否为PRC端口,存在PRC端口即返回程序和版本号;

```

### 空闲扫描

```mermaid
graph LR;
-sl --> 运行进行端口完全欺骗扫描,伪装额外主机对目标进行扫描;
```

### 隐藏扫描

```mermaid
graph LR;
-sN --> A(	 能躲过一些无状态防火墙和<br>报文过滤的路由器,比SYN还隐蔽);
-sF --> A;
-sX --> A;
```

## 信息收集

1. WhoIs查询

> 脚本名称：whois-domain.nse 【查询目标WhoIs信息】<br>
> nmap --script=whois-domain.nse 192.168.30.177

2. DNS信息收集

> 脚本名称：dns-brute.nse 【通过DNS记录进行查询并且进行爆破】<br>
> nmap --script=dns-brute.nse 192.168.30.177

3. 扫描WEB漏洞

> 脚本名称：http:stored-xss.nse 【扫描XSS】<br>
> nmap --script=http:stored-xss.nse 192.168.30.177 <br>
> 还有很多脚本

## 漏洞利用

1. 检测MySQL密码

> 脚本名称：mysql-empty-password 【检查目标是否存在弱口令或者密码为root】<br>
> nmap --script=mysql-empty-password 192.168.30.177 <br>

2. FTP服务认证

> 脚本名称：ftp-brute【爆破目标是否存在弱口令】<br>
> nmap --script=ftp-brute 192.168.30.177 -p 21<br>

> 使用字典 <br >
> nmap --script=ftp-brute --script-args userdb=user.txt,passdb=pass.txt 192.168.30.177 -p 21


3. wordpress认证

> 脚本名称：http-wordpress-brute <br>
> nmap --script=http-wordpress-brute 192.168.30.177 -p 80

> 使用字典 <br >
> nmap --script=http-wordpress-brute --script-args userdb=user.txt,passdb=pass.txt 192.168.30.177 -p 80

![](G:\GitHub\Test1\test1\渗透笔记\NoteBook\kali的使用\Image\1.png)

![2](G:\GitHub\Test1\test1\渗透笔记\NoteBook\kali的使用\Image\2.png)

![3](G:\GitHub\Test1\test1\渗透笔记\NoteBook\kali的使用\Image\3.png)

![4](G:\GitHub\Test1\test1\渗透笔记\NoteBook\kali的使用\Image\4.png)