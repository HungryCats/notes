# <font color="Red">CSS</font>

<!-- more -->

## <font color="Pink">First</font>

<br>

### <font color="#A9D0D9">CSS 体验</font>

> 层叠样式表 (Cascading Style Sheets，缩写为 CSS)，是一种 样式表 语言，用来描述 HTML 文档的呈现（美化内容）。

> 书写位置：title 标签下方添加 style 双标签，style 标签里面书写 CSS 代码。

> 提示：属性名和属性值成对出现 → 键值对。

```HTML
<title>CSS 初体验</title>
<style>
/* 选择器 { } */
p {
/* CSS 属性 */
color: red;
}
</style>
<p>体验 CSS</p>
```

<br>

### <font color="#A9D0D9">CSS 引入方式</font>

1. 内部样式表：学习使用
   
   - CSS 代码写在 style 标签里面

2. 外部样式表：开发使用
   
   - CSS 代码写在单独的 CSS 文件中（.css）
   
   - 在 HTML 使用 link 标签引入

```HTML
<link rel="stylesheet" href="#">
```

3. 行内样式：配合 JavaScript 使用
   
   - CSS 写在标签的 style 属性值里

```HTML
<div style="color: red; font-size:20px;">行内样式</div>
```

### <font color="#A9D0D9">选择器</font>

<br>

> 作用：查找标签，设置样式。

<br>

#### <font color="#2A878F">标签选择器</font>

标签选择器：使用标签名作为选择器 → 选中同名标签设置相同的样式。

例如：p, h1, div, a, img......

```HTML
<style>
p {
color: red;
}
</style>
```

> 注意：标签选择器无法差异化同名标签的显示效果。

<br>

#### <font color="#2A878F">类选择器</font>

作用：查找标签，差异化设置标签的显示效果。

步骤：

- 定义类选择器 → .类名

- 使用类选择器 → 标签添加 class="类名"

```HTML
<style>
/* 定义类选择器 */
.red {
color: red;
}
</style>
<!-- 使用类选择器 -->
<div class="red">类选择器/div>
<div class="red size">类选择器</div>
```

注意：

- 类名自定义，不要用纯数字或中文，尽量用英文命名

- 一个类选择器可以供多个标签使用

- 一个标签可以使用多个类名，类名之间用空格隔开

> 开发习惯：类名见名知意，多个单词可以用 - 连接，例如：news-hd。

<br>

#### <font color="#2A878F">id 选择器</font>

作用：查找标签，差异化设置标签的显示效果

场景：id 选择器一般配合 JavaScript 使用，很少用来设置 CSS 样式

步骤：

- 定义 id 选择器 → #id 名

- 使用 id 选择器 → 标签添加 id = "id 名"

规则：

- 同一个 id 选择器在一个页面只能使用一次

```HTML
<style>
/* 定义 id 选择器 */
#red {
color: red;
}
</style>
<!-- 使用 id 选择器 -->
<div id="red">id选择器</div>
```

样式：

<style>
/* 定义 id 选择器 */
#red {
color: red;
}
</style>

<!-- 使用 id 选择器 -->

<div id="red">id选择器</div>

<br>

#### <font color="#2A878F">通配符选择器</font>

作用：查找页面所有标签，设置相同样式。

通配符选择器：\*,不需要调用，浏览器自动查找页面所有标签，设置相同的样式

> 经验：通配符选择器可以用于清除标签的默认样式，例如：标签默认的外边距、内边距

```HTML
<style>
* {
    margin:0;
    padding:0;
}
</style>
```

### <font color="#A9D0D9">画盒子</font>

属性：
width → 宽度

height → 高度

background-color → 背景颜色

```HTML
<style>
    .red {
        width:100px;
        height:100px;
        background-color:brown;
    }
    .orange {
        width:200px;
        height:200px;
        background-color:orange;
    }
</style>
<div class="red">cats</div>
<div class="orange">dogs</div>
```

样式：

<style>
    .red {
        width:100px;
        height:100px;
        background-color:brown;
    }
    .orange {
        width:200px;
        height:200px;
        background-color:orange;
    }
</style>

<div class="red">cats</div>
<div class="orange">dogs</div>

<br>

### <font color="#A9D0D9">文字控制属性</font>

#### <font color="#2A878F">字体大小</font>

- 属性名：font-size
- 属性值：文字尺寸，PC 端网页最常用的单位 px
- 注意一定要带单位，否则属性不生效

```HTML
<style>
p {
font-size: 30px;
}
</style>
```

<br>

#### <font color="#2A878F">字体粗细</font>

- 属性名：font-weight

- 属性值：

- 数字：

- > 正常：400

- > 加粗：700

- 关键字：

- > 正常：normal

- > 加粗：bold

```HTML
<style>
    h3 {
        font-weight:400;
    }
    div {
        font-weight:700;
    }
</style>
<h3>标题文字默认加粗</h3>
<div>div标签</div>
```

<br>

#### <font color="#2A878F">文字样式(是否倾斜)</font>

作用：清除文字默认的倾斜效果

属性名：font-style

属性值：

- 正常(不倾斜)：normal
- 倾斜：italic

```HTML
<style>
    em {
        font-style:normal;
    }
    div {
        font-style:italic;
    }
</style>
<em>em标签默认倾斜</em>
<div>div标签</div>
```

样式：

<style>
    .bqx {
        font-style:normal;
    }
    .qx {
        font-style:italic;
    }
</style>

<em class="bqx">em标签默认倾斜</em>

<div class="qx">div标签</div>

<br>

### <font color="#A9D0D9">行高</font>

作用：设置多行文本的间距

属性名：line-height

属性值：

- 数字 + px
- 数字（当前标签 font-size 属性值的倍数）

```HTML
<style>
    p {
    line-height: 30px;
    /* 当前标签字体大小为16px */
    line-height: 2;
    }
</style>
<p>文字</p>
```

> 行高的测量方法：从一行文字的最顶端（最底端）量到下一行文字的最顶端（最底端）。

行高-单行文字垂直居中

垂直居中技巧：行高属性值等于盒子高度属性值

注意：该技巧适用于单行文字垂直居中效果

```HTML
<style>
div {
height: 100px;
background-color: skyblue;
/* 注意：只能是单行文字垂直居中 */
line-height: 100px;
}
</style>
<div>文字</div>
```

样式：

<style>
.hg {
height: 100px;
background-color: skyblue;
/* 注意：只能是单行文字垂直居中 */
line-height: 100px;
}
</style>

<div class="hg">文字</div>

<br>

### <font color="#A9D0D9">字体族</font>

属性名：font-family
属性值：字体名

```HTML
<style>
    div {
        font-family:楷体;
    }
</style>
<div>楷体文字</div>
```

样式：

<style>
    .kaiti {
        font-family:楷体;
    }
</style>

<div class="kaiti">楷体文字</div>

<br>

> 拓展（了解）：font-family属性值可以书写多个字体名，各个字体名用逗号隔开，执行顺序是从左向右依次查找
> 
> font-family 属性最后设置一个字体族名，网页开发建议使用无衬线字体

```HTML
font-family: Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53", sans-serif;
```

<br>

### <font color="#A9D0D9">font复合属性</font>

> 使用场景：设置网页文字公共样式

复合属性：属性的简写方式，一个属性对应多个值的写法，各个属性值之间用空格隔开。

font: 是否倾斜 是否加粗 字号/行高 字体（必须按顺序书写）

```HTML
<style>
    div {
        font: italic 700 30px/2 楷体;
    }
</style>
```

