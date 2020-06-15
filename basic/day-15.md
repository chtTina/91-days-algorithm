<!--
 * @Descripttion: 
 * @version: 
 * @Author: tina.cai
 * @Date: 2020-06-14 17:03:25
 * @LastEditors: tina.cai
 * @LastEditTime: 2020-06-16 00:40:03
--> 
# 129. 求根到叶子节点数字之和

## 题目描述

```
给定一个二叉树，它的每个结点都存放一个 0-9 的数字，每条从根到叶子节点的路径都代表一个数字。

例如，从根到叶子节点路径 1->2->3 代表数字 123。

计算从根到叶子节点生成的所有数字之和。

说明: 叶子节点是指没有子节点的节点。

示例 1:

输入: [1,2,3]
    1
   / \
  2   3
输出: 25
解释:
从根到叶子节点路径 1->2 代表数字 12.
从根到叶子节点路径 1->3 代表数字 13.
因此，数字总和 = 12 + 13 = 25.
示例 2:

输入: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
输出: 1026
解释:
从根到叶子节点路径 4->9->5 代表数字 495.
从根到叶子节点路径 4->9->1 代表数字 491.
从根到叶子节点路径 4->0 代表数字 40.
因此，数字总和 = 495 + 491 + 40 = 1026.
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/sum-root-to-leaf-numbers
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/35#issuecomment-644242263

### 思路

1.首先定义一个sum计算总和；
2.拆分子节点，如果当前节点为null直接返回，定一个变量存储传入的值*10 + 当前跟节点的值，
如果当前节点左右都为null则证明到底了，sum = sum+ k；循环的遍历左右节点的子节点总和；

### 代码
```js
/**
 * @param {TreeNode} root
 * @return {number}
 */
var sumNumbers = function(root) {
  this.sum = 0;
  childNumbers(this.sum, root);
  return this.sum;
};

var childNumbers = function(val, root){
  if(root == null) return;
  let k = val * 10 + root.val;
  if(root.left == null && root.right == null){
    this.sum += k;
  }

  childNumbers(k, root.left);
  childNumbers(k, root.right);
}
```

# 参考回答
