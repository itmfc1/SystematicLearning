24-Linux文本处理命令-cut sort wc



![image-20201116224955089](../image/image-20201116224955089.png)

文本处理命令

* cut
* sort
* wc





```shell
[root@node0924 a]# man cut
[root@node0924 a]# cat test2.txt
hello msb
hello angelababy
hello dilireba
iiii250 wyf
hello zhangxinyi
11 hel mhellosbjy lo
h2341123ibj
iiii521 fanbingbing
111 hello 222
wo ai bj tam
hiahelloahiahello
helloahiahelloahi
[root@node0924 a]# cut -d ' ' -f1 test2.txt
hello
hello
hello
iiii250
hello
11
h2341123ibj
iiii521
111
wo
hiahelloahiahello
helloahiahelloahi
[root@node0924 a]# 

```

`man cut`  查看切割命令

`cut -d ' ' -f1 test2.txt` 以空格切割文本，显示第1个位置。

`-d` 自定义分隔符

`-f` 显示的位置



```shell
[root@node0924 a]# cut -d ' ' -f1,2 test2.txt
hello msb
hello angelababy
hello dilireba
iiii250 wyf
hello zhangxinyi
11 hel
h2341123ibj
iiii521 fanbingbing
111 hello
wo ai
hiahelloahiahello
helloahiahelloahi
[root@node0924 a]# cut -d ' ' -f1,2,3 test2.txt
hello msb
hello angelababy
hello dilireba
iiii250 wyf
hello zhangxinyi
11 hel mhellosbjy
h2341123ibj
iiii521 fanbingbing
111 hello 222
wo ai bj
hiahelloahiahello
helloahiahelloahi
[root@node0924 a]# cut -d ' ' -f1-3 test2.txt
hello msb
hello angelababy
hello dilireba
iiii250 wyf
hello zhangxinyi
11 hel mhellosbjy
h2341123ibj
iiii521 fanbingbing
111 hello 222
wo ai bj
hiahelloahiahello
helloahiahelloahi
[root@node0924 a]# 

```

`cut -d ' ' -f1,2 test2.txt`  显示第一列和第二列

`cut -d ' ' -f1,2,3 test2.txt` 显示第一列、第二列、第三列

`cut -d ' ' -f1-3 test2.txt` 显示第1~3列



```shell
[root@node0924 a]# cut -d ' ' -f1-3 -s test2.txt
hello msb
hello angelababy
hello dilireba
iiii250 wyf
hello zhangxinyi
11 hel mhellosbjy
iiii521 fanbingbing
111 hello 222
wo ai bj
[root@node0924 a]# 

```

`cut -d ' ' -f1-3 -s test2.txt`  不显示没有分割符的行



```shell
[root@node0924 a]# ls
1dir  2dir  3dir  adir  profile  test2.txt  test.txt  xdir  ydir  zdir  zfg
[root@node0924 a]# cp /etc/passwd ./
[root@node0924 a]# ls
1dir  2dir  3dir  adir  passwd  profile  test2.txt  test.txt  xdir  ydir  zdir  zfg
[root@node0924 a]# cat passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
saslauth:x:499:76:"Saslauthd user":/var/empty/saslauth:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
mfc9:x:500:500::/home/mfc9:/bin/bash
mfc01:x:501:501::/home/mfc01:/bin/bash
mfc02:x:502:502::/home/mfc02:/bin/bash
mfc03:x:503:503::/home/mfc03:/bin/bash
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/false
ntp:x:38:38::/etc/ntp:/sbin/nologin
mfc19:x:504:505::/home/mfc19:/bin/bash
[root@node0924 a]# 

```

`cp /etc/passwd ./`  准备文件



```shell
[root@node0924 a]# cut -d ":" -f1 passwd
root
bin
daemon
adm
lp
sync
shutdown
halt
mail
uucp
operator
games
gopher
ftp
nobody
vcsa
saslauth
postfix
sshd
mfc9
mfc01
mfc02
mfc03
mysql
ntp
mfc19
[root@node0924 a]# 

```

`cut -d ":" -f1 passwd`打印所有的用户名,以`:`为分隔符，打印第1列



