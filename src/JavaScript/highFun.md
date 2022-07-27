
### 高阶函数

英文叫Higher-order function。JavaScript的函数其实都指向某个变量。既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。

>高阶函数就是对其他函数进行操作的函数，它接收函数作为参数或将函数作为返回值输出。

### 一个最简单的高阶函数

```js
function add(x, y, f) {
    return f(x) + f(y);
}
```

当我们调用add(-5, 6, Math.abs)时，参数x，y和f分别接收-5，6和函数Math.abs，根据函数定义，我们可以推导计算过程为：

```js
x = -5;
y = 6;
f = Math.abs;
f(x) + f(y) ==> Math.abs(-5) + Math.abs(6) ==> 11;
return 11;
```

### JavaScript中的内置高阶函数

1. map(); // array.map(callback,[ thisObject]);

```js
const arr = [1, 2, 3];
const newArr = arr.map(item => item * 2);
console.log(newArr); //[2, 4, 6]
```

2. reduce(); // array.reduce(function(total, currentValue, currentIndex, arr), initialValue);

```js
const arr = [1, 2, 3];
let sum = arr.reduce((accumulator, currentValue, currentIndex, array) => {
    return accumulator + currentValue;
});
console.log(sum); // 10
const arr = [1, 2, 3];
let sum1 = arr.reduce((accumulator, currentValue, currentIndex, array) => {
    return accumulator + currentValue;
}, 10);
console.log(sum1); // 20
```

1. filter(); // array.filter(callback(element[, index[, array]])[, thisArg])

```js
const arr = [1, 1, 2, 2, 3, 4, 3, 4, 5, 5, 4];
const newArr = arr.filter((ele, index, self) => {
    return self.indexOf(ele) === index;
});
console.log(newArr); // [1, 2, 3, 4, 5]
```

4. sort(); // arr.sort([compareFunction])

```js
const arr = [1, 20, 10, 5];
let compareNumbers= function (a, b) {
    return a - b;
}
const newArr = arr.sort(compareNumbers);
console.log(newArr); // [1, 5, 10, 20]
```
<!-- #### 自动计算高度class

https://codesandbox.io/s/gaojiezujian-8kvzu?file=/src/HocWindowInnerHeight/index.js


#### 自动计算高度hooks

https://codesandbox.io/s/gaojiezujian-8kvzu?file=/src/HocWindowInnerHeight/indexHook.js -->