样式：

<style>
    .fuhe {
        font: italic 700 30px/2 楷体;
    }
</style>

<div class="fuhe">font复合属性</div>

<br>

> 注意：字号和字体值必须书写，否则 font 属性不生效

<br>

### <font color="#A9D0D9">文本修饰属性</font>

#### <font color="#2A878F">文本缩进</font>

属性名：text-indent

属性值：

- 数字 + px
- 数字 + em (推荐：1em = 当前标签的自豪大小)

```HTML
<style>
    .shsj {
        text-indent:2em;
        font-size:30px;
    }
</style>
<p class="shsj">层叠样式表（Cascading Style Sheets，缩写为 CSS）是一种样式表语言，用来描述 HTML 或 XML（包括如 SVG、MathML 或 XHTML 之类的 XML 分支语言）文档的呈现。CSS 描述了在屏幕、纸质、音频等其他媒体上的元素应该如何被渲染的问题。</p>
```

<style>
    .shsj {
        text-indent:2em;
    }
</style>

<p class="shsj">层叠样式表（Cascading Style Sheets，缩写为 CSS）是一种样式表语言，用来描述 HTML 或 XML（包括如 SVG、MathML 或 XHTML 之类的 XML 分支语言）文档的呈现。CSS 描述了在屏幕、纸质、音频等其他媒体上的元素应该如何被渲染的问题。</p>

#### <font color="#2A878F">文本对齐</font>

> 作用：控制内容水平对齐方式

属性名：text-align

属性值：
left -> 左对齐(默认)

center -> 居中对齐

right -> 右对齐

```HTML
<style>
    h1 {
        text-align:center;
    }
</style>
<h1>居中</h1>
```

<br>

水平对齐方式-图片

> text-align本质是控制内容的对齐方式，属性要设置给内容的父级。

```HTML
<style>
    div {
        text-align: center;
    }
</style>
<div>
    <img src="./images/1.jpg" alt="">
</div>
```

#### <font color="#2A878F">修饰线</font>

属性名：text-decoration

属性值：

none -> 无

underline -> 下划线

line-through -> 删除线

overline -> 上划线

```HTML
<style>
    a {
        text-decoration:none;
    }
    div {
        text-decoration:underline;
    }
    p {
        text-decoration:line-through;
    }
    span {
        text-decoration:overline;
    }
</style>
<a href="#">去掉下划线</a>
<div>添加下划线</div>
<p>添加删除线</p>
<span>添加上划线</span>
```

样式：

<style>
    .qdxhx {
        text-decoration:none;
    }
    .tjxhx {
        text-decoration:underline;
    }
    .tjscx {
        text-decoration:line-through;
    }
    .tjshx {
        text-decoration:overline;
    }
</style>

<a href="#" class="qdxhx">去掉下划线</a>

<div class="tjxhx">添加下划线</div>
<p class="tjscx">添加删除线</p>
<span class="tjshx">添加上划线</span>

<br>

### <font color="#A9D0D9">文字颜色</font>

属性值：color

属性值：

颜色关键字 -> 颜色英文单词 -> red,green,blue...

rgb表示法 -> rgb(r,g,b) -> r,g,b表示红绿蓝三原色,取值：0-255

rgba表示法 -> rgba(r,g,b,a) -> a表示透明度,取值：0-1

十六进制表示法 -> #RRGGBB -> #000000,#ffcc00,简写：#000,#fc0

<br>

---

<br>

## <font color="Pink">Second</font>

### <font color="#A9D0D9">选择器</font>

#### <font color="#2A878F">复合选择器</font>

定义：由两个或多个基础选择器，通过不同的方式组合而成。

作用：更准确、更高效的选择目标元素（标签）。

#### <font color="#2A878F">后代选择器</font>

后代选择器：选中某元素的后代元素。

选择器写法：父选择器 子选择器 { CSS 属性}，父子选择器之间用空格隔开。

```HTML
<style>
    div span {
        color: red;
    }
</style>
<span> span 标签</span>
<div>
    <span>这是 div 的儿子 span</span >
</div>
```

<br>

#### <font color="#2A878F">子代选择器</font>

子代选择器：选中某元素的子代元素（最近的子级）。

选择器写法：父选择器 > 子选择器 { CSS 属性}，父子选择器之间用 > 隔开。

```HTML
<style>
    div > span {
        color: red;
    }
</style>
<div>
    <span>这是 div 里面的 span</span>
    <p>
        <span>这是 div 里面的 p 里面的 span</span>
    </p>
</div>
```

<br>

#### <font color="#2A878F">并集选择器</font>

并集选择器：选中多组标签设置相同的样式。

选择器写法：选择器1, 选择器2, …, 选择器N { CSS 属性}，选择器之间用 , 隔开。

```html
<style>
    div,
    p,
    span {
        color: red;
    }
</style>
<div> div 标签</div>
<p>p 标签</p>
<span>span 标签</span>
```

#### <font color="#2A878F">交集选择器</font>

交集选择器：选中同时满足多个条件的元素。

选择器写法：选择器1选择器2 { CSS 属性}，选择器之间连写，没有任何符号。

```html
<style>
    p.box {
        color: red;
    }
</style>
<p class="box">p 标签，使用了类选择器 box</p>
<p>p 标签</p>
<div class="box">div 标签，使用了类选择器 box</div>
```

> 注意：如果交集选择器中有标签选择器，标签选择器必须书写在最前面。

<br>

#### <font color="#2A878F">伪类选择器</font>

伪类选择器：伪类表示元素状态，选中元素的某个状态设置样式。

鼠标悬停状态：选择器:hover { CSS 属性 }

```html
<style>
    a:hover {
        color: red;
    }
    .box:hover {
        color: green;
    }
</style>
<a href="#">a 标签</a>
<div class="box">div 标签</div>
```

样式：

<style>
    .ahover:hover {
        color: red;
    }
    .boxx:hover {
        color: green;
    }
</style>

<a href="#" class="ahover">a 标签</a>

<div class="boxx">div 标签</div>

<br>

#### <font color="#2A878F">超链接伪类</font>

超链接一共四个状态

:link -> 访问前

:visited -> 访问后

:hover -> 鼠标悬停

:active -> 点击时(激活)

> 提示：如果要给超链接设置以上四个状态，需要按 LVHA 的顺序书写。

> 经验：工作中，一个 a 标签选择器设置超链接的样式， hover状态特殊设置

<br>

### <font color="#A9D0D9">CSS三大特性</font>

CSS特性：化简代码 / 定位问题，并解决问题

> 继承性
> 
> 层叠性
> 
> 优先级

#### <font color="#2A878F">继承性</font>

继承性：子级标签默认继承父级标签的文字控制属性

```html
<style>
    body {
        font-size:30px;
        color:red;
        font-weight:700;
    }
</style>
<body>
    <div>div</div>
    <p>p</p>
    <span>span</span>
</body>
```

> 注意：如果标签有默认文字样式会继承失败。 例如：a 标签的颜色、标题的字体大小。

<br>

#### <font color="#2A878F">层叠性</font>

特点：

- 相同的属性会覆盖：后面的css属性覆盖前面的css属性

- 不同的属性会叠加：不同的属性都生效

```html
<style>
    div {
        color: red;
        font-weight: 700;
    }
    div {
        color: green;
        font-size: 30px;
    }
</style>
<div>div 标签</div>
```

样式：

