<!--
 * @Descripttion: 
 * @version: 
 * @Author: tina.cai
 * @Date: 2020-06-14 17:03:26
 * @LastEditors: tina.cai
 * @LastEditTime: 2020-06-15 11:07:05
--> 
#  100. 相同的树

## 题目描述

```
给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

示例 1:

输入:       1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

输出: true
输出: true

示例 2:

输入:      1          1
          /           \
         2             2

        [1,2],     [1,null,2]

输出: false
示例 3:

输入:       1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

输出: false
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/same-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/34#issuecomment-643877457

### 思路

思路：
递归左节点及右节点，
如果p==null&&q==null则是相同的树返回true；
如果其中一个为null，返回false不是相同的树；
如果p.val不等于q.val，返回false不是相同的树；


### 代码
```js
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
  if(p == null && q == null){
    return true
  }

  if(p == null || q == null){
    return false
  }

  if(p.val !== q.val){
    return false
  }

  return isSameTree(p.left, q.left) && isSameTree(p.right, q.right)

};
```

# 参考回答
