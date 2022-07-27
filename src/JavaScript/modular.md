### 介绍

将一个复杂的程序依据一定的规则(规范)封装成几个块(文件), 并进行组合在一起 块的内部数据与实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信

### CommonJS(NodeJS)

把整个模块都加载进来，运行时加载 -- require、module.exports

```js
// example.js
var x = 5;
var addX = function (value) {
  return value + x;
};

// bad
module.exports.x = x;
module.exports.addX = addX;
```

```js
// A文件
var firstName = "Michael";
var lastName = "Jackson";
var year = 1958;

// good
module.exports = {
  firstName,
  lastName,
  year,
};
```

```js
// 导入是一样的
// B文件
const Info = require("./A");
console.log(Info); // {firstName: "Michael", lastName: "Jackson", year: 1958}

// 当然，也可以使用解构赋值 -- 但是还是加载了整个对象
const { year } = require("./A");
console.log(year); // 1958
```


### ESModule(ES6 模块)


#### 单独导出

``` js
// A文件
// bad
export var firstName = "Michael";
export var lastName = "Jackson";
export var year = 1958;
```

``` js
// good
var firstName = "Michael";
var lastName = "Jackson";
var year = 1958;

// 这个大括号只是大括号而已，它圈定哪些变量要被输出去
// commonjs module.export = 后面接的真的是个对象
export { firstName, lastName, year };  
```

`导入`

``` js
// 一般写法
import { year } from "./A";
console.log(year); // 1958

// 重命名写法
import { year as thatYear } from ".A"; // 重命名变量
console.log(year); // 1958

// 导入全部模块并存在一个对象里
import * as Info from "./A";
console.log(Info); // Module {firstName: "Michael", lastName: "Jackson", year: 1958}
```

#### 默认导出

``` js
// A文件
var firstName = "Michael";
var lastName = "Jackson";
var year = 1958;

export default { nn: firstName, lastName, year }; // 现在就不报错了，因为后面跟的真的是一个对象
```

`导入`

``` js
import JacksonInfo from "./A";
console.log(JacksonInfo); // {firstName: "Michael", lastName: "Jackson", year: 1958}
```


#### 转发导出

```js
export { year, firstName } from "./A";

// 上面这种写法基本等同于下面这两句，不过上面的写法有个特别之处，那就是转发导出的模块，是没有导入到当前模块的，所以才说和下面的写法“基本相同”
import { year, firstName } from "./A";
export { year, firstName };
```

### CommonJS 和 ES6 模块的区别

1. ES6模块是静态导入，编译时加载的；而CommonJS是动态导入，运行时加载的；

2. **ES6模块不使用默认导出时**，即使导出原始数据类型，导出的仍然是其引用。而CommonJS导出原始数据类型则只是导出一个值而已；

``` js
// CommonJS中
var num = 0

module.exports = { num }; // 就是导出 { num: 0 }这个对象而已
```

``` js
// ES6模块中
var num = 0

export { num }; // 导出当前num变量的指针，取值的时候都是跑回当前这个源模块来取
```

``` js
// ES6模块默认导出
var num = 0

export default num ; // 这样导出的东西又变成值了，而不是活指针
```
