June 30, 2018 5:49 AM
June 12, 2018 10:36 AMJune 11, 2018 3:27 PM
June 10, 2018 5:49 PM



&nbsp;<font color=#0099ff size=4 face="黑体">黑体</font>
*车体*
**加粗**
\\*#--反车线可显示特殊符号。
<u>我是 underline</u>
&nbsp;<----------这里有一个空格。
1234
&emsp;<---------这里有2个空格。
1234
&<-------

~~delete me~~

1. abc
	1. abc
	2. cdef
		1. cdefg
		2. ggggg
		3. r4rrrr
2. xyz
	1. xyzjj
	2. kkk


![CSDN图标](https://img-blog.csdn.net/20150316184625949 "这是CSDN的图标")
![raspberrypi](/home/henry/rpi/raspberrypi.png  "this is raspbery pi")



<center><font size=6>My raspberry pi settings</font></center>

##### 刻录树莓派系统 

树莓派运行的官方系统是基于 Debian 的衍生版 Raspbian，你也可以安装其它移值树莓派上 的 Linux 发行版。</br>可以从 Raspberrypi.org 上下载最新版 Raspbian “wheezy” 后刻录到 SD 卡 中。将下载后的压缩包解压，得到 img 格式镜像。

##### Windows:

1. 在 Windows 下，可以使用 Win32DiskImager 向 SD 卡写入系统镜像。
2. Mac OS X 和 Linux 的用户可以通过命令行写入镜 像文件。

##### Linux:

下面以 Ubuntu 为例，其它 Linux 发行版和 Mac OS X 相同： 

1. 解压的镜像文件放在 Home 文件夹下（也就是 /home/（你的用户名））， 
2. dh -h 方法, lsblk, <font color=red>sudo blkid</font>
	1. 先不插入 SD 卡，终端中输入 df -h，之后再插入 SD 卡，再次运行 df -h，
	2. 找到新出现的设备，记下设备名，如 "/dev/mmcblk0p1" 
或 "/dev/sdd1"（最后的“p1”和“1”代表分区编号）。 
	3. 卸载 SD 卡，umount /dev/（设备名）， 
3. <font color=red>sudo dd bs=4M if=~/2012-12-16-wheezy-raspbian.img of=/dev/mmcblk0</font>
注意，因为你要拷贝的是整个 SD 卡，所以去掉分区编号“p1”。之后是
你的 SD 读写速度。
&nbsp;<font color=red>erase /mbr： sudo dd bs=512 count=1 if=/etc/zero of=/dev/sbx</font>
4. sudo tail -f /var/log/messages 方法
键入以上命令，再插入reader，就知道sda or sdb，然後dd，完成。
5. 拷贝完成后，会出现写入数据大小和所用时间的列表。之后卸载 SD ，可以将其插入 raspberry pi 完成任务。
6. sudo raspi-config
7. 在 jessie, /etc/resolv.conf 找不到 nameserver. 可以在 /etc/resolvconf.conf 加入：
nameserver 192.168.1.4 就可以。然后 reboot. ok

### End



-----------------------------------------------------------------------


### apt-get 与 dpkg 之不同

**apt-get 安装软件**
命令： apt-get install softname1 softname2……  //在线安装软件包

卸载软件
命令： apt-get remove softname1 softname2 softname3……

卸载并清除配置
命令： apt-get remove --purge softname1

更新软件信息数据库
命令： apt-get update

进行系统升级
命令： apt-get upgrade

搜索软件包
命令： apt-cache search softname1 softname2 softname3……

**Deb软件包相关安装与卸载**
安装deb软件包
命令： dpkg -i xxx.deb        //安装本地软件包，不解决依赖关系

删除软件包
命令：  dpkg -r xxx.deb

连同配置文件一起删除
命令： dpkg -r --purge xxx.deb


### End




----------------------------------------------------------



### 解决语言设置错误的问题 发布时间：2014-01-11

在使用 ubuntu 命令行登录的时候，出现：

perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
    LANGUAGE = (unset),
    LC_ALL = (unset),
    LC_MESSAGES = "zh_CN.UTF-8",
    LANG = "zh_CN.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").

这样的错误，虽说不影响使用，但是感觉挺烦的说。

那么要如何解决呢，有必要记录下

安装 localepurge 管理语言文件

sudo apt-get install localepurge

选择我们想要的语言，例如 en_US.UTF-8 和 zh_CN.UTF-8。

当然也可以使用以下命令再次进行配置：

sudo dpkg-reconfigure localepurge

生成自己想要的语言

sudo locale-gen zh_CN.UTF-8 en_US.UTF-8

打印出当前的配置信息

locale

到此，搞定！！！

默认情况下终端 ssh 的时候会将本地的 locale 传到服务器中，可以通过命令指定 ssh 服务器的语言：
LC_ALL=en_US.UTF-8 ssh <host>




------------------------------------------------



### Sources.list stretch


sudo vi /etc/apt/sources.list 改成国内sources

deb http://mirrors.aliyun.com/raspbian/raspbian/ stretch main contrib non-free rpi
deb-src http://mirrors.aliyun.com/raspbian/raspbian/ stretch main contrib non-free rpi

deb http://mirrors.163.com/raspbian/raspbian/ stretch main contrib non-free rpi
deb-src http://mirrors.163.com/raspbian/raspbian/ stretch main contrib non-free rpi

deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi
deb-src http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi

deb http://mirrors.shu.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi
deb-src http://mirrors.shu.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi

**修改 raspi.list**

修改/etc/apt/sources.list.d/raspi.list

\#deb http://archive.raspberrypi.org/debian/ jessie main ui
\# Uncomment line below then 'apt-get update' to enable 'apt-get source'
\#deb-src http://archive.raspberrypi.org/debian/ jessie main ui
\#科大源
deb http://mirrors.ustc.edu.cn/archive.raspberrypi.org/debian/ jessie main ui

##### 新方法安装 sources.list

sh -c 'printf "deb http://ftp.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list'  
sudo apt update  
sudo <font color=red>apt -t jessie-backports</font> install shadowsocks-libev  

### Q&A

