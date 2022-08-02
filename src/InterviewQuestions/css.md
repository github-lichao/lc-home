### License盒模型（高频）

>盒模型都是由四个部分组成的，分别是margin、border、padding和content。

- 标准盒模型的width和height属性的范围只包含了content，
- IE盒模型的width和height属性的范围包含了border、padding和content。

### 隐藏元素的方法有哪些
1.使用display: none; 隐藏dom；

2.使用visibility: hidden; 隐藏dom；

3.使用z-index: -888; 把元素的层级调为负数，然后其他元素覆盖即可；

4.使用opacity: 0; 把元素的透明度调为0，也可以达到隐藏；

5.使用固定定位position: absolute; 把元素定位到看不见的区域；

6.使用transform: scale(0, 0); 把元素缩放为0，也可以实现元素隐藏。

### 盒子水平垂直居中方法（高频）
1.利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过translate来调整元素的中心点到页面的中心

2.利用绝对定位，设置四个方向的值都为0，并将margin设置为auto，由于宽高固定，因此对应方向实现平分，可以实现水平和垂直方向上的居中。该方法适用于盒子有宽高的情况

3.利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过margin负值来调整元素的中心点到页面的中心。该方法适用于盒子宽高已知的情况

4.使用flex布局，通过align-items:center和justify-content:center设置容器的垂直和水平方向上为居中对齐，然后它的子元素也可以实现垂直和水平的居中

### CSS样式优先级
- !important
- 内联样式（1000）
- ID选择器（0100）
- 类选择器（0010）
- 元素选择器（0001）
- 通配符选择器（0000）

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

### flex:1到底是什么

>flex实际上是flex-grow、flex-shrink和flex-basis三个属性的缩写。

```css
flex:1 ==> flex:1 1 auto
```
#### flex-grow
flex-grow属性指定了flex容器中剩余空间的多少应该被分配给项目。flex-grow设置的值为扩张因子，默认为0，剩余空间将会按照这个权重分别分配给子元素项目。

例如：父元素的宽度为500px，其中有两个元素A和B，A的宽度为100px，B的宽度为150px。假如不设置flex-grow属性，那么父元素的剩余宽度为500-(100+150)=250px。

```html
<div id="container">
        <div id="A">100px</div>
        <div id="B">150px</div>
</div>
```
```css
		#container {
            display: flex;
            width: 500px;
            margin: 20px;
            border: 1px solid#000;
        }

        #A {
            width: 100px;
            height: 200px;
            background-color: aqua;
        }

        #B {
            width: 150px;
            height: 200px;
            background-color: chocolate;
        }
```

#### flex-shrink
flex-shrink属性指定了flex元素的收缩规则。flex元素仅在默认宽度之和大于容器的时候才会发生收缩。默认属性值为1，所以在空间不够的时候，子项目将会自动缩小。

#### flex-basis
flex-basis属性指定了flex元素在主轴方向上的初始大小。如果不使用box-sizing改变盒模型的话，那么这个属性就决定了flex元素的内容的尺寸。如果设置了flex-basis值，那么元素占用的空间为flex-basis值；如果没有设置或者设置为auto，那么元素占据的空间为元素的width/height值。

#### 详解请看： 
https://blog.csdn.net/weixin_43554584/article/details/113839778?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-2-113839778-blog-124444419.pc_relevant_sortByStrongTime&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-2-113839778-blog-124444419.pc_relevant_sortByStrongTime&utm_relevant_index=5
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

### css实现左侧固定右侧自适应
基本html和css
```html
<div class="con conX"> //conX代表：con1 con2 con3
    <div class="con_l conX_l">左侧固定width 200px</div>  //conX_l代表：con1_l con2_l con3_l
    <div class="con_r conX_r">右侧自适应</div>  //conX_r代表：con1_r con2_r con3_r
</div>
```
```css
.con{
    height:120px;
    background:#ccc;
    margin-bottom:20px;
}
.con_l{
    width:200px;
    height:80%;
    background:palegreen;
}
.con_r{
    height:100%;
    background:peru;
}
```

1、左侧元素浮动，右侧元素添加overflow:hidden，触发bfc，bfc的区域不会与float的元素重叠
```css
.con1_l{
    float:left;
}
.con1_r{
    overflow: hidden;
}
```
2、左侧元素浮动，右侧元素添加margin-left，值为左侧元素的宽度
```css
.con2_l{
    float:left;
}
.con2_r{
    margin-left:200px;
}
```
3、左侧元素浮动，右侧元素添加子元素，父元素添加padding-left
```html
<div class="con">
    <div class="con_l con3_l">左侧固定width 200px</div>
    <div class="con_r con3_r">
        <div class="con3_r_con">右侧自适应</div>
    </div>
</div>
```
```css
.con3_l{
    float:left;
}
.con3_r{
    padding-left:200px;
}
.con3_r_con{
    height:100%;
    background:palevioletred;
}
```
4、左侧元素position定位，0px 0px。右侧元素margin-left:200px;
```css
.con4{
    position:relative;
}
.con4_l{
    position:absolute;
}
.con4_r{
    margin-left:200px;
}
```
5、使用width:calc（100%-200px)
```css
.con5_l{
    float:left;
}
.con5_r{
    width:calc(100% - 200px);
    float:left;
}
```
6、使用table-cell表格布局,宽度会被内容撑开。如果宽度不够的话，不会充满浏览器的宽
```css
.con6{
    display:table;
}
.con6_l,.con6_r{
    display:table-cell;
}
```
7、使用flex布局
```css
.con7{
    display:flex;
}
.con7_r{
    flex-grow:1;
}
```