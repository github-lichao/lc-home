数组的总结

## 创建数组

``` js
// bad
var arr = new Array(1, 2);

// good
var arr = [1, 2];
```

## 改变原有数组的方法：(9个)

### splice() 添加/删除数组元素

```js
let a = [1, 2, 3, 4, 5, 6, 7];
let item = a.splice(0, 3); // [1,2,3]
console.log(a); // [4,5,6,7]
// 从数组下标0开始，删除3个元素
let item1 = a.splice(0,3,'添加'); // [4,5,6]
console.log(a); // ['添加',7]
// 从数组下标0开始，删除3个元素，并添加元素'添加'
```

### sort() 数组排序

```js
 var array =  [10, 1, 3, 4,20,4,25,8];
 // 升序 a-b < 0   a将排到b的前面，按照a的大小来排序的 
 array.sort(function(a,b){
   return a-b;
 });
 console.log(array); // [1,3,4,4,8,10,20,25];
 // 降序 
 array.sort(function(a,b){
   return b-a;
 });
 console.log(array); // [25,20,10,8,4,4,3,1];
 ```

 ### pop() 删除一个数组中的最后的一个元素

 ### shift() 删除数组的第一个元素

 ### push() 向数组的末尾添加元素


### unshift()向数组开头添加元素


### reverse() 

 ```js
  let  a =  [1,2,3];
  a.pop();  // 3, 返回被删除的元素
  console.log(a); // [1,2]
  a.shift(); // 1
  console.log(a); // [2]
  a.push("末尾添加");  // 2 ,返回数组长度
  console.log(a) ; [2,"末尾添加"]
  a.unshift("开头添加"); // 3
  console.log(a); //["开头添加", 2, "末尾添加"]
  a.reverse();   // ["末尾添加", 2, "开头添加"]
  console.log(a) // ["末尾添加", 2, "开头添加"]  
  ```

### ES6: copyWithin() 指定位置的成员复制到其他位置

```js
let a = ['zhang', 'wang', 'zhou', 'wu', 'zheng'];
 // 1位置开始被替换, 2位置开始读取要替换的  5位置前面停止替换
 a.copyWithin(1, 2, 5);
 // ["zhang", "zhou", "wu", "zheng", "zheng"]
 ```

### ES6: fill() 填充数组

```js
['a', 'b', 'c'].fill(7)
// [7, 7, 7]
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```

## 不改变原数组的方法(6 种)

### join() 数组转字符串

```js
let a= ['hello','world'];
let str2=a.join('+'); // 'hello+world'

a.join() // "1,2,3,4"  默认用逗号分隔

[undefined, null].join('#') // '#'  如果数组成员是undefined或null或空位，会被转成空字符串
['a',, 'b'].join('-') // 'a--b'  如果数组成员是undefined或null或空位，会被转成空字符串
```


### cancat 合并两个或多个数组

```js
let a = [1, 2, 3];
let b = [4, 5, 6];
//连接两个数组
let newVal=a.concat(b); // [1,2,3,4,5,6]
```

### ES6 扩展运算符...合并数组

```js
 let a = [2, 3, 4, 5]
 let b = [ 4,...a, 4, 4]
 console.log(a,b); 
 //[2, 3, 4, 5] [4,2,3,4,5,4,4]
```

### indexOf() 查找数组是否存在某个元素，返回下标

```js
let a=['啦啦',2,4,24,NaN]
console.log(a.indexOf('啦'));  // -1 
console.log(a.indexOf('啦啦')); // 0
```

### ES7 includes() 查找数组是否包含某个元素 返回布尔

>1. indexOf 方法不能识别 NaN

>2. indexOf 方法检查是否包含某个值不够语义化，需要判断是否不等于-1，表达不够直观

```js
let a=['OB','Koro1',1,NaN];
a.includes(NaN); // true 识别NaN
a.includes('Koro1',100); // false 超过数组长度 不搜索
a.includes('Koro1',-3);  // true 从倒数第三个元素开始搜索 
```

### slice() 浅拷贝数组的元素

>字符串也有一个 slice() 方法是用来提取字符串的，不要弄混了。

```js
 let a = [{name: 'OBKoro1'}, {name: 'zhangsan'}];
 let b = a.slice(0,1);
 console.log(b, a); // 下面是因为浅拷贝的原因
 // [{"name":"OBKoro1"}]  [{"name":"OBKoro1"}]
 a[0].name='改变原数组';
 console.log(b,a); 
 // [{"name":"改变原数组"}] [{"name":"改变原数组"}]
```

## 遍历方法

### for循环

