34-配置本地Yum源



配置本地Yum源

* Why？为什么需要配置本地源
  * 封闭式开发
  * 军工类项目
  * 没有外部网络

* How？怎么配置本地源



repo本地目录源：

mount /dev/cdrom /mnt

 

baseurl=file:///mnt

gpgcheck=0

enable=1

 

yum clean all

yum makecache

yum repolist



```shell
[root@node0924 yum.repos.d]# mount /dev/cdrom /mnt
mount: block device /dev/sr0 is write-protected, mounting read-only
mount: /dev/sr0 already mounted or /mnt busy
mount: according to mtab, /dev/sr0 is already mounted on /mnt
[root@node0924 yum.repos.d]# 

```

`mount /dev/cdrom /mnt`  将`/dev/cdrom`挂载在`/mnt`下



```shell
[root@node0924 yum.repos.d]# pwd
/etc/yum.repos.d
[root@node0924 yum.repos.d]# ls
back                     CentOS-Base.repo.rpmnew  CentOS-Media.repo  mysql-community.repo
CentOS-Base.repo         CentOS-Debuginfo.repo    CentOS-Vault.repo  mysql-community-source.repo
CentOS-Base.repo.backup  CentOS-fasttrack.repo    epel.repo
[root@node0924 yum.repos.d]# vim CentOS-Base.repo

```

`vim CentOS-Base.repo`  修改文件，这是我们从阿里云下下载出来的。

![image-20201120220515402](../image/image-20201120220515402.png)



修改文件内容

![image-20201120220930675](../image/image-20201120220930675.png)

```
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the 
# remarked out baseurl= line instead.
#
#

[local]
name=local
baseurl=file:///mnt
gpgcheck=1
enable=1


```



```shell
[root@node0924 yum.repos.d]# ls
back                     CentOS-Base.repo.rpmnew  CentOS-Media.repo  mysql-community.repo
CentOS-Base.repo         CentOS-Debuginfo.repo    CentOS-Vault.repo  mysql-community-source.repo
CentOS-Base.repo.backup  CentOS-fasttrack.repo    epel.repo
[root@node0924 yum.repos.d]# vim CentOS-Base.repo
[root@node0924 yum.repos.d]# yum clean all
Loaded plugins: fastestmirror
Cleaning repos: epel local mysql-connectors-community mysql-tools-community mysql57-community-dmr
Cleaning up Everything
Cleaning up list of fastest mirrors
[root@node0924 yum.repos.d]# yum makecache
Loaded plugins: fastestmirror
Determining fastest mirrors
epel                                                                                    | 4.7 kB     00:00     
epel/group_gz                                                                           |  74 kB     00:00     
epel/filelists_db                                                                       | 7.9 MB     00:00     
epel/prestodelta                                                                        |  435 B     00:00     
epel/primary_db                                                                         | 6.1 MB     00:00     
epel/other_db                                                                           | 3.0 MB     00:00     
local                                                                                   | 3.6 kB     00:00 ... 
local/group_gz                                                                          | 1.4 kB     00:00 ... 
local/filelists_db                                                                      | 182 kB     00:00 ... 
local/primary_db                                                                        | 492 kB     00:00 ... 
local/other_db                                                                          | 147 kB     00:00 ... 
mysql-connectors-community                                                              | 2.6 kB     00:00     
mysql-connectors-community/filelists_db                                                 |  82 kB     00:00     
mysql-connectors-community/primary_db                                                   |  58 kB     00:00     
mysql-connectors-community/other_db                                                     |  13 kB     00:00     
mysql-tools-community                                                                   | 2.6 kB     00:00     
mysql-tools-community/filelists_db                                                      | 203 kB     00:00     
mysql-tools-community/primary_db                                                        |  63 kB     00:00     
mysql-tools-community/other_db                                                          |  17 kB     00:00     
mysql57-community-dmr                                                                   | 2.6 kB     00:00     
mysql57-community-dmr/filelists_db                                                      | 1.4 MB     00:00     
mysql57-community-dmr/primary_db                                                        | 246 kB     00:00     
mysql57-community-dmr/other_db                                                          |  66 kB     00:00     
Metadata Cache Created
[root@node0924 yum.repos.d]# 

```



`yum clean all`  清理yum

`yum makecache` 下载



