css
### css3新特性
>选择器: p:nth-child(n){color: '#FFF'}

>新增伪元素: ::before 和 ::after

>盒子模型属性：圆角-->border-radius、阴影-->box-shadow、边框效果-->border-image

>背景：背景效果-->background-size、background-origin、background-clip

>文本效果：文字阴影-->text-shadow、自动换行-->word-wrap

>颜色：新增 RGBA(颜色透明)-->color: rgba(255, 0, 0, 0.75);

>渐变：线性渐变、径向渐变  background:linear-gradient(red, green, blue);

>字体：@font-face{font-family: BorderWeb;}

>2D/3D转换：动画-->transform、旋转-->transform-origin

>过渡与动画：transition、@keyframes、animation

>多列布局: column-count: 5;

>媒体查询: @media (max-width: 480px) {.box: {column-count: 1;}}

### css选择器优先级和权重
下面的优先级逐级增加：
>通用选择器（*）< 元素(类型)选择器 < 类选择器 < 属性选择器 < 伪类 < ID 选择器 < 内联样式

元素选择器：
```css
html {color:black;}
h1 {color:blue;}
h2 {color:silver;}
```
属性选择器：

```css
a[href] {color:red;}
<a href="http://w3school.com.cn">W3School</a>
```
#### css优先级规则：
>css选择规则的权值不同时，权值高的优先；css选择规则的权值相同时，后定义的规则优先；css属性后面加 !important 时，无条件绝对优先；

### 介绍下 BFC 及其应用

>所谓 BFC，指的是一个独立的布局环境，BFC 内部的元素布局与外部互不影响。

>触发 BFC 的方式有很多，常见的有：

>设置浮动
overflow 设置为 auto、scroll、hidden
positon 设置为 absolute、fixed
常见的 BFC 应用有：

>解决浮动元素令父元素高度坍塌的问题
解决非浮动元素被浮动元素覆盖问题
解决外边距垂直方向重合的问题

### px 和 em 的区别

>px全称pixel像素，是相对于屏幕分辨率而言的，它是一个绝对单位，但同时具有一定的相对性。因为在同一个设备上每个像素代表的物理长度是固定不变的，这点表现的是绝对性。但是在不同的设备之间每个设备像素所代表的物理长度是可以变化的，这点表现的是相对性

>em是一个相对长度单位，具体的大小需要相对于父元素计算，比如父元素的字体大小为80px，那么子元素1em就表示大小和父元素一样为80px，0.5em就表示字体大小是父元素的一半为40px

### flex 布局如何使用？

>flex 是 Flexible Box 的缩写，意为"弹性布局"。指定容器display: flex即可。

>容器有以下属性：flex-direction，flex-wrap，flex-flow，justify-content，align-items，align-content。

>flex-direction属性决定主轴的方向；

>flex-wrap属性定义，如果一条轴线排不下，如何换行；

>flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap；

>justify-content属性定义了项目在主轴上的对齐方式。

>align-items属性定义项目在交叉轴上如何对齐。

>align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

>项目（子元素）也有一些属性：order，flex-grow，flex-shrink，flex-basis，flex，align-self。

>order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

>flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

>flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

>flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。

>flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

>align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性。默认值为 auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

### 如何用 css 或 js 实现多行文本溢出省略效果，考虑兼容性

#### CSS 实现方式

单行：
```css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```
多行：
```css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3; //行数
overflow: hidden;
```
兼容：
```css
p{position: relative; line-height: 20px; max-height: 40px;overflow: hidden;}
p::after{content: "..."; position: absolute; bottom: 0; right: 0; padding-left: 40px;
background: -webkit-linear-gradient(left, transparent, #fff 55%);
background: -o-linear-gradient(right, transparent, #fff 55%);
background: -moz-linear-gradient(right, transparent, #fff 55%);
background: linear-gradient(to right, transparent, #fff 55%);
}
```

#### js实现方式：

>使用split + 正则表达式将单词与单个文字切割出来存入words,加上 '...',判断scrollHeight与clientHeight，超出的话就从words中pop一个出来

###  CSS3 中 transition 和 animation 的属性分别有哪些

