# 160. 相交链表

## 题目描述

```
编写一个程序，找到两个单链表相交的起始节点。

如下面的两个链表：

img
image

在节点 c1 开始相交。

示例 1：

img
image

输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。

示例 2：

img
image

输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。

示例 3：

img
image

输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。

注意：

如果两个链表没有交点，返回 null.
在返回结果后，两个链表仍须保持原有的结构。
可假定整个链表结构中没有循环。
程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/intersection-of-two-linked-lists
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/28#issuecomment-642062668

### 思路

循环a链表定义一个flag标识，循环b链表如果存在flag为true则返回当前，否则返回null

### 代码
```js
/**
 * @param {ListNode} headA
 * @param {ListNode} headB
 * @return {ListNode}
 */
// var getIntersectionNode = function(headA, headB) {
//   while(headA){
//     headA.flag = true;
//     headA = headA.next
//   }

//   while(headB){
//     if(headB.flag) return headB
//     headB = headB.next
//   }
//   return null;

// };
var getIntersectionNode = function(headA, headB) {
  while(headA){
    headA.flag = true;
    headA = headA.next
  }

  while(headB){
    if(headB.flag) return headB
    headB = headB.next
  }
  return null;
};
```

# 参考回答

## 前置知识

- 数组的遍历(正向遍历和反向遍历)

## 思路

这道题其实我们可以把它想象成小学生练习加法，只不过现在是固定的“加一”那么我们只需要考虑如何通过遍历来实现这个加法的过程就好了。

加法我们知道要从低位到高位进行运算，那么只需要对数组进行一次反向遍历即可。

伪代码：

```java
for(int i = n - 1; i > - 1; i --) {
  内部逻辑
}
```

内部逻辑的话，其实有三种情况：

```
1. 个位上的数字小于9
    17
+   1
= 18
2. 个位数上等于9，其他位数可以是0-9的任何数，但是首位不等于9
    199
+     1
=  200

    109
+      1
=  110
3. 所有位数都为9
    99
+    1
= 100

      999
+       1
=  1000
```

第一种情况是最简单的，我们只需将数组的最后一位进行+1操作就好了

第二种情况稍微多了一个步骤：我们需要把个位的carry向前进一位并在计算是否有更多的进位

第三种其实和第二种是一样的操作，只是由于我们知道数组的长度是固定的，所以当我们遇到情况三的时候需要扩大数组的长度。我们只需要在结果数组前多加上一位就好了。

```js
// 首先我们要从数组的最后一位开始我们的计算得出我们新的sum
sum = arr[arr.length - 1] + 1

// 接下来我们需要判断这个新的sum是否超过9
sum > 9 ?

// 假如大于 9, 那么我们会更新这一位为 0 并且将carry值更改为1
carry = 1
arr[i] = 0

// 假如不大于 9，更新最后一位为sum并直接返回数组
arr[arr.length - 1] = sum
return arr

// 接着我们要继续向数组的倒数第二位重复进行我们上一步的操作
...

// 当我们完成以后，如果数组第一位时的sum大于0，那么我们就要给数组的首位增添一个1
result = new array with size of arr.length + 1
result[0] = 1
result[1] ...... result[result.length - 1]  = 0 // 
```
## 代码

```js
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
    var carry = 1 // 我们将初始的 +1 也当做是一个在个位的 carry
    for(var i = digits.length - 1; i > -1; i-- ) {
        if(carry) {
            var sum = carry + digits[i]
            digits[i] = sum % 10
            carry = sum > 9 ? 1 : 0 // 每次计算都会更新下一步需要用到的 carry
        }
    }
    if(carry === 1) {
        digits.unshift(1) // 如果carry最后停留在1，说明有需要额外的一个长度 所以我们就在首位增添一个 1
    }
    return digits
};
```

_Originally posted by @chtTina in https://github.com/leetcode-pp/91alg-1/issues/1#issuecomment-636883697_