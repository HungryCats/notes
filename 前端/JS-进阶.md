# <font color="Red">JS-进阶</font>

## <font color="Pink">First</font>

### <font color="#A9D0D9">作用域</font>

> 了解作用域对程序执行的影响及作用域链的查找机制，使用闭包函数创建隔离作用域避免全局变量污染。
> 
> 作用域（scope）规定了变量能够被访问的“范围”，离开了这个“范围”变量便不能被访问，作用域分为全局作用域和局部作用域。

#### <font color="#2A878F">局部作用域</font>

> 局部作用域分为函数作用域和块作用域。

##### <font color="#6163d3">函数作用域</font>

在函数内部声明的变量只能在函数内部被访问，外部无法直接访问。

```html
<script>
    function getSum() {
        //函数内部是函数作用域 属于局部变量
        const num = 10
    }
    console.log(num) // 此处报错 函数外部不能使用局部作用域变量
</script>
```

总结：

1. 函数内部声明的变量，在函数外部无法被访问

2. 函数的参数也是函数内部的局部变量

3. 不同函数内部声明的变量无法互相访问

4. 函数执行完毕后，函数内部的变量实际被清空了

##### <font color="#6163d3">块级作用域</font>

> 在 JavaScript 中使用 `{}` 包裹的代码称为代码块，代码块内部声明的变量外部将【有可能】无法被访问。

```html
<script>
  {
    // age 只能在该代码块中被访问
    let age = 18;
    console.log(age); // 正常
  }

  // 超出了 age 的作用域
  console.log(age) // 报错

  let flag = true;
  if(flag) {
    // str 只能在该代码块中被访问
    let str = 'hello world!'
    console.log(str); // 正常
  }

  // 超出了 age 的作用域
  console.log(str); // 报错

  for(let t = 1; t <= 6; t++) {
    // t 只能在该代码块中被访问
    console.log(t); // 正常
  }

  // 超出了 t 的作用域
  console.log(t); // 报错
</script>
```

> JavaScript 中除了变量外还有常量，常量与变量本质的区别是【常量必须要有值且不允许被重新赋值】，常量值为对象时其属性和方法允许重新赋值。

```html
<script>
  // 必须要有值
  const version = '1.0.0';

  // 不能重新赋值
  // version = '1.0.1';

  // 常量值为对象类型
  const user = {
    name: '小明',
    age: 18
  }

  // 不能重新赋值
  user = {};

  // 属性和方法允许被修改
  user.name = '小小明';
  user.gender = '男';
</script>
```

总结：

1. `let` 声明的变量会产生块作用域，`var` 不会产生块作用域

2. `const` 声明的常量也会产生块作用域

3. 不同代码块之间的变量无法互相访问

4. 推荐使用 `let` 或 `const`

注：开发中 `let` 和 `const` 经常不加区分的使用，如果担心某个值会不小被修改时，则只能使用 `const` 声明成常量。

#### <font color="#2A878F">全局作用域</font>

> `<script>` 标签和 `.js` 文件的【最外层】就是所谓的全局作用域，在此声明的变量在函数内部也可以被访问。

```html
<script>
  // 此处是全局

  function sayHi() {
    // 此处为局部
  }

  // 此处为全局
</script>
```

> 全局作用域中声明的变量，任何其它作用域都可以被访问，如下代码所示：

```html
<script>
    // 全局变量 name
    const name = '小明'

      // 函数作用域中访问全局
    function sayHi() {
      // 此处为局部
      console.log('你好' + name)
    }

    // 全局变量 flag 和 x
    const flag = true
    let x = 10

      // 块作用域中访问全局
    if(flag) {
      let y = 5
      console.log(x + y) // x 是全局的
    }
</script>
```

总结：

1. 为 `window` 对象动态添加的属性默认也是全局的，不推荐！

2. 函数中未使用任何关键字声明的变量为全局变量，不推荐！！！

3. 尽可能少的声明全局变量，防止全局变量被污染

#### <font color="#2A878F">作用域链</font>

作用域链本质上是底层的变量查找机制。

- 在函数被执行时，会优先查找当前函数作用域中查找变量。

- 如果当前作用域查找不到则会依次逐级查找父级作用域直到全局作用域，

```html
<script>
  // 全局作用域
  let a = 1
  let b = 2

  // 局部作用域
  function f() {
    let c
    // let a = 10;
    console.log(a) // 1 或 10
    console.log(d) // 报错

    // 局部作用域
    function g() {
      let d = 'yo'
      // let b = 20;
      console.log(b) // 2 或 20
    }

    // 调用 g 函数
    g()
  }

  console.log(c) // 报错
  console.log(d) // 报错

  f();
</script>
```

总结：

1. 嵌套关系的作用域串联起来形成了作用域链

2. 相同作用域链中按着从小到大的规则查找变量

3. 子作用域能够访问父作用域，父级作用域无法访问子级作用域

#### <font color="#2A878F">垃圾回收机制</font>

> 垃圾回收机制(Garbage Collection) 简称 GC
> 
> JS中内存的分配和回收都是自动完成的，内存在不使用的时候会被垃圾回收器自动回收。
> 
> 不再用到的内存，没有及时释放，就叫做内存泄漏（内存无法被回收）的情况

JS环境中分配的内存, 一般有如下生命周期：

1. 内存分配：当我们声明变量、函数、对象的时候，系统会自动为他们分配内存

2. 内存使用：即读写内存，也就是使用变量、函数等

3. 内存回收：使用完毕，由垃圾回收自动回收不再使用的内存

4. 说明：
- 全局变量一般不会回收(关闭页面回收)；

- 一般情况下局部变量的值, 不用了, 会被自动回收

##### <font color="#6163d3">算法说明</font>

堆栈空间分配区别：

1. 栈（操作系统）: 由操作系统自动分配释放函数的参数值、局部变量等，基本数据类型放到栈里面。

2. 堆（操作系统）: 一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收。复杂数据类型放到堆里面。

两种常见的浏览器垃圾回收算法: 引用计数法 和 标记清除法

**引用计数法**

IE采用的引用计数算法, 定义“内存不再使用”，就是看一个对象是否有指向它的引用，没有引用了就回收对象
算法：

1. 跟踪记录被引用的次数

2. 如果被引用了一次，那么就记录次数1,多次引用会累加 ++

3. 如果减少一个引用就减1 --

4. 如果引用次数是0 ，则释放内存

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711111303533-1020577809.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711111322910-2124765153.png)

但它却存在一个致命的问题：嵌套引用（循环引用）

如果两个对象相互引用，尽管他们已不再使用，垃圾回收器不会进行回收，导致内存泄露。

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711111406988-153767273.png)

因为他们的引用次数永远不会是0。这样的相互引用如果说很大量的存在就会导致大量的内存泄露

**标记清除法**

现代的浏览器已经不再使用引用计数算法了。

现代浏览器通用的大多是基于标记清除算法的某些改进算法，总体思想都是一致的。

核心：

1. 标记清除算法将“不再使用的对象”定义为“无法达到的对象”。

2. 就是从根部（在JS中就是全局对象）出发定时扫描内存中的对象。 凡是能从根部到达的对象，都是还需要使用的。

3. 那些无法由根部出发触及到的对象被标记为不再使用，稍后进行回收。

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711111955919-1157770497.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711112055256-1758887149.png)