<style>
    .first {
        color: red;
        font-weight: 700;
    }
    .first {
        color: green;
        font-size: 30px;
    }
</style>

<div class="first">div 标签</div>

<br>

> 注意：选择器类型相同则遵循层叠性，否则按选择器优先级判断。

<br>

#### <font color="#2A878F">选择器的优先级</font>

优先级：也叫权重,当一个标签使用了多种选择器时,基于不同种类的选择器的匹配规则。

规则：选择器优先级高的样式生效

公式： 通配符选择器 < 标签选择器 < 类选择器 < id选择器 < 行内样式 < !important

> 选中的标签范围越大,优先级越低

```html
<style>
    * {
        color:red !important;
    }
    div {
        color:green;
    }
    .yxj {
        color:blue;
    }
    #text {
        color:orange;
    }
</style>
<body>
    <div class="yxj" id="text" style="color:purple">div标签</div>
</body>
```

> !important 提权 -> 将权重(优先级)提到最高  谨慎使用！！！

<br>

优先级-叠加计算规则

叠加计算：如果是复合选择器,则需要权重叠加计算

公式：(每一级之间不存在进位)

(行内样式  id选择器个数  类选择器个数  标签选择器个数)

<br>

规则：

从左向右依次比较选个数，同一级个数多的优先级高，如果个数相同，则向后比较

!important 权重最高

继承权重最低

<br>

练习题一:

```html
<style>
    /* (行内样式  id选择器个数  类选择器个数  标签选择器个数) */
    /* 0，0，2，1 */
    .ci .c2 .div {
        color:blue;
    }
    /* 0，1，0，1 */
    div #box3 {
        color:green;
    }
    /* 0,1,1,0 */
    #box1 .c3 {
        color:orange;
    }
</style>
<div id="box1" class="c1">
    <div id="box2" class="c2">
        <div id="box3" class="c3">
            饿死的冏猫
        </div>
    </div>
</div>
```

答案：orange

<br>

练习题二:

```html
<style>
    /* (行内样式  id选择器个数  类选择器个数  标签选择器个数) */
    /* 0,2,0,0 */
    #father #son {
        color:blue;
    }
    /* 0,,1,1,1 */
    #father p.c2 {
        color:black;
    }
    /* 0,0,2,2 */
    div.c1 p.c2 {
        color:red;
    }
    /* 继承 */
    #father {
        color:green !important;
    }
    /* 继承 */
    div#father.c1 {
        color:yellow;
    }
</style>
<div id="father" class="c1">
    <p id="son" class="c2">
        饿死的冏猫
    </p>
</div>
```

答案: blue

<br>

### <font color="#A9D0D9">背景属性-拆分写法</font>

> 背景色 -> background-color
> 
> 背景图 -> background-image
> 
> 背景图平铺方式 -> background-repeat
> 
> 背景图位置 -> background-position
> 
> 背景图缩放 -> background-size
> 
> 背景图固定 -> background-attachment

<br>

#### <font color="#2A878F">背景图</font>

属性:

background-image

网页中，使用背景图实现装饰性的图片效果。

属性名：background-image（bgi）

属性值：url(背景图 URL)

```html
<style>
div {
width: 400px;
height: 400px;
background-image: url();
}
</style>
<div>div 标签</div>
```

> 提示：背景图默认有平铺（复制）效果。

<br>

#### <font color="#2A878F">背景图平铺方式</font>

属性:

background-repeat

属性值:

no-repeat -> 不平铺

repeat -> 平铺(默认)

repeat-x -> 水平方向平铺

repeat-y -> 垂直方向平铺

```html
<style>
    div {
        width: 400px;
        height: 400px;
        background-color: pink;
        background-image: url(./images/1.png);
        /* 不平铺:盒子左上角显示背景图 */
        background-repeat: no-repeat;
    }
</style>
<div>div 标签</div>
```

<br>

#### <font color="#2A878F">背景图位置</font>

属性:

background-position

属性值:水平方向位置 垂直方向位置

- 关键字
  
    left -> 左侧
  
    right -> 右侧
  
    center -> 居中
  
    top -> 顶部
  
    bottom -> 底部

- 坐标
  
    数字 + px,正负都可以
  
    水平：正数向右；负数向左
  
    垂直：正数向下；负数向上

```html
<style>
    div {
        width: 400px;
        height: 400px;
        background-color: pink;
        background-image: url(./images/1.png);
        background-repeat: no-repeat;

        /* 左上角 默认值*/
        background-position:0 0;
        background-position:left top;

        /* 水平: 正数向右,负数向左 */
        background-position:right bottom;
        background-position:50px 0;
        background-position:-50px 0;

        /* 垂直: 正数向下,负数向上*/
        background-position:0 100px;
        background-position:0 -100px;

        /* 数字和单词混用 */
        background-position:50px center;

        /* 关键字写一个,另一个方向居中 */
        background-position:bottom;
    }
</style>
<div>div 标签</div>
```

提示：

> 关键字取值方式写法，可以颠倒取值顺序
> 
> 可以只写一个关键字，另一个方向默认为居中；数字只写一个值表示水平方向，垂直方向为居中

<br>

#### <font color="#2A878F">背景图缩放</font>

作用:设置背景图大小

属性名:

background-size

常用属性值:

- 关键字

- cover -> 等比例缩放背景图片以完全覆盖背景区，可能背景图片部分看不见

- contain -> 等比例缩放背景图片以完全装入背景区，可能背景区部分空白

<br>

- 百分比
- 根据盒子尺寸计算图片大小

<br>

- 数字 + 单位（例如：px） 一般不用

```html
<style>
    div {
        width: 500px;
        height: 400px;
        background-color: pink;
        background-image: url(./images/1.png);
        background-repeat: no-repeat;

        /* cover:图片完全覆盖盒子,可能导致图片显示不全 */
        background-size: cover;
        /* contain:如果图的宽高跟盒子尺寸相等停止缩放,可能导致盒子有露白 */
        background-size: contain;
        /* 图片宽度跟盒子宽度一致,图片的高度按照图片比例等比缩放 */
        background-size: 100%;
    }
</style>
```

<br>

#### <font color="#2A878F">背景图固定</font>

> 作用：背景不会随着元素的内容滚动。

background-attachment

属性值：

fixed

```html
<style>
    body {
        background-image: url(./images/bg.jpg);
        background-repeat: no-repeat;
        background-position:center top;
        background-attachment: fixed;
    }
</style>
```

<br>

### <font color="#A9D0D9">背景属性-复合写法</font>

属性名：background

属性值：背景色 背景图 背景图平铺方式 背景图位置/背景图缩放 背景图固定（空格隔开各个属性值，不区分顺序）

```html
<style>
    div {
        width: 400px;
        height: 400px;
        /* 倘若背景图的比例跟盒子的宽高比例一样不管是哪一种缩放都一样 */
        background: pink url(./images/1.png) no-repeat center bottom/cover;
    }
</style>
<div></div>
```

<br>

### <font color="#A9D0D9">显示模式</font>

> 显示模式：标签（元素）的显示方式。
> 
> 作用：布局网页的时候，根据标签的显示模式选择合适的标签摆放内容。

#### <font color="#2A878F">块级元素</font>

特点：

- 独占一行

- 宽度默认是父级的100%

- 添加宽高属性生效

<br>

#### <font color="#2A878F">行内元素</font>

特点：

- 一行可以显示多个

- 设置宽高属性不生效

- 宽高尺寸由内容撑开

<br>

#### <font color="#2A878F">行内块元素</font>