``` js
var a = [1, 2, 3];

// for循环
for(var i = 0; i < a.length; i++) {
  console.log(a[i]);
}
```

### forEach:按升序为数组中含有效值的每一项执行一次回调函数

> 1.无法中途退出循环，只能用 return 退出本次回调，进行下一次回调.  

> 2.它总是返回 undefined 值,即使你 return 了一个值。


### every 检测数组所有元素是否都符合判断条件

> 如果数组中检测到有一个元素不满足, 则整个表达式返回 false,且元素不会再进行检测


```js
function isBigEnough(element, index, array) { 
  return element >= 10; // 判断数组中的所有元素是否都大于10
}
[12, 5, 8, 130, 44].every(isBigEnough);   // false
[12, 54, 18, 130, 44].every(isBigEnough); // true
// 接受箭头函数写法 
[12, 5, 8, 130, 44].every(x => x >= 10); // false
[12, 54, 18, 130, 44].every(x => x >= 10); // true
```

### some 数组中的是否有满足判断条件的元素

> 如果有一个元素满足条件，则表达式返回 true, 剩余的元素不会再执行检测

### filter 过滤原始数组，返回新数组

``` js
[1, 2, 3, 4, 5].filter(function (elem) {
  return (elem > 3);
})
// [4, 5]
```

### map 对数组中的每个元素进行处理，返回新的数组

### reduce && reduceRight 为数组提供累加器，合并为一个值

> reduce() 方法对累加器和数组中的每个元素（从左到右）应用一个函数，最终合并为一个值。

```js
// 数组求和 
let sum = [0, 1, 2, 3].reduce(function (a, b) {
  return a + b;
}, 0);
// 6
// 将二维数组转化为一维 将数组元素展开
let flattened = [[0, 1], [2, 3], [4, 5]].reduce(
  (a, b) => a.concat(b),
  []
);
// [0, 1, 2, 3, 4, 5]
```

### ES6：find()& findIndex() 根据条件找到数组成员

> 这两个方法都可以识别 NaN,弥补了 indexOf 的不足.

```js
[1, 4, -5, 10,NaN].find((n) => Object.is(NaN, n)); 
// 返回元素NaN
[1, 4, -5, 10].findIndex((n) => n < 0); 
// 返回索引2
```

### ES6 keys()&values()&entries() 遍历键名、遍历键值、遍历键名+键值

一个数据结构只要部署了Symbol.iterator属性（可遍历），就被视为具有 iterator 接口，就可以用for...of循环遍历它的成员

```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1    
for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'    
for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```


``` js
Object.prototype.objCustom = function() {}; 
Array.prototype.arrCustom = function() {};

let iterable = [3, 5, 7];
iterable.foo = 'hello';

for (let i in iterable) {
  console.log(i); // 0, 1, 2, "foo", "arrCustom", "objCustom"
}

for (let i in iterable) { 
  if (iterable.hasOwnProperty(i)) {
    // 所以不推荐使用for...in遍历数组，会多出 foo 这个
    console.log(i); // 0, 1, 2, "foo"
  }
}
// 不会遍历自定义属性
for (let i of iterable) {
  console.log(i); // logs 3, 5, 7
}

```


### while 、 do while

do while先执行后判断，循环至少执行一次，即便条件为false

while先判断后执行

```js
var a = [1, 2, 3];

var i = 0;
while (i < a.length) {
  console.log(a[i]);
  i++;
}

var l = a.length;
while (l >= 0) {
  console.log(a[l]);
  l--
}
```

```js
let i = 2;

do {
  console.lg(i);  // 2
  i++
} while (i < 2) {
  console.log(i);   // 3
}
```




## 判断一个 object 是否是数组

1. Array.isArray

``` js
var arr = [1, 2, 3];

typeof arr // "object"
Array.isArray(arr) // true
```

2. Object.prototype.toString

这里使用 call 来使 toString 中 this 指向 obj。进而完成判断
```js
function isArray(obj){
 return Object.prototype.toString.call( obj ) === '[object Array]';
}
```

3. 原型链

基本思想: 实例如果是某个构造函数构造出来的那么 它的 `__proto__` 是指向构造函数的 prototype属性

```js
function isArray(obj){
 return obj.__proto__ === Array.prototype;
}
```

## 链式使用

``` js
var users = [
  {name: 'tom', email: 'tom@example.com'},
  {name: 'peter', email: 'peter@example.com'}
];

users
.map(function (user) {
  return user.email;
})
.filter(function (email) {
  return /^t/.test(email);
})
.forEach(function (email) {
  console.log(email);
});
// "tom@example.com"
```