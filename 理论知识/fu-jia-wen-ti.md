# 附加问题
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

* Expires（强缓存）+过期时间   Expires是HTTP1.0提出的一个表示资源过期时间的header，它描述的是一个绝对时间

* Cache-control（强缓存） 描述的是一个相对时间，在进行缓存命中的时候，都是利用客户端时间进行判断 管理更有效，安全一些 Cache-Control: max-age=3600

* Last-Modified/If-Modified-Since（协商缓存） 标示这个响应资源的最后修改时间。Last-Modified是服务器相应给客户端的，If-Modified-Sinces是客户端发给服务器，服务器判断这个缓存时间是否是最新的，是的话拿缓存。

* Etag/If-None-Match（协商缓存） etag和last-modified类似，他是发送一个字符串来标识版本。

### 3.AMD/CMD/CommonJs到底是什么？它们有什么区别？
> AMD/CMD/CommonJs是JS模块化开发的标准，目前对应的实现是RequireJs/SeaJs/nodeJs
* [Javascript模块化编程（一）：模块的写法](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)
* [Javascript模块化编程（二）：AMD规范](http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html)
* [Javascript模块化编程（三）：require.js的用法](http://www.ruanyifeng.com/blog/2012/11/require_js.html)

* CommonJs主要针对服务端，AMD/CMD主要针对浏览器端，所以最容易混淆的是AMD/CMD。（顺便提一下，针对服务器端和针对浏览器端有什么本质的区别呢？服务器端一般采用同步加载文件，也就是说需要某个模块，服务器端便停下来，等待它加载再执行。而浏览器端要保证效率，需要采用异步加载，这就需要一个预处理，提前将所需要的模块文件并行加载好。）

* AMD，即 (Asynchronous Module Definition)，这种规范是异步的加载模块，requireJs应用了这一规范。先定义所有依赖，然后在加载完成后的回调函数中执行;
* CMD (Common Module Definition), 是seajs推崇的规范，CMD则是依赖就近，用的时候再require;
* AMD和CMD最大的区别是对依赖模块的执行时机处理不同，而不是加载的时机或者方式不同，二者皆为异步加载模块。
AMD依赖前置，js可以方便知道依赖模块是谁，立即加载；而CMD就近依赖，需要使用把模块变为字符串解析一遍才知道依赖了那些模块，这也是很多人诟病CMD的一点，牺牲性能来带来开发的便利性，实际上解析模块用的时间短到可以忽略。

* AMD 是提前执行，CMD 是延迟执行;CMD 推崇依赖就近，AMD 推崇依赖前置;
* AMD/CMD区别，虽然都是并行加载js文件，但还是有所区别，AMD是预加载，在并行加载js文件同时，还会解析执行该模块（因为还需要执行，所以在加载某个模块前，这个模块的依赖模块需要先加载完成）；而CMD是懒加载，虽然会一开始就并行加载js文件，但是不会执行，而是在需要的时候才执行。

* AMD/CMD的优缺点.一个的优点就是另一个的缺点， 可以对照浏览。
                + AMD优点：加载快速，尤其遇到多个大文件，因为并行解析，所以同一时间可以解析多个文件。
                + AMD缺点：并行加载，异步处理，加载顺序不一定，可能会造成一些困扰，甚至为程序埋下大坑。
                + CMD优点：因为只有在使用的时候才会解析执行js文件，因此，每个JS文件的执行顺序在代码中是有体现的，是可控的。
                + CMD缺点：执行等待时间会叠加。因为每个文件执行时是同步执行（串行执行），因此时间是所有文件解析执行时间之和，尤其在文件较多较大时，这种缺点尤为明显。

* 如何使用？CommonJs的话，因为nodeJs就是它的实现，所以使用node就行，也不用引入其他包。AMD则是通过<script>标签引入RequireJs。CMD则是引入SeaJs。

### 4. get和post有什么不同
get是从服务器上获取数据，post是向服务器传送数据
get请求可以将查询字符串参数追加到url的末尾; post请求应该把数据作为请求的主体提交.
get请求数据有大小限制；post没有
post比get安全性更高

### 5. cookie和session有什么联系和区别

cookie数据存放在客户的浏览器上，session数据放在服务器上。

session比cookie更安全

单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

一般用cookie来存储sessionid

### 6. 








