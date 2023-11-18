---
title: CSS记录
date: 2023-09-01 19:27:33
tags: 
- CSS
- Web
description: The key record of CSS. 
---
#### 行内样式
`style` 是 CSS 的属性名
在 CSS 中名-值对中间用 `:`
`font-size: xx px;` 可以设置字体大小
一般不推荐使用行内样式，不能复用并且不利于维护。
```
<h1 style="color: red; font-size: 50px;">Hello World</h1>
```

#### 内部样式
在 `<head>` 标签或者 `<body>` 标签中加一个 `<style>` 标签(不过一般都是写在 `head` 里面)。

#### 外部样式
可以新建一个 `xxx.css` 文件，然后在 HTML 文件的 `<head>` 标签中加一个 `<link>` 标签
```
<link rel="stylesheet" href="./xxx.css">
```
其中 `rel` 是 `relation` 的缩写，就是说 `href` 的文件和当前 HTML 文件的关系。

#### 样式优先级 
行内样式的优先级 > 内部样式
对于内部样式和外部样式，它俩平级，但是后来者居上，也就是说，谁写在后面，就是展现谁的样式。

#### 选择器
1. 通配选择器：
```
* {

}
```

2. 类选择器：在标签中添加属性 `class="xxx"`，注意在 `style` 中的格式，需要在 `xxx` 前面加一个 `.`，来区分类名和标签名。
```
.xxx {

}
```
要是一个标签属于两个 `class` 的话，写成 `class="xxx yyy"` 的格式，而不是分开写两个 `class`，那样的话后一个 `class` 会被忽略。

3. ID 选择器：
```
# xxx {

}
```

4. 交集选择器：
就是将两个选择器紧紧的写在一起。如果交集选择器中有元素，元素必须在开头(因为字母放在最后会引起单词的歧义)，并且我们交集的条件可以是多个。
`id` 选择器理论上可以作为交集选择器，但是我们的 `id` 是唯一的，已经可以唯一定义了，所以一般就是 `class` 和标签一起写。
同时也不存在两个元素同时在标签选择器中。
```
p.xxx {

}
```

5. 并集选择器
就是在不同选择器之间加上逗号 `,`
```
.rich,.beauty,.dog,.pig {

}
```
不过这样写的话，逗号和点写在一起看起来有些乱，我们一般竖着写：
```
.rich,
.beauty,
.dog,
.pig {

}
```

6. 后代选择器
比如说 `ul` 中的所有 `li`，中间直接空格就可以。但是除了选择了儿子以外，孙子 `li` 也被选择了。
```
ul li {

}
```

7. 子代选择器
`div` 标签中的子代 `a` 标签(排除了孙子等标签，只有儿子)
```
div>a {

}
```

8. 兄弟选择器
用 `+` 连接，只有紧紧相邻的兄弟，如果 `div` 紧紧相邻的没有 `p`，但是有 `p` 中间隔了别的标签，也不不起作用的。(睡在我下铺的兄弟) 相邻兄弟选择器
```
div+p {

}
```
如果是 `div~p {}` 就是 `div` 的所有兄弟 `p`，而不是紧紧相邻的了。

9. 属性选择器
`[title] {}` 选择具有 `title` 属性的标签
`[title="xxx"] {}` 选择具有 `title` 属性并且属性内容是 `xxx` 的标签。
`[title^="a"] {}` 选择具有 `title` 属性并且属性内容是以 `a` 开头的标签。
`[title$="a"] {}` 选择具有 `title` 属性并且属性内容是以 `a` 结尾的标签。
`[title*="a"] {}` 选择具有 `title` 属性并且属性内容中含有 `a` 的标签

#### 伪类选择器
可以理解为是对于元素的状态的一种描述。比如，已经访问过的超链接和未访问过的超链接，就是加一个冒号，后面就是元素的状态
```
a:link {

}
a:visited {

}
```

#### 三大特性
1. 层叠性
如果样式发生了冲突，就会根据一定的规则(选择器优先级)，进行样式层叠(覆盖)。(当权重一样的时候，我们才考虑在代码中的顺序)
2. 继承性
元素会自动拥有其父元素、或者祖先元素上设置的**某些样式**，优先继承离得最近的。
常见的可继承属性：`test-?? font-?? line-?? color`
3. 优先级
`!important > 行内样式 > ID 选择器 > 类选择器 > 元素选择器 > * > 继承的样式`

#### 像素 Pixel
虽然 `cm` 和 `mm` 这两个单位也可以用在网页中，但是对于网页来说，这两个单位不够精细。所以我们就是用 `px` 这个单位(是 Pixel 的缩写)，因为它很小，所以很精细。
{%asset_img 像素.png%}
可以看出来，虽然电脑屏幕一般大小，但是右边的像素多，所以每一个像素的大小就小。所以像素我们不确定多么大，需要看屏幕，它是一个相对单位。
像素点越小，呈现出来的图片就越细腻，越清晰

