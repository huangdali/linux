# liunx学习笔记

# 一、linux常用命令

##  ls
查看当前目录下的文件夹及文件信息

- ls /bin 表示查看根目录下的bin文件夹的东西
- ls -a 表示显示隐藏文件
- ls -l 表示以列表的形式显示内容
- ls -lh 表示以列表的形式显示内容，并且文件大小为友好提示
- ls -alh 表示显示但前目录下的所有文件（包括隐藏的），并且友好显示文件的大小
- ls *.txt 表示以txt结尾的所有文件[正则表达式]
- ls *.t?t ？表示任意一个字符（必须为一个）
- ls [0-9a-z].txt []表示满足其中一个即可满足


## pwd
显示当前文件夹的全（绝对）路径




## cd
进入到指定目录

- cd ..  退回到上一层目录
- cd - 回到上一次的目录
- cd ~ 回到当前用户的根目录（/home/hdl）

.表示当前路径

..表示上一层路径

## clear
清屏

## tab
命令补全

## touch
创建一个文件
>linux中没有后缀的说法

## >、>>
重定向，配合ls使用
>表示将输出信息保存到文件中

\>表示如何有文件，则覆盖

\>\>表示如何有文件，会追加信息，不会覆盖之前的内容

## more
分屏显示文件内容
>空格表示显示下一页

## |
管道
> 合并多个命令

## mkdir
创建文件夹

- mkdir python 创建一个python文件夹
- mkdir a/b/c -p 创建嵌套目录，必须加-p（表示递归创建）

## rmdir
删除空目录

## rm
删除任何目录/文件（不可找回）
- rm 文件夹 -r 表示删除文件夹(-r表示递归地删除文件、文件夹)
- rm 文件  直接删除
- rm -rf 文件夹   不提示直接删除（递归删除）

## tree
以树的形式显示当前文件夹的目录树（可看文件目录结构）
```java
.
├── 01.py
├── 1.txt
├── a
│   └── b
│       └── c
├── linux_note.txt
├── print.txt
└── python
```

> 后面可以跟对应的目录，表示查看指定目录的目录树

## cat
查看文件内容

合并两个文件内容并输出
```java
cat 1.txt 2.txt
```


cat支持 \>重定向


## grep
按关键词查询文件内容
```java
hdl@hdl:~/桌面$ grep 'a' haha.txt
四、clear
asgashagasg
sgasg
asgag
ahgag

```

-n表示显示行号
```java
hdl@hdl:~/桌面$ grep -n 'a' haha.txt
17:四、clear
22:asgashagasg
25:sgasg
29:asgag
32:ahgag
```

-i 表示忽略大小写

-v 表示取反

正则表达式：^a（以a开头的）

          a$（a结尾的）

## --help
查看帮助文档（参数介绍）

## man
同上

man ls 查看ls的帮助文档

man print 查看c语言中print函数的帮助文档

## history
查看历史命令

## find
查找文件，支持正则表达式

查找当前文件夹下的文件
```java
hdl@hdl:~/桌面$ find -name '0*'
./01.py

```


查找指定文件夹下的文件(下面表示查找根目录下的所有以.txt结尾的文件)
```java
find / -name '*.txt'
```

## cp
复制文件

-v 显示进度

-i 提示是否复制

//表示复制01.py到但前文件夹下，名字为01_c.py

cp 01.py 01_c.py

//复制当前文件夹下的所有包含1的文件到a/b文件夹下

cp *1* a/b

## mv
移动/剪切、重命名

