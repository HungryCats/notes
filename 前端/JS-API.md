# <font color="Red">JS-APIs</font>

## <font color="Pink">First</font>

### <font color="#A9D0D9">变量声明</font>

- 变量声明有三个 var let 和 const

- var，老派写法，问题很多，基本淘汰

- let or const ？

- 建议：const 优先，尽量使用cosnt，cosnt 语义化好

### <font color="#A9D0D9">DOM</font>

> 作用：就是使用JS去操作html和浏览器
> 
> 分类：DOM(文档对象模型)、BOM(浏览器对象模型)

> DOM（Document Object Model）是将整个 HTML 文档的每一个标签元素视为一个对象，这个对象下包含了许多的属性和方法，通过操作这些属性或者调用这些方法实现对 HTML 的动态更新，为实现网页特效以及用户交互提供技术支撑。

简言之 DOM 是用来动态修改 HTML 的，其目的是开发网页特效及用户交互。

#### <font color="#2A878F">DOM树</font>

> 将HTML文档以树状结构直观的表现出来，我们称之为文档树或 DOM 树
> 描述网页内容关系的名词
> 作用：文档树直观的体现了标签与标签之间的关系

![DOM树](https://img-blog.csdnimg.cn/8d8e0fa6c9ce4f39bdab608400f0e63e.png)

#### <font color="#2A878F">DOM对象(重要)</font>

DOM对象：浏览器根据html标签生成的JS对象

- 所有的标签属性都可以在这个对象上面找到
- 修改这个对象的属性会自动映射到标签身上

DOM的核心思想

- 把网页内容当做对象来处理

document 对象

- 是DOM里提供的一个对象

- 所以他提供的属性和方法都是用来访问和操作网页内容的
  
  例如：document.write()

- 网页所有内容都在document里面

### <font color="#A9D0D9">获取DOM元素</font>

1. querySelector   满足条件的第一个元素
2. querySelectorAll  满足条件的元素集合 返回伪数组
3. 了解其他方式
   - `getElementById`
   - `getElementsByTagName`

总结：

- `document.getElementById` 专门获取元素类型节点，根据标签的 `id`  属性查找

- 任意 DOM 对象都包含 `nodeType` 属性，用来检检测节点类型
1. 选择匹配第一个元素
   
    语法：
   
   ```html
   <script>
       document.querySelector('css选择器')
   </script>
   ```
   
    参数：
   
   - 包含一个或多个有效的css选择器 字符串
     
     返回值：
   
   - css选择器匹配的第一个元素，一个HTMLElement对象。

2. 选择匹配的多个元素
   
    语法：
   
   ```html
   <script>
   document.querSelectorAll('css选择器')
   </script>
   ```
   
    参数：
   
   - 包含一个或者多个有效的css选择器 字符串
     
     返回值：
   
   - css选择器匹配的NodeList 对象集合
   
   - `document.querSelectorAll('ul li')`

    得到的是一个伪数组：
    
    - 有长度有索引号的数组
    - 但是没有pop() push() 等数组方法
    
    想要得到里面的每一个对象，则需要 **for循环** 遍历的方式获得
    
    就算只有一个元素，通过 `querSelectorAll()` 获取过来的也是一个伪数         组，里面只有一个元素而已

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>饿死的冏猫</title>
</head>
  <style>
    .box {
      width: 200px;
      height: 200px;
    }
  </style>
</head>

<body>
  <div class="box">123</div>
  <div class="box">abc</div>
  <p id="nav">导航栏</p>
  <ul class="nav">
    <li>测试1</li>
    <li>测试2</li>
    <li>测试3</li>
  </ul>
  <script>
    // 1. 获取匹配的第一个元素
    // const box = document.querySelector('div')
    // const box = document.querySelector('.box')
    // console.log(box)
    // const nav = document.querySelector('#nav')
    // console.log(nav)
    // nav.style.color = 'red'
    // 1. 我要获取第一个小 ul li
    // const li = document.querySelector('ul li:first-child')
    // console.log(li)
    // 2. 选择所有的小li
    // const lis = document.querySelectorAll('ul li')
    // console.log(lis)

    // 1.获取元素
    const lis = document.querySelectorAll('.nav li')
    // console.log(lis)
    for (let i = 0; i < lis.length; i++) {
      console.log(lis[i]) // 每一个小li对象
    }

    const p = document.querySelectorAll('#nav')
    // console.log(p)
    // p[0].style.color = 'red'
  </script>
</body>
</html>
```

<br>

### <font color="#A9D0D9"> 操作元素内容</font>

> 通过修改 DOM 的文本内容，动态改变网页的内容。

1. `innerText` 将文本内容添加/更新到任意标签位置，**文本中包含的标签不会被解析。**

2. `innerHTML` 将文本内容添加/更新到任意标签位置，**文本中包含的标签会被解析。**

总结：如果文本内容中包含 `html` 标签时推荐使用 `innerHTML`，否则建议使用 `innerText` 属性。

```html
<body>
  <div class="box">我是文字的内容</div>
  <script>
    // const obj = {
    //   name: 'cats老师'
    // }
    // console.log(obj.name)
    // obj.name = 'red老师'
    // 1. 获取元素
    const box = document.querySelector('.box')
    // 2. 修改文字内容  对象.innerText 属性
    // console.log(box.innerText)  // 获取文字内容
    // // box.innerText = '我是一个盒子'  // 修改文字内容
    // box.innerText = '<strong>我是一个盒子</strong>'  // 不解析标签

    // 3. innerHTML 解析标签
    console.log(box.innerHTML)
    // box.innerHTML = '我要更换'
    box.innerHTML = '<strong>我要更换</strong>'
  </script>
</body>
```

<br>

### <font color="#A9D0D9">DOM修改元素常见属性</font>

> 1. 操作元素常用样式属性
> 2. 操作元素**样式**属性
> 3. 操作**表单元素**属性
> 4. 自定义属性

#### <font color="#2A878F">操作元素常用样式属性</font>

可以通过JS设置/修改标签元素属性，比如通过src更换图片

最常见的属性比如：href、title、src等

语法：

`对象.属性 = 值` -> 有则改无则增

```html
<body>
  <img src="./images/1.webp" alt="">
  <script>
    // 1. 获取图片元素
    const img = document.querySelector('img')
    // 2. 修改图片对象的属性   对象.属性 = 值
    img.src = './images/2.webp'
    img.title = 'cats老师的艺术照'
  </script>
</body>
```

示例：

页面刷新，图片随机更换

需求：当我们刷新页面，页面中的图片随机显示不同的图片

分析：

① ：随机显示，则需要用到随机函数

② ：更换图片需要用到图片的 src 属性，进行修改

③ ：核心思路：

1. 获取图片元素

2. 随机得到图片序号

3. 图片.src = 图片随机路

```html
<body>
  <img src="./images/1.webp" alt="">
  <script>
    // 取到 N ~ M 的随机整数
    function getRandom(N, M) {
      return Math.floor(Math.random() * (M - N + 1)) + N
    }
    // 1. 获取图片对象
    const img = document.querySelector('img')
    // 2. 随机得到序号
    const random = getRandom(1, 6)
    // 3. 更换路径
    img.src = `./images/${random}.webp`
  </script>
</body>
```

<br>

#### <font color="#2A878F">操作元素样式属性</font>

> 还可以通过 JS 设置/修改标签元素的样式属性。

> 比如通过 轮播图小圆点自动更换颜色样式

> 点击按钮可以滚动图片，这是移动的图片的位置 left 等等

学习路径：

- 通过 style 属性操作CSS

- 操作类名(className) 操作CSS

- 通过 classList

<br>

##### <font color="#6163d3">style修改样式属性</font>

语法：

  `对象.style.样式属性 = 值`

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    .box {
      width: 200px;
      height: 200px;
      background-color: pink;
    }
  </style>
</head>
<body>
  <div class="box"></div>
  <script>
    // 1. 获取元素
    const box = document.querySelector('.box')
    //2. 修改样式属性 对象.style.样式属性 = '值'  别忘了跟单位
    box.style.width = '300px'
    // 多组单词的采取 小驼峰命名法
    box.style.backgroundColor = 'hotpink'
    box.style.border = '2px solid blue'
    box.style.borderTop = '2px solid red'
  </script>
</body>
```

页面刷新，页面随机更换背景图片

需求：当我们刷新页面，页面中的背景图片随机显示不同的图片

分析：

- 随机函数

- css页面背景图片 background-image

- 标签选择body，因为body是唯一的标签，可以直接写document.body.style

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    body {
      background: url(./images/desktop_1.jpg) no-repeat top center/cover;
    }
  </style>
</head>
<body>
  <script>
    // console.log(document.body)
    // 取到 N ~ M 的随机整数
    function getRandom(N, M) {
      return Math.floor(Math.random() * (M - N + 1)) + N
    }
    // 随机数
    const random = getRandom(1, 10)
    document.body.style.backgroundImage = `url(./images/desktop_${random}.jpg)`
  </script>
</body>
```

<br>

##### <font color="#6163d3">类名修改样式</font>

> 如果修改的样式比较多，直接通过style属性修改比较繁琐，可以借助于css类名的形式
> 
> className是使用新值换旧值，如果需要添加一个类，需要保留之前的类名

语法：

  `元素.className = 'active'` -> active 是一个css类名

注意：**会覆盖原来的类名！！！**

```html
  <style>
    div {
      width: 200px;
      height: 200px;
      background-color: pink;
    }
    .nav {
      color: red;
    }
    .box {
      width: 300px;
      height: 300px;
      background-color: skyblue;
      margin: 100px auto;
      padding: 10px;
      border: 1px solid #000;
    }
  </style>
</head>
<body>
  <div class="nav">123</div>
  <script>
    // 1. 获取元素
    const div = document.querySelector('div')
    // 2.添加类名  class 是个关键字 我们用 className
    div.className = 'nav box'
  </script>
</body>
```

##### <font color="#6163d3">classList修改样式</font>

为了解决className容易覆盖以前的类名，可以通过classList方式追加和删除类名

语法：

1. 追加一个类
   
   - `元素.classList.add('类名')`

2. 删除一个类
   
   - `元素.classList.remove('类名')`

3. 切换一个类
   
   - `元素.classList.toggle('类名')`

```html
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    .box {
      width: 200px;
      height: 200px;
      color: #333;
    }
    .active {
      color: red;
      background-color: pink;
    }
  </style>
</head>
<body>
  <div class="box active">文字</div>
  <script>
    // 通过classList添加
    // 1. 获取元素
    const box = document.querySelector('.box')
    // 2. 修改样式
    // 2.1 追加类 add() 类名不加点，并且是字符串
    box.classList.add('active')
    // 2.2 删除类  remove() 类名不加点，并且是字符串
    box.classList.remove('box')
    // 2.3 切换类  toggle()  有还是没有啊， 有就删掉，没有就加上
    box.classList.toggle('active')
  </script>
</body>
```

#### <font color="#2A878F">操作表单元素属性</font>

表单很多情况，也需要修改属性，比如点击眼睛，可以看到密码，本质是把表单类型转换为文本框

正常的有属性有取值的跟其他的标签属性没有任何区别

> 获取: DOM对象.属性名
> 
> 设置: DOM对象.属性名= 新值
> 
> 表单属性中添加就有效果，移除就没有效果，一律用布尔值表示 ，true 添加该属性，false 移除该属性
> 比如：disable checked selected 

`表单.value = '用户名'`

`表单.type = 'password'`

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <!-- <input type="text" value="电脑"> -->
  <input type="checkbox" name="" id="">
  <button>点击</button>
  <script>
    // 1 获取元素
    const uname = document.querySelector('input')
    // 2. 获取值  获取表单里面的值 用的  表单.value
    // console.log(uname.value) // 电脑
    // console.log(uname.innerHTML)  innertHTML 得不到表单的内容
    // 3. 设置表单的值
    uname.value = '我要买电脑'
    // console.log(uname.type)
    uname.type = 'password'

    // 1. 获取
    const ipt = document.querySelector('input')
    // console.log(ipt.checked)  // false   只接受布尔值
    ipt.checked = true
    // ipt.checked = 'true'  // 会选中，不提倡  有隐式转换

    // 1.获取
    const button = document.querySelector('button')
    // console.log(button.disabled)  // 默认false 不禁用
    button.disabled = true   // 禁用按钮

  </script>
</body>
```

#### <font color="#2A878F">自定义属性</font>

标准属性: 标签天生自带的属性 比如class id title等, 可以直接使用点语法操作比如： disabled、checked、selected

> 自定义属性：

> 在html5中推出来了专门的data-自定义属性  

> 在标签上一律以data-开头

> 在DOM对象上一律以dataset对象方式获取

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <div data-id="1" data-spm="不知道">1</div>
  <div data-id="2">2</div>
  <div data-id="3">3</div>
  <div data-id="4">4</div>
  <div data-id="5">5</div>
  <script>
    const one = document.querySelector('div')
    console.log(one.dataset.id)  // 1
    console.log(one.dataset.spm)  // 不知道
  </script>
</body>
```

### <font color="#A9D0D9">定时器-间歇函数</font>

`setInterval` 是 JavaScript 中内置的函数，它的作用是间隔固定的时间自动重复执行另一个函数，也叫定时器函数。

目标： 能够使用定时器函数重复执行代码

定时器函数可以开启和关闭

> 开启定时器
> 
> `setInterval(函数,间隔时间)`
> 
> 作用：每隔一段时间调用这个函数
> 
> 间隔时间单位是毫秒

```html
<script>
function repeat() {
  console.log('前端程序员，就是头发多咋滴~~')
}
setInterval(repeat,1000)
</script>
```

注意！！！

- **函数名不要加小括号**

- **定时器返回的是一个数字**

> 关闭定时器
> 
> `let 变量名 = setInterval(函数,间隔时间)`
> 
> `clearInterval(变量名)`

```html
<script>
let timer = setInterval(function() {
  console.log('hi~~')
},1000)
clearInterval(timer)
</script>
```

```html
<body>
  <script>
    setInterval(函数, 间隔时间)
    setInterval(function () {
      console.log('一秒执行一次')
    }, 1000)

    function fn() {
      console.log('一秒执行一次')
    }
    // setInterval(函数名, 间隔时间)  函数名不要加小括号
    let n = setInterval(fn, 1000)
    // setInterval('fn()', 1000)
    console.log(n)
    // 关闭定时器
    clearInterval(n)

    // let m = setInterval(function () {
    //   console.log(11)
    // }, 2000)
    // console.log(m)

    // const num = 10
    // num = 10
    // console.log(num)
    let i = 1
    setInterval(function () {
      i++
      document.write(`${i} `)
    }, 200)
  </script>
</body>
```

### <font color="#A9D0D9">阅读注册协议</font>

需求：按钮60s之后才可以使用

```html
<body>
    <textarea name="" id="" cols="30" rows="10">
        用户注册协议
        欢迎注册成为京东用户！在您注册过程中，您需要完成我们的注册流程并通过点击同意的形式在线签署以下协议，请您务必仔细阅读、充分理解协议中的条款内容后再点击同意（尤其是以粗体或下划线标识的条款，因为这些条款可能会明确您应履行的义务或对您的权利有所限制）。
        【请您注意】如果您不同意以下协议全部或任何条款约定，请您停止注册。您停止注册后将仅可以浏览我们的商品信息但无法享受我们的产品或服务。如您按照注册流程提示填写信息，阅读并点击同意上述协议且完成全部注册流程后，即表示您已充分阅读、理解并接受协议的全部内容，并表明您同意我们可以依据协议内容来处理您的个人信息，并同意我们将您的订单信息共享给为完成此订单所必须的第三方合作方（详情查看
    </textarea>
    <br>
    <button class="btn" disabled>我已经阅读用户协议(5)</button>
    <script>
        // 1. 获取元素
        const btn = document.querySelector('.btn')
        // console.log(btn.innerHTML)  butto按钮特殊用innerHTML
        // 2. 倒计时
        let i = 5
        // 2.1 开启定时器
        let n = setInterval(function () {
            i--
            btn.innerHTML = `我已经阅读用户协议(${i})`
            if (i === 0) {
                clearInterval(n)  // 关闭定时器
                // 定时器停了，我就可以开按钮
                btn.disabled = false
                btn.innerHTML = '我已经阅读用户协议啦！'
            }
        }, 1000)

    </script>
</body>
```

## <font color="Pink">Second</font>

> 事件:
> 
> 事件是编程语言中的术语，它是用来描述程序的行为或状态的，**一旦行为或状态发生改变，便立即调用一个函数。**
> 
> 例如：用户使用【鼠标点击】网页中的一个按钮、用户使用【鼠标拖拽】网页中的一张图片

### <font color="#A9D0D9">事件监听</font>

> 结合 DOM 使用事件时，需要为 DOM 对象添加事件监听，等待事件发生（触发）时，便立即调用一个函数。

> `addEventListener` 是 DOM 对象专门用来添加事件监听的方法，它的两个参数分别为【事件类型】和【事件回调】。

语法：

`元素对象.addEventListener('事件类型',要执行的函数)`

完成事件监听分成3个步骤：

1. 获取 DOM 元素

2. 通过 `addEventListener` 方法为 DOM 节点添加事件监听

3. 等待事件触发，如用户点击了某个按钮时便会触发 鼠标单击`click` 事件类型、鼠标经过`mouserover`事件等

4. 事件触发后，相对应的回调函数会被执行

注意！！！

事件类型要加`引号`

函数是点击之后再去执行，每次点击都会执行一次

```html
<button>按钮</button>
<script>
  const btn = document.querySelector('.btn')
  //修改元素样式
  btn.addEventListener('click',function() {
    alter('被点击了呢~')
  })
</script>
```

```html
<body>
  <button>点击</button>
  <script>
    // 需求： 点击了按钮，弹出一个对话框
    // 1. 事件源   按钮  
    // 2.事件类型 点击鼠标   click 字符串
    // 3. 事件处理程序 弹出对话框
    const btn = document.querySelector('button')
    btn.addEventListener('click', function () {
      alert('你早呀~')
    })

  </script>
</body>
```

#### <font color="#2A878F">随机点名案例</font>

> 业务分析：
> 
> 点击开始按钮随机抽取数组的一个数据，放到页面中
> 
> 点击结束按钮删除数组当前抽取到的一个数据
> 
> 当抽取到最后一个数据的时候，两个按钮同时禁用(写在开始里面，只剩最后一个数据不用抽了)
> 
> 核心：利用定时器快速展示，体制定时器结束展示

```html
<head>
    <meta charset="UTF-8">
    <title>饿死的冏猫</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        h2 {
            text-align: center;
        }
        .box {
            width: 600px;
            margin: 50px auto;
            display: flex;
            font-size: 25px;
            line-height: 40px;
        }
        .qs {

            width: 450px;
            height: 40px;
            color: red;
        }
        .btns {
            text-align: center;
        }
        .btns button {
            width: 120px;
            height: 35px;
            margin: 0 50px;
        }
    </style>
</head>
<body>
    <h2>随机点名</h2>
    <div class="box">
        <span>名字是：</span>
        <div class="qs">这里显示姓名</div>
    </div>
    <div class="btns">
        <button class="start">开始</button>
        <button class="end">结束</button>
    </div>

    <script>
        // 数据数组
        const arr = ['顾倾寒', '季莹莹', '胡桃', '妖刀姬', '崔三娘']
        // 定时器的全局变量
        let timerId = 0
        // 随机号要全局变量
        let random = 0
        // 业务1.开始按钮模块
        const qs = document.querySelector('.qs')
        // 1.1 获取开始按钮对象
        const start = document.querySelector('.start')
        // 1.2 添加点击事件
        start.addEventListener('click', function () {
            timerId = setInterval(function () {
                // 随机数
                random = parseInt(Math.random() * arr.length)
                // console.log(arr[random])
                qs.innerHTML = arr[random]
            }, 35)
            // 如果数组里面只有一个值了，还需要抽取吗？  不需要  让两个按钮禁用就可以
            if (arr.length === 1) {
                // start.disabled = true
                // end.disabled = true
                start.disabled = end.disabled = true
            }
        })

        // 2. 关闭按钮模块
        const end = document.querySelector('.end')
        end.addEventListener('click', function () {
            clearInterval(timerId)
            // 结束了，可以删除掉当前抽取的那个数组元素
            arr.splice(random, 1)
            console.log(arr)
        })
    </script>
</body>
```

#### <font color="#2A878F">事件监听版本</font>

- DOM L0
  事件源.on事件 = function() { }

- DOM L2
  事件源.addEventListener(事件， 事件处理函数)

- 区别：
  on方式会被覆盖，addEventListener方式可绑定多次，拥有事件更多特性，推荐使用

```html
<body>
  <button>点击</button>
  <script>
    const btn = document.querySelector('button')
    // btn.onclick = function () {
    //   alert(11)
    // }
    // btn.onclick = function () {
    //   alert(22)
    // }

    // let num = 10
    // num = 20
    btn.addEventListener('click', function () {
      alert(11)
    })
    btn.addEventListener('click', function () {
      alert(22)
    })
  </script>
</body>
```

### <font color="#A9D0D9">事件类型</font>

| 鼠标事件            | 焦点事件       | 键盘事件           | 文本事件         |
| --------------- | ---------- | -------------- | ------------ |
| 鼠标触发            | 表单获得光标     | 键盘触发           | 表单输入触发       |
| click 鼠标点击      | focus 获得焦点 | keydown 键盘按下触发 | input 用户输入事件 |
| mouseenter 鼠标经过 | blur 失去焦点  | keyup 键盘抬起触发   |              |
| mouseleave 鼠标离开 |            |                |              |

#### <font color="#2A878F">鼠标事件</font>

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    div {
      width: 200px;
      height: 200px;
      background-color: pink;
    }
  </style>
</head>

<body>
  <div></div>
  <script>
    const div = document.querySelector('div')
    // 鼠标经过
    div.addEventListener('mouseenter', function () {
      console.log(`轻轻的我来了`)
    })
    // 鼠标离开
    div.addEventListener('mouseleave', function () {
      console.log(`轻轻的我走了`)
    })

  </script>
</body>
```

#### <font color="#2A878F">焦点事件</font>

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <input type="text">
  <script>
    const input = document.querySelector('input')
    input.addEventListener('focus', function () {
      console.log('有焦点触发')
    })
    input.addEventListener('blur', function () {
      console.log('失去焦点触发')
    })
  </script>
</body>
```

案例：

```html
<head>
    <meta charset="UTF-8">
    <title>饿死的冏猫</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        ul {

            list-style: none;
        }
        .mi {
            position: relative;
            width: 223px;
            margin: 100px auto;
        }
        .mi input {
            width: 223px;
            height: 48px;
            padding: 0 10px;
            font-size: 14px;
            line-height: 48px;
            border: 1px solid #e0e0e0;
            outline: none;
        }
        .mi .search {
            border: 1px solid #ff6700;
        }
        .result-list {
            display: none;
            position: absolute;
            left: 0;
            top: 48px;
            width: 223px;
            border: 1px solid #ff6700;
            border-top: 0;
            background: #fff;
        }
        .result-list a {
            display: block;
            padding: 6px 15px;
            font-size: 12px;
            color: #424242;
            text-decoration: none;
        }
        .result-list a:hover {
            background-color: #eee;
        }
    </style>
</head>
<body>
    <div class="mi">
        <input type="search" placeholder="小米笔记本">
        <ul class="result-list">
            <li><a href="#">全部商品</a></li>
            <li><a href="#">小米11</a></li>
            <li><a href="#">小米10S</a></li>
            <li><a href="#">小米笔记本</a></li>
            <li><a href="#">小米手机</a></li>
            <li><a href="#">黑鲨4</a></li>
            <li><a href="#">空调</a></li>
        </ul>
    </div>
    <script>
        // 1. 获取元素
        const input = document.querySelector('[type=search]')
        const ul = document.querySelector('.result-list')
        // console.log(input)
        // 2. 监听事件 获得焦点
        input.addEventListener('focus', function () {
            // ul显示
            ul.style.display = 'block'
            // 添加一个带有颜色边框的类名
            input.classList.add('search')
        })
        // 3. 监听事件 失去焦点
        input.addEventListener('blur', function () {
            ul.style.display = 'none'
            input.classList.remove('search')
        })
    </script>
</body>
```

#### <font color="#2A878F">键盘事件</font>

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>

<body>
  <input type="text">
  <script>
    const input = document.querySelector('input')
    // 1. 键盘事件
    // input.addEventListener('keydown', function () {
    //   console.log('键盘按下了')
    // })
    // input.addEventListener('keyup', function () {
    //   console.log('键盘弹起了')
    // })
    // 2. 用户输入文本事件  input
    input.addEventListener('input', function () {
      //获取用户输入的内容
      console.log(input.value)
    })
  </script>
</body>
```

**focus伪类选择器**

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    input {
      width: 200px;
      transition: all .3s;
    }

    /* focus伪类选择器  获得焦点 */
    input:focus {
      width: 300px;
    }
  </style>
</head>

<body>
  <input type="text">
</body>
```

案例：

> 需求：用户输入文字，可以和·计算用户输入的字数

> 分析：
> 
> 判断用户输入事件 input
> 
> 不断取得文本框里面的字符长度，文本域.value.length
> 
> 把数字给下面文本框

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    .wrapper {
      min-width: 400px;
      max-width: 800px;
      display: flex;
      justify-content: flex-end;
    }
    .avatar {
      width: 48px;
      height: 48px;
      border-radius: 50%;
      overflow: hidden;
      background: url(./images/avatar.jpg) no-repeat center / cover;
      margin-right: 20px;
    }
    .wrapper textarea {
      outline: none;
      border-color: transparent;
      resize: none;
      background: #f5f5f5;
      border-radius: 4px;
      flex: 1;
      padding: 10px;
      transition: all 0.5s;
      height: 30px;
    }
    .wrapper textarea:focus {
      border-color: #e4e4e4;
      background: #fff;
      height: 50px;
    }
    .wrapper button {
      background: #00aeec;
      color: #fff;
      border: none;
      border-radius: 4px;
      margin-left: 10px;
      width: 70px;
      cursor: pointer;
    }
    .wrapper .total {
      margin-right: 80px;
      color: #999;
      margin-top: 5px;
      opacity: 0;
      transition: all 0.5s;
    }
    .list {
      min-width: 400px;
      max-width: 800px;
      display: flex;
    }
    .list .item {
      width: 100%;
      display: flex;
    }
    .list .item .info {
      flex: 1;
      border-bottom: 1px dashed #e4e4e4;
      padding-bottom: 10px;
    }
    .list .item p {
      margin: 0;
    }
    .list .item .name {
      color: #FB7299;
      font-size: 14px;
      font-weight: bold;
    }
    .list .item .text {
      color: #333;
      padding: 10px 0;
    }
    .list .item .time {
      color: #999;
      font-size: 12px;
    }
  </style>
</head>
<body>
  <div class="wrapper">
    <i class="avatar"></i>
    <textarea id="tx" placeholder="发一条友善的评论" rows="2" maxlength="200"></textarea>
    <button>发布</button>
  </div>
  <div class="wrapper">
    <span class="total">0/200字</span>
  </div>
  <div class="list">
    <div class="item" style="display: none;">
      <i class="avatar"></i>
      <div class="info">
        <p class="name">清风徐来</p>
        <p class="text">大家都辛苦啦，感谢各位大大的努力，能圆满完成真是太好了[笑哭][支持]</p>
        <p class="time">2022-10-10 20:29:21</p>
      </div>
    </div>
  </div>
  <script>
    const tx = document.querySelector('#tx')
    const total = document.querySelector('.total')
    // 1. 当我们文本域获得了焦点，就让 total 显示出来
    tx.addEventListener('focus', function () {
      total.style.opacity = 1
    })
    // 2. 当我们文本域失去了焦点，就让 total 隐藏出来
    tx.addEventListener('blur', function () {
      total.style.opacity = 0
    })
    // 3. 检测用户输入
    tx.addEventListener('input', function () {
      // console.log(tx.value.length)  得到输入的长度
      total.innerHTML = `${tx.value.length}/200字`
    })
  </script>
</body>
```

### <font color="#A9D0D9">事件对象</font>

> 任意事件类型被触发时与事件相关的信息会被以对象的形式记录下来，我们称这个对象为事件对象。

语法：

> 在事件绑定的回调函数的第一个参数就是事件对象
> 
> 一般命名为 event ev e
> 
>  `元素.addEventListeren('click',function(e) {})`

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <!-- <button>点击</button> -->
  <input type="text">
  <script>
    // const btn = document.querySelector('button')
    // btn.addEventListener('click', function (e) {
    //   console.log(e)
    // })

    const input = document.querySelector('input')
    input.addEventListener('keyup', function (e) {
      // console.log(11)
      // console.log(e.key)
      if (e.key === 'Enter') {
        console.log('我按下了回车键')
      }
    })
  </script>
</body>
```

#### <font color="#2A878F">常见的事件对象属性</font>

1. `ev.type` 当前事件的类型

2. `ev.clientX/Y` 光标相对浏览器窗口的位置

3. `ev.offsetX/Y` 光标相于当前 DOM 元素的位置

4. `ev.key` 用户按下键盘的值

> 注：在事件回调函数内部通过 window.event 同样可以获取事件对象。

##### <font color="#6163d3">评论回车发布</font>

> 需求：用户输入文字，可以和·计算用户输入的字数

> 分析：
> 
> 用到按下键盘事件 keydown 或 keyup 都可以
> 
> 如果用户按下的是回车键，则发布信息
> 
> 让留言板信息模块显示，把拿到的数据渲染到对应标签内部

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    .wrapper {
      min-width: 400px;
      max-width: 800px;
      display: flex;
      justify-content: flex-end;
    }

    .avatar {
      width: 48px;
      height: 48px;
      border-radius: 50%;
      overflow: hidden;
      background: url(./images/avatar.jpg) no-repeat center / cover;
      margin-right: 20px;
    }

    .wrapper textarea {
      outline: none;
      border-color: transparent;
      resize: none;
      background: #f5f5f5;
      border-radius: 4px;
      flex: 1;
      padding: 10px;
      transition: all 0.5s;
      height: 30px;
    }

    .wrapper textarea:focus {
      border-color: #e4e4e4;
      background: #fff;
      height: 50px;
    }

    .wrapper button {
      background: #00aeec;
      color: #fff;
      border: none;
      border-radius: 4px;
      margin-left: 10px;
      width: 70px;
      cursor: pointer;
    }

    .wrapper .total {
      margin-right: 80px;
      color: #999;
      margin-top: 5px;
      opacity: 0;
      transition: all 0.5s;
    }

    .list {
      min-width: 400px;
      max-width: 800px;
      display: flex;
    }

    .list .item {
      width: 100%;
      display: flex;
    }

    .list .item .info {
      flex: 1;
      border-bottom: 1px dashed #e4e4e4;
      padding-bottom: 10px;
    }

    .list .item p {
      margin: 0;
    }

    .list .item .name {
      color: #FB7299;
      font-size: 14px;
      font-weight: bold;
    }

    .list .item .text {
      color: #333;
      padding: 10px 0;
    }

    .list .item .time {
      color: #999;
      font-size: 12px;
    }
  </style>
</head>

<body>
  <div class="wrapper">
    <i class="avatar"></i>
    <textarea id="tx" placeholder="发一条友善的评论" rows="2" maxlength="200"></textarea>
    <button>发布</button>
  </div>
  <div class="wrapper">
    <span class="total">0/200字</span>
  </div>
  <div class="list">
    <div class="item" style="display: none;">
      <i class="avatar"></i>
      <div class="info">
        <p class="name">清风徐来</p>
        <p class="text">大家都辛苦啦，感谢各位大大的努力，能圆满完成真是太好了[笑哭][支持]</p>
        <p class="time">2022-10-10 20:29:21</p>
      </div>
    </div>
  </div>
  <script>
    const tx = document.querySelector('#tx')
    const total = document.querySelector('.total')
    const item = document.querySelector('.item')
    const text = document.querySelector('.text')
    // 1. 当我们文本域获得了焦点，就让 total 显示出来
    tx.addEventListener('focus', function () {
      total.style.opacity = 1
    })
    // 2. 当我们文本域失去了焦点，就让 total 隐藏出来
    tx.addEventListener('blur', function () {
      total.style.opacity = 0
    })
    // 3. 检测用户输入
    tx.addEventListener('input', function () {
      // console.log(tx.value.length)  得到输入的长度
      total.innerHTML = `${tx.value.length}/200字`
    })

    // 4. 按下回车发布评论
    tx.addEventListener('keyup', function (e) {
      // 只有按下的是回车键，才会触发
      // console.log(e.key)
      if (e.key === 'Enter') {
        // 如果用户输入的不为空就显示和打印
        if (tx.value.trim()) {
          // console.log(11)
          item.style.display = 'block'
          // console.log(tx.value)  // 用户输入的内容
          text.innerHTML = tx.value
        }
        // 等我们按下回车，结束，清空文本域
        tx.value = ''
        // 按下回车之后，就要把 字符统计 复原
        total.innerHTML = '0/200字'
      }

    })
  </script>
</body>
```

##### <font color="#6163d3">trim方法</font>

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>

<body>
  <textarea name="" id="" cols="30" rows="10"></textarea>
  <script>
    const str = '          im a teacher  '
    // console.log(str.trim())  // 去除字符串左右的空格
    const tx = document.querySelector('textarea')
    tx.addEventListener('keyup', function (e) {
      // console.log(tx.value)
      if (e.key === 'Enter') {
        // console.log(tx.value)
        console.log(tx.value.trim() === '')
      }
    })
  </script>
</body>
```

### <font color="#A9D0D9">环境对象this及回调函数</font>

#### <font color="#2A878F">环境对象this</font>

> 环境对象指的是函数内部特殊的变量 `this` ，它代表着当前函数运行时所处的环境。
> 
> 作用：让代码更简洁

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <button>点击</button>
  <script>
    // 每个函数里面都有this 环境对象  普通函数里面this指向的是window
    // function fn() {
    //   console.log(this)
    // }
    // window.fn()
    const btn = document.querySelector('button')
    btn.addEventListener('click', function () {
      // console.log(this)  // btn 对象
      // btn.style.color = 'red'
      this.style.color = 'red'
    })
  </script>
</body>
```

结论：

1. `this` 本质上是一个变量，数据类型为对象

2. 函数的调用方式不同 `this` 变量的值也不同

3. 【谁调用 `this` 就是谁】是判断 `this` 值的粗略规则

4. 函数直接调用时实际上 `window.sayHi()` 所以 `this` 的值为 `window`

#### <font color="#2A878F">回调函数</font>

> 如果将函数 A 做为参数传递给函数 B 时，我们称函数 A 为回调函数。
> 
> 简单理解：当一个函数当作参数来传递给另一个函数的时候，这个函数就是回调函数

```html
<script>
function fn() {
  console.log('我是回调函数')
}
//fn传递给了setInterval，fn就是回调函数
setInterval(fn,1000)
</script>
```

```html
<script>
  // 调用定时器，匿名函数做为参数
  setInterval(function () {
    console.log('我是回调函数...');
  }, 1000);
</script>
```

结论：

1. 回调函数本质还是函数，只不过把它当成参数使用

2. 使用匿名函数做为回调函数比较常见

#### <font color="#2A878F">案例-tab切换</font>

> 分析：
> 
> 主要核心是类的切换，设定一个当前类，可以让当前元素高亮
> 
> 鼠标经过当前选项卡，先移除其余元素身上的当前类，而只给当前元素添加类
> 
> 注意，当前类只能有一个

```html
<head>
  <meta charset="UTF-8" />
  <title>饿死的冏猫</title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    .tab {
      width: 590px;
      height: 340px;
      margin: 20px;
      border: 1px solid #e4e4e4;
    }

    .tab-nav {
      width: 100%;
      height: 60px;
      line-height: 60px;
      display: flex;
      justify-content: space-between;
    }

    .tab-nav h3 {
      font-size: 24px;
      font-weight: normal;
      margin-left: 20px;
    }

    .tab-nav ul {
      list-style: none;
      display: flex;
      justify-content: flex-end;
    }

    .tab-nav ul li {
      margin: 0 20px;
      font-size: 14px;
    }

    .tab-nav ul li a {
      text-decoration: none;
      border-bottom: 2px solid transparent;
      color: #333;
    }

    .tab-nav ul li a.active {
      border-color: #e1251b;
      color: #e1251b;
    }

    .tab-content {
      padding: 0 16px;
    }

    .tab-content .item {
      display: none;
    }

    .tab-content .item.active {
      display: block;
    }
  </style>
</head>

<body>
  <div class="tab">
    <div class="tab-nav">
      <h3>每日特价</h3>
      <ul>
        <li><a class="active" href="javascript:;">精选</a></li>
        <li><a href="javascript:;">美食</a></li>
        <li><a href="javascript:;">百货</a></li>
        <li><a href="javascript:;">个护</a></li>
        <li><a href="javascript:;">预告</a></li>
      </ul>
    </div>
    <div class="tab-content">
      <div class="item active"><img src="#" alt="" /></div>
      <div class="item"><img src="#" alt="" /></div>
      <div class="item"><img src="#" alt="" /></div>
      <div class="item"><img src="#" alt="" /></div>
      <div class="item"><img src="#" alt="" /></div>
    </div>
  </div>
  <script>
    // 1. a 模块制作 要给 5个链接绑定鼠标经过事件
    // 1.1 获取 a 元素 
    const as = document.querySelectorAll('.tab-nav a')
    // console.log(as) 
    for (let i = 0; i < as.length; i++) {
      // console.log(as[i])
      // 要给 5个链接绑定鼠标经过事件
      as[i].addEventListener('mouseenter', function () {
        // console.log('鼠标经过')
        // 排他思想  
        // 干掉别人 移除类active
        document.querySelector('.tab-nav .active').classList.remove('active')
        // 我登基 我添加类 active  this 当前的那个 a 
        this.classList.add('active')

        // 下面5个大盒子 一一对应  .item 
        // 干掉别人
        document.querySelector('.tab-content .active').classList.remove('active')
        // 对应序号的那个 item 显示 添加 active 类
        document.querySelector(`.tab-content .item:nth-child(${i + 1})`).classList.add('active')

      })
    }
  </script>
</body>
```

## <font color="Pink">Third</font>

### <font color="#A9D0D9">表单全选反选案例</font>

> 需求：用户点击全选，则下面复选框全部选择，取消全选则全部取消
> 分析：
> 
> - 全选复选框点击，可以得到当前按钮的 checked
> 
> - 把下面所有的小复选框状态checked，改为和全选复选框一致

```html
<head lang="en">
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    table {
      border-collapse: collapse;
      border-spacing: 0;
      border: 1px solid #c0c0c0;
      width: 500px;
      margin: 100px auto;
      text-align: center;
    }

    th {
      background-color: #09c;
      font: bold 16px "微软雅黑";
      color: #fff;
      height: 24px;
    }

    td {
      border: 1px solid #d0d0d0;
      color: #404060;
      padding: 10px;
    }

    .allCheck {
      width: 80px;
    }
  </style>
</head>

<body>
  <table>
    <tr>
      <th class="allCheck">
        <input type="checkbox" name="" id="checkAll"> <span class="all">全选</span>
      </th>
      <th>商品</th>
      <th>商家</th>
      <th>价格</th>
    </tr>
    <tr>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>小米手机</td>
      <td>小米</td>
      <td>￥1999</td>
    </tr>
    <tr>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>小米净水器</td>
      <td>小米</td>
      <td>￥4999</td>
    </tr>
    <tr>
      <td>
        <input type="checkbox" name="check" class="ck">
      </td>
      <td>小米电视</td>
      <td>小米</td>
      <td>￥5999</td>
    </tr>
  </table>
  <script>
    // 1. 获取大复选框
    const checkAll = document.querySelector('#checkAll')
    // 2. 获取所有的小复选框
    const cks = document.querySelectorAll('.ck')
    // 3. 点击大复选框  注册事件
    checkAll.addEventListener('click', function () {
      // 得到当前大复选框的选中状态
      // console.log(checkAll.checked)  // 得到 是 true 或者是 false
      // 4. 遍历所有的小复选框 让小复选框的checked  =  大复选框的 checked
      for (let i = 0; i < cks.length; i++) {
        cks[i].checked = this.checked
      }
    })
    // 5. 小复选框控制大复选框

    for (let i = 0; i < cks.length; i++) {
      // 5.1 给所有的小复选框添加点击事件
      cks[i].addEventListener('click', function () {
        // 判断选中的小复选框个数 是不是等于  总的小复选框个数
        // 一定要写到点击里面，因为每次要获得最新的个数
        // console.log(document.querySelectorAll('.ck:checked').length)
        // console.log(document.querySelectorAll('.ck:checked').length === cks.length)
        checkAll.checked = document.querySelectorAll('.ck:checked').length === cks.length
      })
    }
  </script>
</body>
```

### <font color="#A9D0D9">事件流</font>

> 事件流是对事件执行过程的描述，了解事件的执行过程有助于加深对事件的理解，提升开发实践中对事件运用的灵活度。

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230709163058167-1965226885.png)