#### <font color="#2A878F">闭包</font>

> 闭包是一种比较特殊和函数，使用闭包能够访问函数作用域中的变量。从代码形式上看闭包是一个做为返回值的函数。
> 
> 闭包 = 内层函数 + 外层函数的变量

> 闭包作用：封闭数据，提供操作，外部也可以访问函数内部的变量

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711141235436-1135640625.png)

```html
<body>
  <script>
    // 1. 闭包 : 内层函数 + 外层函数变量
    // function outer() {
    //   const a = 1
    //   function f() {
    //     console.log(a)
    //   }
    //   f()
    // }
    // outer()

    // 2. 闭包的应用： 实现数据的私有。统计函数的调用次数
    // let count = 1
    // function fn() {
    //   count++
    //   console.log(`函数被调用${count}次`)
    // }

    // 3. 闭包的写法  统计函数的调用次数
    function outer() {
      let count = 1
      function fn() {
        count++
        console.log(`函数被调用${count}次`)
      }
      return fn
    }
    const re = outer()
    // const re = function fn() {
    //   count++
    //   console.log(`函数被调用${count}次`)
    // }
    re()
    re()
    // const fn = function() { }  函数表达式
    // 4. 闭包存在的问题： 可能会造成内存泄漏
  </script>
</body>
```

闭包的作用？

- 封闭数据，实现数据私有，外部也可以访问函数内部的变量

- 闭包很有用，因为它允许将函数与其所操作的某些数据（环境）关联起来

闭包可能引起的问题？

- 内存泄漏

#### <font color="#2A878F">变量提升</font>

变量提升是 JavaScript 中比较“奇怪”的现象，它允许在变量声明之前即被访问。

```html
  <script>
    // 1. 把所有var声明的变量提升到 当前作用域的最前面
    // 2. 只提升声明， 不提升赋值
    // var num
    // console.log(num + '件')
    // num = 10
    // console.log(num)

    function fn() {
      console.log(num)
      var num = 10
    }
    fn()
  </script>
```

总结：

1. 变量在未声明即被访问时会报语法错误

2. 变量在声明之前即被访问，变量的值为 `undefined`

3. `let` 声明的变量不存在变量提升，推荐使用 `let`

4. 变量提升出现在相同作用域当中,只提升声明， 不提升赋值

5. 实际开发中推荐先声明再访问变量

### <font color="#A9D0D9">函数</font>

#### <font color="#2A878F">函数提升</font>

> 函数提升与变量提升比较类似，是指函数在声明之前即可被调用

```html
<script>
  // 调用函数
  // 1. 会把所有函数声明提升到当前作用域的最前面
  // 2. 只提升函数声明，不提升函数调用
  foo()
  // 声明函数
  function foo() {
    console.log('声明之前即被调用...')
  }

  // 不存在提升现象
  bar()  // 错误
  // 函数表达式 必须先声明和赋值， 后调用 否则 报错
  var bar = function () {
    console.log('函数表达式不存在提升现象...')
  }
</script>
```

总结：

1. 函数提升能够使函数的声明调用更灵活

2. 函数表达式不存在提升的现象

3. 函数提升出现在相同作用域当中

#### <font color="#2A878F">函数参数</font>

##### <font color="#6163d3">默认值</font>

```html
<script>
  // 设置参数默认值
  function sayHi(name="小明", age=18) {
    document.write(`<p>大家好，我叫${name}，我今年${age}岁了。</p>`);
  }
  // 调用函数
  sayHi();
  sayHi('小红');
  sayHi('小刚', 21);
</script>
```

总结：

1. 声明函数时为形参赋值即为参数的默认值

2. 如果参数未自定义默认值时，参数的默认值为 `undefined`

3. 调用函数时没有传入对应实参时，参数的默认值被当做实参传入

##### <font color="#6163d3">动态参数</font>

> `arguments` 是函数内部内置的伪数组变量，它包含了调用函数时传入的所有实参。

```html
<script>
  function getSum() {
    // arguments 动态参数 只存在于 函数里面
    // 是伪数组 里面存储的是传递过来的实参
    // console.log(arguments)  [2,3,4]
    let sum = 0
    for (let i = 0; i < arguments.length; i++) {
      sum += arguments[i]
    }
    console.log(sum)
  }
  getSum(2, 3, 4)
  getSum(1, 2, 3, 4, 2, 2, 3, 4)
</script>
```

总结：

1. `arguments` 是一个伪数组

2. `arguments` 的作用是动态获取函数的实参

##### <font color="#6163d3">剩余参数</font>

```html
<script>
  function getSum(a, b, ...arr) {
    console.log(arr)  // 使用的时候不需要写 ...
  }
  getSum(2, 3)
  getSum(1, 2, 3, 4, 5)
</script>
```

总结：

1. `...` 是语法符号，置于最末函数形参之前，用于获取多余的实参

2. 借助 `...` 获取的剩余实参，是个真数组

##### <font color="#6163d3">拓展-展开运算符</font>

> 展开运算符(…),将一个数组进行展开
> 
> 典型运用场景： 求数组最大值(最小值)、合并数组等

```html
<script>
  const arr1 = [1, 2, 3]
  // 展开运算符 可以展开数组
  // console.log(...arr)

  // console.log(Math.max(1, 2, 3))
  // ...arr1  === 1,2,3
  // 1 求数组最大值
  console.log(Math.max(...arr1)) // 3
  console.log(Math.min(...arr1)) // 1

  // 2. 合并数组
  const arr2 = [3, 4, 5]
  const arr = [...arr1, ...arr2]
  console.log(arr)

</script>
```

> 剩余参数：函数参数使用，得到真数组
> 
> 展开运算符：数组中使用，数组展开

#### <font color="#2A878F">箭头函数</font>

目的：引入箭头函数的目的是更简短的函数写法并且不绑定this，箭头函数的语法比函数表达式更简洁。

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711145217201-1888851831.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711145227751-53818363.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711145239965-997786500.png)

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711145250852-1830745757.png)

```html
<script>
  const fn = function () {
    console.log(123)
  }

  // 1. 箭头函数 基本语法
  const fn = () => {
    console.log(123)
  }
  fn()
  const fn = (x) => {
    console.log(x)
  }
  fn(1)

  // 2. 只有一个形参的时候，可以省略小括号
  const fn = x => {
    console.log(x)
  }
  fn(1)

  // 3. 只有一行代码的时候，我们可以省略大括号
  const fn = x => console.log(x)
  fn(1)

  // 4. 只有一行代码的时候，可以省略return
  const fn = x => x + x
  console.log(fn(1))

  // 5. 箭头函数可以直接返回一个对象
  const fn = (uname) => ({ uname: uname })
  console.log(fn('刘德华'))

</script>
```

总结：

1. 箭头函数属于表达式函数，因此不存在函数提升

2. 箭头函数只有一个参数时可以省略圆括号 `()`

3. 箭头函数函数体只有一行代码时可以省略花括号 `{}`，并自动做为返回值被返回

##### <font color="#6163d3">箭头函数参数</font>

> 箭头函数中没有 `arguments`，只能使用 `...` 动态获取实参

```html
<script>
  // 1. 利用箭头函数来求和
  const getSum = (...arr) => {
    let sum = 0
    for (let i = 0; i < arr.length; i++) {
      sum += arr[i]
    }
    return sum
  }
  const result = getSum(2, 3, 4)
  console.log(result) // 9
</script>
```

