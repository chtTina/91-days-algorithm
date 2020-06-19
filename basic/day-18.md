<!--
 * @Descripttion: 
 * @version: 
 * @Author: tina.cai
 * @Date: 2020-06-16 00:37:55
 * @LastEditors: tina.cai
 * @LastEditTime: 2020-06-19 15:43:50
--> 
# 124. 二叉树中的最大路径和

## 题目描述

````
给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。

示例 1:

输入: [1,2,3]

       1
      / \
     2   3

输出: 6
示例 2:

输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/binary-tree-maximum-path-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
````

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/39#issuecomment-646489669

### 思路

遍历树获取左右最大值，如果比以前保存的值大则覆盖，最后返回左右子树最大值加上当前节点的值

### 代码
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxPathSum = function(root) {
  this.res = root.val;
  getMax(root)
  return this.res;

};

var getMax = function(root){
  if(root == null) return 0;
  let left = Math.max(0, getMax(root.left));
  let right = Math.max(0, getMax(root.right));
  this.res = Math.max(res, left + right + root.val)
  
  return Math.max(left, right) + root.val;
}
```

# 参考回答