#### 颜色
1. 颜色名
但是它太有限了，并且不是很精确，所以开发的时候一般不用。
2. RGB 或者 RGBA
RGB 中三个字母分别是 RED GREEN BLUE(范围都是从 0 到 255)
`rgb(xx, xx, xx);`
`rgba(xx, xx, xx, xx);` 前三位和 `rgb` 相同，最后一位是透明度，范围是 0 - 1。
3. HEX 或者 HEXA
`#xxxxxx` 井号后面一共六位，每一位都是十六进制的数字，每两位组合起来分别表示红、绿、蓝
然后 HEXA 就像 RGBA，就是添加了一个透明度，它也是用两位十六进制来表示，也就是说一共八位。
4. HSL 或者 HSLA
这两个东西用的不是很多。
`hsl(hue, saturation, lightness);` 色相、饱和度、亮度
`Hue` 在这里是用角度表示的，写为 `xxdeg`
HELA 就是 `hsl(hue, saturation, lightness, xx);` 最后一位 0 - 1 表示透明度。
{%asset_img 色相环.png%}

#### 字体属性

`font-family: "xxx";` 字体族，其实就是字体样式。通常情况下，把字体分为两大类。第一类是衬线字体，第二类是非衬线字体。衬线字体的横竖撇捺特别有棱角，目前写网页还是非衬线字体比较多。

`font-style: xxx;` 字体风格。默认为 `normal`，斜体是 `italic`

`font-weight:xxx;` 字体粗细，参数为 `lighter normal bold bolder`，或者写 100 - 1000 的数字，数字越大越粗。

#### 文本属性
`letter-spacing:xxx px;` 字母间距(汉字被认为是字母)
`word-spacing:xxx px;` 词间距
`text-decoration:xxx;` 文本修饰 `overline underline line-through` 还可以改为波浪线等形式，并且也可以改颜色。
`text-indent:xx;` 文本缩进
`text-align:xxx;` `xxx` 可以是 `left center right` 就是靠哪里对齐。
`line-height:xxx;` 调整行高，就是上下之间的距离变大，但是字体的大小不变。其中 `xxx` 可以为像素、也可以写一个数字，表示是 `font-size` 的多少倍，也可以写成百分比，表示是 `font-size` 的多少倍。
`vertical-align:xxx;` `xxx` 可以是 `top baseline bottom middle` 

#### 列表属性
`list-style-type:xxx;` `xxx` 可以是 `none square lower-roman upper-roman decimal`
`list-style-position:xxx;` 可以是 `inside outside`
`list-style-image:xxx;` 找一个图片，自定义前面的点。

#### 表格属性
`border-width:xxx px;` 宽度 
`border-color:xxx;` 颜色
`border-style:xxx;` 样式
边框的相关属性，不仅仅是表格可以使用，其他元素如 `h1 p` 也可以使用。
`table-layout:fixed;` 可以控制表格的列宽。
`border-spacing:xxx px;` 控制单元格之间的距离。
`borer-collapse: collapse;` 合并相邻单元格的标签。写了合并以后，上面的 `border-spacing:xxx;` 无论 `xx` 是多少都失效了。
`empty-cells: show / hide;` 隐藏没有内容的单元格。
`caption-side:xxx;` 设置表格标题的位置，可以是 `top bottom`

#### 背景属性
`background-color:xxx;`
`background-repeat:repeat / no-repeat / repeat-y / repeat-x;` 如果图片较小，是否重复显示
`background-image:xxx;`
`background-position:xxx;` 可以控制背景图片的位置。`xxx` 可以是 `left top / left bottom / left center / xx px xx px`

#### 鼠标属性
`cursor:xxx;` 参数可以为 `pointer / move / wait / crosshair / help `
`cursor: url("xxx"),pointer;` 其中 `xx` 是一个图片的地址，此时鼠标的样式就变为了图片的样子。

#### CSS 常用的长度单位
1. `px`
2. `em` 相当于当前元素的 `font-size` 的倍数。如果自己没有就沿着父元素一直网上找，如果都没有，就是用默认的。
3. `rem` r 是 root 的意思。相对于根元素的 `font-size` 的倍数，如果没有，就使用默认的。
4. `%` 相对于父元素计算。