##### <font color="#6163d3">箭头函数 this</font>

> 箭头函数不会创建自己的this,它只会从自己的作用域链的上一层沿用this。

```html
<script>
  // 以前this的指向：  谁调用的这个函数，this 就指向谁
  console.log(this)  // window
  // // 普通函数
  function fn() {
    console.log(this)  // window
  }
  window.fn()

  // 对象方法里面的this
  const obj = {
    name: 'andy',
    sayHi: function () {
      console.log(this)  // obj
    }
  }
  obj.sayHi()

  // 2. 箭头函数的this  是上一层作用域的this 指向
  const fn = () => {
    console.log(this)  // window
  }
  fn()
  // 对象方法箭头函数 this
  const obj = {
    uname: 'cats',
    sayHi: () => {
      console.log(this)  // this 指向谁？ window
    }
  }
  obj.sayHi()

  const obj = {
    uname: 'cats',
    sayHi: function () {
      console.log(this)  // obj
      let i = 10
      const count = () => {
        console.log(this)  // obj 
      }
      count()
    }
  }
  obj.sayHi()

</script>
```

### <font color="#A9D0D9">解构赋值</font>

> 解构赋值是一种快速为变量赋值的简洁语法，本质上仍然是为变量赋值，分为数组解构、对象解构两大类型。

#### <font color="#2A878F">数组解构</font>

> 数组解构是将数组的单元值快速批量赋值给一系列变量的简洁语法。

```html
<script>
  // const arr = [100, 60, 80]
  // 数组解构 赋值
  // // const [max, min, avg] = arr
  const [max, min, avg] = [100, 60, 80]
  // // const max = arr[0]
  // // const min = arr[1]
  // // const avg = arr[2]
  console.log(max) // 100
  console.log(avg) // 80

  // 基本语法：典型应用交互2个变量
  // 交换2个变量的值
  let a = 1
  // 注意： js 前面必须加分号情况
  let b = 2;
  [b, a] = [a, b]
  console.log(a, b)
</script>
```

总结：

1. 赋值运算符 `=` 左侧的 `[]` 用于批量声明变量，右侧数组的单元值将被赋值给左侧的变量

2. 变量的顺序对应数组单元值的位置依次进行赋值操作

3. 变量的数量大于单元值数量时，多余的变量将被赋值为  `undefined`

4. 变量的数量小于单元值数量时，可以通过 `...` 获取剩余单元值，但只能置于最末位

5. 允许初始化变量的默认值，且只有单元值为 `undefined` 时默认值才会生效

##### <font color="#6163d3">必须加分号的两种情况</font>

```html
<script>
  // 1. 立即执行函数要加
  // (function () { })();
  // (function () { })();
  // 2. 使用数组的时候
  // const arr = [1, 2, 3]
  const str = 'cats';
  [1, 2, 3].map(function (item) {
    console.log(item)
  })

  let a = 1
  let b = 2
    ;[b, a] = [a, b]

  console.log(a, b)
</script>
```

##### <font color="#6163d3">细节</font>

```html
<script>

  const pc = ['海尔', '联想', '小米', '方正']
  const [hr, lx, mi, fz] = ['海尔', '联想', '小米', '方正']
  console.log(hr)
  console.log(lx)
  console.log(mi)
  console.log(fz)

  // 请将最大值和最小值函数返回值解构 max 和min 两个变量
  function getValue() {
    return [100, 60]
  }
  const [max, min] = getValue()
  console.log(max)
  console.log(min)
  // 1. 变量多， 单元值少 ， undefined
  const [a, b, c, d] = [1, 2, 3]
  console.log(a) // 1
  console.log(b) // 2
  console.log(c) // 3
  console.log(d) // undefined
  // 2. 变量少， 单元值多
  const [a, b] = [1, 2, 3]
  console.log(a) // 1
  console.log(b) // 2
  // 3.  剩余参数 变量少， 单元值多
  const [a, b, ...c] = [1, 2, 3, 4]
  console.log(a) // 1
  console.log(b) // 2
  console.log(c) // [3, 4]  真数组
  // 4.  防止 undefined 传递
  const [a = 0, b = 0] = [1, 2]
  const [a = 0, b = 0] = []
  console.log(a) // 1
  console.log(b) // 2
  // 5.  按需导入赋值
  const [a, b, , d] = [1, 2, 3, 4]
  console.log(a) // 1
  console.log(b) // 2
  console.log(d) // 4

  const arr = [1, 2, [3, 4]]
  console.log(arr[0])  // 1
  console.log(arr[1])  // 2
  console.log(arr[2])  // [3,4]
  console.log(arr[2][0])  // 3

  // 多维数组解构
  const arr = [1, 2, [3, 4]]
  const [a, b, c] = [1, 2, [3, 4]]
  console.log(a) // 1
  console.log(b) // 2
  console.log(c) // [3,4]


  const [a, b, [c, d]] = [1, 2, [3, 4]]
  console.log(a) // 1
  console.log(b) // 2
  console.log(c) // 3
  console.log(d) // 4
</script>
```

#### <font color="#2A878F">对象解构</font>

> 对象解构是将对象属性和方法快速批量赋值给一系列变量的简洁语法。

总结：

1. 赋值运算符 `=` 左侧的 `{}` 用于批量声明变量，右侧对象的属性值将被赋值给左侧的变量

2. 对象属性的值将被赋值给与属性名相同的变量

3. 对象中找不到与变量名一致的属性时变量值为 `undefined`

4. 允许初始化变量的默认值，属性不存在或单元值为 `undefined` 时默认值才会生效

注：支持多维解构赋值

```html
<script>
  // 对象解构
  // const obj = {
  //   uname: 'cats',
  //   age: 18
  // }
  // obj.uname
  // obj.age 
  // const uname = 'red老师'
  // 解构的语法
  // const { uname, age } = {age: 18, uname: 'cats' }
  // // 等价于 const uname =  obj.uname
  // 要求属性名和变量名必须一直才可以
  // console.log(uname)
  // console.log(age)
  // 1. 对象解构的变量名 可以重新改名  旧变量名: 新变量名
  // const { uname: username, age } = { uname: 'cats', age: 18 }

  // console.log(username)
  // console.log(age)
  // 2. 解构数组对象
  const pig = [
    {
      uname: '佩奇',
      age: 6
    }
  ]
  const [{ uname, age }] = pig
  console.log(uname)
  console.log(age)
</script>
```

##### <font color="#6163d3">多级对象结构</font>

```html
<script>
  // const pig = {
  //   name: '佩奇',
  //   family: {
  //     mother: '猪妈妈',
  //     father: '猪爸爸',
  //     sister: '乔治'
  //   },
  //   age: 6
  // }
  // // 多级对象解构
  // const { name, family: { mother, father, sister } } = pig
  // console.log(name)
  // console.log(mother)
  // console.log(father)
  // console.log(sister)

  const person = [
    {
      name: '佩奇',
      family: {
        mother: '猪妈妈',
        father: '猪爸爸',
        sister: '乔治'
      },
      age: 6
    }
  ]
  const [{ name, family: { mother, father, sister } }] = person
  console.log(name)
  console.log(mother)
  console.log(father)
  console.log(sister)
</script>
```

