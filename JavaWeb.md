# HTTL & CSS

## 引言

- B/S软件结构

B/S(Broswer/Server)

**客户端 <--------> 服务器端**

客户端：浏览器

服务器端：WEB服务器

- 前端开发流程

|      PS ——>      |      Html ——>      |           JSP            |
| :--------------: | :----------------: | :----------------------: |
| 根据需求设计网页 | 将设计做成静态网页 | 将静态网页修改为动态网页 |

- 网页组成部分

**内容、表现、行为**

内容（结构）是在页面中可以看到的数据，一般内容使用html技术实现

表现指这些内容在页面上的展现形式；比如布局、颜色、大小等，一般使用css技术实现

行为指页面中元素与输入设备交互的响应，一般使用javascript技术实现

## HTML

### 简介

- 介绍

HTML超文本标记语言，通过标签来标记要显示的网页中的各个部分，网页文件本身是**文本文件**

- 创建HTML文件

1.创建一个web工程（静态的web工程）

2.在工程下创建html文件

e.g.

```html
<!DOCTYPE html> <!-- 约束，声明 -->
<html lang="zh_CN"> <!-- html标签，表示html开始 lang="zh_CN"表示中文 html标签一般分为两部分，分别是head和body -->
<head> <!-- 表示头部信息，一般包含title标签，css样式，js代码 -->
    <meta charset="UTF-8"> <!-- 表示当前界面使用utf8字符集 -->
    <title>标题</title> <!-- 表示标题 -->
</head>
<body> <!-- body标签是整个html界面显示的主体内容 -->
    helloworld
</body>
</html>
```

- 书写规范

\<html>	表示整个页面的开始
	\<head>	头信息
		\<title>标题\</title>
	\</head>
	\<body>	body是页面主题内容
		页面主题内容
	\</body>
\</html>	表示整个页面的结束		

### 标签

- html标签介绍

1.标签格式

​	`<标签名>封装数据</标签名>`

2.标签名大小写不敏感

3.标签拥有自己的属性

​	i.基本属性：bgcolor = "red"			可以修改简单样式效果

​	ii.事件属性：onclick = "alert('你好！');"			可以直接设置事件响应后代码

4.标签又分为单标签和双标签

​	i.单标签格式：<标签名/> 			也称自结束标签

​	ii.双标签格式：<标签名>...封装数据...</标签名>

- 语法

1.标签不能交叉嵌套

2.标签必须正确闭合

3.属性必须有值，属性值必须加“”

4.注释不能嵌套

- 常用标签介绍

**1.`font`字体标签**

\<font>可以规定文本的字体，颜色，尺寸

在HTML4.01中，font元素不建议使用

使用样式（替代\<font>）来定义字体，颜色，尺寸



**2.特殊字符**

e.g.把\<br/>作为文本显示在页面

```html
<body>
    &lt;br\&gt;
</body>
```

常见特殊字符

| 特殊字符 | 描述 | 字符编号 |
| -------- | ---- | -------- |
| <        | 小于 | \&lt;    |
| >        | 大于 | \&gt;    |
| &        | 和号 | \&amp;   |
| "        | 引号 | \&quot;  |
|          | 空格 | \&nbsp;  |

注：通常情况下，html会裁掉文档中的空格（或连续空白字符），如果连续输入10个空格，则会去掉9个空格

​		使用\&nbsp;就可以在文档中增加空格



**3.标题标签**

h1-h6 都是标题标签

h1最大，h6最小

`align`：对其属性 ，left左对齐（默认），center居中，right右对齐 



==**4，超链接属性**==

在网页中所有点击之后可以跳转的内容都是超链接

e.g.演示

```html
<a href="https://www.baidu.com/">百度</a> <!-- 跳转至百度的超链接 -->
```

超链接属性

1.href：设置连接地址

2.target：设置进行跳转目标；

​					_self			表示当前页面（默认）