特点：

- 一行可以显示多个

- 设置宽高属性生效

- 宽高尺寸也可以由内容撑开

```html
<style>
    /* 独占一行;添加宽高属性生效 */
    div {
        width:100px;
        height:100px;
    }
    .div1 {
        background-color:brown;
    }
    .div2 {
        background-color:orange;
    }
    /* 行内:一行共存多个;尺寸由内容撑开;加宽高不生效 */
    span {
        width:200px;
        height:200px;
    }
    /* 行内块:一行共存多个;尺寸由内容撑开;加宽高生效 */
    img {
        width:200px;
        height:200px;
    }
</style>
<body>
    <!-- 块元素 -->
    <div class="div1">div 标签1</div>
    <div class="div2">div 标签2</div>

    <!-- 行内元素 -->
    <span>span1</span>
    <span>span2</span>

    <!-- 行内块元素 -->
    <img src="#" alt="">
    <img src="#" alt="">
</body>
```

<br>

#### <font color="#2A878F">转换显示模式</font>

<br>

属性：display

属性值:

block -> 块级

inline-block -> 行内块

inline -> 行内

```html
<style>
    /* 块级：独占一行；宽度默认是父级的100%；加宽高生效 */
    div {
      width: 100px;
      height: 100px;

      /* display: inline-block; */

      display: inline;
    }

    .div1 {
      background-color: brown;
    }

    .div2 {
      background-color: orange;
    }

    /* 行内：一行共存多个；尺寸由内容撑开；加宽高 不 生效 */
    span {
      width: 200px;
      height: 200px;

      /* display: block; */
      display: inline-block;
    }

    .span1 {
      background-color: brown;
    }

    .span2 {
      background-color: orange;
    }

    /* 行内块：一行共存多个；默认尺寸由内容撑开；加宽高生效 */
    img {
      width: 100px;
      height: 100px;

      display: block;
    }
</style>
</head>
<body>
  <!-- 块元素 -->
  <div class="div1">div 标签1</div>
  <div class="div2">div 标签2</div>

  <!-- 行内元素 -->
  <span class="span1">span11111111</span>
  <span class="span2">span1</span>

  <!-- 行内块元素 -->
  <img src="./images/1.png" alt="">
  <img src="./images/1.png" alt="">

</body>
```

<br>

---

<br>

## <font color="Pink">Third</font>

### <font color="#A9D0D9">选择器</font>

#### <font color="#2A878F">结构伪类选择器</font>

> 作用：根据元素的结构关系查找元素。

E:first-child -> 查找第一个E元素

E:last-child -> 查找最后一个E元素

E:nth-child(N) -> 查找第N个E元素(第一个元素N值为1)

<br>

```html
<style>
    li:first-child {
        background-color:green;
    }
    li:last-child {
        background-color:red;
    }
    li:nth-child(3) {
        background-color:blue;
    }
</style>
<body>
    <li>li 1</li>
    <li>li 2</li>
    <li>li 3</li>
    <li>li 4</li>
</body>
```

:nth-child(公式)

> 作用:根据元素的结构关系查找多个元素
> 
> 提示：公式中的n取值从 0 开始。

<br>

偶数标签 -> 2n

奇数标签 -> 2n + 1; 2n - 1

<br>

(5可以是任意的数字)

找到5的倍数的标签 -> 5n 

找到第5个以后的标签 -> n + 5

找到第5个以前的标签 -> -n + 5

```html
<style>
    li:nth-child(2n) {
        background-color:blue;
    }
    li:nth-child(2n + 1) {
        background-color:blue;
    }
    li:nth-child(5n) {
        background-color:blue;
    }
    li:nth-child(n + 5) {
        background-color:blue;
    }
    li:nth-child(-n + 5) {
        background-color:blue;
    }
</style>
<body>
    <li>li 1</li>
    <li>li 2</li>
    <li>li 3</li>
    <li>li 4</li>
    <li>li 5</li>
    <li>li 6</li>
    <li>li 7</li>
    <li>li 8</li>
    <li>li 9</li>
    <li>li 10</li>
</body>
```

#### <font color="#2A878F">伪元素选择器</font>

> 作用：创建虚拟元素（伪元素），用来摆放装饰性的内容。

E::before -> 在E元素里面**最前面**添加一个伪元素
E::after -> 在E元素里面**最后面**添加一个伪元素

<br>

注意点：

- 必须设置 content: ""属性，用来 设置伪元素的内容，如果没有内容，则引号留空即可

- 伪元素默认是行内显示模式

- 权重和标签选择器相同

```html
<style>
    div {
        width:300px;
        height:300px;
        background-color:pink;
    }
    div::before {
        /* content:可以为空但必须有 */
        content: "老鼠";
        width:100px;
        height:100px;
        background-color:brown;
        /* 转为块级 */
        display:block;
    }
    div::after {
        /* content:可以为空但必须有 */
        content: "大米";
        width:100px;
        height:100px;
        background-color:orange;
        /* 转为行内块 */
        display:inline-block;
    }
</style>
<div>爱</div>
```

<br>

### <font color="#A9D0D9">盒子模型</font>

<br>

> 作用：布局网页，摆放盒子和内容。

<br>

#### <font color="#2A878F">盒子模型-组成</font>

- 内容区域 – width & height

- 内边距 – padding（出现在内容与盒子边缘之间）

- 边框线 – border

- 外边距 – margin（出现在盒子外面）

```html
<style>
div {
    width: 200px;
    height: 200px;
    background-color: pink;
    border: 5px solid brown;
    /* 内容与盒子边缘之间 */
    padding: 20px;
    /* 出现在盒子外面，拉开两个盒子之间的距离 */
    margin: 50px;
}
</style>
<div>div</div>
```

<br>

#### <font color="#2A878F">盒子模型-边框线</font>

四个方向

属性名：border

属性值：边框线粗细 线条样式 颜色（不区分顺序）

> solid -> 实线
> 
> dashed -> 虚线
> 
> dotted -> 点线

#### <font color="#2A878F">单方向边框线</font>

属性名：border-方位名词

属性值：边框线粗细 线条样式 颜色（不区分顺序）

```html
<style>
div {
    width: 100px;
    height: 100px;
    background-color: pink;

    border-top: 2px solid red;
    border-right: 3px dashed green;
    border-bottom: 4px dotted blue;
    border-left: 5px solid orange;
}
</style>
<div></div>
```

样式：

<style>
.dfxbkx {
    width: 100px;
    height: 100px;
    background-color: pink;

    border-top: 2px solid red;
    border-right: 3px dashed green;
    border-bottom: 4px dotted blue;
    border-left: 5px solid orange;
}
</style>

<div class="dfxbkx"></div>

<br>

#### <font color="#2A878F">盒子模型-内边距</font>

> 作用：设置 内容 与 盒子边缘 之间的距离。

属性名：padding / padding-方位名词

```html
<style>
div {
    width: 200px;
    height: 200px;
    background-color: pink;
    /* 四个方向 内边距相同 */
    padding: 30px;
    /* 单独设置一个方向内边距 */
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 40px;
    padding-left: 80px;
}
</style>
<div></div>
```

<br>

#### <font color="#2A878F">内边距多值写法</font>

> 一个值 -> padding:10px; -> 四个方向内边距均为10px
> 
> 四个值 -> padding：10px 20px 40px 80px; -> 上:10px;右:20px;下:40px;左:80px;
> 
> 三个值 -> padding：10px 20px 40px; -> 上:10px;左右:20px;下:40px;
> 
> 两个值 -> padding：10px 20px; -> 上下:10px;左右:20px;

