<!--
 * @Descripttion: 
 * @version: 
 * @Author: tina.cai
 * @Date: 2020-06-16 00:37:55
 * @LastEditors: tina.cai
 * @LastEditTime: 2020-06-19 10:44:44
--> 
# 105. 从前序与中序遍历序列构造二叉树

## 题目描述

````
根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出

前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
````

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/38#issuecomment-646402636

### 思路

由于知道前序第一个就是根节点，计算去切分的位置，分别递归复值左右及根节点即可得到一棵树

### 代码
```js
/**
* @param {number[]} preorder
* @param {number[]} inorder
* @return {TreeNode}
**/
var buildTree = function(preorder, inorder) {
  if (inorder.length === 0) return null
  let root = new TreeNode(preorder[0]);
  let mid = inorder.indexOf(preorder[0])
  root.left = buildTree(preorder.slice(1,mid + 1), inorder.slice(0, mid));
  root.right = buildTree(preorder.slice(mid + 1), inorder.slice(mid + 1));
  return root;
};
```

# 参考回答
