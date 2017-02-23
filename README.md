# 浅谈媒体查询（Media Queries） 响应式布局

>demo 为媒体查询实现的简单响应式布局，可以给大家提供一个参考，欢迎下载，如果觉得不错的话，可以点击`stars`。



# 1. 前言

  随着移动终端设备的发展，移动web开发的需求也越来越多，移动产品的屏幕规格也多样化，这对于前端开发的同志们来说是非常打脑壳的，我们不得不去为了提升用户体验而做屏幕适配。目前主流的适配方法便是使用 `bootstrap` 响应式布局，这里我们只是浅谈如何使用媒体查询 `@media` 的方式进行响应式布局。

# 2. 什么是响应式布局

  响应式布局是Ethan Marcotte在2010年5月份提出的一个概念，简而言之，就是一个网站能够兼容多个终端——而不是为每个终端做一个特定的版本。这个概念是为解决移动互联网浏览而诞生的。

  响应式布局可以为不同终端的用户提供更加舒适的界面和更好的用户体验，而且随着目前大屏幕移动设备的普及，用大势所趋来形容也不为过。随着越来越多的设计师采用这个技术，我们不仅看到很多的创新，还看到了一些成形的模式。

# 3. 响应式布局的优缺点

## a. 优点

- 面对不同分辨率设备灵活性强
- 能够快捷解决多设备显示适应问题

## b. 缺点

- 兼容各种设备工作量大，效率低下
- 代码累赘，会出现隐藏无用的元素，加载时间加长
- 一定程度上改变了网站原有的布局结构，会出现用户混淆的情况

# 4. 媒体查询 Media Queries

  说到响应式布局，就不得不提到CSS3中的Media Query（媒体查询），Media Query是制作响应式布局的一个利器，使用这个工具，我们可以非常方便快捷的制造出各种丰富的实用性强的界面。CSS3 的多媒体查询继承了 CSS2 多媒体类型的所有思想： 取代了查找设备的类型，CSS3 根据设置自适应显示。媒体查询可用于检测很多事情，例如：

- viewport（视窗）的宽度与高度
- 设备的宽度与高度
- 朝向（智能手机横屏，竖屏）
- 分辨率

# 5. 自适应视窗

```html
<meta name="viewport" content="width=device-width,initial-scale=1">
```

> 代码原意翻译过来既是： 视窗的宽度等于设备宽度，原始比例始终为 1:1 。这样在改变 device-width 的时候任意变化修改都能自适应了。

  `meta viewport` 这个属性是在移动设备上设置原始大小显示和是否缩放的声明，其主要参数设置如下所示：

- width-viewport：viewport的宽度
- height-viewport：viewport的高度
- initial-scale：初始的缩放比例
- minimum-scale：允许用户缩放到的最小比例
- maximum-scale：允许用户缩放到的最大比例
- user-scalable：用户是否可以手动缩放

# 6. 媒体查询语法

> 语法结构：`@media 设备名 only(选取条件)|not(选取条件)|and(设备选取条件)`

- 多媒体查询由多种媒体组成，可以包含一个或多个表达式，表达式根据条件是否成立返回 `true` 或 `false` 。
- 如果指定的多媒体类型匹配设备类型则查询结果返回 true，文档会在匹配的设备上显示指定样式效果。
- 除非你使用了`not`或`only`操作符，否则所有的样式会适应在所有设备上显示效果。

## a. 判断媒体类型，引用不同的样式表



```html
<link rel="stylesheet" media="mediaType and|not|only (media feature)" href="styles.css">
```

> 通过设定屏幕的判断条件，调用对应的css文件，该实例多用于页面不同风格的css调用与选取，使用该方法可能需要为一个页面制作多个css文件。



## b. 判断媒体类型，执行不同的css样式属性

```css
@media mediaType and|not|only (media feature) {
      /* css code... */
}
```

> 上述实例可以出现在外部样式表与内部样式表中。`mediaType`指定媒体类型，`mediaFeature`指定判断条件。

## c. 逻辑关键字：not|only|all

