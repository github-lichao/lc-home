对象相关的方法

### 1. in 运算符

```js
var obj = { p: 1 };

"p" in obj; // true

"toString" in obj; // true
```

in 运算符的一个问题是，它不能识别哪些属性是对象自身的，哪些属性是继承的。

通过 hasOwnProperty 解决 -- hasOwnProperty() 方法会返回一个布尔值，表示对象自身属性中是否具有指定的属性

```js
const object1 = {};
object1.property1 = 42;

console.log(object1.hasOwnProperty("property1"));
// expected output: true

console.log(object1.hasOwnProperty("toString"));
// expected output: false

console.log(object1.hasOwnProperty("hasOwnProperty"));
// expected output: false
```

下面是一个数据格式转换的例子

```js
let object = {
  react: {
    number1: 18,
    number2: 19,
    children: {
      test: {
        number1: 20,
        number2: 21,
        default: 22
      },
      mocha: {
        number1: 30,
        number2: 31,
        children: {
          mocha1: {
            number1: 401,
            number2: 411,
            default: 421
          },
          mocha2: {
            number1: 402,
            number2: 412,
            default: 422
          },
          mocha3: {
            number1: 403,
            number2: 413,
            default: 423
          }
        }
      }
    }
  },
  vue: {
    number1: 18,
    number2: 20,
    default: 12
  }
}
const objectLoop = (object) => {
  const data = {};
  for (const key in object) {
    if (Object.prototype.hasOwnProperty.call(object, key)) {
      const props = object[key];
      if (props && props.children) {
        data[key] = objectLoop(object[key].children);
      } else {
        data[key] = props.default;
      }
    }
  }
  return data;
};

objectLoop(object)

{
  react: {
    mocha: {
      mocha1: 421,
      mocha2: 422,
      mocha3: 422
    },
    test: 22
  },
  vue: 12
}
```

### 2. for ... in

不推荐使用 for...in 遍历数组

```js
// 1. 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。

// 2. 它不仅遍历对象自身的属性，还遍历继承的属性。

var obj = { a: 1, b: 2, c: 3 };

for (var i in obj) {
  console.log("键名：", i);
  console.log("键值：", obj[i]);
}
// 键名： a
// 键值： 1
// 键名： b
// 键值： 2
// 键名： c
// 键值： 3
```

如果继承的属性是可遍历的，那么就会被 for...in 循环遍历到

需要通过 hasOwnProperty 过滤一下

```js
var person = { name: "老张" };

for (var key in person) {
  if (person.hasOwnProperty(key)) {
    console.log(key);
  }
}
// name
```

### 3. with 语句

建议不要使用 with 语句

### 4. Object.create()

构造函数作为模板，可以生成实例对象。但是，有时拿不到构造函数，只能拿到一个现有的对象。

```js
var person1 = {
  name: "张三",
  age: 38,
  greeting: function () {
    console.log("Hi! I'm " + this.name + ".");
  },
};

var person2 = Object.create(person1);

person2.name; // 张三
person2.greeting(); // Hi! I'm 张三.
```
