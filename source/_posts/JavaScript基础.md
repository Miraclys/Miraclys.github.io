---
title: JavaScript基础
date: 2023-08-28 14:10:05
tags: JavaScript, WEB
description: The key record of JavaScript. 
---
变量的声明就是 `var name = xxx;`。其中 `var` 是 `variable` 的缩写（虽然和方差 variance 的缩写一样）。

在 JS 中使用 {} 来分块，同一个 {} 中的语句我们称之为一组语句，它们要么都执行，要么都不执行。

其实函数也是一个对象，可以如下定义一个函数：`f = new Function("console.log('this is a function. ')")`。但是一般不这么使用。

```
var obj = {
    name: 'lys',
    age: 19,
    address: 'SDU'
}
for (var x in obj) {
    console.log(x); // 这样只是枚举的对象中的元素名字
}
for (var x in obj){
    console.log(obj[x]); // 不能直接 obj.x 来获得具体元素，应用 [] 的引用方式。
}
```

数组创建 `var arr = new Array()` 或者 `var arr = []`。但是一般不使用 `new Array()` 的创建方式。并且数组中的元素类型也是不一定的，不一定非要是 Number 类型的。
其实数组也是一个对象，只不过索引方式是 []，所以对象有的东西数组也有。

数组既然是对象，就有方法，在 JS 中数组有一些常用的方法：
1. `push()` 向数组末尾添加一个或者多个元素，并且返回新的数组的长度。
2. `pop()` 从数组末尾删除一个元素，并且返回删除的元素。
3. `unshift()` 向数组的**开头**添加一个或者多个元素，并且返回新的数组的长度。
4. `shift()` 从数组开头删除一个元素，并且返回删除的元素。
5. `join()` 将所有的元素连接成一个字符串。
6. `slice()` 返回数组的一部分，不修改原数组。

建立函数
```
function xxx() {

}
```

如果是构造函数
```
function Person() {

}
var person = new Person();
```
如果不写前面的 function 直接 new，会出现错误。

arr.forEach(xx) 中间 xx 都要传递一个函数，如果之前定义了 `function fun() {}` 就写为 `arr.forEach(fun)`，但是一般不这样，一般都是用匿名函数。
```
var arr = [1, 2, 3];
arr.forEach(function(a, b, c) {
    console.log(a);
});
```
上面就是输出 a，遍历的时候会将 arr 中的元素传递给 function。
会传递三个参数，第一个是数组当前遍历到元素 value，第二个是当前遍历到的索引 index，第三个是正在遍历的数组。

函数在调用的时候，浏览器会向里面传递两个隐含的参数
1. 上下文对象的 this
2. 封装实参的类数组对象 arguments，在调用函数的时候，我们所传递的实参都会在 arguments 中保存。

在 JS 中，对象有 3 类
{%asset_img 对象.png%}
DOM Document Object Model
JS 通过 DOM 对于 HTML 文档进行操作，只要理解了 DOM，就可以随心所欲操作 WEB 页面。

节点 Node 是构成 HTML 文档的最基本的单元，常用节点分为四类
- 文档节点 整个 HTML 文档
- 元素节点 HTML 文档中的 HTML 标签
- 属性节点 元素的属性
- 文本节点 HTML 标签中的文本
{%asset_img 节点.png%}

{%asset_img 节点的属性.png%}
上面的三个属性是每一个节点都有的三个属性。

innerHTML 可以获得到文字

事件就是文档或浏览器窗口中发生的一些特定的交互瞬间。JavaScript 与 HTML 之间的交互是通过事件实现的。比如对于 Web 应用来说，有下面一些有代表性的事件：点击某个元素、将鼠标移动至某个元素上方、按下键盘上某个键等等。

`onload` 事件会在整个页面加载完成之后发生。
```
window.onload= function() {
    xxx
}
```
这一段代码是页面加载完成之后执行的。

标签就是元素，元素就是标签。

{%asset_img 获取元素节点.png%}