1.  repository does not have release file.
Then, delete http://mirrors.163.com/raspbian......
2. apt-get update ; <font color=red>Hash Sum Mismatch</font>
sudo rm -rf /var/lib/apt/lists/*
Then, I ran
sudo apt-get update
sudo apt-get upgrade
everything ok.
3. <font color=red>NO_PUBKEY</font> 8B48AD6246925553 NO_PUBKEY 7638D0442B90D010
	1. gpg --keyserver pgpkeys.mit.edu --recv-key  8B48AD6246925553
gpg -a --export 8B48AD6246925553 | sudo apt-key add -
	2. gpg --keyserver pgpkeys.mit.edu --recv-key 7638D0442B90D010
gpg -a --export 7638D0442B90D010 | sudo apt-key add -
4. And finally to install letsencrypt:
apt-get <u>install -t jessie-backports letsencrypt</u>


##### End Sources.list



-------------------------------------




### [树莓派 Stretch9 最小化安装 PIXEL](https://linux.cn/article-9657-1.html)

1. sudo apt-get install xorg #安装X
2. sudo apt-get install lxde openbox #安装LXDE桌面 
3. sudo apt-get install raspberrypi-ui-mods #安装GUI服务 
4. reboot
5. <font color=red>sudo apt-get install rpi-chromium-mods #chromium browser, 迟 D 安装。</font>
6. sudo apt-get install iceweasel.<font color=red>安装 firefox</font>
7. sudo apt-get install pix-icons pix-plym-splash rpd-wallpaper #安装PIXEL样式 


OK, 大功告成，就是这么简单。
千万别忘了使用 raspi-config 设置卓面启动。

**Debian安装Chromium浏览器**

sudo apt-get update
sudo apt-get install chromium chromium-l10n


### End



---------------------------------------




# Network 

sudo vi /etc/network/interfaces

auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static 
address 192.168.1.3
netmask 255.255.255.0
network 192.168.1.0
gateway 192.168.1.1


<font color=red>20180430 最新方法</font>

sudo vi /etc/dhcpcd.conf
在最尾地方，安照它的提示，加入 static address.
以后不用再改 /etc/network/interfaces.

interface eth0
static ip_address=192.168.1.2/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.4

##### **Q&A**
20180510 there is no <font color=red>dhcpcd.conf</font> files on Debian9 ???

#### End Network 



-----------------------------------



### [禁用IPv6](https://linux.cn/article-3373-1-rel.html)

A) 方案1：
1. 编辑文件 - /etc/sysctl.conf
$ sudo gedit /etc/sysctl.conf
在文件的最后加入下面的行。
\# IPv6 disabled
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
保存并关闭
2. 重启sysctl
$ sudo sysctl -p
再次检查ifconfig的输出，这里应该没有IPv6地址了。

B) 方案2：禁用 IPv6 - GRUB 方案
1. IPv6同样可以通过编辑grub配置文件禁用。
$ sudo gedit /etc/default/grub
查找包含"GRUBCMDLINELINUX"的行，并如下编辑：
GRUB_CMDLINE_LINUX="ipv6.disable=1"
2. 同样可以加入名为"GRUBCMDLINELINUX_DEFAULT"的变量，这同样有用。保存并关闭文件，重新生成grub配置。
$ sudo update-grub2
重启，现在IPv6应该就已经禁用了。

### Reference

1. [Linux 局域网路由新手指南：第 1 部分](https://linux.cn/article-9657-1.html)

### End Disable IPv6




------------------------------------



### Usb Image Tool 要 net frame 不好用。

接下來設定時區，指令為：
 sudo dpkg-reconfigure tzdata

### End



------------------------------------------




### Hostname

1. 改 /etc/hostname file.
2. 改 /etc/hosts file.

### End


----------------------------------------



### Samba 

1. sudo apt-get install samba
sudo apt-get inatall samba-common-bin
2. /etc/samba/smb.conf
user = share
[share]
comment = shared file
path     = /home/pi/share/
browseable  = yes
public       = yes
writeable    = yes
create mask  = 0777
sudo /etc/init.d/samba restart
sudo service samba restart

##### End Samba



----------------------------------------



### mysql 5.5 主从配置

一)sudo apt-get install mysql-server

二)修改 mysql 的配置文件, sudo vi /etc/mysql/my.cnf
找到 bind-address = 127.0.0.1
改为 bind-address = 0.0.0.0
mysql的bind-address设置 2010-10-28
msyql默认的bind-address是127.0.0.1，这样的话就算你创建的用户有可以remote访问的话 也不能通过-h 来访问，mysql只接受localhost，
错误提示为：ERROR 2003 (HY000): Can't connect to MySQL server on 'localhost' (10061)

bind-address后面增加远程访问IP地址或者禁掉这句话就可以让远程机登陆访问了。

三)配置MySQL主服务器的my.cnf文件 
vi /etc/my.cnf #编辑配置文件，在[mysqld]部分添加下面内容 
1)server-id=22             #设置服务器id，ip 地址尾段 
2)log_bin=mysql-bin        #启动MySQ二进制日志系统，
注意: 这参数到底是自己加，还是 my.cnf 里参数？？？ 
3)binlog-do-db=test1       #需要同步的数据库名，如果有多个数据库，可重复此参数。
4)binlog-ignore-db=mysql   #不同步mysql系统数据库 
5)service mysqld restart     #重启MySQL 
6)mysql -u root -p          #进入mysql控制台
7)show master status; 查看主服务器，出现以下类似信息 
+------------------+----------+--------------+------------------+ 
| File | Position | Binlog_Do_DB | Binlog_Ignore_DB | +------------------+----------+--------------+------------------+ 
| mysql-bin.000019 | 7131 | test1 | mysql | +------------------+----------+--------------+------------------+ 
1 row in set (0.00 sec) 
注意：这里记住File的值：mysql-bin.000019和Position的值：7131，后面会用到。

四)配置MySQL从服务器的my.cnf文件 
1)vi /etc/mysql/my.cnf           #编辑配置文件，在[mysqld]部分添加下面内容 
2)server-id=44            #配置文件中已经有一行server-id=44 ip 尾段
3)log-bin=mysql-bin      #启动MySQ二进制日志系统，
注意：到底是自己加？ 还是 my.cnf 里的参数？？？
4)binlog-do-db=test1   #需要同步的数据库名，如果有多个数据库，可重复此参数，每个 数据库一行
5) binlog-ignore-db=mysql #不同步mysql系统数据库 
6) :wq! #保存退出
7) service mysqld restart     #重启MySQL 
注意：MySQL 5.1.7版本之后，已经不支持把master配置属性写入my.cnf配置文件中了，只需要把 同步的数据库和要忽略的数据库写入即可。 
8)mysql -u root -p                  #重新进入MySQL控制台 
9) mysql>slave stop;                #停止slave同步进程 
10)mysql>change master to 
master_host='192.168.21.169',
master_user='replication',
master_password='123456',
master_log_file='mysql-bin.000019' ,
master_log_pos=7131;             #执行同步语句 
slave start;                        #开启slave同步进程 
mysql>SHOW SLAVE STATUS\G      #查看slave同步信息，出现以下内容 


Slave_IO_State: Waiting for master to send event 
Master_Host: 192.168.21.169 
Master_User: osyunweidbbak 
Master_Port: 3306 
Connect_Retry: 60 
Master_Log_File: mysql-bin.000019 
Read_Master_Log_Pos: 7131 
Relay_Log_File: 
MySQLSlave-relay-bin.000002 
Relay_Log_Pos: 253 
Relay_Master_Log_File: mysql-bin.000019 
Slave_IO_Running: Yes 
Slave_SQL_Running: Yes 
Replicate_Do_DB: osyunweidb 
Replicate_Ignore_DB: mysql 
Replicate_Do_Table: 
Replicate_Ignore_Table: 
1 row in set (0.00 sec) 
注意查看： Slave_IO_Running: Yes 
          Slave_SQL_Running: Yes 
以上这两个参数的值为Yes，即说明配置成功！之后，自己检测  :-)


### Q&A

1)权限不够，因 mysql 自动生成时，/var/lib/mysql/ 的属性是 mysql.mysql.
2)chmod 0777 就可以解决问题。

Ubuntu下mysql5.5主从配置 (2012-09-14)
一、MySQL主服务器192.168.1.22
           从服务器 192.168.1.44
二、配置MySQL主服务器
     mysql -uroot -p      #进入MySQL控制台 
     create database test1; #建立数据库test1
     create table user(id (int(4), name varchar(10));
     inser into user values(1, 'henry');

     grant replication slave on *.* to 'replication'@'192.168.1.%' identified by '123456' ;

     flush privileges;

insert into mysql.user(Host,User,Password) values('localhost', 'replication', password('123456'));
  insert(Host,User,Password) values('localhost','osyunweiuser',
password('123456')); #创建用 户osyunweiuser #建立MySQL主从数据库
同步用户osyunweidbbak密码123456 
flush privileges; #刷新系统授权表 
授权用户osyunweidbbak只能从192.168.21.168这个IP访问
主服务器192.168.21.169上面的数据库，并且只具有数据库备份的权限 

三、把MySQL主服务器中的数据库 test1导入到MySQL从服务器
1. 导出数据库 test1
mysqldump -u root -p test1> test1.sql #在MySQL主服务器 进行操作，导出数据库
备注：在导出之前可以先进入MySQL控制台执行下面命令 flush tables with read lock; #数据库只读锁定命令，防止导出数据库的时候有数据写入 
unlock tables; #解除锁定 
2. 导入MySQL从服务器 
create database test1                        #从服务器增加 database test1
mysql -u root -p test1 < test1.sql 
mysql -h192.168.1.22 -ureplication -p123456  #测试在从服务器上登录到主服务器


### End



-------------------------------------------------------------




### tightvncserver

1. sudo apt-get install tightvncserver
sudo vncserver :1 -geometry 1024x768 -depth 24，以上是以 root 自行， 其他 user，remove 'sudo'.
以上是一次性运行，开机自动运行自己处理。
2. Password:abcd1234
3. client:
	1. sudo apt-get install xtightvncviewer.
	2. 192.168.1.2:5901, 5901 是第 1 援冲区，如此类推。


###### <font color=red>x11vnc 可以直接在Mon 上控制电脑</font>
1. apt-get install x11vnc.
2. server : x11vnc -display :0
3. 装个VNC client : 192.168.1.x:0 完成。

### End



-----------------------------------------------------------




### 中文显示安装

中文显示
安装locale

1. 第一步，先为终端进行相关更新： sudo apt-get update 
2. 第二步：为我们debian系统安装中文字库： sudo apt-get install ttf-wqy-zenhei
3. 第三步：我们可以更改系统中的菜单界面，将其变成中文的，

指令是：sudo dpkg-reconfigure locales 我们用空格键勾选前面带有 “zhCN” 的选项，
这些表示是中文字库。 但是要确保 “zhCN.UTF-8” 被选中，同使在选local字库时
选择“zh_CN.UTF-8”

**20180430 参照下面设定**

**中文输入法的安装**
第一步：我们先进行scim的安装： sudo apt-get install scim.
第二步：安装中文scim表格： sudo apt-get install scim-tables-zh 
第三步：安装中文拼音： sudo apt-get install scim-pinyin


### End 中文显示安装



----------------------------------------------------------




### CUPS 

**配置用户**

1. sudo apt-get install cups  #20130219 安装指令
2. sudo lpinfo -v
3. sudo lpstat -t
4. 把 pi 用加到 lpadmin，<font color=red >sudo usermod -a -G lpadmin pi</font>
5. <font color=red>server printer set 好，client 那边就自动显示出来，不用重新 setting</font>


### End Cups


------------------------------------------


### OwnCloud Start

OwnCloud-10.0.8 创建私有云

A)更新树莓派系统
        sudo apt-get update
        sudo apt-get upgrade

B)安装LAMP环境:
        sudo apt-get install apache2 mariadb-server libapache2-mod-php7.0 \ 
			php7.0-gd php7.0-json php7.0-mysql php7.0-curl \
			php7.0-intl php7.0-mcrypt php-imagick \
			php7.0-zip php7.0-xml php7.0-mbstring

C)sudo mysql_secure_installation


D)sudo mysql -uroot -pr1o2o3t
  Create MySQL Database and User

	mysql> CREATE DATABASE owncloud;
	mysql> GRANT ALL ON owncloud.* to 'henry'@'192.168.1.%' IDENTIFIED BY 'henry123';
	mysql> grant all on owncloud.* to 'henry'@'localhost' identified by 'henry123';
	mysql> FLUSH PRIVILEGES;
	mysql> quit

E) May 15, 2018 最新版本 owncloud-10.0.8.tar.bz

1. 下载最新版ownCloud-10.0.8.tar.bz2
	wget https://download.owncloud.org/community/owncloud-10.0.8.tar.bz2
2. 用命令解压tar压缩包：
tar xvf owncloud-10.0.8.tar.bz2
3. 移动解压后的目录到你的 /var/www/html/owncloud
$sudo mv -r -v owncloud/ /var/www/html/owncloud
4. $cd /var/www/html
$sudo chown -R www-data:www-data owncloud
$sudo chmod -R 755 owncloud
5. 修改 trusted_domains
sudo vi /var/www/html/owncloud/config/config.php
'trusted_domains' ==>
	array (
	0 => 'localhost',
	1 => '192.168.1.8',<font color=red>必须加上自己地址才能访问</font>
	}
6. 当 owncloud 配置完，在 owncloud download page, install owncloud-client and follow the install manual.

**Contact Sync**

1. download <font color=red>DavDroid apk</font> from [F-Droid](https://f-droid.org/packages/at.bitfire.davdroid/)
2. 在 Davdroid 界面，增加账户---> 使用 URL 和用户名登录。
	1. 根地址：http://192.168.1.6/owncloud/remote.php/dav
	2. 用户名：henry
	3. 密码 ： henry123
3. 从 server 新增联系人，可以同步到手机。
4. 先把手机联系人变成 xxx.vcf file, >= version4.0, 然后 import 到 server Contacts.
5. 再同步到手机联系人。

#### END




------------------------------------




![dnsmasq](/home/pi/rpi/dnsmasq.jpg "dnsmasq 标志")

### Dnsmasq

1. Dnsmasq 提供 DNS 缓存和 DHCP 服务功能。
作为域名解析服务器(DNS)，dnsmasq可以通过缓存 DNS 请求，来提高对访问过的网址的连接速度。作为DHCP 服务器，dnsmasq 可以用于为局域网电脑分配内网ip地址和提供路由。DNS和DHCP两个功能可以同时或分别单独实现。dnsmasq轻量且易配置，适用于个人用户或少于50台主机的网络。此外它还自带了一个 PXE 服务器。

2. Dnsmasq的主要作用：
	1. 将Dnsmasq作为本地DNS服务器使用，直接修改电脑的本地DNS的IP地址即可。
	2. 应对ISP的DNS劫持（反DNS劫持），输入一个不存在的域名，正常的情况下浏览器是显示无法连接，DNS劫持会跳转到一个广告页面。先随便nslookup 一个不存在的域名，看看ISP商劫持的IP地址。
	3. 智能DNS加快解析速度，打开/etc/dnsmasq.conf文件，server=后面可以添加指定的DNS，例如国内外不同的网站使用不同的DNS。
	
    国内指定DNS：
server=/cn/114.114.114.114
server=/taobao.com/114.114.114.114
server=/taobaocdn.com/114.114.114.114
	
    国外指定DNS
server=/google.com/223.5.5.5

3. 屏蔽网页广告，将指广告的URL指定127这个IP，就可以将网页上讨厌的广告给去掉了。
address=/ad.youku.com/127.0.0.1
address=/ad.iqiyi.com/127.0.0.1

5. 指定域名解析到特定的IP上。这个功能可以让你控制一些网站的访问，非法的DNS就经常把一些正规的网站解析到不正确IP上。
例如：address=/freehao123.com/123.123.123.123

6. 管理控制内网DNS，首先将局域网中的所有的设备的本地DNS设置为已经安装Dnsmasq的服务器IP地址。然后修改已经安装Dnsmasq的服务器Hosts文件：/etc/hosts，指定域名到特定的IP中。

例如想让局域网中的所有用户访问www.freehao123.com时跳转到192.168.0.2，添加：192.168.0.2 www.freehao123.com在Hosts文件中既可，整个过程也可以说是“DNS劫持”。


#### dnsmasq的解析流程

1. dnsmasq先去解析本机hosts文件，
2. 再去解析/etc/dnsmasq.d/下的*.conf文件，
3. 并且这些文件的优先级要高于dnsmasq.conf，我们自定义的resolv.dnsmasq.conf中的DNS也被称为上游DNS，这是最后去查询解析的；

如果不想用hosts文件做解析，我们可以在<font color=red>/etc/dnsmasq.conf中加入no-hosts</font>这条语句，这样的话就直接查询上游DNS了，如果我们不想做上游查询，就是不想做正常的解析，我们可以加入<font color=red>no-reslov</font>这条语句。



##### 安装

1. sudo apt-get install -y dnsmasq
  sudo apt-get install dnsutils
2. nameserver 主要在 /etc/resolv.conf
3. resolv.dnsmasq.conf 是放 dnsmasq 找不到 nameserver 时，往上层找 nameserver.
4. resolvconf.conf 只会产生1条 nameserver
sudo resolvconf -u

**配置DNSmasq**

sudo mv dnsmasq.conf resolv.dnsmasq.conf
Dnsmasq的配置文件是放在 /etc/dnsmasq.conf 中
打开编辑，配置：
i) resolv-file=/etc/resolv.dnsmasq.conf，表示dnsmasq 会从这个指定的文件中寻找上游dns服务器。同时取消 
ii) strict-order 前面的注册#号。
检查一下
iii) no-hosts前面是不是已经有了#号，默认的情况下是有的，dnsmasq 会首先寻找本地的 hosts 文件再去寻找缓存下来的域名, 最后去上游dns 服务器寻找。

vii) cache-size=4096 设置缓存大小
viii) log-queries 开启debug模式，记录客户端查询记录到/var/log/debug中

2) 测试DNSmasq
nslookup www.12306.cn
可以显示dns 工作否。

在客户机修改 resolv.conf 将nameserver设置为192.168.1.3
nameserver 192.168.1.3
linux使用dig命令测试
dig <font color=red>\*host not domain*</font>是主机不是网络
dig www.google.com
......
;; Query time: 205 msec
;; SERVER: 192.168.1.3#53(192.168.1.3)
;; WHEN: Sun Apr 13 17:39:03 2014
重启dnsmasq即可，我们可在局域网另外一个机器用dig命令测试。
dig gateway

; <<>> DiG 9.8.4-rpz2+rl005.12-P1 <<>> gateway
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 43215
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;gateway.            IN    A

;; ANSWER SECTION:
gateway.        0    IN    A    192.168.0.1

;; Query time: 2 msec
验证服务器已启动
[root@master ~]# netstat -tunlp | grep 53
tcp 0 0 0.0.0.0:53 0.0.0.0:* LISTEN 10246/dnsmasq
udp 0 0 0.0.0.0:53 0.0.0.0:* 10246/dnsmasq
确认服务启动后，就可以将客户端PC的DNS服务器指向dnsmsq服务器（注意iptables），可以正常访问网络页面为正常！

5.测试
[root@cn-ptmind ~]# dig www.ptmind.com
中间省略。。。。。
;; Query time: 50 msec #首次查询域名使用50Mms！！！！
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Tue Oct 8 12:51:50 2013
;; MSG SIZE rcvd: 48
[root@cn-ptmind ~]# dig www.ptmind.com
中间省略。。。。。
;; Query time: 0 msec #再次查询域名使用0Mms，说明已经缓存！！！！！！！！
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Tue Oct 8 12:51:53 2013
;; MSG SIZE rcvd: 48


##### Q&A

1. 查看配置文件语法是否正确，可执行下列命令
[root@localhost ~]# dnsmasq --test
dnsmasq: syntax check OK.


### End DNSmasq


------------------------------------------------------


### nfs-kernel-server安装与配置

Debian or Raspbian: nfs-kernel-server not starting portmapper is not running
作者: lesca 分类: Tutorials 发布时间: 2016-05-04 21:08

Error Message
Debian or Raspbian: nfs-kernel-server not starting portmapper is not running … (warning) rpcbind.target

Fix Steps                                                            
Here is my first try, but it doesn’t work for me. It just reset the configs. So if you messed it up, try this first.

apt-get purge rpcbind nfs-kernel-server nfs-common                       
apt-get install nfs-kernel-server                                          

Now check the service startup dependencies by command below. And make sure you find rpcbind before nfs service.

systemctl list-dependencies nfs-kernel-server.service                      

If it is not, unfortunately you should try purge and install them again 
as mentioned above, which should fixes the dependency issue and will also 
remove the config files, like /etc/exports. Backup it in advance if necessary!
 
Next, I have a look into /etc/init.d/nfs-kernel-server and find its 
start level is 2 3 4 5. However, nfs-common and rpcbind have differenct 
run level, I change it to the same, i.e. 2 3 4 5.

Have a look at these files' runlevel                                      
/etc/init.d/nfs-kernel-server                                             
/etc/init.d/nfs-common                                                 
/etc/init.d/rpcbind                                                      

This is the runlevel of nfs-kernel-server

\# BEGIN INIT INFO                                                   
\# Provides:          nfs-kernel-server                                   
\# Required-Start:    $remote_fs nfs-common $portmap $time              
\# Required-Stop:     $remote_fs nfs-common $portmap $time             
\# Should-Start:      $named                                            
\# Default-Start:     2 3 4 5                                             
\# Default-Stop:      0 1 6                                               
\# Short-Description: Kernel NFS server support                             
\# Description:       NFS is a popular protocol for file sharing across        
\#                    TCP/IP networks. This service provides NFS server    
\#                    functionality, which is configured via the             
\#                    /etc/exports file.                                  

\### END INIT INFO                                                    

Then try to update-rc.d the changed init scripts with defaults. First try fails. The trick is to remove and add them again.

update-rc.d -f rpcbind remove         
update-rc.d rpcbind defaults                                             
update-rc.d -f nfs-common remove                                       
update-rc.d nfs-common defaults                                        
update-rc.d -f nfs-kernel-server remove                                   
update-rc.d nfs-kernel-server defaults                                     

以上命令行发生 errors, 重新再做一次。直至 no errors。
sudo vi /etc/exports;  sudo reboot


After that, check the order of the services. It should be rpcbind, nfs-common, and nfs-kernel-server.
Reboot the server, it works for me now! Cheers!


### End




-------------------------------------------------------------




![vsftp](/home/pi/rpi/vsftp.jpg)

### vsftp

1)apt-get install vsdtpd.
2)在 /etc/vsftpd.conf, uncomment write_enable=yes  done.
3)sudo reboot. done
3)sudo reboot. done
3)sudo reboot. done

### End vsftp




---------------------------------------------



### Systemd

1. <font color=red>Debian9</font>, system 中的 systemd 预设放在 /lib/systemd/system/ 中。
2. systemd 这个启动服务的机制，主要是通过一只名为 systemctl 的指令来处理的 
4. user 在 /etc/systemd/system/shadowsocks.service. 
5. 平时 apt install mysql，mysql.service 留在 /etc/systemd/system/中。



$ sudo systemctl  enable  shadowsocks-libev.service 
Created symlink <font color=red>/etc/systemd/system/multi-user.target.wants</font>/shadowsocks-libev.service → /lib/systemd/system/shadowsocks-libev.service.



### End Systemd



----------------------------------------------



## Shadowsocks-libev

1. raspberry pi B, 不能安装 shadowsocks-libev, 因其架构不成，要 armv6, >=B+ 就可以。
2. shadowsocks-python-pip ,都装不了。
3. 要等新版 debian 出来，再试试 :-( 。


![shadowsocks](/home/pi/rpi/shadowsocks.png)

&emsp;&emsp;pc computer  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;  Google/Facebook
&emsp;&emsp;&emsp;&emsp;  ||  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;||
&nbsp;1)Reques || 6)Response  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;  3)Request || 4)Response
&emsp;&emsp;&emsp;&emsp;  ||  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;||
&emsp;&emsp;SS Local ----- 2)Encrypt Request----- Great Wall ---------------------------------> SS Server
&emsp;&emsp;SS Local <------------------------------- Great Wall ----- 5)Encrypt Response ----- SS Server

**shadowsocks 原理**

如上图， shadowsocks 的原理很简单，只需要在 GFW 两端各自部署一个代理节点。 境外的节点为 SS Server ，下文称为 服务端 ； 境内的节点为 SS Local ，下文称为 本地端 ； 上网的 PC 或者移动设备等，则统一称为 客户端 ； SS Local 可以是一台独立的服务器，也可以是 PC 或移动设备上一个应用进程。

SS Server 运行一个后台服务， SS Local 也运行一个后台服务。 两个服务通过 TCP 相连并交换数据，数据采用加密算法加密。 这相当于，在一堵墙上打了一个洞——加密隧道。这样一来：

    真正的请求在 SS Server 发起，不受到 GFW 域名污染；
    SS Server 的 IP 不在 GFW 黑名单内，便绕过了 IP 封杀；
    经过加密的报文，GFW 读不懂，便不会被过滤了；

再来看看，经过 shadowsocks 转发的一次请求如何进行。完整步骤如下：

1. 客户端 发起的请求，被代理到 本地端 ；
2. 请求通过加密隧道到达 服务端 ；
3. 服务端 向目标服务器(如 Google)发起请求；
4. 目标服务器返回响应；
5. 服务端 通过加密隧道回传响应内容；
6. 本地端 向 客户端 返回响应；

虽然饶了一大圈，但总算达到目的了。


**安装 shadowsocks, python-pip**

1. sudo apt-get install python-pip
2. sudo pip install shadowsocks
3. sudo vi config.json
{
    "server":"185.186.146.62",
    "server_port":8388,
    "local_address": "192.168.1.4",
    "local_port":1080,
    "password":"abcd1234",
    "timeout":300,
    "method":"aes-256-cfb"
}


**sudo vi /etc/systemd/system/shadowsocks.service**

[Unit]
Description=Shadowsocks

[Service]
TimeoutStartSec=0
ExecStart=/usr/local/bin/sslocal -c /home/pi/shadowsocks.json

[Install]
WantedBy=multi-user.target

sudo systemctl enable shadowsocks
sudo systemctl start shadowsocks
sudo reboot

#### 安装 shadowsocks-libev

A) jessie 用 stretch 库，安装 shadowsocks-libev

1. sh -c 'printf "deb http://ftp.debian.org/debian stretch-backports main" > /etc/apt/sources.list.d/jessie-backports.list'  
2. sudo apt update  
3. sudo <font color=red>apt -t stretch-backports</font> install shadowsocks-libev  

B) <font color=red>server</font> 配置
pi@ck32$ cat hi.json
{
    "server":"107.172.6.122",
    "server_port":8488,
    "local_port":1080,
    "password":"abcd1234",
    "timeout":60,
    "method":"chacha20-ietf-poly1305"
}

C) <font color=red>client</font> 配置
pi@ck32$ cat hi.json
{
    "server":"107.172.6.122",
    "server_port":8488,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"abcd1234",
    "timeout":60,
    "method":"chacha20-ietf-poly1305"
}

D) 编写 systemd scripts:

1. 在 /lib/systemd/system/ 下编写，
2. 安装 shadowsocks-libev 时，已经写好 systemd-scripts.

[Unit]
Description=Shadowsocks

[Service]
TimeoutStartSec=0
ExecStart=/usr/local/bin/ss-local -c /etc/shadowsocks-libev/%i.service

[Install]
WantedBy=multi-user.target

sudo systemctl start shadowsocks-libev-local@hi.service
And enable auto-start at boot time.

sudo systemctl enable shadowsocks-libev-local@location-of-your-server.service
Check its status. Make sure it’s running.

systemctl status shadowsocks-libev-local@location-of-your-server.service

Now the ss-local process listens on 127.0.0.1:1080 on your Ubuntu desktop and it’s connected to your Shadowsocks server.

D) 启动 server

1. systemctl start shadowsocks-libev.service
2. systemctl enable shadowsocks-libev.service


### Remarks

&nbsp;<font color=blue>多重的重复设置方式 @ </font>：以 shadowsocks-libev 为例：

1. /lib/systemd/system/shadowsocks-libev-server<font color=red>@hi</font>.service，与配置文件<font color=red>%i</font>相呼应。
[Service]
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
ExecStart=/usr/bin/ss-server -c /etc/shadowsocks-libev/%i.json
2. %i 与 %I 是相同的，它会到 /etc/shadowsocks-libev/ 寻找对应文件，方便重复设置。
3. 不论是 server, 还是 client, 都可以用以上方法去设定。
4. [鸟哥的 Linux 私房菜 第四版 17.3 systemctl 针对 service 类型的配置文件](https://wizardforcel.gitbooks.io/vbird-linux-basic-4e/content/150.html)

### Q&A

1. 用 shadowsocks-libev 试一下，好像快很多：-）
2. Go to http://dnsleaktest.com You will see your Shadowsocks server’s IP address, which indicates that your proxy is working.
3. [root@study ~]# systemctl show getty.target
\# 那个 show 的指令可以将 getty.target 的默认设置值也取出来显示！





### End Shadowsocks-libev



------------------------------------------------



## <font color=orange>Vim Start 添加 python3 和 python2.7 支持</font>

[vim 添加 python3 支持](https://blog.csdn.net/u012587734/article/details/78572355)

[Vim 与 Python 真是天作之合](http://codingpy.com/article/vim-and-python-match-in-heaven/)


##### <font color=red>No Terminal Library Found when Compiling Vim</font>

I think you should install a ncurses-dev library.
you can do so by running sudo apt-get install libncurses5-dev libncursesw5-dev


### Remove old-vim

1.sudo apt-get remove vim
2.sudo apt-get remove vim-runtime
3.sudo apt-get remove vim -tiny
4.sudo apt-get remove vim-common

### vim install on source code

看看 $PATH 变数  
pi@dell7:env

git clone https://github.com/vim/vim.git
cd vim/src
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp=yes \
            --enable-pythoninterp=yes \
            --with-python-config-dir=/usr/lib/python2.7/config \
            --enable-python3interp=yes \
            --with-python3-config-dir=/usr/lib/python3.5/config \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-gui=gtk2 --enable-cscope \
            --prefix=/usr/local/vim8

 记得创建prefix目录。和找对python安装路径

sudo make
sudo make install


添加完成。但是还没有进入到环境变量中。可以自行添加。也可以设置：

sudo update-alternatives --install /usr/bin/editor editor /usr/local/vim8/bin/vim 1
sudo update-alternatives --set editor /usr/local/vim8/bin/vim
sudo update-alternatives --install /usr/bin/vim vim /usr/local/vim8/bin/vim 1
sudo update-alternatives --set vim /usr/local/vim8/bin/vim


### debian中修改crontab默认编辑器为vim

root@fyhqy:~# update-alternatives --config editor

有 3 个候选项可用于替换 editor (提供 /usr/bin/editor)。

  选择       路径              优先级  状态

* 0            /bin/nano            40        自动模式
  1            /bin/nano            40        手动模式
  2            /usr/bin/vim.basic   30        手动模式
  3            /usr/bin/vim.tiny    10        手动模式

要维持当前值[*]请按回车键，或者键入选择的编号：2
update-alternatives: 使用 /usr/bin/vim.basic 来提供 /usr/bin/editor (editor)，于 手动模式 中。



### 建立 .vimrc 文件:

	set backspace=2         "可随时用退格键删除
	set autoindent          "自动缩排
	set ruler               "可显示最后一行的状态
	set showmode            "左下角那一行的状态
	set nu                  "可以在每一行的最前面显示行号啦！
	set bg=dark             "显示不同的底色色调
	syntax on               "进行语法检验，颜色显示。


### vim 插件有3种方法：（由老至新)

1. pahtogen
2. .vim/bundle/
:PluginInstall
3. Vim-plug .vim/autoload
:PlugInstall

### Q&A

1. check :vim --version, only +python appear, -python3 no change???

### [Vim-plug](https://github.com/junegunn/vim-plug)

**Installation**

curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

**Usage**

Add a vim-plug section to your ~/.vimrc:

1. Begin the section with call plug#begin()
2. List the plugins with Plug commands
3. call plug#end() to update &runtimepath and initialize plugin system
	1. Automatically executes filetype plugin indent on and syntax enable. You can revert the settings after the call. e.g. filetype indent off, syntax off, etc.

### <font color=purple size=3>Example: A small sensible Vim configuration</font>

call plug#begin()
Plug 'tpope/vim-sensible'
call plug#end()


Reload .vimrc and :PlugInstall to install plugins.


### End

-------------------------------------------------


### [iamcco/markdown-preview.vim](https://github.com/iamcco/markdown-preview.vim)

##### Installation with vim-plug

add Plug 'iamcco/markdown-preview.vim' to the vimrc and type :PlugInstall

Plug 'iamcco/mathjax-support-for-mkdp'
Plug 'iamcco/markdown-preview.vim'


###  End markdown-preview


---------------------------------------------------



### Netselect Begin

树莓派笔记之使用netselect选择最快Raspbian软件源

A)安装netselect

  sudo apt-get install netselect
  运行需要root权限,请使用sudo.此外也有一个netselect-apt,可以看看

B)下载我做的脚本文件

  git clone https://github.com/sjqlwy/ccrm.git
  cd ./ccrm
  运行sudo sh ccrm.sh即可以显示最好的3个源，根据自己需求修改/etc/apt/sources.list。一般格式为

  deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ wheezy main non-free contrib
  修改方式可参考https://lug.ustc.edu.cn/wiki/mirrors/help/raspbian
  其中crm是官方国内源列表，ccrm.sh里我设置好了比较通用的参数。

  更多信息请访问软件主页http://apenwarr.ca/netselect/

  软件详细参数请打开nsREADME

  注意：清华源即将下线

  建议删除sources.list.d/raspi.list,里面包含了archive.raspbian.org

  这个软件源主要多了armel的支持，对于Pi 2（armhf）是没必要的，

  可以备份删除该文件并换用比较全的源以加速更新（个人观点，希望指出错误）。

  更新2015-4-25：添加阿里，搜狐源；补全官方亚洲源。

  更新2015-4-27：搜狐源不全，阿里源似乎可以取代archive.raspbian.org了

  更新2017-2-25：archive.raspbian.org国内目前有ustc替代，修改/etc/apt/sources.list.d/raspi.list

### Netselect End 



---------------------------------------------------------



### Raspbian Stretch 9

设定声音和resolution

1)把 /boot/config.txt
disable_overscan=1  #uncomment
hdmi_group=1
hdmi_mode=31
hdmi_driver=1
就可以没声。





##### [Debian 9 Mate桌面如何安装Fcitx五笔拼音输入法 配置fcitx五笔拼音输入法](https://www.linuxdashen.com/debian-9-mate%E6%A1%8C%E9%9D%A2%E5%A6%82%E4%BD%95%E5%AE%89%E8%A3%85fcitx%E4%BA%94%E7%AC%94%E6%8B%BC%E9%9F%B3%E8%BE%93%E5%85%A5%E6%B3%95)
发布于2017-06-24 由Linux魔法师

这篇教程讲解如何在Debian 9 Mate桌面上安装Fcitx五笔拼音输入法。五笔拼音输入法既可以让你打五笔，又可以打拼音。如果不会打五笔，就打拼音，它会教你五笔怎么打，非常方便。

**Debian 9 Mate安装fcitx五笔拼音输入法**

首先打开一个终端窗口 （Terminal），登录为root用户。

su -

然后输入下面的命令以更新本地软件包索引，并安装fcitx输入法框架以及fcitx五笔拼音输入法。

apt update
apt install fcitx fcitx-table-wbpy fcitx-config-gtk

**配置fcitx五笔拼音输入法**

上面的apt install命令完成后，重新登录系统，这样是为了检测新安装的输入法。不重新登录的话，你就找不到Fcitx五笔拼音输入法。重新登录后，以普通用户在终端里输入下面的命令打开fcitx输入法配置窗口。

fcitx-config-gtk3

点击输入法配置窗口左下角的加号按钮以添加中文输入法。

然后，在新的窗口中，去掉只显示当前语言（Only Show Current Language）的勾。在列表中选中五笔拼音输入法。我用英文版的Debian 9 Mate系统，WubiPinyin在列表的最下方。如果你用中文版，那么可能在列表的其他位置。

点击确认（OK）按钮后，就能使用Ctrl+空格键调出Fcitx五笔拼音输入法了。

细心的童鞋可能会发现我的Debian 9使用的是Ubuntu的 Ambiance 主题。说明一下这是Debian 9系统，不是Ubuntu。以上就是Debian 9安装Fcitx五笔拼音输入法的步骤。

B)中文输入法 1/2
1)sudo apt-get install fcitx fctix-googlepinyin fctix-module-cloudpinyin fctix-sunpinyin
2)sudo reboot
Ba)中文输入法 2/2
1)sudo apt-get install ttf-wqy-zenhei
2)sudo apt-get install scim-pinyin, done.

C)Static ip address
a)no need edit /etc/network/interfaces file.
b)edit /etc/dhcpcd.conf, add static netmask 255.255.255.0 , done


#### Q&A

1. 安装 stretch-lite 后，boot-time over 1min 35.763s ？？？

### End Stretch 9



-----------------------------------------------------



### [Git](https://git-scm.com/book/zh/v1/%E8%B5%B7%E6%AD%A5)

安装：
sudo apt-get install git

Config：
1. $ git config --global user.name "Your Name"
2. $ git config --global user.email "email@example.com"
因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。
--global 是全局设定，可以不用。

创建版本库
什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，
这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，
以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：

\$ mkdir git
\$ cd git
\$ git init

瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），
细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，
没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。


### 添加远程库

1）在 github 加一个 account。
现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，
并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，
又可以让其他人通过该仓库来协作，真是一举多得。

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

在GitHub的提示，在本地的learngit仓库下运行命令：

$ git remote add origin git@github.com:michaelliao/learngit.git
请千万注意，把上面的michaelliao替换成你自己的GitHub账户名，否则，
你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，
因为你的SSH Key公钥不在我的账户列表中。

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

###### <font color=red>配置Git</font>

首先在本地创建ssh key；
1. $ ssh-keygen -t rsa -C "name@126.com"
2. 把 .ssh/id-ras.pub copy 到 github.com/personal file/setting 中， ok.
3. 验证链接是否成功输入：
$ ssh -T git@github.com

$<font color=red>如果每次 git push, 要求输入 username, 更改以下设置：</font>
在 /.git/config 中
	url = https://ck32:henry123@github.com/ck32/rpi7.txt

拉出：git pull--------------git clone https://github.com/yck32/rpi.<font color=red>git</font>
推送：git push

### 显示情性访
1. <font color=blue>@@ -1,4 +1,4 @@</font> 此列为状态列，
2. 1. <font color=red>-abbbbbbb</font>减号，红色代表 delete.
3. <font color=green>+bbbbbbb</font>加号，绿色代表 append.
4. 白色，代表本文，以示对照。

### End Git


-------------------------------------------------------


## <font color=blue>Node.js 和 npm</font>

Debian9安装最新版Nodejs和NPM
首先，您需要在我们的系统中由Nodejs官方网站提供node.js PPA。如果尚未安装，我们还需要安装python-software-properties软件包。您可以选择安装最新的Node.js版本或LTS版本。

最新版安装命令：

curl -sL https://deb.nodesource.com/setup_9.x | sudo bash -

安装LTS长期维护版：

apt-get install curl python-software-properties
curl -sL https://deb.nodesource.com/setup_8.x |  bash -

二、安装Node.js和NPM

添加所需的PPA文件后，可以安装Nodejs包。NPM也将与node.js一起安装。该命令还会在您的系统上安装许多其他相关软件包。

apt-get install nodejs

三、检查Node.js和NPM版本

安装node.js后，验证并检查安装的版本。你可以在node.js 官方网站上找到关于当前版本的更多细节。

检查Node.js版本
node -v

检查npm版本
npm -v

## End


----------------------------------------------------------



### 查看 Linux 發行版和版本号

1)sudo lsb_release -a
2)cat /etc/*-release
3)cat /etc/os-release
4)uname -a
5)cat /proc/version
6)sudo dmesg | grep Linux


-------------------------------------------


### [Debian9安装最新版Nodejs和NPM](https://www.5yun.org/15395.html)

Node.js是一个基于Chrome V8 JavaScript引擎构建的平台.Nodejs可用于轻松构建快速，可
扩展的网络应用程序。最新版本node.js ppa由其官方网站维护。我们可以将这个PPA添加到
Debian 9（Stretch） Debian 8（Jessie）和Debian 7（Wheezy）系统中。这篇我抄来的文
章可以帮助你在Debian 9/8/7系统上安装最新的Nodejs和NPM。

1. 添加Node.js PPA
> curl -sL https://deb.nodesource.com/setup_9.x | sudo bash -
2. 安装Node.js和NPM
> apt-get install nodejs
3. 检查Node.js和NPM版本
	1. node -v
	2. npm -v


------------------------------------------


### <font color=blue>Root file system requires manual fsck</font>

1. boot to the GRUB menu
2. choose Advanced Options
3. choose Recovery mode
4. at the prompt, type <font color=red>fsck -yf / or sudo fsck -f /dev/sda1</font>
5. repeat the fsck command if there were errors
6. type reboot

### End



-----------------------------



### [haroopad](http://pad.haroopress.com)
[add](http://pad.haroopress.com)

##### installation

sudo dpkg -i haroopad-v0.13.1-ia32.deb ------> done

**Q&A**

1. 标签 <font color=red>font</font> , 不能放在每句开头。
2. &nbsp之前，可以用 font.

### End



---------------------------------


### Generating locales

sudo locale -a

Missing locales are generated with locale-gen:

locale-gen en_US.UTF-8

Alternatively a locale file can be created manually with localedef:[1]

localedef -i en_US -f UTF-8 en_US.UTF-8

Setting Locale Settings

The locale settings can be set (to en_US.UTF-8 in the example) as follows:

export LANGUAGE=en_US.UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
locale-gen en_US.UTF-8
dpkg-reconfigure locales

Make sure you updated /etc/default/locale correctly. Then you could just source /etc/default/locale after running locale-gen.


### End



---------------------------------------




### Raspberry PI install Asterisk 15

A) Install:

sudo apt-get install -y gcc make perl
sudo apt-get install -y libxml2 libxml2-dev
sudo apt-get install -y speex libspeexdsp-dev libspeex-dev ncurses-dev bison openssl libssl-dev sqlite3 libsqlite3-dev
sudo apt-get install -y libncurses5-dev subversion git-core libjansson-dev uuid-dev build-essential libsrtp0-dev

wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-15-current.tar.gz
tar zxvf asterisk-15-current.tar.gz
cd asterisk-15.0.5 (Path 會改的)
./configure
make menuselect
make -j 4 (用4個 core, for Raspberry Pi 2 ) / make (Raspberry Pi )<font color=red>耗时 >=3小时</font>
sudo make install
sudo make samples
sudo make config

### 簡單的dialplan

cd /etc/asterisk
vi extensions.conf 加在最後面

[mycontext]
exten => _2XXX,1,Answer()
exten => _2XXX,n,NoOP(exten=${EXTEN})
exten => _2XXX,n,Dial(SIP/${EXTEN})
exten => _2XXX,n,Hangup

vi sip.conf 加在最後面

[2001]
type = friend
context=mycontext
callerid = User One <2001>
secret = secret12345
host = dynamic
canreinvite = no
dtmfmode = rfc2833
mailbox = 2001
disallow = all
allow = ulaw,speex,ilbc
transport = udp

[2002]
type = friend
context=mycontext
callerid = User Two <2002>
secret = secret12345
host = dynamic
canreinvite = no
dtmfmode = rfc2833
mailbox = 2002
disallow = all
allow = ulaw,speex,ilbc
transport = udp

### Remarks

0) adduser asterisk
Asterisk is running with "asterisk" and I have done the below steps:

sudo adduser asterisk
sudo chown asterisk. /var/run/asterisk
sudo hown -R asterisk. /etc/asterisk
sudo chown -R asterisk. /var/{lib,log,spool}/asterisk
sudo chown -R asterisk. /usr/lib64/asterisk

1)/etc/asterisk.conf, uncomment following:
runuser = asterisk
rungroup = asterisk

2)At last, run asterisk -rvvv

done!


### END




### ArclinuxARM

1. Start fdisk to partition the SD card:
fdisk /dev/sdX

2. At the fdisk prompt, delete old partitions and create a new one:
	1. Type o. This will clear out any partitions on the drive.
	2. Type p to list partitions. There should be no partitions left.
	3. Type n, then p for primary, 1 for the first partition on the drive, press ENTER to accept the default first sector, then type +100M for the last sector.
	4. Type t, then c to set the first partition to type W95 FAT32 (LBA).
	5. Type n, then p for primary, 2 for the second partition on the drive, and then press ENTER twice to accept the default first and last sector.
	6. Write the partition table and exit by typing w.
3. Create and mount the FAT filesystem:
    mkfs.vfat /dev/sdX1
    mkdir boot
    mount /dev/sdX1 boot

4. Create and mount the ext4 filesystem:
    mkfs.ext4 /dev/sdX2
    mkdir root
    mount /dev/sdX2 root

5. Download and extract the root filesystem (as root, not via sudo):
    wget http://os.archlinuxarm.org/os/ArchLinuxARM-rpi-latest.tar.gz
    bsdtar -xpf ArchLinuxARM-rpi-latest.tar.gz -C root
    sync

	1. sudo apt install automake
	2. sudo apt install libtool
	3. wget https://www.libarchive.org/downloads/libarchive-3.3.1.tar.gz
	4. tar xzf libarchive-3.3.1.tar.gz
	5. cd libarchive-3.3.1
	6. ./build/autogen.sh
	7. ./configure
	8. make
	9. sudo make install

6. Move boot files to the first partition:
    mv root/boot/* boot
	cd boot; vi boot.txt
    hdmi_group=1
    hdmi_mode=16
    hdmi_drive=1

7. Unmount the two partitions:
    umount boot root
8. Insert the SD card into the Raspberry Pi, connect ethernet, and apply 5V power.
9. Use the serial console or SSH to the IP address given to the board by your router.
	. Login as the default user alarm with the password alarm.
    . The default root password is root.
10. Initialize the pacman keyring and populate the Arch Linux ARM package signing keys:
    pacman-key --init
    pacman-key --populate archlinuxarm