##### <font color="#6163d3">案例</font>

```html
<script>
  // 1. 这是后台传递过来的数据
  const msg = {
    "code": 200,
    "msg": "获取新闻列表成功",
    "data": [
      {
        "id": 1,
        "title": "5G商用自己，三大运用商收入下降",
        "count": 58
      },
      {
        "id": 2,
        "title": "国际媒体头条速览",
        "count": 56
      },
      {
        "id": 3,
        "title": "乌克兰和俄罗斯持续冲突",
        "count": 1669
      },
    ]
  }

  // 需求1： 请将以上msg对象  采用对象解构的方式 只选出  data 方面后面使用渲染页面
  // const { data } = msg
  // console.log(data)
  // 需求2： 上面msg是后台传递过来的数据，我们需要把data选出当做参数传递给 函数
  // const { data } = msg
  // msg 虽然很多属性，但是我们利用解构只要 data值
  function render({ data }) {
    // const { data } = arr
    // 我们只要 data 数据
    // 内部处理
    console.log(data)

  }
  render(msg)

  // 需求3， 为了防止msg里面的data名字混淆，要求渲染函数里面的数据名改为 myData
  function render({ data: myData }) {
    // 要求将 获取过来的 data数据 更名为 myData
    // 内部处理
    console.log(myData)

  }
  render(msg)

</script>
```

### <font color="#A9D0D9">forEach方法</font>

> forEach() 方法用于调用数组的每个元素，并将元素传递给回调函数
> 
> 主要使用场景： 遍历数组的每个元素

语法：

```html
<script>
被遍历的数组.forEach(function (当前数组元素,当前元素索引号) {
  // 函数体
})
</script>
```

```html
<script>
  // forEach 就是遍历  加强版的for循环  适合于遍历数组对象
  const arr = ['red', 'green', 'cats']
  const result = arr.forEach(function (item, index) {
    console.log(item)  // 数组元素 red  green cats
    console.log(index) // 索引号
  })
  // console.log(result)
</script>
```

注意：

1. forEach 主要是遍历数组

2. 参数当前数组元素是必须要写的， 索引号可选。

### <font color="#A9D0D9">filter筛选数组</font>

> filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素
> 
> 主要使用场景： 筛选数组符合条件的元素，并返回筛选之后元素的新数组

语法：

```html
<script>
  被遍历的数组.filter(function (currentValue,index) {
    return 筛选条件
  })
</script>
```

```html
<script>
  const arr = [10, 20, 30]
  // const newArr = arr.filter(function (item, index) {
  //   // console.log(item)
  //   // console.log(index)
  //   return item >= 20
  // })
  // 返回的符合条件的新数组

  const newArr = arr.filter(item => item >= 20)
  console.log(newArr)
</script>
```

## <font color="Pink">Second</font>

### <font color="#A9D0D9">深入对象</font>

#### <font color="#2A878F">三种创建方式</font>

1. 利用对象字面量创建对象

`const o = { name: '冏猫'} `

2. 利用 new Object 创建对象 

`const o = new Object({ name: '冏猫'}) `

3. 利用构造函数创建对象

#### <font color="#2A878F">构造函数</font>

> 构造函数 ：是一种特殊的函数，主要用来初始化对象
> 
> 可以通过构造函数来快速创建多个类似的对象。

不过有两个约定：

1. 它们的命名以大写字母开头。

2. 它们只能由 "new" 操作符来执行。

总结：

2. 使用 `new` 关键字调用函数的行为被称为实例化

3. 实例化构造函数时没有参数时可以省略 `()`

4. 构造函数的返回值即为新创建的对象

5. 构造函数内部的 `return` 返回的值无效！

#### <font color="#2A878F">实例成员</font>

> 通过构造函数创建的对象称为实例对象，实例对象中的属性和方法称为实例成员。

```html
<script>
  // 构造函数
  function Person() {
    // 构造函数内部的 this 就是实例对象
    // 实例对象中动态添加属性
    this.name = '小明'
    // 实例对象动态添加方法
    this.sayHi = function () {
      console.log('大家好~')
    }
  }
  // 实例化，p1 是实例对象
  // p1 实际就是 构造函数内部的 this
  const p1 = new Person()
  console.log(p1)
  console.log(p1.name) // 访问实例属性
  p1.sayHi() // 调用实例方法
</script>
```

总结：

1. 构造函数内部 `this` 实际上就是实例对象，为其动态添加的属性和方法即为实例成员

2. 为构造函数传入参数，动态创建结构相同但值不同的对象

注：构造函数创建的实例对象彼此独立互不影响。

#### <font color="#2A878F">静态成员</font>

> 在 JavaScript 中底层函数本质上也是对象类型，因此允许直接为函数动态添加属性或方法，构造函数的属性和方法被称为静态成员。

```html
<script>
  // 构造函数
  function Person(name, age) {
    // 省略实例成员
  }
  // 静态属性
  Person.eyes = 2
  Person.arms = 2
  // 静态方法
  Person.walk = function () {
    console.log('^_^人都会走路...')
    // this 指向 Person
    console.log(this.eyes)
  }
</script>
```

总结：

1. 静态成员指的是添加到构造函数本身的属性和方法

2. 一般公共特征的属性或方法静态成员设置为静态成员

3. 静态成员方法中的 `this` 指向构造函数本身

### <font color="#A9D0D9">内置构造函数</font>

> 在 JavaScript 中最主要的数据类型有 6 种：
> 
> 基本数据类型：
> 
> - 字符串、数值、布尔、undefined、null
> 
> 引用类型: 
> 
> - 对象
> 
> 其实字符串、数值、布尔、等基本类型也都有专门的构造函数，这些我们称为包装类型。
> 
> JS中几乎所有的数据都可以基于构成函数创建。

> 引用类型
> 
> Object，Array，RegExp，Date 等
> 
> 包装类型
> 
> String，Number，Boolean 等

#### <font color="#2A878F">基本包装类型</font>

```html
<script>
  // const str = 'cats'
  // console.log(str.length)
  // const num = 12
  // console.log(num.toFixed(2))
  // const str = 'cats'
  // js 底层完成， 把简单数据类型包装为了引用数据类型
  // const str = new String('cats')
</script>
```

#### <font color="#2A878F">Object</font>

> `Object` 是内置的构造函数，用于创建普通对象。
> 
> 学习三个常用静态方法（静态方法就是只有构造函数Object可以调用的）

```html
<script>
  const o = { uname: 'cats', age: 18 }
  // 1.获得所有的属性名
  console.log(Object.keys(o))  //返回数组['uname', 'age']
  // 2. 获得所有的属性值
  console.log(Object.values(o))  //  ['cats', 18]
  // 3. 对象的拷贝
  // const oo = {}
  // Object.assign(oo, o)
  // console.log(oo)
  Object.assign(o, { gender: '女' })
  console.log(o)
</script>
```

总结：

1. 推荐使用字面量方式声明对象，而不是 `Object` 构造函数

2. `Object.assign` 静态方法创建新的对象

3. `Object.keys` 静态方法获取对象中所有属性(键)

4. `Object.values` 表态方法获取对象中所有属性值

#### <font color="#2A878F">Array</font>

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711194147937-1540226829.png)

> `Array` 是内置的构造函数，用于创建数组。