```shell
[root@node0924 a]# ls
1dir  2dir  3dir  adir  ctxt.txt  passwd  profile  test2.txt  test.txt  xdir  ydir  zdir  zfg
[root@node0924 a]# cat ctxt.txt
angelababy 10
dilireba 11
zhangxinyi 8
zhangxinyi 8
Angelababy 10
[root@node0924 a]# 

```

`cat ctxt.txt`  准备文本



```shell
[root@node0924 a]# sort -t ' ' -k1 ctxt.txt
angelababy 10
Angelababy 10
dilireba 11
zhangxinyi 8
zhangxinyi 8
[root@node0924 a]# 

```

`sort -t ' ' -k1 ctxt.txt`  根据名字的字典序排序



```shell
[root@node0924 a]# sort -t ' ' -k1 -u ctxt.txt
angelababy 10
Angelababy 10
dilireba 11
zhangxinyi 8
[root@node0924 a]# 

```

`sort -t ' ' -k1 -u ctxt.txt`  去掉重复的行 `-u`



```shell
[root@node0924 a]# sort -t ' ' -k1 -u -f ctxt.txt
angelababy 10
dilireba 11
zhangxinyi 8
[root@node0924 a]# 

```

`sort -t ' ' -k1 -u -f ctxt.txt`  忽略大小写 `-f`



```shell
[root@node0924 a]# sort -t ' ' -k2 ctxt.txt
angelababy 10
Angelababy 10
dilireba 11
zhangxinyi 8
zhangxinyi 8
[root@node0924 a]# sort -t ' ' -k2 -n ctxt.txt
zhangxinyi 8
zhangxinyi 8
angelababy 10
Angelababy 10
dilireba 11
[root@node0924 a]# sort -t ' ' -k2 -n -r ctxt.txt
dilireba 11
Angelababy 10
angelababy 10
zhangxinyi 8
zhangxinyi 8
[root@node0924 a]# 

```

`sort -t ' ' -k2 ctxt.txt`  按第二列排序，字典序

`sort -t ' ' -k2 -n ctxt.txt` 按第二列排序，数字，升序 `-n`

`sort -t ' ' -k2 -n -r ctxt.txt` 按第二列排序，数字，降序 `-r`



![image-20201116230728470](../image/image-20201116230728470.png)

sort 排序



```shell
[root@node0924 a]# ls
1dir  2dir  3dir  adir  ctxt.txt  passwd  profile  test2.txt  test.txt  xdir  ydir  zdir  zfg
[root@node0924 a]# cat ctxt.txt
angelababy 10
dilireba 11
zhangxinyi 8
zhangxinyi 8
Angelababy 10
[root@node0924 a]# wc ctxt.txt
 5 10 71 ctxt.txt
[root@node0924 a]# 

```

`wc ctxt.txt`  统计数据

```
 5 10 71 ctxt.txt
```

统计数据

* 5 行数据
* 10个单词
* 71个字节



```shell
[root@node0924 a]# cat -A ctxt.txt
angelababy 10^M$
dilireba 11^M$
zhangxinyi 8^M$
zhangxinyi 8^M$
Angelababy 10^M$
[root@node0924 a]# 

```

`cat -A ctxt.txt`   查看文本



```shell
[root@node0924 a]# man wc
[root@node0924 a]# 

```

`man wc` 查看命令



```shell
[root@node0924 a]# wc -w ctxt.txt
10 ctxt.txt
[root@node0924 a]# wc -l ctxt.txt
5 ctxt.txt
[root@node0924 a]# wc -c ctxt.txt
71 ctxt.txt
[root@node0924 a]# 

```

`wc -w ctxt.txt`  10个单词

`wc -l ctxt.txt` 5行数据

`wc -c ctxt.txt` 71个字节



```shell
# 和管道配合使用，统计数据
[root@node0924 a]# cat ctxt.txt | wc
      5      10      71
# 数据行数
[root@node0924 a]# cat ctxt.txt | wc -l
5
# 数据字节数
[root@node0924 a]# cat ctxt.txt | wc -c
71
# 数据单词书
[root@node0924 a]# cat ctxt.txt | wc -w
10
# passwd数据行数，即用户数
[root@node0924 a]# cat passwd | wc -l
26
[root@node0924 a]# 

```

`cat ctxt.txt | wc` 统计数据，配合管道使用。



