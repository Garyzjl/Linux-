# Linux指令操作
## 一、日常操作
1.cd指令   	- 进入指定文件夹
   cd  目录	- 进入指定目录(也可以是文件夹对应的路径)
			   ~相对路径 — 绝对路径
  cd  ..  	 - 返回上层目录
  cd  ~	 - 回到根目录

2.ls指令		- 查看当前目录中的内容

   ls
   ls  -l/-lh
   ls -a              - 隐藏文件也一起显示
   ls -R		- 递归显示所有内容
   ls -S/-t	        - 按大小/时间排序

3.pwd指令 	- 显示当前完整目录
   pwd

4.文件操作指令
touch  文件名	   - 新建文件
cat  文件名   		   - 查看文件内容
rm  文件名		    - 删除文件
rm - r  目录		    - 删除文件夹

cp  文件名1  文件名2	- 将文件1中的内容拷贝到文件2中
cp -r  文件名/目录名   目录2	- 将文件/目录拷贝到目录2中

mv	文件名1  文件名2	- 将文件1中的内容移动到文件2中 ,并且删除文件1（文件重命名）
mv	文件名1  文件目录	- 将文件1移动到指定目录中  
(注意：cp/mv/rm 后面可以跟： -i询问  -f强制  -n不覆盖)

mkdir  目录名		        - 新建文件夹
mkdir -p a/b/c		        - 按层级创建a,b,c三个文件夹
mkdir -p a/{b,c}/{d,e,f}	-同一层级常见多个
rmdir  目录名		        - 删除指定空目录

5.history		- 显示历史指令记录
bashrc 配置显示时间：export  HISTTIMEFORMAT="[%y‐%m‐%d_%T] " 
修改bashrc 后使其生效:  source ~/.bashrc  或 .  .bashrc   

6.链接
ln -s 源路径  目标路径		- 给源路径对应的文件在目标路径下创建一个软链接(可以看成是快捷键)
ln 源路径  目标路径		- 给源路径对应的文件在目标路径下创建一个硬链接

7.快捷键
ctr + f 		- 前进一个字符
ctr + b		- 后退一个字符
ctr + a		- 回到行首
ctr + e 		- 回到行尾
ctr + w		- 向左删除一个单词
ctr + u		- 向左删除全部
ctr + k		- 向右删除全部
ctr + y		- 粘贴上次删除的内容
ctr + l		- 清屏  

## 二、进程相关指令
1.ps指令
ps						- 进程状态
ps -aux  或者  ps ex		- 查看进程
ps -aux|grep 进程名		- 查看指定进程
psgrep  进程名

2.top指令
top 						- 动态监控进程
top  -p PID1,PID2,….		- 动态监控指定进程

3.free指令
free -单位				- 以指定单位查看内存

4.kill指令
kill 进程号					- 杀死指定的进程
kill -1/-9/-15				- -1(HUP)不间断重启，-9(KILL)强制杀死进程,-15(TERM)正常终止进程  
pkill  进程名				- 按名字处理进程
killall 进程名				- 处理名字匹配的进程
uptime					- 查看系统状态

## 三、权限管理
1.user和group
users 						-查看当前用户
groupadd  分组名				- 添加分组
useradd ‐G 分组列表 ‐m ‐s /bin/bash 用户名		- 创建一个用户添加到指定的分组中
usermod -G 分组列表 用户名		- 修改分组
sudo							- 以管理员执行其他程序
su - 用户名					        - 切换用户身份

2.查找
grep  查看对象 目录/文件  参数
参数：
-i      忽略大小写
-n    显示行标号
-E    通过正则表达式匹配
-v    忽略字段
-rn  递归查找目录，并打印行号
—include=‘*.py’     仅包含 py文件
—exclude=‘*.js’      不包含 js 文件

find    DIR -name  ‘*.xxx’ 找到目录下所有名字匹配的文件找出文件夹
例：find /tmp/xyz/ ‐perm 0642 ‐size +10k ‐size ‐100k ‐name '*.log'