> 技巧：从上开始顺时针赋值，当前方向没有数值则与对面取值相同。

<br>

#### <font color="#2A878F">盒子模型-尺寸计算</font>

默认情况：盒子尺寸 = 内容尺寸 + border 尺寸 + 内边距尺寸

结论：给盒子加 border / padding 会撑大盒子

解决：

手动做减法，减掉 border / padding 的尺寸

內减模式：box-sizing: border-box

```html
<style>
div {
    /* 需要200*200的盒子 */
    /* width: 200px;
    height: 200px; */

    /* 手动减去 */
    /* width: 160px;
    height: 160px; */

    background-color: pink;

    /* padding撑大盒子 */
    padding: 20px;

    /* 内减模式: 加padding和border不会撑大盒子 */
    box-sizing:border-box;
}
</style>
<div></div>
```

<br>

#### <font color="#2A878F">盒子模型-外边距</font>

作用：拉开两个盒子之间的距离

属性名：margin

> 提示：与 padding 属性值写法、含义相同 不做赘述!!!

#### <font color="#2A878F">版心居中</font>

> 左右 margin 值 为 auto（盒子要有宽度!!!）

<br>

### <font color="#A9D0D9">清除默认样式</font>

```html
<style>
/* 清除默认内外边距 */
* {
    margin: 0;
    padding: 0;
    /* 内减模式: 加padding和border不会撑大盒子 */
    box-sizing: border-box;
}

/* 清除列表项目符号 */
li {
    list-style: none;
}
</style>
<ul>
    <li></li>
</ul>
```

<br>

### <font color="#A9D0D9">盒子模型-元素溢出</font>

> 作用：控制溢出元素的内容的显示方式

属性名： overflow

属性值：

hidden -> 溢出隐藏

scroll -> 溢出滚动(无论是否溢出,都显示滚动条位置)

auto -> 溢出滚动(溢出才显示滚动条位置)

<br>

### <font color="#A9D0D9">外边距问题</font>

#### <font color="#2A878F">合并现象</font>

场景：垂直排列的兄弟元素，上下 margin 会合并

现象：取两个 margin 中的较大值生效

```html
<style>
.one {
    margin-bottom: 50px;
}
.two {
    margin-top: 20px;
}
</style>
```

如果需要两个盒子之间设置间距是100px,不能给两个盒子分别设置50xp而是只需给一个盒子设置100px。

<br>

#### <font color="#2A878F">外边距塌陷</font>

场景：父子级的标签，子级的添加 上外边距 会产生塌陷问题

现象：导致父级一起向下移动

```html
<style>
.father {
    width:300px;
    height:300px;
    background-color:pink;
}
.son {
    width: 100px;
    height: 100px;
    background-color: orange;
    /* 会出现塌陷问题 */
    margin-top: 50px;
}
</style>
<div class="father">
    <div class="son">son</div>
</div>
```

解决方法：

1. 取消子级margin，父级设置padding (推荐!!!)

2. 父级设置 overflow:hidden

3. 父级设置 border-top

<br>

```html
<style>
.father {
    width:300px;
    height:300px;
    background-color:pink;

    /*取消子级margin，父级设置padding*/
    /* 内边距撑大盒子 */
    padding-top:50px;
    /* 开启内减模式 */
    box-sizing:border-box;

    /* 父级设置 overflow:hidden */
    overflow:hidden;

    /* 父级设置 border-top 也会撑大盒子 */
    border-top:1px solid #000;
}
.son {
    width: 100px;
    height: 100px;
    background-color: orange;

    /* 会出现塌陷问题 */
    margin-top: 50px;
}
</style>
<div class="father">
    <div class="son">son</div>
</div>
```

<br>

### <font color="#A9D0D9">行内元素 – 内外边距问题</font>

场景：行内元素添加 margin 和 padding，无法改变元素垂直位置(可以改变水平位置)

解决方法：给行内元素添加 **line-height** 可以改变垂直位置

```html
<style>
    span {
        margin:50px;
    }
</style>
<span>span</span>
<span>span</span>
```

<br>

### <font color="#A9D0D9">圆角与盒子阴影</font>

#### <font color="#2A878F">盒子模型-圆角</font>

> 作用：设置元素的外边框为圆角。

属性名：border-radius

属性值：数字+px / 百分比

提示：属性值是圆角半径

<br>

多值写法：

技巧：从左上角开始顺时针赋值，当前角没有数值则与对角取值相同。

```html
<style>
div {
    margin: 50px auto;
    width: 200px;
    height: 200px;
    background-color: orange;

    /* border-radius: 20px; */

    /* 记忆：从左上角顺时针赋值，没有取值的角与对角取值相同 */

    /* 四值：左上  右上  右下  左下 */
    /* border-radius: 10px 20px 40px 80px; */

    /* 三值：左上  右上+左下  右下 */
    /* border-radius: 10px 40px 80px; */

    /* 两值：左上+右下  右上+左下 */
    border-radius: 10px 80px;
}
</style>
<div></div>
```

常见应用-正圆形状：

给**正方形**盒子设置圆角属性值为 宽高的一半 / 50%

常见应用-胶囊形状：

给**长方形**盒子设置圆角属性值为 盒子高度的一半

```html
<style>
img {
    width: 200px;
    height: 200px;

    /* border-radius: 100px; */

    /* 最大值是50%。超过50%没有效果 */
    border-radius: 50%;
}
div {
    width: 200px;
    height: 80px;
    background-color: orange;

    border-radius: 40px;
}
</style>
<!-- 正圆形 -- 头像 -->
<img src="./images/1.jpg" alt="">

<!-- 胶囊状 -->
<div></div>
```

<br>

#### <font color="#2A878F">盒子模型-阴影</font>

> 作用：给元素设置阴影效果

属性名：box-shadow

属性值：X 轴偏移量 Y 轴偏移量 模糊半径 扩散半径 颜色 内外阴影

注意：

- X 轴偏移量 和 Y 轴偏移量 必须书写
- 默认是外阴影，内阴影需要添加 inset

```html
<style>
div {
    margin: 50px auto;
    width: 200px;
    height: 80px;
    background-color: orange;

    box-shadow: 2px 5px 10px 1px rgba(0,0,0,0.5) inset;
}
</style>
</head>
<body>
  <div></div>
</body>
```

<br>

## <font color="Pink">Fourth</font>

CSS 书写顺序：

1. 盒子模型属性

2. 文字样式

3. 圆角、阴影等修饰属性

<br>

### <font color="#A9D0D9">标准流</font>

> 标准流也叫文档流，指的是标签在页面中默认的排布规则，例如：块元素独占一行，行内元素可以一行显示多个。

<br>

### <font color="#A9D0D9">浮动</font>

基本使用

> 作用：让块元素水平排列。

属性名：float

属性值：

- left: 左对齐

- right: 右对齐

> 特点：顶对齐；具备行内块显示模式特点；浮动的盒子会脱离标准流；不再占用标准流的位置。

```html
<style>
/* 特点：顶对齐；具备行内块显示模式特点；浮动的盒子会脱标 */
.one {
    width: 100px;
    height: 100px;
    background-color: brown;

    float: left;
}

.two {
    width: 200px;
    height: 200px;
    background-color: orange;

    /* float: left; */

    float: right;
}
</style>
</head>
<body>
  <div class="one">one</div>
  <div class="two">two</div>
</body>
```

