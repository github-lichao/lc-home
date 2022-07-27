### 概念

闭包是指有权访问另外一个函数作用域中的变量的函数

### 应用场景

1. 节流防抖
2. 函数柯里化
3. 给元素伪数组添加事件

其实也可以用 let 去做

```js
// DOM操作
let li = document.querySelectorAll("li");
for (var i = 0; i < li.length; i++) {
  (function (i) {
    li[i].onclick = function () {
      alert(i);
    };
  })(i);
}
```

4. 不使用循环返回数组

有点类似函数柯里化，保存上一个函数的值

```js
function getArr() {
  let num = 10;
  let arr = [];
  return (function () {
    arr.unshift(num);
    num--;
    if (num > 0) {
      arguments.callee();
    }
    return arr;
  })();
}
console.log(getArr()); //[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

5. 使用闭包模拟私有变量

```js
var counter = (function () {
  var privateCounter = 0;

  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function () {
      changeBy(1);
    },
    decrement: function () {
      changeBy(-1);
    },
    value: function () {
      return privateCounter;
    },
  };
})();
counter.value(); //0
counter.increment(); //1
counter.increment(); //2
counter.decrement(); //1
```
