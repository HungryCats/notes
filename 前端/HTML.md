# <font color="Red">HTML</font>

---

## <font color="Pink">HTML的基本骨架</font>

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- 网页标题 -->
    <title>HUNGRYCATS</title>
</head>
<body>

</body>
</html>
```

---

## <font color="Pink">标签的关系</font>

> 父子关系(嵌套关系)：子级标签换行且缩进(Tab键)

```HTML
<html>
    <head></head>
</html>
```

> 兄弟关系(并列关系)：兄弟标签换行要对齐

```HTML
<head></head>
<body></body>
```

---

## <font color="Pink">注释</font>

概念：注释是对代码的解释和说明，能够提高程序的可读性，方便理解、查找代码。

注释不会再浏览器中显示。

```HTML
<!-- 我是 HTML 注释 -->
```

---

## <font color="Pink">标题标签</font>

```HTML
<h1></h1> 
<h2></h2>
<h3></h3>
<h4></h4>
<h5></h5>
<h6></h6>
```

特点：

- 文字加粗
- 自豪逐渐减小
- 独占一行(换行)

<hr>

## <font color="Pink">段落标签</font>

> 显示特点：
> 
> p标签独占一行
> 
> 段落之间存在间隙

```HTML
<!-- 一般用在新闻段落、文章段落、产品描述信息等等。 -->
<p></p>
```

<hr>

## <font color="Pink">换行与水平线</font>

- 换行：&lt;br&gt; (单标签)

- 水平线： &lt;hr&gt; (单标签)

<hr>

## <font color="Pink">文本格式化标签</font>

> 作用：为文本添加特殊格式，以突出重点。常见的文本格式：加粗、倾斜、下划线、删除线等。

```HTML
<!-- 重点 自带强调含义 -->
<strong>加粗</strong>
<em>倾斜</em>
<ins>下划线</ins>
<del>删除线</del>

<!-- 了解 -->
<b>加粗</b>
<i>倾斜</i>
<u>下划线</u>
<s>删除线</s>
```

样式：
<strong>加粗</strong>
<em>倾斜</em>
<u>下划线</u>
<del>删除线</del>

<hr>

## <font color="Pink">图像标签</font>

> 作用：在网页中插入图片

```HTML
<!-- src用于指定图像的位置和名称，是的必须属性。 -->
<img src="图片的URL">
```

alt         替换文本        图片无法显示的时候显示的文字

title       提示文本        鼠标悬停在图片上面的时候显示的文字

<font color="Green">了解即可一般在css中设置宽高</font>

width       图片的宽度      值为数字，没有单位

height      图片的高度      值为数字，没有单位

```HTML
<!-- 标签名和属性之间用空格隔开 -->
<img src="" alt="文字" title="文字" width="100" height="100">
```

路径

相对路径：从当前文件位置出发查找目标文件

特殊符号：
/ 表示进入某个文件夹里面  ————> 文件夹名/

. 表示当前文件所在文件夹  ————>  ./

.. 进入当前文件的上一级文件夹 ————>  ../

绝对路径：从盘符出发查找目标文件

<hr>

## <font color="Pink">超链接标签</font>

> 作用：点击跳转到其他页面。

拓展：开发初期，不确定跳转地址，则 href 属性值写为 #，表示空链接，页面不会跳转，在当前页面刷新一次。

超链接默认是在当前窗口跳转页面，添加 target="_blank" 实现新窗口打开页面。

href 属性值是跳转地址，是超链接的必须属性。

```HTML
<a href="https://www.baidu.com">跳转到百度</a>
<!-- 跳转到本地文件：相对路径查找 -->
<!-- target="_blank" 新窗口跳转页面 -->
<a href="./01-标签的写法.html" target="_blank">跳转到01-标签的写法</a>
<!-- 开发初期，不知道超链接的跳转地址，href属性值写#，表示空链接，不会跳转 -->
<a href="#">空链接</a>
```

<hr>

## <font color="Pink">音频</font>

```HTML
<audio src="音频的 URL"></audio>
```

属性：
src(必须) 音频URL 支持格式：MP3、Ogg、Wav

controls 显示音频控制面板

loop 循环播放

autoplay 浏览器一般禁用自动播放的功能

<hr>

## <font color="Pink">视频标签</font>

```HTML
<video src="视频的 URL"></video>

<!-- 在浏览器中，想要自动播放，必须有 muted 属性 -->
<video src="./media/vue.mp4" controls loop muted autoplay></video>
```

属性：
src(必须) 视频URL 支持格式：MP4、WebM、Ogg

controls 显示音频控制面板

loop 循环播放

autoplay 浏览器一般静音状态自动播放

muted 静音播放

<hr>

## <font color="Pink">列表</font>

> 作用：布局内容排列整齐的区域
> 列表分类：无序列表 、有序列表、定义列表

<font color="Coral">无序列表：</font>

> 标签：ul 嵌套 li ，ul 是无序列表，li 是列表条目

> ul标签里面只能包裹li标签

> li标签里面可以包裹任何内容

```HTML
<ul>
    <li>列表条目</li>
    <li>列表条目</li>
    <li>列表条目</li>
