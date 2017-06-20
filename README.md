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

## ping
测试网络是否通畅

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
- r 读取权限
- w 写权限
- x 执行权限

第一位：区分文件还是文件夹

第一个rwx：表示但前用户权限

第二个rwx：表示与但前用户所在同一个组的用户的权限

第三个rwx：表示组外用户权限












































































