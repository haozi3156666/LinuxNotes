# LinuxNotes
linux基础知识

======================学习一========================== 
命令格式： 命令 [-选项] [参数] 
	eg: ls -la /etc 
1)个别命令不遵循此格式 
2）当有多个选项时，可以写在一起 
3）简化选项与完整选项 
	-a等于--all 

-------------- 

一 文件操作命令
	ls	-a	(all,查看隐藏文件（以 . 开头的文件，一般做系统文件）)
		-h	（human 人性化显示，有些单位会显示出来）
		-d	(dir，查看目录)
		-i	（i节点，文件号）
		-l	（long 查看详细信息，比如权限等）
drwxr-xr-x    （以d（dir）开头，目录；以l（link）开头，软链接；）后面表示权限(r(read),w(write),e(execute)) ， rw-       r--        r--
		        u(root)  g(group)   o(others)
21     文件引用技术   
root      所有者
root    所属组
4096  大小
6月7 11:40 lib  最后修改时间
	                        
-----------------------------------------------

mkdir	-p	（递归创建）
rmdir  删除空目录
cd 	改变目录
pwd	当前目录的绝对路径

cp 	-rp
	-r 复制目录时的选项
	-p 保留文件属性（比如修改时间）
mv	剪切与改名
rm	-rf [删除文件或目录]
	-r 删除目录
	-f 不提示删除
-----------------------------------------------------
文件处理命令：
touch	文件名	(创建文件)

cat 	 文件名	（查看文件）	查看小文件
     	-n	（查看行号）	

more  		分页查看
	-f（空格）	翻页
	Enter		换行
	q或Q		推出
less	可以往前翻页
	进去后可以输入  /内容  搜索你需要的东西

head	-n	看一个文件的前n行
tail	-n	看一个文件的后n行
	-f	动态的看一个文件（比如动态的日志，实时更新的）

-----------------------------------------------------
文件处理命令：ln
ln	-s 原文件 目标文件	（生成软链接）
	源文件	目标文件	（生成硬链接，和cp -p 操作一样，只是源文件和目标文件同步更新，i节点和源文件的i节点相同，不能跨分区）

-------------------------------------------------------

权限管理命令：chmod
chomod	[{ugoa}{+-=}{rwx}][文件或目录]
	[421][文件或目录]
	-R 递归调用
权限的数字表示：
r --- 2*2=4	读权限	可以查看文件内容  可以列出目录中的内容
w --- 2		写权限	可以修改文件内容  可以添加，删除文件夹文件
x --- 1		可执行	可以执行  可以进入目录

----------------------------------------------------------
改变一个文件的所有者（只有root能够操作）
chown	[用户][文件或目录]

改变一个文件的所属组
chgrp	[所属组][文件或目录]

查看或设置默认的权限
umask -S	（新建文件的可执行权限会自动去掉）

----------------------------------------------------------
通配符：
* ---匹配任意字符
? ---匹配单个字符	
文件搜索命令
find	[搜索范围][匹配条件]
	/home/	   -name    *testfile.txt*
		   -iname(不区分大小写)
		   -size    +n（大于）|-n（小于）|=n（等于）  单位：1数据块 = 512字节=0.5k
		   -user 用户名
 		   -type   f(file)|d(dir)|l(link)
		   -inum   n
联合查找：
连接符：-a     （and）
	-o	(or)

	-exec|-ok ls -l  {} \;	对查询结果的操作(-ok多了一个确认的提示)
    eg：
--------------------------------------------------------

其它搜索命令：
locate 文件名			（从资料库中查找，不能实时查找，但速度非常快，一般用来搜索系统文件）
updatedb 更新文件资料库

which 命令名	（查找一个命令在系统中的绝对位置）
whereis	命令名	不仅能查找命令所在位置，还能查找到帮助文档所在位置和配置文件所在位置


grep	-v（排除字符串）	地址
	-i（忽虏大小写）

---------------------------------------------------

帮助命令：
man	命令名	（manual，查看命令的详细信息）

命令	--help	（查看命令的主要选项）

help	命令	（只能查看shell内置命令


--------------------------------------------------

用户管理命令：
useradd	  用户名
passwd	用户名	（为用户设置密码）

who	（查看登录的用户名）
登录的用户名	登录的终端（tty--本地登录，pts--远程登录）
登录时间 （登录的远程主机的ip地址）