作用： reduce 返回累计处理的结果，经常用于求和等

基本语法：

`arr.reduce(function(){},起始值)`\

`arr.reduce(finction(上一次值,当前值){},初始值)`

`const arr = [1,2,3,4]`

如果有起始值,则把起始值累加到里面

```html
<script>
  //数组reduce方法
  //arr.reduce(function(上一次值,当前值){},初始值)
  const arr = [1,5,8]

  //1. 没有初始值
  const total = arr.reduce(function (prev,current){
    return prev + current
  })
  console.log(total)

  //2.有初始值
  const total = arr.reduce(function(prev,current){
    return prev + current 
  },10)
  console.log(total)

  //3.箭头函数的写法
  const total = arr.reduce((prev,current) => prev + current,10)
  console.log(total)
</script>
```

reduce 执行过程：

1. 如果没有起始值,则上一次值以数组的第一个数组元素的值

2. 每一次循环,把返回值给做为 下一次循环的上一次值

3. 如果有起始值,则 起始值做为上一次值

```html
<script>
  const arr = [{
    name: '张三',
    salary: 10000
  }, {
    name: '李四',
    salary: 10000
  }, {
    name: '王五',
    salary: 20000
  },
  ]
  // 涨薪的钱数  10000 * 1.3 
  // const money = arr.reduce(function (prev, current) {
  //   return prev + current.salary * 1.3
  // }, 0)
  const money = arr.reduce((prev, current) => prev + current.salary * 1.3, 0)
  console.log(money)
</script>
```

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230711202024175-2030538039.png)

总结：

1. 推荐使用字面量方式声明数组，而不是 `Array` 构造函数

2. 实例方法 `forEach` 用于遍历数组，替代 `for` 循环 (重点)

3. 实例方法 `filter` 过滤数组单元值，生成新数组(重点)

4. 实例方法 `map` 迭代原数组，生成新数组(重点)

5. 实例方法 `join` 数组元素拼接为字符串，返回字符串(重点)

6. 实例方法  `find`  查找元素， 返回符合测试条件的第一个数组元素值，如果没有符合条件的则返回 undefined(重点)

7. 实例方法`every` 检测数组所有元素是否都符合指定条件，如果**所有元素**都通过检测返回 true，否则返回 false(重点)

8. 实例方法`some` 检测数组中的元素是否满足指定条件   **如果数组中有**元素满足条件返回 true，否则返回 false

9. 实例方法 `concat`  合并两个数组，返回生成新数组

10. 实例方法 `sort` 对原数组单元值排序

11. 实例方法 `splice` 删除或替换原数组单元

12. 实例方法 `reverse` 反转数组

13. 实例方法 `findIndex`  查找元素的索引值

```html
<script>
  // const arr = ['red', 'blue', 'green']
  // const re = arr.find(function (item) {
  //   return item === 'blue'
  // })
  // console.log(re)

  const arr = [
    {
      name: '小米',
      price: 1999
    },
    {
      name: '华为',
      price: 3999
    },
  ]
  // 找小米 这个对象，并且返回这个对象
  // const mi = arr.find(function (item) {
  //   // console.log(item)  //
  //   // console.log(item.name)  //
  //   console.log(111)
  //   return item.name === '华为'
  // })
  // 1. find 查找
  // const mi = arr.find(item => item.name === '小米')
  // console.log(mi)
  // 2. every 每一个是否都符合条件，如果都符合返回 true ，否则返回false
  const arr1 = [10, 20, 30]
  const flag = arr1.every(item => item >= 20)
  console.log(flag)
</script>
```

```html
<script>
  const spec = { size: '40cm*40cm', color: '黑色' }
  //1. 所有的属性值回去过来  数组
  // console.log(Object.values(spec))
  // 2. 转换为字符串   数组join('/') 把数组根据分隔符转换为字符串
  // console.log(Object.values(spec).join('/'))
  document.querySelector('div').innerHTML = Object.values(spec).join('/')
</script>
```

##### <font color="#6163d3">伪数组转换为真数组</font>

静态方法 Array.from()

```html
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
  </ul>
  <script>
    //  Array.from(lis) 把伪数组转换为真数组
    const lis = document.querySelectorAll('ul li')
    // console.log(lis)
    // lis.pop() 报错
    const liss = Array.from(lis)
    liss.pop()
    console.log(liss)
  </script>
</body>
```

#### <font color="#2A878F">包装类型</font>

##### <font color="#6163d3">String</font>

`String` 是内置的构造函数，用于创建字符串。

```html
<script>
  //1. split 把字符串 转换为 数组  和 join() 相反
  // const str = 'cats,red'
  // const arr = str.split(',')
  // console.log(arr)
  // const str1 = '2022-4-8'
  // const arr1 = str1.split('-')
  // console.log(arr1)
  // 2. 字符串的截取   substring(开始的索引号[， 结束的索引号])
  // 2.1 如果省略 结束的索引号，默认取到最后
  // 2.2 结束的索引号不包含想要截取的部分
  // const str = '饿死的冏猫'
  // console.log(str.substring(5, 7))
  // 3. startsWith 判断是不是以某个字符开头
  // const str = '饿死的冏猫'
  // console.log(str.startsWith('饿'))
  // 4. includes 判断某个字符是不是包含在一个字符串里面
  const str = '饿死的冏猫'
  console.log(str.includes('饿')) // true
</script>
```

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substring" target="_blank">subString文档</a>

总结：

1. 实例属性 `length` 用来获取字符串的度长(重点)

2. 实例方法 `split('分隔符')` 用来将字符串拆分成数组(重点)

3. 实例方法 `substring（需要截取的第一个字符的索引[,结束的索引号]）` 用于字符串截取(重点)

4. 实例方法 `startsWith(检测字符串[, 检测位置索引号])` 检测是否以某字符开头(重点)

5. 实例方法 `includes(搜索的字符串[, 检测位置索引号])` 判断一个字符串是否包含在另一个字符串中，根据情况返回 true 或 false(重点)

6. 实例方法 `toUpperCase` 用于将字母转换成大写

7. 实例方法 `toLowerCase` 用于将就转换成小写

8. 实例方法 `indexOf`  检测是否包含某字符

9. 实例方法 `endsWith` 检测是否以某字符结尾

10. 实例方法 `replace` 用于替换字符串，支持正则匹配

11. 实例方法 `match` 用于查找字符串，支持正则匹配

注：String 也可以当做普通函数使用，这时它的作用是强制转换成字符串数据类型。

##### <font color="#6163d3">Number</font>

`Number` 是内置的构造函数，用于创建数值。

```html
<script>
  // toFixed 方法可以让数字指定保留的小数位数
  const num = 10.923
  // console.log(num.toFixed())
  console.log(num.toFixed(1))
  const num1 = 10
  console.log(num1.toFixed(2))
</script>
```

总结：

1. 推荐使用字面量方式声明数值，而不是 `Number` 构造函数

2. 实例方法 `toFixed` 用于设置保留小数位的长度

## <font color="Pink">Third</font>

### <font color="#A9D0D9">编程思想</font>

#### <font color="#2A878F">面向过程</font>

面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次

调用就可以了。

 举个栗子：蛋炒饭

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712084108798-479375589.png)

#### <font color="#2A878F">面向对象</font>

