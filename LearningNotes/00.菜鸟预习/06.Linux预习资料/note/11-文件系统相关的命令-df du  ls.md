11-文件系统相关的命令-df du  ls



![image-20201114201417243](../image/image-20201114201417243.png)



```shell
# clear清屏
[root@node0924 1894]# clear
# 查看分区的使用情况
[root@node0924 1894]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3        97G  2.3G   89G   3% /
tmpfs           490M     0  490M   0% /dev/shm
/dev/sda1       190M   48M  132M  27% /boot
# 回到根目录
[root@node0924 1894]# cd
# 查看文件
[root@node0924 ~]# ls
a                install.log                               mysql-community-release-el6-5.noarch.rpm.1  test
anaconda-ks.cfg  install.log.syslog                        soft                                        zfg
data             mysql-community-release-el6-5.noarch.rpm  springboot
# 查看文件的使用情况
[root@node0924 ~]# du a/
4	a/adir/bdir
8	a/adir
4	a/ydir
4	a/3dir
4	a/xdir
4	a/2dir
4	a/zdir
8	a/1dir
44	a/
# 查看文件的使用情况，-h显示大小
[root@node0924 ~]# du -h a/
4.0K	a/adir/bdir
8.0K	a/adir
4.0K	a/ydir
4.0K	a/3dir
4.0K	a/xdir
4.0K	a/2dir
4.0K	a/zdir
8.0K	a/1dir
44K	a/
[root@node0924 ~]# 

```



![image-20201114201911688](../image/image-20201114201911688.png)

```shell
# 显示/etc/下的文件信息
[root@node0924 ~]# ls /etc/
123                      environment  issue           ntp             rc6.d             statetab
adjtime                  ethers       issue.net       nutcracker      rc.d              statetab.d
aliases                  exports      krb5.conf       openldap        rc.local          sudo.conf
aliases.db               favicon.png  ld.so.cache     opt             rc.sysinit        sudoers
alternatives             filesystems  ld.so.conf      pam.d           redhat-release    sudoers.d
audisp                   fonts        ld.so.conf.d    pango           redis             sudo-ldap.conf
audit                    fstab        libaudit.conf   passwd          resolv.conf       sysconfig
bash_completion.d        gai.conf     libuser.conf    passwd-         resolv.conf.save  sysctl.conf
bashrc                   gcrypt       localtime       pkcs11          rpc               sysctl.d
blkid                    gnupg        login.defs      pki             rpm               system-release
centos-release           group        logrotate.conf  plymouth        rsyslog.conf      system-release-cpe
chkconfig.d              group-       logrotate.d     pm              rsyslog.d         terminfo
cron.d                   grub.conf    lvm             popt.d          rwtab             udev
cron.daily               gshadow      magic           ppp             rwtab.d           vimrc
crypttab                 gshadow-     makedev.d       prelink.conf.d  sasl2             virc
csh.cshrc                host.conf    man.config      printcap        securetty         wgetrc
csh.login                hosts        mke2fs.conf     profile         security          X11
dbus-1                   hosts.allow  modprobe.d      profile.d       selinux           xdg
default                  hosts.deny   motd            protocols       services          xinetd.d
depmod.d                 init         mtab            rc              sestatus.conf     yum
dhcp                     init.conf    multipath       rc0.d           shadow            yum.conf
DIR_COLORS               init.d       my.cnf          rc1.d           shadow-           yum.repos.d
DIR_COLORS.256color      inittab      my.cnf.d        rc2.d           shells
DIR_COLORS.lightbgcolor  inputrc      NetworkManager  rc3.d           skel
dracut.conf              iproute2     networks        rc4.d           ssh
dracut.conf.d            iscsi        nsswitch.conf   rc5.d           ssl
# 显示当前目录下的文件信息
[root@node0924 ~]# ls
a                install.log                               mysql-community-release-el6-5.noarch.rpm.1  test
anaconda-ks.cfg  install.log.syslog                        soft                                        zfg
data             mysql-community-release-el6-5.noarch.rpm  springboot
[root@node0924 ~]# 
```



