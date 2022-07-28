### 基本类型

>Number、String、Boolean、Undefined、null、symbol

### 引用类型
>Object、Array、Function

### undefined和null的区别

>undefined:表示不存在这个值。一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但还 没 有定义。当尝试读取时会返回 undefined

例如变量被声明了，但没有赋值时，就等于 undefine

>null: 表示一个对象被定义了，值为’空值‘

```js
null == undefined // true
null === undefined // false
```

### === 和==的区别
>===  三个等号称为同等符。
```
当等号两边的值类型相同的时候，直接比较等号两边的值。值相同则返回true。
若等号两边的值类型不同时直接返回false。
就是说三个等号，既要判断值也要判断类型是否相等。
```
>==  两个等号称为等值符
```
当等号两边的值为相同类型时，比较值是否相同，
类型不同时 会发生类型的自动转换，转换为相同类型后再作比较。
总的来说就是两个等号 只要值相等 就可以
```

### 数组去重
>利用 ES6 set 关键字
```js
function unique(arr) {
  return [...new Set(arr)];
}
```

>利用 ES5 filter 方法：
```js
function unique(arr) {
  return arr.filter((item, index, array) => {
    return array.indexOf(item) === index;
  });
}
```

>for循环 + splice 去重
```js
let arr = [0, 2, 4, 7, 1, 2, 0];
function unipue(arr) {
    for(var i = 0; i < arr.length; i++) {
        for(var j = i + 1; j < arr.length; j++) {
            if(arr[i] === arr[j]){
                arr.splice(j, 1);
            }
        }
    }
}
unipue(arr); // [0, 2, 4, 7, 1]
```

### 防抖、节流
>防抖：单位时间内，频繁触发一个事件，以最后一次触发为准

#### 防抖的实现：
- 声明一个全部变量存储定时器ID。
- 每一次触发交互的时候，先清除上一次的定时器，然后开启本次定时器。
```js
      //输入框事件
      let timeID = null
      document.querySelector('input').oninput = function () {
        //1先清除之前的定时器
        clearTimeout(timeID)
        //2.开启本次定时器
        timeID = setTimeout(() => {
          console.log(`发送ajax,搜索的内容是${this.value}`)
        }, 500)
      }
```

>节流 ：规定在一个单位时间内，只能触发一次函数。如果这个单位时间内触发多次函数，只有一次生效。

#### 节流的实现：
- 声明一个全局变量存储触发事件。
- 每一次触发事件，获取当前时间。
- 判断当前时间与上一次触发事件，是否超过了间隔。
- 如果超过间隔时间，则执行事件处理代码，然后存储本次触发的时间。
```js
    //声明一个全局变量存储触发时间
    let lastTime = null
    //页面滚动事件
    window.onscroll = function () {
      //1.每一次触发 先获取本次时间戳
      let currentTime = Date.now()
      //2.判断当前时间 与 上次触发时间 是否超过间隔
      if (currentTime - lastTime >= 500) {
        console.log(document.documentElement.scrollTop)//获取滚动距离
        //3.存储本次的触发时间
        lastTime = currentTime
      }
    }
```

#### 应用场景：
>防抖：search联想搜索，用户在不断输入内容的时候，用防抖来节约请求资源。window触发resize时候，不断调整浏览器窗口大小会不断的触发这个事件，用防抖让其只触发一次。

>节流：鼠标不断点击（mousedown）触发，让其单位时间内只触发一次。监听滚动事件，滑到底部自动加载更多。

### 实现数组扁平化

#### ES6 flat(),括号内不写数字，默认拉平一级。可以写数字，写几就拉平几级。也可以写Infinity，代表无穷大
```js
let arr = [1, [2, 3, [4], 5], 6];
let newArr = arr.flat(Infinity);
console.log(newArr); //[1, 2, 3, 4, 5, 6]
```