面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712084102385-1098384098.png)

在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工。

面向对象编程具有灵活、代码可复用、容易维护和开发的优点，更适合多人合作的大型软件项目。

面向对象的特性：

- 封装性

- 继承性

- 多态性

### <font color="#A9D0D9">构造函数</font>

封装是面向对象思想中比较重要的一部分，js面向对象可以通过构造函数实现的封装。

同样的将变量和函数组合到了一起并能通过 this 实现数据的共享，所不同的是借助构造函数创建出来的实例对象之

间是彼此不影响的

```html
<script>
  // 1.公共的属性写到 构造函数里面
  function Star(uname, age) {
    this.uname = uname
    this.age = age
    // this.sing = function () {
    //   console.log('唱歌')
    // }
  }
  const ldh = new Star('刘德华', 55)
  const zxy = new Star('张学友', 58)
  // console.log(ldh === zxy)  // false
  console.log(ldh.sing === zxy.sing)

</script>
```

> 总结：
> 
> 1. 构造函数体现了面向对象的封装特性
> 
> 2. 构造函数实例创建的对象彼此独立、互不影响

封装是面向对象思想中比较重要的一部分，js面向对象可以通过构造函数实现的封装。

前面我们学过的构造函数方法很好用，但是 存在`浪费内存`的问题

### <font color="#A9D0D9">原型对象</font>

构造函数通过原型分配的函数是所有对象所 共享的。

- JavaScript 规定，每一个构造函数都有一个 `prototype 属性`，指向另一个对象，所以我们也称为原型对象

- 这个对象可以挂载函数，对象实例化不会多次创建原型上函数，节约内存

- 我们可以把那些不变的方法，直接定义在 `prototype 对象`上，这样所有对象的实例就可以共享这些方法。

- 构造函数和原型对象中的this 都指向 实例化的对象

```html
<script>
  // 构造函数  公共的属性和方法 封装到 Star 构造函数里面了
  // 1.公共的属性写到 构造函数里面
  function Star(uname, age) {
    this.uname = uname
    this.age = age
    // this.sing = function () {
    //   console.log('唱歌')
    // }
  }
  // 2. 公共的方法写到原型对象身上   节约了内存
  Star.prototype.sing = function () {
    console.log('唱歌')
  }
  const ldh = new Star('刘德华', 55)
  const zxy = new Star('张学友', 58)
  ldh.sing() //调用
  zxy.sing() //调用
  // console.log(ldh === zxy)  // false
  console.log(ldh.sing === zxy.sing)

  // console.dir(Star.prototype)
</script>
```

#### <font color="#2A878F">构造函数,原型的this</font>

```html
<script>
  let that
  function Star(uname) {
    // that = this
    // console.log(this)
    this.uname = uname
  }
  // 原型对象里面的函数this指向的还是 实例对象 ldh
  Star.prototype.sing = function () {
    that = this
    console.log('唱歌')
  }
  // 实例对象 ldh   
  // 构造函数里面的 this 就是  实例对象  ldh
  const ldh = new Star('刘德华')
  ldh.sing()
  console.log(that === ldh)
</script>
```

#### <font color="#2A878F">数组最大值,求和方法</font>

```html
<script>
  // 自己定义 数组扩展方法  求和 和 最大值 
  // 1. 我们定义的这个方法，任何一个数组实例对象都可以使用
  // 2. 自定义的方法写到  数组.prototype 身上
  // 1. 最大值
  const arr = [1, 2, 3]
  Array.prototype.max = function () {
    // 展开运算符
    return Math.max(...this)
    // 原型函数里面的this 指向谁？ 实例对象 arr
  }
  // 2. 最小值
  Array.prototype.min = function () {
    // 展开运算符
    return Math.min(...this)
    // 原型函数里面的this 指向谁？ 实例对象 arr
  }
  console.log(arr.max())
  console.log([2, 5, 9].max())
  console.log(arr.min())
  // const arr = new Array(1, 2)
  // console.log(arr)
  // 3. 求和 方法 
  Array.prototype.sum = function () {
    return this.reduce((prev, item) => prev + item, 0)
  }
  console.log([1, 2, 3].sum())
  console.log([11, 21, 31].sum())
</script>
```

#### <font color="#2A878F">constructor 属性</font>

在哪里？ 每个原型对象里面都有个constructor 属性（constructor 构造函数）

作用：该属性指向该原型对象的构造函数， 简单理解，就是指向我的爸爸，我是有爸爸的孩子

**使用场景：**

如果有多个对象的方法，我们可以给原型对象采取对象形式赋值.

但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor 就不再指向当前构造函数了

此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。

```html
<script>
  // constructor  单词 构造函数

  // Star.prototype.sing = function () {
  //   console.log('唱歌')
  // }
  // Star.prototype.dance = function () {
  //   console.log('跳舞')
  // }
  function Star() {
  }
  // console.log(Star.prototype)
  Star.prototype = {
    // 从新指回创造这个原型对象的 构造函数
    constructor: Star,
    sing: function () {
      console.log('唱歌')
    },
    dance: function () {
      console.log('跳舞')
    },
  }
  console.log(Star.prototype)
  // console.log(Star.prototype.constructor)

  // const ldh = new Star()
  // console.log(Star.prototype.constructor === Star)
</script>
```

#### <font color="#2A878F">对象原型</font>

对象都会有一个属性 `__proto__` 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 

原型对象的属性和方法，就是因为对象有 `__proto__` 原型的存在。

注意：

- `__proto__` 是JS非标准属性

- `[[prototype]]`和`__proto__`意义相同

- 用来表明当前实例对象指向哪个原型对象prototype

- `__proto__`对象原型里面也有一个 constructor属性，指向创建该实例对象的构造函数

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712092840429-346408350.png)

#### <font color="#2A878F">原型继承</font>

继承是面向对象编程的另一个特征，通过继承进一步提升代码封装的程度，JavaScript 中大多是借助原型对象实现继承的特性。

龙生龙、凤生凤、老鼠的儿子会打洞描述的正是继承的含义。

```html
<script>
  // 继续抽取   公共的部分放到原型上
  // const Person1 = {
  //   eyes: 2,
  //   head: 1
  // }
  // const Person2 = {
  //   eyes: 2,
  //   head: 1
  // }
  // 构造函数  new 出来的对象 结构一样，但是对象不一样
  function Person() {
    this.eyes = 2
    this.head = 1
  }
  // console.log(new Person)
  // 女人  构造函数   继承  想要 继承 Person
  function Woman() {

  }
  // Woman 通过原型来继承 Person
  // 父构造函数（父类）   子构造函数（子类）
  // 子类的原型 =  new 父类  
  Woman.prototype = new Person()   // {eyes: 2, head: 1} 
  // 指回原来的构造函数
  Woman.prototype.constructor = Woman

  // 给女人添加一个方法  生孩子
  Woman.prototype.baby = function () {
    console.log('宝贝')
  }
  const red = new Woman()
  console.log(red)
  // console.log(Woman.prototype)
  // 男人 构造函数  继承  想要 继承 Person
  function Man() {

  }
  // 通过 原型继承 Person
  Man.prototype = new Person()
  Man.prototype.constructor = Man
  const cats = new Man()
  console.log(cats)
</script>
```

#### <font color="#2A878F">原型链</font>