如上图所示，任意事件被触发时总会经历两个阶段：【捕获阶段】和【冒泡阶段】。

简言之，捕获阶段是【从父到子】的传导过程，冒泡阶段是【从子向父】的传导过程。

#### <font color="#2A878F">事件捕获</font>

事件捕获概念(了解即可)：

> 从DOM的根元素开始去执行对应的事件 (从外到里)
> 
> 事件捕获需要写对应代码才能看到效果

语法：

`DOM.addEventListener(事件类型,事件处理函数,是否使用捕获机制)`

说明：

- addEventListener第三个参数传入 true 代表是捕获阶段触发（很少使用）

- 若传入false代表冒泡阶段触发，默认就是false

- 若是用 L0 事件监听，则只有冒泡阶段，没有捕获

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    .father {
      width: 500px;
      height: 500px;
      background-color: pink;
    }

    .son {
      width: 200px;
      height: 200px;
      background-color: purple;
    }
  </style>
</head>

<body>
  <div class="father">
    <div class="son"></div>
  </div>
  <script>
    const fa = document.querySelector('.father')
    const son = document.querySelector('.son')
    // 山东  济南  蓝翔   目标（老师）  捕获阶段
    //  蓝翔  济南   山东   冒泡阶段
    document.addEventListener('click', function () {
      alert('我是爷爷')
    }, true)
    fa.addEventListener('click', function () {
      alert('我是爸爸')
    }, true)
    son.addEventListener('click', function () {
      alert('我是儿子')
    }, true)

  </script>
