## this
### 一.this的来源
this是JavaScript的关键字;this不仅函数内可以用，在所有函数外(全局上下文中)也可以用；函数中的this的含义在函数声明时无法确定，要到运行期才能确定，而且与调用函数的方式有关；代码是否是严格模式也会影响this的取值。

### 二.this到底是什么
在ES5.1中，有一个所谓执行上下文(Execution Context，EC)的概念，简单的说就是JS引擎的执行进入到某块代码区域时，为该代码区域建立的上下文对象，主要用来记录该区域中声明的变量、函数等。

EC有三个重要组成部分：**VE**、**LE**和**ThisBinding**。前两个是词法环境，暂且不管。第三个**ThisBinding**就是指在该代码区域的this的值。

可见，this是跟某块代码区域关联的。而在JS中，代码区域有三种：
* global代码
* function代码
* eval代码

此文中主要讨论前两种。

### 三.全局代码区域中的this
全局代码区域是所有函数之外的区域。在此区域中的this就是指全局对象window(在Node.js中是global)。

### 四.函数代码区域中的this
函数代码区域是指某个函数内的代码，但是不包括它所嵌套的函数内的代码。从我们可以看出：
> this是与包裹它的且离它最近的函数相关的，this既不能穿透到外部的函数，也不能穿透进内部的函数。

```javascript
//示例：
btn.addListener('click', function() {
    var that = this;
    dosth(function() {
        console.log(that.name);
    });
});
```
通常每个函数中的this是不同的，内部函数可以引用外部函数的局部变量，但是不能直接引用外部函数的this。通过将外部函数的this赋值给一个局部变量可以解决这个问题。

函数内的this的具体函数比较复杂，主要与调用这个函数的方式有关。主要包括以下情况：
#### 1.直接调用时
```javascript
//示例：
var num = 123;
function fn() {
    console.log(this.num);
}

function fn2() {
    "use strict"
    console.log(this.num);
}

fn(); // 输出123
fn2(); // 报错
```
直接调用函数时，如果是在严格模式下，this会被设为undefined；如果是在非严格模式下，this会被设为全局对象window。
#### 2.作为方法调用时
```javascript
//示例：
var student = {
    name: 'Tom',
    sayName: function() {
        console.log(this.name);
    }
};

student.sayName(); // 输出Tom
```
作为方法调用时，this指方法所属的对象。
#### 3.call和apply方法：调用时指定this
除了上述两种固定的情况外，Javascript提供了一种可以随心所欲地根据需要更改函数中this方法。即使用函数对象的call或apply方法来调用函数，显然这种方式给编程带来了极大的灵活性。
```javascript
//示例：
function fn() {
    var args = Array. prototype. slice.call(arguments, 1);
    console.log(args);
}

fn(1, 2, 3); // 输出[2, 3]
```
这种方法常用的场景就是：把一个对象的方法"借"给另一个具有类似结构的对象使用。
#### 4. bind方法：重新绑定函数的this
与call和apply不同，bind方法是在调用前就把函数内的this绑定了，而且一旦绑定就不能再改变。实际上bind方法返回了一个原函数的新版本。
```javascript
//示例：
function fn() {
    console.log(this.age);
}

var fn2 = fn.bind({age: 18});
fn2() // 输出18
fn2.call({age: 25}) // 输出18
```
通过bind得到的函数，不论用哪种方式调用，它的this都是相同的。
#### 5.

