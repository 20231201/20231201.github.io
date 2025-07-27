---
title: docker安装与html5基础
---

# docker安装与html5基础

​      December 06, 2023            9474    

[TOC]

## 虚拟机docker安装

### pip安装

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)pip安装

### bash脚本

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)bash脚本

docker安装完成

![docker start docker-wordpress-nginx](../img/docker start docker-wordpress-nginx.png)

## ssh登录

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)ssh登录

## html5基础

### 基础元素

```
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<!-- TemplateBeginEditable name="doctitle" -->
<title>html5基础</title>
<!-- TemplateEndEditable -->
<!-- TemplateBeginEditable name="head" -->
<!-- TemplateEndEditable -->
</head>
<body>
<b> 	定义粗体文本
<em> 	定义着重文字
<i> 	定义斜体字
<small> 定义小号字
<strong>定义加重语气
<sub> 	定义下标字
<sup> 	定义上标字
<ins> 	定义插入字
<del> 	定义删除字
<br>
sup
strong
<p>p</p>
<p>abc<img src="../img/docker start docker-wordpress-nginx.png" width="70" height="20" alt="1"/>def</p>
<table border="1">
	<tr>
    	<td>1</td>
        <td>2</td>
        <td>3</td>
    </tr>
    <tr>
    	<td>4</td>
        <td>5</td>
        <td>6</td>
    </tr>
</table>
<form action="/submit_form" method="post">  
<label for="fname">First Name:</label><br>  
<input type="text" id="fname" name="fname"><br>  
<label for="lname">Last Name:</label><br>  
<input type="text" id="lname" name="lname"><br>  
<label for="email">Email:</label><br>  
<input type="email" id="email" name="email"><br>  
<label for="pwd">Password:</label><br>  
<input type="password" id="pwd" name="pwd"><br>  
<input type="submit" value="Submit">  
</form>   
</body>
</html>
```

| head   | 定义了文档的信息                   |
| ------ | ---------------------------------- |
| title  | 定义了文档的标题                   |
| base   | 定义了页面链接标签的默认链接地址   |
| link   | 定义了一个文档和外部资源之间的关系 |
| meta   | 定义了HTML文档中的元数据           |
| script | 定义了客户端的脚本文件             |
| style  | 定义了HTML文档的样式文件           |

### 链接

以下是 HTML 中创建链接的基本语法和属性：`<a>` 元素：创建链接的主要HTML元素是`<a>`（锚）元素。`<a>`元素具有以下属性：

- `href`：指定链接目标的URL，这是链接的最重要属性。可以是另一个网页的URL、文件的URL或其他资源的URL。

- `target`（可选）：指定链接如何在浏览器中打开。常见的值包括 `_blank`（在新标签或窗口中打开链接）和 `_self`（在当前标签或窗口中打开链接）。

- `title`（可选）：提供链接的额外信息，通常在鼠标悬停在链接上时显示为工具提示。

- `rel`（可选）：指定与链接目标的关系，如 nofollow、noopener 等。

  出现形式：

- 一个未访问过的链接显示为蓝色字体并带有下划线。

- 访问过的链接显示为紫色并带有下划线。

- 点击链接时，链接显示为红色并带有下划线。

### css

CSS 可以通过以下方式添加到HTML中:

- 内联样式- 在HTML元素中使用”style” **属性** 
- 内部样式表 -在HTML文档头部 `<head>` 区域使用`<style>` **元素** 来包含CSS
- 外部引用 - 使用外部 CSS文件

背景色属性（background-color）定义一个元素的背景颜色.

我们可以使用font-family（字体），color（颜色），和font-size（字体大小）属性来定义字体的样式:

```
<h1 style="font-family:verdana;">一个标题</h1> <p style="font-family:arial;color:red;font-size:20px;">一个段落。</p>
```

使用 text-align（文字对齐）属性指定文本的水平与垂直对齐方式.

内部样式表：

当单个文件需要特别样式时，就可以使用内部样式表。你可以在`<head>`  部分通过 `<style>`标签定义内部样式表:

```
<head>
<style type="text/css">
body {background-color:yellow;}
p {color:blue;}
</style>
</head>
```

外部样式表：

当样式需要被应用到很多页面的时候，外部样式表将是理想的选择。使用外部样式表，你就可以通过更改一个文件来改变整个站点的外观。

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

在 HTML 中，图像由`<img>` 标签定义。

<img> 是空标签，意思是说，它只包含属性，并且没有闭合标签。

要在页面上显示图像，你需要使用源属性（src）。src 指 “source”。源属性的值是图像的 URL 地址。

定义图像的语法是：