</body>
```

#### <font color="#2A878F">事件冒泡</font>

事件冒泡概念: 当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。这一过程被称为事件冒泡

- 简单理解：当一个元素触发事件后，会依次向上调用所有父级元素的 同名事件

- 事件冒泡是默认存在的

- L2事件监听第三个参数是 false，或者默认都是冒泡

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    .father {
      width: 500px;
      height: 500px;
      background-color: pink;
    }

    .son {
      width: 200px;
      height: 200px;
      background-color: purple;
    }
  </style>
</head>

<body>
  <div class="father">
    <div class="son"></div>
  </div>
  <script>
    const fa = document.querySelector('.father')
    const son = document.querySelector('.son')
    // 山东  济南  蓝翔   目标（cats老师）  捕获阶段
    //  蓝翔  济南   山东   冒泡阶段
    document.addEventListener('click', function () {
      alert('我是爷爷')
    })
    fa.addEventListener('click', function () {
      alert('我是爸爸')
    })
    son.addEventListener('click', function (e) {
      alert('我是儿子')
    })
  </script>
</body>
```

#### <font color="#2A878F">阻止冒泡</font>

- 问题：因为默认就有冒泡模式的存在，所以容易导致事件影响到父级元素

- 需求：若想把事件就限制在当前元素内，就需要阻止事件冒泡

