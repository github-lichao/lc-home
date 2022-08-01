### 什么是TS？

>TS是JS的超集。

* 拓展了JS的语法：主要添加了静态类型和基于类的面向对象编程。

* 不存在浏览器兼容性问题：因为在编译时，它产生的都是JavaScript代码

### ts 和 js 的区别是什么？

- Typescript 是 JavaScript 的超集，可以被编译成 JavaScript 代码。 用 JavaScript 编写的合法代码，在 TypeScript 中依然有效。

- Typescript 是纯面向对象的编程语言，包含类和接口的概念。 程序员可以用它来编写面向对象的服务端或客户端程序，并将它们编译成 JavaScript 代码。 

### TS和JS的关系
TS引入了很多了面向对象程序设计的特征：
```ts
interfaces  接口
classes  类
enumerated types 枚举类型
generics 泛型
modules 模块
```
主要特点：
- TS 是一种面向对象编程语言，而 JS 是一种脚本语言（尽管 JS 是基于对象的）。
- TS 支持可选参数， JS 则不支持该特性。
- TS 支持静态类型，JS 不支持。
- TS 支持接口，JS 不支持接口。

### 为什么要用 ts

- TS 在开发时就能给出编译错误， 而 JS 错误则需要在运行时才能暴露。
- 作为强类型语言，你可以明确知道数据的类型。代码可读性极强，几乎每个人都能理解。
- TS 非常流行，被很多业界大佬使用。像 Asana、Circle CI 和 Slack 这些公司都在用 TS。 
- TypeScript支持面向对象的编程特性，比如类、接口、继承、泛型等等。
- TypeScript在编译时提供了错误检查功能。它将编译代码，如果发现任何错误，它将在运行脚本之前突出显示这些错误。
- TypeScript支持所有JavaScript库，因为它是JavaScript的超集。
- TypeScript支持静态类型、强类型、模块、可选参数等。

### TypeScript 和 JavaScript 哪个更好

- 由于 TS 的先天优势，TS 越来越受欢迎。但是TS 最终不可能取代 JS，因为 JS 是 TS 的核心。
- 选择 TypeScript 还是 JavaScript 要由开发者自己去做决定。如果你喜欢类型安全的语言，那么推荐你选择 TS。 如果你已经用 JS 好久了，你可以选择走出舒适区学习 TS，也可以选择坚持自己的强项，继续使用 JS。

### 什么是泛型

- 泛型是指在定义函数、接口或类的时候，不预先指定具体的类型，使用时再去指定类型的一种特性。
- 可以把泛型理解为代表类型的参数 

```ts
function createArray1(length: any, value: any): Array<any> {
    let result: any = [];
    for (let i = 0; i < length; i++) {
        result[i] = value;
    }
    return result;
}
 
let result = createArray1(3, 'x');
console.log(result);
 
// 最傻的写法：每种类型都得定义一种函数
function createArray2(length: number, value: string): Array<string> {
    let result: Array<string> = [];
    for (let i = 0; i < length; i++) {
        result[i] = value;
    }
    return result;
}
 
function createArray3(length: number, value: number): Array<number> {
    let result: Array<number> = [];
    for (let i = 0; i < length; i++) {
        result[i] = value;
    }
    return result;
}
// 或者使用函数重载，写法有点麻烦
function createArray4(length: number, value: number): Array<number>
function createArray4(length: number, value: string): Array<string>
function createArray4(length: number, value: any): Array<any> {
    let result: Array<number> = [];
    for (let i = 0; i < length; i++) {
        result[i] = value;
    }
    return result;
}
createArray4(6, '666');
//使用泛型
// 有关联的地方都改成 <T>
function createArray<T>(length: number, value: T): Array<T> {
    let result: T[] = [];
    for (let i = 0; i < length; i++) {
        result[i] = value;
    }
    return result;
}
// 使用的时候再指定类型
let result = createArray<string>(3, 'x');
// 也可以不指定类型，TS 会自动类型推导
let result2 = createArray(3, 'x');
console.log(result);
```

### 什么是函数类型接口

```ts
对方法传入的参数和返回值进行约束
// 注意区别
 
// 普通的接口
interface discount1{
  getNum : (price:number) => number
}
 
// 函数类型接口
interface discount2{
  // 注意:
  // “:” 前面的是函数的签名，用来约束函数的参数
  // ":" 后面的用来约束函数的返回值
  (price:number):number
}
let cost:discount2 = function(price:number):number{
   return price * .8;
}
 
// 也可以使用类型别名
type Add = (x: number, y: number) => number
let add: Add = (a: number, b: number) => a + b
```

### 什么是 类 类型接口
>如果接口用于一个类的话，那么接口会表示“行为的抽象”。
>对类的约束，让类去实现接口，类可以实现多个接口。
>接口只能约束类的公有成员（实例属性/方法)，无法约束私有成员，构造函数，静态属性/方法。
```ts
// 接口可以在面向对象编程中表示为行为的抽象
interface Speakable {
    name: string;
  
     // ":" 前面的是函数签名，用来约束函数的参数
    // ":" 后面的用来约束函数的返回值
    speak(words: string): void
}
 
interface Speakable2 {
    age: number;
}
 
class Dog implements Speakable, Speakable2 {
    name!: string;
    age = 18;
 
    speak(words: string) {
        console.log(words);
    }
}
 
let dog = new Dog();
dog.speak('汪汪汪');
```

