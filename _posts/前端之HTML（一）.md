---
title: 前端之HTML（一）
tags: HTML,CSS,JS
grammar_cjkRuby: true
---
最近学到前端的一些知识，感觉挺有意思的。总结一下常用的知识。
##### 一 HTML,CSS,JS的关系
一个基本的网站包含很多网页，一个网页又有html,css,js组成。
html 是主题，装载着各种dom元素，css用来装饰dom元素，js用来控制dom元素，DOM是document Object Model,即文档对象模型。
举个例子：比如一个html(内容)是一个美女，css（装饰）就是漂亮的衣服，js（交互）就是优美的动作。
##### 二 HTML介绍
html是用来描述网页的一种语言，它不是一种编程语言，而是一种标记语言（标记标签），总的来说，html使用标记标签来描述网页，本文就用标签来代替标记标签进行说明。学html就是重点学习标签。
###### 2.1 标签（tag）
- HTML 标签是由尖括号包围的关键词，比如 <html>
- HTML 标签通常是成对出现的，比如 <b> 和 </b>
- 标签对中的第一个标签是开始标签，第二个标签是结束标签
- 开始和结束标签也被称为开放标签和闭合标签
比如下面的一个简单的例子：

``` html
<html>
<body>

<h1>我的第一个标题</h1>

<p>我的第一个段落。</p>

</body>
</html>
```
例子解释：

``` javascript
- <html> 与 </html> 之间的文本描述网页
- <body> 与 </body> 之间的文本是可见的页面内容
- <h1> 与 </h1> 之间的文本被显示为标题
- <p> 与 </p> 之间的文本被显示为段落
```
###### 2.2 注释

``` xml
<!-- 注释内容 -->
```
###### 2.3 常用的标签
2.3.1 标题：h1~h6
``` xml
<h1>这是一级标题</h1>
<h2>这是二级标题</h2>
<h3>这是三级标题</h3>
<h4>这是四级标题</h4>
<h5>这是五级标题</h5>
<h6>这是六级标题</h6>
<h7>这是七级标题</h7>
```
2.3.2   HTML 段落
``` html
HTML 段落是通过 <p> 标签进行定义的。
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```
2.3.3 HTML 链接
``` html
HTML 链接是通过 <a> 标签进行定义的。所谓的超链接是指从一个网页指向一个目标的连接关系，这个目标可以是另一个网页，也可以是相同网页上的不同位置，还可以是一个图片，一个电子邮件地址，一个文件，甚至是一个应用程序。
<a href="http://futuretechx.com" target="_blank">this is my blog link</a>
```
> 什么是URL？ 
> URL是统一资源定位器(Uniform ResourceLocator)的缩写，也被称为网页地址，是因特网上标准的资源的地址。 
> URL举例
> http://www.sohu.com/stu/intro.html
> http://222.172.123.33/stu/intro.html
> 
> URL地址由4部分组成 
> 第1部分：为协议：http://、ftp://等  
> 第2部分：为站点地址：可以是域名或IP地址
> 第3部分：为页面在站点中的目录：stu 
> 第4部分：为页面名称，例如 index.html 各部分之间用“/”符号隔开。

href属性指定目标网页地址。该地址可以有几种类型：
绝对URL - 指向另一个站点（比如 href="http://www.jd.com）
相对URL - 指当前站点中确切的路径（href="index.htm"）
锚URL - 指向页面中的锚（href="#top"）
 
target：
_blank表示在新标签页中打开目标网页
_self表示在当前标签页中打开目标网页

2.3.4 HTML 图像

``` html
HTML 图像是通过 <img> 标签进行定义的。图像的名称和尺寸是以属性的形式提供的。
<img src="http://futuretechx.com/wp-content/uploads/2018/11/WeChat-Image_20181106135518.jpg" alt="load fail">
<img src="图片的路径" alt="图片未加载成功时的提示" title="鼠标悬浮时提示信息" width="宽" height="高(宽高两个属性只用一个会自动等比缩放)">
```
2.3.5 水平线
`<hr /> 标签在 HTML 页面中创建水平线。`
2.3.6 换行 