#### split和toString共同处理
数组会默认带一个toString的方法，所以可以把数组直接转换成逗号分隔的字符串，然后再用split方法把字符串重新转换为数组，
>这种转换方式会有个问题，值最后返回的是字符串类型。
```js
let arr = [1, [2, [4, [5, [6]]]]];
function flatten3(arr) {
	return arr.toString().split(',');
}
console.log(flatten3(arr));	// ['1','2','3','4','5','6']
```

#### 递归
```js
let arr = [1, [2, 3, [4], 5], 6];
const myFlat = (arr) => {
  const helper = (arr) => {
    let res = [];
    for (const item of arr) {
      if (typeof item === 'object') {
        res.push(...item);
      } else {
        res.push(item);
      }
    }
    return res;
  };

  while (arr.some(item => typeof item === 'object')) {
    arr = helper(arr);
  }
  return arr;
};
console.log(myFlat(arr)); //[1, 2, 3, 4, 5, 6]

```

#### JSON和正则表达式共同实现
用JSON.stringify的方法先转换为字符串，然后通过正则表达式过滤掉字符串中的数组的方括号，最后再利用JSON.parse把它转换成数组
```js
let arr = [1, [2, [4, [5, [6]]]]]	;
function flatten(arr) {
	let str = JSON.stringify(arr);
	str = str.replace(/(\[|\])/g, '');
	str = '[' + str + ']';
	return JSON.parse(str);
}
console.log(flatten(arr)); //[1, 2, 4, 5, 6]
```

### ES6 新加入的 Symbol 是个什么东西？

>ES5 的对象属性名都是字符串，这容易造成属性名的冲突，ES6 引入了一种新的原始数据类型 Symbol，表示独一无二的值

### let const 和 var

> let和const是ES6新增的声明变量的关键词，之前声明变量的关键词是var。

#### let
- 声明之后可以更改，声明时可以不赋值。
- 不存在变量提升。即所声明的变量一定要在声明后使用。
- 存在块级作用域。
- 在同一作用域不允许重复声明变量，会报错

#### const
- 一旦声明必须赋值,不能使用null占位。
- 声明后不能再修改。
- 如果声明的是复合类型数据，可以修改其属性
- 存在块级作用域。
- 在同一作用域不允许重复声明变量，会报错。

#### var
- 声明之后可以更改，声明时可以不赋值。
- 允许重复声明变量，后一个变量会覆盖前一个变量。
- var声明的变量存在变量提升（将变量提升到当前作用域的顶部）。即变量可以在声明之前调用，值为undefined。
- 全局作用域。

### for...in 和 for...of 的区别
推荐 for...of 遍历数组, for...in 循环对象

>for...of 循环，作为遍历所有数据结构的统一的方法,一个数据结构只要部署了 Symbol.iterator 属性，就被视为具有 iterator 接口，就可以用 for...of 循环遍历它的成员

>for...in 循环出的是 key，for...of 循环出的是 value

>for...of 循环调用遍历器接口，数组的遍历器接口只返回具有数字索引的属性。这一点跟 for...in 循环也不一样。

```js
let arr = [3, 5, 7];
arr.foo = "hello";

for (let i in arr) {
  console.log(i); // "0", "1", "2", "foo"
}

for (let i of arr) {
  console.log(i); //  "3", "5", "7"
}
```

### setTimeout、Promise、Async/Await 的区别
事件循环中分为宏任务队列和微任务队列。

其中settimeout的回调函数放到宏任务队列里，等到执行栈清空以后执行；

new Promise 回调立即执行

promise.then 里的回调函数会放到相应宏任务的微任务队列里，等宏任务里面的同步代码执行完再执行；

async函数表示函数里面可能会有异步方法，await后面跟一个表达式，

async方法执行时，遇到await会立即执行表达式（这个函数里有微任务是先放进队列中，然后是await 下面的代码），

await 表达式下面的代码（await下面的代码）放到微任务队列里，让出执行栈让同步代码先执行。