案例：

```html
  <style>
    * {
      margin: 0;
      padding: 0;
      /* 内减模式: 加padding和border不会撑大盒子 */
      box-sizing: border-box;

    }

    li {
      list-style: none;
    }

    .product {
      margin: 50px auto;
      width: 1226px;
      height: 628px;
      background-color: pink;
    }

    .left {
      float: left;
      width: 234px;
      height: 628px;
      background-color: skyblue;
    }

    .right {
      float: right;
      width: 978px;
      height: 628px;
      background-color: brown;
    }

    .right li {
      float: left;
      margin-right: 14px;
      margin-bottom: 14px;
      width: 234px;
      height: 300px;
      background-color: orange;
    }

    /* 第四个li和第八个li 去掉右侧的margin */
    .right li:nth-child(4n) {
      margin-right: 0;
    }

    /* 细节：如果父级宽度不够，浮动的盒子会掉下来 */
  </style>
</head>
<body>
  <!-- 版心：左右，右面：8个产品 → 8个 li -->
  <div class="product">
    <div class="left"></div>
    <div class="right">
      <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
      </ul>
    </div>
  </div>
</body>
```

### <font color="#A9D0D9">清除浮动</font>

场景：浮动元素会脱标，如果父级没有高度，子级无法撑开父级高度（可能导致页面布局错乱）

列如：

```html
<style>
  .father {
    margin: 10px auto;
    width: 1200px;
    /* height: 300px; */
    background-color: pink;
  }

  .left {
    float: left;
    width: 200px;
    height: 300px;
    background-color: skyblue;
  }

  .right {
    float: right;
    width: 950px;
    height: 300px;
    background-color: orange;
  }

  .bottom {
    height: 100px;
    background-color: brown;
  }

</style>
</head>
<body>
<div class="father">
  <div class="left"></div>
  <div class="right"></div>
</div>
<div class="bottom"></div>
</body>
```

<style>
  .fatherr {
    margin: 10px auto;
    width: 1200px;
    /* height: 300px; */
    background-color: pink;
  }

  .leftt {
    float: left;
    width: 200px;
    height: 300px;
    background-color: skyblue;
  }

  .rightt {
    float: right;
    width: 950px;
    height: 300px;
    background-color: orange;
  }

  .bottomm {
    height: 100px;
    background-color: brown;
  }

</style>

</head>
<body>
<div class="fatherr">
  <div class="leftt"></div>
  <div class="rightt"></div>
</div>
<div class="bottomm"></div>
</body>

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

解决方法：清除浮动（清除浮动带来的影响）

#### <font color="#2A878F">额外标签法(了解)</font>

在父元素内容的最后添加一个块级元素，设置 CSS 属性 clear: both

例如：

```html
<style>
  .father {
    margin: 10px auto;
    width: 1200px;
    /* height: 300px; */
    background-color: pink;
  }

  .left {
    float: left;
    width: 200px;
    height: 300px;
    background-color: skyblue;
  }

  .right {
    float: right;
    width: 950px;
    height: 300px;
    background-color: orange;
  }

  .bottom {
    height: 100px;
    background-color: brown;
  }
  .clearfix {
    clear:both;
  }
</style>
</head>
<body>
<div class="father">
  <div class="left"></div>
  <div class="right"></div>
  <div class="clearfix"></div>
</div>
<div class="bottom"></div>
</body>
```

<br>

<style>
  .father2 {
    margin: 10px auto;
    width: 1200px;
    /* height: 300px; */
    background-color: pink;
  }

  .left2 {
    float: left;
    width: 200px;
    height: 300px;
    background-color: skyblue;
  }

  .right2 {
    float: right;
    width: 950px;
    height: 300px;
    background-color: orange;
  }

  .bottom2 {
    height: 100px;
    background-color: brown;
  }
  .clearfix {
    clear:both;
  }
</style>

</head>
<body>
<div class="father2">
  <div class="left2"></div>
  <div class="right2"></div>
  <div class="clearfix"></div>
</div>
<div class="bottom2"></div>
</body>

<br>
<br>

#### <font color="#2A878F">单伪元素法</font>

1. 准备 after 伪元素
2. 父级使用 clear

```html
  <style>
    .father {
      margin: 10px auto;
      width: 1200px;
      /* height: 300px; */
      background-color: pink;
    }

    .left {
      float: left;
      width: 200px;
      height: 300px;
      background-color: skyblue;
    }

    .right {
      float: right;
      width: 950px;
      height: 300px;
      background-color: orange;
    }

    .bottom {
      height: 100px;
      background-color: brown;
    }

    /* 单伪元素法 */
  .clearfix::after {
    content: "";
    display: block;
    clear: both;
  }
  </style>
</head>
<body>
  <div class="father clearfix">
    <div class="left"></div>
    <div class="right"></div>
  </div>
  <div class="bottom"></div>
</body>
```

#### <font color="#2A878F">双伪元素法(推荐)</font>

1. 准备 after 和 before 伪元素
2. 父级使用 clear

<br>

```html
  <style>
    .father {
      margin: 10px auto;
      width: 1200px;
      /* height: 300px; */
      background-color: pink;
    }

    .left {
      float: left;
      width: 200px;
      height: 300px;
      background-color: skyblue;
    }

    .right {
      float: right;
      width: 950px;
      height: 300px;
      background-color: orange;
    }

    .bottom {
      height: 100px;
      background-color: brown;
    }

    /* befor 解决外边距塌陷问题 */
    /* 双伪元素法 */
    .clearfix::before,
    .clearfix::after {
        content: "";
        display:table;
  }
  /* after 清除浮动 */
  .clearfix::after {
    clear:both;
  }
  </style>
</head>
<body>
  <div class="father clearfix">
    <div class="left"></div>
    <div class="right"></div>
  </div>
  <div class="bottom"></div>
</body>
```

#### <font color="#2A878F">overfow法</font>

> overflow:visible;        默认值，超出部分正常显示（正常超出显示）。
> 
> overflow:hidden;        超出部分隐藏（被修剪）不显示。
> 
> overflow:auto;           超出部分自动，如果横向或者纵向内容超出，不会在区域外显示，会出现横向或者纵向滚动条。
> 
> overflow:scroll;         与overflow:auto;类似，但是不管超没超出横纵向都会出现滚动条。
> 
> overflow:inherit;        继承父元素的overflow属性。

父元素添加css属性：overflow:hidden;

overflow的特殊用法。

当overflow的取值不是默认值的时候，就会创建BFC，从而起到一些独特的作用。

BFC：Block Format Context （块级格式化上下文） 它是一块独立的渲染区域。

BFC渲染区域：这个区域是由某个html元素创建，以下元素会在其内部创建BFC区域：

根元素

浮动和绝对定位

overflow不等于visible的块盒

BFC的作用：

1. 消除浮动，自动高度会计算浮动元素。

2. 它的边框盒不会与浮动元素重叠。

3. 不会和它的子元素进行外边距合并。

<br>

### <font color="#A9D0D9">总结</font>

浮动属性：float,left表示左浮动,right表示有浮动

特点：

1. 浮动后的盒子顶对齐

2. 浮动后的盒子具备行内块的特点

3. 父级宽度不够,浮动的子级会换行

4. 浮动后的盒子脱标

清除浮动：子级浮动,父级没有高度,子级无法撑开父级高度,影响布局

<br>

### <font color="#A9D0D9">Flex布局</font>

