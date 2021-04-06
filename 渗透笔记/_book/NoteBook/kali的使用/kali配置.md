# IP设置

> 配置文件：/etc/networking/interface

## 临时IP

```shell
ifconfig eth0 192.168.31.111/24
```

## 永久IP

```shell
auto eth0
#iface eth0 inet dhcp #如果原文件中有这一行，就注释掉
iface eth0 inet static
address 192.168.1.53
netmask 255.255.255.0
gateway 192.168.1.1
```

## 动态IP

```shell
auto eth0
iface eth0 inet dhcp
```

## 配置默认路由

```shell
route add default gw 192.168.1.1
```

## 重启网络命令

> service networking restart

# DNS配置

> 配置文件：/etc/resolv.conf

## 命令

```shell
echo nameserver 8.8.8.8 > /etc/resolv.conf
或者
gedit /etc/resolv.conf
添加
nameserver 8.8.8.8
```

# 更换源文件

> 配置文件：/etc/apt/sources.list

```
#中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
 
#阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
 
#清华大学
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
 
#浙大
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
 
#东软大学
deb http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
deb-src http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
 
#官方源
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib
 
deb http://mirrors.163.com/debian/ jessie main non-free contrib
deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib
deb http://mirrors.163.com/debian/ jessie-backports main non-free contrib
deb-src http://mirrors.163.com/debian/ jessie main non-free contrib
deb-src http://mirrors.163.com/debian/ jessie-updates main non-free contrib
deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib
deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib
deb-src http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib
```

## 更新命令

```shell
apt-get update  # 取回更新的软件包列表信息
apt-get upgrade # 进行一次升级
apt-get clean # 删除已经下载的安装包
reboot  #重启
```

# XShell远程连接

1. 修改配置文件`gedit /etc/ssh/sshd_config `【把注释去掉】

   ![](G:\GitHub\Test1\test1\渗透笔记\NoteBook\kali的使用\Image\图像 1.png)

2. 重启服务`/etc/init.d/ssh restart `

3. 配置开机启动`update-rc.d ssh enable`

4. 关闭开机启动`update-rc.d ssh disable`