## Object.assign、扩展运算符

> Object.assign 、扩展运算符 是 浅拷贝

```js
// 如果源对象某个属性的值是基本类型，没有问题
let a = { a: 1 };
let b = Object.assign({}, a);
console.log(a); // {a:1}
a.a = 3;
console.log(b); // {a:1}

// 如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。

const obj1 = { a: { b: 1 } };
const obj2 = Object.assign({}, obj1);
// 或者
// const obj2 = { ...obj1 };

obj1.a.b = 2;
obj2.a.b; // 2
```

## 作用域

**JavaScript采用的是静态作用域，函数定义的位置就决定了函数的作用域**

- **作用域：**规定了如何查找变量。
- **静态作用域：**又称词法作用域，函数的作用域在函数定义的时候就决定了，通俗点说就是你在写代码时将变量和块作用域写在哪里决定的。
- **动态作用域：**函数的作用域在函数调用时才决定的。

```js
var val = 1;
function test() {
    console.log(val);
}
function bar() {
    var val = 2;
    test();
}

bar();
// 结果是 1
```