``` xml
<br>
```
2.3.7 加粗

``` xml
<b>加粗</b>
```
2.3.8 斜体

``` xml
<i>斜体</i>
```
2.3.9 下划线

``` xml
<u>下划线</u>
```
2.3.10 删除线

``` xml
<s>删除</s>
```

> HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码。

##### 2.4 特殊字符

| 内容 | 对应代码 |
| ---- | -------- |
| 空格 | `&nbsp;`   |
| >    | `&gt;`     |
| <    | `&lt;`     |
| &    | `&amp;`    |
| ¥    | `&yen;`    |
| 版权 | `&copy;`   |
| 注册 |   `&reg;` |
![特殊字符](./images/1547794273530.png)
##### 2.5 div标签和span标签
段落是通过 <p> 标签定义的。浏览器会自动地在段落的前后添加空行。（<p> 是块级元素）
div标签用来定义一个块级元素，并无实际的意义。主要通过CSS样式为其赋予不同的表现。
span标签用来定义内联(行内)元素，并无实际的意义。主要通过CSS样式为其赋予不同的表现。
块级元素与行内元素的区别：
所谓块元素，是以另起一行开始渲染的元素，行内元素则不需另起一行。如果单独在网页中插入这两个元素，不会对页面产生任何的影响。
这两个元素是专门为定义CSS样式而生的。
注意：
关于标签嵌套：通常块级元素可以包含内联元素或某些块级元素，但内联元素不能包含块级元素，它只能包含其它内联元素。
p标签不能包含块级标签，p标签也不能包含p标签。
##### 2.6 列表
2.6.1 无序列表

``` xml
<ul type="disc">
  <li>第一项</li>
  <li>第二项</li>
</ul>
```
type属性：
 - disc（实心圆点，默认值） 
 - circle（空心圆圈） 
 - square（实心方块） 
 - none（无样式）
 
2.6.2 有序列表

``` xml
<ol type="1" start="2">
  <li>第一项</li>
  <li>第二项</li>
</ol>
```
type属性：
- 1 数字列表，默认值
- A 大写字母
- a 小写字母
- Ⅰ大写罗马
- ⅰ小写罗马
2.6.3 标题列表

``` xml
<dl>
  <dt>标题1</dt>
  <dd>内容1</dd>
  <dt>标题2</dt>
  <dd>内容1</dd>
  <dd>内容2</dd>
</dl>
```
##### 2.7 表格
表格是一个二维数据空间，一个表格由若干行组成，一个行又有若干单元格组成，单元格里可以包含文字、列表、图案、表单、数字符号、预置文本和其它的表格等内容。
表格最重要的目的是显示表格类数据。表格类数据是指最适合组织为表格格式（即按行和列组织）的数据。
表格的基本结构：

``` xml
<table>
  <thead>
  <tr>
    <th>序号</th>
    <th>姓名</th>
    <th>爱好</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <td>1</td>
    <td>小明</td>
    <td>读书</td>
  </tr>
  <tr>
    <td>2</td>
    <td>小红</td>
    <td>喝茶</td>
  </tr>
  </tbody>
</table>
```
属性:
- border: 表格边框.
- cellpadding: 内边距
- cellspacing: 外边距.
- width: 像素 百分比.（最好通过css来设置长宽）
- rowspan: 单元格竖跨多少行
- colspan: 单元格横跨多少列（即合并单元格）
##### 2.8 form
功能：
- 表单用于向服务器传输数据，从而实现用户与Web服务器的交互
- 表单能够包含input系列标签，比如文本字段、复选框、单选框、提交按钮等等。
- 表单还可以包含textarea、select、fieldset和 label标签。

表单属性:

