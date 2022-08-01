### 输入一个URL到页面过程中发生了什么（高频）

- 首先在浏览器中输入URL
- 查找缓存：浏览器先查看浏览器缓存-系统缓存-路由缓存中是否有该地址页面，如果有则显示页面内容。如果没有则进行下一步。
- DNS域名解析：浏览器向DNS服务器发起请求，解析该URL中的域名对应的IP地址。DNS服务器是基于UDP的，因此会用到UDP协议。
- 建立TCP连接：解析出IP地址后，根据IP地址和默认80端口，和服务器建立TCP连接
- 发起HTTP请求：浏览器发起读取文件的HTTP请求，，该请求报文作为TCP三次握手的第三次数据发送给服务器
- 服务器响应请求并返回结果：服务器对浏览器请求做出响应，并把对应的html文件发送给浏览器
- 关闭TCP连接：通过四次挥手释放TCP连接
- 浏览器渲染：客户端（浏览器）解析HTML内容并渲染出来，浏览器接收到数据包后的解析流程为：
  - 构建DOM树：词法分析然后解析成DOM树（dom tree），是由dom元素及属性节点组成，树的根是document对象
  - 构建CSS规则树：生成CSS规则树（CSS Rule Tree）
  - 构建render树：Web浏览器将DOM和CSSOM结合，并构建出渲染树（render tree）
  - 布局（Layout）：计算出每个节点在屏幕中的位置
  - 绘制（Painting）：即遍历render树，并使用UI后端层绘制每个节点。


### 浏览器渲染机制、重绘、重排

网页生成的过程：

- 构建DOM树：词法分析然后解析成DOM树（dom tree），是由dom元素及属性节点组成，树的根是document对象
- 构建CSS规则树：生成CSS规则树（CSS Rule Tree）
- 构建render树：Web浏览器将DOM和CSSOM结合，并构建出渲染树（render tree）
- 布局（Layout）：计算出每个节点在屏幕中的位置
- 绘制（Painting）：即遍历render树，并使用UI后端层绘制每个节点。

>重排：当DOM的变化影响了元素的几何信息(DOM对象的位置和尺寸大小)，浏览器需要重新计算元素的几何属性，将其安放在界面中的正确位置，这个过程叫做重排。

触发条件：添加或者删除可见的DOM元素，元素尺寸改变——边距、填充、边框、宽度和高度

>重绘：当一个元素的外观发生改变，但没有改变布局,重新把元素外观绘制出来的过程，叫做重绘。

触发条件：改变元素的color、background、box-shadow等属性

### cookie，localStorage，sessionStorage，indexDB 的区别
#### cookie（html4，其它的都是html5）
- 一般由服务器生成，可以设置过期时间
- 数据存储大小：4k
- 每次都会携带在 header 中，对于请求性能影响

#### localStorage
- 除非被清理--localstorage.removeItem()，否则一直存在
- 数据存储大小：5M
- 场景：常用于长期登录（+判断用户的登录状态），适合长期保存在本地的数据

#### sessionStorage
- 页面关闭就清理
- 数据存储大小：5M
- 场景：常用于敏感账号一次性登陆，如关闭当前页面再次打开页面就要重新登陆

#### indexDB
- 除非被清理，否则一直存在
- 数据存储大小：理论上无限,然而IndexDB的数据库超过50M的时候浏览器会弹出确认。基本上也相当于没有限制了。
- 查询速度快，但是 indexDB 目前兼容性还不是很好

### 跨域问题处理方法

#### 通过 jsonp 跨域
>只能是 get 请求

JSONP 是通过动态<code>script</code>元素使用的，可以为src属性指定一个跨域 URL，<code>script</code>有能力从其他域加载资源。

```js
<script>
  var script = document.createElement("script");
  script.type = "text/javascript";

  // 传参一个回调函数名给后端，方便后端返回时执行这个在前端定义的回调函数
  script.src =
    "http://www.daxihong.com:8080/login?user=admin&callback=jsonCallback";
  document.head.appendChild(script);

  // 回调执行函数
  function jsonCallback(res) {
    alert(JSON.stringify(res));
  }
</>
// 服务器端返回如下(返回即执行全局函数)
jsonCallback({ status: 0, user: "admin" });
```
#### 跨域资源共享（CORS）
整个 CORS 通信过程，都是浏览器自动完成，不需要用户参与，只要服务器实现了 CORS 接口，就可以跨源通信；

两种方式：简单请求，非简单请求

非简单请求多一个预检请求的过程

JSONP 只支持 GET 请求，CORS 支持所有类型的 HTTP 请求。JSONP 的优势在于支持老式浏览器，以及可以向不支持 CORS 的网站请求数据。