- 前提：阻止事件冒泡需要拿到事件对象

- 语法：
  `事件对象.stopPropagation()`

- 注意：此方法可以阻断事件流动传播，不光在冒泡阶段有效，捕获阶段也有效

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    .father {
      width: 500px;
      height: 500px;
      background-color: pink;
    }

    .son {
      width: 200px;
      height: 200px;
      background-color: purple;
    }
  </style>
</head>

<body>
  <div class="father">
    <div class="son"></div>
  </div>
  <script>
    const fa = document.querySelector('.father')
    const son = document.querySelector('.son')
    // 山东  济南  蓝翔   目标（cats老师）  捕获阶段
    //  蓝翔  济南   山东   冒泡阶段
    document.addEventListener('click', function () {
      alert('我是爷爷')
    })
    fa.addEventListener('click', function () {
      alert('我是爸爸')
    })
    son.addEventListener('click', function (e) {
      alert('我是儿子')
      // 组织流动传播  事件对象.stopPropagation()
      e.stopPropagation()
    })
  </script>
</body>
```

#### <font color="#2A878F">解绑事件</font>

> on事件方式，直接使用null覆盖就可以实现事件的解绑

语法：

```html
<script>
  //绑定事件
  btn.onclick = function () {
    alter('点击了')
  }
  //解绑事件
  btn.onclick = null;
</script>
```

> addEventListener方式，必须使用：
> 
> removeEventListener(事件类型,事件处理函数,[获取捕获或者冒泡阶段])

```html
<script>
  function fn() {
    alter('点击了')
  }
  //绑定事件
  btn.addEventListener('click',fn)
  //解绑事件
  btn.removeEventListener('click',fn)
</script>
```

> 注意！！！匿名函数无法解绑

示例：

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <button>点击</button>
  <script>
    const btn = document.querySelector('button')
    // btn.onclick = function () {
    //   alert('点击了')
    //   // L0 事件移除解绑
    //   btn.onclick = null
    // }
    function fn() {
      alert('点击了')
    }
    btn.addEventListener('click', fn)
    // L2 事件移除解绑
    btn.removeEventListener('click', fn)
  </script>
</body>
```

#### <font color="#2A878F">鼠标经过事件的区别</font>

> 鼠标经过事件
> 
> mouseover 和 mouseout 会有冒泡效果
> 
> mouseenter 和 mouseleave 没有冒泡效果(推荐)

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    .dad {
      width: 400px;
      height: 400px;
      background-color: pink;
    }
    .baby {
      width: 200px;
      height: 200px;
      background-color: purple;
    }
  </style>
</head>
<body>
  <div class="dad">
    <div class="baby"></div>
  </div>
  <script>
    const dad = document.querySelector('.dad')
    const baby = document.querySelector('.baby')
    // dad.addEventListener('mouseover', function () {
    //   console.log('鼠标经过')
    // })
    // dad.addEventListener('mouseout', function () {
    //   console.log('鼠标离开')
    // })

    dad.addEventListener('mouseenter', function () {
      console.log('鼠标经过')
    })
    dad.addEventListener('mouseleave', function () {
      console.log('鼠标离开')
    })
  </script>
</body>
```

#### <font color="#2A878F">两种注册事件的区别</font>

> 传统on注册（L0）
> 
> 同一个对象,后面注册的事件会覆盖前面注册(同一个事件)
> 
> 直接使用null覆盖偶就可以实现事件的解绑
> 
> 都是冒泡阶段执行的

> 事件监听注册（L2）
> 
> 语法: addEventListener(事件类型, 事件处理函数, 是否使用捕获)
> 
> 后面注册的事件不会覆盖前面注册的事件(同一个事件)
> 
> 可以通过第三个参数去确定是在冒泡或者捕获阶段执行
> 
> 必须使用removeEventListener(事件类型, 事件处理函数, 获取捕获或者冒泡阶段)
> 
> 匿名函数无法被解

### <font color="#A9D0D9">事件委托</font>

> 事件委托是利用事件流的特征解决一些开发需求的知识技巧
> 
> 优点：减少注册次数，可以提高程序性能

> 原理：事件委托其实是利用事件冒泡的特点。
> 
> 给父元素注册事件，当我们触发子元素的时候，会冒泡到父元素身上，从而触发父元素的事件
> 
> 实现：事件对象.target. tagName 可以获得真正触发事件的元素

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>

<body>
  <ul>
    <li>第1个孩子</li>
    <li>第2个孩子</li>
    <li>第3个孩子</li>
    <li>第4个孩子</li>
    <li>第5个孩子</li>
    <p>我不需要变色</p>
  </ul>
  <script>
    // 点击每个小li 当前li 文字变为红色
    // 按照事件委托的方式  委托给父级，事件写到父级身上
    // 1. 获得父元素
    const ul = document.querySelector('ul')
    ul.addEventListener('click', function (e) {
      // alert(11)
      // this.style.color = 'red'
      // console.dir(e.target) // 就是我们点击的那个对象
      // e.target.style.color = 'red'
      // 我的需求，我们只要点击li才会有效果
      if (e.target.tagName === 'LI') {
        e.target.style.color = 'red'
      }
    })
  </script>
</body>
```