innerHTML 对于「自结束标签」没有意义。如：
{%asset_img 自结束标签.png%}
如果想读取元素的属性，直接 `元素.属性名`。但是读取元素的 `class` 属性的时候不能直接 `元素.class` 因为 class 是 JS 中的保留字，应该写为 `元素.className`

{%asset_img 查找子节点.png%}
但是 `childNodes` 有个缺陷，此时如果我们使用 `children` 就不会出现这种问题了，它返回的是当前元素的所有子元素。
{%asset_img childnodes缺陷.png%}

`innerText` 和 `innerHTML` 类似，但是 `innerText` 获取的会将 html 标签去除。

{%asset_img 获取兄弟节点.png%}

`getElementsByName()` 一般用来操作一些表单项目。 

获取 `body` 标签的话有两种方式：
1. `var body = document.getElementsByTagName()[0];` 因为 `getElementsByTagName()` 返回的是一个集合 `Collection`，但是我们又只有一个 `body`，所以直接返回索引 0 就可以了。
2. 其实在 `document` 中就有一个属性 `body`，我们直接 `var body = document.body;` 就可以了。

`html` 元素是 `document.documentElement;`

`document.all` 代表的是页面的所有元素。也可以写成 `document.getElementsByTagName("*")`

`document.getElementsByClassName();` 可以根据元素的 `class` 属性值获取一组节点对象。

`document.querySelector();` 需要一个选择器字符串作为参数，可以根据一个 CSS 选择器来查询一个元素节点对象。但是使用这个方法只会返回唯一的一个元素，如果满足条件的元素有多个，但是只会返回第一个。如果需要多个就使用 `document.querySelectorAll();`

`父节点.insertBefore(新节点, 旧节点)` 是在旧节点前面添加新节点。

超链接点击以后会默认跳转页面，如果我们不希望出现此默认行为，我们可以在超链接的 `onclick = function() {}` 中写上 `return false;`

`confirm()` 函数会弹出一个带有确定和取消两个按键的提示框，并且如果我们点击确定，会返回 true，如果点击取消，会返回 false。

{%asset_img 执行顺序.png%}
一个比较细节容易忽视的点，直观上我们认为 this 和 allA[i] 是一样的。
图中，我们的 `onclick = function() {}` 可以认为只是函数之间的一个赋值，里面的内容并没有执行。只有我们在点击按钮的时候，`function` 里面的内容才会执行。如果我们 `function` 里面使用 `allA[i]`，等到我们点击的时候 for 循环早就已经执行完毕，此时的 i 必然是 all 的length，所以就会出现错误。我们正确的做法应该是将 function 里面的 allA[i] 改为 this。

通过 JS 修改元素的样式：`元素.style.样式名 = 样式值` 其中样式值需要是一个字符串。
注意，如果 CSS 样式名称中含有 `-`，如 `background-color` 这种命名在 JS 中是不合法的，我们需要将这种命名改为驼峰命名法，去掉 `-`，然后将 `-` 的字母大写。

通过 JS 的 style 修改的往往是内联样式，而内联样式有较高的优先级，所以通过 JS 修改的样式往往会立即显示。

事件对象：
当事件的响应函数被触发的时候，浏览器每次会将一个事件对象作为实参传递进响应函数。在事件对象中封装了当前关于事件的一切信息，比如鼠标的坐标、键盘的哪一个按键被按下、鼠标滚轮的移动方向

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>
            this is a title.
        </title>
        <script>
            window.onload = function() {
                var box1 = document.getElementById("box1");
                document.onmousemove = function(event) {
                    var clientX = event.clientX;
                    var clientY = event.clientY;
                    box1.style.left = clientX + "px";
                    box1.style.top = clientY + "px";
                }
            }
        </script>
    </head>
    <body>
        <style>
            #box1 {
                width: 100px;
                height: 100px;
                background-color: red;
                position: absolute;
            }
        </style>
        <box id="box1"></box>
    </body>