https://www.ruanyifeng.com/blog/2016/04/cors.html

```js
const path = require('path')
const Koa = require('koa')
const koaStatic = require('koa-static')
const bodyParser = require('koa-bodyparser')
const router = require('./router')
const cors = require('koa2-cors')
const app = new Koa()
const port = 9871

...
// 处理cors
app.use(cors({
  origin: function (ctx) {
    return 'http://localhost:9099'
  },
  credentials: true,
  allowMethods: ['GET', 'POST', 'DELETE'],
  allowHeaders: ['t', 'Content-Type']
}))
// 路由
app.use(router.routes()).use(router.allowedMethods())
// 监听端口
...
```
#### nodejs 中间件代理跨域

```js
module.exports = {
  entry: {},
  module: {},
  ...
  devServer: {
      historyApiFallback: true,
      proxy: [{
          context: '/login',
          target: 'http://www.daxihong.com:8080',  // 代理跨域目标接口
          changeOrigin: true,
          secure: false,  // 当代理某些https服务报错时用
          cookieDomainRewrite: 'www.daxihong.com'  // 可以为false，表示不修改
      }],
      noInfo: true
  }
}
```
#### nginx 反向代理中设置
和使用 node 中间件跨域原理相似。前端和后端都不需要写额外的代码来处理， 只需要配置一下 Ngnix

```js
server{
  # 监听9099端口
  listen 9099;
  # 域名是localhost
  server_name localhost;
  #凡是localhost:9099/api这个样子的，都转发到真正的服务端地址http://localhost:9871
  location ^~ /api {
      proxy_pass http://localhost:9871;
  }
}
```

### 常见状态码

301（永久重定向）： 搜索引擎认为旧地址不会再用到，会把地址跟内容都更新成新地址及其内容

302（临时重定向）： 搜索引擎认为跳转只是临时的，保留旧地址，抓取新的内容， 一些旧有的用户代理会错误地将请求方法转换为 GET。

307（临时重定向）： 和302差不多，区别于可以确保请求方法和消息主体不会发生变化。

304：请求资源未修改，可以使用缓存的资源，不用在服务器取

400：客户端请求的语法错误，服务器无法理解

401：请求要求用户的身份认证

403：没权限

404：请求资源不存在

500：服务器内部错误，无法完成请求

502：作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应

503：请求未完成，因服务器过载、宕机或维护等

https://www.runoob.com/http/http-status-codes.html

### Http和Https的区别

HTTP 是不安全的，而 HTTPS 是安全的

HTTP 标准端口是80 ，而 HTTPS 的标准端口是443

HTTP 无法加密，而HTTPS 对传输的数据进行SSL加密

HTTP无需证书，而HTTPS 需要CA机构颁发的SSL证书

### TCP三次握手

第一次握手：客服端发送一个请求连接，服务器端只能确认自己可以接受客服端发送的报文段

第二次握手： 服务端向客服端发送一个链接，确认客服端收到自己发送的报文段

第三次握手： 服务器端确认客服端收到了自己发送的报文段

### GET 和 POST 有什么区别
从缓存角度来讲，GET 请求会被浏览器主动缓存下来，留下历史记录，而 POST 默认不会。

从参数角度来讲，GET 一般放在 URL 中，因此不安全，POST 放在请求体中，因此会更加安全。

从TCP角度来讲，GET 请求会把请求报文一次性发出去，而 POST 会分为两个 TCP 数据包，首先发 header 部分，如果服务器响应 100(continue)， 然后发 body 部分。

### 如何排查内存泄漏问题
>面试官可能会问为什么页面越来越卡顿，直至卡死，怎么定位到产生这种现象的源代码（开发环境）

我这么回答的：

1.先会检查是否是网络请求太多，导致数据返回较慢，可以适当做一些缓存

2.也有可能是某块资源的bundle太大，可以考虑拆分一下

3.然后排查一下js代码，是不是某处有过多循环导致占用主线程时间过长

4.浏览器某帧渲染的东西太多，导致的卡顿

5.在页面渲染过程中，可能有很多重复的重排重绘
#### 后来想到可能是问的内存泄漏
- 闭包使用不当引起内存泄漏
- 全局变量
  - 全局的变量一般是不会被垃圾回收掉的
- 分离的DOM节点
- 控制台的打印
- 遗忘的定时器

>虽然JavaScript的垃圾回收是自动的，但我们有时也是需要考虑要不要手动清除某些变量的内存占用的，例如你明确某个变量在一定条件下再也不需要，但是还会被外部变量引用导致内存无法得到释放时，你可以用null对该变量重新赋值就可以在后续垃圾回收阶段释放该变量的内存了