</ul>
```

样式：

<ul>
    <li>列表条目</li>
    <li>列表条目</li>
    <li>列表条目</li>
</ul>

<font color="Coral">有序列表：</font>

> 标签：ol嵌套li，ol是有序列表，li是列表条目

> ol标签里面只能包裹li标签

> li标签里面可以包裹任何内容

```HTML
<ol>
    <li>列表条目</li>
    <li>列表条目</li>
    <li>列表条目</li>
</ol>
```

样式：

<ol>
    <li>列表条目</li>
    <li>列表条目</li>
    <li>列表条目</li>
</ol>

<font color="Coral">定义列表：</font>

> 标签：dl嵌套dt和dd，dl是定义列表，dt是定义列表的标题，dd是定义列表的描述/详情
> dl里面只能包含dr和dd
> dt和dd里面可以包含任何内容

```HTML
<dl>
    <dt>标题</dt>
    <dd>详情</dd>
    <dd>详情</dd>
    <dd>详情</dd>
</dl>
```

样式：

<dl>
    <dt>标题</dt>
    <dd>详情</dd>
    <dd>详情</dd>
    <dd>详情</dd>
</dl>

<hr>

## <font color="Pink">表格</font>

> 标签：table嵌套tr，tr嵌套td/th

table  表格

tr  行

th  表头单元格

td  内容单元格

提示：网页中，表格默认没有边框线，使用border属性添加边框线

```HTML
<table border="1">
    <tr>
        <th>姓名</th>
        <th>语文</th>
        <th>数学</th>
        <th>总分</th>
    </tr> 
    <tr>
        <td>张三</td>
        <td>100</td>
        <td>100</td>
        <td>200</td>
    </tr>
    <tr>
        <td>总结</td>
        <td>全市第一</td>
        <td>全市第一</td>
        <td>全市第一</td>
    </tr>
</table>
```

样式：

<table border="1">
    <tr>
        <th>姓名</th>
        <th>语文</th>
        <th>数学</th>
        <th>总分</th>
    </tr> 
    <tr>
        <td>张三</td>
        <td>100</td>
        <td>100</td>
        <td>200</td>
    </tr>
    <tr>
        <td>总结</td>
        <td>全市第一</td>
        <td>全市第一</td>
        <td>全市第一</td>
    </tr>
</table>

表格结构标签：了解即可没有什么太大用处

作用：用表格结构标签把内容划分区域，让表格结构更清晰，语义更清晰。

thead  表格头部  表格头部内容

tbody  表格主体  主要内容区域

tfoot  表格底部  汇总信息区域

```HTML
<table border="1">
    <thead>
        <tr>
            <th>姓名</th>
            <th>语文</th>
            <th>数学</th>
            <th>总分</th>
        </tr> 
    </thead>
    <tbody>
        <tr>
            <td>张三</td>
            <td>100</td>
            <td>100</td>
            <td>200</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>总结</td>
            <td>全市第一</td>
            <td>全市第一</td>
            <td>全市第一</td>
        </tr>
    </tfoot>
</table>
```

合并单元格：

保留最左最上的单元格，添加属性（取值是数字，表示需要合并的单元格数量）

- 跨行合并，保留最上单元格，添加属性 rowspan

- 跨列合并，保留最左单元格，添加属性 colspan

```HTML
<table border="1">
    <thead>
        <tr>
        <th>姓名</th>
        <th>语文</th>
        <th>数学</th>
        <th>总分</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td>张三</td>
        <td>99</td>
        <td rowspan="2">100</td>
        <td>199</td>
        </tr>
        <tr>
        <td>李四</td>
        <td>98</td>
        <!-- <td>100</td> -->
        <td>198</td>
        </tr>
    </tbody>
    <tfoot>
        <tr style="text-align:center">
        <td>总结</td>
        <td colspan="3">全市第一</td>
        <!-- <td>全市第一</td>
        <td>全市第一</td> -->
        </tr>
    </tfoot>