which         指令 - 精确查找当前可执行的指令
whereis      指令 - 查找所有匹配的命令

## 四、权限管理
1.user和group : 一个系统可以有多个用户和多个分组； 一个分组中可以有多个用户，一个用户在不同的分组中(多对多)

users           - 查看当前用户
groups        - 查看当前分组
groupadd  分组名          - 添加分组

useradd ‐G 分组列表 ‐m ‐s /bin/bash 用户名      - 创建一个用户添加到指定的分组中(在home创建相应的文件夹)
usermod -G 分组列表 用户名         - 修改分组
passwd 用户名         - 修改密码

su - 用户名     - 切换用户身份
sudo               - 以管理员执行其他程序
注意： a.在ubuntu需要将用户添加到sudo分组中，才能使用sudo以管理员的身份执行程序
             b.在centOS中需要先执行visudo指令进入sudoers文件中在指定的位置添加内容
Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
xiaoming ALL=(ALL)      ALL (自己添加的，xiaoming是用户名)

2.chmod 
chmod    权限值   文件 - 修改指定文件的权限

chmod    [a,u,g,o][+,-][r,w,x]  文件 - 为指定文件，给所有用户添加相应的权限
   (a:所有，u:自己，g:同组，o:其他；+：添加， -: 取消；r:读，w:写，x:执行)
chown  用户名  文件 - 改变文件所有者

(权限制是三组二进制值)
self      group    other
rwx      rwx        rwx
111       101 001            - 自己读写可执行，同一分组的只读可执行，其他的只可执行
110      100        000

## 五、日志管理
1.cat指令
cat    文件 - 查看文件内容

2.查看部分
head -n  N  文件 - 查看前N行内容
tail  -n  N    文件  - 查看后N行内容

3.
less [-N]  文件
- 按 j 向下
- 按 k 向上
- 按 f 向下翻屏
- 按 b 向上翻屏
- 按 g 到全文开头
- 按 G 到全文结尾
- 按 Q 退出  

more [-N]  文件     - 和less差不多，这个是尽可能多，less是尽可能少的加载

4.处理
sort   - 排序  (cat 文件 |sort)
uniq - 去重  (cat 文件 |uniq) - 只会去重相邻的重复是数据，一般结合sort一起使用:  |sort|uniq
`awk ‘{print $N}’ - 打印第N列的内容(netstat -natp|awk ‘{print $4}’)`

history |awk '{print $4}' |sort |uniq ‐c | sort ‐rnk 1 | head ‐n 3    -获取历史指令中，使用最频繁的三个指令

5.统计
wc -c(字符)/-w(单词)/-l(行)  文件

6.查找
grep  查看对象 目录/文件  参数
参数：
-i 忽略大小写
-n   显示行标号
-E   通过正则表达式匹配
-v   忽略字段
-rn  递归查找目录，并打印行号
—include=‘*.py’ 仅包含 py文件
—exclude=‘*.js’ 不包含 js 文件

例如：
grep you bb.txt  
grep you bb.txt -i
grep you bb.txt -i -n
grep -E '[0-9]+' bb.txt 

find    DIR -name  ‘*.xxx’ 找到目录下所有名字匹配的文件
找出文件夹
例：find /tmp/xyz/ ‐perm 0642 ‐size +10k ‐size ‐100k ‐name '*.log'

which  指令               - 精确查找当前可执行的指令
whereis  指令           - 查找所有匹配的命令


## 六、网络管理
ifconfig     查看网卡状态
netstat   -natp                              - 查看网络连接状态
netstat   -natp|grep  端口号      - 查看指定端口的网络连接状态 

ping  地址 
ping  -i   时间 地址
ping  -c  次数    地址

telnet  ip地址 端口                       - 查看远程主机网络连接状况

dig 地址             - 查看DNS
wget  地址         - 下载