```shell
[root@node0924 yum.repos.d]# yum repolist
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
repo id                              repo name                                                           status
base                                 local                                                                6,367
epel                                 Extra Packages for Enterprise Linux 6 - x86_64                      12,585
mysql-connectors-community           MySQL Connectors Community                                             145
mysql-tools-community                MySQL Tools Community                                                   96
mysql57-community-dmr                MySQL 5.7 Community Server Development Milestone Release               432
repolist: 19,625
[root@node0924 yum.repos.d]# 

```

`yum repolist` 查看本地信息,`6,367`个本地源



```shell
[root@node0924 yum.repos.d]# yum install java
Loaded plugins: fastestmirror
Setting up Install Process
Loading mirror speeds from cached hostfile
No package java available.
Error: Nothing to do
[root@node0924 yum.repos.d]# yum install httpd
Loaded plugins: fastestmirror
Setting up Install Process
Loading mirror speeds from cached hostfile
No package httpd available.
Error: Nothing to do
[root@node0924 yum.repos.d]# 

```

这是没有切换DVD1，使用迷你版的内容。

`yum install java`

`yum install httpd`

本地安装



```shell
[root@node0924 yum.repos.d]# yum install java
Loaded plugins: fastestmirror
Setting up Install Process
Loading mirror speeds from cached hostfile
Resolving Dependencies
--> Running transaction check
---> Package java-1.7.0-openjdk.x86_64 1:1.7.0.45-2.4.3.3.el6 will be installed
--> Processing Dependency: jpackage-utils >= 1.7.3-1jpp.2 for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: xorg-x11-fonts-Type1 for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: tzdata-java for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: rhino for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: libpulse.so.0(PULSE_0)(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: libasound.so.2(ALSA_0.9.0rc4)(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: libasound.so.2(ALSA_0.9)(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: libpulse.so.0()(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: libgif.so.4()(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: libasound.so.2()(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Processing Dependency: libXtst.so.6()(64bit) for package: 1:java-1.7.0-openjdk-1.7.0.45-2.4.3.3.el6.x86_64
--> Running transaction check
---> Package alsa-lib.x86_64 0:1.0.22-3.el6 will be installed
---> Package giflib.x86_64 0:4.1.6-3.1.el6 will be installed
---> Package jpackage-utils.noarch 0:1.7.5-3.12.el6 will be installed
---> Package libXtst.x86_64 0:1.2.1-2.el6 will be installed
---> Package pulseaudio-libs.x86_64 0:0.9.21-14.el6_3 will be installed
--> Processing Dependency: libsndfile.so.1(libsndfile.so.1.0)(64bit) for package: pulseaudio-libs-0.9.21-14.el6_3.x86_64
--> Processing Dependency: libsndfile.so.1()(64bit) for package: pulseaudio-libs-0.9.21-14.el6_3.x86_64
--> Processing Dependency: libasyncns.so.0()(64bit) for package: pulseaudio-libs-0.9.21-14.el6_3.x86_64
---> Package rhino.noarch 0:1.7-0.7.r2.2.el6 will be installed
--> Processing Dependency: jline for package: rhino-1.7-0.7.r2.2.el6.noarch
---> Package tzdata-java.noarch 0:2013g-1.el6 will be installed
---> Package xorg-x11-fonts-Type1.noarch 0:7.2-9.1.el6 will be installed
--> Processing Dependency: ttmkfdir for package: xorg-x11-fonts-Type1-7.2-9.1.el6.noarch
--> Processing Dependency: ttmkfdir for package: xorg-x11-fonts-Type1-7.2-9.1.el6.noarch
--> Processing Dependency: mkfontdir for package: xorg-x11-fonts-Type1-7.2-9.1.el6.noarch
--> Processing Dependency: mkfontdir for package: xorg-x11-fonts-Type1-7.2-9.1.el6.noarch
--> Running transaction check
---> Package jline.noarch 0:0.9.94-0.8.el6 will be installed
---> Package libasyncns.x86_64 0:0.8-1.1.el6 will be installed
---> Package libsndfile.x86_64 0:1.0.20-5.el6 will be installed
--> Processing Dependency: libvorbisenc.so.2()(64bit) for package: libsndfile-1.0.20-5.el6.x86_64
--> Processing Dependency: libvorbis.so.0()(64bit) for package: libsndfile-1.0.20-5.el6.x86_64
--> Processing Dependency: libogg.so.0()(64bit) for package: libsndfile-1.0.20-5.el6.x86_64
--> Processing Dependency: libFLAC.so.8()(64bit) for package: libsndfile-1.0.20-5.el6.x86_64
---> Package ttmkfdir.x86_64 0:3.0.9-32.1.el6 will be installed
---> Package xorg-x11-font-utils.x86_64 1:7.2-11.el6 will be installed
--> Processing Dependency: libfontenc.so.1()(64bit) for package: 1:xorg-x11-font-utils-7.2-11.el6.x86_64
--> Processing Dependency: libXfont.so.1()(64bit) for package: 1:xorg-x11-font-utils-7.2-11.el6.x86_64
--> Running transaction check
---> Package flac.x86_64 0:1.2.1-6.1.el6 will be installed
---> Package libXfont.x86_64 0:1.4.5-2.el6 will be installed
---> Package libfontenc.x86_64 0:1.0.5-2.el6 will be installed
---> Package libogg.x86_64 2:1.1.4-2.1.el6 will be installed
---> Package libvorbis.x86_64 1:1.2.3-4.el6_2.1 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

===============================================================================================================
 Package                          Arch               Version                            Repository        Size
===============================================================================================================
Installing:
 java-1.7.0-openjdk               x86_64             1:1.7.0.45-2.4.3.3.el6             base              26 M
Installing for dependencies:
 alsa-lib                         x86_64             1.0.22-3.el6                       base             370 k
 flac                             x86_64             1.2.1-6.1.el6                      base             243 k
 giflib                           x86_64             4.1.6-3.1.el6                      base              37 k
 jline                            noarch             0.9.94-0.8.el6                     base              86 k
 jpackage-utils                   noarch             1.7.5-3.12.el6                     base              59 k
 libXfont                         x86_64             1.4.5-2.el6                        base             136 k
 libXtst                          x86_64             1.2.1-2.el6                        base              29 k
 libasyncns                       x86_64             0.8-1.1.el6                        base              24 k
 libfontenc                       x86_64             1.0.5-2.el6                        base              24 k
 libogg                           x86_64             2:1.1.4-2.1.el6                    base              21 k
 libsndfile                       x86_64             1.0.20-5.el6                       base             233 k
 libvorbis                        x86_64             1:1.2.3-4.el6_2.1                  base             168 k
 pulseaudio-libs                  x86_64             0.9.21-14.el6_3                    base             462 k
 rhino                            noarch             1.7-0.7.r2.2.el6                   base             778 k
 ttmkfdir                         x86_64             3.0.9-32.1.el6                     base              43 k
 tzdata-java                      noarch             2013g-1.el6                        base             155 k
 xorg-x11-font-utils              x86_64             1:7.2-11.el6                       base              75 k
 xorg-x11-fonts-Type1             noarch             7.2-9.1.el6                        base             520 k

Transaction Summary
===============================================================================================================
Install      19 Package(s)

Total download size: 29 M
Installed size: 100 M
Is this ok [y/N]: N
Exiting on user Command
Your transaction was saved, rerun it with:
 yum load-transaction /tmp/yum_save_tx-2020-11-21-20-46k0sl24.yumtx
[root@node0924 yum.repos.d]# 
[root@node0924 yum.repos.d]# yum install httpd
Loaded plugins: fastestmirror
Setting up Install Process
Loading mirror speeds from cached hostfile
Resolving Dependencies
--> Running transaction check
---> Package httpd.x86_64 0:2.2.15-29.el6.centos will be installed
--> Processing Dependency: httpd-tools = 2.2.15-29.el6.centos for package: httpd-2.2.15-29.el6.centos.x86_64
--> Processing Dependency: apr-util-ldap for package: httpd-2.2.15-29.el6.centos.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.2.15-29.el6.centos.x86_64
--> Processing Dependency: libaprutil-1.so.0()(64bit) for package: httpd-2.2.15-29.el6.centos.x86_64
--> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.2.15-29.el6.centos.x86_64
--> Running transaction check
---> Package apr.x86_64 0:1.3.9-5.el6_2 will be installed
---> Package apr-util.x86_64 0:1.3.9-3.el6_0.1 will be installed
---> Package apr-util-ldap.x86_64 0:1.3.9-3.el6_0.1 will be installed
---> Package httpd-tools.x86_64 0:2.2.15-29.el6.centos will be installed
---> Package mailcap.noarch 0:2.1.31-2.el6 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

===============================================================================================================
 Package                     Arch                 Version                             Repository          Size
===============================================================================================================
Installing:
 httpd                       x86_64               2.2.15-29.el6.centos                base               821 k
Installing for dependencies:
 apr                         x86_64               1.3.9-5.el6_2                       base               123 k
 apr-util                    x86_64               1.3.9-3.el6_0.1                     base                87 k
 apr-util-ldap               x86_64               1.3.9-3.el6_0.1                     base                15 k
 httpd-tools                 x86_64               2.2.15-29.el6.centos                base                73 k
 mailcap                     noarch               2.1.31-2.el6                        base                27 k

Transaction Summary
===============================================================================================================
Install       6 Package(s)

Total download size: 1.1 M
Installed size: 3.6 M
Is this ok [y/N]: Y
Downloading Packages:
---------------------------------------------------------------------------------------------------------------
Total                                                                           12 MB/s | 1.1 MB     00:00     
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
Warning: RPMDB altered outside of yum.
  Installing : apr-1.3.9-5.el6_2.x86_64                                                                    1/6 
  Installing : apr-util-1.3.9-3.el6_0.1.x86_64                                                             2/6 
  Installing : apr-util-ldap-1.3.9-3.el6_0.1.x86_64                                                        3/6 
  Installing : httpd-tools-2.2.15-29.el6.centos.x86_64                                                     4/6 
  Installing : mailcap-2.1.31-2.el6.noarch                                                                 5/6 
  Installing : httpd-2.2.15-29.el6.centos.x86_64                                                           6/6 
  Verifying  : httpd-2.2.15-29.el6.centos.x86_64                                                           1/6 
  Verifying  : apr-util-ldap-1.3.9-3.el6_0.1.x86_64                                                        2/6 
  Verifying  : httpd-tools-2.2.15-29.el6.centos.x86_64                                                     3/6 
  Verifying  : apr-1.3.9-5.el6_2.x86_64                                                                    4/6 
  Verifying  : mailcap-2.1.31-2.el6.noarch                                                                 5/6 
  Verifying  : apr-util-1.3.9-3.el6_0.1.x86_64                                                             6/6 

Installed:
  httpd.x86_64 0:2.2.15-29.el6.centos                                                                          

Dependency Installed:
  apr.x86_64 0:1.3.9-5.el6_2                           apr-util.x86_64 0:1.3.9-3.el6_0.1                      
  apr-util-ldap.x86_64 0:1.3.9-3.el6_0.1               httpd-tools.x86_64 0:2.2.15-29.el6.centos              
  mailcap.noarch 0:2.1.31-2.el6                       

Complete!
[root@node0924 yum.repos.d]# 

```

