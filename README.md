# 浅谈@media响应式布局
# 1. 前言



闲暇之余，浅谈@media媒体查询实现响应式布局。随着移动设备的发展，移动web开发的需求也越来越多，移动产品的屏幕规格也多样化，这对于前端开发的同志们来说是非常打脑壳的，我们不得不去为了提升用户体验而做屏幕适配。

# 2. CSS3 多媒体查询

CSS3 的多媒体查询继承了 CSS2 多媒体类型的所有思想： 取代了查找设备的类型，CSS3 根据设置自适应显示。媒体查询可用于检测很多事情，例如：

- viewport（视窗）的宽度与高度
- 设备的宽度与高度
- 朝向（智能手机横屏，竖屏）
- 分辨率

# 3. 自适应视窗

```html
<meta name="viewport" content="width=device-width,initial-scale=1">
```

> 代码原意翻译过来既是： 视窗的宽度等于设备宽度，原始比例始终为 1:1 。这样在改变 device-width 的时候任意变化修改都能自适应了。

# 4. 多媒体查询语法

- 多媒体查询由多种媒体组成，可以包含一个或多个表达式，表达式根据条件是否成立返回 `true` 或 `false` 。
- 如果指定的多媒体类型匹配设备类型则查询结果返回 true，文档会在匹配的设备上显示指定样式效果。
- 除非你使用了`not`或`only`操作符，否则所有的样式会适应在所有设备上显示效果。

## I. 判断媒体类型，引用不同的样式表



```html
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="styles.css">
```

> 通过设定屏幕的判断条件，调用对应的css文件，该实例多用于页面不同风格的css调用与选取，使用该方法可能需要为一个页面制作多个css文件。



## II. 判断媒体类型，执行不同的css样式属性

```css
@media media type and|not|only (media feature) {
      /* css code... */
}
```

> 上述实例可以出现在外部样式表与内部样式表中。`mediatype`指定媒体类型，`mediafeature`指定判断条件。

## III. not/only/all

| 类型   | 描述                                      |
| ---- | --------------------------------------- |
| not  | 排除掉某些特定设备的，比如`@media not print`表示非打印设备; |
| only | 指定某种特别的媒体类型;                            |
| all  | all：所有设备;                               |

> tips：对于支持 Media Queries 的移动设备来说，如果存在 only 关键字，移动设备的 Web 浏览器会忽略 only关键字并直接根据后面的表达式应用样式文件。对于不支持 Media Queries 的设备但能够读取 Media Type 类型的 Web浏览器，遇到 only 关键字时会忽略这个样式文件。

## IV.  media type

| 值      | 描述              |
| ------ | --------------- |
| all    | 用于所有多媒体类型设备     |
| print  | 用于打印机           |
| screen | 用于电脑屏幕，平板，智能手机登 |
| speech | 用于屏幕阅读器         |

## V. media feature

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

## VI. 示例

```css
// 1、当设备屏幕小于1180px时会采用该样式
@media screen and (max-width:1180px) { css codes }

// 2、当设备屏幕大于850px时会采用该样式
@media screen and (min-width:850px) {  css codes }

// 3、当设备屏幕大于850px,小于1180px时会采用该样式
@media screen and (max-width:850px) and (min-width:1180px) {  css codes }

// 4、仅当电脑、手机、平板设备屏幕小于1180px时会采用该样式
@media only screen and (max-width:1180px) { css codes }
```



# 5. @media 注意事项

有的时候你会发现一个奇怪的问题，就是你的@media没有起作用。我们知道`min-width`表示最小即大于等于（`>=`），`max-width`表示最大即小于等于（`<=`），代码从上往下依次执行，后面重复代码会覆盖之前的代码。正确的适配顺序如下：



> 1. `max-width:num0;`：小于等于，分辨率从大写到小，如果同一选择器在更小分辨率下没有重写则会沿用css中定义的基本样式；

> 1. `(min-width:num1) and (max-width:num2)` :大于等于num1，同时满足小于等于num2；写完`max-width`则开始写其中间值。num1必须在num0的基础上+1px，以免覆盖之前width<=num0的样式，num2 则不要求必须在 num3 的基础上 -1px (因为后面定义的 `width >= num3` 就算 width 的 num 相等也会根据先后原则覆盖这个样式) 。

> 1. `min-wdith: num3` 大于等于 分辨率从小写到大 如果同一选择器样式在更大分辨率下没有重写则会沿用之前 `@media` 定义的样式 其次再是 CSS中定义的基本样式

# 6. 横排竖屏判断

## I. 用CSS判断横竖屏

```css
/*横屏*/
@media (orientation:portrait) {} 

/*竖屏*/
@media (orientation:landscape) {}

/*横屏*/
<link rel="stylesheet" media="all and (orientation:portrait)" href="portrait.css">

/*竖屏*/
<link rel="stylesheet" media="all and (orientation:landscape)" href="landscape.css">
```

## II. 用JavaScript判断横竖屏

```javascript
// 判断手机横竖屏状态
function judgeOrientation() {
  if(window.orientation==180||window.orientation==0) {
    alert('竖屏状态')
  }
  if(window.orientation==90||window.orientation==-90) {
    alert('横屏状态')
  }
}

window.addEventListener("onorientationchange" in window ? "orientationchange" : "resize", judgeOrientation, false);

// 移动端的浏览器一般都支持window.orientation这个参数，通过这个参数可以判断出手机是处在横屏还是竖屏状态。

// 从而根据实际需求而执行相应的程序。通过添加监听事件onorientationchange，进行执行就可以了。
```

## III. 用@media判断横竖屏

```css
/*竖屏*/
@media screen and (orientation:portrait) {}
/*横屏*/
@media screen and (orientation:landscape) {}
```



