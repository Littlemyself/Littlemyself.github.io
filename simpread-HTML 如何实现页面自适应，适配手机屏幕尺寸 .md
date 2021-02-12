

### 1、首先在网页代码的头部，加入一行`viewport`标签

在网页的头部中增加以下这句话，可以让网页的宽度自动适应手机屏幕的宽度

```php+HTML
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no">
```

**width=device-width** width 为设置 layout viewport 的宽度，为一个正整数，”width-device” 表示宽度是设备屏幕的宽度  
**initial-scale=1.0** initial-scale 为设置页面的初始缩放值，可以是一个带小数的数字，1.0 就是占网页的 100%  
**minimum-scale=1.0** 表示最小的缩放比例  
**maximum-scale=1.0** 表示最大的缩放比例  
**user-scalable=no** 表示用户是否可以调整缩放比例，值为”no” 或”yes”

### 2、宽度不要用绝对的

```css
width:auto; / width:XX%;（父元素一定要有宽度）
```

### 3、字体大小是页面默认大小的 100%，即 16 像素，不要使用绝对大小 "px"，要使用相对大小 “rem”

```css
html{font-size:62.5%;}
body {font:normal 100% Arial,sans-serif;font-size:14px; font-size:1.4rem; } 
```

html 的字体大小设置为`font-size:62.5%`**原因**：浏览器默认字体大小是`16px`，`rem`与`px`关系为：`1rem = 10px`，10/16=0.625=62.5%，**为了子元素相关尺寸计算方便**，这样写最合适不过了。

### 4、流动布局，"流动布局" 的含义是，各个区块的位置都是浮动的，不是固定不变的

```css
.left{ width:30%; float:left} 
.right{ width:70%; float:right;}
```

像这样，用左浮动和右浮动，好处是，如果宽度太小，放不下两个元素，后面的元素会自动滚动到前面元素的下方，不会在水平方向`overflow`（溢出），避免了水平滚动条的出现

### 5、选择加载 CSS

"自适应网页设计" 的核心，就是 CSS3 引入的 Media Query 模块。自动探测屏幕宽度，然后加载相应的 CSS 文件

```css
<link rel="stylesheet" type="text/css" media="screen and (max-device-width: 600px)" href="style/css/css600.css" />
```

**这段代码的意思是：如果屏幕宽度小于 600 像素（max-device-width: 600px），就加载 css600.css 文件。**

**如果屏幕宽度在 600 像素到 980 像素之间，则加载 css600-980.css 文件**

```css
<link rel="stylesheet" type="text/css" media="screen and (min-width: 600px) and (max-device-width: 980px)" href="css600-980.css" /> 
```

还有 (不建议使用)：除了用 html 标签加载 CSS 文件，还可以在现有 CSS 文件中加载

```css
@import url("css600.css") screen and (max-device-width: 600px); 
```

### 6、CSS 的 @media 与 @media screen，媒体查询 / 匹配

媒体查询也是 css3 的方法，我们要解决的问题是适应手机屏幕

媒体查询的功能就是为不同的媒体设置不同的 css 样式，这里的 “媒体” **包括页面尺寸，设备屏幕尺寸**等。

**首先先讲一下 @media 与 @media screen 区别**

**`@media`与`@media screen`两者在手机设备上没有区别，但`@media screen`的 css 在打印设备里是无效的，而`@media`在打印设备里是有效的，如果 css 需要用在打印设备里，那么就用`@media` 。**

### 语法

以`@media`或`@media screen and`开头来表示这是一条媒体查询语句。`@media`后面的是一个或者多个表达式，如果表达式为真，则应用样式。

**@media**

```css
@media (max-width: 600px) {
  .mainner {
    display: none;
  }
}
```

上面的代码在屏幕宽度小于 600px 的时候，会作用大括号里的内容。

**注：max-width 是目标显示区域的宽度，例如，浏览器宽度。**

媒体查询可以在 link 标签上加 media 属性或 css 文件中使用。具体例子就不举了。

**@media screen**

以下例子为当屏幕宽度小于 400px 的时候，就取消浮动

```css
@media screen and (max-device-width: 400px) 
{  .left {
     float:none;
   } 
 }
```

**注：max-device-width 是设备整个显示区域的宽度，例如，真实的设备屏幕宽度。**

### 知识扩展

> @media only screen and  
> only(限定某种设备)  
> screen 是媒体类型里的一种  
> and 被称为关键字，其他关键字还包括 not  
> not 指定某种特定的媒体类型，可以用来排除不支持媒体查询的浏览器

例如：如果浏览器窗口小于 500px, 背景将变为浅蓝色：

```css
@media only screen and (max-width: 500px) {
    body {
        background-color: lightblue;
    }
}
```

### 7、图片自适应，"自适应网页设计" 还必须实现图片的自动缩放。

```css
img {width: 100%;} 
```

windows 平台缩放图片时，可能出现图像失真现象。这时，可以尝试使用 IE 的专有命令

```css
img { width:100%; -ms-interpolation-mode: bicubic;} 

```

**或使用 js–imgSizer.js**

```php
addLoadEvent(function() { 
　　var imgs = document.getElementById("content").getElementsByTagName("img"); 
　　imgSizer.collate(imgs); 
});
```

附代码
---

```css
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta >
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title></title>
        <style type="text/css">
            body{
                background: url(images/bg.png) no-repeat;
                background-size:100% 100%;
                background-attachment: fixed;
            }
            .container{
                width: 100%;
                text-align: center;
                position: absolute;
                top: 96px;
            }
             .container img{
                transform: scale(0.8);
                height: auto;
                width: auto\9;

            }
            #img1{
                width: 100%;
                position: absolute;
                bottom: 10px;
                margin-bottom: 40%;
                transform: scale(0.9);
                /*background: yellowgreen;*/
            }
            #img2{
                width: 100%;
                position: absolute;
                bottom: 20px;
                margin-bottom: 12%;
                transform: scale(0.9);
            }
        </style>
    </head>
    <body>
        <div>
            <img src="images/logo@2x.png" alt="" />
        </div>
        <input type="image" src="images/iOS@2x.png"/>
        <input type="image" src="images/Android@2x.png"/>
        
    </body>
</html>
```