uptime	查看登录的时间

w	查看一些信息

---------------------------------------------

压缩解压缩命令：
.gz文件（只能压缩文件，不能压缩目录，不保留源文件）
	压缩：	gzip	文件名
	解压缩	gunzip	文件名

.tar.gz文件(打包并压缩，能压缩目录)
	压缩：	tar 	-c（打包） 		生成的文件	需要打包的文件目录
			-v(产看详细信息)	
			-f（指定文件名）
			-z（打包同时压缩）
	解压缩：
		tar	-x（解包）
			-v
			-f
			-z


.zip
	zip  -r（压缩目录）  [压缩后文件名] [文件或目录]
	upzip

.bz2(压缩比非常高)
	bzip2	-k(产生压缩文件后保留源文件)	文件
	bunzip2	...

.tar.bz2
	压缩：tar  -cjf japan
	解压缩：tar -xjf japan.tar.bz2

---------------------------------------------

网络命令：
write 用户名  （需要用户都登录） | mail 用户名 （不许要登录也行，用mail命令接收）
内容
ctrl+D结束并发送

-----
广播：（write all）
wall

-----
ping -c（指定发送次数）  ip地址
-----
ifconfig
查看当前计算机网卡信息，可以查看当前ip，mac地址等

-----
last（所有用户登录的信息）
lastlog(查看用户的登录信息)
------
******traceroute www.baidu.com	(查看访问网站的详细路径)

******netstat	-t	tcp协议
		-u	udp协议
		-l	监听
		-r	路由
		-n	显示ip地址和端口号
例子：
	netstat -tlun  查询当前计算机开得端口
	netstat	-an	查看所有的监听信息
		-rn
-------
moute（挂载）

--------------------------------------
shutdown  -h（关机） [时间]
	  -r（重启）  [时间]
	  -c  （取消前一个关机命令）


logout
--------------------------------------
vim工作模式：
vi filename
命令模式---- :命令 -----编辑模式
插入模式
                           
a---在光标所在字符后插入
A---在光标所在行尾插入
i---在光标所在字符前插入
I---在光标所在行首插入
o---在光标下插入新行
O---在光标上插入新行

命令模式下的操作：
:set nu(number)  设置行号
:set nonu   取消行号
gg	到第一行
G	到最后一行
nG	到第n行
:n	到第n行

$	移动到行尾
0	移动到行首

x	删除光标所在字符
nx	删除光标所在处后的n格字符
dd	删除/剪切光标所在行，ndd删除n行
dG	删除光标所在行到文件末尾内容
D	删除光标所在出的行尾内容
:n1,n2d	删除指定范围的行

yy	复制当前行
nyy	复制当前行的
dd	剪切当前行
ndd	剪切当前行以下n行
p|P	粘贴在当前光标所在行下|行上

R	从光标出开始替换，按Esc结束
r	替换光标所在处的这个字符
u	取消上一步操作

/string	搜索指定的字符串，忽虏大小写：set ic
n(next)	定位到查找的下一个字符串

:%s/oldstring/newstring/g	全文替换指定字符串
:n1,n2s/oldstring/newstring/g	在一定范围内替换字符串

:w 文件名  （相当与另存为），没有文件名相当与保存
:wq 保存退出
:wq! 强制保存退出（所有者和root才能操作）


:r !命令   将命令执行结果导入到光标所在处
	
:map 快捷键  出发命令
  eg：在行首插入#（注释）
	:map 快捷键组合(如：ctrl+/) I#<Esc>
      取消#
	:map 快捷键组合(如：shift+/) 0x

连续行注释：
	:n1,n2s/^/#/g	  第n1到n2行的行首加上#
	:n1,n2s/^#//g	  去掉行首的#
	:n1,n2s/^/\/\//g	在行首加上//

替换：
     :ab mymail sanlee@lampbrother.net


-------------------------------------------
查看我是哪个用户：
	whoami

切换登陆的用户：
	su 用户名
	
以某个用户进行操作
	sudo -u 用户名 操作命令

软件包的分类：
源码包
	脚本安装包
二进制包（RPM包，系统默认包，编译后的01代码串文件）


-------------------------------------------

rpm  安装(已经编译好的rpm文件包，安装经常需要安装相应的依赖包)
包名，包全名