</html>
```
`clientX` 和 `clientY` 是用于我们鼠标在当前可见窗口的坐标，所以对于有滚动条的窗口的话可能会出现一些错误。所以我们这时候使用 `pageX` 和 `pageY` 这两和属性是相对于整个页面的。

{%asset_img document和window.png%}

事件的冒泡(bubble)
所谓事件的冒泡就是事件的想上传导，当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发。在开发中，大部分情况冒泡是有用的，如果不希望发生事件冒泡可以通过事件对象来取消冒泡。
`event.cancelBubble = true;`

我们希望只绑定一次事件，即可应用到多个元素之上，即使元素是后来添加的。我们可以尝试将元素绑定给其共同的祖先元素。然后通过冒泡来实现事件的发生。这其实就是事件的「委派」。

`document.getElementsByTagName();` 返回的不是一个数组（一个NodeList对象，指定标签名的集合 collection），虽然我们可以遍历，它也有长度。

点击超链接时会自动默认跳转，我们把超链接的 `href` 修改为 `javascript:;` 就不会发生跳转了。

事件给谁绑定的，function 中的 this 就是谁。
```
 ul.onclick = function() {
    alert(this);
    alert("我是一个响应函数。");
}
```
像这一个，第一个 `alert` 输出的就是 `[object HTMLUListElement]`。
但是事件绑定对象不等于事件触发对象，我们如果想要获得事件**触发对象**需要使用 `event.target` 属性。
```
<!DOCTYPE html>
<html>
    <title>
        <meta charset="UTF-8">
        <title>this is a test.</title>
    </title>
    <body>
        <script>
            window.onload = function() {
                var btn1 = document.getElementById("btn1");
                var ul = document.getElementsByTagName("ul")[0];
                btn1.onclick = function() {
                    var li = document.createElement("li");
                    li.innerHTML = "<a href='javascript:;' class='link'>新建的超链接</a>"
                    ul.appendChild(li);
                }
                ul.onclick = function(event) {
                    if (event.target.className == 'link') {
                        alert("这是一个响应函数");
                    }
                }
            }
        </script>
        <button id="btn1">我是一个按钮</button>
        <ul>
            <li><a href="javascript:;" class="link">这是一个超链接</a></li>
            <li><a href="javascript:;" class="link">这是一个超链接</a></li>
            <li><a href="javascript:;" class="link">这是一个超链接</a></li>
        </ul>
    </body>
</html>
```

使用 `对象.事件 = 函数` 的形式绑定响应函数，它只能同时为一个事件绑定一个响应函数，不能绑定多个，如果绑定了多个，那么后面的就会覆盖掉前面的。
我们可以使用 `addEventListener(xxx, xxx, xxx)` 为元素绑定响应函数。
它的参数：
1. 事件的字符串，如果是 onclick 不要前面的 on
2. 回调函数，当事件被触发时，该函数会被调用。
3. 是否在捕获阶段触发，需要布尔值，一般是 false
   
JavaScript中的call()函数是用于调用函数的方法之一，它允许你显式地指定函数内部的this关键字，并传递参数给该函数。call()方法的语法如下：
```
functionName.call(thisArg, arg1, arg2, ...);
```
总之，call()方法是JavaScript中用于在指定上下文对象上调用函数的强大工具，它允许你更灵活地控制函数的执行环境。

```
<!DOCTYPE html>
<html>
    <title>
        <meta charset="UFT-8">
        this is a test.
    </title>
    <body>
        <style>
            #box1 {
                width: 100px;
                height: 100px;
                background-color: red;
                position: absolute;
            }
        </style>
        <script>
            window.onload = function() {
                var box1 = document.getElementById("box1");
                box1.onmousedown = function(event) {
                    var offsetX = event.clientX - box1.offsetLeft;
                    var offsetY = event.clientY - box1.offsetTop;
                    document.onmousemove = function(event) {
                        var x = event.clientX;
                        var y = event.clientY;
                        box1.style.left = x - offsetX + "px";
                        box1.style.top = y - offsetY + "px";
                    }
                    document.onmouseup = function() {
                        document.onmousemove = null;
                        document.onmouseup = null;
                    }
                }
            }
        </script>
        <div id="box1"></div>
    </body>