#### 盒子模型
1. 块元素 block
在页面中独占一行，不会与任何元素共占一行，是从上到下排列的。
默认宽度就是撑满父级元素，高度由内容决定。
2. 行内元素 inline
在页面中不是独占一行，一行中不能容下的行内元素，会在下一行继续从左到右排列。
默认宽度和高度都是由内容决定。
但是 **无法通过 CSS 设置宽和高。**
最具有代表性的其实就是 `<span>`
3. 行内块元素 inline-block
又叫做内联块元素。在页面中不独占一行，会在下一行继续从左到右排列。
默认宽度和高度都是由内容决定。
**可以通过 CSS 设置宽和高。**
最具代表性的其实是 `<img>`
{%asset_img 各元素显示模式.png%}

##### 修改元素的显示模式
上面是各种元素的默认显示形式，不过我们可以在 CSS 中修改 `display` 属性来调整它的显示形式。
`display: block / inline-block / inline;` 如果是 `display: none;` 那么这个元素就直接不显示了，并且也不会占用网页的空间。

##### 盒子模型的组成部分
我们设置的背景颜色会填充内边距区域，也会填充边框区域。
外边距不会影响盒子大小，只会影响其位置。
{%asset_img 分区.png%}

`width-min width-max height-min height-max padding-left padding-top padding-bottom padding-right`

`border` 的属性同样也可以是 `border-left-width border-left-style ... `

`margin` 的属性可以同 `padding` 一样修改。

#### 处理溢出
`overflow: hidden;` 直接隐藏，还可以写 `scroll auto` 默认是 `visible`，也可以 x y 方向分开处理，就是写成 `overflow-x` 和 `overflow-y`

#### 隐藏元素的方式
1. 就是 `display: none;` 通过这种方式隐藏的元素不会再去占据页面的位置。
2. 有一个属性专门控制元素的显示 `visibility: show;` 默认是 `show`，如果想隐藏就改为 `hidden`。不过通过这种方式隐藏的仍然会占位。

一个关于开发者模式四个分区作用的说明。
{%asset_img 开发者模式.png%}
{%asset_img 布局技巧.png%}

#### 浮动 float
浮动最早期设计出来是为了实现文字环绕图片或者说文字环绕文字。现在浮动是主流的页面布局方式之一。
1. 给第一个子元素设置 `margin-top` 会被父元素抢走，但是如果这个子元素浮动以后，就不会这样了。
2. 浮动后的元素不会被当作文本处理了(行内和行内块都会被当作文本处理)
3. 脱离文档流
4. 不会独占一行，可以共用一行

```
<!DOCTYPE html>
<html>
    <head>
        <title>
            this is a test.
        </title>
        <style>
            .outer {
                background-color: gray;
                border: black 1px solid;
            }
            .box {
                margin: 10px;
                width: 100px;
                height: 100px;
                background-color: skyblue;
                border: solid black 1px;
            }
            .box1 {
                float: right;
            }
        </style>
    </head>
    <body>
        <div class="outer">
            <div class="box box1">1</div>
            <div class="box box2">2</div>
            <div class="box box3">3</div>
        </div>
    </body>
</html>
```

浮动之后，盒子因为脱离了标准文档流，它撑不起父盒子的高度，导致父盒子高度塌陷
##### 清除浮动带来影响的方式
1. 父盒子设置固定高度
虽然，给父盒子设置了固定高度能暂时解决我们的问题，但是它的使用不灵活，如果未来子盒子的高度需求发生了改变(网页的多处地方)，那么我们得手动需要更改父盒子的高度。后期不易维护。
2. 内墙法
所谓内墙法,有一个规则:在浮动元素的后面加一个空的块级元素(通常是div),并且该元素设置clear:both；属性。
clear属性，字面意思就是清除，那么both,就是清除浮动元素对我左右两边的影响。
3. 伪元素清除法
https://juejin.cn/post/6886247611318140942
在最后补加一个没有实际意义的块元素 `div`，然后添加 `div` 的 CSS 属性 `clear: both;`，这个块元素没有高，没有宽，没有内容，就是专门用来撑起父元素。
或者更加优雅写成
```
xxx::after {
    content: '';
    display: block;
    clear: both;
}
```
其中 `content: ''` 表示元素为空，`display: block` 才能撑起父元素(因为另起一行了)，`clear: both;` 就是消除之前的浮动带来的所有影响。
4. `overflow: hidden;`

#### 定位
开启相对定位的元素并未脱离文档流。
如果一个元素开启了定位，那么它的层级就比普通元素的层级高。
相对定位：
1. 对于元素的位置进行微调。
2. 配合绝对定位

绝对定位：
1. 一旦开启绝对定位，就脱离了文档流。
2. 绝对定位参考的点是它的包含块。
    对于没有脱离文档流的元素，它的父元素就是它的包含块。
    对于脱离文档流的元素，它的第一个开启定位的祖先元素就是它的包含块。