</table>
```

<table border="1">
    <thead>
        <tr>
        <th>姓名</th>
        <th>语文</th>
        <th>数学</th>
        <th>总分</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td>张三</td>
        <td>99</td>
        <td rowspan="2">100</td>
        <td>199</td>
        </tr>
        <tr>
        <td>李四</td>
        <td>98</td>
        <!-- <td>100</td> -->
        <td>198</td>
        </tr>
    </tbody>
    <tfoot>
        <tr style="text-align:center">
        <td>总结</td>
        <td colspan="3">全市第一</td>
        <!-- <td>全市第一</td>
        <td>全市第一</td> -->
        </tr>
    </tfoot>
</table>

<hr>

## <font color="Pink">表单</font>

> 作用：收集用户信息。
> 使用场景：登录页面 注册页面 搜索区域

<font color="Coral">input 标签</font>

input 标签 type 属性值不同，则功能不同。

```HTML
<input type="..." >
```

属性值：

text        文本框，用于输入单行文本

> <input type="text">

password    密码框

> <input type="password">

radio       单选框

> <input type="radio">

checkbox    多选框

> <input type="checkbox">

file        上传文件

> <input type="file">

input 标签占位文本

> 占位文本：提示信息，文本框和密码框都可以使用。

```HTML
<input type="..." placeholder="提示信息">
```

<input type="..." placeholder="提示信息">

<br>
<br>

<font color="Coral">单选框</font>

属性：

name    控件名字    控件分组，同组只能选中一个(单选功能)

checkd  默认选中    属性名和属性值相同，简写为一个单词

> 提示：name 属性值自定义。

```HTML
<input type="radio" name="gender" checked> 男
<input type="radio" name="gender"> 女
```

<input type="radio" name="gender" checked> 男
<input type="radio" name="gender"> 女

<br>
<br>

<font color="Coral">多选框</font>

多选框也叫复选框，默认选中：checked。

```HTML
<input type="checkbox" checked> 敲前端代码
```

<input type="checkbox" checked> 敲前端代码

<br>
<br>

<font color="Coral">上传文件</font>

默认情况下，文件上传表单控件只能上传一个文件，添加 multiple 属性可以实现文件多选功能。

```HTML
<input type="file" mutiple>
```

<input type="file" mutiple>

<br>
<br>

<font color="Coral">下拉菜单</font>

> 标签：select 嵌套 option，select 是下拉菜单整体，option是下拉菜单的每一项
> 默认显示第一项，selected 属性实现默认选中功能。

```HTML
<select>
    <option>北京</option>
    <option>上海</option>
    <option>广州</option>
    <option>深圳</option>
    <option selected>山东</option>
</select>
```

<select>
    <option>北京</option>
    <option>上海</option>
    <option>广州</option>
    <option>深圳</option>
    <option selected>山东</option>
</select>

<br>
<br>

<font color="Coral">文本域</font>

> 作用：多行输入文本的表单控件。

```HTML
<textarea name="" id="" cols="30" rows="10">输入评论</textarea>
```

<textarea>输入评论</textarea>

<br>
<br>

> 注意点：
> 
> 实际开发中，使用 CSS 设置 文本域的尺寸
> 
> 实际开发中，一般禁用右下角的拖拽功能

<font color="Coral">label 标签</font>

> 作用：网页中，某个标签的说明文本。
> 
> 经验：用 label 标签绑定文字和表单控件的关系，增大表单控件的点击范围。

- 写法一
- label 标签只包裹内容，不包裹表单控件
- 设置 label 标签的 for 属性值 和表单控件的 id 属性值相同

```HTML
<input type="radio" id="man">
<label for="man">男</label>
```

<input type="radio" id="man">
<label for="man">男</label>

<br>
<br>

- 写法二：使用 label 标签包裹文字和表单控件，不需要属性

> 提示：支持 label 标签增大点击范围的表单控件：文本框、密码框、上传文件、单选框、多选框、下拉菜单、文本域等等。

```HTML
<label><input type="radio"> 女</label>
```

<label><input type="radio"> 女</label>

<br>
<br>

<font color="Coral">按钮</font>

```HTML
<button type="">按钮</button>
```

<button type="">按钮</button>

<br>
<br>

属性：

submit  提交按钮，点击后可以提交数据到后台(默认功能)

reset   重置按钮，点击后将表单控件恢复默认值

button  普通按钮，默认没有功能，一般配合JavaScript使用

> 提示：按钮需配合 form 标签（表单区域）才能实现对应的功能。

```HTML
<!-- form 表单区域 -->
<!-- action="" 发送数据的地址 -->
<form action="">
用户名：<input type="text">
<br><br>
密码：<input type="password">
<br><br>
<!-- 如果省略 type 属性，功能是 提交 -->
<button type="submit">提交</button>
<button type="reset">重置</button>
<button type="button">普通按钮</button>
</form>
```

<form action="">
用户名：<input type="text">
<br><br>
密码：<input type="password">
<br><br>
<button type="submit">提交</button>
<button type="reset">重置</button>
<button type="button">普通按钮</button>
</form>

<br>
<br>

<font color="Coral">语义化</font>

1. 无语义的布局标签

> 作用：布局网页（划分网页区域，摆放内容）

- div：独占一行
- span：不换行

```HTML
<div>div 标签，独占一行</div>
<span>span 标签，不换行</span>
```

2. 有语义的布局标签

header      网页头部

nav         网页导航

footer      网页底部

aside       网页侧边栏

section     网页区块

article     网页文章

<font color="Coral">字符实体</font>

```HTML
空格 ————>  
小于号 ————> <
大于号 ————> >
```


