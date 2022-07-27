### 介绍

async 函数是什么？一句话，它就是 Generator 函数的语法糖。

async 函数对 Generator 函数的改进，体现在以下四点。

1. 内置执行器

2. 更好的语义

3. 更广的适用性

4. 返回值是 Promise

### 我们希望即使前一个异步操作失败，也不要中断后面的异步操作

正常会中断后面的执行，或者使用 try catch

```js
async function f() {
  await Promise.reject("出错了").catch((e) => console.log(e));
  return await Promise.resolve("hello world");
}

f().then((v) => console.log(v));
// 出错了
// hello world
```


### 如果不存在继发关系，最好让它们同时触发。

```js
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);

// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;
```


### async 函数的实现原理

async 函数的实现原理，就是将 Generator 函数和自动执行器，包装在一个函数里。