```css
transition 过渡动画：

transition-property：指定过渡的 CSS 属性
transition-duration：指定过渡所需的完成时间
transition-timing-function：指定过渡函数
transition-delay：指定过渡的延迟时间

animation 关键帧动画：

animation-name：指定要绑定到选择器的关键帧的名称
animation-duration：动画指定需要多少秒或毫秒完成
animation-timing-function：设置动画将如何完成一个周期
animation-delay：设置动画在启动前的延迟间隔
animation-iteration-count：定义动画的播放次数
animation-direction：指定是否应该轮流反向播放动画
animation-fill-mode：规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式
animation-play-state：指定动画是否正在运行或已暂停
```

### 分析比较 opacity: 0、visibility: hidden、display: none 优劣和适用场景

>display: none (不占空间，不能点击)（场景，显示出原来这里不存在的结构）

>visibility: hidden（占据空间，不能点击）（场景：显示不会导致页面结构发生变动，不会撑开）

>opacity: 0（占据空间，可以点击）（场景：可以跟transition搭配）

### 清除浮动的方法

>clear 清除浮动（添加空div法）在浮动元素下方添加空div，并给该元素写css样式：{clear:both;height:0;overflow:hidden;}

>给浮动元素父级设置高度

>父级同时浮动（需要给父级同级元素添加浮动）

>父级设置成inline-block，其margin: 0 auto居中方式失效

>给父级添加overflow:hidden 清除浮动方法

>万能清除法 after 伪类清浮动（现在主流方法，推荐使用）

### 说说两种盒模型以及区别

>盒模型也称为框模型，就是从盒子顶部俯视所得的一张平面图，用于描述元素所占用的空间。它有两种盒模型，W3C盒模型和IE盒模型（IE6以下，不包括IE6以及怪异模式下的IE5.5+）

>理论上两者的主要区别是二者的盒子宽高是否包括元素的边框和内边距。当用CSS给给某个元素定义高或宽时，IE盒模型中内容的宽或高将会包含内边距和边框，而W3C盒模型并不会。

### 如何触发重排和重绘？

>任何改变用来构建渲染树的信息都会导致一次重排或重绘：

>添加、删除、更新DOM节点
通过display: none隐藏一个DOM节点-触发重排和重绘
通过visibility: hidden隐藏一个DOM节点-只触发重绘，因为没有几何变化
移动或者给页面中的DOM节点添加动画
添加一个样式表，调整样式属性
用户行为，例如调整窗口大小，改变字号，或者滚动。

### 重绘与重排的区别？

>重排:  部分渲染树（或者整个渲染树）需要重新分析并且节点尺寸需要重新计算，表现为重新生成布局，重新排列元素

>重绘:  由于节点的几何属性发生改变或者由于样式发生改变，例如改变元素背景色时，屏幕上的部分内容需要更新，表现为某些元素的外观被改变

>单单改变元素的外观，肯定不会引起网页重新生成布局，但当浏览器完成重排之后，将会重新绘制受到此次重排影响的部分

>重排和重绘代价是高昂的，它们会破坏用户体验，并且让UI展示非常迟缓，而相比之下重排的性能影响更大，在两者无法避免的情况下，一般我们宁可选择代价更小的重绘。

>『重绘』不一定会出现『重排』，『重排』必然会出现『重绘』。

### 如何优化图片

>对于很多装饰类图片，尽量不用图片，因为这类修饰图片完全可以用 CSS 去代替。

>对于移动端来说，屏幕宽度就那么点，完全没有必要去加载原图浪费带宽。一般图片都用 CDN 加载，可以计算出适配屏幕的宽度，然后去请求相应裁剪好的图片。

>小图使用 base64 格式

>将多个图标文件整合到一张图片中（雪碧图）

>选择正确的图片格式：

>对于能够显示 WebP 格式的浏览器尽量使用 WebP 格式。因为 WebP 格式具有更好的图像数据压缩算法，能带来更小的图片体积，而且拥有肉眼识别无差异的图像质量，缺点就是兼容性并不好
>小图使用 PNG，其实对于大部分图标这类图片，完全可以使用 SVG 代替
>照片使用 JPEG

### 如何用 CSS 实现一个三角形

>可以利用 border 属性

>利用盒模型的 border 属性上下左右边框交界处会呈现出平滑的斜线这个特点，通过设置不同的上下左右边框宽度或者颜色即可得到三角形或者梯形。

>如果想实现其中的任一个三角形，把其他方向上的 border-color 都设置成透明即可。

示例代码如下：
```js
<div></div>
```
```css
div{
width: 0;
height: 0;
border: 10px solid red;
border-top-color: transparent;
border-left-color: transparent;
border-right-color: transparent;
}
```