<!--
 * @Descripttion: 
 * @version: 
 * @Author: tina.cai
 * @Date: 2020-06-06 23:12:22
 * @LastEditors: tina.cai
 * @LastEditTime: 2020-06-07 12:51:04
--> 
# 206.反转链表

## 题目描述

```
反转一个单链表。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
进阶:
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-linked-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/24#issuecomment-640155664

### 思路

1. 定义当前及上一个节点为null；
2. 直到当前不等于null循环该链表；
3. 把next存起来，当前的next等于上一个节点，上一个节点等于当前节点，当前节点等于下一个节点；

### 代码
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
  let cur = head;
  let pre = null;
  while(cur){
    const next = cur.next;
    cur.next = pre;
    pre = cur;
    cur = next;
  }
  return pre
};
```

# 参考回答



## 伪代码：

```js
    var reverseList = function(head) {
        let cur = head;
        let pre = null;
        while(cur){
            const next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
```