| 类型   | 描述                                       |
| ---- | ---------------------------------------- |
| not  | 排除某种指定的媒体类型，换句话来说就是用于排除符合表达式的设备，比如`@media not print and （max-width:1200px）`表示排除宽度小于等于1200px的打印设备; |
| only | 用来指定某种特定的媒体类型，可以用来排除不支持媒体查询的浏览器。 其实only很多时候是用来对那些不支持Media Query但却支持Media Type的设备隐藏样式表的。 其主要有：支持媒体特性（Media Queries）的设备，正常调用样式，此时就当only不存在；对于不支持媒体特性(Media Queries)但又支持媒体类型(Media Type)的设备，就会忽略样式，因为其先读only而不是screen；另外不支持Media Queries的浏览器，不论是否支持only，样式都不会被采用； |
| all  | all：所有设备，如果在Media Query 中没有明确指定Media Tpe，那么其默认值就为all; |

## d.  media type

| 值      | 描述              |
| ------ | --------------- |
| all    | 用于所有多媒体类型设备     |
| print  | 用于打印机           |
| screen | 用于电脑屏幕，平板，智能手机登 |
| speech | 用于屏幕阅读器         |

## e. 可用设备参数

| 值                       | 描述                                       |
| ----------------------- | ---------------------------------------- |
| aspect-ratio            | 定义输出设备中的页面可见区域宽度与高度的比率                   |
| color                   | 定义输出设备每一组彩色原件的个数。如果不是彩色设备，则值等于0          |
| color-index             | 定义在输出设备的彩色查询表中的条目数。如果没有使用彩色查询表，则值等于0     |
| device-aspect-ratio     | 定义输出设备的屏幕可见宽度与高度的比率。                     |
| device-height           | 定义输出设备的屏幕可见高度。                           |
| device-width            | 定义输出设备的屏幕可见宽度。                           |
| grid                    | 用来查询输出设备是否使用栅格或点阵。                       |
| height                  | 定义输出设备中的页面可见区域高度。                        |
| max-aspect-ratio        | 定义输出设备的屏幕可见宽度与高度的最大比率。                   |
| max-color               | 定义输出设备每一组彩色原件的最大个数。                      |
| max-color-index         | 定义在输出设备的彩色查询表中的最大条目数。                    |
| max-device-aspect-ratio | 定义输出设备的屏幕可见宽度与高度的最大比率。                   |
| max-device-height       | 定义输出设备的屏幕可见的最大高度。                        |
| max-device-width        | 定义输出设备的屏幕最大可见宽度。                         |
| max-height              | 定义输出设备中的页面最大可见区域高度。                      |
| max-monochrome          | 定义在一个单色框架缓冲区中每像素包含的最大单色原件个数。             |
| max-resolution          | 定义设备的最大分辨率。                              |
| max-width               | 定义输出设备中的页面最大可见区域宽度。                      |
| min-aspect-ratio        | 定义输出设备中的页面可见区域宽度与高度的最小比率。                |
| min-color               | 定义输出设备每一组彩色原件的最小个数。                      |
| min-color-index         | 定义在输出设备的彩色查询表中的最小条目数。                    |
| min-device-aspect-ratio | 定义输出设备的屏幕可见宽度与高度的最小比率。                   |
| min-device-width        | 定义输出设备的屏幕最小可见宽度。                         |
| min-device-height       | 定义输出设备的屏幕的最小可见高度。                        |
| min-height              | 定义输出设备中的页面最小可见区域高度。                      |
| min-monochrome          | 定义在一个单色框架缓冲区中每像素包含的最小单色原件个数              |
| min-resolution          | 定义设备的最小分辨率。                              |
| min-width               | 定义输出设备中的页面最小可见区域宽度。                      |
| monochrome              | 定义在一个单色框架缓冲区中每像素包含的单色原件个数。如果不是单色设备，则值等于0 |
| orientation             | 定义输出设备中的页面可见区域高度是否大于或等于宽度。               |
| resolution              | 定义设备的分辨率。如：96dpi, 300dpi, 118dpcm        |
| scan                    | 定义电视类设备的扫描工序。                            |
| width                   | 定义输出设备中的页面可见区域宽度。                        |

## f. 示例