基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，我们将原型对象的链状结构关系称为原型链

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712094503821-230183188.png)

```html
<script>
  // function Objetc() {}
  console.log(Object.prototype)
  console.log(Object.prototype.__proto__)

  function Person() {

  }
  const ldh = new Person()
  // console.log(ldh.__proto__ === Person.prototype)
  // console.log(Person.prototype.__proto__ === Object.prototype)
  console.log(ldh instanceof Person)
  console.log(ldh instanceof Object)
  console.log(ldh instanceof Array)
  console.log([1, 2, 3] instanceof Array)
  console.log(Array instanceof Object)
</script>
```

1. 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。

2. 如果没有就查找它的原型（也就是 `__proto__`指向的 prototype 原型对象）

3. 如果还没有就查找原型对象的原型（Object的原型对象）

4. 依此类推一直找到 Object 为止（null）

5. `__proto__`对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线

6. 可以使用 `instanceof` 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上

## <font color="Pink">Fourth</font>

### <font color="#A9D0D9">深浅拷贝</font>

开发中我们经常需要复制一个对象。如果直接用赋值会有下面问题：

```html
<script>
  const obj = {
    uname: 'cats',
    age: 18
  }
  const o = obj
  console.log(o) // {uname: 'cats', age: 18}
  o.age = 20
  console.log(o) // {uname: 'cats', age: 20}
  // 但是 obj 对象里面的 age值 发生了变化
  console.log(obj) // {uname: 'cats', age: 20}
</script>
```

#### <font color="#2A878F">浅拷贝</font>

首先浅拷贝和深拷贝只针对引用类型

浅拷贝：拷贝的是地址

常见方法：

1. 拷贝对象：Object.assgin() / 展开运算符 {...obj} 拷贝对象

2. 拷贝数组：Array.prototype.concat() 或者 [...arr]

```html
<script>
  const obj = {
    uname: 'cat',
    age: 18,
    family: {
      baby: 'cats'
    }
  }
  // 浅拷贝
  // const o = { ...obj }
  // console.log(o)
  // o.age = 20
  // console.log(o)
  // console.log(obj)
  const o = {}
  Object.assign(o, obj)
  o.age = 20
  o.family.baby = 'dogs'
  console.log(o) // family: {baby: 'dogs'}
  // 但是 obj 对象里面的 family对象 baby 发生了变化
  console.log(obj) // family: {baby: 'dogs'}
</script>
```

> 如果是简单数据类型拷贝值，引用数据类型拷贝的是地址 (简单理解： 如果是单层对象，没问题，如果有多层就有问题)

#### <font color="#2A878F">深拷贝</font>

首先浅拷贝和深拷贝只针对引用类型

深拷贝：拷贝的是对象，不是地址

常见方法：

1. 通过`递归`实现深拷贝

2. `lodash`/`cloneDeep`

3. 通过`JSON.stringify()`实现

##### <font color="#6163d3">递归实现深拷贝</font>

函数递归：

如果一个函数在内部可以调用其本身，那么这个函数就是递归函数

- 简单理解:函数内部自己调用自己, 这个函数就是递归函数

- 递归函数的作用和循环效果类似

- 由于递归很容易发生“栈溢出”错误（stack overflow），所以必须要加退出条件 return

```html
<script>
  let i = 1
  function fn() {
    console.log(`这是第${i}次`)
    if (i >= 6) {
      return
    }
    i++
    fn()
  }
  fn()
</script>
```

**模拟setInterval效果**

```html
<div></div>
<script>
  function getTime() {
    document.querySelector('div').innerHTML = new Date().toLocaleString()
    setTimeout(getTime, 1000)
  }
  getTime()
</script>
```

**案例**

```html
<body>
  <script>
    const obj = {
      uname: 'cats',
      age: 18,
      hobby: ['乒乓球', '足球'],
      family: {
        baby: '小cats'
      }
    }
    const o = {}
    // 拷贝函数
    function deepCopy(newObj, oldObj) {
      debugger
      for (let k in oldObj) {
        // 处理数组的问题  一定先写数组 在写 对象 不能颠倒
        if (oldObj[k] instanceof Array) {
          newObj[k] = []
          //  newObj[k] 接收 []  hobby
          //  oldObj[k]   ['乒乓球', '足球']
          deepCopy(newObj[k], oldObj[k])
        } else if (oldObj[k] instanceof Object) {
          newObj[k] = {}
          deepCopy(newObj[k], oldObj[k])
        }
        else {
          //  k  属性名 uname age    oldObj[k]  属性值  18
          // newObj[k]  === o.uname  给新对象添加属性
          newObj[k] = oldObj[k]
        }
      }
    }
    deepCopy(o, obj) // 函数调用  两个参数 o 新对象  obj 旧对象
    console.log(o)
    o.age = 20
    o.hobby[0] = '篮球'
    o.family.baby = '老cats'
    console.log(obj)
    console.log([1, 23] instanceof Object)
  </script>
</body>
```

##### <font color="#6163d3">cloneDeep实现深拷贝</font>

js库lodash里面cloneDeep内部实现了深拷贝

```html
<!-- 先引用 -->
<script src="./lodash.min.js"></script>
<script>
  const obj = {
    uname: 'cats',
    age: 18,
    hobby: ['乒乓球', '足球'],
    family: {
      baby: '小cats'
    }
  }
  const o = _.cloneDeep(obj)
  console.log(o)
  o.family.baby = '老cats'
  console.log(obj)
</script>
```

##### <font color="#6163d3">JSON序列化</font>

```html
<script>
  const obj = {
    uname: 'cats',
    age: 18,
    hobby: ['乒乓球', '足球'],
    family: {
      baby: '小cats'
    }
  }
  // 把对象转换为 JSON 字符串
  // console.log(JSON.stringify(obj))
  const o = JSON.parse(JSON.stringify(obj))
  console.log(o)
  o.family.baby = '123'
  console.log(obj)
</script>
```

### <font color="#A9D0D9">异常处理</font>

#### <font color="#2A878F">throw</font>

> 异常处理是指预估代码执行过程中可能发生的错误，然后最大程度的避免错误的发生导致整个程序无法继续运行

```html
<script>
  function fn(x, y) {
    if (!x || !y) {
      // throw '没有参数传递进来'
      throw new Error('没有参数传递过来')
    }

    return x + y
  }
  console.log(fn())
</script>
```

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712145241944-1833237306.png)

总结：

1. throw 抛出异常信息，程序也会终止执行

2. throw 后面跟的是错误提示信息

3. Error 对象配合 throw 使用，能够设置更详细的错误信息

#### <font color="#2A878F">try ... catch</font>

```html
<body>
  <p>123</p>
  <script>
    function fn() {
      try {
        // 可能发送错误的代码 要写到 try
        const p = document.querySelector('.p')
        p.style.color = 'red'
      } catch (err) {
        // 拦截错误，提示浏览器提供的错误信息，但是不中断程序的执行
        console.log(err.message)
        throw new Error('你看看，选择器错误了吧')
        // 需要加return 中断程序
        // return
      }
      finally {
        // 不管你程序对不对，一定会执行的代码
        alert('弹出对话框')
      }
      console.log(11)
    }
    fn()
  </script>
</body>
```

总结：

1. `try...catch` 用于捕获错误信息

2. 将预估可能发生错误的代码写在 `try` 代码段中

