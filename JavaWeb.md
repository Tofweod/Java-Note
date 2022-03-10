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

### 介绍

- CSS技术介绍

CSS是层叠样式表单，是用于（增强）控制网页样式并允许将样式信息与网页内容分离的一种标记性语言

- CSS语法

```css
p{
    font-size:80px;
}
/*
	p------------选择器
	fontsize-----属性
	80px---------值
*/
```

选择器：浏览器根据选择器决定CSS样式影响的html元素（标签）

属性：是要改变的样式名，并且每个属性都有一个值；

​			属性和值用冒号分开，并由花括号包围，这样组成一个简单的完整的样式声明 e.g.`p{color:red}`

多个声明：如果要定义不止一个声明，则需要用分号将每个声明隔开

​					注：一般每行只描述一个属性

CSS注释：/\*注释内容\*/

### CSS与HTML结合方式

- 方式1

在标签的**style属性**上设置"key:value"，修改标签样式

```html
<div style="color:red;border:1px;border-style: solid;" >div标签1</div>
```

缺点：

​	1.样式多了代码冗长

​	2.可读性非常差

​	3.CSS代码没有复用性



- 方式2

在head标签中使用sytle标签定义各种需要的css样式

格式：

```css
xxx{
    Key:value value;
    Key:value value;
}
```

e.g.

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- style标签专门用来定义css样式代码,里面是css代码 -->
    <style type="text/css">
        div{
            color:red;
            border:1px;
            border-style:solid;
        }
    </style>
</head>
```

注：style里的注释应使用/**/

问题：

​	1.只能在同一页面复用代码，不能在多个页面复用css代码

​	2.维护不方便，如果有很多页面就要到每个页面修改，工作量巨大



- **方式3**

把css样式写为一个单独的css文件，再通过==link标签==引入

e.g.

```css
// 1.css文件
div{
    color:red;
    border:1px solid orange;
}
```

把css样式引入html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- link标签专门引入css样式 -->
    <link rel="stylesheet" type="text/css" href="1.css"/>
</head>
<body>
    <div>div标签1</div><br/>
    <div>div标签1</div><br/>
</body>
</html>
```



### CSS选择器

- 标签名选择器

格式：

```css
标签名{
	属性:值;
}
```

标签名选择器，可以决定哪些标签被动地使用样式



- id选择器

格式：

```css
#id属性值{
    属性:值;
}
```

id选择器可以通过id属性**选择性**的去选择使用样式

e.g.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #id001{
            color:blue;
            font:30px;
            border:yellow 1px solid;
        }

        #id002{
            color:red;
            font:20px;
            border:blue 5px dashed;
        }
    </style>
</head>
<body>
    <div id="id001">div标签 id001</div><br/>
    <span id="id002">span标签 id002</span><br/>
</body>
</html>
```



- class选择器（类型选择器）

class类型选择器格式：

```css
.class属性值{
    属性:值;
}
```

class选择器可以通过class属性有效的选择性去使用样式

e.g.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .class01{
            color:blue;
            font:30px;
            border:1px yellow solid;
        }
    </style>
</head>
<body>
    <div class="class01">div标签 class01</div><br/>
    <span class="class01">span标签 class01</span><br/>
</body>
</html>
```



- 组合选择器

格式：

```css
选择器1，选择器2...选择器n{
    属性:值;
}
```

组合选择器可以让多个选择器公用同一个css代码

### 常用样式

1.字体颜色

`color : red`;

颜色也可以用rgb值和十六进制表示值（后者必须加#），如rgb(255,0,0),#00F6DE



2.宽度和高度

`width : 1px; height : 1px;`

宽高可以写像素值（单位px），也可以写百分比值



3.背景颜色`background-color : blue;`



4.字体大小`font-size`



5.边框设置

`border : color size style`



6.DIV居中(DIV框相对于页面居中)

`margin-left : auto;`

`margin-right : auto;`



7.文本居中

`text-align : center;`



8.超链接去下划线

`text-decoration : none;`



9.表格细线

