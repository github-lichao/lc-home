### React中key的作用
Keys是React用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识。

### 你对虚拟dom和diff算法的理解
虚拟DOM本质上是JavaScript对象,是对真实DOM的抽象表现。 状态变更时，记录新树和旧树的差异 最后把差异更新到真正的dom

### React的生命周期
```js
安装
当组件的实例被创建并插入到 DOM 中时，这些方法按以下顺序调用：

constructor()
static getDerivedStateFromProps()
render()
componentDidMount()

更新中
更新可能由道具或状态的更改引起。当重新渲染组件时，这些方法按以下顺序调用：

static getDerivedStateFromProps()
shouldComponentUpdate()
render()
getSnapshotBeforeUpdate()
componentDidUpdate()

卸载
当组件从 DOM 中移除时调用此方法：

componentWillUnmount()
```

### React组件之间通信方式
父子组件,父->子直接用Props,子->父用callback回调
非父子组件,用发布订阅模式的Event模块
项目复杂的话用Redux等全局状态管理管库
Context Api context 会使组件复用性变差

### React组件的通讯
https://zhuanlan.zhihu.com/p/528530806

### setState是同步还是异步的
#### 1.在正常的react的事件流里（如onClick等）

>setState和useState是异步执行的（不会立即更新state的结果）

多次执行setState和useState，只会调用一次重新渲染render不同的是，

setState会进行state的合并，而useState则不会

#### 2.在setTimeout，Promise.then等异步事件中

>setState和useState是同步执行的（立即更新state的结果）

多次执行setState和useState，每一次的执行setState和useState，都会调用一次render

### 常用的hooks有哪些
>useState、useEffect 、useContext、 useCallback、useMemo

### React元素与组件的区别？
组件是由元素构成的。元素数据结构是普通对象，而组件数据结构是类或纯函数。

### 说一下 react-fiber
>react fiber：在数据更新时，react生成了一棵更大的虚拟dom树，给第二步的diff带来了很大压力——我们想找到真正变化的部分，这需要花费更长的时间。js占据主线程去做比较，渲染线程便无法做其他工作，用户的交互得不到响应，所以便出现了react fiber。

>react fiber没法让比较的时间缩短，但它使得diff的过程被分成一小段一小段的，因为它有了“保存工作进度”的能力。js会比较一部分虚拟dom，然后让渡主线程，给浏览器去做其他工作，然后继续比较，依次往复，等到最后比较完成，一次性更新到视图上。