</html>
```
实现一个小方块位置的拖拽。

键盘事件一般都会绑定给可以获取到焦点的对象或者是 `document` 对象。对于 `onkeydown` 事件来说，如果我们一直按着某个按键不松手，则事件就会一直触发。当 `onkeydown` 连续触发时，第一次和第二次之间的间隔会长一点，其他后面的会非常快，这是为了防止我们误操作。

我们可以使用 `event` 的 `keyCode` 属性可以返回被按下键的 `Unicode` 编码。或者使用 `key` 属性直接返回被按键的按键。
如果判断 `alt` 或者 `ctrl` 或者 `shift` 和某个键是否同时被按下，可以同时使用 `event` 的 `altKey、shiftKey、ctrlKey` 属性和 `key` 属性。

BOM browser object model 浏览器对象模型
BOM 可以使我们通过 JS 来操作浏览器，DOM 可以使我们通过 JS 来操作网页。
{%asset_img bom对象.png%}

`uerAgent` 用户代理，通常指的是浏览器，其中 `navigator` 的属性 `userAgent` 是一个字符串，包含用来描述浏览器的内容，不同的浏览器有着不同的 userAgent

Gecko CSS 渲染的一个引擎。

`history` 对象 `length` 属性，返回浏览器历史列表中 url 数量。
方法：`back` 加载 `history` 列表中前一个 url，`forward` 加载 `history` 列表中下一个 url，`go(xx)` 加载列表中某一个具体的页面，xx 如果是正，就是前多少个，如果是负，就是加载后面第xx个页面。

`location` 对象
如果直接打印 `location` 可以获取当前的地址栏，也就是网页的完整路径。如果直接将 `location` 修改为一个路径，就会直接跳转到那个页面。

`window` 的 `setInterval` 方法。(Interval 是 间隔、中场休息、幕间休息、间隙 的意思)
- 定时调用
- 可以将一个函数，每隔一段时间执行一次
- 参数：
    1. 回调函数
    2. 每次调用的时间间隔，单位是毫秒
- 返回值：
    返回一个 Number 类型的数据
    这个数字用来作为定时器的唯一标识(因为一个页面上可能有很多个定时器)
    比如我们的 `clearInterval(xx)` 方法，可以用来关闭一个定时器，其中的 `xx` 就需要我们的标识作为参数。  
```
setInterval(function() {
    xxx.innerHTML = ++count;
}, 1000);
```

延时调用：一个函数不是马上执行，而是一段时间之后再执行(只会执行一次)。
用法和定时调用差不多 `setTimeout(xxx);`
`clearTimeout(xxx);` 是关闭延时调用。

延时调用其实和定时调用是可以互相代替的。

JSON(JavaScript Object Notation)
因为和 JavaScript 中对象的表示方法一样，只不过在 JSON 中属性名字必须加双引号。
JSON 分类：
1. 对象 `{}`
2. 数组 `[]`

在 JS 中，为我们提供了一个工具类就叫做 JSON，这个对象可以帮助我们将一个 JSON 转换为 JS 对象，也可以将一个 JS 对象转换为 JSON。
`JSON.parse(xx);`
- 将字符串转换为 JS 对象
- 需要一个 JSON 字符串作为参数，返回一个 JS 对象

`JSON.stringfy();`
- 将 JS 对象转换为字符串
- 需要一个 JS 对象作为参数，但会一个 JSON 字符串。

`===` 是严格相等的意思，它用于比较两个值是否完全相等，包括值和数据类型。
使用严格相等运算符是 JavaScript 编程中的一种良好实践，因为它可以减少潜在的错误和不确定性，确保比较的值具有相同的类型和值。