Flex 布局也叫弹性布局，是浏览器提倡的布局模型，非常适合结构化布局，提供了强大的空间分布和对齐能力。

Flex 模型不会产生浮动布局中脱标现象，布局网页更简单、更灵活。

#### <font color="#2A878F">Flex-组成</font>

> 设置方式：给父元素设置display:flex,子元素可以自动挤压或拉伸

组成部分：

- 弹性容器

- 弹性盒子

- 主轴：默认在水平方向

- 侧轴 / 交叉轴：默认在垂直方向

```html
  <style>
    /* 弹性容器 */
    .box {
      display: flex;

      height: 300px;
      border: 1px solid #000;
    }

    /* 弹性盒子：沿着主轴方向排列 */
    .box div {
      width: 200px;
      /* height: 100px; */
      background-color: pink;
    }
  </style>
</head>
<body>
  <div class="box">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>1</div>
    <div>2</div>
    <div>3</div>
  </div>
</body>
```

<br>

#### <font color="#2A878F">Flex布局-主轴与侧轴对齐方式</font>

- 创建flex容器： display: flex

- 主轴对齐方式： justify-content

- 侧轴对齐方式： align-items

- 某个弹性盒子侧轴对齐方式： align-self

- 修改主轴方向： flex-direction

- 弹性伸缩比： flex 

- 弹性盒子换行： flex-wrap

- 行对齐方式： align-content

<br>

##### <font color="#D0E0E3">主轴对齐方式：</font>

属性名：justify-content

属性值：

> flex-start -> 默认值，弹性盒子从**起点**开始依次排列
> 
> flex-end -> 弹性盒子从**终点**开始依次排列
> 
> **center** -> 弹性盒子沿主轴**居中**排列
> 
> **space-between** -> 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子**之间**
> 
> **space-around** -> 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子**两侧**
> 
> **space-evenly** -> 弹性盒子沿主轴均匀排列，弹性盒子与容器之间间距相等

<br>

```html
<style>
    .box {
      display: flex;
      /* justify-content: flex-start; */

      /* justify-content: flex-end; */

      /* 居中 */
      /* justify-content: center; */

      /* 父级剩余的尺寸分配成间距 */

      /* 弹性盒子之间的间距相等 */
      /* justify-content: space-between; */

      /* 间距出现在弹性盒子两侧 */
      /* 视觉效果：弹性盒子之间的间距是两端间距的2倍 */
      /* justify-content: space-around; */

      /* 各个间距都相等 */
      justify-content: space-evenly;

      height: 300px;
      border: 1px solid #000;
    }

    .box div {
      width: 200px;
      height: 100px;
      background-color: pink;
    }
  </style>
</head>
<body>
  <div class="box">
    <div>1</div>
    <div>2</div>
    <div>3</div>
  </div>
</body>
```

<br>

##### <font color="#D0E0E3">侧轴对齐方式：</font>

属性名：

- align-items： 当前弹性容器内所有弹性盒子的侧轴对齐方式(给弹性容器设置)

- align-self： 单独控制某个弹性盒子的侧轴对齐方式(给弹性盒子设置)

属性值：

> **stretch** -> 弹性盒子沿着侧轴线**拉伸至铺满容器**(弹性盒子没有设置侧轴方向尺寸则默认拉伸)
> 
> **center** -> 弹性盒子沿侧轴**居中**排列
> 
> flex-start -> 弹性盒子从**起点**开始依次排列
> 
> flex-end -> 弹性盒子从**终点**开始依次排列

```html
  <style>
    .box {
      display: flex;
      /* 弹性盒子在侧轴方向没有尺寸才能拉伸 */
      /* align-items: stretch; */

      /* align-items: center; */

      /* align-items: flex-start; */

      align-items: flex-end;

      height: 300px;
      border: 1px solid #000;
    }

    /* 第二个div，侧轴居中对齐 */
    .box div:nth-child(2) {
      align-self: center;
    }

    .box div {
      width: 200px;
      height: 100px;
      background-color: pink;
    }
  </style>
</head>
<body>
  <div class="box">
    <div>1</div>
    <div>2</div>
    <div>3</div>
  </div>
</body>
```

<br>

#### <font color="#2A878F">修改主轴方向</font>

> 主轴默认在水平方向，侧轴默认在垂直方向

属性名：

属性值：

row -> 水平方向，从左向右(默认)

**column** -> **垂直方向，从上向下**

row-reverse -> 水平方向，从右向左

column-reverse -> 垂直方向，从下向上

```html
  <style>
    .box {
      display: flex;

      /* 修改主轴方向 垂直方向；侧轴自动变换到水平方向 */
      flex-direction: column;

      /* 主轴在垂直，视觉效果：垂直居中 */
      justify-content: center;

      /* 侧轴在水平，视觉效果：水平居中 */
      align-items: center;

      width: 150px;
      height: 120px;
      background-color: pink;
    }

    img {
      width: 32px;
      height: 32px;
    }
  </style>
</head>
<body>
  <div class="box">
    <img src="./images/1.png" alt="">
    <span>媒体</span>
  </div>
</body>
```

<br>

#### <font color="#2A878F">弹性伸缩比</font>

> 作用：控制弹性盒子的主轴方向的尺寸。

属性名：flex

属性值：

- 整数数字，表示占用父级剩余尺寸的份数

- 默认情况下，主轴方向尺寸是靠内容撑开；侧轴默认拉伸

<br>

```html
  <style>
    /* 默认情况下，主轴方向尺寸是靠内容撑开；侧轴默认拉伸 */
    .box {
      display: flex;
      flex-direction: column;

      height: 300px;
      border: 1px solid #000;
    }

    .box div {
      /* height: 100px; */
      background-color: pink;
    }

    .box div:nth-child(1) {
      width: 200px;
    }

    .box div:nth-child(2) {
      flex: 1;
    }

    .box div:nth-child(3) {
      flex: 2;
    }
  </style>
</head>
<body>
  <div class="box">
    <div>1</div>
    <div>2</div>
    <div>3</div>
  </div>
</body>
```

<br>

#### <font color="#2A878F">**弹性盒子换行**</font>

> 弹性盒子可以自动挤压或拉伸，默认情况下，所有弹性盒子都在一行显示。

属性名：flex-wrap

属性值：

- wrap: 换行

- nowrap: 不换行(默认)

#### <font color="#2A878F">行内对齐方式</font>

属性名：align-content

属性值：

> flex-start -> 默认值，弹性盒子从**起点**开始依次排列
> 
> flex-end -> 弹性盒子从**终点**开始依次排列
> 
> **center** -> 弹性盒子沿主轴**居中**排列
> 
> **space-between** -> 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子**之间**
> 
> **space-around** -> 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子**两侧**
> 
> **space-evenly** -> 弹性盒子沿主轴均匀排列，弹性盒子与容器之间间距相等

> 调整 行对齐方式：对单行弹性盒子不生效!!!

<br>

```html
  <style>
    .box {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;

      /* 调整 行对齐方式：对单行弹性盒子不生效 */
      /* align-content: flex-start; */
      /* align-content: flex-end; */

      /* align-content: center; */

      /* align-content: space-between; */
      /* align-content: space-around; */

      /* 没有代码提示 */
      align-content: space-evenly;


      height: 400px;
      border: 1px solid #000;
    }

    .box div {
      width: 200px;
      height: 100px;
      background-color: pink;
    }
  </style>
</head>
<body>
  <div class="box">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>6</div>
    <div>7</div>
    <div>8</div>
  </div>
</body>
```

<br>