```
<img src="url" alt="some_text"><!--URL 指存储图像的位置-->
```

alt 属性用来为图像定义一串预备的可替换的文本。

替换文本属性的值是用户定义的。

```
<img src="2.gif" alt="Big Boat">
```

height（高度） 与 width（宽度）属性用于设置图像的高度与宽度。

属性值默认单位为像素:

```
<img src="3.jpg" alt="Pulpit rock" width="304" height="228">
```

### 表单

```
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<!-- TemplateBeginEditable name="doctitle" -->
<title>无标题文档</title>
<!-- TemplateEndEditable -->
<!-- TemplateBeginEditable name="head" -->
<!-- TemplateEndEditable -->
</head>
<body>
<label for="name">姓名：</label>
<input type="text" id="name" name="name" required><br>
<label for="password">密码：</label>
<input type="password" id="password" name="password" required><br>
    <label>性别:</label>
    <input type="radio" id="male" name="gender" value="male" checked>
    <label for="male">男</label>
    <input type="radio" id="female" name="gender" value="female">
    <label for="female">女</label>
<br>
<p>爱好</p>
<label for="subscribe1">1</label>
<input type="checkbox" id="subscribe1" name="subscribe">
<label for="subscribe2">2</label>
<input type="checkbox" id="subscribe2" name="subscribe" >
<label for="subscribe3">3</label>
<input type="checkbox" id="subscribe3" name="subscribe" >
<br>
<label for="country">国家</label>
<select id="country" name="country">
	<option value="">cn</option>
    <option value="">usa</option>
    <option value="">uk</option>
</select>
</body>
</html>
```

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)表单

### 实现类似http://www.hunan.gov.cn/的页面

```
<!DOCTYPE html>  
<html>  
<head>  
  <meta charset="UTF-8">  
  <title>湖南省政府网站</title>  
  <style>  
    body {  
      font-family: Arial, sans-serif;  
      margin: 0;  
      padding: 0;  
    }  
    header {  
      background-color: #333;  
      color: #fff;  
      padding: 10px;  
      text-align: center;  
    }  
    nav {  
      background-color: #555;  
      color: #fff;  
      padding: 10px;  
      text-align: center;  
    }  
    nav ul {  
      list-style-type: none;  
      margin: 0;  
      padding: 0;  
      overflow: hidden;  
    }  
    nav ul li {  
      float: left;  
    }  
    nav ul li a {  
      display: block;  
      color: #fff;  
      text-align: center;  
      padding: 14px 16px;  
      text-decoration: none;  
    }  
    main {  
      margin: 15px;  
    }  
    article {  
      margin-bottom: 30px;  
    }  
    article h1 {  
      font-size: 24px;  
    }  
    article p {  
      font-size: 16px;  
    }  
    aside {  
      background-color: #f1f1f1;  
      padding: 10px;  
    }  
    footer {  
      background-color: #333;  
      color: #fff;  
      padding: 10px;  
      text-align: center;  
    }  
  </style>  
</head>  
<body>  
  <header>  
    <nav>  
      <ul>  
        <li><a href="#">首页</a></li>  
        <li><a href="#">新闻</a></li>  
        <li><a href="#">政务公开</a></li>  
        <li><a href="#">互动交流</a></li>  
        <li><a href="#">专题专栏</a></li>  
        <li><a href="#">联系我们</a></li>  
      </ul>  
    </nav>  </header>  <nav>   <ul>   <li><a href="#">政策法规</a></li><li><a href="#">发展规划</a></li><li><a href="#">财政资金</a></li><li><a href="#">公共资源</a></li><li><a href="#">人事信息</a></li></ul></nav><main>   <article>   <h1>欢迎来到湖南省政府网站</h1>   <p>此网站旨在提供湖南省政府的相关信息。</p>   <p></p>   <figure>
    <img src="屏幕截图 2023-12-07 162816.png" width="1000" alt="Image 1"><figcaption></figcaption></figure>   <figure>
    <img src="2.png" width="1000" alt="Image 2"><figcaption></figcaption></figure>   <figure>
    <img src="3.png" width="1000" alt="Image 3"><figcaption></figcaption></figure>   <figure>
    <img src="4.png" width="1000" alt="Image 4"><figcaption></figcaption></figure></article><article>   <h2>相关链接</h2>   
    <ul>   
    <li><a href="#">链接1</a></li>
    <li><a href="#">链接2</a></li>
    <li><a href="#">链接3</a></li>
    <li><a href="#">链接4</a></li>
    </ul>
</article></main>
<footer>&copy; 2023 湖南省政府。保留所有权利。</footer>
</body>
</html>
```