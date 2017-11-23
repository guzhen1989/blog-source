---
title: lean to code html & css 第一节
tags:
  - lean to code html & css
  - html
  - css
categories:
  - lean to code html & css
---

> 本节根据[shayhowe](https://shayhowe.com/)的《[Learn to Code HTML & CSS](https://learn.shayhowe.com/html-css/)》的Lesson 1 *[Building Your First Web Page](https://learn.shayhowe.com/html-css/building-your-first-web-page/)* 翻译

# 构建你的第一个web页面
&ensp;&ensp;&ensp;&ensp;如果可以的话，想象一下在互联网发明之前的一段时间。网站不存在，书面印刷和书写紧密的书籍是您的主要信息来源。这需要付出相当大的努力去试读和确认这是你需要的内容。

&ensp;&ensp;&ensp;&ensp;今天，您可以打开网页浏览器，跳转到您选择的搜索引擎，然后搜索。任何可以想象的信息都在你的指尖。而究其原因就是某人在某个地方建立了一个网站，其内容就是你确切需要的。

&ensp;&ensp;&ensp;&ensp;在本书中，我将向您展示如何使用两种最主要的计算机语言（HTML和CSS）来构建自己的网站。

&ensp;&ensp;&ensp;&ensp;在开始学习如何使用HTML和CSS构建网站之前，理解两种语言之间的区别，每种语言的语法以及一些常用术语是很重要的。

## 什么是html & css
&ensp;&ensp;&ensp;&ensp;HTML(HyperText Markup Language 超文本标记语言)是将内容定义为例如标题，段落或图像来给出内容结构和含义的标记语言。CSS（Cascading Style Sheets 层叠样式表）是一种使用例如字体或颜色来定义内容的展现方式的展现语言。

&ensp;&ensp;&ensp;&ensp;这两种语言（HTML和CSS）彼此独立，并且应该保持这种状态。 CSS不应该写在HTML文档中，反之亦然。通常，HTML将始终代表内容，CSS将始终代表该内容的外观。

&ensp;&ensp;&ensp;&ensp;通过这些对HTML和CSS的区别的理解，我们来深入一下HTML。

# HTML
## 了解常见的HTML术语
&ensp;&ensp;&ensp;&ensp;在开始使用HTML时，您可能会遇到新的（通常是陌生的）术语。随着时间的推移，你将会越来越熟悉它们，但是你应该首先使用的三个常见的HTML术语是元素，标签和属性。
### 元素（Elements）
&ensp;&ensp;&ensp;&ensp;元素是定义页面内对象的结构和内容的指示符。一些更常用的元素包括多层次的标题（标识为<code>&lt;h1&gt;</code>到<code>&lt;h6&gt;</code>元素）和段落（标识为<code>&lt;p&gt;</code>元素）;该列表包括<code>&lt;a&gt;</code>，<code>&lt;div&gt;</code>，<code>&lt;span&gt;</code>，<code>&lt;strong&gt;</code>和<code>&lt;em&gt;</code>元素等等。

&ensp;&ensp;&ensp;&ensp;元素通过使用围绕元素名称的小于和大于尖括号&lt;&gt;来标识。因此，元素将类似如下所示：
```html
<a>
```
### 标签（Tags）
&ensp;&ensp;&ensp;&ensp;围绕元素的小于和大于尖括号的使用创建了所谓的标签。标签通常以成对的开启和关闭标签出现。

&ensp;&ensp;&ensp;&ensp;<i>开始标记</i>标记元素的开始。它由一个小于号的后面跟一个元素的名字组成，然后以一个大于号结束;例如<code>&lt;div&gt;</code>。

&ensp;&ensp;&ensp;&ensp;<i>结束标记</i>标记元素的结束。它由一个小于号的后面跟一个正斜杠和元素的名字组成，然后以大于号结束;例如<code>&lt;/div&gt;</code>。

&ensp;&ensp;&ensp;&ensp;在开始和结束标签之间的内容是该元素的内容。例如，锚链接将具有开始标记<code>&lt;a&gt;</code>的开始标记和结束标记<code>&lt;/a&gt;</code>。两个标签之间的内容就是锚链接的内容。

&ensp;&ensp;&ensp;&ensp;所以，锚链接标签看起来有点像这样：
```html
<a>...</a>
```

### 属性（Attributes）
&ensp;&ensp;&ensp;&ensp;<i>属性</i>是用来提供关于元素的附加信息的。 最常见的属性包括标识元素的<code>id</code>属性; 分类元素的<code>class</code>属性; 指定可嵌入内容的来源的<code>src</code>属性和提供链接资源的<code>href</code>属性。

&ensp;&ensp;&ensp;&ensp;属性是在开始标签的元素名称后面定义的。一般来说，属性包括名称和值。这些属性的格式由属性名称，后跟等号和引用的属性值组成。例如，包含<code>href</code>属性的<code>&lt;a&gt;</code>元素看起来如下所示：
```html
<a href="http://shayhowe.com/">Shay Howe</a>
```
<iframe width="100%" height="100" src="//jsfiddle.net/1132053388/ze8L0779/embedded/html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
&ensp;&ensp;&ensp;&ensp;前面的代码将在网页上显示文字“Shay Howe”，并在用户点击“Shay Howe”文字时将用户带到http://shayhowe.com/。 锚元素使用开始标签<code>&lt;a&gt;</code>和闭合标签<code>&lt;/a&gt;</code>包裹文本，而超链接引用的属性和值在开始标签中用<code>href ="http://shayhowe.com"</code>声明。
![](html-syntax-outline.png)

&ensp;&ensp;&ensp;&ensp;现在您已经知道了HTML元素，标签和属性了，我们来组装我们的第一个网页吧。如果这里有什么新东西的话，不用担心，我们会在我们使用的时候解释它。

## 配置HTML文档结构
&ensp;&ensp;&ensp;&ensp;HTML文档是以<code>.html</code>文件扩展名而不是<code>.txt</code>文件扩展名保存的纯文本文档。 要开始编写HTML，您首先需要一个您习惯使用的纯文本编辑器。 但是，这不包括Microsoft Word或Pages，因为那些是富文本编辑器。 两种更流行的用于编写HTML和CSS的纯文本编辑器是Dreamweaver和Sublime Text。 免费的替代品还包括用于Windows的Notepad ++和用于Mac的TextWrangler。

&ensp;&ensp;&ensp;&ensp;所有HTML文档都必需具有必需以下的声明和元素：<code>&lt;!DOCTYPE html&gt;</code>，<code>&lt;html&gt;</code>，<code>&lt;head&gt;</code>和<code>&lt;body&gt;</code>。

&ensp;&ensp;&ensp;&ensp;文档类型声明或<code>&lt;!DOCTYPE html&gt;</code>通知Web浏览器正在使用哪个版本的HTML，并放置在HTML文档的开头。因为我们将使用最新版本的HTML，所以我们的文档类型声明就是<code>&lt;!DOCTYPE html&gt;</code>。在文档类型声明之后，<code>&lt;html&gt;</code>元素表示文档的开始。

&ensp;&ensp;&ensp;&ensp;在<code>&lt;!DOCTYPE html&gt;</code>元素中，<code>&lt;head&gt;</code>元素标识文档的顶部，里面包括任意元数据（关于页面的附带信息）。<code>&lt;head&gt;</code>元素内的内容不会显示在网页上。相反，它可能包含文档标题（显示在浏览器窗口中的标题栏上），或者指向任何外部文件的链接或任何其他有用的元数据。

&ensp;&ensp;&ensp;&ensp;网页中的所有可见内容都将落入<body>元素中。典型的HTML文档结构看起来像这样：
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Hello World</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <p>This is a web page.</p>
  </body>
</html>
```
<iframe width="100%" height="300" src="//jsfiddle.net/1132053388/ad1tu54L/embedded/html,css,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
&ensp;&ensp;&ensp;&ensp;上面的代码显示了以文档类型声明开始的文档<code>&lt;!DOCTYPE html&gt;</code>，紧接着是<code>&lt;html&gt;</code>元素。 在<code>&lt;html&gt;</code>元素里面有<code>&lt;head&gt;</code>和<code>&lt;body&gt;</code>元素。 <code>&lt;head&gt;</code>元素通过<code>&lt;meta charset =“utf-8”&gt;</code>标签申明页面的字符编码，并通过<code>&lt;title&gt;</code>元素申明文档的标题。 <code>&lt;body&gt;</code>元素通过<code>&lt;h1&gt;</code>元素和<code>&lt;p&gt;</code>元素包含一个标题和段落。 因为标题和段落嵌套在<code>&lt;body&gt;</code>元素中，所以它们在网页上是可见的。

&ensp;&ensp;&ensp;&ensp;当一个元素被放置在另一个元素的内部时，也被称为嵌套元素，缩进该元素以保持文档结构组织的清晰是一个好主意。 在前面的代码中，<code>&lt;head&gt;</code>和<code>&lt;body&gt;</code>元素嵌套在<code>&lt;html&gt;</code>元素中并缩进。 在<code>&lt;head&gt;</code>和<code>&lt;body&gt;</code>元素中添加新元素时，新嵌套元素也将缩进。

> <big>自闭元素</big>
&ensp;&ensp;&ensp;&ensp;在前面的例子中，<code>&lt;meta&gt;</code>元素只有一个标签，没有包含结束标签。 不要害怕，这是故意的。 并非所有元素都包含开始和结束标记。 一些元素只是从一个标签内的属性接收他们的内容或行为。 <code>&lt;meta&gt;</code>元素是这些元素之一。 上面的<code>&lt;meta&gt;</code>元素使用charset属性和值进行控制。 其他常见的自闭元素包括:
- <code>&lt;br&gt;</code>
- <code>&lt;embed&gt;</code>
- <code>&lt;hr&gt;</code>
- <code>&lt;img&gt;</code>
- <code>&lt;input&gt;</code>
- <code>&lt;link&gt;</code>
- <code>&lt;meta&gt;</code>
- <code>&lt;param&gt;</code>
- <code>&lt;source&gt;</code>
- <code>&lt;wbr&gt;</code>

&ensp;&ensp;&ensp;&ensp;这里使用的<code>&lt;!DOCTYPE html&gt;</code>文档类型和<code>&lt;html&gt;</code>，<code>&lt;head&gt;</code>和<code>&lt;body&gt;</code>元素的结构相当常见。我们将保存这个文档结构，因为我们会在创建新的HTML文档时经常使用它。

><big>代码检查</big>
&ensp;&ensp;&ensp;&ensp;无论我们在写代码的时候多么小心，我们都会不可避免地犯错误。 谢天谢地，在编写HTML和CSS时，我们有校验器来检查我们的工作。 W3C已经构建了扫描HTML和CSS代码中错误的校验器。 校验我们的代码不仅可以使代码在所有浏览器中正确呈现，还可以教会我们编写代码的最佳实践。

## 练习
&ensp;&ensp;&ensp;&ensp;作为网页设计师和前端开发人员，我们有幸参加了一些专门针对我们的工作的大型会议。我们将组织自己的会议（Styles Conference），并在下面的课程中为它建立一个网站。开始了！

1. 让我们打开我们的文本编辑器，创建一个名为index.html的新文件，并将其保存到一个我们不会忘记的位置。我将在我的桌面上创建一个名为“styles-conference”的文件夹，并将其保存在此处;大家可以一样处理。
2. 在index.html文件中，我们来添加文档结构，包括<code>&lt;!DOCTYPE html&gt;</code>文档类型和<code>&lt;html&gt;</code>，<code>&lt;head&gt;</code>和<code>&lt;body&gt;</code>元素。
```html
<!DOCTYPE html>
<html lang="en">
  <head>
  </head>
  <body>
  </body>
</html>
```
3. 在<code>&lt;head&gt;</code>元素中，添加<code>&lt;meta&gt;</code>和<code>&lt;title&gt;</code>元素。 <code>&lt;meta&gt;</code>元素应该包含正确的charset(编码)属性和值，而<code>&lt;title&gt;</code>元素应该包含页面的标题——“Styles Conference”。
```html
<head>
  <meta charset="utf-8">
  <title>Styles Conference</title>
</head>
```
4. 在<code>&lt;body&gt;</code>元素中，添加<code>&lt;h1&gt;</code>和<code>&lt;p&gt;</code>元素。 <code>&lt;h1&gt;</code>元素应包含我们希望包含的标题——让我们再次使用“Styles Conference”，而<code>&lt;p&gt;</code>元素应包含一个简单的段落来介绍我们的会议。
```html
<body>
  <h1>Styles Conference</h1>
  <p>Every year the brightest web designers and front-end developers descend on Chicago to discuss the latest technologies. Join us this August!</p>
</body>
```
5. 现在是时候看看我们已经完成了的页面！让我们去找到我们的index.html文件（我的在桌面上的“styles-conference”文件夹中）。双击此文件或将其拖入Web浏览器来打开查看。
![](lesson_1.png)

&ensp;&ensp;&ensp;&ensp;让我们切换一下，不管HTML，先看看CSS。请记住，HTML将定义我们网页的内容和结构，而CSS将定义我们网页的视觉风格和外观。
# CSS
## 了解常见的CSS术语
&ensp;&ensp;&ensp;&ensp;除HTML术语外，还有一些常用的CSS[术语](http://www.impressivewebs.com/css-terms-definitions/)，您可能需要自己熟悉这些术语。这些术语包括选择器，属性和值。与HTML术语一样，使用CSS越多，你将会越来越熟悉它们。

### 选择器（Selectors）
&ensp;&ensp;&ensp;&ensp;当元素被添加到网页中时，可以使用CSS对其进行样式化。选择器指定我们的HTML中的哪个或哪些元素来应用样式（如颜色，大小和位置）。选择器可以包含不同限定符的组合，取决于我们的目的来选择独特的元素。例如，我们可能希望选择页面上的每个段落，或者我们可能只想在页面上选择一个特定的段落。

&ensp;&ensp;&ensp;&ensp;选择器通常以属性值为目标，如<code>id</code>或<code>class</code>值，或者定位元素的类型，如<code>&lt;h1&gt;</code>或<code>&lt;p&gt;</code>。

&ensp;&ensp;&ensp;&ensp;在CSS中，选择器后面跟随大括号{}，其中包含要应用于所选元素的样式。下面的选择器是针对所有的<code>&lt;p&gt;</code>元素。
```css
p {...}
```

### 属性（Properties）
&ensp;&ensp;&ensp;&ensp;一旦选择了一个元素，属性决定了将应用于该元素的样式。属性名称落在选择器之后的大括号{}内，且在冒号:之前。我们可以使用许多属性，例如<code>background</code>,<code>color</code>,<code>font-size</code>,<code>height</code>和<code>width</code>。在下面的代码中，我们定义了要应用于所有<code>&lt;p&gt;</code>元素的颜色和字体大小属性。
```css
p {
  color: ...;
  font-size: ...;
}
```

### 值（Values）
&ensp;&ensp;&ensp;&ensp;到目前为止，我们已经使用选择器选择了一个元素，并确定了我们想要使用样式的属性。现在我们可以用一个值来确定这个属性的行为。值可以被识别为冒号:和分号;之间的文本。在这里，我们选择所有的<code>&lt;p&gt;</code>元素，并将<code>color</code>属性的值设置为<code>orange</code>，并将font-size属性的值设置为<code>16</code>像素。
```css
p {
  color: orange;
  font-size: 16px;
}
```

&ensp;&ensp;&ensp;&ensp;在CSS中，规则集是以选择器开始的，紧接着是花括号。在这些大括号内是由属性和值对组成的。每个属性值对都从一个属性开始，后面是一个冒号和属性值，最后是一个分号。

&ensp;&ensp;&ensp;&ensp;在大括号内缩进属性和值对是一种常见的做法。与HTML一样，这些缩进有助于我们的代码的组织保持清晰。
![](css-syntax-outline.png)

&ensp;&ensp;&ensp;&ensp;了解一些常用术语和CSS的一般语法是一个很好的开始，但是在深入了解之前我们还有其他一些东西需要学习。具体来说，我们需要仔细看看选择器在CSS中如何工作的。

## 使用选择器
### 类型选择器（Type Selectors）
&ensp;&ensp;&ensp;&ensp;类型选择器按元素类型定位元素。例如，如果我们想要定位所有的<code>&lt;div&gt;</code>元素，我们将使用div的类型选择器。以下代码显示了<code>div</code>元素的类型选择器以及它选择的相应HTML。
```css
div { ... }
```
```html
<div>...</div>          
<div>...</div>
```

### 类选择器（Class Selectors）
&ensp;&ensp;&ensp;&ensp;类选择器允许我们根据元素的类属性值选择一个元素。类选择器比类型选择器更具体一些，因为它们选择一组特定的元素而不是一种类型的所有元素。

&ensp;&ensp;&ensp;&ensp;类选择器允许我们通过在多个元素中使用相同的类属性值，将同样的样式同时应用于不同的元素。

&ensp;&ensp;&ensp;&ensp;在CSS中，类用前导点<code>.</code>表示，后跟类属性值。在这里，类选择器将选择包含awesome类属性值的任何元素，包括<code>div</code>元素和<code>p</code>元素。
```css
.awesome { ... }
```
```html
<div class="awesome">...</div>
<p class="awesome">...</p>
```

### ID选择器（ID Selectors）
&ensp;&ensp;&ensp;&ensp;

