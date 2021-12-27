[TOC]

# Web基础知识

## HTML基本概念

HyperText Markup Language（<u>超文本</u>**标记语言**）

超文本：用HTML编写的文档中可以包含指向其他文档或资源的链接，即超链接

标记：HTML文档是由一些**标签**（**tag**）组成的文本文件，标签标识了内容和类型

### HTML基本格式

```html
<!-- 指定HTML文档的版本和类型，使浏览器解析结果唯一 -->
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN""http://www.w3.org/TR/html4/loose.dtd">
<html>
    <head>
		<!-- 标题 -->
        <!--meta：提供原信息，供机器解读-->
        <!-- 例子：声明文档使用的字符编码：写法一、二等价 -->
        <!-- 写法一： -->
        <meta charset="utf-8">
        <!-- 写法二：添加http请求的请求头信息：Content-Type:"text/html; charset=utf-8" -->
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <!-- link：链接外部文件 -->
        <!-- 例子：链接css样式文件 -->
        <link rel="stylesheet" href="${pageContext.request.contextPath}/client/style.css" type="text/css" />
    </head>
    <body>
        <!-- html文档中显示的内容 -->
    </body>
</html>
```

| 标签名         | 说 明                 | 标签名    | 说 明        |
| -------------- | --------------------- | --------- | ------------ |
| \<html\>       | HTML文档的开始        | \<br\>    | 换行         |
| \<head\>       | 文档的头部            | \<hr\>    | 水平线       |
| \<title\>      | 文档的标题            | \<a\>     | 锚           |
| \<meta>        | 关于XHTML文档的元信息 | \<img\>   | 图像         |
| \<link>        | 文档与外部资源的关系  | \<table\> | 表格         |
| \**<script\>** | **客户端脚本**        | \<tr\>    | 表格中的行   |
| \<style\>      | 样式信息              | \<td\>    | 表格中的单元 |
| \<body\>       | 文档的主体            | \<form\>  | 表单         |



### HTML标签

