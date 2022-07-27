### hash 模式


a 标签锚点大家应该不陌生，而浏览器地址上 # 后面的变化，是可以被监听的，浏览器为我们提供了原生监听事件 hashchange ，它可以监听到如下的变化：

- 点击 a 标签，改变了浏览器地址
- 浏览器的前进后退行为
- 通过 window.location 方法，改变浏览器地址


### history 模式

这种模式要玩好，还需要后台配置支持


history 模式会比 hash 模式稍麻烦一些，因为 history 模式依赖的是原生事件 popstate ，下面是来自 MDN 的解释

调用`history.pushState()`或者 `history.replaceState()`不会触发`popState`事件。只有在浏览器做出动作时，才会触发该事件，如用户点击浏览器的回退按钮，或者在js中调用`history.back()`，`histroy.forward()`方法

小知识：`pushState` 和 `replaceState` 都是 HTML5 的新 API，他们的作用很强大，可以做到改变浏览器地址却不刷新页面。这是实现改变地址栏却不刷新页面的重要方法。



这里注意，不能在浏览器直接打开静态文件，需要通过 web 服务，启动端口去浏览网址。

### 参考

https://juejin.cn/post/6917523941435113486