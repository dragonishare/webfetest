### 1.写一个组合继承
``` javascript
var Super = function(name){
  this.name = name;
}
Super.prototype.func1 = function() { console.log('func1'); }
var Sub = function(name,age) {
  Super.call(this, name);
  this.age = age;
}
Sub.prototype = new Super();
```
### 2.深拷贝方案有哪些，手写一个深拷贝

```javascript
var clone = function(v) {
  var o = v.constructor === Array ? [] : {};
  for (var i in v) {
    o[i] = typeof v[i] === "Object" ? clone(v[i]) : v[i];
  }
  return o;
}
```

### 3.判断数组有哪些方法

a instanceof Array
a.constructor == Array
Object.prototype.toString.call(a) == [Object Array]

### 4.图片预加载和懒加载
预加载：
```javascript
function loadImage(url, callback) {
    var img = new Image();
    img.src = url;
    if (img.complete) { // 如果图片已经存在于浏览器缓存，直接调用回调函数 防止IE6不执行onload BUG
        callback.call(img);
        return;
    }
    img.onload = function () {
        callback.call(img);//将回调函数的this替换为Image对象
    };
};
```
懒加载：

当网页滚动的事件被触发 -> 执行加载图片操作 -> 判断图片是否在可视区域内 -> 在，则动态将data-src的值赋予该图片。
```javascript
var aImages = document.getElementById("SB").getElementsByTagName('img'); //获取id为SB的文档内所有的图片
loadImg(aImages);
window.onscroll = function() { //滚动条滚动触发
loadImg(aImages);
};
//getBoundingClientRect 是图片懒加载的核心
function loadImg(arr) {
for(var i = 0, len = arr.length; i < len; i++) {
 if(arr[i].getBoundingClientRect().top < document.documentElement.clientHeight && !arr[i].isLoad) {
 arr[i].isLoad = true; //图片显示标志位
 //arr[i].style.cssText = "opacity: 0;";
 (function(i) {
  setTimeout(function() {
  if(arr[i].dataset) { //兼容不支持data的浏览器
   aftLoadImg(arr[i], arr[i].dataset.imgurl);
  } else {
   aftLoadImg(arr[i], arr[i].getAttribute("data-imgurl"));
  }
  arr[i].style.cssText = "transition: 1s; opacity: 1;" //相当于fadein
  }, 500)
 })(i);
 }
}
}
 
function aftLoadImg(obj, url) {
var oImg = new Image();
oImg.onload = function() {
 obj.src = oImg.src; //下载完成后将该图片赋给目标obj目标对象
}
oImg.src = url; //oImg对象先下载该图像
}
```
### 5.将url的查询参数解析成字典对象
```javascript
function getQueryObject(url) {
    url = url == null ? window.location.href : url;
    var search = url.substring(url.lastIndexOf("?") + 1);
    var obj = {};
    var reg = /([^?&=]+)=([^?&=]*)/g;
    search.replace(reg, function (rs, $1, $2) {
        var name = decodeURIComponent($1);
        var val = decodeURIComponent($2);              
        val = String(val);
        obj[name] = val;
        return rs;
    });
    return obj;
}
  
getQueryObject("http://www.cnblogs.com/leee/p/4456840.html?name=1&dd=ddd**")
Object {name: "1", dd: "ddd**"}
```
### 6.