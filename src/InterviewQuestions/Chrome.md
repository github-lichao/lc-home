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