这是切换DVD1

`yum install java`

`yum install httpd`

本地安装



```shell
[root@node0924 yum.repos.d]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3        97G  3.1G   89G   4% /
tmpfs           490M     0  490M   0% /dev/shm
/dev/sda1       190M   48M  132M  27% /boot
/dev/sr0        4.2G  4.2G     0 100% /mnt
[root@node0924 yum.repos.d]# umount /mnt
[root@node0924 yum.repos.d]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3        97G  3.1G   89G   4% /
tmpfs           490M     0  490M   0% /dev/shm
/dev/sda1       190M   48M  132M  27% /boot
[root@node0924 yum.repos.d]# 

```

`umount /mnt` 卸载本地光盘

`df -h` 查看盘符,没有/mnt挂载



```shell
[root@node0924 yum.repos.d]# mount /dev/cdrom /mnt
mount: block device /dev/sr0 is write-protected, mounting read-only
[root@node0924 yum.repos.d]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3        97G  3.1G   89G   4% /
tmpfs           490M     0  490M   0% /dev/shm
/dev/sda1       190M   48M  132M  27% /boot
/dev/sr0        4.2G  4.2G     0 100% /mnt
[root@node0924 yum.repos.d]# 

```

`mount /dev/cdrom /mnt` 挂载

`df -h` 查看盘符



补充一点内容，需要下载CentOS文件 DVD1

地址：https://vault.centos.org/6.5/isos/x86_64/

![image-20201120222422870](../image/image-20201120222422870.png)





