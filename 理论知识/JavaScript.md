# JavaScript 相关问题
### 1.let和const的区别
let声明的变量可以改变，值和类型都可以改变，没有限制。
const声明的变量不得改变值

### 2. es6新特性

### 3. 闭包和闭包常用场景
> 应用场景 设置私有变量和方法
 不适合场景：返回闭包的函数是个非常大的函数
 闭包的缺点就是常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。

### 4.为什么会出现闭包这种东西，解决了什么问题
> 受JavaScript链式作用域结构的影响，父级变量中无法访问到子级的变量值，为了解决这个问题，才使用闭包这个概念

### 5. 介绍一下你所了解的作用域链,作用域链的尽头是什么，为什么
> 每一个函数都有一个作用域，比如我们创建了一个函数，函数里面又包含了一个函数，那么现在 就有三个作用域，这样就形成了一个作用域链。
作用域的特点就是，先在自己的变量范围中查找，如果找不到，就会沿着作用域链往上找。

### 6. 一个Ajax建立的过程是怎样的，主要用到哪些状态码
ajax：在不切换页面的情况下完成异步的HTTP请求

(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象.

(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息.

(3)设置响应HTTP请求状态变化的函数.

(4)发送HTTP请求.

(5)获取异步调用返回的数据.

(6)使用JavaScript和DOM实现局部刷新.

当前状态readystate

0 代表未初始化。 还没有调用 open 方法
1 代表正在加载。 open 方法已被调用，但 send 方法还没有被调用
2 代表已加载完毕。send 已被调用。请求已经开始
3 代表交互中。服务器正在发送响应
4 代表完成。响应发送完毕

常用状态码status

404 没找到页面(not found)
403 禁止访问(forbidden)
500 内部服务器出错(internal service error)
200 一切正常(ok)
304 没有被修改(not modified)(服务器返回304状态，表示源文件没有被修改）

### 7.说说你还知道的其他状态码，状态码的存在解决了什么问题

302/307　　临时重定向
301　永久重定向
**状态码：** 表示网页服务器超文本传输协议响应状态的3位数字代码

* 2xx成功 ==> 代表请求已成功被服务器接收、理解、并接受
> a.200 OK 请求已成功，请求所希望的响应头或数据体将随此响应返回（GET）。
  b.204 No Content 服务器成功处理了请求，没有返回任何内容（创建成功 ==> POST）。
  
* 3xx重定向 ==> 代表需要客户端采取进一步的操作才能完成请求
> a.301 Move Permanently 被请求的资源已永久移动到新位置，并且将来任何对此资源的引用都应该使用本响应返回的若干个URI之一。
  b.302 Found 要求客户端执行临时重定向。
  c.304 Not Modified 表示资源未被修改。在这种情况下，由于客户端仍然具有以前下载的副本，因此不需要重新传输资源。
  
* 4xx客户端错误 ==> 代表了客户端看起来可能发生了错误，妨碍了服务器的处理
> a.403 Forbidden 客户端错误，服务器已经理解请求，但是拒绝执行它。
  b.404 Not Found 请求失败，请求所希望得到的资源未被在服务器上发现，但允许用户的后续请求。
  
5xx服务器错误 ==> 表示服务器无法完成明显有效的请求
> a.500 Internal Server Error 通用错误消息，服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。
  b.502 Bad Gateway 作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应。

借助状态码,用户可以知道服务器端是正常处理了请求,还是出现了什么错误

### 8.JavaScript的内存回收机制

垃圾回收器会每隔一段时间找出那些不再使用的内存，然后为其释放内存。

一般使用标记清除方法  当变量进入环境标记为进入环境，离开环境标记为离开环境

还有引用计数方法

堆栈

stack为自动分配的内存空间，它由系统自动释放；而heap则是动态分配的内存，大小不定也不会自动释放。

基本数据类型存放在栈中

引用类型 存放在堆内存中，首先从栈中获得该对象的地址指针，然后再从堆内存中取得所需的数据

### 9. 函数防抖和函数节流
函数防抖是指频繁触发的情况下，只有足够的空闲时间，才执行代码一次

函数防抖的要点，也是需要一个setTimeout来辅助实现。延迟执行需要跑的代码。
如果方法多次触发，则把上次记录的延迟执行代码用clearTimeout清掉，重新开始。
如果计时完毕，没有方法进来访问触发，则执行代码。

``` javascript
//函数防抖
var timer = false
document.getElementById("debounce").onScroll = function() {
        clearTimeout(timer)  
        timer = setTimeout(function(){
                console.log(‘函数防抖’) 
  }, 300)     
}
```
函数节流是指一定时间内js方法只跑一次

函数节流的要点是，声明一个变量当标志位，记录当前代码是否在执行。
如果空闲，则可以正常触发方法执行。
如果代码正在执行，则取消这次方法执行，直接return。
``` javascript
//函数节流
var canScroll = true;
document.getElementById('throttle').onScroll = function() {
               if (!canScroll) {
                return;
               }
                canScroll = false;
                setTimeout(function(){
                   console.log('函数节流');
                   canScroll = true;
                },300)       
}
```

### 10. javaScript中的this是什么，有什么用，它的指向是什么

全局代码中的this  是指向全局对象

作为对象的方法调用时指向调用这个函数的对象。

作为构造函数指向新创建的对象

使用apply和call设置this

### 11. 简单介绍一下promise，他解决了什么问题

Promise，就是一个对象，用来传递异步操作的消息。有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和 Rejected（已失败）。

有了 Promise 对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。

### 12.严格模式的特性

严格模式对Javascript的语法和行为，都做了一些改变。

全局变量必须显式声明。

对象不能有重名的属性

函数必须声明在顶层

* 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
* 消除代码运行的一些不安全之处，保证代码运行的安全；
* 提高编译器效率，增加运行速度；
* 为未来新版本的Javascript做好铺垫。

### 13.js的原型链，如何实现继承？

```javascript
function foo(){}
foo.prototype.z = 3;
var obj = new foo();
obj.x=1;
obj.y=2;
obj.x //1
obj.y //2
obj.z //3
```
### 14.事件模型和事件代理
事件三个阶段：事件捕获，目标，事件冒泡（低版本ie不支持捕获阶段）

w3c绑定事件target.addEventListener(event,handler,false)

解绑target.removeEventListener(eventType, handler, false)

ie绑定 target.attachEvent(on+event, handler)

解绑target.detachEvent("on"+eventType, handler)

事件代理优点：

可以大量节省内存占用，减少事件注册，比如在table上代理所有td的click事件就非常棒

可以实现当新增子对象时无需再次对其绑定事件，**对于动态内容部分尤为合适**

bind和trigger实现：

创建一个类或是匿名函数，在bind和trigger函数外层作用域创建一个字典对象，用于存储注册的事件及响应函数列表，bind时，如果字典没有则创建一个，key是事件名称，value是数组，里面放着当前注册的响应函数，如果字段中有，那么就直接push到数组即可。trigger时调出来依次触发事件响应函数即可。
```javascript
function Emitter() {
    this._listener = [];//_listener[自定义的事件名] = [所用执行的匿名函数1, 所用执行的匿名函数2]
}
  
//注册事件
Emitter.prototype.bind = function(eventName, callback) {
    var listener = this._listener[eventName] || [];//this._listener[eventName]没有值则将listener定义为[](数组)。
    listener.push(callback);
    this._listener[eventName] = listener;
}
  
 //触发事件
Emitter.prototype.trigger = function(eventName) {
    var args = Array.prototype.slice.apply(arguments).slice(1);//atgs为获得除了eventName后面的参数(注册事件的参数)
    var listener = this._listener[eventName];
  
    if(!Array.isArray(listener)) return;//自定义事件名不存在
    listener.forEach(function(callback) {
        try {
            callback.apply(this, args);
        }catch(e) {
            console.error(e);
        }
    })
}
```
### 15.setTimeout,setInterval,requestAnimationFrame之间的区别

setInterval如果函数执行的时间很长的话，第二次的函数会放到队列中，等函数执行完再执行第二次，导致时间间隔发生错误。

而settimeout一定是在这个时间定时结束之后,它才会执行

requestAnimationFrame是为了做动画专用的一个方法，这种方法对于dom节点的操作会比较频繁。
### 16.