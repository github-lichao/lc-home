### valueOf()

valueOf方法是一个所有对象都拥有的方法，返回指定对象的原始值。

不同对象的valueOf方法不尽一致，

```js
// 数组的valueOf方法返回数组本身。
var arr = [1, 2, 3];
arr.valueOf() // [1, 2, 3]


// Boolean 布尔值
true.valueOf()  // true


// Date
const date = new Date();  // Fri Sep 10 2021 14:13:07 GMT+0800 (中国标准时间) {}
date.valueOf();  // 1631254411540

new Date().valueOf()   // 获取当前时间时间戳。 1631091318854

new Date('2021-09-09 10:00:00').valueOf()     // 把指定时间转为时间戳

// 把当前时间戳转为日期格式（年月日 -- 2021-09-10）
moment(
  new Date(new Date().valueOf()),
  "YYYY/MM/DD"
)                                             


// Function
new Function().valueOf()  // ƒ anonymous() {}


// Number
let n = new Number(1)
n.valueOf()   // 1


// Object
let o = new Object()
o.valueOf()   // {}


// String
'11'.valueOf()    // '11'


// Error
let e = new Error();
e.valueOf()       // Error  at <anonymous>:1:9


// Symbol
let s = Symbol()
s.valueOf()       // Symbol()

```

### toString()

toString方法也是对象的通用方法，数组的toString方法返回数组的字符串形式。

``` js
var arr = [1, 2, 3];
arr.toString() // "1,2,3"

var arr = [1, 2, 3, [4, 5, 6]];
arr.toString() // "1,2,3,4,5,6"
```


### 什么时候会自动调用

toString 和 valueOf 是一直会调用的，但是里面输出的内容需要注意一下，可能发生类型转换，

- 比如：
  - alert 只能输出字符串，如果输入的不是字符串，
  - 输出的值我们使用了 `模版字符串`，调用 toString
  - 输出的值乘以1，或者自增，会自动调用 valueOf


下面这个输出就有问题

```js
function add() {
    // 第一次执行时，定义一个数组专门用来存储所有的参数
    var _args = Array.prototype.slice.call(arguments);

    // 在内部声明一个函数，利用闭包的特性保存_args并收集所有的参数值
    var _adder = function() {
        _args.push(...arguments);
        return _adder;
    };

    // 利用toString隐式转换的特性，当最后执行时隐式转换，并计算最终的值返回
    _adder.toString = function () {
        return _args.reduce(function (a, b) {
            return a + b;
        });
    }
    return _adder;
}

add(1)(2)(3)  // 输出的是一个function

// 下面这个输出的是 6，因为发生了类型转换
alert(add(1)(2)(3))
```