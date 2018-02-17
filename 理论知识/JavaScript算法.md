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
### 4. 