### 什么是混合类型接口

>一个对象可以同时作为函数和对象使用
```ts
interface FnType {
    (getName:string):string;
}
 
interface MixedType extends FnType{
    name:string;
    age:number;
}
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}
 
function getCounter(): Counter {
    let counter = <Counter>function (start: number) { };
    counter.interval = 123;
    counter.reset = function () { };
    return counter;
}
 
let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```

### never 和 void 的区别

- void 表示没有任何类型（可以被赋值为 null 和 undefined）。
- never 表示一个不包含值的类型，即表示永远不存在的值。
拥有 void 返回值类型的函数能正常运行。拥有 never 返回值类型的函数无法正常返回，无法终止，或会抛出异常。 


### type 和 interface 的区别？

相同点：

- 都可以描述 '对象' 或者 '函数'
- 都允许拓展(extends)

不同点：

- type 可以声明基本类型，联合类型，元组
- type 可以使用 typeof 获取实例的类型进行赋值
- 多个相同的 interface 声明可以自动合并 使用 interface 描述‘数据结构’，使用 type 描述‘类型关系’

### keyof 和 typeof 关键字的作用

>keyof 索引类型查询操作符 获取索引类型的属性名，构成联合类型。

```ts
interface Person { 
    name: string;
    age: number;
}
type K1 = keyof Person; // "name" | "age"
type K2 = keyof Person[]; // "length" | "toString" | "pop" | "push" | "concat" | "join"
```

>typeof 获取一个变量或对象的类型。

js中判断某个数据的类型
```js
let a = 8
console.log(typeof a)// 'number'
```

ts中的typeof是 根据已有的值 来获取值的类型  来简化代码的书写
```ts
interface Person { 
    name: string;
    age: number;
}
const person: Person = [name: 'LC', age: 25]
type TPrson = typeof person;
```

### 数组定义的两种方式
```ts
type Foo = Array<string>;
interface Bar {
  baz: Array<{ name: string; age: number }>;
}

type Foo = string[];
interface Bar {
  baz: { name: string; age: number }[];
}
```

### declare，declare global 是什么
>declare 是用来定义全局变量、全局函数、全局命名空间、js modules、class 等 declare global 为全局对象 window 增加新的属性

```ts
declare global {
  interface Window {
    csrf: string;
  }
}
```

### 如何联合枚举类型的 Key

```ts
enum str {
  A,
  B,
  C,
}
type strUnion = keyof typeof str; // 'A' | 'B' | 'C'
```

### 如何将 unknown 类型指定为一个更具体的类型
- 对 unknown 使用类型断言，虽然能通过类型编译，但是运行时可能会报错，不太推荐
- 使用typeof进行类型收缩

### TypeScript中any,never,unknown和viod有什么区别？

>unknown类型和any类型类似。与any类型不同的是unknown类型可以接受任意类型赋值，但是unknown类型赋值给其他类型前，必须被断言

>never，never表示永远不存在的类型。比如一个函数总是抛出错误，而没有返回值。或者一个函数内部有死循环，永远不会有返回值。函数的返回值就是never类型。

>void, 没有显示的返回值的函数返回值为void类型。如果一个变量为void类型，只能赋予undefined或者null。

### 使用 Union Types 时有哪些注意事项

>属性或方法访问: 当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，我们只能访问此联合类型的所有类型里共有的属性或方法。

```ts
function getLength(something: string | number): number {
  return something.length;
}
// index.ts(2,22): error TS2339: Property 'length' does not exist on type >'string | number'.
//   Property 'length' does not exist on type 'number'.

function getString(something: string | number): string {
  return something.toString();
}
// 公共方法和属性可以访问
```

### 如何基于一个已有类型, 扩展出一个大部分内容相似, 但是有部分区别的类型
- 首先可以通过Pick和Omit, 比如Partial, Required.
```ts
interface Test {
    name: string;
    sex: number;
    height: string;
}

type Sex = Pick<Test, 'sex'>;

const a: Sex = { sex: 1 };

type WithoutSex = Omit<Test, 'sex'>;

const b: WithoutSex = { name: '1111', height: 'sss' };

```

- 再者可以通过泛型

### 什么是泛型, 泛型的具体使用

>泛型是指在定义函数、接口或类的时候，不预先指定具体的类型，使用时再去指定类型的一种特性。

可以把泛型理解为代表类型的参数
```ts
interface Test<T = any> {
    userId: T;
}

type TestA = Test<string>;
type TestB = Test<number>;

const a: TestA = {
    userId: '111',
};

const b: TestB = {
    userId: 2222,
};

```

### TypeScript中?. , ?? , !： , _ , ** 等符号的含义？
- ?. 可选链
- ?? 类似与短路或，??避免了一些意外情况，0，NaN以及"",false被视为false值。只有undefind,null被视为false值。
- !. 在变量名后添加!，可以断言排除undefined和null类型
- _ 声明该函数将被传递一个参数，但您并不关心它
- !: 待会分配这个变量，ts不要担心
- ** 求幂