```shell
# pwd查看当前目录
[root@node0924 ~]# pwd
/root
[root@node0924 ~]# 
```



![image-20201114202236697](../image/image-20201114202236697.png)



```shell
# 查看帮助文档
[root@node0924 ~]# man ls
# 回到根目录
[root@node0924 ~]# cd
# 查看当前目录
[root@node0924 ~]# pwd
/root
# 查看当前目录的文件
[root@node0924 ~]# ls
a                install.log                               mysql-community-release-el6-5.noarch.rpm.1  test
anaconda-ks.cfg  install.log.syslog                        soft                                        zfg
data             mysql-community-release-el6-5.noarch.rpm  springboot
# 查看当前目录的文件，包含隐藏文件
[root@node0924 ~]# ls -a
.                .cshrc                                      soft
..               data                                        springboot
a                install.log                                 .tcshrc
anaconda-ks.cfg  install.log.syslog                          test
.a.swp           mysql-community-release-el6-5.noarch.rpm    .test.txt.swp
.bash_history    mysql-community-release-el6-5.noarch.rpm.1  .viminfo
.bash_logout     .mysql_history                              zfg
.bash_profile    .pki
.bashrc          .rediscli_history
[root@node0924 ~]# 

```



![image-20201114202535766](../image/image-20201114202535766.png)



```shell
# 以长文件的方式展示文件，详细信息
[root@node0924 ~]# ls -l
total 60
drwxr-xr-x. 9 root root 4096 Nov 14 18:50 a
-rw-------. 1 root root  900 Sep 25 07:50 anaconda-ks.cfg
drwxr-xr-x. 4 root root 4096 Sep 28 20:23 data
-rw-r--r--. 1 root root 8815 Sep 25 07:50 install.log
-rw-r--r--. 1 root root 3384 Sep 25 07:50 install.log.syslog
-rw-r--r--. 1 root root 5824 Nov 12  2015 mysql-community-release-el6-5.noarch.rpm
-rw-r--r--. 1 root root 5824 Nov 12  2015 mysql-community-release-el6-5.noarch.rpm.1
drwxr-xr-x. 5 root root 4096 Sep 28 20:46 soft
drwxr-xr-x. 2 root root 4096 Sep 29 01:56 springboot
drwxr-xr-x. 6 root root 4096 Nov 14 18:50 test
-rw-r--r--. 1 root root   45 Sep 26 03:45 zfg
# ls -l 类似于 ll
[root@node0924 ~]# ll
total 60
drwxr-xr-x. 9 root root 4096 Nov 14 18:50 a
-rw-------. 1 root root  900 Sep 25 07:50 anaconda-ks.cfg
drwxr-xr-x. 4 root root 4096 Sep 28 20:23 data
-rw-r--r--. 1 root root 8815 Sep 25 07:50 install.log
-rw-r--r--. 1 root root 3384 Sep 25 07:50 install.log.syslog
-rw-r--r--. 1 root root 5824 Nov 12  2015 mysql-community-release-el6-5.noarch.rpm
-rw-r--r--. 1 root root 5824 Nov 12  2015 mysql-community-release-el6-5.noarch.rpm.1
drwxr-xr-x. 5 root root 4096 Sep 28 20:46 soft
drwxr-xr-x. 2 root root 4096 Sep 29 01:56 springboot
drwxr-xr-x. 6 root root 4096 Nov 14 18:50 test
-rw-r--r--. 1 root root   45 Sep 26 03:45 zfg
[root@node0924 ~]# 

```



```
drwxr-xr-x. 9 root root 4096 Nov 14 18:50 a
-rw-------. 1 root root  900 Sep 25 07:50 anaconda-ks.cfg
```

`drwxr-xr-x`和`-rw-------`

`d`代表文件夹，`-`代表文件。

往后数9位，代表文件的权限。

`rwxr-xr-x`和`rw-------`，每三位一组。

`rwx`属主的权限

`r-x`属组的权限

`r-x`其他人的权限



```shell
#        .分割  硬连接数量  属主  属组  字节大小 时间戳(最后修改的时间) 
-rw-------.     1        root root  900    Sep 25 07:50    anaconda-ks.cfg

```

