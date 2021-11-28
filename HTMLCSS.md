---
title: HTMLCSS
date: 2021-10-10 9:48:05
tags: HTMLCSS
categories: 面试
cover: https://z3.ax1x.com/2021/10/27/5T7MS1.jpg
---

# **HTML5**

## HTML5语义化标签

![img](https://upload-images.jianshu.io/upload_images/15827882-4057d561069e7a15.png?imageMogr2/auto-orient/strip|imageView2/2/w/484/format/webp)

### 优点

- 在没有CSS的情况下，更好的呈现出内容的结构
- 比`<div>`标签有更加丰富的意义，利于开发和维护
- 方便搜索引擎识别页面结构，有利于搜索引擎优化（SEO）
- 方便其他设备解析（移动设备、盲人阅读器等）

### header

- 放在页面或布局的顶部，一般放置导航栏或标题。
- 一个文档中可以包含一对或者一对以上的<header>标签。
- 标签的位置是次要的，不一定非要显示在页面的上方，我们可以为任何需要的区块标签添加<header>元素

### hgroup

- 如果有连续多个h1-h6标签就用hgroup
- 如果有连续多个标题和其他文章数据，h1-h6标签就用hgroup包住，和其他文章元数据一起放入header标签

### nav

- 表示页面的导航，也可以在<header>标签中使用，还可以显示在侧边栏中
- 为了方便搜索引擎解析，最好是将主要的链接放在nav中

### aside

- 所包含的内容不是页面的主要内容、具有独立性，是对页面的补充
- 一般使用在页面、文章的侧边栏、广告、友情链接等区域

### footer

一般被放置在页面或者页面中某个区块的底部，包含版权信息、联系方式等信息。一个页面也可以有多个footer

### article

使用在相对比较独立、完整的的内容区块，所以我们可以在一篇博客、一个论坛帖子、一篇新闻报道或者一个用户评论中

### section

一组或者一节内容。

**如果我们的页面中需要一个单独的模块来实现一个单独的功能，就用<article>，其他的时候都用<section>**

### address

address代表区块容器，必须是作为联系信息出现，邮编地址、邮件地址等等,一般出现在footer

## 增强型表单

html5修改一些新的input输入特性，改善更好的输入控制和验证

| 输入类型       | 描述                     |
| -------------- | ------------------------ |
| color          | 主要用于选取颜色         |
| date           | 选取日期                 |
| datetime       | 选取日期(UTC时间)        |
| datetime-local | 选取日期（无时区）       |
| month          | 选择一个月份             |
| week           | 选择周和年               |
| time           | 选择一个时间             |
| email          | 包含e-mail地址的输入域   |
| number         | 数值的输入域             |
| url            | url地址的输入域          |
| tel            | 定义输入电话号码和字段   |
| search         | 用于搜索域               |
| range          | 一个范围内数字值的输入域 |

 

html5新增了五个表单元素

| <datalist> | 用户会在他们输入数据时看到域定义选项的下拉列表 |
| ---------- | ---------------------------------------------- |
| <progress> | 进度条，展示连接/下载进度                      |
| <meter>    | 刻度值，用于某些计量，例如温度、重量等         |
| <keygen>   | 提供一种验证用户的可靠方法生成一个公钥和私钥   |
| <output>   | 用于不同类型的输出比如尖酸或脚本输出           |

html5新增表单属性

| 属性         | 描述                                  |
| ------------ | ------------------------------------- |
| placehoder   | 输入框默认提示文字                    |
| required     | 要求输入的内容是否可为空              |
| pattern      | 描述一个正则表达式验证输入的值        |
| min/max      | 设置元素最小/最大值                   |
| step         | 为输入域规定合法的数字间隔            |
| height/wdith | 用于image类型<input>标签图像高度/宽度 |
| autofocus    | 规定在页面加载时，域自动获得焦点      |
| multiple     | 规定<input>元素中可选择多个值         |

## 音频和视频

音频：<audio src=" "></audio>

```html
<audio controls>    //controls属性提供添加播放、暂停和音量控件。
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
您的浏览器不支持 audio 元素。        //浏览器不支持时显示文字
</audio>
```

视频：<video src=" "></video>

```html
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
您的浏览器不支持Video标签。
</video>
```

## Canvas绘图

## SVG绘图

## 地理定位

使用getCurrentPosition()方法来获取用户的位置。以实现“LBS服务”

```js
var x=document.getElementById("demo");
function getLocation()
  {
  if (navigator.geolocation)
    {
    navigator.geolocation.getCurrentPosition(showPosition);
    }
  else{x.innerHTML="Geolocation is not supported by this browser.";}
  }
function showPosition(position)
  {
  x.innerHTML="Latitude: " + position.coords.latitude +
  "<br />Longitude: " + position.coords.longitude;
  }
```

## 拖放API

拖放是一种常见的特性，即捉取对象以后拖到另一个位置。

在html5中，拖放是标准的一部分，任何元素都能够拖放。

```html
<div draggable="true"></div>
```

当元素拖动时，我们可以检查其拖动的数据。

```html
<div draggable="true" ondragstart="drag(event)"></div>
<script>
function drap(ev){
    console.log(ev);
}
</script>
```

| 拖动生命周期 | 属性名      | 描述                                           |
| ------------ | ----------- | ---------------------------------------------- |
| 拖动开始     | ondragstart | 在拖动操作开始时执行脚本                       |
| 拖动过程中   | ondrag      | 只要脚本在被拖动就运行脚本                     |
| 拖动过程中   | ondragenter | 当元素被拖动到一个合法的防止目标时，执行脚本   |
| 拖动过程中   | ondragover  | 只要元素正在合法的防止目标上拖动时，就执行脚本 |
| 拖动过程中   | ondragleave | 当元素离开合法的防止目标时                     |
| 拖动结束     | ondrop      | 将被拖动元素放在目标元素内时运行脚本           |
| 拖动结束     | ondragend   | 在拖动操作结束时运行脚本                       |

## Web Worker

Web Worker可以通过加载一个脚本文件，进而创建一个独立工作的线程，在主线程之外运行。

 基本使用：

   Web Worker的基本原理就是在当前javascript的主线程中，使用Worker类加载一个javascript文件来开辟一个新的线程，

起到互不阻塞执行的效果，并且提供主线程和新县城之间数据交换的接口：postMessage、onmessage。

```js
//worker.js
onmessage =function (evt){
  var d = evt.data;//通过evt.data获得发送来的数据
  postMessage( d );//将获取到的数据发送会主线程
}
```

```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<script type="text/javascript">
//WEB页主线程
var worker =new Worker("worker.js"); //创建一个Worker对象并向它传递将在新线程中执行的脚本的URL
worker.postMessage("hello world");     //向worker发送数据
worker.onmessage =function(evt){     //接收worker传过来的数据函数
   console.log(evt.data);              //输出worker发送来的数据
}
</script>
</head>
<body></body>
</html>
```

## Web Storage

客户端存储数据有两个对象，其用法基本是一致。

localStorage：没有时间限制的数据存储

sessionStorage:在浏览器关闭的时候就会清除。

```js
localStorage.setItem(key,value);//保存数据
let value = localStorage.getItem(key);//读取数据
localStorage.removeItem(key);//删除单个数据
localStorage.clear();//删除所有数据
let key = localStorage.key(index);//得到某个索引的值
```

## WebSocket

WebSocket是HTML5中的协议，支持持久连接，http协议不支持持久性连接，HTTP1.1中的keep-alive，将多个http请求合并为1个

HTTP生命周期通过Request来界定，再HTTP1.0中，Request一个Response就结束了

在HTTP1.1中，有一个connection: Keep-alive，也就是说，在一个HTTP连接中，可以发送多个Request，接收多个Response。

基本请求如下：

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
Origin: http://example.com
```

多了下面2个属性：

```
Upgrade:webSocket``Connection:Upgrade
```

告诉服务器发送的是websocket

```
Sec-WebSocket-Key: x``3``JJHMbDL``1``EzLkh``9``GBhXDw==``Sec-WebSocket-Protocol: chat, superchat``Sec-WebSocket-Version: ``13
```

# CSS3

## CSS优先级

!important>style>id>class

## CSS3新增

CSS3新增属性用法整理：

1、box-shadow（阴影效果）

2、border-color（为边框设置多种颜色）

3、border-image（图片边框）

4、text-shadow（文本阴影）

5、text-overflow（文本截断）

| 值       | 描述                                 |
| :------- | :----------------------------------- |
| clip     | 修剪文本。                           |
| ellipsis | 显示省略符号来代表被修剪的文本。     |
| *string* | 使用给定的字符串来代表被修剪的文本。 |

6、word-wrap（自动换行）

7、border-radius（圆角边框）

8、opacity（透明度）

9、box-sizing（控制盒模型的组成模式）

10、resize（元素缩放）

11、outline（外边框）

12、background-size（指定背景图片尺寸）

13、background-origin（指定背景图片从哪里开始显示）

14、background-clip（指定背景图片从什么位置开始裁剪）

15、background（为一个元素指定多个背景）

16、hsl（通过色调、饱和度、亮度来指定颜色颜色值）

17、hsla（在hsl的基础上增加透明度设置）

18、rgba（基于rgb设置颜色，a设置透明度）

## 锚伪类

使用顺序：

a:link -> a:visited -> a:hover -> a:active

光标：

未访问 -> 已访问 -> 移动到链接上 -> 点击选中链接

## CSS3新增伪类有哪些?

- p:first-of-type 选择属于其父元素的首个元素
- p:last-of-type 选择属于其父元素的最后元素
- p:only-of-type 选择属于其父元素唯一的元素
- p:only-child 选择属于其父元素的唯一子元素
- p:nth-child(2) 选择属于其父元素的第二个子元素
- :enabled :disabled 表单控件的禁用状态。
- :checked 单选框或复选框被选中。

# em和rem

**em**是相对父元素的单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。

任意浏览器的默认字体高都是16px，则满足1em=16px，则10px=0.625em。为了简化运算，在css的body选择器中设置`font-size: 62.5%`，这样1em=10px。

**rem**是css3新增的一个相对根元素的单位

rem与em的区别在于，使用rem为元素设定字体大小时，仍然是相对大小，但相对的是HTML根元素。

# viewport

**通过动态设置`meta`标签的`viewport`让`css`中的`1px`等于设备的`1px`。**

在 PC 端，视口指的是浏览器的可视区域，其宽度和浏览器窗口的宽度保持一致

- viewport 标签只对移动端浏览器有效，对 PC 端浏览器是无效的

而移动端则较为复杂，它涉及到三个视口：

- 布局视口（Layout Viewport）

  布局视口的宽度限制css布局的宽，为了能在移动设备上正常显示那些为pc端浏览器设计的网站，移动设备上的浏览器都会把自己默认的viewport设为980px或其他值，**一般都比移动端浏览器可视区域大很多，所以就会出现浏览器出现横向滚动条的情况**

- 视觉视口（Visual Viewport）

  **在移动端缩放不会改变布局视口的宽度**，当缩小的时候，屏幕覆盖的css像素变多，视觉视口变大，当放大的时候，屏幕覆盖的css像素变少，视觉视口变小。

- 理想视口（Ideal Viewport）

  在用户不进行手动缩放的情况下，可以将页面理想地展示。那么所谓的理想宽度就是浏览器（屏幕）的宽度了。

设置理想视口就在header中加入这样一行代码：

```html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

| 属性名        | 取值                  | 描述                                                |
| ------------- | --------------------- | --------------------------------------------------- |
| width         | 正整数或device-width  | 定义视口的宽度，单位为像素                          |
| height        | 正整数或device-height | 定义视口的高度，单位为像素，一般不用                |
| initial-scale | [0.0-10.0]            | 定义初始缩放值                                      |
| minimum-scale | [0.0-10.0]            | 定义放大最大比例，它必须小于或等于maximum-scale设置 |
| maximum-scale | [0.0-10.0]            | 定义缩小最小比例，它必须大于或等于minimum-scale设置 |
| user-scalable | yes / no              | 定义是否允许用户手动缩放页面，默认值 yes            |

# 移动端适配

## 媒体查询

**Media Queries**，它主要是通过查询设备的宽度来执行不同的 `css` 代码，最终达到界面的配置。

```css
@media screen and (max-width: 600px) { /*当屏幕尺寸小于600px时，应用下面的CSS样式*/
  /*你的css代码*/
}
```

优点

- media query可以做到设备像素比的判断，方法简单，成本低，特别是对移动和PC维护同一套代码的时候。
- 图片便于修改，只需修改css文件
- 调整屏幕宽度的时候不用刷新页面即可响应式展示

缺点

- 代码量比较大，维护不方便
- 为了兼顾大屏幕或高清设备，会造成其他设备资源浪费，特别是加载图片资源
- 为了兼顾移动端和PC端各自响应式的展示效果，难免会损失各自特有的交互方式

## rem实现

设计稿是640px，有一个红色的盒子宽高都是320px，里面的文字是32px，代码如下：

页面元素使用rem单位时，是相对于这个html标签的font-size的大小为基础的

**字体大小：内容的宽度 / 设计稿的宽度 × 100 px**

乘100是因为：一般浏览器的最小字体是12px，如果html的font-size=（320/640）px，相当于font-size=0.5px，那么这个数值就小于12px，会造成一些计算的错误

*100后，font-size是50px，就可以解决这种字体小于12px的问题，然后在设置元素宽高数值的时候除以100就可以了，则红色盒子设为3.2rem

```html
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1">
  <script type="text/javascript">
    var clientWidth = document.documentElement.clientWidth
    document.documentElement.style.fontSize = clientWidth / 640 * 100 + 'px';
    console.log(clientWidth);
  </script>
</head>
<body style="margin: 0 ;padding: 0;font-size: 0.32rem">
  <div style="width: 3.2rem;height: 3.2rem ;background: red">
    <span>danny.xie</span>
  </div>
</body>
```

## 小程序的rpx布局

小程序有个`rpx`可以根据屏幕自适应。官方文档的介绍：**可以根据屏幕宽度进行自适应。规定屏幕宽为750rpx。**

**如在 iPhone6 上，屏幕宽度为375px，共有750个物理像素，**

**则`750rpx = 375px = 750`物理像素，`1rpx = 0.5px = 1物理像素`**

也就是说，它内部的实现原理其实和基于设计图的rem布局的原理差不多。

只不过小程序内部处理了一下，**让rpx直接能够根据屏幕宽度自适应**，而不是像rem那样依赖于根元素的font-size.

## vw和vh

视口单位主要包括以下4个：

-    vw：1vw等于视口宽度的1%
-    vh：1vh等于视口高度的1%
-    vmin：选取vw和vh中最小的那个
-    vmax：选取vw和vh中最大的那个

比如：浏览器高度950px，宽度为1920px,

1 vh = 950px/100 = 9.5 px，1vw = 1920px/100 =19.2 px。

1 px = 100vh / 950                1px = 100vw / 1920 

# **各属性的百分比设定**

- 子元素width、height的百分比：子元素的width或height中使用百分比，是相对于子元素的直接父元素
- margin和padding的百分比：在垂直方向和水平方向都是相对于直接父亲元素的width，而与父元素的height无关
- border-radius的百分比：border-radius的百分比是相对于自身宽度，与父元素无关

# 宽度距离属性

- clientLeft,clientTop
  表示内容区域的左上角相对于整个元素左上角的位置（包括边框）。(取决于边框的像数值？)
- clientWidth,clientHeight
  内容区域的宽高，不包括边框宽度值。
- clientX、clientY
  点击位置距离当前body可视区域的x，y坐标
- offsetLeft,offsetTop
  相对于最近的祖先定位元素。
- offsetParent
  某元素的父元素 例如：this.offsetParent.tagName.toLowerCase() 得到body...
- offsetWidth,offsetHeight 
  整个元素的尺寸(不包括因为滚动条变宽的宽度，包括滚动条的宽度和高度)
- offsetX, offsetY
  相对于带有定位的父盒子的x，y坐标
- scrollLeft,scrollTop
  元素滚动的距离大小
- scrollWidth,scrollHeight
  整个内容区域的宽度(包括需拉动滚动条隐藏起来的那些部分) scrollWidth = scrollTop+clientWidth
- pageX、pageY
  对于整个页面来说，包括了被卷去的body部分的长度
- screenX、screenY
  点击位置距离当前电脑屏幕的x，y坐标
- x、y
  和screenX、screenY一样

# 盒子模型

box-sizing属性：用来控制元素的盒子模型的解析模式，默认为content-box

## 标准盒子模型

box-sizing: content-box

宽度=内容的宽度（content）+ border + padding + margin

元素的height/width = content部分的高/宽

## IE盒子模型

box-sizing: border-box

宽度=内容的宽度（content + border + padding）+ margin

元素的height/width = content + border + padding部分的高/宽

# Position

* `static`（默认）：按照正常文档流进行排列；

* `relative`（相对定位）：不脱离文档流，参考自身静态位置通过 top, bottom, left, right 定位；

  移动相对定位元素，但它原本所占的空间不会改变。经常被用来作为绝对定位元素的容器块。

* `absolute`（绝对定位）：参考距其最近一个不为static的父级元素通过top, bottom, left, right 定位。脱离文档流，因此不占据空间。 

* `fixed`（固定定位）：所固定的参照对象是可视窗口。脱离文档流， 因此不占据空间。

* `sticky`（粘性定位）：粘性定位的元素是依赖于用户的滚动

  它的行为就像 position:relative; 而当页面滚动超出目标区域时，它的表现就像 position:fixed;，它会固定在目标位置。

  指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。

元素脱离文档流，所以它们可以覆盖页面上的其它元素，**z-index**属性指定了一个元素的堆叠顺序

# Display

* `inline`（默认）：内联
* `none`：隐藏
* `block`：块显示
* `table`：表格显示
* `list-item`：项目列表
* `inline-block`：内联块，表现为同行显示并可修改宽高内外边距等属性

## 块级元素

` div , dl , form , h1 , h2 , h3 , h4 , h5 , h6 , ol , p , table , ul , li`

## 内联元素

`br , font , i , img , input , label , select , span , textarea , u`

## 隐藏元素

`display: none`：可以隐藏某个元素，且隐藏的元素不会占用任何空间。也就是说，该元素不但被隐藏了，而且该元素原本占用的空间也会从页面布局中消失。

`visibility: hidden`：可以隐藏某个元素，但隐藏的元素仍需占用与未隐藏之前一样的空间。也就是说，该元素虽然被隐藏了，但仍然会影响布局。

# BFC

BFC(Block formatting context)直译为"块级格式化上下文"。它是**一个独立的渲染区域**， 它决定了其子元素将如何定位，并且与这个区域外部毫不相干。

内部的Box会在垂直方向，一个接一个地放置。

Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠。

## 可以包含浮动的元素（清除浮动）

```html
<div style="border: 1px solid #000;">
    <div style="width: 100px;height: 100px;background: #eee;float: left;"></div>
</div>
```

![img](https://pic4.zhimg.com/80/v2-371eb702274af831df909b2c55d6a14b_720w.png)

由于容器内元素浮动，脱离了文档流，所以容器只剩下 2px 的边距高度。如果使触发容器的 BFC，那么容器将会包裹着浮动元素。

```html
<div style="border: 1px solid #000;overflow: hidden">
    <div style="width: 100px;height: 100px;background: #eee;float: left;"></div>
</div>
```

效果如图：

![img](https://pic4.zhimg.com/80/v2-cc8365db5c9cc5ca003ce9afe88592e7_720w.png)

## BFC 可以阻止元素被浮动元素覆盖

```html
<div style="height: 100px;width: 100px;float: left;background: lightblue">我是一个左浮动的元素</div>
<div style="width: 200px; height: 200px;background: #eee">我是一个没有设置浮动, 
也没有触发 BFC 元素, width: 200px; height:200px; background: #eee;</div>
```

![img](https://pic4.zhimg.com/80/v2-dd3e636d73682140bf4a781bcd6f576b_720w.png)

这时候其实第二个元素有部分被浮动元素所覆盖，(但是文本信息不会被浮动元素所覆盖) 如果想避免元素被覆盖，可触第二个元素的 BFC 特性，在第二个元素中加入 **overflow: hidden**，就会变成：

![img](https://pic3.zhimg.com/80/v2-5ebd48f09fac875f0bd25823c76ba7fa_720w.png)



## 触发 BFC 特性条件

- body 根元素
- 浮动元素：float 除 none 以外的值
- 绝对定位元素：position (absolute、fixed)
- display 为 inline-block、table-cells、flex
- overflow 除了 visible 以外的值 (hidden、auto、scroll)

# CSS选择器

## CSS选择符

* id选择器：`#myid`
* 类选择器：`.myclassname`
* 标签选择器：`div, h1~h6, p ……`
* 相邻选择器：`h1 + p`
* 子选择器：`ul > li`
* 后代选择器：`li a`
* 通配符选择器：`*`
* 属性选择器：`a[属性名]`
* 伪类选择器：`a:hover, li:nth-child`

## 优先级

元素选择符：1
class选择符：10
id选择符：100
元素标签：1000
!important声明的样式优先级最高，如果冲突再进行计算。
如果优先级相同，则选择最后出现的样式。继承得到的样式的优先级最低。

## 选择器解析

虽然我们平常写css选择器是从左到右书写的，但是，这只不过是为了方便使用者书写

真正的解析顺序时反过来的，也就是从子节点搜索到根节点，大大减少查找次数提高效率。

由于css tree是树结构，如果从根节点开始，如果到最后一个子节点仍然找不到的话，就是回到之前的父节点，继续查找其他的子节点

[![IffdOO.png](https://z3.ax1x.com/2021/11/16/IffdOO.png)](https://imgtu.com/i/IffdOO)

从子节点开始解析，**先判断孙节点是否匹配，只有匹配才会继续深入**，否则直接跳过，然后这就从多个多条线（深度优先遍历）变成了多个单条线的问题

[![IffR6f.png](https://z3.ax1x.com/2021/11/16/IffR6f.png)](https://imgtu.com/i/IffR6f)

## 可继承的属性

* 字体系列：`font-family，font-size，font-style，font-weight，font-stretch，font-size-adjust；`
* 列表相关：`list-style，list-style-image，list-style-position，list-style-type，list-style-color；`
* 文本系列：`text-indent，text-align，line-height，word-spaceing，letter-spacing，text-transform，direction，color；`
* 元素可见性：`visibility；`
* 表格布局：`caption-side，border-collapse，border-spacing，empty-cells，table-layout；`
* 光标属性：`cursor；`

## 不可继承的属性

`width、height、margin 、border、padding、display、text-decoration、vertical-align、background、float、clear、overflow、z-index、position、top、right、bottom、left、size、content、outline`等



# 清除浮动

## 什么时候需要清除浮动

如果一个块级元素没有设置height，其高度就由子元素撑开，如果子元素使用了浮动，脱离了标准的文档流，那么父元素的高度将不能被其撑开。表现出**高度塌陷**的现象。

## 清除浮动的方式

* 父级元素定义height

* 父级结尾处添加一个空`div`，设置css样式`clear: both`

  原理：添加一个空div， 利用css提高的`clear: both`清除浮动，让父级 div 能自动获取到高度

* 父级定义伪元素`:after`。原理：元素生成伪元素的作用和效果相当于方法2中的原理，使用伪元素生成一个看不见的块级元素，并且设置`clear:both`

* 父级div添加css属性：`overflow:hidden`

# 回流

**重绘：**当渲染树中的一些元素需要更新属性，而这些属性只是影响元素的外观、风格，而不会影响布局的操作，比如 background-color，我们将这样的操作称为重绘。

**回流：**当渲染树中的一部分（或全部）因为元素的规模尺寸、布局、隐藏等改变而需要重新构建的操作，会影响到布局的操作，这样的操作我们称为回流。

回流必定会发生重绘，重绘不一定会引发回流。回流所需的成本比重绘高的多，改变父节点里的子节点很可能会导致父节点的一系列回流。

## 哪些因素会导致回流？

1、调整窗口的大小；

2、改变字体，如果用rem 设置了根目录的字体大小，这样就减少了回流的次数；

3、增加或者移除样式表；

4、内容的变化，用户在input中输入了文字（这是不可避免的）；

5、激活CSS的伪类；

6、操作class属性；

7、基本操作DOM(包括js中的domcument等)；

8、计算offsetWidth与offsetHeight 属性，获取元素在窗口中的位置；

9、在html代码中直接设置style 属性的值，这个降低了代码的利用率，还影响性能。

## 如何避免回流？

1、如果想设定元素的样式，直接改变class名，而不是改变class中的某个特定的属性，比如height，weight;

2、避免设置多项内联样式，就是说少使用style；

3、应用元素动画的时候，使用属性的position属性的fixed值或absolute值；

4、避免使用table布局；

5、尽量在DOM树的最末端改变class,改变子节点的样式。

# 居中布局

## 水平居中

* 行内元素：`text-align: center`
* 块级元素：`margin: 0 auto`
* 绝对定位和移动：`absolute + transform`

```css
.son {
    /*
    当把当前元素设置为绝对定位后，
    如果父级元素没有开启定位的话，当前元素是相对于页面定位的
    如果父级元素开启了，则是相对于父级元素定位
    */
    position: absolute;
    /*
    设置离左边距的距离为50%(结果就是child的左边距居中了)
    */
    left: 50%;
    /*
    因为我们需要子元素整体居中，所以我们对子元素进行平移
    */
    transform: translateX(-50%);
}
```

* 绝对定位和负边距：`absolute + margin`

```css
.son {
    position: absolute;
    left: 50%;
    width: 100px;
    margin-left: -50px;
}
```

**说明：**宽度固定相比于使用transform ，有兼容性更好

* flex布局：`flex + justify-content: center`

## 垂直居中

* 子元素为单行文本：`line-height: height的值`
* 绝对定位和移动：`absolute + transform`

```css
.son {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
}
```

* 绝对定位和负边距：`absolute + margin`

```css
.son {
    position: absolute;
    top: 50%;
    height: 100px;
    margin-top: -50px;
}
```

* flex布局：`flex + align-items: center`
* `display:table-cell; 和vertical-align:middle;`

```css
.parent {
    display: table;
    width: 50px;
    height: 500px;
}
.son {
    display: table-cell;
    vertical-align: middle;
    background-color: aqua;
}
```

## 水平垂直居中

* 已知元素宽高：`absolute + margin:auto`

```css
.son {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    right: 0;
    margin: auto;
}
```

* 已知元素宽高：`absolute + 负margin`

```css
.son {
    width: 800px;
    height: 400px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -200px;
    margin-left: -400px;
}
```

* 绝对定位和移动：`absolute + transform`

```css
.son {
    position:absolute;
    left:50%;    /* 定位父级的50% */
    top:50%;
    transform: translate(-50%,-50%); /*自己的50% */
}
```

* flex布局：`flex + justify-content + align-items`

```css
.box {
    display:flex;
    justify-content:center;  /*子元素水平居中*/
    align-items:center;      /*子元素垂直居中*/
    height: 400px;
}
.son {
    background: green;
    width: 200px;
    height: 200px;
}
```

# 一行文字的省略

```html
<p style="
  width: 200px;
  overflow: hidden; // 超出部分隐藏
  white-space: nowrap; // 文本强制一行内显示
  text-overflow: ellipsis; // 文本有溢出时显示省略号
  ">
    省略我吧！
    省略我吧！
    省略我吧！
    省略我吧！
    省略我吧！
    省略我吧！
    省略我吧！
    省略我吧！
  </p>
```

# 两栏布局

## 左float右margin-left（左边宽度固定）

```html
<div class="left">left</div>
<div class="right">right</div>
```
```css
body,div{padding: 0 ;margin:0;}
.left,.right{height: 200px;}
.left{float: left;width: 200px;background-color:skyblue;}
.right{margin-left: 200px; background-color: greenyellow;}
```
因为块级元素有流体特性，即默认会填充满外部容器，所以只需要设置margin，不需要设置width就可以让content填满剩余的部分

## 绝对定位（左边宽度固定）

```html
<div class="wrap">
	<div class="left">left</div>
	<div class="right">right</div>
</div>
```
```css
.wrap{position : relative; }
.left{ width: 200px; }
.right{ position: absolute; top: 0; left: 200px; right: 0}
```

通过设置right:0；来限制右边块级元素的宽度



## 弹性布局

```html
<div class="wrap">
	<div class="left">left</div>
	<div class="right">right</div>
</div>
```
```css
body,div{padding: 0 ;margin:0;}
.wrap{display: flex;}
.left,.right{height: 200px;}
.left{width: 200px;background-color:skyblue;}
.right{flex: 1; background-color: greenyellow;}
```
但好像实际的应用中，并不喜欢弹性布局

## 左float 右overflow:hidden

```html
<div class="left">left</div>
<div class="right">right</div>
```

```css
body,div{padding: 0 ;margin:0;}
.left,.right{height: 200px;}
.left{float: left;width: 200px;background-color:skyblue;}
.right{overflow:hidden; background-color: greenyellow;}
```

右侧设置的overflow:hidden会触发块级格式化上下文（BFC）。

### BFC

触发BFC的方法：

- body根元素
- 浮动元素（除了float:none）
- 定位的元素（absolute、fixed）
- display ( inline-block、table-cells、flex )
- overflow ( hidden、auto、scroll )

具有BFC特性的元素可以看作是隔离了的独立容器，容器里的元素不会在布局上影响外面的元素，所以右边可以用触发BFC的元素来清除左边浮动的影响。

**触发了BFC的元素仍然保持流体特性**，也就是说BFC元素虽然不与浮动交集，自动退避浮动元素宽度的距离，但是在布局上自动填满浮动内容以外的剩余空间

# Flex

## flex-direction

用于控制项目排列方向与顺序

- row(默认)
- row-reverse(横向反转)
- column
- column-reverse(纵向反转)

## flex-wrap

用于控制项目是否换行，nowrap表示不换行

- nowrap(默认)
- wrap(换行)
- wrap-reverse(换行并反转)

## justify-content

用于控制项目在横轴的对齐方式，默认flex-start即左对齐

- flex-start(默认)
- flex-end(右对齐)
- center(居中)
- space-between(左右两侧项目紧贴容器，且项目之间间距相等)
- space-around(项目之间间距 = 左右两侧项目到容器间距的2倍)
- space-evenly(项目之间间距 = 左右两侧项目到容器间距)

## align-items

用于控制项目在纵轴排列方式，默认stretch即如果项目没设置高度，或高度为auto，则占满整个容器

- stretch(默认)
- flex-start(项目在纵轴紧贴容器顶部)
- flex-end(项目在纵轴紧贴容器底部)
- center(项目在纵轴中心位置)
- baseline(让项目以第一行文字的基线为参照进行排列)

## align-content

用于控制多行(一行多个)项目的对齐方式，如果项目只有一行则不会起作用

- stretch(默认)
- flex-start(项目在纵轴紧贴容器顶部)
- flex-end(项目在纵轴紧贴容器底部)
- center(项目在纵轴中心位置)
- space-between(上下两端项目紧贴容器，且项目之间间距相等)
- space-around(项目之间间距 = 上线两端项目到容器间距的2倍)
- space-evenly(项目之间间距 = 上下两端项目到容器间距)

## flex-grow

指定flex元素的flex增长系数，指定flex容器中剩余空间的多少应该分配给元素

分配的是宽度还是高度，取决于`flex-direction`值

<img src="https://z3.ax1x.com/2021/10/15/581Sun.png" alt="image-20211015192924640"  />

<img src="https://z3.ax1x.com/2021/10/15/581iNT.png" alt="image-20211015193204540"  />

## flex-shrink

指定flex元素的收缩规则，flex元素宽度之和大于容器时才会发生收缩

box1 flex-shrink: 1;   box2  flex-shrink: 3

400px+400px>500px，收缩后盒子宽的比例为3:1
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200114095829277.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020011409585066.png)

## flex-basis

指定flex元素在主轴方向上的初始大小

当一个元素同时被设置了 `flex-basis` (除值为 `auto` 外) , `flex-basis` 具有更高的优先级.

**可以使用一个，两个或三个值来指定 `flex`属性。**

```css
/* 一个值, 无单位数字: flex-grow */
flex: 2;

/* 一个值, width/height: flex-basis */
flex: 10em;
flex: 30px;
flex: min-content;

/* 两个值: flex-grow | flex-basis */
flex: 1 30px;

/* 两个值: flex-grow | flex-shrink */
flex: 2 2;

/* 三个值: flex-grow | flex-shrink | flex-basis */
flex: 2 2 10%;
```

