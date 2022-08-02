### oader 和 plugin 的区别
Loader 本质就是一个函数，在该函数中对接收到的内容进行转换，返回转换后的结果。 因为 Webpack 只认识 JavaScript，所以 Loader 就成了翻译官，对其他类型的资源进行转译的预处理工作。

Plugin 就是插件，基于事件流框架 Tapable，插件可以扩展 Webpack 的功能，在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。

Loader 在 module.rules 中配置，作为模块的解析规则，类型为数组。每一项都是一个 Object，内部包含了 test(类型文件)、loader、options (参数)等属性。

Plugin 在 plugins 中单独配置，类型为数组，每一项是一个 Plugin 的实例，参数都通过构造函数传入

### 常用Loader（高频）
raw-loader：加载文件原始内容（utf-8）

file-loader：把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件 (处理图片和字体)

source-map-loader：加载额外的 Source Map 文件，以方便断点调试

svg-inline-loader：将压缩后的 SVG 内容注入代码中

image-loader：加载并且压缩图片文件

json-loader 加载 JSON 文件（默认包含）

babel-loader：把 ES6 转换成 ES5

ts-loader: 将 TypeScript 转换成 JavaScript

awesome-typescript-loader：将 TypeScript 转换成 JavaScript，性能优于 ts-loader

sass-loader：将SCSS/SASS代码转换成CSS

css-loader：加载 CSS，支持模块化、压缩、文件导入等特性

style-loader：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS

postcss-loader：扩展 CSS 语法，使用下一代 CSS，可以配合 autoprefixer 插件自动补齐 CSS3 前缀

vue-loader：加载 Vue.js 单文件组件

### 常用的Plugin
define-plugin：定义环境变量 (Webpack4 之后指定 mode 会自动配置)

ignore-plugin：忽略部分文件

html-webpack-plugin：简化 HTML 文件创建 (依赖于 html-loader)

web-webpack-plugin：可方便地为单页应用输出 HTML，比 html-webpack-plugin 好用

uglifyjs-webpack-plugin：不支持 ES6 压缩 (Webpack4 以前)

terser-webpack-plugin: 支持压缩 ES6 (Webpack4)

webpack-parallel-uglify-plugin: 多进程执行代码压缩，提升构建速度

mini-css-extract-plugin: 分离样式文件，CSS 提取为独立文件，支持按需加载 (替代extract-text-webpack-plugin)

serviceworker-webpack-plugin：为网页应用增加离线缓存功能

clean-webpack-plugin: 目录清理

### webpack打包优化的方法

#### 为什么要优化打包？
- 项目越做越大，依赖包越来越多，打包文件太大
- 单页面应用首页白屏时间长，用户体验差
#### 我们的目的
- 减小打包后的文件大小
- 首页按需引入文件
- 优化 webpack 打包时间

1、 按需加载

```js
// 引入全部组件
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(ElementUI)

// 按需引入组件
import { Button } from 'element-ui'
Vue.component(Button.name, Button)
```

2、优化 loader 配置
- 优化正则匹配
- 通过 cacheDirectory 选项开启缓存
- 通过 include、exclude 来减少被处理的文件。

3、优化文件路径——省下搜索文件的时间
- extension 配置之后可以不用在 require 或是 import 的时候加文件扩展名,会依次尝试添加扩展名进行匹配。
- mainFiles 配置后不用加入文件名，会依次尝试添加的文件名进行匹配
- alias 通过配置别名可以加快 webpack 查找模块的速度。

4、生产环境关闭 sourceMap
- sourceMap 本质上是一种映射关系，打包出来的 js 文件中的代码可以映射到代码文件的具体位置,这种映射关系会帮助我们直接找到在源代码中的错误。
- 打包速度减慢，生产文件变大，所以开发环境使用 sourceMap，生产环境则关闭。

5、代码压缩
- UglifyJS: vue-cli 默认使用的压缩代码方式，它使用的是单线程压缩代码，打包时间较慢
- ParallelUglifyPlugin: 开启多个子进程，把对多个文件压缩的工作分别给多个子进程去完成

6、提取公共代码
- 相同资源重复被加载，浪费用户流量，增加服务器成本。
- 每个页面需要加载的资源太大，导致网页首屏加载缓慢，影响用户体验。

7、CDN 优化
- 随着项目越做越大，依赖的第三方 npm 包越来越多，构建之后的文件也会越来越大。
- 再加上又是单页应用，这就会导致在网速较慢或者服务器带宽有限的情况出现长时间的白屏。

8、使用 HappyPack 多进程解析和处理文件
- 由于运行在 Node.js 之上的 Webpack 是单线程模型的，所以 Webpack 需要处理的事情需要一件一件的做，不能多件事一起做。
- HappyPack 就能让 Webpack 把任务分解给多个子进程去并发的执行，子进程处理完后再把结果发送给主进程。
- HappyPack 对 file-loader、url-loader 支持的不友好，所以不建议对该 loader 使用。


使用方法如下：

HappyPack 插件安装： npm i -D happypack
webpack.base.conf.js 文件对 module.rules 进行配置
```js
//webpack.base.conf.js
module: {
  rules: [
    {
      test: /\.js$/,
      use: ['happypack/loader?id=babel'],
      include: [resolve('src'), resolve('test')],
      exclude: path.resolve(__dirname, 'node_modules')
    },
    {
      test: /\.vue$/,
      use: ['happypack/loader?id=vue']
    }
  ]
}
```