3. 不论是块元素、行内元素还是行内块元素，只要进行了绝对定位，就变成了**定位元素**
    定位元素：
    1. 默认被内容撑开。
    2. 但是也是可以进行设置的。

固定定位：
就是直接对于视口定位。
1. 并且元素变成了定位元素。
2. 脱离了文档流。

粘性定位：
`position: sticky;`
参考点是离它最近的拥有滚动行为的祖先元素。包含粘性定位元素的父容器也不在视图上时，胶水就失效了。

这几个定位的层级是平等的。

#### z-index
属性 `z-index`(纯数值，没有单位) 就相当于 `z` 轴上的坐标，`z` 越大，层级越高，所以在屏幕上显示的优先级越高。

#### 布局
版心的大小一般是 900 - 1200 px
{%asset_img 常见布局名词.png%}

#### 重置默认样式
1. 使用全局选择器
在简单的案例中，我们可能使用这种方式，但是实际开发中我们不会使用。
```
* { padding: 0px; margin: 0px; }
```
2. 使用 `reset.css` 可以是自己一直以来的一个标准模板，也可以是使用一些公司开源的自己的 `reset.css`(比如小米、阿里...)
3. `Normalize.css` 是一种最新方案，它再清楚默认样式的基础上，保留了一些有价值的默认样式。
这是一个标准化的东西，有很多的网站和用户去维护这个东西。
http://necolas.github.io/normalize.css/

#### 练习
{%asset_img 练习1.png%}
```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        * {
            margin: 0px;
            padding: 0px;
        }
        .leftfix {
            float: left;
        }
        .rightfix {
            float: right;
        }
        .clearfix {
            overflow: hidden;
        }
        .container {
            margin: 0 auto;
            width: 960px;
            text-align: center;
        }
        .top-header {
            width: 960px;
            height: 80px; 
        }
        .logo,
        .banner1,
        .banner2 {
            background-color: gray;
            height: 80px;
            line-height: 80px;
        }
        .logo {
            width: 200px;
        }
        .banner2 {
            width: 200px;
        }
        .banner1 {
            width: 540px;
            margin: 0 10px;
        }
        .menu {
            background-color: gray;
            height: 30px;
            margin: 10px auto;
            line-height: 30px;
        }
        .item1,
        .item2 {
            height: 198px;
            width: 368px;
            border: solid black 1px;
            line-height: 198px;
        }
        .item2 {
            margin-left: 10px;
            margin-right: 10px;
        }
        .item3,
        .item4,
        .item5,
        .item6 {
            width: 178px;
            height: 198px;
            border: 1px solid black;
            margin-top: 10px;
            line-height: 198px;
            margin-bottom: 10px;
        }
        .item4,
        .item5,
        .item6 {
            margin-left: 10px;
        }
        .item7,
        .item8,
        .item9 {
            width: 198px;
            height: 128px;
            border: 1px solid black;
            margin-bottom: 10px;
            line-height: 128px;
        }
        .footer {
            background-color: gray;
            width: 960px;
            height: 60px;
            line-height: 60px;
        }
    </style>
</head>
<body>
    <div class="container">
        <!--header-->
        <div class="top-header clearfix">
            <div class="logo leftfix">
                logo
            </div>
            <div class="banner1 leftfix">
                banner1
            </div>
            <div class="banner2 leftfix">
                banner2
            </div>
        </div>
        <!--menu-->
        <div class="menu">
            菜单
        </div>
        <!--content-->
        <div class="content clearfix">
            <!--left-->
            <div class="left-content leftfix">
                <!--top-->
                <div class="top-content clearfix">
                    <div class="item1 leftfix">
                        栏目一
                    </div>
                    <div class="item2 leftfix">
                        栏目二
                    </div>
                </div>
                <!--bottom-->
                <div class="bottom-content clearfix">
                    <div class="item3 leftfix">栏目三</div>
                    <div class="item4 leftfix">栏目四</div>
                    <div class="item5 leftfix">栏目五</div>
                    <div class="item6 leftfix">栏目六</div>
                </div>
            </div>
            <!--right-->
            <div class="right-content leftfix">
                <div class="item7">栏目七</div>
                <div class="item8">栏目八</div>
                <div class="item9">栏目九</div>
            </div>
        </div>
        <!--footer-->
        <div class="footer">
            页脚
        </div>
    </div>
</body>
</html>
```
调整背景图的位置用 `background-position:xxx;`

布局里面，一堆东西横向排列一堆东西纵向排列，而且这一堆东西还很相似，往往我们都用 ul li

大多数情况都是给子元素开启固定定位，给父元素开启相对定位。

img 方式引入图片的话，我们不需要给出宽和高，就是图片默认的宽和高。但是 `div` 设置图片背景的时候，`div` 必须先有宽和高，才能显示图片。