​					_blank			表示打开新的窗口



**5.列表标签**

- 无序列表
- 有序列表
- 定义列表

无序列表格式：

\<ul>
	\<li>内容1\</li>
	\<li>内容2\</li>
	\<li>内容3\</li>
\</ul>

type属性可以修改列表项前面符号（**存在兼容问题**）

有序列表格式

\<ol>
	\<li>内容1\</li>
	\<li>内容2\</li>
	\<li>内容3\</li>
\</ol>



**6.img标签**

img标签可以在html页面上显示图片

​		在web中，路径分为相对路径和绝对路径

​				相对路径：

​						`.`					表示当前文件所在目录

​						`..`					表示当前文件所在的上一级目录

​						`文件名`			表示当前文件所在目录的文件，相当于`./文件名`

​				绝对路径：

​						`http://ip:port/工程名/资源路径`

​		==src属性可以设置图片路径==

​		width属性设置图片宽度

​		height属性设置图片高度

​		border属性设置图片边框大小

​		alt属性设置当指定路径找不到图片时用来替代显示的文笔内容

e.g.

```html
<img src='' width='' height='' border='' /> 
```



==**7.表格标签**==

\<table>\</table>		表格标签

\<th>\<th>					表头标签

\<tr>\</tr>					表行标签

\<td>\</td>					单元格标签				

e.g.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <table border="1" width="300" height="300" align="center" cellspacing="0"> <!-- 修改表格边框，宽高，表格对齐方式，单元格间距 --> 
        <!-- align也可以设置表格在页面文本对齐方式 -->
        <!-- cellspacing设置单元格间距 -->
        <tr>
            <th>1.1</th>
            <th>1.2</th>
            <th>1.3</th>
        </tr>
        <tr>
            <td>2.1</td> <!-- align设置单元格文本对齐方式 -->
            <td>2.2</td>
            <td>2.3</td>
        </tr>
        <tr>
            <td>3.1</td>
            <td>3.2</td>
            <td>3.3</td>
        </tr>
    </table>
</body>
</html>
```

- 跨行跨列设置

colspan属性跨行（向右占行）

rowspan属性设置跨列 （向下占列）



**8.iframe标签**

iframe内嵌窗口标签，可以在一个html页面上打开一个小窗口，去加载一个单独的页面

```html
<iframe src="页面路径名">
    
</iframe>
```

e.g.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Iframe使用</title>
</head>
<body>
    <!--
        iframe标签和a标签组合使用
        1.在iframe中使用name属性定义一个名称
        2.在a标签的target属性上设置iframe的name的属性值
    -->
    <iframe width="300" height="400" name="menu"></iframe><br/>
    <ul>
        <li><a href="web01.html">web01</a></li>
        <li><a href="web02.html">web02</a></li>
        <li><a href="web03.html">web03</a></li>
    </ul>
</body>
</html>
```



**9.表单标签**

表单就是html页面中用于收集用户信息的所有元素集合，然后把这些信息发送给服务器

e.g.