### <font color="#A9D0D9">阻止元素的默认行为</font>

> 我们某些情况下需要阻止元素默认行为的发生
> 
> 比如 阻止 链接的跳转，表单域跳转

语法：

`e.preventDefault()`

```html
<form action="htt://www.baidu.com">
  <input type="submit" value="提交">
</form>
<a href="htt://www.baidu.com">百度一下</a>
<script>
  const form = documnet.querySelector('form')
  form.addEventListener('click',function(e){
    //阻止表单默认提交行为
    e.preventDefault()
  })

  const a = documnet.querySelector('a')
  a.addEventListener('click',function(e){
    //阻止表单默认提交行为
    e.preventDefault()
  })
</script>
```

### <font color="#A9D0D9">其他事件</font>

#### <font color="#2A878F">页面加载事件</font>

> 加载外部资源（如图片、外联CSS和JavaScript等）加载完毕时触发的事件

> 为什么要学？
> 
> - 有些时候需要等页面资源全部处理完了做一些事情
> 
> - 老代码喜欢把 script 写在 head 中，这时候直接找 dom 元素找不到

> `事件名：load`
> 
> 监听页面所有资源加载完毕：
> 
> 给 window 添加 load 事件
> 
> `window.addEventListener('load',function(){//执行的操作})`
> 
> 注意：不光可以监听整个页面资源加载完毕，也可以针对某个资源绑定load事件

> 当初始的 HTML 文档被完全加载和解析完成之后，DOMContentLoaded 事件被触发，而无需等待样式表、图像等完全加载
> 
> `事件名：DOMContentLoaded`
> 
> 监听页面DOM加载完毕：
> 
> 给 document 添加 DOMContentLoaded 事

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <script>
    // 等待页面所有资源加载完毕，就回去执行回调函数
    // window.addEventListener('load', function () {
    //   const btn = document.querySelector('button')
    //   btn.addEventListener('click', function () {
    //     alert(11)
    //   })
    // })

    // img.addEventListener('load', function () {
    //   // 等待图片加载完毕，再去执行里面的代码
    // })

    document.addEventListener('DOMContentLoaded', function () {
      const btn = document.querySelector('button')
      btn.addEventListener('click', function () {
        alert(11)
      })
    })
  </script>
</head>
<body>
  <button>点击</button>
</body>
```

总结：

页面加载事件有哪两个？如何添加？

1. load 事件
   
   - 监听整个页面资源给 window 加

2. DOMContentLoaded
   
   - 给 document 加
   
   - 无需等待样式表、图像等完全加载

#### <font color="#2A878F">页面滚动事件</font>

> 滚动条在滚动的时候持续触发的事件
> 
> 为什么要学？
> 
> 很多网页需要检测用户把页面滚动到某个区域后做一些处理， 比如固定导航栏，比如返回顶部
> 
> `事件名：scroll`
> 
> 监听整个页面滚动：
> 
> `window.addEventListener('scroll',function(){//需要执行的操作})`
> 
> 给window或document添加scroll事
> 
> 监听某个元素的内部滚动直接给某个元素加即可

**页面滚动事件-获取位置**

> `scrollLeft和scrollTop （属性）`
> 
> 获取被卷去的大小
> 
> 获取元素内容往左、往上滚出去看不到的距离
> 
> 这两个值是可读写的
> 
> 尽量在scroll事件里面获取被卷去的距离

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230709200434877-893583893.png)

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    body {
      padding-top: 100px;
      height: 3000px;
    }

    div {
      display: none;
      margin: 100px;
      overflow: scroll;
      width: 200px;
      height: 200px;
      border: 1px solid #000;
    }
  </style>
</head>

<body>
  <div>
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
  </div>
  <script>
    const div = document.querySelector('div')
    // 页面滚动事件
    window.addEventListener('scroll', function () {
      // console.log('我滚了')
      // 我想知道页面到底滚动了多少像素， 被卷去了多少  scrollTop
      // 获取html元素写法  
      // document.documentElement  
      // console.log(document.documentElement.scrollTop)
      const n = document.documentElement.scrollTop
      if (n >= 100) {
        div.style.display = 'block'
      } else {
        div.style.display = 'none'
      }
    })
    // const div = document.querySelector('div')
    // div.addEventListener('scroll', function () {
    //   // console.log(111)
    //   // scrollTop 被卷去的头部
    //   console.log(div.scrollTop)
    // })
  </script>
</body>
```

总结：

1. 被卷去的头部或者左侧用那个属性？是否可以读取和修改？
   
   - `scrollTop / scrollLeft`
   
   - 可以读取，也可以修改（赋值）

2. 检测页面滚动的头部距离（被卷去的头部）用那个属性？
   
   - `document.documentElement.scrollTop`

**页面滚动事件-滚动到指定的坐标**

- scroll() 方法可以把内容滚动到指定坐标

语法：

`元素.scrollTo(x,y)`

例如：让页面滚动到 y 轴 1000像素的位置

`window.scrollTo(0,1000)`

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    body {
      height: 3000px;
    }
  </style>
</head>
<body>
  <script>
    document.documentElement.scrollTop = 800
    window.addEventListener('scroll', function () {
      // 必须写到里面
      const n = document.documentElement.scrollTop
      // 得到是什么数据   数字型 不带单位
      // console.log(n)
    })
  </script>
</body>
```

#### <font color="#2A878F">页面尺寸事件</font>

> 会在窗口尺寸改变的时候触发事件：
> 
> resiz

`window.addEventListener('resize',function(){//执行的代码})`

```html
<script>
  // resize 浏览器窗口大小发生变化的时候触发的事件
  window.addEventListener('resize', function () {
    console.log(1)
  })
</script>
```

> 检测屏幕宽度

```html
<script>
window.addEventListener('resize',function(){
  let w = document.documentElement.clientWidth
  console.log(w)
})
</script>
```

##### <font color="#6163d3">获取元素宽高</font>

> 获取宽高：
> 
> 获取元素的可见部分宽高（不包含边框，margin，滚动条等）
> 
> `clientWidth和clientHeight`

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710082223473-2053977461.png)

```html
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    div {
      display: inline-block;
      /* width: 200px; */
      height: 200px;
      background-color: pink;
      padding: 10px;
      border: 20px solid red;
    }
  </style>
</head>

<body>
  <div>123123123123123123123123123123123123123</div>
  <script>
    const div = document.querySelector('div')
    console.log(div.clientWidth)
    // resize 浏览器窗口大小发生变化的时候触发的事件
    window.addEventListener('resize', function () {
      console.log(1)
    })
  </script>
</body>
```

##### <font color="#6163d3">元素尺寸于位置</font>

> 使用场景：
> 
> 前面案例滚动多少距离，都是我们自己算的，最好是页面滚动到某个元素，就可以做某些事。
> 
> 简单说，就是通过js的方式，得到元素在页面中的位置
> 
> 这样我们可以做，页面滚动到这个位置，就可以做某些操作，省去计算了

获取宽高：

- 获取元素的自身宽高、包含元素自身设置的宽高、padding、border

- `offsetWidth和offsetHeight`

- 获取出来的是数值,方便计算

- 注意: 获取的是可视宽高, 如果盒子是隐藏的,获取的结果是0

- 获取位置：

- 获取元素距离自己定位父级元素的左、上距离

- `offsetLeft和offsetTop` 注意是只读属

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710082932877-11587553.png)

> 获取位置：
> 
> 1. offsetLeft和offsetTop 注意是只读属性
>    
>     获取元素距离自己定位父级元素的左、上距离
> 
> 2. element.getBoundingClientRect()
>    
>     方法返回元素的大小及其相对于视口的位置

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    div {
      position: relative;
      width: 200px;
      height: 200px;
      background-color: pink;
      margin: 100px;
    }

    p {
      width: 100px;
      height: 100px;
      background-color: purple;
      margin: 50px;
    }
  </style>
</head>

<body>
  <div>
    <p></p>
  </div>
  <script>
    const div = document.querySelector('div')
    const p = document.querySelector('p')
    // console.log(div.offsetLeft)
    // 检测盒子的位置  最近一级带有定位的祖先元素
    console.log(p.offsetLeft)
  </script>
</body>
```

总结：

1. offsetWidth和offsetHeight是得到元素什么的宽高？
   
   - 内容 + padding + border

2. offsetTop和offsetLeft 得到位置以谁为准？
   
   - 带有定位的父级
   
   - 如果都没有则以 文档左上角 为准

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710084008605-499956045.png)

##### <font color="#6163d3">案例</font>

```html
<head>
    <meta charset="UTF-8">
    <title>饿死的冏猫</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        .content {
            overflow: hidden;
            width: 1000px;
            height: 3000px;
            background-color: pink;
            margin: 0 auto;
        }

        .backtop {
            display: none;
            width: 50px;
            left: 50%;
            margin: 0 0 0 505px;
            position: fixed;
            bottom: 60px;
            z-index: 100;
        }

        .backtop a {
            height: 50px;
            width: 50px;
            background: url(./images/bg2.png) 0 -600px no-repeat;
            opacity: 0.35;
            overflow: hidden;
            display: block;
            text-indent: -999em;
            cursor: pointer;
        }

        .header {
            position: fixed;
            top: -80px;
            left: 0;
            width: 100%;
            height: 80px;
            background-color: purple;
            text-align: center;
            color: #fff;
            line-height: 80px;
            font-size: 30px;
            transition: all .3s;
        }

        .sk {
            width: 300px;
            height: 300px;
            background-color: skyblue;
            margin-top: 500px;
        }
    </style>
</head>

<body>
    <div class="header">我是顶部导航栏</div>
    <div class="content">
        <div class="sk">秒杀模块</div>
    </div>
    <div class="backtop">
        <img src="./images/close2.png" alt="">
        <a href="javascript:;"></a>
    </div>
    <script>
        const sk = document.querySelector('.sk')
        const header = document.querySelector('.header')
        // 1. 页面滚动事件
        window.addEventListener('scroll', function () {
            // 当页面滚动到 秒杀模块的时候，就改变 头部的 top值
            // 页面被卷去的头部 >=  秒杀模块的位置 offsetTop
            const n = document.documentElement.scrollTop
            // if (n >= sk.offsetTop) {
            //     header.style.top = 0
            // } else {
            //     header.style.top = '-80px'
            // }
            header.style.top = n >= sk.offsetTop ? 0 : '-80px'
        })
    </script>
</body>
```

## <font color="Pink">Fourth</font>

### <font color="#A9D0D9">日期对象</font>

#### <font color="#2A878F">实例化</font>

> 日期对象：用来表示时间的对象
> 作用：可以得到当前系统时间

> 在代码中发现了 new 关键字时，一般将这个操作称为实例化
> 
> 创建一个时间对象并获取时间

- 获得当前时间
  
  `const date = new Date()`

- 获得指定时间
  
  `const date = new Date('2023-07-10')`

#### <font color="#2A878F">日期对象方法</font>

> 使用场景：因为日期对象返回的数据我们不能直接使用，所以需要转换为实际开发中常用的格式

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710084719683-2029546633.png)

**案例：页面显示时间**

需求：将当前时间以：YYYY-MM-DD HH:mm 形式显示在页面 2008-08-08 08:08

分析：

1. 调用日期对象方法进行转换

2. 记得数字要补0

3. 字符串拼接后，通过 innerText 给 标签

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    div {
      width: 300px;
      height: 40px;
      border: 1px solid pink;
      text-align: center;
      line-height: 40px;
    }
  </style>
</head>

<body>
  <div></div>
  <script>
    const div = document.querySelector('div')
    function getMyDate() {
      const date = new Date()
      let h = date.getHours()
      let m = date.getMinutes()
      let s = date.getSeconds()
      h = h < 10 ? '0' + h : h
      m = m < 10 ? '0' + m : m
      s = s < 10 ? '0' + s : s
      return `今天是: ${date.getFullYear()}年${date.getMonth() + 1}月${date.getDate()}号 ${h}:${m}:${s}`
    }

    div.innerHTML = getMyDate()
    setInterval(function () {
      div.innerHTML = getMyDate()
    }, 1000)
  </script>
</body>
```

