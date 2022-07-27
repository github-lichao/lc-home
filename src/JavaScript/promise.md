### 缺点

1. 无法取消Promise，一旦新建它就会立即执行，无法中途取消

2. 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部

3. 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

如果某些事件不断地反复发生，一般来说，使用 Stream 模式是比部署Promise更好的选择。



### 注意

一般来说，不要在then()方法里面定义 Reject 状态的回调函数（即then的第二个参数），总是使用catch方法。


一般总是建议，Promise 对象后面要跟catch()方法，这样可以处理 Promise 内部发生的错误。

### then/catch

catch() 是 then 第二个参数的语法糖

catch()方法返回的还是一个 Promise 对象，因此后面还可以接着调用then()方法。


then方法返回的是一个新的Promise实例（注意，不是原来那个Promise实例）。因此可以采用链式写法，即then方法后面再调用另一个then方法。

```js
const someAsyncThing = function() {
  return new Promise(function(resolve, reject) {
    // 下面一行会报错，因为x没有声明
    resolve(x + 2);
  });
};

someAsyncThing()
.catch(function(error) {
  console.log('oh no', error);
})
.then(function() {
  console.log('carry on');
});
// oh no [ReferenceError: x is not defined]
// carry on
```


### finally()

不管 Promise 对象最后状态如何，都会执行的操作


服务器使用 Promise 处理请求，然后使用finally方法关掉服务器

``` js
server.listen(port)
  .then(function () {
    // ...
  })
  .finally(server.stop);
  // 或者
  .finally(() => {
    // doSomething
  })
```

finally方法的回调函数不接受任何参数，这意味着没有办法知道，前面的 Promise 状态到底是fulfilled还是rejected。这表明，finally方法里面的操作，应该是与状态无关的，不依赖于 Promise 的执行结果。


### all()

只有都成功了，才会成功

参数的 Promise 实例，自己定义了catch方法，那么它一旦被rejected，并不会触发Promise.all()的catch方法。

```
// 生成一个Promise对象的数组
const promises = [2, 3, 5, 7, 11, 13].map(function (id) {
  return getJSON('/post/' + id + ".json");
});

Promise.all(promises).then(function (posts) {
  // ...
}).catch(function(reason){
  // ...
});
```

上面代码中，promises是包含 6 个 Promise 实例的数组，只有这 6 个实例的状态都变成fulfilled，或者其中有一个变为rejected，才会调用Promise.all方法后面的回调函数。



### race()

只要p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变


``` js
const p = Promise.race([
  fetch('/resource-that-may-take-a-while'),
  new Promise(function (resolve, reject) {
    setTimeout(() => reject(new Error('request timeout')), 5000)
  })
]);

p
.then(console.log)
.catch(console.error);
```


### allSettled()

得到所有的状态，all只能得到全部成功的状态，和一个失败的状态，race只能得到最快的状态

``` js
const promises = [
  fetch('/api-1'),
  fetch('/api-2'),
  fetch('/api-3'),
];

await Promise.allSettled(promises);
removeLoadingIndicator();
```

上面示例中，数组promises包含了三个请求，只有等到这三个请求都结束了（不管请求成功还是失败），removeLoadingIndicator()才会执行。



### any()

等到一个成功的，除非全部失败

``` js
Promise.any([
  fetch('https://v8.dev/').then(() => 'home'),
  fetch('https://v8.dev/blog').then(() => 'blog'),
  fetch('https://v8.dev/docs').then(() => 'docs')
]).then((first) => {  // 只要有一个 fetch() 请求成功
  console.log(first);
}).catch((error) => { // 所有三个 fetch() 全部请求失败
  console.log(error);
});
```


### resolve()

有时需要将现有对象转为 Promise 对象，Promise.resolve()方法就起到这个作用。

```
const jsPromise = Promise.resolve($.ajax('/whatever.json'));
```

```
Promise.resolve('foo')
// 等价于
new Promise(resolve => resolve('foo'))
```


### reject()


```
const p = Promise.reject('出错了');
// 等同于
const p = new Promise((resolve, reject) => reject('出错了'))

p.then(null, function (s) {
  console.log(s)
});
// 出错了
```


### try()

让同步函数同步执行，异步函数异步执行

```
const f = () => console.log('now');
Promise.try(f);
console.log('next');
// now
// next
```

因为这样就可以不管f是否包含异步操作，都用then方法指定下一步流程，用catch方法处理f抛出的错误
