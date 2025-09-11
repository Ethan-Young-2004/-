# 用户

## root用户

- 完整的系统控制
- 对系统损害几乎有无限的能力
- 除非必要，不要登录

## 普通（非权限）用户

- 权限有限
- 造成损害能力有限

# 终端 terminal

与计算机相连的输入输出设备，显示主机运算输出，接受主机要求的输入

现代计算机终端不再是单独的物理设备，console和tty终端都是虚拟出来的概念

Linux中以文件形式存在

## 终端类型

 ![screen-capture](5d8e1c74c7511debbf55ebd580116afe.png)

## 查看当前的终端设备

tty

## 交互式接口

启动终端后，在终端设备附加一个交互式应用程序

### 交互式接口类型

- GUI
- CLI

### shell

![screen-capture](b4cf5caeb6d9383feada20d0bd3132e3.png)

![screen-capture](4fbef274cc908fe2d2c67979c8143e02.png)

- shell是命令解释器---接收用户的输入并解释执行
- shell是一种编程语言
- shell是用户和机器的交互式接口

### 各种shell

![screen-capture](717ad74803214b340103ecf23da5dee0.png)

### bash shell

目前Linux的标准shell，与sh相兼容

### 主机名

hostname NAME  临时生效

hostnamectl set-hostname NAME 持久生效

![screen-capture](bbcdb66b40cb0cf587bb4e1a8aa9b5f4.png)

<br/>

### 命令提示符

- #代表当前用户为root
- $代表当前用户为普通用户

PS1颜色设置

# 命令执行过程

- 内部命令
- 外部命令 PATH中按照先后顺序
- hash 缓存表

执行顺序 内部->hash->外部

## 别名

执行顺序 别名->原命令->内部->hash->外部

alias unalias 仅对当前shell有效   

若需要永久有效   /etc/bashrc   /etc/bash.bashrc   修改后需要重新登陆或重新读取

![screen-capture](e3268a15e52866aef69084e79eef91b0.png)

别名与原命令重名时执行原命令

![screen-capture](ef93d92e8a82b9c63111b1acc45b06ca.png)

## 命令格式

![screen-capture](8b9500c4be371f6a1bd2805324c3cf33.png)

### 选项风格

- 短选项 短选项可连在一起
- 长选项 长选项不可连在一起
- BSD 不带-

选项，参数，命令间使用空格分隔

结束或取消执行Crtl+C Crtl+D

多个命令使用;分开

一个命令使用\分成多行

## 硬件相关命令

lscpu 和 cat /proc/cpuinfo cpu信息

lsmem 和 cat /proc/meminfo 和 free 内存信息

lsblk 和 cat /proc/partitions 磁盘信息

arch 架构

uname -a -r 内核版本

cat etc/os-release 操作系统版本

cat /etc/issue 本地终端登录前的欢迎/提示信息

## 日期和时间

系统时钟：Linux内核通过CPU时钟频率进行

硬件时钟：主板上的时间

### 显示和设置系统时间

![screen-capture](fe6eaf74a8f9d12c21e576b68cdfca18.png)

UTC时间 CST时间

***

时间戳 
date +%s 从1970/01/01到当前过了多少秒

***

硬件时钟查看

![screen-capture](defd425296540b57ce3fd1ecb9d7d010.png)

***

时区 etc/localtime

设置时区 timedatectl set-timezone

***

日历

![screen-capture](c5bc910ebfc6adff4de9538f6671cb00.png)

### 关机和重启

关机

![screen-capture](0b59beca0da96a0249ca2095bb19addf.png)

***

重启

![screen-capture](c86c42a7957b85cdd2566d3dce233030.png)

***

关机或重启 shutdown 会广播所有用户 安全的关机

![screen-capture](457bc3a6eaf62276e386b1b51cfcf20c.png)

### 用户登录信息

whoami  who am i

who

![screen-capture](dbb77d6e1914e934148d9334952d1a4e.png)

w

![screen-capture](a0083647b60b1499ba7381dace611edd.png)