#### <font color="#2A878F">时间戳</font>

> 使用场景： 如果计算倒计时效果，前面方法无法直接计算，需要借助于时间戳完成

> 什么是时间戳:
> 
> 是指1970年01月01日00时00分00秒起至现在的毫秒数，它是一种特殊的计量时间的方式

> 算法：
> 
> 将来的时间戳 - 现在的时间戳 = 剩余时间毫秒数
> 
> 剩余时间毫秒数 转换为 剩余时间的 年月日时分秒 就是 倒计时时间
> 
> 比如 将来时间戳 2000ms - 现在时间戳 1000ms = 1000ms
> 
> 1000ms 转换为就是 0小时0分1

**三种方式获取时间戳：**

1. 使用 getTime() 方法

```html
<script>
  const date = new Date()
  console.log(date.getTime())
</script>
```

2. 简写 +new Date()

```html
<script>
  console.log(+new Date())
</script>
```

3. 使用 Date.now()

无需实例化

但是只能得到当前的时间戳， 而前面两种可以返回指定时

```html
<script>
  console.log(Date.now())
</script>
```

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <script>
    // 1. getTime()
    const date = new Date()
    console.log(date.getTime())
    // 2. +new Date()
    console.log(+new Date())
    // 3. Date.now()
    console.log(Date.now());

    // 2. +new Date()
    console.log(+new Date())
    console.log('-----------------');
    console.log(+new Date('2022-4-1 18:30:00'))

    // 我要根据日期 Day()  0 ~ 6  返回的是 星期一
    const arr = ['星期天', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
    // const date = new Date()
    console.log(arr[new Date().getDay()])
  </script>
</body>
```

##### <font color="#6163d3">案例：毕业倒计时效果</font>

需求：计算到下课还有多少时间

> 分析：
> 
> 用将来时间减去现在时间就是剩余的时间
> 
> 核心： 使用将来的时间戳减去现在的时间戳
> 
> 把剩余的时间转换为 天 时 分 

注意：

1. 通过时间戳得到是毫秒，需要转换为秒在计算

2. 转换公式

```html
d = parseInt(总秒数/ 60/60 /24); // 计算天数

h = parseInt(总秒数/ 60/60 %24) // 计算小时

m = parseInt(总秒数 /60 %60 ); // 计算分数

s = parseInt(总秒数%60); // 计算当前秒
```

```html
<head>
  <meta charset="UTF-8" />
  <title>饿死的冏猫</title>
  <style>
    .countdown {
      width: 240px;
      height: 305px;
      text-align: center;
      line-height: 1;
      color: #fff;
      background-color: brown;
      /* background-size: 240px; */
      /* float: left; */
      overflow: hidden;
    }

    .countdown .next {
      font-size: 16px;
      margin: 25px 0 14px;
    }

    .countdown .title {
      font-size: 33px;
    }

    .countdown .tips {
      margin-top: 80px;
      font-size: 23px;
    }

    .countdown small {
      font-size: 17px;
    }

    .countdown .clock {
      width: 142px;
      margin: 18px auto 0;
      overflow: hidden;
    }

    .countdown .clock span,
    .countdown .clock i {
      display: block;
      text-align: center;
      line-height: 34px;
      font-size: 23px;
      float: left;
    }

    .countdown .clock span {
      width: 34px;
      height: 34px;
      border-radius: 2px;
      background-color: #303430;
    }

    .countdown .clock i {
      width: 20px;
      font-style: normal;
    }
  </style>
</head>

<body>
  <div class="countdown">
    <p class="next">今天是2023年7月10日</p>
    <p class="title">下班倒计时</p>
    <p class="clock">
      <span id="hour">00</span>
      <i>:</i>
      <span id="minutes">25</span>
      <i>:</i>
      <span id="scond">20</span>
    </p>
    <p class="tips">18:30:00下课</p>
  </div>
  <script>
    // 随机颜色函数
    // 1. 自定义一个随机颜色函数
    function getRandomColor(flag = true) {
      if (flag) {
        // 3. 如果是true 则返回 #ffffff
        let str = '#'
        let arr = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f']
        // 利用for循环随机抽6次 累加到 str里面
        for (let i = 1; i <= 6; i++) {
          // 每次要随机从数组里面抽取一个  
          // random 是数组的索引号 是随机的
          let random = Math.floor(Math.random() * arr.length)
          // str = str + arr[random]
          str += arr[random]
        }
        return str

      } else {
        // 4. 否则是 false 则返回 rgb(255,255,255)
        let r = Math.floor(Math.random() * 256)  // 55
        let g = Math.floor(Math.random() * 256)  // 89
        let b = Math.floor(Math.random() * 256)  // 255
        return `rgb(${r},${g},${b})`
      }

    }

    // 页面刷新随机得到颜色
    const countdown = document.querySelector('.countdown')
    countdown.style.backgroundColor = getRandomColor()
    // 函数封装 getCountTime
    function getCountTime() {
      // 1. 得到当前的时间戳
      const now = +new Date()
      // 2. 得到将来的时间戳
      const last = +new Date('2024-7-10 18:30:00')
      // console.log(now, last)
      // 3. 得到剩余的时间戳 count  记得转换为 秒数
      const count = (last - now) / 1000
      // console.log(count)
      // 4. 转换为时分秒
      // h = parseInt(总秒数 / 60 / 60 % 24)   //   计算小时
      // m = parseInt(总秒数 / 60 % 60);     //   计算分数
      // s = parseInt(总秒数 % 60);   
      // let d = parseInt(count / 60 / 60 / 24)               //   计算当前秒数
      let h = parseInt(count / 60 / 60 % 24)
      h = h < 10 ? '0' + h : h
      let m = parseInt(count / 60 % 60)
      m = m < 10 ? '0' + m : m
      let s = parseInt(count % 60)
      s = s < 10 ? '0' + s : s
      console.log(h, m, s)

      //  5. 把时分秒写到对应的盒子里面
      document.querySelector('#hour').innerHTML = h
      document.querySelector('#minutes').innerHTML = m
      document.querySelector('#scond').innerHTML = s
    }
    // 先调用一次
    getCountTime()

    // 开启定时器
    setInterval(getCountTime, 1000)
  </script>
</body>
```

### <font color="#A9D0D9">节点操作</font>

#### <font color="#2A878F">DOM节点</font>

DOM节点

- DOM树里每一个内容都称之为节点

![DOM树](https://img-blog.csdnimg.cn/8d8e0fa6c9ce4f39bdab608400f0e63e.png)

> 节点类型

> 元素节点
> 
> - 所有的标签 比如 body、 div
> 
> - html 是根节

> 属性节点
> 
> - 所有的属性 比如 href

> 文本节点
> 
> - 所有的文本

> 其他

#### <font color="#2A878F">查找节点</font>

> 父节点查找：
> 
> parentNode 属性
> 
> 返回最近一级的父节点 找不到返回为nul
> 
> `子元素.parentNode`

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <div class="yeye">
    <div class="dad">
      <div class="baby">x</div>
    </div>
  </div>
  <script>
    const baby = document.querySelector('.baby')
    console.log(baby)  // 返回dom对象
    console.log(baby.parentNode)  // 返回dom对象
    console.log(baby.parentNode.parentNode)  // 返回dom对象
  </script>
</body>
```

> 子节点查找：
> 
> childNodes
> 
> 获得所有子节点、包括文本节点（空格、换行）、注释节点等
> 
> children 属性 (重点)
> 
> 仅获得所有元素节点
> 
> 返回的还是一个伪数
> 
> `父元素.children`

> 兄弟关系查找：
> 
> 1. 下一个兄弟节点
> 
> `nextElementSibling 属性`
> 
> 2. 上一个兄弟节点
> 
> `previousElementSibling 属性`

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
</head>
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
  </ul>
  <script>
    // const ul = document.querySelector('ul')  // ul
    // console.log(ul.children)  // 得到伪数组  选择的是 亲儿子 
    const li2 = document.querySelector('ul li:nth-child(2)')
    console.log(li2.previousElementSibling)  // 上一个兄弟
    console.log(li2.nextElementSibling)  // 下一个兄弟
  </script>
</body>
```

#### <font color="#2A878F">总结</font>

1. 查找父节点用那个属性？
- `parentNode`
2. 查找所有子节点用那个属性？
- `children`
3. 查找兄弟节点用那个属性？
- `nextElementSibling`

- `previousElementSiblin`

#### <font color="#2A878F">增加节点</font>

很多情况下，我们需要在页面中增加元素

- 比如，点击发布按钮，可以新增一条信息

一般情况下，我们新增节点，按照如下操作：

- 创建一个新的节点

- 把创建的新的节点放入到指定的元素内

##### <font color="#6163d3">创建节点</font>

> 即创造出一个新的网页元素，再添加到网页内，一般先创建节点，然后插入节点
> 
> 创建元素节点方法：
> 
> `document.createElement('标签名')`

##### <font color="#6163d3">追加节点</font>

要想在界面看到，还得插入到某个父元素中

1. 插入到父元素的最后一个子元素:
   
    `父元素.appendChild(要插入的元素)`

2. 插入到父元素中某个子元素的前面
   
    `父元素.insertBefore(要插入的元素,在哪个元素前面)`

```html
<body>
  <ul>
    <li>我是老大</li>
  </ul>
  <script>
    // // 1. 创建节点
    // const div = document.createElement('div')
    // // console.log(div)
    // 2. 追加节点  作为最后一个子元素
    // document.body.appendChild(div)
    const ul = document.querySelector('ul')
    const li = document.createElement('li')
    li.innerHTML = '我是li'
    // ul.appendChild(li)
    // ul.children
    // 3. 追加节点
    // insertBefore(插入的元素, 放到哪个元素的前面)
    ul.insertBefore(li, ul.children[0])
  </script>
</body>
```

#### <font color="#2A878F">克隆节点</font>

特殊情况下，我们新增节点，按照如下操作：

- 复制一个原有的节点

- 把复制的节点放入到指定的元素内部

**克隆节点**

`元素.cloneNode(布尔值)`

> cloneNode会克隆出一个跟原标签一样的元素，括号内传入布尔值
> 
> - 若为true，则代表克隆时会包含后代节点一起克隆
> 
> - 若为false，则代表克隆时不包含后代节点
> 
> - 默认为fals

```html
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
  </ul>
  <script>
    const ul = document.querySelector('ul')
    // 1 克隆节点  元素.cloneNode(true)
    // const li1 = ul.children[0].cloneNode(true)
    // console.log(li1)
    // 2. 追加
    ul.appendChild(ul.children[0].cloneNode(true))
  </script>
</body>
```

#### <font color="#2A878F">删除节点</font>

若一个节点在页面中已不需要时，可以删除它

在 JavaScript 原生DOM操作中，要删除元素必须通过父元素删除

语法：

`父元素.removeChild(要删除的元素)`

> 注：
> 
> 如不存在父子关系则删除不成功
> 
> 删除节点和隐藏节点（display:none） 有区别的： 隐藏节点还是存在的，但是删除，则从html中删除节点

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    .box {
    display: none;
    }
    </style>
    </head>

    <body>
    <div class="box">123</div>
    <ul>
    <li>没用了</li>
    </ul>
    <script>
    const ul = document.querySelector('ul')
    // 删除节点  父元素.removeChlid(子元素)
    ul.removeChild(ul.children[0])
    </script>
    </body>
    ```

    ### <font color="#A9D0D9">案例</font>

    ```html
    <head>
    <meta charset="UTF-8" />
    <title>学生信息管理</title>
    <style>
    * {
      margin: 0;
      padding: 0;
    }

    a {
      text-decoration: none;
      color:#721c24;
    }
    h1 {
      text-align: center;
      color:#333;
      margin: 20px 0;

    }
    table {
      margin:0 auto;
      width: 800px;
      border-collapse: collapse;
      color:#004085;
    }
    th {
      padding: 10px;
      background: #cfe5ff;

      font-size: 20px;
      font-weight: 400;
    }
    td,th {
      border:1px solid #b8daff;
    }
    td {
      padding:10px;
      color:#666;
      text-align: center;
      font-size: 16px;
    }
    tbody tr {
      background: #fff;
    }
    tbody tr:hover {
      background: #e1ecf8;
    }
    .info {
      width: 900px;
      margin: 50px auto;
      text-align: center;
    }
    .info  input, .info select {
      width: 80px;
      height: 27px;
      outline: none;
      border-radius: 5px;
      border:1px solid #b8daff;
      padding-left: 5px;
      box-sizing: border-box;
      margin-right: 15px;
    }
    .info button {
      width: 60px;
      height: 27px;
      background-color: #004085;
      outline: none;
      border: 0;
      color: #fff;
      cursor: pointer;
      border-radius: 5px;
    }
    .info .age {
      width: 50px;
    }
  </style>
</head>
<body>
  <h1>新增学员</h1>
  <form class="info" autocomplete="off">
    姓名：<input type="text" class="uname" name="uname" />
    年龄：<input type="text" class="age" name="age" />
    性别:
    <select name="gender" class="gender">
      <option value="男">男</option>
      <option value="女">女</option>
    </select>
    薪资：<input type="text" class="salary" name="salary" />
    就业城市：<select name="city" class="city">
      <option value="北京">北京</option>
      <option value="上海">上海</option>
      <option value="广州">广州</option>
      <option value="深圳">深圳</option>
      <option value="曹县">曹县</option>
    </select>
    <button class="add">录入</button>
  </form>
  <h1>就业榜</h1>
  <table>
    <thead>
      <tr>
        <th>学号</th>
        <th>姓名</th>
        <th>年龄</th>
        <th>性别</th>
        <th>薪资</th>
        <th>就业城市</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody>
      <!-- 
        <tr>
          <td>1001</td>
          <td>欧阳霸天</td>
          <td>19</td>
          <td>男</td>
          <td>15000</td>
          <td>上海</td>
          <td>
            <a href="javascript:">删除</a>
          </td>
        </tr> 
        -->
    </tbody>
  </table>
  <script>
    // 获取元素
    const uname = document.querySelector('.uname')
    const age = document.querySelector('.age')
    const gender = document.querySelector('.gender')
    const salary = document.querySelector('.salary')
    const city = document.querySelector('.city')
    const tbody = document.querySelector('tbody')
    // 获取所有带有name属性的 元素
    const items = document.querySelectorAll('[name]')
    // 声明一个空的数组， 增加和删除都是对这个数组进行操作
    const arr = []

    // 1. 录入模块
    // 1.1 表单提交事件
    const info = document.querySelector('.info')
    info.addEventListener('submit', function (e) {
      // 阻止默认行为  不跳转
      e.preventDefault()
      // console.log(11)

      // 这里进行表单验证  如果不通过，直接中断，不需要添加数据
      // 先遍历循环
      for (let i = 0; i < items.length; i++) {
        if (items[i].value === '') {
          return alert('输入内容不能为空')
        }
      }
      // 创建新的对象
      const obj = {
        stuId: arr.length + 1,
        uname: uname.value,
        age: age.value,
        gender: gender.value,
        salary: salary.value,
        city: city.value
      }
      // console.log(obj)
      // 追加给数组里面
      arr.push(obj)
      // console.log(arr)
      // 清空表单  重置 
      this.reset()
      // 调用渲染函数
      render()
    })

    // 2. 渲染函数 因为增加和删除都需要渲染
    function render() {
      // 先清空tbody 以前的行 ，把最新数组里面的数据渲染完毕 
      tbody.innerHTML = ''
      // 遍历arr数组
      for (let i = 0; i < arr.length; i++) {
        // 生成 tr 
        const tr = document.createElement('tr')
        tr.innerHTML = `
          <td>${arr[i].stuId}</td>
          <td>${arr[i].uname}</td>
          <td>${arr[i].age}</td>
          <td>${arr[i].gender}</td>
          <td>${arr[i].salary}</td>
          <td>${arr[i].city}</td>
          <td>
            <a href="javascript:" data-id=${i}>删除</a>
          </td>
        `
        // 追加元素  父元素.appendChild(子元素)
        tbody.appendChild(tr)
      }
    }

    // 3. 删除操作
    // 3.1 事件委托 tbody
    tbody.addEventListener('click', function (e) {
      if (e.target.tagName === 'A') {
        // 得到当前元素的自定义属性 data-id
        // console.log(e.target.dataset.id)
        // 删除arr 数组里面对应的数据
        arr.splice(e.target.dataset.id, 1)
        console.log(arr)
        // 从新渲染一次
        render()
      }
    })
  </script>
</body>
```

## <font color="Pink">Fifth</font>

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710095147957-1753875923.png)

