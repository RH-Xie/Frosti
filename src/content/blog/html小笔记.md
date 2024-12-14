---
title: HTML笔记
pubDate: 2021-4-5 16:46:00
tags:
  - 前端
categories:
  - tech
description: 一些浅显的基础，看起来总像是在抄书
image: https://images.weserv.nl/?url=s2.loli.net/2023/08/22/IVkOajYhz2DC1y7.webp
---



# # 序言

每一点内容均有例子，尽量清晰地讲诉每一个常见符号的作用。如果你想查询某个符号，请看边栏，或者前往W3C、[tutorialspoint](https://www.tutorialspoint.com/html/index.htm)。文章附带了新手理解层面的一些见解，有所不周，还请见谅。

Hypertext Markup Language，简称HTML，是世界上最广泛用于编写网页的语言。

> Hypertext是一种网页连接方式（类似word中的超文本），网页上可以点击的连接其实就是Hypertext（超文本）
>
> Html是标记语言，也就是用带标记（Tag）的文字告诉网页如何架构其显示内容的一种语言~~（其实我更想叫它标签语言，但入乡随俗了）~~

应用：网页页面，网页导航，跨平台UI，离线阅读，游戏开发

与html密切相关：javascript,php,angular。在此栽下一棵树。



# 第一个网页

猜猜会是谁？当然是大家喜闻乐见的Hello World了！

```html
<!DOCTYPE html>
<html>
	<head>
		<title>Is this a descrption for document?</title>
	</head>
	<body>
		<h1>This is the first website by Makri_BW</h1>
		<p>Hello World!</p>
	</body>
</html>
```

如果你没有合适的HTML代码展示平台，可以点击[这里](http://tpcg.io/v5h38Z3B
)查看效果

下面一一解释上文所用Tag的作用

| 序号Sr.No | 标记Tag          | 描述Description                                              |
| --------- | ---------------- | ------------------------------------------------------------ |
| 1         | \<!DOCTYPE html> | Document Type 规定文本类型和HTML版本的标记，这里规定的文本类型即html |
| 2         | \<html>          | 包含完整的HTML文本，主要由文本头（暂不理是什么，用\<head>\</head>>表示）和文本体（即文本内容，用\<body>\</body>表示） |
| 3         | \<head>          | 可以存放\<title>\<link>等HTML标记                            |
| 4         | \<title>         | 如上提及，在\<head>内部.                                     |
| 5         | \<body>          | 存放\<h1>\<div>\<p>等标记                                    |
| 6         | \<h1>            | heading 1 一级标题，以此类推，\<h2>是二级标题。              |
| 7         | \<p>             | Paragraph，自然段                                            |

## <!DOCTYPE>声明标记

作用是供浏览器理解HTML版本

## 标题标记

\<h1>为一级标题，\<h2>为二级标题，依此类推到。一级标题最大，六级标题最小，超过六级会变成与大小相当的文字。至于有无标题作用，我们以后讨论。

## 自然段标记

\<p>\</p>所包含内容即为一个自然段。

### \<br />换行标记

\<br />即line break，可在\<p>\</p>中使用，以达到自己想要的目的。

### \<center>\</center>居中标记

\<center>\</center>，在\<p>\</p>之外中使用，例如：

```html
<!DOCTYPE html>
<html>
	<head>
		<title>This is name of the page</title>
	</head>
	<body>
	    <h2>Centring the content</h2>
		<center>
		    <h1>Title</h1>
		    <p>We Are the Center of Galaxy</p>
		</center>
	</body>
</html>
```

建议读者亲自敲一下以上代码，熟悉一下格式，也可以[点击此处查看效果](http://tpcg.io/Vi9qHr20)。

### \<hr />分割线

本身叫Horizontal Lines，缩写hr。在各大论坛中和贴主们形影不离的存在。视觉上既有强制分隔的作用，又有装饰作用。来看看[这个](http://tpcg.io/oL7KsUG5)例子，加深体会

```html
<!DOCTYPE html>
<html>
	<head>
		<title>This is name of the page</title>
	</head>
	<body>
	    <h2>Centring the content</h2>
		<center>
		    <h1>Title</h1>
		    <hr />
		    <p>We Are the Center of Galaxy</p>
		</center>
	</body>
</html>
```

读到这里，你应该早发现了**\<br />**换行标记和**\<hr />**分割线标记似乎是**同一类型**的。它们没有其他标签那样的开始、结束标签（譬如\<p>和\</p>)，格式为\<xx />，标签名和斜杠之间有空格。它们有一个共同的名字，叫做**置空元素**，俗称**空标签**。以后你还会遇到很多相当有趣的空标签。

### \<pre>\</pre>格式保护

全名Preserve Formatting。在HTML中打一段代码，经常要换行，老是\<br />来\<br />去，相信你会感到十分繁琐。所以\<pre>\</pre>之间的文字排版格式会被保留下来，就像txt一样，\<br />这样的标记，你不需要单独去打了，而且这样你的内容会非常直观，就像看源代码一样。

具体[例子](http://tpcg.io/76TScrhN)：

```html
<!DOCTYPE html>
<html>
	<head>
		<title>This is name of the page</title>
	</head>
	<body>
		<center>
		    <h1>Title</h1>
		    <hr /N
		    <p>We are going to show you some codes below</p>
		</center> 
		<p>
		    <pre>
def Func()
{
    print("你好")
}
            </pre>
	</body>
</html>
```

如果你尝试不使用\<pre>\</pre>，那么需要加4个\<br />。越是长的代码，越能体现\<pre>\</pre>格式保护的优势。

### **&nbsp**;不换行的空格

全称Nonbreaking space，强制不换行的空格，这一点针对带空格的书名、报名、人名等，英文中使用得比较多。

给出[例子](http://tpcg.io/OhhfWR)，调成Mobile&nbsp;320\*568之后，可见整个*12 Angry Men*都推到了下面，**以此防止重要内容断开**。

建议读者去掉代码中的\&nbsp;之后，再试一次，看看有何异同。

## 区分“标记”和“元素”

标记分为开始标记和结束标记，而元素是标记+包含的内容，

> 比如：
>
> \<p>是开始标记\</p>是结束标记，
>
> \<p>This is the content between the opening tag and closing tag\</p>则是一个元素



# 第二个网页

我们补充几个常用符号，通过上面的学习，相信下面内容读起来，你再熟悉不过了。

下划线：\<u>\</u>

斜体：\<i>\</i>

加粗：\<b>\</b>或\<strong>\</strong>

引用：

Ⅰ.\<blockquote>\</blockquote>，引用一大段话，与\<p>\</p>同级，作为一个自然段，会居中显示。

Ⅱ.\<q>\</q>，引用一小句话，位于\<p>\</p>等之内，作用不明显。

（还有个\<div>\</div>，因为跟CSS挂钩，所以在此先不作要求，等到CSS篇再细说）

## 属性

原名Attributes，用于修饰标记的内容，由“键值对”构成（打双引号使因为像，但并不完全是键值对），常常放在**开始标记**(Opening Tags)中，常见的由align（对齐）、title（光标提示，光标浮在标记内文字上面时，会显示提示，俗称tooltip，下面会详细演示）、style（css相关的风格设置，有颜色、对齐等等）、dir（文字方向，阿拉伯文是从右到左读的，dir因此而生）

### title

浏览网页的时候，相信你有见过将鼠标放在某些地方，那里就会冒出一些提示来，这就是属性title，下面看个[例子](http://tpcg.io/jF86OmIh
)立刻明白：

```html
<!DOCTYPE html>
<html>

   <head>
      <title>The title Attribute Example</title>
   </head>
	
   <body>
      <h3 title = "Hello HTML!&#x0a;这就是提示，也叫Tooltip">Float your cursor here</h3>
   </body>
	
</html>
```

这里放了个\&#x0a;是啥意思？其实是想让你先亲自去试试，那是个换行符。你会问为何不用\<br />？可以参考下面的解释，但实际上我对自己的搜索并不满意，我还是不清楚为何title属性中的字符串不能用\<br />——目前只是解释为不合语义；希望看到这里的各位爷指出问题关键，帮帮我这个菜鸡。

> https://stackoverflow.com/questions/26093623/br-not-working-in-title-tag-for-tooltip \<br />在title属性中不起作用
>
> https://stackoverflow.com/questions/1726073/is-it-sometimes-bad-to-use-br  什么时候不该用\<br />？

## 注释

格式：\<!-- 注释内容 -->

作为一个html编辑者，自然要在交流过程中对自己的代码写下一些注释。

请注意这个交流的对象**不仅仅是他人**，还有**未来的你**。

```html
<!DOCTYPE html>
<html>

   <head>  
      <title>Multiline Comments</title>
   </head> 
	  <!--This is the end of tag <head></head> -->
   <body>
      <!-- 
         This is a multiline comment and it can
         span through as many as lines you like.
      -->
      
      <p>Document content goes here.....</p>
   </body>
   <!--End of this html tag-->
   <!-- And you can see that spaces 
   are not required to both tags of comment-->
</html>
```

查看[效果](http://tpcg.io/GQEicU9X)

## 图片

格式： \<img src = "图片路径或网址，即图片直链" alt = "Test Image" />

这个很新鲜了吧？经过前面枯燥的学习，终于有点好康的东西了。

我们来一一解释：img src即image source，图片来源，一般后边的双引号里是图片路径，以.png、.jpeg结尾居多，有两种表示方式：

<details><summary>①绝对“路径”</summary>其实是互联网上的图片链接，比如：
    <blockquote>https://i.loli.net/2019/12/30/e9th3ZPN5CAOFoV.png</blockquote>
    <blockquote>https://inews.gtimg.com/newsapp_ls/0/13249243546/0</blockquote>
嘛，为什么说“一般”，第二个链接就可以看出来了，您尽可打开看一看，至少笔者在写时这俩图片的图床都没有爆炸。
</details>

<details><summary>②相对路径</summary>以"/"起头，以为以你现在的网页为零点，进入"/"后的路径进行图片的读取。<br /><br />这一点对一个大型网站来说十分有用，在节省代码量的同时减少了访问其他网站（如不属于本网站的图床网站）的机会，维护起来更稳定——万一哪天图床变了、炸了，或者是你的网址变了，使用绝对路径的你会发现，网页里的图全崩了。<br /><br/>具体到某一个网站，我们可以用github来举例。如果你的respiratory既做博客网站的存放点，同时也储存了图片，那么就可以使用相对路径，访问respiratory的图片。<br /><br />我的博客文件储存在：https://github.com/RH-Xie/RH-Xie.github.io/<br /><br />
那么我想展示一下我的头像：（可能要代理才能看到）<br />
<src img= "https://github.com/RH-Xie/RH-Xie.github.io/blob/master/images/20201108230401.jpg" alt = "MyIcon" />
</details>

alt为alternate text，替代文本。当**图片显示不出**的时候，浏览器就会在图片位置放上一个表示“图片”的小图标和alt后双引号内的文字，以示此处原应有图，因为访问超时而**获取不到图片**。如果你没有开github的代理，那么你有可能在上面的“相对路径”里就见到这个了

查看[效果](http://tpcg.io/9KkHGq)：

```html
<!DOCTYPE html>
<html>

   <head>
      <title>Using Image in Webpage</title>
   </head>
	
   <body>
      <p>Simple Image Insert</p>
      <img src = "/html/images/test.png" alt = "Test Image" />
   </body>
	
</html>
```

### 图片跳转

在论坛的的顶部，我们常常见到有该论坛的图标，点击它们，一般会返回到论坛的主页。而我们只要把上述的图片与超链接结合起来，就可以得到这样的功能。在各大下载站点的广告也常有应用。

这里依然以mcbbs为例：

```html
<!DOCTYPE html>
<html>
    <head>
        <title>An example of Image Link</title>
    </head>
    <body>
        <p>Click the picture below</p>
        <a href = "https://www.mcbbs.net" target = "_self">
            <img src = "https://www.mcbbs.net/template/MCBBS_v3/image/logo.png" alt = "The Icon of MCBBS(CN)" border = "4"/>
        </a>
    </body>
</html>
```

[查看效果](http://tpcg.io/iS7hQwU5)

这里的\<a>\</a>全名为anchor，原意为“锚”，可以引申为“导航”，是专门用于展示可点击链接的地方。关于它的属性不只有href，但href十分常用。href全名为html reference，即网页引用，后面跟一个url链接（网页的链接，Uniform Resource Locator，通俗来讲就是**网址**）。

alt标签，不是键盘上的ALT！其全名`alternative`，**可替代的文字**。当图片显示不出时，就会显示这些文字，不过链接依然能跳转（一般来说）。



还有几个常用的属性：download，指定下载文件的文件名；target，指定以什么方式打开新的网页，如\_self在本网页跳转只下个网页，\_parent、\_top、_blank则是打开新窗口以访问网页。具体区别建议谷歌，这里不作区分



## 视频

类似图片，多了一点属性。其实这个不需要专门去学，知道一下几个属性即可，因为在一般的视频网站“分享”下回直接有html源码让你复制到html文件中。

|     属性     |                         作用                         |
| :----------: | :--------------------------------------------------: |
|     src      | 视频源链接，一般只有播放器，没有评论、点赞之类的按键 |
|    width     |     视频宽度，可以填像素，也可以填占窗口的百分比     |
|    height    |                    视频高度，同理                    |
|     name     |              在javascript中用于引用元素              |
| marginheight |                       边缘高度                       |
| marginwidth  |                       边缘宽度                       |

演示代码：

```
<iframe src="//player.bilibili.com/player.html?aid=501616931&bvid=BV1rN411R7XQ&cid=294474330&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

由于B站视频现在是自动播放的，以防其发出不必要的巨响，请读者自行尝试将代码嵌入到编辑器中调试



# 第三个网页

以上，我们分别认识了HTML的文字处理和一些常用的部件，那么接下来应该整体规划一下我们的**网页布局**了。事实上现在设计者更倾向于使用CSS和Javascript来设计布局，而这里只是以HTML作引导，为上述两者铺基础，以便之后学习CSS和Javascript时不会吃力。

## 表格

表格，一种具有布局性质的零部件。

下面是一个简单的表格

```
<!DOCTYPE html>
    <html>
        <head>
        	<title>一个简单的表格</title>
        </head>
        <body>
            <table border = "1">
                <tr>
                    <th>商品名</th>
                    <th>价格</th>
                </tr>
                <tr>
                    <td>榨汁机</td>
                    <td>35</td>
                </tr>
                <tr>
                    <td>菜刀</td>
                    <td>50</td>
                </tr>
            </table>
	</html>
```

展示效果：

<!DOCTYPE html>
    <html>
        <head>
        	<title>一个简单的表格</title>
        </head>
        <body>
            <table border = "1">
                <tr>
                    <th>商品名</th>
                    <th>价格</th>
                </tr>
                <tr>
                    <td>榨汁机</td>
                    <td>35</td>
                </tr>
                <tr>
                    <td>菜刀</td>
                    <td>50</td>
                </tr>
            </table>
	</html>

你只需要记住

- tr = Table Row，即表格的一行；
- th = Table Heading（或Table Header，记住就行）会稍显粗一点；
- td = Table Data，表格数据。

认识到html中表格是**以行(Row)为单位**的即可，即一行一个\<tr>\</tr>，东西全在里面了。

如果你发现这个表格太胖了，那么给table来个属性`width`和`height`，让它限制一下大小：

```html
      <table width = "像素或者百分比" height = "像素或者百分比" border = "1">
```



<!DOCTYPE html>
    <html>
        <head>
        	<title>一个简单的表格</title>
        </head>
        <body>
            <table width = "200" height = "100" border = "1">
                <tr>
                    <th>商品名</th>
                    <th>价格</th>
                </tr>
                <tr>
                    <td>榨汁机</td>
                    <td>35</td>
                </tr>
                <tr>
                    <td>菜刀</td>
                    <td>50</td>
                </tr>
            </table>
	</html>



如果你问，我皮，我就不对齐，多了一列出来，怎么着？

```
<!DOCTYPE html>
    <html>
        <head>
        	<title>一个突出了一列的表格</title>
        </head>
        <body>
            <table border = "1">
                <tr>
                    <th>商品名</th>
                    <th>价格</th>
                </tr>
                <tr>
                    <td>榨汁机</td>
                    <td>35</td>
                </tr>
                <tr>
                    <td>菜刀</td>
                    <td>50</td>
                    <td>多出来一列
                </tr>
            </table>
	</html>
```

<!DOCTYPE html>
    <html>
        <head>
        	<title>一个简单的表格</title>
        </head>
        <body>
            <table border = "1">
                <tr>
                    <th>商品名</th>
                    <th>价格</th>
                </tr>
                <tr>
                    <td>榨汁机</td>
                    <td>35</td>
                </tr>
                <tr>
                    <td>菜刀</td>
                    <td>50</td>
                    <td>多出来一列
                </tr>
            </table>
	</html>

也没怎么样，多一列就多一列，不会报错。这样对注释是很友好的，或者我只是不想要什么标题，就这么干。

如果你想要更复杂的表格：

<!DOCTYPE html>
    <html>
        <head>
        	<title>一个简单的表格</title>
        </head>
        <body>
            <table border = "1">
                <tr>
                    <th>商品名</th>
                    <th>价格</th>
                    <th>类型</th>
                </tr>
                <tr>
                    <td>榨汁机</td>
                    <td>35</td>
                    <td rowspan = "2">厨具</td>
                </tr>
                <tr>
                    <td>菜刀</td>
                    <td>50</td>
                </tr>
                <tr>
                    <td colspan = '3'>总计：85</td>
                </tr>
            </table>
	</html>

这就像你的物理实验报告，你往往要串行串列、合并着写，而非每一个方格都是1x1。

实现功能的是\<td>\</td>的标签，合并行（即竖着合并）为`rowspan`，合并列为`colspan`，后面跟上数值。比如上面“厨具”、“总计：85”对应的就是：

```html
<td rowspan = "2">厨具\</td>
<td colspan = '3'>总计：85\</td>
```

（注意外面有\<tr>\</tr>包裹）

另外还有一个不太重要的东西\<caption>\</caption>，表格名。

比如在上面的代码里\<table>\</table>内加入

```html
<caption>价格表一览</caption>
```

表格会变为：

<!DOCTYPE html>
    <html>
        <head>
        	<title>一个简单的表格</title>
        </head>
        <body>
            <table border = "1">
                <caption>价格表一览</caption>
                <tr>
                    <th>商品名</th>
                    <th>价格</th>
                    <th>类型</th>
                </tr>
                <tr>
                    <td>榨汁机</td>
                    <td>35</td>
                    <td rowspan = "2">厨具</td>
                </tr>
                <tr>
                    <td>菜刀</td>
                    <td>50</td>
                </tr>
                <tr>
                    <td colspan = '3'>总计：85</td>
                </tr>
            </table>
	</html>
**未完待续**...


## 布局



事实上，本篇教程省去了很多的内容，比如\<meta>标签和多种强调标签（phrase tags）。原因是它们的作用在**局限于html的时候**作用不大，或者有替代品。有必要的话，以后在css|javascript有接触到它们时，我再回来补充；而在那之前，本篇教程不作讲解，读者可以前往[tutorialspoint](https://www.tutorialspoint.com/html/)查询详细信息。

最后说一点点菜鸡作者的感受：庆幸我们是生在互联网时代的人们，是长期接触过浏览器，受弹窗广告洗礼的人们，才切身体会到网页设计的有趣。许多tag在学习的时候，脑中不由得就有了熟悉的例子。

本文以后也许还会进行一次更新，有两点：一个是根据整体来调整各个标签所占的分量，增删内容，突出重点；二是文章结构的调整，让三个网页的例子更加清晰地站在三个部分的结尾。