[更多标签可查看](https://www.runoob.com/tags/html-reference.html)

标签的格式：

双标签：`<标签名>封装的数据</标签名>`

单标签：`<标签名 />`

`<br />`：换行

`<hr />`：水平线

标签也可以拥有自己的属性：

1. 基本属性，如：`bgcolor='red'`：背景颜色为红色
2. 事件（触发）属性，如：`onclick="alert('你好！')"`：点击后触发警告框，显示’你好！‘



#### 标题标签:h1-h6

其中h1字号最大，h6字号最小

其中可以添加的属性有`align`: "right", "center", "left" ->分别表示右对齐，居中，左对齐

如：`<h1 align="right">标题名</h1>`



#### 超链接标签: `<a></a>`

常用属性：

href="skip_url"

target="\_self"（在当前页面跳转）/"\_blank"（跳转到新的页面）[默认为\_self]



#### 列表标签

无序列表(unorder list)：`<ul></ul>`

有序列表(order list)：`<ol></ol>`

列表中的每一项(list item)：`<li></li>`

常用属性：

type：用来设置列表中每一项前的符号，如.*^%$#等等都可以设置

例子：

```html
<h3>
    羽毛球五大项
</h3>
<ul>
    <li>男单</li>
    <li>女单</li>
    <li>男双</li>
    <li>女双</li>
    <li>混双</li>
</ul>
```



#### img标签

作用：用于显示图片

属性：

**src：**设置源路径，在*web中路径*分为相对路径和绝对路径

​	相对路径：

​		.					当前文件所在目录

​		..				   表示当前文件所在的上一级目录

​		文件名 		表示当前文件所在目录下的某文件，相当于‘ ./文件名 ’

​	绝对路径：

​	如：`http://ip:port/工程名/资源路径`

**width, height：**用于设置在页面上显示的图片的大小

**border:**给图片加边框，数值表示边框粗细

**alt:**设置当src下的文件找不到时用来替代的文本内容

例子：

```html
<img src="img0.png" width=200 height=200 border="1" alt="图片找不到"/>
```



#### 表格标签

```html
<!-- tr：行， td：列 -->
<table>
    <tr>
    	<td>内容</td>
    </tr>
</table>
```

`<b></b>`：加粗标签

`<th>内容</th>`  的效果等价于 `<td align="center">内容</td>` 

table属性：

`cellpadding`：创建单元格内容与其边框之间的空白

td属性：

`colspan`：单元格跨列（短宽）

`rowspan`：单元格跨行（瘦长）

​	如：`cellpadding="5"`



#### iframe标签

作用：在当前窗口上建一个内联窗口



#### 表单标签

- what is 表单？
- 表单是html页面中用来==收集==用户信息的所有元素集合，然后把这些信息==发给服务器==

例子：

```html
<!-- form标签表示表单 -->
<form>
    <!-- input type="text" 表示文本输入框 
		 事件处理属性：onmouseover：鼠标经过触发事件
					onblur：失去焦点（鼠标离开文本框）触发事件
					onclick：鼠标点击触发事件
	-->
    用户名：<input type="text" /><br />
    <!-- input type="password" 表示密码输入框 -->
    密码：<input type="password" /><br />
    <!-- input type="radio" 表示单选按钮(radio button)，其中属性name的功能是分组-->
    <!-- 如果name的值一致，那么他们就属于同一组，一组中只有一个button能被按下-->
    <!-- 可以用属性checked="checked"设置默认项 -->
    性别：男<input type="radio" name="sex"/>女<input type="radio" name="sex"/><br />
    <!-- input type="checkbox" 表示多选框 -->
    掌握编程语言：C++<input type="checkbox" />Java<input type="checkbox" />Python<input 		type="checkbox" /><br />
    <!-- select 表示下拉列表框 -->
    <!-- options标签表示一个选项，若该项为默认项，可以用 selected="selected"选中 -->
    国籍：<select>
        <option>--请选择国籍--</option>
        <option>中国</option>
        <option>美国</option>
        <option>英国</option>
    </select><br />
	<!--textarea标签表示多行文本输入框 属性rows,cols设置多少行，每行写多少个字-->
	自我评价：<textarea rows="5" cols="20">默认值</textarea><br />
	<input type="reset" value="重置" />
	<input type="submit" value="提交" />
	<input type="button" value="按钮" />
	<input type="file" value="文件上传"/>
	<!-- input type="hidden" 这里面的value对于用户不可见，用于发送一些不需要用户参与的信息 -->
	<input type="hidden" name="hid" value="隐藏信息" />
</form>
```



#### frameset标签

作用：

用来定义一个框架集，`<frameset>` 元素被用来组织一个或者多个` <frame>` 元素。每个` <frame>` 有各自独立的文档。

`<frameset>` 中的每个` <frame>` 都可以设置不同的属性，比如 border, scrolling, noresize 等等。



## HTTP协议

超文本传输协议（HyperText Transfer Protocol）

定义：它规定了Web客户与服务器之间如何通信，是一个基于==请求——响应==的==无状态==协议

==特点：==

- **HTTP是无连接**：无连接的含义是<u>限制每次连接只处理一个请求</u>。服务器处理完客户的请求，并收到客户的应答后，<u>即断开连接</u>。采用这种方式可以节省传输时间。
- **HTTP是媒体独立的**：这意味着，只要客户端和服务器知道如何处理的数据内容，<u>任何类型的数据都可以通过HTTP发送</u>。客户端以及服务器指定使用适合的MIME-type内容类型。
- **HTTP是无状态**：HTTP协议是无状态协议。无状态是指<u>协议对于事务处理没有记忆能力</u>。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。

### 请求：

```
请求行 -> 	请求方式(get/post) 请求URL地址 HTTP协议版本
请求头 -> 	放一些服务器要使用的附加信息
(request header)比如人机识别、爬与反爬机制等
请求体（实体内容） ->	请求参数（具体要请求获取的信息）
```

- **GET**：向特定的资源发出请求，==从服务器上获取数据==。==如将参数直接放在URL之后==（就是把数据放置在HTTP请求行中）
  - url中?后面的即为传输数据，多个参数间用&连接
  - 限制 **form** 表单数据必须为 **ASCII** 字符

- **POST**：传输数据给服务器进行增删改等操作，向指定资源==提交==数据进行处理请求（例如==提交表单或者上传文件==）。==数据被包含在请求体中==。POST请求可能会导致新的资源的创建和/或已有资源的修改。
  - 支持整个 **ISO10646** 字符集


### 响应：

```
状态行 ->	HTTP协议版本 状态码(status code) 状态码描述
响应头 ->	放一些客户端要使用的附加信息（重要）
(response header)cookies，密钥等
响应体（实体内容） ->	服务器返回的真正客户端要用的内容（HTML,JSON）等
```

**HTTP状态码** 由三个十进制数字组成，第一个十进制数字定义了状态码的类型，后两个数字没有分类的作用。

| 类型  | 类型描述                                       |
| ----- | ---------------------------------------------- |
| **1** | 信息，服务器收到请求，需要请求者继续执行操作   |
| **2** | 成功，操作被成功接收并处理                     |
| **3** | 重定向，需要进一步的操作以完成请求             |
| **4** | 客户端错误，请求包含语法错误或无法完成请求     |
| **5** | 服务器错误，服务器在处理请求的过程中发生了错误 |

#### 常见的HTTP状态码：

- **200** - 请求成功
- **301** - 资源（网页等）被永久转移到其它URL
- **404** - 请求的资源（网页等）不存在
- **500** - 内部服务器错误



## Tomcat服务器

定义：它是运行Servlet和JSP的**容器**，即提供了Servlet和JSP功能的**服务器**。

特点：默认端口是8080，可以通过编辑 $tomcat-install\conf\server.xml文件中Connector元素的port属性修改其端口号；要想使用Tomcat，必须先安装Java运行时环境

### Web应用默认页面的配置

<u>一个Web应用可以配置==多个==默认页面</u>

在Tomcat服务器根目录下的\conf文件夹中的web.xml文件中可以修改默认页面。

实际使用时，若没有指定据图要访问的页面资源，Tomcat会按照\<welcome-file-list\>元素中指定默认页面的==顺序==，依次查找这些默认页面。

### 如何将web工程部署到Tomcat中？

<u>只需将web工程整个目录拷贝到Tomcat的webapps目录下即可</u>

## 万维网工作原理

1. 输入URL
2. URL服务器名--->DNS域名解析--->IP地址
3. 给IP地址对应的服务器发HTTP请求
4. 服务器回发HTTP应答
5. 浏览器解析并显示应答中的内容给客户



## Web体系结构

- web服务器：提供web页面和其他资源，上面装有能够提供web服务的软件
  - 常见的web服务器：==Tomcat==
- web客户端：用户通过客户端访问web资源
  - 浏览器



## 万维网的核心部分：三个标准

- 统一资源标识符URI
  - 作用：资源定位的统一形式
- 超文本传送协议HTTP
  - 是浏览器和WEB服务器通信的基础，是应用层协议
- 超文本标记语言HTML



## URI和URL

URI构成：资源名称

URL构成：传输协议+主机地址（IP or 域名）+端口号+资源名称(URI)       [端口号和资源名称可省略]



# Java web三大语言

- **HTML** 			定义了网页的内容
- **CSS**				描述了网页的布局
- **JavaScript** 	表达网页的动作，行为



## CSS基本格式

Cascading Stylesheets（层叠样式表）

作用：设置HTML页面中的文本内容（字体、大小、对齐方式等）、图片的外形（宽高、边框样式、边距等）以及==版面的布局==等外观显示样式

### 选择器

#### 标记选择器

用html标记名称作为选择器，即`< >`中的内容

```css
选择器{属性1:属性值1;属性2:属性值2;属性3:属性值3;}
```

#### 类选择器

用html页面中元素的class属性值作为选择器，使用" . "进行标识

```css
.类名{属性1:属性值1;属性2:属性值2;属性3:属性值3;}
```

#### id选择器

用html页面中元素的id属性值作为选择器，使用" # "进行标识

```css
#id名{属性1:属性值1;属性2:属性值2;属性3:属性值3;}
```

#### 通配符选择器

能匹配页面中4

的所有元素（实际应用中不建议使用）

```css
*{属性1:属性值1;属性2:属性值2;属性3:属性值3;}
```



### 使用链入式将css文件链接到html/jsp文件中

```jsp
<head>
    <link href="CSS文件的路径" type="text/css" rel="stylesheet" />
</head>
```

`ref`：定义当前文档与被链接文档之间的关系。"stylesheet"表示被链接的文档是一个样式表文件



# Servlet

## Servlet基本概念

**定义：**==使用java语言编写的运行在服务器端的程序==。主要用于处理客户端发送的HTTP请求，并返回一个响应



## Servlet的生命周期

**Servlet不是独立的应用程序，它不能由用户或程序员直接调用，它的产生与销毁完全由容器（Web容器）管理。**

三大阶段：初始化阶段、运行阶段、销毁阶段

<u>在整个生命周期中，service()方法被调用多次，init(),destroy()方法仅被调用一次</u>

==[图P85]==：

1. 客户端发送请求
2. 由Servlet容器来解析请求
3. 查找容器内是否已有该Servlet实例对象，若无，Servlet容器创建Servlet实例对象
4. 运用init()方法初始化Servlet程序的参数
5. 运用service()方法处理请求
6. 返回处理结果给Servlet容器
7. Servlet容器返回响应给客户端
8. ==当服务器关闭或该Web应用被移出容器==时，运行destroy()方法销毁Servlet程序



servlet程序的配置文件：

### web.xml

```xml
<!-- 用于注册（定义）一个servlet -->
<servlet>
    <servlet-name>servlet名称</servlet-name>
    <servlet-class>servlet完整类名</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>servlet名称（与上面<servlet>中定义的必须相同）</servlet-name>
    <!--
		url-pattern:配置访问地址
		/  斜杠在服务器解析的时候，表示地址为：http://ip:port/工程路径
		即/asite  表示地址为：http://ip:port/工程路径/asite
	-->
    <url-pattern>/asite</url-pattern>
</servlet-mapping>
```

#### \<servlet-mapping\>

作用：用于映射一个Servlet程序的对外访问路径，也叫作==虚拟路径==

特性：

- 同一个Servlet程序==可以被映射成多个虚拟路径==，即客户端可以通过多个路径实现对同一个Servlet实例对象的访问
- 按照==最具体原则==进行虚拟路径与Servlet程序的匹配

##### 虚拟路径中通配符的用法

- \*.扩展名：如"*.do"表示匹配所有**结尾**为“\*.do"的url地址
- /*：如"/abc/\*"匹配所有以"/abc"**开始**的URL地址

<u>两种用法不能混用！！！</u>

##### 缺省Servlet

/：用于处理其他所有Servlet都不处理的访问请求



## HttpServlet类

<u>一般在实际项目开发中，都是使用==继承HttpServlet类==的方法来实现Servlet程序</u>

作用：专门用于**创建**应用于==HTTP协议==的**Servlet**

功能：

- 根据用户请求方式的不同，定义对应的doXxx()方法处理用户请求
- 通过service()方法将HTTP请求和响应分别转为HttpServletRequest和HttpServletResponce类型的对象

具体操作步骤：

1. 定义一个类继承HttpServlet类
2. 根据业务需要重写doGet()或doPost()方法
3. 到web.xml中配置servlet程序的访问地址



## ServletConfig接口

**定义+作用：**用于加载Servlet的==初始化参数==。当Tomcat初始化一个Servlet的时候，会将该Servlet的配置信息封装到一个ServletConfig对象中。

在一个Web应用中可以存在多个ServletConfig对象——==ServletConfig对象与Servlet程序对应==

可以在web.xml文件中获取对应的Servlet由\<init-param\>进行配置的配置信息，该元素位于\<servlet\>下

[例子：P105]

用法：

`ServletConfig config = this.getServletConfig();`

` string answer = config.getInitParameter("encoding");`



## ServletContext接口

**定义+作用：**当 Servlet容器 启动时，会==为每个 **Web** 应用创建一个唯一的 **ServletContext** 对象==代表当前的 **Web** 应用，该对象封装了当前 **Web** 应用的所有信息。

可以在web.xml文件中获取由\<context-param\>进行配置的整个web应用的初始化信息，该标签位于根元素\<web-app\>下[例子：P106]

用法：

`ServletContext context = this.getServletContext();`

`Enumeration<String> paramNames = context.getInitParameterNames();`



## 请求和响应

Web服务器收到一个http请求，会针对每个请求创建一个**HttpServletRequest**和**HttpServletResponse**对象

Servlet调用service()方法时：

- 从客户端取数据找 **HttpServletRequest**
- 向客户端发送数据找 **HttpServletResponse**

### HttpServletResponse类

每次请求进来，Tomcat服务器都会创建一个Response对象传递给Servlet程序去使用。

HttpServletResponse类的对象专门用来<u>封装HTTP响应信息</u>

<u>在HttpServletResponse接口中定义了==向客户端发送==响应状态码、响应信息头、响应信息体的方法</u>供我们调用



#### 两个输出流的说明

==两者互相排斥，不可同时使用==

**getOutputStream()**：

直接输出==字节==数组中的==二进制==数据，常用于下载，所获取的字节输出流对象为(Servlet)OutputStream类型

**getWriter()**：

直接输出==字符==文本内容，所获取的字符输出流对象为PrintWriter类型

```Java
package example;
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class First extends HttpServlet{
	public void doGet(HttpServletRequest request, HttpServletResponse response)
		throws ServletException, IOException {
		
	String data = "hey my princess";
	PrintWriter out = response.getWriter();
	out.write(data);
			
//	OutputStream out = response.getOutputStream();
//	out.write(data.getBytes());
	}
	public void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
	doGet(request,response);
	}
}
```



##### 解决中文乱码输出的问题

<u>问题出现的原因：计算机中数据传输过程中数据都是二进制。故当传输文本时，会产生字符与字节的转换。</u>

<u>字符与字节的转换靠查码表完成，发送方和接收方使用的==码表不同==，就会造成乱码</u>



因为中文用UTF-8编码，故我们要通知：

- HttpServletResponse（服务器）
- 浏览器（客户端）

使用utf-8编码输出



有两种方案可以实现上述的两个步骤：

推荐使用`response.setContentType("text/html;charset=utf-8");`，一步到位

```java
package example;
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class First extends HttpServlet{
	public void doGet(HttpServletRequest request, HttpServletResponse response)
		throws ServletException, IOException {
		
	String data = "华南理工大学";
	response.setContentType("text/html;charset=utf-8");
	PrintWriter out = response.getWriter();	
	out.write(data);
        
//	response.setCharacterEncoding("utf-8");服务器端
//	PrintWriter out = response.getWriter();
//	response.setHeader("Content-Type", "text/html;charset=utf-8");客户端
//	out.write(data);
	}
	public void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
	doGet(request,response);
	}
```



### HttpServletRequest类

HttpServletRequest接口专门用来<u>封装HTTP请求信息</u>

在HttpServletRequest接口中<u>定义了获取请求行、请求头和请求消息体的相关方法</u>==供服务器端调用==

#### 常用方法：

**String getMethod()：**用于获取HTTP请求消息中的请求方式（如GET、POST等）

**String getContextPath()：**用于获取请求URL中属于WEB应用程序的路径，表示相对于整个WEB站点的根目录

**String getParameter(String name)：**用于获取某个指定名称的参数值，如果请求消息中没有包含指定名称的参数，getParameter()方法返回null；如果请求消息中包含有多个该指定名称的参数，getParameter()方法返回第一个出现的参数值

**String[] getParameterValues(String name)：**获得HTTP请求消息中的同一个参数名所对应的所有参数值

**Map getParameterMap()：**用于将请求消息中的所有参数名和值装入进一个Map对象中返回



#### 解决请求参数的中文乱码问题

`req.setCharacterEncoding()`方法：用于设置request对象的解码方式

*注：这种解决乱码的方式==只对POST方式有效==，对GET方式无效*

`req.setCharacterEncoding("utf-8")`



#### 综合例子

验证登录信息成功后跳转到新的网页，否则重定向到原来的网页

前提：需要在/firstServlet/login.html中设置表单数据提交到该servlet程序中

```java
package example;
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class First extends HttpServlet{
	public void doGet(HttpServletRequest request, HttpServletResponse response)
		throws ServletException, IOException {
	response.setContentType("text/html;charset=utf-8");
	String username = request.getParameter("username");
	String password = request.getParameter("password");
	if (("hxy").equals(username) && ("123").equals(password)){
		response.sendRedirect("/firstServlet/welcome.html");
	}
	else {
		response.sendRedirect("/firstServlet/login.html");
	}

	}
	public void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
	doGet(request,response);
	}
}
```



## 重定向

`response.sendRedirect("...");`

定义：Web服务器端在响应第一次请求的时候，让客户端（浏览器）再向另外一个URL发出请求，从而达到转发的目的。==它本质上是两次HTTP请求，对应两个request对象。==

具体过程：

1. 用户在浏览器端输入特定URL，请求访问服务器端的某个组件。

2. 服务器端的组件返回一个状态码为302的响应结果，该响应结果的含义为：

   让浏览器端再请求访问另一个Web组件，在响应结果中提供了另一个Web组件的URL。另一个Web组件有可能在同一个Web服务器上，也有可能不在同一个Web服务器上。

3. ==当浏览器端接收到这种响应结果后，再立即自动请求访问另一个Web组件==。

4. 浏览器端接收到另一个Web组件的响应结果。

作用：封装了某个路径所指定的资源



## RequestDispatcher对象

### 请求转发：

`request.getRequestDispatcher("...").forward(request,response);`

定义：在Servlet中，如果当前Web资源不想处理请求时，可以<u>通过forward()方法将当前请求传递给其他的Web资源</u>进行处理==[书P138图]==

特点：

- ==整个过程客户端只发一次请求==
- ==客户端（浏览器）上看到的地址不会发生变化==
- 两个web资源共享Response域中的数据
- *可以转发到WEB-INF目录下（浏览器不可以直接访问该目录下内容，但请求转发可以进来）*
- 不可以访问该工程以外的资源

```java
//获取另外一个WEB资源的相对路径(the_turn_path)
ResquestDispatcher dispatcher = request.getRequestDispatcher("/the_turn_path");
//将request,response对象传递给另外一个web资源
dispatcher.forward(request,response);
```

另外，还可以用一对方法通过Request对象传递数据，这样可以用来验证转发信息过来的WEB资源的身份

例子：

发送方：`request.setAttribute("name","EllenHe");`

接收方：`String name = (String)request.getAttribute("name");`

​				`其中name=="EllenHe"`

### 请求包含

`request.getRequestDispatcher("...").include(request,response);`

定义：当客户端访问Servlet1时，Servlet1通过<u>调用include()方法将其他资源（如Servlet2）包含了进来</u>

[与请求转发的相同点：也是将Servlet请求转发给其他WEB资源进行处理]

特点：

<u>当请求处理完毕后，回送给客户端的响应结果既包含Servlet1的响应结果，也包含其他资源（如Servlet2）的响应结果==[书P140图]==</u>



```java
//获取另外一个WEB资源的相对路径(the_turn_path)
ResquestDispatcher dispatcher = request.getRequestDispatcher("/the_turn_path?p1=abc");
//将request,response对象传递给另外一个web资源
dispatcher.include(request,response);
```



## Session会话及其会话技术

==会话管理就是管理浏览器客户端和服务器端之间会话过程中产生的会话数据==

### Cookie对象

cookie是一种会话技术，以<u>键值对</u>的方式存在

特点：将==用户的信息保存在客户端==（用户各自的浏览器）中

*注：一个cookie的大小不能超过4kb，且Cookie数据只能是非中文的字符串类型的数据*

**工作原理：**==[图P145]==

1. 当用户通过浏览器==第一次==访问该Web服务器时，==服务器向客户端发送cookie==
2. 接下来，浏览器每次访问该Web服务器时，都会在==请求头(Request Header)中将cookie==发送给服务器端

#### Cookie API

javax.servlet.http.Cookie类

##### cookie的构造方法

```java
Cookie ck = new Cookie(String name,String value)
```

cookie一经创建，<u>name不可修改</u>，而value允许被修改

下面通过一个使用cookie技术实现显示用户上次访问时间的功能的例子了解一下cookie类的基本操作：

*注：name为"lastAccess"的cookie对象的值即为用户上次访问时间*

只展示关键部分代码：

```java
	String lastAccessTime = null; //用来储存用户上次访问时间
	Cookie[] cookies = req.getCookies();
	for (int i=0; cookies!=null && i<cookies.length; i++){
        //获取cookie对象名字
        if ("lastAccess").equals(cookies[i].getName()){
            //获取cookie对象的值
            lastAccessTime = cookies[i].getValue();
            break;
        }
    }
	//显示用户上次访问时间
	if (lastAccessTime == null){
        resp.getWriter().print('你是首次访问本站！！！');
    }
	else{
        resp.getWriter().print('你上次访问时间是'+lastAccessTime);
    }
	//创建一个当前时间的标准格式化字符串
	String currentTime = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss").format(new Date());
	//重新创建一个记录了当前访问时间的Cookie	
	Cookie cookie = new Cookie("lastAccess",currentTime);
	//将Cookie封装到服务器应答信息中并发送
	resp.addCookie(cookie);
```

#### cookie的存活时间

在==默认情况==下，Cookie对象的Max-Age属性的值为-1，即==浏览器关闭时，删除这个对象==。

可以通过setMaxAge()方法进行设置，让Cookie对象<u>在客户端的存活时间</u>更长 [单位：秒]，（将Cookie数据保存在浏览器所在机器的硬盘）

例子：

设置cookie存活时间为1小时

`cookie.setMaxAge(60*60)`



### Session对象

特点：

- 是一种==将会话数据保存在服务器端==的技术
- session技术依赖于cookie技术，如果cookie被禁用，session也将失效

*注：一个session的大小可以超过4kb，session中可以储存中文字符串，<u>可以保存对象</u>*

**工作原理：**

1. 当客户端访问Web服务器时，==Servlet容器就会创建==一个Session对象和ID属性，并且把ID属性值以Cookie的形式封装在应答中发送给客户端

   ​		==ID和客户端一一对应==

2. 当客户端后续请求访问Web服务器时，==服务器从它的请求头中获取cookie值==（Session ID）,服务器就能判断出该请求是哪个客户端发出的，从而选择对应的Session对象为其服务

```java
import javax.servlet.http.*;
import xxx.User;
..........
// 如果不存在 session 会话，则创建一个 session 对象
HttpSession session = request.getSession();  
// 将一个名为name的对象保存进session中
session.setAttribute(String name,Object value);
// 获取session中名为name的值（String类）
String value = session.getAttribute(String name);
// 获取session中名为name的值（对象），比如获取User类对象
User user = (User) session.getAttribute(String name);
// 删除session中名为name的属性
session.removeAttribute(String name);
// 删除整个session对象
session.invalidate()
```



## Filter过滤器

### 功能

对Servlet容器调用Servlet的过程进行拦截，从而在Servlet进行响应==处理前后==实现一些特殊功能。==[图：P232]==

1. 客户端发送一个请求，被Filter==预处理==后再交给服务器中具体的目标资源。

   ​	<u>目标资源包括：html页面，jsp页面，Servlet程序，文本，图片，视频等等</u>

2. 服务器中的资源处理完后，回发一个响应，被Filter预处理后再返还给浏览器端，显示给用户。

Filter应用到Servlet程序上的顺序与其在web.xml中\<filter-mapping\>所在位置有关。

### 生命周期

<u>类似servlet的：</u>

其中最大的区别是：==在WEB应用程序加载时即调用init()方法创建Filter实例对象==，`init(FilterConfig config)`

每次请求映射的虚拟路径符合\<url-pattern\>的WEB资源时调用doFilter方法

在Web应用程序卸载时调用destroy()方法销毁Filter实例对象

### 重要的类对象参数

#### FilterConfig

<u>类似ServletConfig</u>

作用：获取filter过滤器的配置内容

包括：

获取Filter的名称，即filter-name的内容

获取在Filter中配置的init-param（初始化参数）

获取ServletContext对象

### 配置方法

#### 在web.xml文件中配置

```xml
<!-- 配置Filter -->
     <filter>  
         <filter-name>LogFilter</filter-name>  
         <filter-class>com.mucfc.LogFilter</filter-class>  
     </filter>  
     <filter-mapping>  
         <filter-name>LogFilter</filter-name>  
         <url-pattern>/*</url-pattern><!-- 表示处理根目录下的所有请求 -->
         <!-- dispatcher用于指定被过滤器拦截的资源被Servlet容器的调用方式 -->
         <!-- 默认值是REQUEST -->
         <dispatcher>xxxx</dispatcher>
     </filter-mapping>
```

##### \<dispatcher\>子元素可以设置的值及其意义

- **REQUEST**：当用户**直接访问**页面时，Web容器将会调用过滤器。如果目标资源是通过RequestDispatcher的include()或forward()方法访问时，那么该过滤器就不会被调用。
- **INCLUDE**：如果目标资源是**通过RequestDispatcher的include()方法访问**时，那么该过滤器将被调用。除此之外，该过滤器不会被调用。
- **FORWARD**：如果目标资源是**通过RequestDispatcher的forward()方法访问**时，那么该过滤器将被调用，除此之外，该过滤器不会被调用。
- **ERROR**：如果目标资源是**通过声明式异常处理机制调用**时，那么该过滤器将被调用。除此之外，过滤器不会被调用。

#### 直接在java文件中使用注解

```java
@WebFilter(filterName="log",urlPatterns={"/*"})
public class LogFilter implements Filter {
.................................
}
```

### Filter接口中的方法

`doFilter(ServletRequest request, ServletResponse response, FilterChain chain)`：

用于拦截和响应，可以用于做权限检查（比如是否登录）、设置输出文本的格式



## Listener监听器

监听的是**事件**

### 事件监听器在进行工作时，分为3个步骤

1. 将监听器绑定到事件源（产生事件的对象），也就是注册监听器
2. 事件发生时会触发监听器的成员方法，即事件处理器，传递事件对象
3. 事件处理器通过事件对象获得事件源，并对事件源进行处理

### 常用监听器接口

[详见书P254]

- 监听 **Session**、**request**、**context** 等==域对象的创建与销毁==，分别为 **HttpSessionListener**、**ServletContextListener**、**ServletRequestListener**
  - 域对象的作用范围：
    - context：整个web应用
    - session：一个用户使用该web应用
    - request：一个用户对该web应用发起一次请求

- 监听==域对象属性的增加和删除==，分别为： **HttpSessionAttributeLister**、**ServletContextAttributeListener**、**ServletRequestAttributeListener**
- 监听==域对象属性的状态改变==，分别为：**HttpSessionBindingListener**、**HttpSessionActivationListener**

==[使用例子：P258-259]==

`implements 具体接口`

### web.xml文件中Listener的配置

```xml
<listener>
	<listener-class>xxxx</listener-class>
</listener>
```

### 生命周期

<u>类似Filter的</u>

- 实例化：web容器启动时
- 调用：事件触发性
- 销毁：web容器关闭or重新加载该web应用时



# JSP (Java Service Page)

### 基本概念

#### 定义

建立在Servlet规范之上的动态网页开发技术。

#### 特点

- 在JSP文件中，HTML代码和Java代码共同存在
- HTML代码用来实现网页中静态内容的展示
- Java代码用来实现网页中动态内容的展示

#### 运行原理

==[图P172]==

1. 客户端发送请求，请求访问JSP文件
2. JSP容器先将一个JSP文件转换成一个JAVA源文件（其中定义的类间接地继承了HttpServlet类）
3. 若上一步骤成功，JSP容器将生成的JAVA源文件编译成相应的字节码文件*.class。该\*.class文件就是一个Servlet
4. 由Servlet容器给这个Servlet创建一个实例（该实例常驻内存），并执行Servlet的jspinit()方法
5. 执行jspService()方法来处理客户端的请求。对于每一个请求，JSP容器都会创建一个==新的线程==来处理它
6. 当需要销毁这个Servlet时，会执行jspDestroy()方法，将这个Servlet实例加入“垃圾收集”处理

#### 生存周期

==[图P172]==图6-6左边那幅自己画的

<u>类似Servlet程序</u>

当你通过 http ==请求==一个 JSP 页面时，首先 JSP容器会==调用 _jspService()方法==将JSP编译成为 Servlet，然后执行 Servlet。<u>_jspService()方法在每个request中被调用一次</u>并且负责产生与之相对应的response，并且它还负责产生所有7个HTTP方法的回应，比如GET、POST、DELETE等等。

### JSP基本语法

#### JSP脚本元素

通过JSP脚本元素将Java代码嵌入HTML页面中

##### JSP Scriptlets

一段普通的代码段

```javascript
<% java代码（变量、方法、表达式等） %>
```

##### JSP声明语句

用于==声明（定义）==变量和方法

在JSP声明语句中声明的方法在整个JSP页面内有效，但是在方法内定义的变量只在该方法内有效

```javascript
<%!
    定义的变量或方法等
%>
```

##### JSP表达式

用于将程序数据输出到客户端，它将要输出的变量或表达式直接封装在以"<%="开头和以"%>"结尾的标记中

==表达式之后不能有";"==

```javascript
<%= 要输出的变量或表达式 %>
```

##### JSP注释

注：写在*.jsp文件中的HTML注释会被显示在客户端

```javascript
<%-- 注释内容 --%>
```

### 与Servlet的比较

联系：JSP本质上还是Servlet，JSP文件在用户第一次请求时会被编译成Servlet，然后再由Servlet处理用户的请求

区别：

- 在MVC模式中，Servlet扮演控制器角色，JSP扮演视图角色
- Servlet中没有内置对象 

### JSP指令

#### page指令

**作用**：对页面的某些特性进行描述，特性包括编码方式、采用的语言等

*作用域：整个页面，与其书写的位置无关*

```jsp
<%@ page 属性名1="属性值1" 属性名2="属性值2"... %>
```

##### 常用属性

| 属性名       | 属性值or取值范围                                             |
| ------------ | ------------------------------------------------------------ |
| language     | java                                                         |
| pageEncoding | 当前页面编码格式 (utf-8)                                     |
| contentType  | 客户端根据该属性判断文档类型(text/html; charset=utf-8)与response.setContentType同 |
| import       | 导入包或类                                                   |

#### include指令

**作用**：在JSP页面中静态包含一个文件，文件类型包括HTML文件、JSP文件、文本文件等

```jsp
<%@ include file="被包含的文件地址" %>
```

*插入文件的路径必须使用相对于文件的相对路径*

#### taglib指令

引入一个自定义标签集合的定义，包括库路径、自定义标签

```jsp
<%@ taglib uri="uri" prefix="prefixOfTag" %>
```

**uri** 属性确定标签库的位置，**prefix** 属性指定标签库的前缀。

### JSP隐含对象（无需重新手动创建）

隐式对象：JSP页面中需要频繁使用的对象，JSP中提供了9个隐式（内置）对象，无需开发者显式创建

完整版：[书：P182]

下面详细介绍三个：

#### out对象

javax.servlet.jsp.JspWriter类的实例对象

用于向客户端发送文本内容

它的作用与ServletResponse.getWriter()方法返回的PrintWriter对象非常相似，

区别是：

out对象的类型为JspWriter，它相当于一种==带缓存功能==的PrintWriter  ==[书P183图]==

只有调用了ServletResponse.getWriter()方法，缓冲区中的数据才能真正写入到Servlet引擎所提供的缓冲区中，按队列==顺序==先进先出。==[例子：P183-184]==

#### pageContext对象

javax.servlet.jsp.jspContext类的实例对象

作用：用于获取JSP其他8个隐式对象

pageContext对象的作用范围(scope)有四个值，即为JSP四大域对象[书：P185-186]

##### JSP四大域对象

域对象：<u>可以存取数据的对象。</u>

这四个域对象功能一样，不同的是它们对数据的存取范围

- pageContext
  - 当前jsp页面范围内有效
- request
  - 一个请求内有效
- session
  - 一个会话范围内有效（打开客户端访问服务器，直到关闭客户端）
- application
  - 整个web工程范围内有效（在web工程启动时创建，在web工程停止时销毁）

#### exception对象

java.lang.Exception类的实例对象

只有page指令中指定了属性`isErrorPage="true"`的JSP页面才可以使用



## JSP动作

### \<jsp:include\>动作元素

作用：把指定文件插入正在生成的页面

web容器首先会编译被包含的页面，然后将编译处理后的返回结果包含在页面中，之后编译包含页面，最后将两个页面组合的结果回应给浏览器。

*注：被引用的资源在当前JSP页面输出内容后才被调用，但一般看不出来*

```jsp
<jsp:include page="relative URL" flush="true" />
```

### \<jsp:forward\>动作元素

作用：将当前请求转发到其他web资源。在执行请求转发之后当前页面将不再执行，而是执行该元素指定的目标页面

```jsp
<jsp:forward page="relative URL" />
```

### 用于在JSP页面中轻松使用JavaBean

#### \<jsp:useBean\>动作元素

作用：用来装载一个将在JSP页面中使用的 **JavaBean** 。

==\<jsp:useBean\>中的id与\<jsp:setProperty\>和\<jsp:getProperty\>中的name是一样的==

```jsp
<jsp:useBean id="name" class="package.class" />

<jsp:useBean id="name" class="package.class">
    ...
    <jsp:setProperty ... />
</jsp:useBean>
```

| 属性     | 描述                                                        |
| -------- | ----------------------------------------------------------- |
| class    | 指定Bean的完整包名。                                        |
| type     | 指定将引用该对象变量的类型。                                |
| beanName | 通过 java.beans.Beans 的 instantiate() 方法指定Bean的名字。 |

#### \<jsp:setProperty\>动作元素

作用：用来设置已经实例化的Bean对象的属性

```jsp
<jsp:setProperty name="myName" property="someProperty" .../>
```

可以放置在\<jsp:useBean\>元素的外面或者\<jsp:useBean\>元素的里面

| 属性     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| name     | 表示要设置属性的是哪个Bean。                                 |
| property | 表示要设置哪个属性。有一个特殊用法：如果property的值是"*"，表示所有名字和Bean属性名字匹配的请求参数都将被传递给相应的属性set方法。 |
| value    | value 属性是可选的。该属性用来指定Bean属性的值。value和param不能同时使用，但可以使用其中任意一个。 |
| param    | param 是可选的。它指定用哪个请求参数作为Bean属性的值。       |

### \<jsp:getProperty\>动作元素

作用：提取指定Bean属性的值，转换成字符串，然后输出。

```jsp
<jsp:getProperty name="myName" property="someProperty" .../>
```

| 属性     | 描述                   |
| -------- | ---------------------- |
| name     | 要检索的Bean属性名称。 |
| property | 表示要提取Bean属性的值 |



# EL和JSTL

## JavaBean的基本概念

**定义**：它是Java开发语言中一个可以重复使用的软件构件，==本质上是一个java类==

==特点：它是一种规范，而不是一种技术或工具。==

规范具体如下：

- 它**必须具有一个公共的、无参的构造方法**，这个构造方法可以是编译器自动产生的默认构造方法
- 它**提供公共的setter方法和getter方法（每个属性至少具备get/set方法中的一种）**，让外部程序设置和获取JavaBean的属性
  - ==如果属性类型为boolean：is/get==
  - 属性为其他类型：set/get


### BeanUtils工具

作用：用来操作数据，配合用来封装数据的JavaBean来使用

```
import org.apache.commons.beanutils.BeanUtils;
```

==[例子：P204]==

| 方法声明                                                     | 功能描述                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| static void populate(Object bean, Map<String,?extends Object>properties) | 根据指定的值为相应的javabean属性设置值，以==集合的方式赋值== |
| static void setProperty(Object bean, String name, Object value) |                                                              |
| static ==String== getProperty(Object bean, String name)      | 返回类型一定是String，这里一般我们自己添加类型转换函数       |

## EL的基本概念，标识符，保留字，变量，常量，运算符  

### EL的基本概念

全称：Expression Language

作用：

- 作用在JSP页面中，可以方便地获取Servlet域对象中存储的数据[简化JSP页面的书写]
  - 主要用于==替换==JSP页面中的脚本表达式==<%= %>==
- 当域对象不存在时，EL表达式返回null，不会报错，更推荐在日常开发中使用

语法：

```jsp
${表达式}
```

### 标识符

可以由任意大小写字母、数字、下划线组成

但要满足以下规范：

- 不能以数字开头
- 不能是EL中的保留字，如and/or/gt
- 不能是EL隐式对象，如pageContext

### 保留字

==[书：P207]==

### 变量

EL表达式中的变量不用事先定义就可以直接使用，可以将变量映射到一个对象上

```jsp
${product}
```

### 常量

#### 布尔常量

true/false

#### 整型常量

跟java语言中写法相同

#### 浮点型常量

跟java语言中写法相同

#### 字符串常量

==字符串本身包含的单引号或双引号需要用反斜杠(\\)进行转义==

<u>若字符串用双引号引起来，那么里面的双引号需要转义；反之亦然</u>

#### null常量

### 运算符

#### 点运算符(.)

用于访问JSP页面中某些对象的==属性==

```jsp
${user.username}
```

#### 方括号运算符([])

与点运算符功能相同

==当获取的属性名中包含一些特殊符号（并非数字or字母），必须用方括号==

```jsp
${user["username"]}

<%-- 特殊用法：取出List中指定索引的某个元素 --%>
${user[i].username}
```

#### 算术运算符

\+      \-       \*        / or div        % or mod

#### 比较运算符

| 符号 | 保留字写法 | 例子                     |
| ---- | ---------- | ------------------------ |
| <    | lt         | \${10<2} or \${10 lt 2}  |
| >    | gt         | \${10>2} or \${10 gt 2}  |
| <=   | le         | \${10<=2} or \${10 le 2} |
| >=   | ge         | \${10>=2} or \${10 ge 2} |

#### 逻辑运算符

&&(and)      ||(or)       ！(not)

#### empty运算符

用于判断某个对象是否为null或""，结果为bool类型

```jsp
${empty var}
```

### EL隐式对象

[书：P211-215]

## JSTL的基本概念，标签  

全称：Java Server Page Standard Tag Library——JSP标准标签库

（起因是jsp支持自定义标签）是Sun公司为了==集成==各大厂商制定的自定义标签的==功能==而制定的一套==标准标签库==。它由<u>5个</u>不同功能的标签库共同组成，封装了JSP应用的通用核心功能。

[书：P216]

### JSTL中的core标签库

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
```

#### \<c:out\>标签

作用：将一段文本内容或表达式的结果输出到客户端

```jsp
<%-- 语法1： --%>
<c:out value=”要显示的数据对象” [escapeXml=”true|false”] [default=”默认值”]>
<%-- 语法2： --%>
<c:out value=”要显示的数据对象” [escapeXml=”true|false”]>
    默认值
</c:out>
```

只有当value=""时，\<c:out\>标签才会输出默认值

escapeXml：是否对特殊字符进行HTML编码转义，若进行转义，则以字符形式输出；若不进行转义，则认为是HTML代码，由客户端进行渲染。默认为true，即进行转义

#### \<c:set\>标签

用于将变量存取于JSP范围中或JavaBean属性中

```jsp
<c:set value="值1" var="name1" [scope="page|request|session|application"]>
```

#### \<c:if\>标签

同程序中的if作用相同，用来实现条件控制

```jsp
<c:if test="条件" var="name" [scope="page|request|session|application"]>
    结果
</c:if>
```

- test属性用于存放判断的条件，一般使用EL表达式来编写。
- var指定名称用来==存放判断的结果==类型为true或false。
- scope用来存放var属性存放的范围。

#### \<c:choose\>标签

相当于if-else语句

##### \<c:when\>标签

##### \<c:otherwise\>标签

没有属性，==必须==作为\<c:choose\>标签的最后分支出现

##### 例子

```jsp
<c:set var="count" value="10" />
<c:choose>
	<c:when test="${count==10}">
    	count与10相等
    </c:when>
    <c:otherwise>
    	count与10不相等
    </c:otherwise>
</c:choose>
```

#### \<c:forEach\>标签

循环标签，根据循环条件遍历集合（Collection）中的元素。

```jsp
<c:forEach var=”name” items=”Collection” varStatus=”StatusName” begin=”begin” end=”end” step=”step”>  
    所有内容  
</c:forEach>
```

- var设定变量名用于存储从集合中取出元素。
- items指定要遍历的集合。
- varStatus设定变量名，该变量用于存放集合中元素的信息。
- begin end用于指定遍历的起始位置和终止位置（可选）。
- step 指定循环的步长。

------

其中varStatus有4个状态属性，如下：

| 属性名 | 类型    | 说明                            |
| ------ | ------- | ------------------------------- |
| index  | int     | 当前循环的索引值（从0开始计数） |
| count  | int     | 循环的次数（从1开始计数）       |
| frist  | boolean | 是否为第一个位置                |
| last   | boolean | 是否为第二个位置                |

#### \<c:forTokens\>标签

用于浏览字符串，并根据指定的字符==将字符串截取==。

```jsp
<c:forTokens items="strigOfTokens" delims="delimiters" [var="name" begin="begin" end="end" step="len" varStatus="statusName"] >
```

- items指定被迭代的字符串。
- delims指定使用的分隔符。
- var指定用来存放遍历到的成员。
- begin指定遍历的开始位置（int型从取值0开始）。
- end指定遍历结束的位置（int型，默认集合中最后一个元素）。
- step遍历的步长（大于0的整型）。
- varStatus存放遍历到的成员的状态信息。

*注：\<c:forToken\>的属性varStatus的使用同\<c:forEach\>的使用方法相同。*

# JDBC

全称：Java数据库连接(Java DataBase Connectivity)

## 定义

JDBC是一套用来执行SQL语句的Java ==API==，它要求<u>各个数据库厂商</u>按照==统一==的规范来<u>提供数据库==驱动==</u>[数据库无关]，在程序中由JDBC和具体的数据库驱动联系。==[图：P262]==

## 实现JDBC程序的六个步骤

1. 针对使用的数据库的版本注册驱动

   ​	比如说我们使用的是Mysql数据库，那么语句就必然是Class.forName("com.mysql.jdbc.Driver");

2. 通过DriverManager（驱动管理）获取一个数据库连接（Conection对象）

3. 针对该连接创建一个Statement对象，用于向数据库发送sql语句

4. 编写sql语句，并用Statement对象来发送、执行该sql语句

   （executeQuery()查询操作对应返回对象是ResultSet）

5. 针对返回结果进行处理

6. 关闭数据库连接，释放资源[顺序是先得到的后关闭，即：rs -> stm -> conn]

例子：

```java
package jdbc;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ConnectDB {
	public static void main(String [] args) throws SQLException{
		Statement stm = null; 
		ResultSet rs = null;
		Connection conn = null;
		try {
			// 1.注册数据库驱动
			Class.forName("com.mysql.jdbc.Driver");
			// 2.通过DriverManager获取数据库连接
			String url = "jdbc:mysql://localhost:3306/jdbc";
			String user = "root";
			String password = "hxy010217";
			conn = DriverManager.getConnection(url, user, password);
			// 3.针对这个连接创建一个Statement对象
			stm = conn.createStatement();
			// 4.编写SQL语句，并用Statement语句执行它
			String sql = "select * from users";
			rs = stm.executeQuery(sql);
			// 5.操作ResultSet数据集（迭代器）
			System.out.println("id | name | password");
			while (rs.next()) {
				int id = rs.getInt("id");// 通过列名获取指定字段的值
				String name = rs.getString("usname");
				String pwd = rs.getString("uspassword");
				System.out.println(id + " | " + name + " | " + pwd);
			}
		} catch (ClassNotFoundException e) {
			e.printStackTrace(); // 若连接出现异常，发异常信息
		}finally {
			// 6.全部操作执行完后，断开连接，释放数据库资源（包括ResultSet,Statement,Connection对象）
			if (rs != null) {
				try {
					rs.close();
				} catch (SQLException e) {
					e.printStackTrace(); // 若释放出现异常，发异常信息
				}
				rs = null;
			}
			if (stm != null) {
				try {
					stm.close();
				} catch (SQLException e) {
					e.printStackTrace(); // 若释放出现异常，发异常信息
				}
				conn = null;
			}
			if (conn != null) {
				try {
					conn.close();
				} catch (SQLException e) {
					e.printStackTrace(); // 若释放出现异常，发异常信息
				}
				conn = null;
			}
		}	
	}
}
```

## JDBC常用API

DriverManager.getConnection

Connection.createStatement

Statement.executeQuery

Statement.executeUpdate

ResultSet.getString("name")

### JDBC工具类

可以<u>自己封装</u>一个工具类**JDBCUtils**

提供获取连接对象、释放连接资源的方法，从而达到代码的重复利用。

```java
conn =JdbcUtils.getConnection();
JdbcUtils.closeResource(conn,stm,rs);
```

### Statement对象

用于执行==静态==SQL语句

<u>每次</u>执行SQL语句时，<u>都会</u>对其进行<u>编译</u>

当相同的SQL语句多次执行时，会使数据库==频繁编译相同==的SQL语句，降低数据库的访问效率

有sql注入的隐患

创建一个Statement对象：

`Statement stm = conn.createStatement();`

### PreparedStatement对象

用于执行==动态==SQL语句

可以对SQL语句进行==预编译==，并将预编译的信息==储存==在PreparedStatement对象中。

当相同的SQL语句再次执行时，程序会使用PreparedStatement对象中的数据，无需再次编译，提高了数据的访问效率。

==还可以解决sql注入问题==：参数使用?作为占位符替代



创建一个PreparedStatement对象：

==必须将要预编译的<u>sql语句作为输入</u>才能成功创建==

```java
String sql = "insert into users(name,pwd,gender,email) values(?,?,?,?)";
PreparedStatement preStmt = conn.PreparedStatement(sql);
preStmt.setString(1,"hexuyi");
preStmt.setString(2,"123456");
preStmt.setString(3,"F");
preStmt.setString(4,"123456@qq.com");
```



## 数据库连接池与DBUtils工具

### 目的

普通的JDBC数据库连接开销很大。数据库连接池技术能够==避免频繁地创建数据库连接==。

<u>好处：无需用户自己来进行分配、管理数据库连接</u>

由数据库连接池==负责分配、管理和释放数据库连接==，它允许应用程序重复使用现有的数据库连接，而不是重新建立。[图P285]



# MVC设计模式

## MVC设计模式的基本概念

MVC提供了一种==按功能==对软件进行模块划分的方法。

将软件程序分为三个核心模块：模型(Model),视图(View),控制器(Controller)

- **控制器**（**Controller**）: 负责转发请求，对请求进行处理。
- **视图**（**View**） : 界面设计人员进行图形界面设计。
- **模型**（**Model**）: 程序员编写程序应有的功能（实现算法等等）、数据库专家进行数据管理和数据库设计(可以实现具体的功能)。

[图P309]：

1. 用户通过视图（界面）发送操作请求给控制器，
2. 控制器收到请求后调用模型的功能、修改数据，
3. 视图查看模型的数据状态
4. 若状态发生改变，模型发送状态改变通知给视图
5. 控制器选择视图来呈现控制器的处理结果和模型中的数据

## 两种常用的设计模式

### JSP Model1

[图P307]：JSP + JavaBeans

特点：**每个请求的目标都是JSP页面**，在该结构中==没有一个核心组件控制==应用程序的工作流程，**所有的业务处理**都使用**JavaBeans**实现。

缺点：

**JSP页面需要负责流程控制和产生用户界面**，对于一个业务流程复杂的大型应用程序来说，在<u>JSP页面中依旧会嵌入大量的java代码</u>，这样会给项目管理带来很大的麻烦。



### JSP Model2

[图：P308]：JSP + Servlet + JavaBean

特点：JSP Model2就是MVC设计模式。

控制器：Servlet，模型： JavaBean，视图：JSP

特点：

Servlet接收浏览器发送的请求，

根据请求信息实例化 JavaBean对象来封装操作数据库后返回的数据，

Servlet选择相应的JSP页面将响应结果显示在浏览器中



# Spring

## Spring的基本概念

Spring ==框架==是一个开源的 **Java 平台**，是轻量级的

创造出来的目的是：为了让<u>企业级开发</u>变得==更简单==

**Spring 的优良特性**

- **非侵入式**： 基于Spring开发的应用中的对象可以不依赖于Spring的API
- **控制反转**： **IOC** —— **Inversion of Control**，指的是将==对象的创建权交给 Spring 去创建==。使用 Spring 之前，对象的创建都是由我们自己在代码中new创建，即程序的<u>控制流程</u>完全由开发者控制。而使用 Spring 之后。对象的创建都是给了 Spring 框架：由Spring IoC容器来管理对象、组件的创建和销毁。
  - Spring创建好B对象，然后存储到一个容器里面，==当A对象需要使用B对象时，Spring就从存放对象的那个容器里面取出A要使用的那个B对象==，然后交给A对象使用
  - 比如对象A需要操作数据库，以前我们总是要在A中自己编写代码来获得一个Connection对象， ==有了 spring 我们就只需要告诉spring，A中需要一个Connection，至于这个Connection怎么构造，何时构造，A不需要知道。==
- **依赖注入**： **DI** —— **Dependency Injection**，是指依赖的对象==不需要手动调用 setXX 方法去设置，而是通过配置赋值。==
  - A需要依赖 Connection才能正常运行，而这个Connection是由spring注入到A中的，依赖注入的名字就这么来的。
- **面向切面编程**： **Aspect Oriented Programming** —— **AOP**
- **容器**：Spring 是一个容器，因为它包含并且管理应用对象的生命周期
- **组件化**：Spring 实现了使用简单的组件配置组合成一个复杂的应用。在 Spring 中可以使用XML和Java注解组合这些对象。
- **一站式**：在 IOC 和 AOP 的基础上可以整合各种企业应用的开源框架和优秀的第三方类库（实际上 Spring 自身也提供了表述层的 SpringMVC 和持久层的 Spring JDBC）

## 依赖注入

到底什么是依赖注入？让我们将这两个词分开来看一看。这里将依赖关系部分转化为两个类之间的关联。例如，==类 A 依赖于类 B==（如果没有了类B，那么类A 也不存在）。现在，让我们看一看第二部分，注入。所有这一切都意味着==类 B 将通过 IoC 被注入到类 A 中==。

## 面向切面编程

- AOP不是一种技术，实际上是==编程思想==。
- 主要思想是<u>提取</u>各个模块可能都要<u>重复操作的部分</u>==[切面Pointcut+Advice]==，写成公共方法
- 基本概念
  - 联结点JointPoint：spring允许你使用通知的地方，有非常多
  - 切点Pointcut：开发者真正选择进行切入的点，即某一联结点
  - 织入weaving：将切面真正加入程序代码的过程
  - 目标target：被织入的对象
- AOP主要做三类事
  - 在==哪里[Pointcut切点]==切入，也就是权限校验等非业务操作在哪些业务代码中执行。
  - 在什么时候切入，是业务代码执行前还是执行后。
  - 切入后==做什么事[Advice通知]==，比如做权限校验、日志记录等。

# Eclipse注意事项

1. 新建dynamic web project后需将tomcat中的两个jar文件添加到该工程的build path中，详情可参考桌面中的图片

2. WEB-INF文件夹中的所有文件对外不可见

3. 在content中放置html文件和jsp文件，其相对访问路径为“/工程名称/对应html文件名” [无需加content]

   