| accept-charset | 规定在被提交表单中使用的字符集（默认：页面字符集）。       |
| -------------- | ---------------------------------------------------------- |
| action         | 规定向何处提交表单的地址（URL）（提交页面）。              |
| autocomplete   | 规定浏览器应该自动完成表单（默认：开启）。                 |
| enctype        | 规定被提交数据的编码（默认：url-encoded）。                |
| method         | 规定在提交表单时所用的 HTTP 方法（默认：GET）。            |
| name           | 规定识别表单的名称（对于 DOM 使用：document.forms.name）。 |
| novalidate     | 规定浏览器不验证表单。                                     |
| target         |   规定 action 属性中地址的目标（默认：_self）。                               |

表单元素
基本概念：
HTML表单是HTML元素中较为复杂的部分，表单往往和脚本、动态页面、数据处理等功能相结合，因此它是制作动态网站很重要的内容。
表单一般用来收集用户的输入信息
表单工作原理：
访问者在浏览有表单的网页时，可填写必需的信息，然后按某个按钮提交。这些信息通过Internet传送到服务器上。 
服务器上专门的程序对这些数据进行处理，如果有错误会返回错误信息，并要求纠正错误。当数据完整无误后，服务器反馈一个输入完成的信息。
##### 2.9 Input
`<input>` 元素会根据不同的 type 属性，变化为多种形态。

| tpye属性值 | 表现形式     | 对应的代码 以及效果图                                  |
| ---------- | ------------ | -------------------------------------------- |
| text       | 单行输入文本 | `<input type="text" />`  <input type="text" />                           | 
| password   | 密码输入框   | `<input type="password"  />`  <input type="password"  />                  |
| date       | 日期输入框   | `<input type="date" />`  <input type="date" />                        |
| checkbox   | 复选框       | `<input type="checkbox" checked="checked"  />` <input type="checkbox" checked="checked"  /> |
| radio      | 单选框       | `<input type="radio"  />`      <input type="radio"  />                  |
| submit     | 提交按钮     | `<input type="submit" value="提交" />`  <input type="submit" value="提交" />        |
| reset      | 重置按钮     | `<input type="reset" value="重置"  />`    <input type="reset" value="重置"  />      |
| button     | 普通按钮     | `<input type="button" value="普通按钮"  />`  <input type="button" value="普通按钮"  />   |
| hidden     | 隐藏输入框   | `<input type="hidden"  />`         <input type="hidden"  />                 |
| file       | 文本选择框   | `<input type="file"  />`             <input type="file"  />               |
属性说明：

- name：表单提交时的“键”，注意和id的区别
- value：表单提交时对应项的值 
     - type="button", "reset", "submit"时，为按钮上显示的文本年内容
     -  type="text","password","hidden"时，为输入框的初始值
     - type="checkbox", "radio", "file"，为输入相关联的值
- checked：radio和checkbox默认被选中的项
- readonly：text和password设置只读
- disabled：所有input均适用

2.10 select标签

``` xml
<form action="" method="post">
  <select name="city" id="city">
    <option value="1">北京</option>
    <option selected="selected" value="2">上海</option>
    <option value="3">广州</option>
    <option value="4">深圳</option>
  </select>
</form>
```
属性说明：
- multiple：布尔属性，设置后为多选，否则默认单选
- disabled：禁用
- selected：默认选中该项
- value：定义提交时的选项值

2.11 label标签
定义：`<label>` 标签为 input 元素定义标注（标记）。
说明：
- label 元素不会向用户呈现任何特殊效果。
- `<label>` 标签的 for 属性值应当与相关元素的 id 属性值相同。

``` stata
<form action="">
  <label for="username">用户名</label>
  <input type="text" id="username" name="username">
</form>
```
2.12 textarea多行文本

``` xml
<textarea name="memo" id="memo" cols="30" rows="10">
  默认内容
</textarea>
```
属性说明：
- name：名称
- rows：行数
- cols：列数
- disabled：禁用

以上code的效果图如下：
![enter description here](./images/1547801915032.png)