```css
table{
    border:1px solid black; // 设置边框
    border-collapse:collapse; // 边框合并 table和td间隔去除，并合并为一条细线
}
td{
    border:1px solid black; // 设置边框
}
```



10.列表去修饰

```css
ul{
    list-style:none;
}
```



# JavaScript

## 介绍

- 基本介绍

JavaScript语言诞生主要是完成页面的数据验证，因此运行在客户端，需要运行浏览器来解析执行JavaScript代码

**JS是弱类型，Java是强类型**

弱类型：类型可变

强类型：定义变量时类型已确定且不可变



- 特点

1.交互性（可以做的就是信息的动态交互）

2.安全性（不允许直接访问本地硬盘）

3.跨平台性（只要是可以解释js的浏览器都可以执行，和平台无关）



- JavaScript和HTML结合

**方式1**

在head标签或body标签中使用script标签来书写JavaScript代码

```html
<script type="text/javascript">
    // javascript代码
</script>
```



**方式2**

使用script标签引入单独的javascript代码文件

```html
<script type="text/javascript" src="js文件路径"></script>
```

注：script标签可以用来定义js代码，也可以用来引入js文件；但是两个功能不能混用



## 变量

**变量是可以存放某些值的内存的命名**



- JavaScript变量类型

数值类型：number

字符串类型：string

对象类型：object

布尔类型：boolean

**函数类型**：function



- JS特殊值

undefined：未定义，所有js变量未赋予初始值时的默认值

null：空值

NAN：not a number，非数值



- JS定义变量格式

```javascript
var 变量名;
var 变量名 = 值;
```

e.g.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        var i;
        alert(i) // undefined
        i = 12;
        // typeof函数返回变量数据类型
        alert(typeof(i)) // number
        i = "123";
        alert(typeof(i)); // string
    </script>
</head>
<body>
</body>
</html>
```



- 关系（比较）运算

等于 ： ==			简单的字面值的比较

**全等于**： ===		除了做字面值比较外，还会比较两个变量数据类型

e.g.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        var a = 12;
        var b = "12";
        alert(a==b); // true
        alert(a===b); // false
    </script>
</head>
<body>
</body>
</html>
```



- 逻辑运算

且运算：&&

或运算：||

取反运算：!

**在javascript中所有变量都可以作为一个boolean类型的变量去使用**

`0,null,undefined,"(空串)"`都认为是false



&&运算两种情况

第一种：当表达式全为真，返回最后一个表达式的值

第二种：当表达式中有一个假时，返回第一个为假的表达式的值



||运算两种情况

第一种：当表达式全为假，返回最后一个表达式的值

第二种：当表达式中有一个真时，返回第一个为真的表达式的值

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        var a = "abc";
        var b = true;
        var c = null;
        var d = false;

        // &&运算
        alert(a&&b); // true
        alert(b&&a); // true
        alert(a&&c); // null
        alert(a&&d); // fasle;
        alert(a && c && d); // null

    </script>
</head>
<body>
</body>
</html>
```

注：**&&与||均有短路** 



- **数组运算**

JS中数组定义格式：

```css
var 数组名 = []; // 空数组
var 数组名 = [1,"abc",true]; // 定义数组并赋值，且元素类型可以不同
```

e.g.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        var arr = []; // 定义空数组
        arr[0] = 12;
        alert(arr.length); // 1
        arr[2] = "abc";
        alert(arr.length); //3
        // 数组遍历
        for (var i = 0; i < arr.length; i++) {
            alert(arr[i]);
        }
    </script>
</head>
<body>
</body>
</html>
```

JS中数组只要通过数组下标赋值，**最大下标值就会自动扩容数组**，中间未赋值的值是undefined



## ==函数==

**函数定义**

方式1：使用function关键字来定义函数

```css
function 函数名(形参列表){
    函数体
}
```

e.g.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        // 定义函数
        function fun01(){
            alert("函数被调用")
        }
        // 调用函数
        fun01();
    </script>
</head>
<body>
</body>
</html>
```



方式2：

