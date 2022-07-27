### 涵义

JavaScript 语言之中，`一切皆对象`，`运行环境也是对象`，所以函数都是在某个对象之中运行，`this`就是函数运行时所在的对象（环境）

但是 JavaScript 支持运行环境`动态切换`，也就是说，`this`的指向是`动态的`，没有办法`事先确定`到底指向哪个对象

``` javascript
// this代表属性“运行时”所在的对象。
var person = {
  name: '张三',
  describe: function () {
    return '姓名：'+ this.name;
  }
};

person.describe()
// "姓名：张三"
```

``` javascript
var A = {
  name: '张三',
  describe: function () {
    return '姓名：'+ this.name;
  }
};

var B = {
  name: '李四'
};

B.describe = A.describe;
B.describe()
// "姓名：李四"
```

### 深层this

```js
var a = {
  p: 'Hello',
  b: {
    m: function() {
      console.log(this.p);
    }
  }
};

a.b.m() // undefined
```


### 使用注意点

1. 避免多层 this
2. 避免数组处理方法中的 this
3. 避免回调函数中的 this



### 绑定 this 的方法

#### Function.prototype.call()

```js
var n = 123;
var obj = { n: 456 };

function a() {
  console.log(this.n);
}

a.call() // 123
a.call(null) // 123
a.call(undefined) // 123
a.call(window) // 123
a.call(obj) // 456
```

#### Function.prototype.apply()

```js
function f(x, y){
  console.log(x + y);
}

f.call(null, 1, 1) // 2
f.apply(null, [1, 1]) // 2
```


#### Function.prototype.bind()

bind()方法用于将函数体内的this绑定到某个对象，然后返回一个新函数。

```js
var d = new Date();
d.getTime() // 1481869925657

var print = d.getTime;
print() // Uncaught TypeError: this is not a Date object.

var print = d.getTime.bind(d);
print() // 1481869925657
```


### 箭头函数

箭头函数没有自己的`this`对象,`内部的this`就是定义时上层作用域中的`this`  --  也就是说，箭头函数内部的this指向是固定的

```js
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

var id = 21;

foo.call({ id: 42 });
// id: 42
```

上面代码中，`setTimeout()`的参数是一个箭头函数，这个箭头函数的定义生效是在`foo`函数生成时，而它的真正执行要等到 `100` 毫秒后。如果是`普通函数`，执行时`this`应该指向全局对象`window`，这时应该输出`21`。但是，箭头函数导致`this`总是`指向函数定义生效时`所在的对象（本例是{id: `42`}），所以打印出来的是`42`。



除了this，以下三个变量在箭头函数之中也是不存在的，指向外层函数的对应变量：
`arguments、super、new.target。`

```js
function foo() {
  setTimeout(() => {
    console.log('args:', arguments);
  }, 100);
}

foo(2, 4, 6, 8)
// args: [2, 4, 6, 8]
```