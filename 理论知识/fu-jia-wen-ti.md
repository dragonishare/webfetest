#附加问题
> 涉及http,性能优化等

### 1.http响应中content-type包含哪些内容
请求中的消息主体是用何种方式编码
* application/x-www-form-urlencoded
> 这是最常见的 POST 提交数据的方式 按照 key1=val1&key2=val2 的方式进行编码

* application/json
> 告诉服务端消息主体是序列化后的 JSON 字符串

### 2.浏览器缓存有哪些，通常缓存有哪几种方式
* 强缓存 强缓存如果命中，浏览器直接从自己的缓存中读取资源，不会发请求到服务器。

* 协商缓存 当强缓存没有命中的时候，浏览器一定会发送一个请求到服务器，通过服务器端依据资源的另外一些http header验证这个资源是否命中协商缓存，如果协商缓存命中，服务器会将这个请求返回（304），若未命中请求，则将资源返回客户端，并更新本地缓存数据（200）。

* HTTP头信息控制缓存

* Expires（强缓存）+过期时间 Expires是HTTP1.0提出的一个表示资源过期时间的header，它描述的是一个绝对时间

* Cache-control（强缓存） 描述的是一个相对时间，在进行缓存命中的时候，都是利用客户端时间进行判断 管理更有效，安全一些 Cache-Control: max-age=3600

* Last-Modified/If-Modified-Since（协商缓存） 标示这个响应资源的最后修改时间。Last-Modified是服务器相应给客户端的，If-Modified-Sinces是客户端发给服务器，服务器判断这个缓存时间是否是最新的，是的话拿缓存。

* Etag/If-None-Match（协商缓存） etag和last-modified类似，他是发送一个字符串来标识版本。

### 3. get和post有什么不同
get是从服务器上获取数据，post是向服务器传送数据
get请求可以将查询字符串参数追加到url的末尾; post请求应该把数据作为请求的主体提交.
get请求数据有大小限制；post没有
post比get安全性更高

### 4. cookie和session有什么联系和区别

cookie数据存放在客户的浏览器上，session数据放在服务器上。

session比cookie更安全

单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

一般用cookie来存储sessionid

### 5.跨域通信有哪些方案，各有什么不同

JSONP：由于同源策略的限制，XmlHttpRequest只允许请求当前源，script标签没有同源限制

通过动态`<script>`元素使用，使用时为src指定一个跨域url。回调函数处理JSON数据  兼容性好 不支持post

简述原理与过程：首先在客户端注册一个callback, 然后把callback的名字传给服务器。此时，服务器先生成一个function , function 名字就是传递上来的参数。最后将 json 数据直接以入参的方式，放置到 function 中，这样就生成了一段 js 语法的文档，返回给客户端。客户端浏览器，解析script标签，并执行返回的 javascript 文档，此时数据作为参数，传入到了客户端预先定义好的 callback 函数里
```javascript
 <script> 
  var url = "http://localhost:8080/crcp/rcp/t99eidt/testjson.do?jsonp=callbackfunction";  
  var script = document.createElement('script');  
  script.setAttribute('src', url);  //load javascript   
  document.getElementsByTagName('head')[0].appendChild(script);  
   
  //回调函数 
   function callbackfunction(data){ 
var html=JSON.stringify(data.RESULTSET); 
alert(html); 
     } 
```
cors：通过设置Access-Control-Allow-Origin来允许跨域 cors可用ajax发请求获取数据 但是兼容性没有jsonp好 
### 6.多页面通信有哪些方案，各有什么不同

localstorge在一个标签页里被添加、修改或删除时，都会触发一个storage事件，通过在另一个标签页里监听storage事件，即可得到localstorge存储的值，实现不同标签页之间的通信。

settimeout+cookie

### 7.用Node实现一个用户上传文件的后台服务应该怎么做

multer模块
### 8.XSS和CSRF攻击

xss：比如在一个论坛发帖中发布一段恶意的JavaScript代码就是脚本注入，如果这个代码内容有请求外部服务器，那么就叫做XSS

写一个脚本将cookie发送到外部服务器这就是xss攻击但是没有发生csrf

防范：对输入内容做格式检查 输出的内容进行过滤或者转译

CSRF：又称XSRF，冒充用户发起请求（在用户不知情的情况下）,完成一些违背用户意愿的请求 如恶意发帖，删帖

比如在论坛发了一个删帖的api链接 用户点击链接后把自己文章给删了 这里就是csrf攻击没有发生xss

防范：验证码 token 来源检测
### 9.输入网址后到页面展现的过程

通过dns解析获取ip

tcp链接

客户端发送http请求

tcp传输报文

服务器处理请求返回http报文

客户端解析渲染页面 （构建DOM树 –> 构建渲染树 –> 布局渲染树：计算盒模型位置和大小 –> 绘制渲染树）
### 10. http请求头

get post delete put head options trace connect

OPTIONS：返回服务器针对特定资源所支持的HTTP请求方法

### 11.前端性能优化

1.减少http请求 使用sprite图、合并js和css文件

2.使用cdn 将用户安排在近的服务器上

3.使用缓存 缓存ajax 使用外部的css和js以便缓存 使用expire cach-control etag

4.压缩资源 使用gzip压缩js和css文件

5.代码层面 避免使用样式表达式、通配符选择器、样式放在顶部、脚本放在底部
### 12.如何解决ajax无法后退的问题

HTML5里引入了新的API，即：history.pushState, history.replaceState

可以通过pushState和replaceState接口操作浏览器历史，并且改变当前页面的URL。

onpopstate监听后退
### 13.分域名请求图片的原因和好处

浏览器的并发请求数目限制是针对同一域名的，超过限制数目的请求会被阻塞

浏览器并发请求有个数限制，分域名可以同时并发请求大量图片
### 14.页面的加载顺序

html顺序加载，其中js会阻塞后续dom和资源的加载，css不会阻塞dom和资源的加载但是会阻塞js的加载。

浏览器会使用prefetch对引用的资源提前下载

1.没有 defer 或 async，浏览器会立即加载并执行指定的脚本

2.有 async，加载和渲染后续文档元素的过程将和 script.js 的加载与执行并行进行(下载异步，执行同步，加载完就执行)。

3.有 defer，加载后续文档元素的过程将和 script.js 的加载并行进行（异步），但是 script.js 的执行要在所有元素解析完成之后，DOMContentLoaded 事件触发之前完成。
### 15.计算机网络的分层概述

tcp/ip模型：从下往上分别是链路层，网络层，传输层，应用层

osi模型：从下往上分别是物理层，链路层，网络层，传输层，会话层，表示层，应用层。