文件详细解释。



```shell
# 查看bin目录下的文件详情
[root@node0924 ~]# ls -l /bin/
total 5956
-rwxr-xr-x. 1 root root  24232 Jun 19  2018 arch
lrwxrwxrwx. 1 root root      4 Sep 26 19:27 awk -> gawk
-rwxr-xr-x. 1 root root  23720 Jun 19  2018 basename
-rwxr-xr-x. 1 root root 906568 Mar 23  2017 bash
-rwxr-xr-x. 1 root root  45224 Jun 19  2018 cat
-rwxr-xr-x. 1 root root  52936 Jun 19  2018 chgrp
-rwxr-xr-x. 1 root root  48712 Jun 19  2018 chmod
-rwxr-xr-x. 1 root root  53640 Jun 19  2018 chown
-rwxr-xr-x. 1 root root 116824 Jun 19  2018 cp
-rwxr-xr-x. 1 root root 129992 Mar 22  2017 cpio
-rwxr-xr-x. 1 root root  41704 Jun 19  2018 cut
-rwxr-xr-x. 1 root root 106216 Oct 17  2012 dash
-rwxr-xr-x. 1 root root  55576 Jun 19  2018 date
-rwxr-xr-x. 1 root root  52720 Jun 19  2018 dd
-rwxr-xr-x. 1 root root  90544 Jun 19  2018 df
-rwxr-xr-x. 1 root root   6736 Jan 26  2018 dmesg
lrwxrwxrwx. 1 root root      8 Sep 26 19:27 dnsdomainname -> hostname
lrwxrwxrwx. 1 root root      8 Sep 26 19:27 domainname -> hostname
-rwxr-xr-x. 1 root root  78504 Nov 12  2010 dumpkeys
-rwxr-xr-x. 1 root root  24136 Jun 19  2018 echo
lrwxrwxrwx. 1 root root      4 Sep 26 19:27 egrep -> grep
-rwxr-xr-x. 1 root root  23832 Jun 19  2018 env
lrwxrwxrwx. 1 root root      2 Sep 26 00:15 ex -> vi
-rwxr-xr-x. 1 root root  21112 Jun 19  2018 false
lrwxrwxrwx. 1 root root      4 Sep 26 19:27 fgrep -> grep
-rwxr-xr-x. 1 root root 234512 Mar  1  2016 find
-rwxr-xr-x. 1 root root  36392 Jan 26  2018 findmnt
-rwsr-x---. 1 root fuse  28000 May 11  2016 fusermount
-rwxr-xr-x. 1 root root 375616 Nov 10  2015 gawk
-rwxr-xr-x. 1 root root 163696 Mar 22  2017 grep
lrwxrwxrwx. 1 root root      3 Sep 26 19:27 gtar -> tar
-rwxr-xr-x. 1 root root     61 Mar 22  2017 gunzip
-rwxr-xr-x. 1 root root  64688 Mar 22  2017 gzip
-rwxr-xr-x. 1 root root  13880 Mar 22  2017 hostname
-rwxr-xr-x. 1 root root  11264 Jun 20  2018 ipcalc
lrwxrwxrwx. 1 root root     41 Sep 26 19:30 iptables-xml -> /etc/alternatives/bin-iptables-xml.x86_64
lrwxrwxrwx. 1 root root     20 Sep 26 19:28 iptables-xml-1.4.7 -> /sbin/iptables-multi
-rwxr-xr-x. 1 root root   7920 Nov 12  2010 kbd_mode
-rwxr-xr-x. 1 root root  11576 Jan 26  2018 kill
-rwxr-xr-x. 1 root root  23720 Jun 19  2018 link
-rwxr-xr-x. 1 root root  45664 Jun 19  2018 ln
-rwxr-xr-x. 1 root root 108248 Nov 12  2010 loadkeys
-rwxr-xr-x. 1 root root  11608 Jan 26  2018 logger
-rwxr-xr-x. 1 root root  29720 Jan 26  2018 login
-rwxr-xr-x. 1 root root 109208 Jun 19  2018 ls
-rwxr-xr-x. 1 root root  55336 Jan 26  2018 lsblk
-rwxr-xr-x. 1 root root  45416 Jun 19  2018 mkdir
-rwxr-xr-x. 1 root root  28568 Jun 19  2018 mknod
-rwxr-xr-x. 1 root root  33544 Jun 19  2018 mktemp
-rwxr-xr-x. 1 root root  35928 Jan 26  2018 more
-rwsr-xr-x. 1 root root  77560 Jan 26  2018 mount
-rwxr-xr-x. 1 root root   6728 Jul 24  2015 mountpoint
-rwxr-xr-x. 1 root root 106912 Jun 19  2018 mv
-rwxr-xr-x. 1 root root 123360 Mar 22  2017 netstat
-rwxr-xr-x. 1 root root  25208 Jun 19  2018 nice
lrwxrwxrwx. 1 root root      8 Sep 26 19:27 nisdomainname -> hostname
-rwsr-xr-x. 1 root root  38520 Mar 22  2017 ping
-rwsr-xr-x. 1 root root  36488 Mar 22  2017 ping6
-rwxr-xr-x. 1 root root  31776 Mar 22  2017 plymouth
-rwxr-xr-x. 1 root root  85304 Jun  1  2018 ps
-rwxr-xr-x. 1 root root  28008 Jun 19  2018 pwd
-rwxr-xr-x. 1 root root   8184 Jan 26  2018 raw
-rwxr-xr-x. 1 root root  36360 Jun 19  2018 readlink
-rwxr-xr-x. 1 root root  53592 Jun 19  2018 rm
-rwxr-xr-x. 1 root root  36888 Jun 19  2018 rmdir
-rwxr-xr-x. 1 root root  20392 Jun 19  2018 rpm
lrwxrwxrwx. 1 root root      2 Sep 26 00:15 rvi -> vi
lrwxrwxrwx. 1 root root      2 Sep 26 00:15 rview -> vi
-rwxr-xr-x. 1 root root  69624 Jun 22  2012 sed
-rwxr-xr-x. 1 root root  37448 Nov 12  2010 setfont
lrwxrwxrwx. 1 root root      4 Sep 26 19:27 sh -> bash
-rwxr-xr-x. 1 root root  24264 Jun 19  2018 sleep
-rwxr-xr-x. 1 root root  93496 Jun 19  2018 sort
-rwxr-xr-x. 1 root root  61320 Jun 19  2018 stty
-rwsr-xr-x. 1 root root  34904 Jun 19  2018 su
-rwxr-xr-x. 1 root root  21896 Jun 19  2018 sync
-rwxr-xr-x. 1 root root 390616 Jul 12  2016 tar
-rwxr-xr-x. 1 root root  11352 Jan 26  2018 taskset
-rwxr-xr-x. 1 root root  47928 Jun 19  2018 touch
-rwxr-xr-x. 1 root root  11440 Mar 22  2017 tracepath
-rwxr-xr-x. 1 root root  12304 Mar 22  2017 tracepath6
-rwxr-xr-x. 1 root root  21112 Jun 19  2018 true
-rwxr-xr-x. 1 root root  11256 May 11  2016 ulockmgr_server
-rwsr-xr-x. 1 root root  53480 Jan 26  2018 umount
-rwxr-xr-x. 1 root root  24232 Jun 19  2018 uname
-rwxr-xr-x. 1 root root   2555 Nov 12  2010 unicode_start
-rwxr-xr-x. 1 root root    363 Nov 12  2010 unicode_stop
-rwxr-xr-x. 1 root root  22216 Jun 19  2018 unlink
-rwxr-xr-x. 1 root root   6736 Jun 20  2018 usleep
-rwxr-xr-x. 1 root root 907312 Jul 17  2019 vi
lrwxrwxrwx. 1 root root      2 Sep 26 00:15 view -> vi
lrwxrwxrwx. 1 root root      8 Sep 26 19:27 ypdomainname -> hostname
-rwxr-xr-x. 1 root root     62 Mar 22  2017 zcat
[root@node0924 ~]# 

```



