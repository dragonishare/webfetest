# JavaScript算法相关问题

### 1.判断链表是否有环

使用追赶的方法，设定两个指针slow、fast，从头指针开始，每次分别前进1步、2步。如存在环，则两者相遇；如不存在环，fast遇到NULL退出。

### 2. 输出二叉树的最小深度

 判断左子树或右子树是否为空，若左子树为空，则返回右子树的深度，反之返回左子树的深度，如果都不为空，则返回左子树和右子树深度的最小值。

### 3. 写一个快速排序

```javascript
var quickSort = function (arr){
        if(arr.lenght <= 1) {
           return arr;
          }
 
       var left = [];
       var right = [];
       var mid = arr.splice(Math.floor(arr.length/2), 1);
 
       for(var i=0;i<arr.length;i++){
             if(arr[i]<mid) {
                 left.push(arr[i]);
            }
             if(arr[i]>mid) {
                 right.push(arr[i]);
            }
          return quickSort(left).concat(mid, quickSort(right));
     }  
}  
```
### 4. 冒泡排序、快速排序、去重、查找字符串最多值
```javascript
//冒泡排序
var bubbleSort = function(arr) {
   for (var i = 0; i < arr.length-1; i++) {
     for (var j = i+1; j < arr.length; j++) {
       if (arr[i]>arr[j]) {
         var temp = arr[i];
         arr[i] = arr[j];
         arr[j] = temp;
       }
     }
   }
   return arr;
};

//快速排序
var quickSort = function(arr) {
  if (arr.length <= 1) {
    return arr;
  }
  var len = arr.length;
  var midIndex = Math.floor(len/2);
  var mid = arr.splice(midIndex,1);
  var left = [];
  var right = [];
  for (var i = 0; i < arr.length; i++) {
    if (arr[i] < mid) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }
  return quickSort(left).concat(mid,quickSort(right))
}

// 去重
 var distinct = function(arr) {
   var map = {};
   var result = [];
   for (var i = 0; i < arr.length; i++) {
      if (!map[arr[i]]) {
        map[arr[i]] = true;
        result.push(arr[i]);
      }
   }
   return result;
 }

//查找字符串中最多的值
var search = function(str) {
  var json = {};
  var max = 0;
  var char;
  for (var i = 0; i < str.length; i++) {
    if (!json[str[i]]) {
      json[str[i]]=1;
    } else {
      json[str[i]]++;
    }
  }
  console.log(json);
  for(var i in json){
        if(json[i]>max){
                max = json[i];
                char = i;
        }
}
  console.log(max, char);
}
```
### 5.广度优先遍历的非递归写法
```javascript
function wideTraversal(selectNode) {
   var nodes = [];
   if (selectNode != null) {
     var queue = [];
     queue.unshift(selectNode);
     while (queue.length != 0) {
        var item = queue.shift();
            nodes.push(item);
            var children = item.children;
            for (var i = 0; i < children.length; i++)
                queue.push(children[i]);
      }
   }
   return nodes;
}
```
### 6.广度优先遍历的递归写法：
```javascript
function wideTraversal(node) {
   var nodes = [];
   var i = 0;
   if (!(node == null)) {
     nodes.push(node);
     wideTraversal(node.nextElementSibling);
     node = nodes[i++];
     wideTraversal(node.firstElementChild);
   }
   return nodes;
}
```
### 7.深度优先遍历的递归写法
```javascript
function deepTraversal(node) {
    var nodes = [];
    if (node != null) {  
            nodes.push(node);  
            var children = node.children;  
            for (var i = 0; i < children.length; i++)  
                   deepTraversal(children[i]);  
        }  
    return nodes;
}
```
### 8.深度优先遍历的非递归写法
```javascript
function deepTraversal(node) {
    var nodes = [];
    if (node != null) {
        var stack = [];
        stack.push(node);
        while (stack.length != 0) {
            var item = stack.pop();
            nodes.push(item);
            var children = item.children;
            for (var i = children.length - 1; i >= 0; i--)
                stack.push(children[i]);
        }
    }  
    return nodes;
}
```
### 9.