### <font color="#A9D0D9">定时器-延时函数</font>

> JavaScript 内置的一个用来让代码延迟执行的函数，叫 setTimeout

语法：

`setTimeout(回调函数,等待的毫秒数)`

setTimeout 仅仅只执行一次，所以可以理解为就是把一段代码延迟执行, 平时省略window

清除延时函数:

```html
<script>
  let timer = setTimeout(回调函数,等待的毫秒数)
  clearTimeout(timer)
</script>
```

> 注意点
> 
> - 延时器需要等待,所以后面的代码先执行
> 
> - 每一次调用延时器都会产生一个新的延时器

> 两种定时器对比：执行的次数
> 
> - 延时函数: 执行一次
> 
> - 间歇函数:每隔一段时间就执行一次,除非手动清除

### <font color="#A9D0D9">JS执行机制</font>

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710095805798-995998452.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710095830465-602171344.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710095906814-2116771134.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710095956916-356191858.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710100022728-311240680.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710100051745-133742022.png)

### <font color="#A9D0D9">location对象</font>

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710100159771-915306414.png)

> location 的数据类型是对象，它拆分并保存了 URL 地址的各个组成部分
> 
> 常用属性和方法：
> 
> href 属性获取完整的 URL 地址，对其赋值时用于地址的跳转

```html
<script>
  //可以得到当前文件URL地址
  console.log(location.href)
  //可以通过js方式跳转到目标地址
  location.href = 'http://www.baidu.com'
</script>
```

> location 的数据类型是对象，它拆分并保存了 URL 地址的各个组成部分
> 
> 常用属性和方法：
> 
> search 属性获取地址中携带的参数，符号 ？后面
> 
> `console.log(location.search)`

> location 的数据类型是对象，它拆分并保存了 URL 地址的各个组成部分
> 
> 常用属性和方法：
> 
> hash 属性获取地址中的哈希值，符号 # 后面部分
> `console.log(location.has)`
> 后期vue路由的铺垫，经常用于不刷新页面，显示不同页面，比如 网易云

> location 的数据类型是对象，它拆分并保存了 URL 地址的各个组成部分
> 
> 常用属性和方法：
> 
> reload 方法用来刷新当前页面，传入参数 true 时表示强制

```html
<button>点击刷新</button>
<script>
  let btn = document.querySelector('butten')
  btn.addEventListener('click',function(){
    location.reload(true)
    //强制刷新 类似 ctrl + f5
  })
</script>
```

#### <font color="#2A878F">总结</font>

> location.href 属性获取完整的 URL 地址，对其赋值时用于地址的跳转
> 
> search 属性获取地址中携带的参数，符号 ？后面部分
> 
> hash 属性获取地址中的啥希值，符号 # 后面部分
> 
> reload 方法用来刷新当前页面，传入参数 true 时表示强制刷新

#### <font color="#2A878F">案例</font>

5秒钟之后跳转的页面

> 需求：用户点击可以跳转，如果不点击，则5秒之后自动跳转，要求里面有秒数倒计时

分析：

①：目标元素是链接

②：利用定时器设置数字倒计时

③：时间到了，自动跳转到新的页面

```html
<head>
  <meta charset="UTF-8">
  <title>饿死的冏猫</title>
  <style>
    span {
      color: red;
    }
  </style>
</head>

<body>
  <a href="http://www.baidu.com">支付成功<span>5</span>秒钟之后跳转到首页</a>
  <script>
    // 1. 获取元素
    const a = document.querySelector('a')
    // 2.开启定时器
    // 3. 声明倒计时变量
    let num = 5
    let timerId = setInterval(function () {
      num--
      a.innerHTML = `支付成功<span>${num}</span>秒钟之后跳转到首页`
      // 如果num === 0 则停止定时器，并且完成跳转功能
      if (num === 0) {
        clearInterval(timerId)
        // 4. 跳转  location.href
        location.href = 'http://www.baidu.com'
      }
    }, 1000)
  </script>
</body>
```

### <font color="#A9D0D9">navigator对象</font>

> navigator的数据类型是对象，该对象下记录了浏览器自身的相关信息
> 
> 常用属性和方法：
> 
> 通过 userAgent 检测浏览器的版本及平台

```html
<script>
  // 检测 userAgent（浏览器信息）
  !(function () {
    const userAgent = navigator.userAgent
    // 验证是否为Android或iPhone
    const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
    const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
    // 如果是Android或iPhone，则跳转至移动站点
    if (android || iphone) {
      location.href = 'http://www.baidu.com'
    }
  })();
  // !(function () { })();
  !function () { }()
</script>
```

### <font color="#A9D0D9">histroy对象</font>

> history 的数据类型是对象，主要管理历史记录， 该对象与浏览器地址栏的操作相对应，如前进、后退、历史记录等

常用属性和方法：

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710102101113-2145280640.png)

```html
<body>
  <button>后退</button>
  <button>前进</button>
  <script>
    const back = document.querySelector('button:first-child')
    const forward = back.nextElementSibling
    back.addEventListener('click', function () {
      // 后退一步
      // history.back()
      history.go(-1)
    })
    forward.addEventListener('click', function () {
      // 前进一步
      // history.forward()
      history.go(1)
    })
  </script>
</body>
```

### <font color="#A9D0D9">本地存储</font>

> 目标： 能够使用localStorage 把数据存储的浏览器中
> 
> 作用: 可以将数据永久存储在本地(用户的电脑), 除非手动删除，否则关闭页面也会存在
> 
> 特性：
> 
> 可以多窗口（页面）共享（同一浏览器可以共享）
> 
> 以键值对的形式存储使用

语法:

存储数据：

`localStorage.setItem(key, value)`

获取数据:

`localStorage.getItem(key)`

删除数据：

`localStorage.removeItem(key)`

浏览器查看本地数据：

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710102726690-924223280.png)

> 特性：
> 
> 生命周期为关闭浏览器窗口
> 
> 在同一个窗口(页面)下数据可以共享
> 
> 以键值对的形式存储使用
> 
> 用法跟localStorage 基本相同

```html
<body>
  <script>
    // 1. 要存储一个名字  'uname'， 'cats老师'
    // localStorage.setItem('键'，'值')
    localStorage.setItem('uname', 'cats老师')
    // 2. 获取方式  都加引号
    console.log(localStorage.getItem('uname'))
    // 3. 删除本地存储  只删除名字
    // localStorage.removeItem('uname')
    // 4. 改  如果原来有这个键，则是改，如果么有这个键是增
    localStorage.setItem('uname', 'red老师')

    // 我要存一个年龄
    // 2. 本地存储只能存储字符串数据类型
    localStorage.setItem('age', 18)
    console.log(localStorage.getItem('age'))
  </script>
</body>
```

#### <font color="#2A878F">总结</font>

1. localStorage 作用是什么？
   
   - 可以将数据永久存储在本地(用户的电脑), 除非手动删除，否则关闭页面也会存在

2. localStorage 存储，获取，删除的语法是什么？
   
   - 存储：`localStorage.setItem(key, value)`
   
   - 获取：`localStorage.getItem(key)`
   
   - 删除：`localStorage.removeItem(key)`