```css
// 1、当设备屏幕小于1180px时会采用该样式
@media screen and (max-width:1180px) { css codes }

/* 2、当设备屏幕大于850px时会采用该样式 */
@media screen and (min-width:850px) {  css codes }

/* 3、当设备屏幕大于850px,小于1180px时会采用该样式 */
@media screen and (max-width:850px) and (min-width:1180px) {  css codes }

/* 4、仅当电脑、手机、平板设备屏幕小于1180px时会采用该样式 */
@media only screen and (max-width:1180px) { css codes }

/* 5、设备屏幕的输出宽度Device width,下面的代码指的是iPhone.css样式适用于最大设备宽度为480px，比如说iPhone上的显示，这里的max-device-width所指的是设备的实际分辨率，也就是指可视面积分辨率 */
<link rel="stylesheet" media="screen and (max-device-width:480px)" href="iPhone.css" type="text/css">

/* 6、专门针对iphone4的移动设备 */
<link rel="stylesheet" media="only screen and (-webkit-min-device-pixel-ratio:2)" type="text/css" href="iPhone4.css">

/* 7、iPad，在大数情况下，移动设备iPad上的Safari和在iPhone上的是相同的，只是他们不同之处是iPad声明了不同的方向，比如说 下面的例子，在纵向(portrait)时采用portrait.css来渲染页面；在横向（landscape）时采用landscape.css来渲 染页面。*/

<link rel="stylesheet" media="all and (orientation:portrait)" href="portrait.css" type="text/css"> 

<link rel="stylesheet" media="all and (orientation:landscape)" href="landscape.css" type="text/css">

/*Android，我们可以使用media query为android手机在不同分辨率提供特定样式，这样就可以解决屏幕分辨率的不同给android手机的页面重构问题。*/

/*a、240px的宽度*/
<link rel="stylesheet" media="only screen and (max-device-width:240px)" href="android240.css" type="text/css" />

/*b、360px的宽度*/
<link rel="stylesheet" media="only screen and (min-device-width:241px) and (max-device-width:360px)" href="android360.css" type="text/css" />

/*c、480px的宽度*/
<link rel="stylesheet" media="only screen and (min-device-width:361px) and (max-device-width:480px)" href="android480.css" type="text/css" />



```



# 5. 注意事项

  有的时候你会发现一个奇怪的问题，就是你的@media没有起作用。我们知道`min-width`表示最小即大于等于（`>=`），`max-width`表示最大即小于等于（`<=`），代码从上往下依次执行，后面重复代码会覆盖之前的代码。正确的适配顺序如下：



> `max-width:num0;`：小于等于，分辨率从大写到小，如果同一选择器在更小分辨率下没有重写则会沿用css中定义的基本样式；

> `(min-width:num1) and (max-width:num2)` :大于等于num1，同时满足小于等于num2；写完`max-width`则开始写其中间值。num1必须在num0的基础上+1px，以免覆盖之前width<=num0的样式，num2 则不要求必须在 num3 的基础上 -1px (因为后面定义的 `width >= num3` 就算 width 的 num 相等也会根据先后原则覆盖这个样式) 。

> `min-wdith: num3` 大于等于 分辨率从小写到大 如果同一选择器样式在更大分辨率下没有重写则会沿用之前 `@media` 定义的样式 其次再是 CSS中定义的基本样式

# 7. 横排竖屏判断

## a. 用CSS判断横竖屏

```css
@media screen and (orientation:portrait) {}  /*竖屏*/
@media screen and (orientation:landscape) {} /*竖屏*/

<link rel="stylesheet" media="all and (orientation:portrait)" href="portrait.css"> /*竖屏*/
<link rel="stylesheet" media="all and (orientation:landscape)" href="landscape.css"> /*竖屏*/
```

## b. 用JavaScript判断横竖屏

```javascript
//判断手机横竖屏状态：
window.addEventListener("onorientationchange" in window ? "orientationchange" : "resize", function() {
        if (window.orientation === 180 || window.orientation === 0) {
            alert('竖屏状态！');
        }
        if (window.orientation === 90 || window.orientation === -90 ){
            alert('横屏状态！');
        } 
    }, false);
//移动端的浏览器一般都支持window.orientation这个参数，通过这个参数可以判断出手机是处在横屏还是竖屏状态。
```

- 屏幕方向对应的window.orientation值：

  > ipad, iphone：90或-90 横屏
  >
  > ipad, iphone：0或180  竖屏
  >
  > Andriod：0或180  横屏
  >
  > Andriod：90或-90 竖屏

## c. 用media判断横竖屏

```css
/*竖屏*/
@media screen and (orientation:portrait) {}
/*横屏*/
@media screen and (orientation:landscape) {}
```



