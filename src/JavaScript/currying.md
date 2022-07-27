### 介绍

柯里化本质上是降低通用性，提高适用性

递归调用柯里化函数，返回一个保存了上一个传入参数的函数，其实就是利用闭包来保存之前传入的参数，使得后续函数可以直接使用

```js
// lodash 的函数柯里化 _.curry
var abc = function (a, b, c) {
  return [a, b, c];
};

var curried = _.curry(abc);

curried(1)(2)(3);
// => [1, 2, 3]

curried(1, 2)(3);
// => [1, 2, 3]

curried(1, 2, 3);
// => [1, 2, 3]

// Curried with placeholders.
curried(1)(_, 3)(2);
// => [1, 2, 3]
```

### 作用

1. 参数复用

2. 延迟执行

3. 动态创建

### 参数复用

需要根据参数拼接出几个完整的地址

```js
// 常规实现
function spliceUrl(protocol, hostname, patchname) {
  return `${protocol}${hostname}${patchname}`;
}

const url1 = spliceUrl("https://", "aa.com", "/get/aa/");
const url2 = spliceUrl("https://", "aa.com", "/get/aa/");
```

```js
// currying写法
function spliceUrl(protocol, hostname) {
  return function (patchname) {
    return `${protocol}${hostname}${patchname}`;
  };
}

const urlBase = spliceUrl("https://", "aa.com");
const url1 = urlBase("/get/aa/");
const url2 = urlBase("/get/aa/");
```

### 延迟执行

在实现一个求和函数的时候，希望传入的参数能满足 sum(1)(2)(3)(4);

```js
// 实现一个add方法，使计算结果能够满足如下预期：
// add(1)(2)(3) = 6;
// add(1, 2, 3)(4) = 10;
// add(1)(2)(3)(4)(5) = 15;

const add = (...a) => {
  let num = a.reduce((t, c) => t + c, 0);

  const item = (...b) => {
    num = num + b.reduce((t, c) => t + c, 0);
    return item;
  };

  item.toString = () => num;

  return item;
};

// 需要放在alert中触发toString，才能看到正确结果；如果用console.log，结果是函数，不能触发 toString
// 因为alert只能输出字符串，发生了隐式类型转换，就会调用 toString 和 valueOf
// 因为 console 可以输出各种类型，所以不会发生隐式类型转换，所以就不会调用 toString 和 valueOf
alert(add(1)(2)(3)); // 6
alert(add(1, 2, 3)(4)); // 10
alert(add(1)(2)(3)(4)(5)); // 15
alert(add(2, 6)(1)); // 9
```

### 动态创建

使用监听事件时，判断浏览器兼容性

```js
const whichEvent = (function () {
  if (document.addEventListener) {
    return function (element, event, handler) {
      if (element && event && handler) {
        element.addEventListener(event, handler, false);
      }
    };
  } else {
    return function (element, event, handler) {
      if (element && event && handler) {
        element.attachEvent("on" + event, handler);
      }
    };
  }
})();
```
