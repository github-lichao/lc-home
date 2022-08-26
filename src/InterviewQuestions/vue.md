### vue 的生命周期
>create阶段：vue实例被创建 beforeCreate: 创建前，此时data和methods中的数据都还没有初始化 created： 创建完毕，data中有值，未挂载

>mount阶段： vue实例被挂载到真实DOM节点 beforeMount：可以发起服务端请求，去数据 mounted: 此时可以操作Dom

>update阶段：当vue实例里面的data数据变化时，触发组件的重新渲染 beforeUpdateupdated

>destroy阶段：vue实例被销毁 beforeDestroy：实例被销毁前，此时可以手动销毁一些方法 destroyed

### vue 的通讯方式
父子组件通讯 props $emit parent、children Ref

兄弟之间通讯 event bus

跨组件通讯 $attrs、$listeners Provide、inject

### Vuex 是什么？
https://blog.csdn.net/m0_60265689/article/details/120274308

1.Vuex 是一个专为 Vue.js 应用程序开发的<font color='#ea6f5a'>状态管理模式</font>。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态(state)

2.<font color='#ea6f5a'>Vuex 的状态存储是响应式的。</font>当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

3.<font color='#ea6f5a'>改变 store 中的状态的唯一途径就是显式地提交</font> (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

4.<font color='#ea6f5a'>Vuex 使用单一状态树，用一个对象就包含了全部的应用层级状态。</font>至此它便作为一个“唯一数据源 (SSOT)”而存在。这也意味着，每个应用将仅仅包含一个 store 实例。单一状态树让我们能够直接地定位任一特定的状态片段，在调试的过程中也能轻易地取得整个当前应用状态的快照。——Vuex官方文档

#### 主要包括以下几个模块：

<font color='#ea6f5a'>State</font>：定义了应用状态的数据结构，可以在这里设置默认的初始状态。

<font color='#ea6f5a'>Getter</font>：允许组件从 Store 中获取数据，mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性。

<font color='#ea6f5a'>Mutation</font>：是唯一更改 store 中状态的方法，且必须是同步函数。

<font color='#ea6f5a'>Action</font>：用于提交 mutation，而不是直接变更状态，可以包含任意异步操作。

<font color='#ea6f5a'>Module</font>：允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。
### computed与watch

watch 属性监听 是一个对象，键是需要观察的属性，值是对应回调函数，主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑操作,监听属性的变化，需要在数据变化时执行异步或开销较大的操作时使用

computed 计算属性 属性的结果会被缓存，当computed中的函数所依赖的属性没有发生改变的时候，那么调用当前函数的时候结果会从缓存中读取。除非依赖的响应式属性变化时才会重新计算，主要当做属性来使用 computed中的函数必须用return返回最终的结果 computed更高效，优先使用。data 不改变，computed 不更新。

使用场景computed：当一个属性受多个属性影响的时候使用，例：购物车商品结算功能 watch：当一条数据影响多条数据的时候使用，例：搜索数据

### v-if 和 v-for 的优先级
v-for的优先级是高于v-if的，如果两者同时出现的话，那每次循环都会执行v-if，会很浪费性能，我们正确的做法应该是再v-for的外面新增一个模板标签template，在template上使用v-if

### $nextTick
nextTick是Vue提供的一个全局API,是在下次DOM更新循环结束之后执行延迟回调，在修改数据之后使用$nextTick，则可以在回调中获取更新后的DOM；
2. Vue在更新DOM时是异步执行的。只要侦听到数据变化，Vue将开启1个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个watcher被多次触发，只会被推入到队列中-次。这种在缓冲时去除重复数据对于避免不必要的计算和DOM操作是非常重要的。nextTick方法会在队列中加入一个回调函数，确保该函数在前面的dom操作完成后才调用；

3. 比如，我在干什么的时候就会使用nextTick，传一个回调函数进去，在里面执行dom操作即可；

4. 我也有简单了解nextTick实现，它会在callbacks里面加入我们传入的函数，然后用timerFunc异步方式调用它们，首选的异步方式会是Promise。这让我明白了为什么可以在nextTick中看到dom操作结果。

### v-for中key的作用
key的作用是为了在diff算法执行时更快的找到对应的节点，提高diff速度，更高效的更新虚拟DOM;
Vue在patch过程中判断两个节点是否是相同节点,key是一个必要条件，渲染一组列表时，key往往是唯一标识，所以如果不定义key的话，Vue只能认为比较的两个节点是同一个，哪怕它们实际上不是，这导致了频繁更新元素，使得整个patch过程比较低效，影响性能;
从源码中可以知道，Vue判断两个节点是否相同时主要判断两者的key和元素类型等，因此如果不设置key,它的值就是undefined，则可能永 远认为这是两个相同的节点，只能去做更新操作，这造成了大量的dom更新操作，明显是不可取的。
keep-alive的实现
作用：实现组件缓存

钩子函数： ”activated “组件渲染后调用 ”deactivated“组件销毁后调用

原理：Vue.js内部将DOM节点抽象成了一个个的VNode节点，keep-alive组件的缓存也是基于VNode节点的而不是直接存储DOM结构。它将满足条件（pruneCache与pruneCache）的组件在cache对象中缓存起来，在需要重新渲染的时候再将vnode节点从cache对象中取出并渲染。

配置属性： include 字符串或正则表达式。只有名称匹配的组件会被缓存 exclude 字符串或正则表达式。任何名称匹配的组件都不会被缓存 max 数字、最多可以缓存多少组件实例

### vue-router 怎么传参
1.id传参
```js
//路由配置
{
    path: '/orderDetail/:id',
    name: 'orderdetail',
    component: () => import('../components/orderDetail.vue'),
    meta: { showTabbar: false}
  }
```
this.$router.push({path:`/orderDetail/${this.id}`})
2.query传参

this.$router.push({path:`/orderDetail`,query:{id:this.id}})
3.pramas传参

this.$router.push({name:`orderdetail`,params:{id:this.id}})
插槽
1.普通插槽

2.具名插槽

3.作用域插槽

### vue 的双向绑定原理
当一个Vue实例创建时，Vue会遍历data选项的属性，用 Object.defineProperty 将它们转为 getter/setter并且在内部追踪相关依赖，在属性被访问和修改时通知变化。每个组件实例都有相应的 watcher 程序实例，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的 setter 被调用时，会通知 watcher重新计算，从而致使它关联的组件得以更新。

### Vue2和Vue3区别
属性监听:

defineProperty: 遍历对象，劫持对象的每一个属性; Proxy: 劫持整个对象，并返回一个代理对象;

对数组方法的支持:

defineProperty: push...等不能监听；Proxy: 可以监听；

兼容:

defineProperty(ES5)兼容性比Proxy(ES6)好。

### Vue3
setup函数
2. 声明普通类型 ref

3. 声明复杂类型 reactive

4.watch 的用法

5. v-model 的用法

6. Vue3双向绑定原理

7. Vue3的生命周期

8. Vue3通讯

9. Vue3.2 setup 语法糖等