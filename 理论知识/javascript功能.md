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
### 2.