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

通过动态<script>元素使用，使用时为src指定一个跨域url。回调函数处理JSON数据  兼容性好 不支持post

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
### 6.