### JavaScript 是单线程还是多线程
本质考察的是消息队列和事件循环

- 首先，JavaScript 是单线程，这是它的核心特征，现在和未来都不会改变，即使加入 Web Worker，但子线程完全受主线程控制，不会改变 JavaScript 单线程的本质
- 为了统筹调度唯一主线程上的各种任务，引入消息队列和时间循环机制
- 有需要的话可以展开详述，不过这就是另一个大坑了......

### 闭包
一句话解释: 能够读取其他函数内部变量的函数。

应用场景
- 回调函数
  - 发送 ajax 请求成功|失败的回调
  - setTimeout 的延时回调
  - 一个函数内部返回另一个匿名函数
- 柯里化
- 私有变量

闭包的缺点
- 内存泄露
- 不要随便改变父函数内部变量的值

### call apply bind 之间的关系 & 实现
>call的第二个参数可以是任意类型
>apply的第二个参数必须是数组或类数组
>它两的第一个参数是一个对象。Function的调用者，将会指向这个对象。如果不传，则默认为全局对象window
>bind与call，apply不同的是：返回的值是一个函数，并且需要调用后，才可以执行。

```js
function add(a,b){
    console.log(a+b);
}
function sub(a,b){
    console.log(a-b);
}
add.call(sub, 1, 3); 
//函数sub调用函数add里的方法（a+b）
//输出 4
```
详细的请看：https://juejin.cn/post/6844903773979033614

### 数据类型的判断
typeof：能判断所有 基本类型，函数。不可对 null、对象、数组进行精确判断，因为都返回 object 。
```js
console.log(typeof undefined); // undefined
console.log(typeof 2); // number
console.log(typeof true); // boolean
console.log(typeof "str"); // string
console.log(typeof Symbol("foo")); // symbol
console.log(typeof 2172141653n); // bigint
console.log(typeof function () {}); // function
// 不能判别
console.log(typeof []); // object
console.log(typeof {}); // object
console.log(typeof null); // object
```

instanceof：能判断 对象类型，不能判断 基本数据类型，其内部运行机制是判断在其原型链中能否找到该类型的原型。比如考虑以下代码：
```js
class People {}
class Student extends People {}

const vortesnail = new Student();

console.log(vortesnail instanceof People); // true
console.log(vortesnail instanceof Student); // true
```
Object.prototype.toString.call()：所有原始数据类型都是能判断的，还有 Error 对象，Date 对象等。
```js
Object.prototype.toString.call(2); // "[object Number]"
Object.prototype.toString.call(""); // "[object String]"
Object.prototype.toString.call(true); // "[object Boolean]"
Object.prototype.toString.call(undefined); // "[object Undefined]"
Object.prototype.toString.call(null); // "[object Null]"
Object.prototype.toString.call(Math); // "[object Math]"
Object.prototype.toString.call({}); // "[object Object]"
Object.prototype.toString.call([]); // "[object Array]"
Object.prototype.toString.call(function () {}); // "[object Function]"
```
在面试中有一个经常被问的问题就是：如何判断变量是否为数组？
```js
Array.isArray(arr); // true
arr.__proto__ === Array.prototype; // true
arr instanceof Array; // true
Object.prototype.toString.call(arr); // "[object Array]"
```

### 基本的数据类型介绍，及值类型和引用类型的理解
在 JS 中共有 8 种基础的数据类型，分别为： Undefined 、 Null 、 Boolean 、 Number 、 String 、 Object 、 Symbol 、 BigInt 。

- 其中 Symbol 和 BigInt 是 ES6 新增的数据类型，可能会被单独问：
- Symbol 代表独一无二的值，最大的用法是用来定义对象的唯一属性名。
- BigInt 可以表示任意大小的整数。
- 基本类型 是直接存储在栈（stack）中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；

引用类型 存储在堆（heap）中的对象，占据空间大、大小不固定。如果存储在栈中，将会影响程序运行的性能；