mv a/* c

将a文件夹下的所有文件移动到c文件夹下

-f 不显示友好提示（强制执行）

-i 友好提示

-v 显示移动的速度

## tar
打包、压缩文件、解压文件

//打包当前文件打包为test.tar
```java
tar -cvf test.tar ./*
```

//解压文件

```java
tar -xvf my.tar
```

打包并压缩d文件夹的内容
 ```java
 tar -zcvf test.tar.gz d
 ```

解压gz文件

```java
tar -zxvf test.tar.gz
```
## gzip
1、压缩打包好的文件

//将tar文件压缩，建议使用.gz结尾
```java
gzip my.tar my.tar.gz
```


2、解压缩包为包

```java
gzip -d my.tar.gz
```

## zip
压缩文件

压缩d文件夹为demo.zip
```java
zip demo.zip d
```

## unzip
解压缩

//解压压缩包到指定目录（b文件夹）
```java
unzip -d ./b dmeo.zip
```

## which
查看命令位置
```java
hdl@hdl:~/桌面$ which ls
/bin/ls
```

# linux用户、权限管理

## who
查看当前所有登录的用户
-q 查看有多少个用户登录

## whoami
查看当前用户

## exit
退出当前登录的账户


## ifconfig
查看ip地址
```java
root@hdl:/home/hdl/桌面# ifconfig | grep -n 192.*
18:          inet 地址:192.168.1.5  广播:192.168.1.255  掩码:255.255.255.0

```

禁用网卡

```java
ifconfig 网卡名（eg:wlp3s0） down
```

启用网卡

```java
ifconfig 网卡名（eg:wlp3s0） up
```

设置ip地址
```java
sudo ifconfig 网卡名（eg:wlp3s0） ip地址
```


## ping
测试网络是否通畅

会一直ping

## ssh
远程登录linux

格式： ssh 用户名@ip地址

## useradd
也可以用useradd的链接adduser

-m 自动建立目录

-d 指定home的目录

-g 指定组名称

//创建tj用户 并指定home目录
```java
sudo useradd tj -m -d /home/tj
```


//为新建的用户添加sudo权限
```java
sudo usermod -a -G adm username
sudo usermod -a -G sudo username
```

## passwd
设置、修改密码
```java
sudo passwd tj
```
输入密码

## su

切换到指定用户（会停在但前文件夹）
```java
su 用户名
```

//会跳转到指定账户的home目录

```java
su - 用户名
```

## sudo
申请root权限

//切换到root用户
```java
sudo -s
```

## userdel

删除用户

//不会删除对应的文件夹
```java
userdel 用户名
```

//会删除相应的文件夹
```java
userdel -r 用户名
```

## groupadd
>查看组：cat /etc/group

创建用户组haha
```java
sudo groupadd haha
```

## grouddel
删除组
```java
sudo grouddel haha
```

## groups
查看当前用户所在的组

## usermod
修改用户所在的组(设置默认的组)
```java
sudo usermod -g 用户组名 用户名
```

//添加组
```java
sudo usermod -a -G 用户组名 用户名
```

//为新建的用户添加sudo权限
```java
sudo usermod -a -G adm username
sudo usermod -a -G sudo username
```

## drwxrwxrwx的权限说明
参数说明：
- d 文件夹
- \- 文件/无权限
- r 读取权限 ---->4
- w 写权限  ---->2
- x 执行权限 ---->1

第一位：区分文件还是文件夹

第一个rwx：表示但前用户权限

第二个rwx：表示与但前用户所在同一个组的用户的权限

第三个rwx：表示组外用户权限

## chmod
权限设置

```java
chmod u/g/o/a +/-/= rwx 文件名
```

参数说明：

- u 该文件的拥有者
- g 该文件下的所有组成员
- o 其他用户
- a 所有用户
- \+ 增加权限
- \- 撤销权限
- = 设定权限

eg:
```java
hdl@hdl:~/桌面/b$ chmod u=rw,g=r,o=w 1.txt
hdl@hdl:~/桌面/b$ ls -l
总用量 8
-rw-r---w- 1 hdl hdl    0 6月  21 22:19 1.txt
drwxrwxr-x 3 hdl hdl 4096 6月  19 23:10 a
drwxrwxr-x 2 hdl hdl 4096 6月  20 21:36 d
```

```java
hdl@hdl:~/桌面/b$ chmod 761 2.sh
hdl@hdl:~/桌面/b$ ls -alh
总用量 20K
drwxrwxr-x 4 hdl  hdl  4.0K 6月  21 22:33 .
drwxr-xr-x 6 hdl  hdl  4.0K 6月  20 21:46 ..
-rw-r---w- 1 hdl  hdl     0 6月  21 22:19 1.txt
-rwxrw---x 1 hdl  hdl     8 6月  21 22:33 2.sh
drwxrwxr-x 3 hdl  hdl  4.0K 6月  19 23:10 a
drwxrwxr-x 2 hdl  hdl  4.0K 6月  20 21:36 d
-rw-r--r-- 1 root root    0 6月  21 22:30 test.sh
```
- 7:rwx
- 6:rw-
- 1:--x

chmod 777 文件夹，只会修改文件的权限为777,里面的所有文件不变
         -R 表示文件也变为777

## cal
查看日历

## date
查看当前系统时间

## ps
查看当前系统的进程

```java
ps aux
```

## top
动态查看进程信息（windows中的任务管理器）

## kill
杀死进程

```java
kill  pid数
```

//强制杀死进程
```java
kill -9  pid数
```

## 关机、重启设置
- reboot 重新启动系统
- shutdown -r now  重启系统，会提示用户
- shutdown -h now  马上就关机
- shutdown -h 20:25 定时关机，20：25的时候会关机
- shutdown -h +10 10分钟后会自动关机
- init 0 关机
- init 6 重启


## df
查看硬盘空间占用情况，配合-h效果更佳
```java
df -h
```

## du
查看当前文件夹下的硬盘占用情况，同样配合-h效果更佳
```java
du -h
```

## gedit

文本编辑器

## sublime

## vi
三种模式
- 命令模式（默认）
- 编辑模式
- 末行模式

命令--》编辑模式  i,a,o

- i 在光标左边插入
- a 在光标右边插入
- o 在光标的下方插入
- I 在行首输入
- A 在行末插入
- O 在光标的上一行

编辑--》命令  Esc


保存退出：shift +两次z

：q 退出  q! 强制退出

：w 保存

：wq 保存并退出（x也是保存退出）

# vim
跟vi差不多

ctrl+n代码补全提示

yy 复制  8yy:表示从光标开始复制8行

p粘贴

dd 剪切  8dd：表示光标开始剪切8行

u  撤销

ctrl+r 反撤销

G 跳转到最后一行

14G表示跳转到第15行

gg 跳转到第一行

w 段意

ctrl+b 下一屏

ctrl+e 上一屏

x:上出光标后一个字符，相当于delete

X：表示删除光标前一个字符，相当于Backspace

v:多选

vim 1.pu +22 打开到22行

. 重复执行上一次的命令

r 替换但前的字符

/搜索的内容

将当前文件中的所有abc替换为123
```java
：%s/abc/123/g
```

将当前文件中1-10行的所有abc替换为123
```java
：1,10s/abc/123/g
```

# Ubuntu下载软件

## apt
更新、下载软件

更新已经安装的服务器
```java
apt-get update
```

下载软件的服务器配置文件路径
```java
/etc/apt/sources.list
```







































































