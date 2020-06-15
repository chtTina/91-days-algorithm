<!--
 * @Descripttion: 
 * @version: 
 * @Author: tina.cai
 * @Date: 2020-06-16 00:37:55
 * @LastEditors: tina.cai
 * @LastEditTime: 2020-06-16 01:12:40
--> 
# 513. 找树左下角的值

## 题目描述

````
给定一个二叉树，在树的最后一行找到最左边的值。

示例 1:

输入:

    2
   / \
  1   3

输出:
1
示例 2:

输入:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

输出:
7
``` 

注意: 您可以假设树（即给定的根节点）不为 NULL。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-bottom-left-tree-value
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
````

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/37#issuecomment-644258759

### 思路

思路：定一个变量保存最深度，循环遍历树的左右节点，如果加起来的深度大于最深度则把当前值赋值给最左边的值变量，更新最深度的值为当前；直到跟节点为null；

### 代码
```js
/**
 * @param {TreeNode} root
 * @return {number}
 */
var findBottomLeftValue = function(root) {
  this.defLeft = null;
  this.maxDepth = -1
  findBottom(0,root)
  
  return this.defLeft;
};

var findBottom = function(count,root){
  if(root == null) return ;

  if(this.maxDepth < count){
    this.defLeft = root.val
    this.maxDepth = count  
  }

  count++;
  findBottom(count, root.left);
  findBottom(count, root.right)

}
```

# 参考回答
