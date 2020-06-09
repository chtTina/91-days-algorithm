<!--
 * @Descripttion: 
 * @version: 
 * @Author: tina.cai
 * @Date: 2020-06-10 00:06:05
 * @LastEditors: tina.cai
 * @LastEditTime: 2020-06-10 00:08:35
--> 
# 109.有序链表转换二叉搜索树

## 题目描述

```
给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5   
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/27#issuecomment-641400590

### 思路

1. 首先循环链表用一个数组arr存储链表的所有值；
2. 写递归分治函数，如果左边大于右边return null，如果左边等于右边证明是同一个值，直接return newTree(arr[left/right]);如果右边-左边等于1，则新增一个r的树节点，值为arr[right]，r的左边等于new newTree(arr[left])，直接return r；
3. 得出中间的数组值mid,新增root节点为mid，root节点左边递归等于根的左边，root节点右边递归等于根的右边，最后返回根节点。

### 代码
```js
/**
 * @param {ListNode} head
 * @return {TreeNode}
 */
var sortedListToBST = function(head) {
  let child = head;
  let arr = []

  while(child){
    arr.push(child.val);
    child = child.next
  }

  function createTree(arr, left, right){
    if(left > right) return null
    if(left === right) return new TreeNode(arr[left])
    if(right - left === 1){
      let r = new TreeNode(arr[right]);
      r.left = new TreeNode(arr[left])
      return r;
    }

    let mid = (left + right + 1) >> 1;
    let root = new TreeNode(arr[mid]);
    root.left = createTree(arr, left, mid - 1)
    root.right = createTree(arr, mid + 1, right)
    return root
  }

  return createTree(arr, 0, arr.length - 1)
  
};
```

# 参考回答
