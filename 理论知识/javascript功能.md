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

### 4.