# 文件系统目录结构

## FHS文件系统

FHS文件系统层次化标准

树形结构

### 文件系统目录结构

单根倒置树结构

/表示根，也用于分隔路径

文件名大小写敏感

.开头为隐藏文件

文件名最长255字节

包含路径最长4095字节

颜色对应

- 蓝色目录
- 绿色可执行
- 红色压缩
- 浅蓝色链接
- 灰色其他

除了/和NUL所有字都有效

元数据：metadata即属性和数据：data即文件内容

### 常见文件系统目录

![screen-capture](3576e40d73def3cd2bacb2321b706594.png)

### 应用程序组成部分

![screen-capture](af7887f867db43497268153eae1f8dc8.png)

### Linux下的文件类型

|类型|标识符|
|--|--|
|普通|-|
|目录|d|
|链接|l|
|块设备|b|
|字符设备|c|
|管道|p|
|套接字|s|

#### 管道文件

连接读进程和写进程实现它们之间的数据通信，又称pipe

FIFO

单向

#### 套接字文件

表示进程间网络通信的特殊文件，内核借助缓冲区形成的伪文件

FIFO

双向

# 文件操作命令

### 显示当前目录

```
pwd 
-L 默认
-P 真实路径
```

### 绝对路径和相对路径

绝对路径从根出发，以/开始

相对路径以当前的位置为参考，不用/开始

 ..表示上一层目录

```
basename 基名，取出地址文件名部分
dirname 目录名，取出地址路径部分
```

<br/>

### 更改目录

```
cd
-L 默认
-P 真实路径
```

$PWD #当前目录
$OLDPWD #上一次目录

### 列出目录内容

```
ls
-a
-l
-h
ll -> alias
l. -> alias
```

![screen-capture](0b2764743898dae35794a4596a9740fc.png)

### 查看文件状态

```
stat
```

![screen-capture](899ca93ccd3014c34403ba5b235a14a6.png)

#### 文件时间戳属性

![screen-capture](34c746f6b848e9656660536d7c1c0aa1.png)

### 确定文件内容

```
file 确定文件内容以确定打开方式 -f从文件读取
```

linux下看后缀不一定有用 通过file可以确定文件类型

![screen-capture](4826dca8119adc7da15ae18bad09baba.png)

### 文件通配符

用于匹配符合条件的多个文件

![screen-capture](cb733f6257ab2e3abdd6e8b9ed7256cc.png)

### 创建空文件或刷新时间

```
touch
```

![screen-capture](006d61adc977898a997131308d1461da.png)

### 复制文件或目录

```
cp
```

![screen-capture](18ad5b8f040578b73dfbef60b4ec6c7c.png)

<br/>

### 移动和重命名

```
mv
```

![screen-capture](688876605ed4296c1cc260d4229df3cc.png)

同分区移动快，数据位置没有变化

跨分区移动慢，数据位置变化

```
rename 批量重命名
```

![screen-capture](010ddec81f15c24826ad8861882802ae.png)

### 删除文件

```
rm
```

![screen-capture](f0166aa5898fd9b22b3cd012e6d96587.png)

## 目录操作

### 显示目录树

```
tree -d -L
```

![screen-capture](a8f8b824f39d3cf280e1d9036f4ac188.png)

### 创建目录

```
mkdir
```

![screen-capture](d0d08800f84b1c017a040542e8ab13ac.png)

### 删除目录

```
rmdir
```

只能删除空目录 可以使用rm -r递归删除目录

![screen-capture](16b88b720b7423ba2f5c8bf25ee39a3e.png)

# 文件元数据和节点表结构

## inode表结构

inode索引节点存储元数据

磁盘分为两部分，一部分存储inode，一部分存储数据块

目录记录文件名和inode对应关系

文件名->inode->inode表->数据块

***

cp命令分配空闲inode号，在inode表中生成新条目，在目录创建目录项将名称与inode号关联，拷贝数据块

***

rm命令释放inode号，将数据块放在空闲列表中，数据没有被实际删除而是后续被覆盖

***

mv命令在同分区时用新文件名创建目录对应项，删除旧目录条目，不影响inode表或磁盘数据

跨分区移动相当于cp和rm

***

```
df -i -lh
```

![screen-capture](a40d26fe9277559ab359447a6cfd94f4.png)

inode耗尽或空间占满都会提示没有空间

## 硬链接

允许一个文件有多个文件名

```
ln filename linkname
```

![screen-capture](18f1c7c79345cbe290813a9a5ed5d876.png)

创建目录时默认2个硬链接，自己和目录下的.和目录下的目录下的..

## 软链接（符号链接）

软链接创建独立文件指向目标文件名

```
ln -s filename linkname
```

若使用相对路径，filename是相对于linkname的，而不是当前目录

![screen-capture](858d5d67ea86447dd4732338eaf91b04.png)

## 区别

![screen-capture](70b4211434c3a73e314fa92a830fbcc4.png)

# 重定向和管道

## 标准输入输出

- 标准输入设备
- 标准输出设备
- 标准错误输出设备

## I/O重定向

### 标准输出和错误重定向

将标准输入、输出或错误重定向到指定位置

```
COMMAND OPERATOR FILE|DEVICE

>
1>
2>
&>

>>
1>>
2>>

```

### 标准输入重定向

```
tr 
```

![screen-capture](546068414b2fb9aa7d1ce662451b99ff.png)

标准输入 不带参数输入命令后回车若等待输入说明支持标准输入

### 多行重定向

使用"<<终止词"命令从键盘把多行重定向给标准输入

![screen-capture](30edff3d69a3b4325094d4edc03a9baa.png)

### 高级重定向

```
<<< 
< <()
```

cmd <<< "string" 含义是 here-string ，表示传给给cmd的stdin的内容从这里开始是一个字符串

![screen-capture](e020b53d73aa69e35ac92e8b7943b44a.png)

![screen-capture](442cd4adb721a7f7dd773bc1cf2337b7.png)

cmd1 < <(cmd2) 名称为 Process substitution ,由两部分组成

- <(cmd2)表示把cmd2输出写入临时文件
- cmd1 <是输入重定向

![screen-capture](f5aadccaa662018d2bc5a6a009374d24.png)

## 管道

### 管道

前一条输出发给后一条

```
COMMAND1|COMMAND2|COMMAND3|...
```

### tee命令

将标准输入复制到每个指定文件，并送标准输出

![screen-capture](817bb6ffb2d556645d04ed676a14ac73.png)