## <font color="Pink">Fifth</font>

### <font color="#A9D0D9">定位</font>

> 作用：灵活的改变盒子在网页中的位置

实现：

1. 定位模式：position

2. 边偏移：设置盒子的位置
* left

* right

* top

* bottom

<br>

#### <font color="#2A878F">相对定位</font>

**position: relative**

特点：

* 不脱标,占位,占用自己原来位置

* 显示模式特点保持不变

* 设置边偏移则相对自己原来位置移动

```css
div {
  position: relative;
  top: 100px;
  left: 200px;
}   
```

<br>

#### <font color="#2A878F">绝对定位</font>

**position: absolute**

> 使用场景：子级绝对定位，父级相对定位（**子绝父相**）

特点：

* 脱标，不占位

* 设置边偏移则相对最近的已经定位的祖先元素改变位置

* 如果祖先元素都未定位，则相对浏览器可视区改变位置

* 显示模式具备行内块特点

```css
.father {
  position: relative;
}

.father span {
  position: absolute;
  top: 0;
  right: 0;
}
```

<br>

#### <font color="#2A878F">定位居中</font>

实现步骤：

1. 绝对定位

2. 水平、垂直边偏移为 50%

> left:50% -> 盒子的最左边缘出现在参照物中间
> 
> top:50% -> 盒子的最上边缘出现在参照物中间
> 
> left:50%;top:50%; -> 盒子的左上角出现在盒子中间

1. 子级向左、上移动自身尺寸的一半
* 左、上的外边距为 – 尺寸的一半

* transform: translate(-50%, -50%) (让盒子居中)

```css
img {
  position: absolute;
  left: 50%;
  top: 50%;

  /* margin-left: -265px;
  margin-top: -127px; */

  /* 方便： 50% 就是自己宽高的一半 */
  transform: translate(-50%, -50%);
}
```

<br>

#### <font color="#2A878F">固定定位</font>

**position: fixed**

> 场景：元素的位置在网页滚动时不会改变

特点：
+

* 脱标，不占位

* 显示模式具备行内块特点

* 设置边偏移相对浏览器窗口改变位置

```css
div {
  position: fixed;
  top: 0;
  right: 0;

  width: 500px;
}
```

<br>

#### <font color="#2A878F">堆叠层级z-index</font>

> 默认效果：按照标签书写顺序，后来者居上
> 
> 作用：设置定位元素的层级顺序，改变定位元素的显示顺序

属性名：**z-index**

属性值：**整数数字**（默认值为0，取值越大，层级越高）

```css
.box1 {
  background-color: pink;
  /* 取值是整数，默认是0，取值越大显示顺序越靠上 */
  z-index: 1;
}

.box2 {
  background-color: skyblue;
  left: 100px;
  top: 100px;
  /* 取值是整数，默认是0，取值越大显示顺序越靠上 */
  z-index: 2;
}
```

<br>

### <font color="#A9D0D9">CSS精灵</font>

> CSS 精灵，也叫 **CSS Sprites**，是一种网页**图片应用处理方式**。把网页中**一些背景图片**整合到**一张图片**文件中，再**background-position** 精确的定位出背景图片的位置。
> 
> 优点：减少服务器被请求次数，减轻服务器的压力，提高页面加载速度

实现步骤：

1. 创建盒子，**盒子尺寸**与**小图**尺寸**相同**

2. 设置盒子**背景图**为精灵图

3. 添加 **background-position** 属性，改变**背景图位置**
   
   - 测量小图片**左上角坐标**
   
   - 取**负数**坐标为 background-position 属性值（向左上移动图片位置）

```html
  <style>
    div {
      width: 112px;
      height: 110px;
      background-color: pink;
      background-image: url(./images/abcd.jpg);
      background-position: -256px -276px;
    }
  </style>
</head>
<body>
  <div></div>
</body>
```

<br>

例子：

```html
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    li {
      list-style: none;
    }

    .service {
      margin: 100px auto;
      width: 1190px;
      height: 42px;
      /* background-color: pink; */
    }

    .service ul {
      display: flex;
    }

    .service li {
      display: flex;
      padding-left: 40px;
      width: 297px;
      height: 42px;
      /* background-color: skyblue; */
    }

    .service li h5 {
      margin-right: 10px;
      width: 36px;
      height: 42px;
      /* background-color: pink; */
      background: url(./images/sprite.png) 0 -192px;
    }

    .service li:nth-child(2) h5 {
      background-position: -41px -192px;
    }

    .service li:nth-child(3) h5 {
      background-position: -82px -192px;
    }

    .service li:nth-child(4) h5 {
      background-position: -123px -192px;
    }

    .service li p {
      font-size: 18px;
      color: #444;
      font-weight: 700;
      line-height: 42px;
    }
  </style>
</head>
<body>
  <div class="service">
    <ul>
      <li>
        <h5></h5>
        <p>品类齐全，轻松购物</p>
      </li>
      <li>
        <h5></h5>
        <p>多仓直发，极速配送</p>
      </li>
      <li>
        <h5></h5>
        <p>正品行货，精致服务</p>
      </li>
      <li>
        <h5></h5>
        <p>天天低价，畅选无忧</p>
      </li>
    </ul>
  </div>
</body>
```

<br>

### <font color="#A9D0D9">CSS修饰属性</font>

#### <font color="#2A878F">垂直对齐方式</font>

属性名：vertical-align

属性值：

baseline -> 基线对齐(默认)

top -> 顶部对齐

middle -> 居中对齐

bottom -> 底部对齐

```css
    div {
      border: 1px solid #000;
    }

    img {
      /* vertical-align: middle; */

      /* 顶对齐：最高内容的顶部 */
      /* vertical-align: top; */

      /* 底对齐：最高内容的底部 */
      /* vertical-align: bottom; */

      /* 因为浏览器把行内块、行内标签当做文字处理，默认按基线对齐 */
      /* 效果：图片img的底下有空白，转块级不按基线对齐，空白就消失了 */
      display: block;
    }
```

<br>

#### <font color="#2A878F">过渡</font>

> 作用：可以为一个元素在不同状态之间切换的时候添加**过渡效果**

属性名：**transition（复合属性）**

属性值：**过渡的属性  花费时间 (s)**

提示：

* 过渡的属性可以是具体的 CSS 属性

* 也可以为 all（两个状态属性值不同的所有属性，都产生过渡效果）

* transition 设置给元素本身,而不是加给hover的

```css
img {
  width: 200px;
  height: 200px;
  transition: all 1s;
}

img:hover {
  width: 500px;
  height: 500px;
}
```

<br>

#### <font color="#2A878F">透明度opacity</font>

> 作用：设置**整个元素的透明度**（包含背景和内容）

属性名：opacity

属性值：0 – 1

* 0：完全透明（元素不可见）

* 1：不透明

* 0-1之间小数：半透明

```css
div {
  width: 500px;
  height: 500px;
  background-color: orange;

  opacity: 0;

  opacity: 1;

  opacity: 0.5;
}
```

<br>

#### <font color="#2A878F">光标类型cursor</font>

> 作用：鼠标悬停在元素上时指针显示样式

属性名：cursor

属性值：

default -> 默认值，通常是箭头

pointer -> 小手效果，提示用户可以点击

text -> 工字形，提示用户可以选择文字

move -> 十字光标，提示用户可以移动

```css
div {
  width: 200px;
  height: 200px;
  background-color: pink;

  cursor: pointer;    
  cursor: text;  
  cursor: move;
}
```