```html
<!DOCTYPE html>
<html lang="zh_CN">
<head>
    <meta charset="UTF-8">
    <title>表单</title>
</head>
<body>
     <!--
        form标签就是表单
            <fieldset>定义一组相关的表单元素，并使用边框包裹起来;而<legend>定义<fieldset>元素的标题
            <label>为表单中的各个控件定义标题

            <input>定义输入框
            input type=text是文本输入框 value设置文本框默认值
            input type=password是密码输入框 maxlenth限制长度
            input type=radio是单选框 通过name属性将单选框进行分组 checked="checked"表示默认选中
            input type=checkbox是复选框 同样checked属性用于默认选择
            input type=rest是重置按钮 value属性可以修改按钮中内容
            input type=submit是提交按钮 value属性可以修改按钮中内容
            input type=button是按钮 value属性可以修改按钮中内容
            input type=file是文件域
            input type=hidden是隐藏域
                当我们要发送某些信息，而这些信息不希望用户参与，就可以使用隐藏域（提交时同样会发送给服务器）

            select标签是下拉列表框
                option标签是下拉列表的选项
                可通过selected="selected"默认选中

            textarea表示多行文本输入框 （起始标签和结束标签中的内容是默认值
                rows属性设置可以显示行数，超过则使用滚动条
                cols属性设置可以显示列数
	
		可以通过table标签来格式化表单，使其更为工整
     -->
   <form name="注册信息"> 	<!-- name设置表单的名称 -->
        <fieldset>
           <legend>注册信息</legend>
        <table>
            <tr>
                <td><label>用户名称：</label></td>
                <td>
                    <input type="text" value="默认值name"/><br/>
                </td>
            </tr>
            <tr>
                <td><label>密&nbsp;;码:</label></td>
                <td>
                    <input type="password" maxlength="3"/><br/>
                </td>
            </tr>
            <tr>
                <td><label>确认密码：</label></td>
                <td><input type="password" maxlength="3"/><br/></td>
            </tr>
            <tr>
                <td><label>性&nbsp;别：</label></td>
                <td>
                    <input type="radio" name="sex" checked="checked"/>男
                    <input type="radio" name="sex" />女<br/>
                </td>
            </tr>
            <tr>
                <td><label>兴趣爱好：</label></td>
                <td>
                    <input type="checkbox" name="hobby"/>Java
                    <input type="checkbox" name="hobby"/>CPP
                    <input type="checkbox" name="hobby"/>PHP<br/>
                </td>
            </tr>
            <tr>
                <td><label>国籍：</label></td>
                <td>
                    <select>
                        <option>---请选择国籍---</option>
                        <option selected="selected">中国</option> selected设置默认选中
                        <option>美国</option>
                        <option>日本</option>
                    </select><br/>
                </td>
            </tr>
            <tr>
                <td><label>自我评价：</label></td>
                <td>
                    <textarea rows="10" cols="20" ></textarea><br/>
                </td>
            </tr>
        </table>
            <input type="reset" value="重新设置"/> <!-- 重置 -->
            <input type="submit" value="确定"/> <!-- 提交 -->
            <input type="file"/>
            <input type="hidden"/>
       </fieldset>
    </form>
</body>
</html>
```

效果

![](https://github.com/Tofweod/NoteImg/raw/main/src/JavaWeb/HTML/HTML01.png)

- 细节

action属性：设置提交的服务器地址

method属性：设置提交的方式——get(默认)，post

**表单提交时，数据没有发送给服务器的三种情况**

​	1.表单项没有name属性值(所以每个表单项都需要有name)

​	2.单选，复选，下拉列表中的option标签没有value属性

​	3.表单项不在提交的form标签中

get请求的特点：

​	1.浏览器地址栏中地址是：action属性[+?+请求参数]

​		请求参数格式是：name=value&name=value

​	2.**不安全**

​	3.有数据长度的限制（如果包含非ASCⅡ字符或超过100个字符，必须使用 method="post"）

post请求的特点：

​	1.浏览器地址栏中地址只有action属性值

​	2.相对于get请求更为安全

​	3.理论上没有数据长度限制



**10.其他标签**

- div标签

div标签默认独占一行

- span标签

span标签的长度是封装数据的长度

- p标签（段落标签）

p标签默认会在段落的上方和下方各空出一行（如果有空行则不再空行）

**这些标签都用于封装文本文字**

e.g.演示

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Other</title>
</head>
<body>
    <div>div标签1</div>
    <div>div标签1</div>
    <span>span标签1</span>
    <span>span标签2</span>
    <p>段落标签1</p>
    <p>段落标签2</p>
</body>
</html>
```

效果

![](https://github.com/Tofweod/NoteImg/raw/main/src/JavaWeb/HTML/HTML02.png)



## CSS