```
lrwxrwxrwx. 1 root root      2 Sep 26 00:15 view -> vi
```

`l`开头，代表软连接，类似于windows下的快捷方式。





```shell
[root@node0924 ~]# ls -l /dev/
total 0
crw-rw----. 1 root video    10, 175 Nov 13 20:57 agpgart
drwxr-xr-x. 2 root root         620 Nov 13 20:57 block
drwxr-xr-x. 2 root root          80 Nov 13 20:57 bsg
crw-------. 1 root root     10, 234 Nov 13 20:57 btrfs-control
drwxr-xr-x. 3 root root          60 Nov 13 20:57 bus
lrwxrwxrwx. 1 root root           3 Nov 13 20:57 cdrom -> sr0
lrwxrwxrwx. 1 root root           3 Nov 13 20:57 cdrw -> sr0
drwxr-xr-x. 2 root root        2940 Nov 13 20:58 char
crw-------. 1 root root      5,   1 Nov 13 20:57 console
lrwxrwxrwx. 1 root root          11 Nov 13 20:57 core -> /proc/kcore
drwxr-xr-x. 3 root root          60 Nov 13 20:57 cpu
crw-rw----. 1 root root     10,  61 Nov 13 20:57 cpu_dma_latency
crw-rw----. 1 root root     10,  62 Nov 13 20:57 crash
drwxr-xr-x. 6 root root         120 Nov 13 20:57 disk
crw-rw----. 1 root audio    14,   9 Nov 13 20:57 dmmidi
drwxr-xr-x. 2 root root         100 Nov 13 20:57 dri
lrwxrwxrwx. 1 root root           3 Nov 13 20:57 dvd -> sr0
lrwxrwxrwx. 1 root root           3 Nov 13 20:57 dvdrw -> sr0
lrwxrwxrwx. 1 root root           3 Nov 13 20:57 fb -> fb0
crw-rw----. 1 root video    29,   0 Nov 13 20:57 fb0
lrwxrwxrwx. 1 root root          13 Nov 13 20:57 fd -> /proc/self/fd
crw-rw-rw-. 1 root root      1,   7 Nov 13 20:57 full
crw-rw-rw-. 1 root root     10, 229 Nov 13 20:57 fuse
crw-rw----. 1 root root    248,   0 Nov 13 20:57 hidraw0
crw-rw----. 1 root root     10, 228 Nov 13 20:57 hpet
drwxr-xr-x. 2 root root          40 Nov 13 20:57 hugepages
crw-------. 1 root root    229,   0 Nov 13 20:57 hvc0
drwxr-xr-x. 4 root root         260 Nov 13 20:57 input
crw-rw----. 1 root root      1,  11 Nov 13 20:57 kmsg
srw-rw-rw-. 1 root root           0 Nov 13 20:58 log
brw-rw----. 1 root disk      7,   0 Nov 13 20:57 loop0
brw-rw----. 1 root disk      7,   1 Nov 13 20:57 loop1
brw-rw----. 1 root disk      7,   2 Nov 13 20:57 loop2
brw-rw----. 1 root disk      7,   3 Nov 13 20:57 loop3
brw-rw----. 1 root disk      7,   4 Nov 13 20:57 loop4
brw-rw----. 1 root disk      7,   5 Nov 13 20:57 loop5
brw-rw----. 1 root disk      7,   6 Nov 13 20:57 loop6
brw-rw----. 1 root disk      7,   7 Nov 13 20:57 loop7
crw-rw----. 1 root lp        6,   0 Nov 13 20:57 lp0
crw-rw----. 1 root lp        6,   1 Nov 13 20:57 lp1
crw-rw----. 1 root lp        6,   2 Nov 13 20:57 lp2
crw-rw----. 1 root lp        6,   3 Nov 13 20:57 lp3
lrwxrwxrwx. 1 root root          13 Nov 13 20:57 MAKEDEV -> /sbin/MAKEDEV
drwxr-xr-x. 2 root root          60 Nov 13 20:57 mapper
crw-rw----. 1 root root     10, 227 Nov 13 20:57 mcelog
crw-r-----. 1 root kmem      1,   1 Nov 13 20:57 mem
crw-rw----. 1 root audio    14,   2 Nov 13 20:57 midi
drwxr-xr-x. 2 root root          60 Nov 13 20:57 net
crw-rw----. 1 root root     10,  60 Nov 13 20:57 network_latency
crw-rw----. 1 root root     10,  59 Nov 13 20:57 network_throughput
crw-rw-rw-. 1 root root      1,   3 Nov 13 20:57 null
crw-r-----. 1 root kmem     10, 144 Nov 13 20:57 nvram
crw-rw----. 1 root root      1,  12 Nov 13 20:57 oldmem
crw-r-----. 1 root kmem      1,   4 Nov 13 20:57 port
crw-------. 1 root root    108,   0 Nov 13 20:57 ppp
crw-rw-rw-. 1 root tty       5,   2 Nov 14 20:41 ptmx
drwxr-xr-x. 2 root root           0 Nov 13 20:57 pts
brw-rw----. 1 root disk      1,   0 Nov 13 20:57 ram0
brw-rw----. 1 root disk      1,   1 Nov 13 20:57 ram1
brw-rw----. 1 root disk      1,  10 Nov 13 20:57 ram10
brw-rw----. 1 root disk      1,  11 Nov 13 20:57 ram11
brw-rw----. 1 root disk      1,  12 Nov 13 20:57 ram12
brw-rw----. 1 root disk      1,  13 Nov 13 20:57 ram13
brw-rw----. 1 root disk      1,  14 Nov 13 20:57 ram14
brw-rw----. 1 root disk      1,  15 Nov 13 20:57 ram15
brw-rw----. 1 root disk      1,   2 Nov 13 20:57 ram2
brw-rw----. 1 root disk      1,   3 Nov 13 20:57 ram3
brw-rw----. 1 root disk      1,   4 Nov 13 20:57 ram4
brw-rw----. 1 root disk      1,   5 Nov 13 20:57 ram5
brw-rw----. 1 root disk      1,   6 Nov 13 20:57 ram6
brw-rw----. 1 root disk      1,   7 Nov 13 20:57 ram7
brw-rw----. 1 root disk      1,   8 Nov 13 20:57 ram8
brw-rw----. 1 root disk      1,   9 Nov 13 20:57 ram9
crw-rw-rw-. 1 root root      1,   8 Nov 13 20:57 random
drwxr-xr-x. 2 root root          60 Nov 13 20:57 raw
crw-r--r--. 1 root root     10,  57 Nov 13 20:57 rfkill
lrwxrwxrwx. 1 root root           4 Nov 13 20:57 root -> sda3
lrwxrwxrwx. 1 root root           4 Nov 13 20:57 rtc -> rtc0
crw-rw----. 1 root root    253,   0 Nov 13 20:57 rtc0
lrwxrwxrwx. 1 root root           3 Nov 13 20:57 scd0 -> sr0
brw-rw----. 1 root disk      8,   0 Nov 13 20:57 sda
brw-rw----. 1 root disk      8,   1 Nov 13 20:57 sda1
brw-rw----. 1 root disk      8,   2 Nov 13 20:57 sda2
brw-rw----. 1 root disk      8,   3 Nov 13 20:57 sda3
crw-rw----. 1 root cdrom    21,   0 Nov 13 20:57 sg0
crw-rw----. 1 root disk     21,   1 Nov 13 20:57 sg1
drwxrwxrwt. 2 root root          40 Nov 13 20:57 shm
crw-rw----. 1 root root     10, 231 Nov 13 20:57 snapshot
drwxr-xr-x. 3 root root         200 Nov 13 20:57 snd
brw-rw----. 1 root cdrom    11,   0 Nov 13 20:57 sr0
lrwxrwxrwx. 1 root root          15 Nov 13 20:57 stderr -> /proc/self/fd/2
lrwxrwxrwx. 1 root root          15 Nov 13 20:57 stdin -> /proc/self/fd/0
lrwxrwxrwx. 1 root root          15 Nov 13 20:57 stdout -> /proc/self/fd/1
lrwxrwxrwx. 1 root root           4 Nov 13 20:57 systty -> tty0
crw-rw-rw-. 1 root tty       5,   0 Nov 13 20:57 tty
crw--w----. 1 root tty       4,   0 Nov 13 20:57 tty0
crw-------. 1 root root      4,   1 Nov 13 20:58 tty1
crw--w----. 1 root tty       4,  10 Nov 13 20:57 tty10
crw--w----. 1 root tty       4,  11 Nov 13 20:57 tty11
crw--w----. 1 root tty       4,  12 Nov 13 20:57 tty12
crw--w----. 1 root tty       4,  13 Nov 13 20:57 tty13
crw--w----. 1 root tty       4,  14 Nov 13 20:57 tty14
crw--w----. 1 root tty       4,  15 Nov 13 20:57 tty15
crw--w----. 1 root tty       4,  16 Nov 13 20:57 tty16
crw--w----. 1 root tty       4,  17 Nov 13 20:57 tty17
crw--w----. 1 root tty       4,  18 Nov 13 20:57 tty18
crw--w----. 1 root tty       4,  19 Nov 13 20:57 tty19
crw-------. 1 root root      4,   2 Nov 13 20:58 tty2
crw--w----. 1 root tty       4,  20 Nov 13 20:57 tty20
crw--w----. 1 root tty       4,  21 Nov 13 20:57 tty21
crw--w----. 1 root tty       4,  22 Nov 13 20:57 tty22
crw--w----. 1 root tty       4,  23 Nov 13 20:57 tty23
crw--w----. 1 root tty       4,  24 Nov 13 20:57 tty24
crw--w----. 1 root tty       4,  25 Nov 13 20:57 tty25
crw--w----. 1 root tty       4,  26 Nov 13 20:57 tty26
crw--w----. 1 root tty       4,  27 Nov 13 20:57 tty27
crw--w----. 1 root tty       4,  28 Nov 13 20:57 tty28
crw--w----. 1 root tty       4,  29 Nov 13 20:57 tty29
crw-------. 1 root root      4,   3 Nov 13 20:58 tty3
crw--w----. 1 root tty       4,  30 Nov 13 20:57 tty30
crw--w----. 1 root tty       4,  31 Nov 13 20:57 tty31
crw--w----. 1 root tty       4,  32 Nov 13 20:57 tty32
crw--w----. 1 root tty       4,  33 Nov 13 20:57 tty33
crw--w----. 1 root tty       4,  34 Nov 13 20:57 tty34
crw--w----. 1 root tty       4,  35 Nov 13 20:57 tty35
crw--w----. 1 root tty       4,  36 Nov 13 20:57 tty36
crw--w----. 1 root tty       4,  37 Nov 13 20:57 tty37
crw--w----. 1 root tty       4,  38 Nov 13 20:57 tty38
crw--w----. 1 root tty       4,  39 Nov 13 20:57 tty39
crw-------. 1 root root      4,   4 Nov 13 20:58 tty4
crw--w----. 1 root tty       4,  40 Nov 13 20:57 tty40
crw--w----. 1 root tty       4,  41 Nov 13 20:57 tty41
crw--w----. 1 root tty       4,  42 Nov 13 20:57 tty42
crw--w----. 1 root tty       4,  43 Nov 13 20:57 tty43
crw--w----. 1 root tty       4,  44 Nov 13 20:57 tty44
crw--w----. 1 root tty       4,  45 Nov 13 20:57 tty45
crw--w----. 1 root tty       4,  46 Nov 13 20:57 tty46
crw--w----. 1 root tty       4,  47 Nov 13 20:57 tty47
crw--w----. 1 root tty       4,  48 Nov 13 20:57 tty48
crw--w----. 1 root tty       4,  49 Nov 13 20:57 tty49
crw-------. 1 root root      4,   5 Nov 13 20:58 tty5
crw--w----. 1 root tty       4,  50 Nov 13 20:57 tty50
crw--w----. 1 root tty       4,  51 Nov 13 20:57 tty51
crw--w----. 1 root tty       4,  52 Nov 13 20:57 tty52
crw--w----. 1 root tty       4,  53 Nov 13 20:57 tty53
crw--w----. 1 root tty       4,  54 Nov 13 20:57 tty54
crw--w----. 1 root tty       4,  55 Nov 13 20:57 tty55
crw--w----. 1 root tty       4,  56 Nov 13 20:57 tty56
crw--w----. 1 root tty       4,  57 Nov 13 20:57 tty57
crw--w----. 1 root tty       4,  58 Nov 13 20:57 tty58
crw--w----. 1 root tty       4,  59 Nov 13 20:57 tty59
crw-------. 1 root root      4,   6 Nov 13 20:58 tty6
crw--w----. 1 root tty       4,  60 Nov 13 20:57 tty60
crw--w----. 1 root tty       4,  61 Nov 13 20:57 tty61
crw--w----. 1 root tty       4,  62 Nov 13 20:57 tty62
crw--w----. 1 root tty       4,  63 Nov 13 20:57 tty63
crw--w----. 1 root tty       4,   7 Nov 13 20:57 tty7
crw--w----. 1 root tty       4,   8 Nov 13 20:57 tty8
crw--w----. 1 root tty       4,   9 Nov 13 20:57 tty9
crw-rw----. 1 root dialout   4,  64 Nov 13 20:57 ttyS0
crw-rw----. 1 root dialout   4,  65 Nov 13 20:57 ttyS1
crw-rw----. 1 root dialout   4,  66 Nov 13 20:57 ttyS2
crw-rw----. 1 root dialout   4,  67 Nov 13 20:57 ttyS3
crw-rw-rw-. 1 root root      1,   9 Nov 13 20:57 urandom
crw-rw----. 1 root root    249,   0 Nov 13 20:57 usbmon0
crw-rw----. 1 root root    249,   1 Nov 13 20:57 usbmon1
crw-rw----. 1 root root    249,   2 Nov 13 20:57 usbmon2
crw-rw----. 1 vcsa tty       7,   0 Nov 13 20:57 vcs
crw-rw----. 1 vcsa tty       7,   1 Nov 13 20:57 vcs1
crw-rw----. 1 vcsa tty       7,   2 Nov 13 20:58 vcs2
crw-rw----. 1 vcsa tty       7,   3 Nov 13 20:58 vcs3
crw-rw----. 1 vcsa tty       7,   4 Nov 13 20:58 vcs4
crw-rw----. 1 vcsa tty       7,   5 Nov 13 20:58 vcs5
crw-rw----. 1 vcsa tty       7,   6 Nov 13 20:58 vcs6
crw-rw----. 1 vcsa tty       7, 128 Nov 13 20:57 vcsa
crw-rw----. 1 vcsa tty       7, 129 Nov 13 20:57 vcsa1
crw-rw----. 1 vcsa tty       7, 130 Nov 13 20:58 vcsa2
crw-rw----. 1 vcsa tty       7, 131 Nov 13 20:58 vcsa3
crw-rw----. 1 vcsa tty       7, 132 Nov 13 20:58 vcsa4
crw-rw----. 1 vcsa tty       7, 133 Nov 13 20:58 vcsa5
crw-rw----. 1 vcsa tty       7, 134 Nov 13 20:58 vcsa6
crw-rw----. 1 root root     10,  63 Nov 13 20:57 vga_arbiter
crw-rw-rw-. 1 root root      1,   5 Nov 13 20:57 zero
[root@node0924 ~]# ^C
[root@node0924 ~]# 

```

查看dev下目录的详情

```
crw-------. 1 root root     10, 234 Nov 13 20:57 btrfs-control
brw-rw----. 1 root disk      8,   0 Nov 13 20:57 sda
```

以`c`开头的文件，字符设备文件

以`b`开头的文件，块设备文件



![image-20201114201417243](../image/image-20201114201417243.png)



小结

* 文件命令
  * df
  * du
  * ls
* 目录文件详情
  * 文件类型
    * -
    * d
    * b
    * c
    * l
    * p
    * s
  * 文件权限
    * 9位
  * ...



命令小结

* clear
* df -h
* cd
* ls
* du a/
* du -h a/
* ls /ect/
* pwd
* man ls
* ls -a
* ls -l
* ll
* ls -l /bin/
* ls -l /dev/