#### <font color="#2A878F">存储复杂数据类型</font>

> 本地只能存储字符串,无法存储复杂数据类型.
> 
> 解决：需要将复杂数据类型转换成JSON字符串,在存储到本地
> 
> 语法：JSON.stringify(复杂数据类型)

```html
<script>
  const goods = {
    name: '小米10',
    price: 1999
  }
  localStorage.setItem('goods',JSON.stringify(goods))
</script>
```

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710103316468-1773580814.png)

> 问题：因为本地存储里面取出来的是字符串，不是对象，无法直接使用

```html
<script>
  const obj = localStorage.getItem('goods')
  console.log(obj)
</script>
```

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710103602982-168431250.png)

解决：把取出来的字符串转换为对象

语法：JSON.parse(JSON字符串)

```html
<script>
const obj = JSON.parse(localStorage.getItem('goods'))
console.log(obj)
</script>
```

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710143053112-2090876491.png)

案例：

```html
<body>
  <script>
    const obj = {
      uname: 'cats老师',
      age: 18,
      gender: '女'
    }
    // // 存储 复杂数据类型  无法直接使用
    // localStorage.setItem('obj', obj)  [object object]    
    // // 取
    // console.log(localStorage.getItem('obj'))

    // 1.复杂数据类型存储必须转换为 JSON字符串存储
    localStorage.setItem('obj', JSON.stringify(obj))
    // JSON 对象  属性和值有引号，而是引号统一是双引号
    // {"uname":"cats老师","age":18,"gender":"女"}
    // 取
    // console.log(typeof localStorage.getItem('obj'))
    // 2. 把JSON字符串转换为 对象
    const str = localStorage.getItem('obj') // {"uname":"cats老师","age":18,"gender":"女"}
    console.log(JSON.parse(str))
  </script>
</body>
```

### <font color="#A9D0D9">map方法(迭代数组)</font>

> 作用：map 迭代数组
> 
> map 可以遍历数组处理数据，并且返回新的数组

语法：

```html
<script>
  const arr = ['red', 'blue', 'cats']
  // 1. 数组 map方法 处理数据并且 返回一个数组
   const newArr = arr.map(function (ele, index) {
    // console.log(ele)  // 数组元素
    // console.log(index) // 索引号
    return ele + '颜色'
    })
console.log(newArr)
</script>
```

> map 也称为映射。映射是个术语，指两个元素的集之间元素相互'对应'的关系。
> 
> map重点在于有返回值，forEach没有返回值（undefined）

```html
<script>
  const arr = ['red', 'blue', 'green']
  // map 方法也是遍历  处理数据  可以返回一个数组
  const newArr = arr.map(function (item, i) {
    // console.log(item)  // 数组元素  'red'
    // console.log(i)  // 下标
    return item + '老师'
  })
  console.log(newArr)

  ['red老师', 'blue老师', 'green老师']

  const arr1 = [10, 20, 30]
  const newArr1 = arr1.map(function (item) {
    return item + 10
  })
  console.log(newArr1)
</script>
```

### <font color="#A9D0D9">join方法</font>

> 作用：join() 方法用于把数组中的所有元素转换一个字符串

语法：

```html
<script>
const arr = ['red颜色','blue颜色','green颜色']
console.log(arr.join(''))
</script>
```

> 数组元素是通过参数里面指定的分隔符进行分隔的，空字符串(''),则所有元素之间都没有任何字符

```html
<body>
  <script>
    const arr = ['red', 'blue', 'green']
    // 把数组元素转换为字符串
    console.log(arr.join()) //red,blue,green
    //空的字符则没有分隔符
    console.log(arr.join('')) //redbluegreen
    console.log(arr.join('*')) //red*blue*green
  </script>
</body>
```

## <font color="Pink">Sixth</font>

### <font color="#A9D0D9"> 正则表达式</font>

> **正则表达式**（Regular Expression）是一种字符串匹配的模式（规则）

**定义正则表达式语法：**

`const reg =  /表达式/`

- 其中` /   / `是正则表达式字面量

- 正则表达式也是`对象 `

**使用正则**

- `test()方法`   用来查看正则表达式与指定的字符串是否匹配

- 如果正则表达式与指定的字符串匹配 ，返回`true`，否则`false`

```html
<script>
  // 正则表达式的基本使用
  const str = 'web前端开发'
  // 1. 定义规则
  const reg = /web/

  // 2. 使用正则  test()
  console.log(reg.test(str))  // true  如果符合规则匹配上则返回true
  console.log(reg.test('java开发'))  // false  如果不符合规则匹配上则返回 false
</script>
```

**检索（查找）符合规则的字符串：** (了解)

> exec() 方法 在一个指定字符串中执行一个搜索匹配

语法：

`regObj.exec(被检测字符串)`

如果匹配成功，exec() 方法返回一个数组，否则返回null

```html
<script>
  const str = '我们在学习前端，希望学习前端能高薪毕业'
  // 正则表达式使用：
  // 1. 定义规则
  const reg = /前端/
  // 2. exec()
  console.log(reg.exec(str))  // 返回数组
</script>
```

### <font color="#A9D0D9">元字符</font>

**普通字符:**

- 大多数的字符仅能够描述它们本身，这些字符称作普通字符，例如所有的字母和数字。

- 普通字符只能够匹配字符串中与它们相同的字符。    

- 比如，规定用户只能输入英文26个英文字母，普通字符的话  /[abcdefghijklmnopqrstuvwxyz]/

**元字符(特殊字符)**

- 是一些具有特殊含义的字符，可以极大提高了灵活性和强大的匹配功能。

- 比如，规定用户只能输入英文26个英文字母，换成元字符写法： /[a-z]/  

#### <font color="#2A878F">边界符</font>

> 正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710151135271-839432617.png)

> 如果 ^ 和 $ 在一起，表示必须是精确匹配

```html
<script>
  // 元字符之边界符
  // 1. 匹配开头的位置 ^
  const reg = /^web/
  console.log(reg.test('web前端'))  // true
  console.log(reg.test('前端web'))  // false
  console.log(reg.test('前端web学习'))  // false
  console.log(reg.test('we'))  // false

  // 2. 匹配结束的位置 $
  const reg1 = /web$/
  console.log(reg1.test('web前端'))  //  false
  console.log(reg1.test('前端web'))  // true
  console.log(reg1.test('前端web学习'))  // false
  console.log(reg1.test('we'))  // false  

  // 3. 精确匹配 ^ $
  const reg2 = /^web$/
  console.log(reg2.test('web前端'))  //  false
  console.log(reg2.test('前端web'))  // false
  console.log(reg2.test('前端web学习'))  // false
  console.log(reg2.test('we'))  // false 
  console.log(reg2.test('web'))  // true
  console.log(reg2.test('webweb'))  // flase 
</script>
```

#### <font color="#2A878F">量词</font>

> 量词用来设定某个模式重复次数

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710151402940-989052293.png)

> 注意： 逗号左右两侧千万不要出现空格

```html
<script>
  // 元字符之量词
  // 1. * 重复次数 >= 0 次
  const reg1 = /^w*$/
  console.log(reg1.test(''))  // true
  console.log(reg1.test('w'))  // true
  console.log(reg1.test('ww'))  // true
  console.log('-----------------------')

  // 2. + 重复次数 >= 1 次
  const reg2 = /^w+$/
  console.log(reg2.test(''))  // false
  console.log(reg2.test('w'))  // true
  console.log(reg2.test('ww'))  // true
  console.log('-----------------------')

  // 3. ? 重复次数  0 || 1 
  const reg3 = /^w?$/
  console.log(reg3.test(''))  // true
  console.log(reg3.test('w'))  // true
  console.log(reg3.test('ww'))  // false
  console.log('-----------------------')


  // 4. {n} 重复 n 次
  const reg4 = /^w{3}$/
  console.log(reg4.test(''))  // false
  console.log(reg4.test('w'))  // flase
  console.log(reg4.test('ww'))  // false
  console.log(reg4.test('www'))  // true
  console.log(reg4.test('wwww'))  // false
  console.log('-----------------------')

  // 5. {n,} 重复次数 >= n 
  const reg5 = /^w{2,}$/
  console.log(reg5.test(''))  // false
  console.log(reg5.test('w'))  // false
  console.log(reg5.test('ww'))  // true
  console.log(reg5.test('www'))  // true
  console.log('-----------------------')

  // 6. {n,m}   n =< 重复次数 <= m
  const reg6 = /^w{2,4}$/
  console.log(reg6.test('w'))  // false
  console.log(reg6.test('ww'))  // true
  console.log(reg6.test('www'))  // true
  console.log(reg6.test('wwww'))  // true
  console.log(reg6.test('wwwww'))  // false

  // 7. 注意事项： 逗号两侧千万不要加空格否则会匹配失败

</script>
```

##### <font color="#6163d3">范围</font>

> 表示字符的范围，定义的规则限定在某个范围，比如只能是英文字母，或者数字等等，用表示范围

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710151704792-1803286149.png)

```html
  <script>
    // 元字符之范围  []  
    // 1. [abc] 匹配包含的单个字符， 多选1
    const reg1 = /^[abc]$/
    console.log(reg1.test('a'))  // true
    console.log(reg1.test('b'))  // true
    console.log(reg1.test('c'))  // true
    console.log(reg1.test('d'))  // false
    console.log(reg1.test('ab'))  // false

    // 2. [a-z] 连字符 单个
    const reg2 = /^[a-z]$/
    console.log(reg2.test('a'))  // true
    console.log(reg2.test('p'))  // true
    console.log(reg2.test('0'))  // false
    console.log(reg2.test('A'))  // false
    // 想要包含小写字母，大写字母 ，数字
    const reg3 = /^[a-zA-Z0-9]$/
    console.log(reg3.test('B'))  // true
    console.log(reg3.test('b'))  // true
    console.log(reg3.test(9))  // true
    console.log(reg3.test(','))  // flase

    // 用户名可以输入英文字母，数字，可以加下划线，要求 6~16位
    const reg4 = /^[a-zA-Z0-9_]{6,16}$/
    console.log(reg4.test('abcd1'))  // false 
    console.log(reg4.test('abcd12'))  // true
    console.log(reg4.test('ABcd12'))  // true
    console.log(reg4.test('ABcd12_'))  // true

    // 3. [^a-z] 取反符
    const reg5 = /^[^a-z]$/
    console.log(reg5.test('a'))  // false 
    console.log(reg5.test('A'))  // true
    console.log(reg5.test(8))  // true

  </script>
```

#### <font color="#2A878F">字符类</font>

> 某些常见模式的简写方式，区分字母和数字

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710151855588-1273017070.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710151934074-1936386293.png)

### <font color="#A9D0D9">替换和修饰符</font>

> replace 替换方法，可以完成字符的替换

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710152249614-468047005.png)

```html
  <script>
    // 替换和修饰符
    const str = '欢迎大家学习前端，相信大家一定能学好前端，都成为前端大神'
    // 1. 替换  replace  需求：把前端替换为 web
    // 1.1 replace 返回值是替换完毕的字符串
    // const strEnd = str.replace(/前端/, 'web') 只能替换一个
  </script>
```

> 修饰符约束正则执行的某些细节行为，如是否区分大小写、是否支持多行匹配等
> 
> - i 是单词 ignore 的缩写，正则匹配时字母不区分大小写
> 
> - g 是单词 global 的缩写，匹配所有满足正则表达式的结果

```html
  <script>
    // 替换和修饰符
    const str = '欢迎大家学习前端，相信大家一定能学好前端，都成为前端大神'
    // 1. 替换  replace  需求：把前端替换为 web
    // 1.1 replace 返回值是替换完毕的字符串
    // const strEnd = str.replace(/前端/, 'web') 只能替换一个

    // 2. 修饰符 g 全部替换
    const strEnd = str.replace(/前端/g, 'web')
    console.log(strEnd) 
  </script>
```

**change 事件**

给input注册 change 事件，值被修改并且失去焦点后触发

**判断是否有类**

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230710152547697-1561920213.png)

`元素.classList.contains()` 看看有没有包含某个类，如果有则返回true，么有则返回false