### 文本编辑

- nano
- gedit

### 登录提示信息

etc/motd

## 会话管理

一个终端窗口一个会话 窗口与启动进程连接在一起，窗口关闭会话结束

解绑会话与窗口 

安装 screen

#CentOS7 安装screen
[root@centos7 ~]# yum -y install screen
#CentOS8 安装screen
[root@centos8 ~]# dnf -y install epel-release
[root@centos8 ~]# dnf -y install screen
#ubuntu
[root@ubuntu ~]# apt install screen

![screen-capture](17e1ebac24b8096dae6d91d43ec9227c.png)

安装tmux

## 输出信息 echo

<br/>

## 字符集和编码及语言环境

ASCII

GB2312

Unicode

### 命令行拓展和被括起来的集合

命令行拓展``和$()

把一个命令的输出打印给另一个命令的参数，放在’‘中的一定是有输出信息的命令

![screen-capture](0be8222a966c11a9c24151086efe0822.png)

![screen-capture](03b9ccde8a6ccfe8e4475441a80e03ec.png)

{}可以实现打印重复字符串的简化形式 

离散空间展开/连续空间展开

![screen-capture](90201b4373843300da91d3018296a430.png)

## TAB补全

- 命令补全
- 路径补全

可以确定就1次补齐，否则2次给出列表

![screen-capture](731cf77252f153ad38cb3dece18c3add.png)

## 命令行历史

.bash_history

在终端启动要将.bash_history的内容加载进内存

终端退出会将当前历史记录写入.bash_history

连续重复命令计为1条

没有写入文件的历史不在新终端生效

![screen-capture](f0420cf0417734b04fb8bf7cca96aa68.png)

![screen-capture](9f3beb0e668cc5a3600398b4f0418d49.png)

一个配置要持久生效一定要写文件

## 调用命令历史

![screen-capture](4a3bd0d03d420f877a189c4769487466.png)

![screen-capture](46d6eb23cad8c781ee3580e58dfc906f.png)

![screen-capture](9a46afcd8d05d02bcb1d3e68c8f6e07e.png)

## bash的快捷键

![screen-capture](0919efd424fdfe21b85bf25224301d81.png)

## 登录提示

### 登录前提示

/etc/issue和/etc/issue.d下的.issue文件

![screen-capture](1533d331eb540964c00e4d77af903ec5.png)

ssh登录信息放在/etc.net.net中但内容不支持转义(安全考虑)，需要使用还需要修改sshd的配置文件

### 登陆后提示

motd

etc/motd文件

etc/motd.d/文件夹

![screen-capture](971f8a3548cf84ae8a586b34fb419682.png)

## 获得帮助

![screen-capture](16a14df847f77edad936254288042778.png)

### whatis & whereis

whatis列出简短描述以及对应man手册章节

刚安装完系统不可用可使用 mandb手动初始化

![screen-capture](c700a46bd4fa52017be920071289aff6.png)

whereis 列出命令或系统文件路径以及对应man的文档路径

### 查看命令帮助

#### 内部

help COMMAND

man bash 查看全部

#### 外部

COMMAND --help 或 -h

man COMMAND

info COMMAND

### man命令

帮助手册，是个外部命令，本质是读取特定文件进行输出

标准man 手册一般有以下几个章节:

1. 可执行程序或 shell 命令
2. 系统调用(内核提供的函数)
3. 库调用(程序库中的函数)
https://man7.org/linux/man-pages/index.html
https://man7.org/linux/man-pages/dir_all_alphabetic.html
[root@rokcy8 ~]# yum install man-pages
[root@ubuntu2204 ~]# man man
......
......M58-Magedu
4. 特殊文件(通常位于 /dev)
5. 文件格式和规范，如 /etc/passwd
6. 游戏
7. 杂项
8. 系统管理命令(通常只针对 root 用户)
9. 内核API

![screen-capture](45b6070ca564441cffa43bdc1ad4c3df.png)

![screen-capture](9fd4862fd73e264478945512ceab54a8.png)

### info命令