3. 如果 `try` 代码段中出现错误后，会执行 `catch` 代码段，并截获到错误信息

#### <font color="#2A878F">debugger</font>

相当于断点调试

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712150337660-1701221842.png)

### <font color="#A9D0D9">处理this</font>

#### <font color="#2A878F">普通函数</font>

**普通函数**的调用方式决定了 `this` 的值，即【谁调用 `this` 的值指向谁】，如下代码所示：

```html
<body>
  <button>点击</button>
  <script>
    // 普通函数：  谁调用我，this就指向谁
    console.log(this)  // window
    function fn() {
      console.log(this)  // window    
    }
    window.fn()
    window.setTimeout(function () {
      console.log(this) // window 
    }, 1000)
    document.querySelector('button').addEventListener('click', function () {
      console.log(this)  // 指向 button
    })
    const obj = {
      sayHi: function () {
        console.log(this)  // 指向 obj
      }
    }
    obj.sayHi()
  </script>
</body>
```

> 注： 普通函数没有明确调用者时 `this` 值为 `window`，严格模式下没有调用者时 `this` 的值为 `undefined`。

#### <font color="#2A878F">箭头函数</font>

> **箭头函数**中的 `this` 与普通函数完全不同，也不受调用方式的影响，事实上箭头函数中并不存在 `this` ！箭头函数中访问的 `this` 不过是箭头函数所在作用域的 `this` 变量。

```html
<script>
  console.log(this) // 此处为 window
  // 箭头函数
  const sayHi = function() {
    console.log(this) // 该箭头函数中的 this 为函数声明环境中 this 一致
  }
  // 普通对象
  const user = {
    name: '小明',
    // 该箭头函数中的 this 为函数声明环境中 this 一致
    walk: () => {
      console.log(this)
    },

    sleep: function () {
      let str = 'hello'
      console.log(this)
      let fn = () => {
        console.log(str)
        console.log(this) // 该箭头函数中的 this 与 sleep 中的 this 一致
      }
      // 调用箭头函数
      fn();
    }
  }

  // 动态添加方法
  user.sayHi = sayHi

  // 函数调用
  user.sayHi()
  user.sleep()
  user.walk()
</script>
```

> 在开发中【使用箭头函数前需要考虑函数中 `this` 的值】，**事件回调函数**使用箭头函数时，`this` 为全局的 `window`，因此DOM事件回调函数不推荐使用箭头函数，如下代码所示：

```html
<script>
  // DOM 节点
  const btn = document.querySelector('.btn')
  // 箭头函数 此时 this 指向了 window
  btn.addEventListener('click', () => {
    console.log(this)
  })
  // 普通函数 此时 this 指向了 DOM 对象
  btn.addEventListener('click', function () {
    console.log(this)
  })
</script>
```

> 同样由于箭头函数 `this` 的原因，**基于原型的面向对象也不推荐采用箭头函数**，如下代码所示：

```html
<script>
  function Person() {
  }
  // 原型对像上添加了箭头函数
  Person.prototype.walk = () => {
    console.log('人都要走路...')
    console.log(this); // window
  }
  const p1 = new Person()
  p1.walk()
</script>
```

#### <font color="#2A878F">改变this指向</font>

有 3 个方法可以动态指定普通函数中 `this` 的指向：

##### <font color="#6163d3">call()（了解）</font>

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712152304281-980943059.png)

```html
<script>
  const obj = {
    uname: 'cats'
  }
  function fn(x, y) {
    console.log(this) // window
    console.log(x + y)
  }
  // 1. 调用函数  
  // 2. 改变 this 指向
  fn.call(obj, 1, 2)
</script>
```

总结：

1. `call` 方法能够在调用函数的同时指定 `this` 的值

2. 使用 `call` 方法调用函数时，第1个参数为 `this` 指定的值

3. `call` 方法的其余参数会依次自动传入函数做为函数的参数

##### <font color="#6163d3">apply()</font>

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712152729974-761022780.png)

```html
<script>
  const obj = {
    age: 18
  }
  function fn(x, y) {
    console.log(this) // {age: 18}
    console.log(x + y)
  }
  // 1. 调用函数
  // 2. 改变this指向 
  //  fn.apply(this指向谁, 数组参数)
  fn.apply(obj, [1, 2])
  // 3. 返回值   本身就是在调用函数，所以返回值就是函数的返回值

  // 使用场景： 求数组最大值
  // const max = Math.max(1, 2, 3)
  // console.log(max)
  const arr = [100, 44, 77]
  const max = Math.max.apply(Math, arr)
  const min = Math.min.apply(null, arr)
  console.log(max, min)
  // 使用场景： 求数组最大值
  console.log(Math.max(...arr))
</script>
```

总结：

1. `apply` 方法能够在调用函数的同时指定 `this` 的值

2. 使用 `apply` 方法调用函数时，第1个参数为 `this` 指定的值

3. `apply` 方法第2个参数为**数组**，数组的单元值依次自动传入函数做为函数的参数

##### <font color="#6163d3">bind()</font>

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712153646660-2134165189.png)

```html
<body>
  <button>发送短信</button>
  <script>
    const obj = {
      age: 18
    }
    function fn() {
      console.log(this)
    }

    // 1. bind 不会调用函数 
    // 2. 能改变this指向
    // 3. 返回值是个函数，  但是这个函数里面的this是更改过的obj
    const fun = fn.bind(obj)
    // console.log(fun) 
    fun()

    // 需求，有一个按钮，点击里面就禁用，2秒钟之后开启
    document.querySelector('button').addEventListener('click', function () {
      // 禁用按钮
      this.disabled = true
      window.setTimeout(function () {
        // 在这个普通函数里面，我们要this由原来的window 改为 btn
        this.disabled = false
      }.bind(this), 2000)   // 这里的this 和 btn 一样
    })
  </script>
</body>
```

注：`bind` 方法创建新的函数，与原函数的唯一的变化是改变了 `this` 的值。

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712154546513-43870264.png)

### <font color="#A9D0D9">防抖节流</font>

![img](https://img2023.cnblogs.com/blog/3134450/202307/3134450-20230712161316261-1158915618.png)

1. 防抖（debounce）
   所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间

2. 节流（throttle）
   所谓节流，就是指连续触发事件但是在 n 秒中只执行一次函数

```html
<head>
  <meta charset="UTF-8" />
  <title>饿死的冏猫</title>
  <style>
    .box {
      width: 500px;
      height: 500px;
      background-color: #ccc;
      color: #fff;
      text-align: center;
      font-size: 100px;
    }
  </style>
</head>
<body>
  <div class="box"></div>
  <script>
    const box = document.querySelector('.box')
    let i = 1  // 让这个变量++
    // 鼠标移动函数
    function mouseMove() {
      box.innerHTML = ++i
      // 如果里面存在大量操作 dom 的情况，可能会卡顿
    }
    // 防抖函数
    function debounce(fn, t) {
      let timeId
      return function () {
        // 如果有定时器就清除
        if (timeId) clearTimeout(timeId)
        // 开启定时器 200
        timeId = setTimeout(function () {
          fn()
        }, t)
      }
    }
    // box.addEventListener('mousemove', mouseMove)
    box.addEventListener('mousemove', debounce(mouseMove, 200))
  </script>
</body>
```
