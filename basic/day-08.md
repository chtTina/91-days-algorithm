# 430.扁平化多级双向链表

## 题目描述

```
多级双向链表中，除了指向下一个节点和前一个节点指针之外，它还有一个子链表指针，可能指向单独的双向链表。这些子列表也可能会有一个或多个自己的子项，依此类推，生成多级数据结构，如下面的示例所示。

给你位于列表第一级的头节点，请你扁平化列表，使所有结点出现在单级双链表中。

示例 1：

输入：head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
输出：[1,2,3,7,8,11,12,9,10,4,5,6]
解释：

输入的多级列表如下图所示：
image

扁平化后的链表如下图：

image

示例 2：

输入：head = [1,2,null,3]
输出：[1,3,2]
解释：

输入的多级列表如下图所示：

1---2---NULL
|
3---NULL
示例 3：

输入：head = []
输出：[]
 

如何表示测试用例中的多级链表？

以 示例 1 为例：

1---2---3---4---5---6--NULL
|
7---8---9---10--NULL
|
11--12--NULL
序列化其中的每一级之后：

[1,2,3,4,5,6,null]
[7,8,9,10,null]
[11,12,null]
为了将每一级都序列化到一起，我们需要每一级中添加值为 null 的元素，以表示没有节点连接到上一级的上级节点。

[1,2,3,4,5,6,null]
[null,null,7,8,9,10,null]
[null,11,12,null]
合并所有序列化结果，并去除末尾的 null 。

[1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
 

提示：

节点数目不超过 1000
1 <= Node.val <= 10^5

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/flatten-a-multilevel-doubly-linked-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/25#issuecomment-640714827

### 思路

1. 定义一个数组用来存储child的节点；
2. 循环遍历链表，当前节点存在，且当前节点child或next也存在；判断是否有child
    * 如果有child，判断是否有next，
        + 如果有则把当前next推进存储child的数组中，存储child的上一个节点信息cur.child.prev = cur,把当前元素next指向子元素cur.next= cur.child; 把当前元素的子元素置为空cur.child = null;
        + 如果无，存储child的上一个节点信息cur.child.prev = cur,把当前元素next指向子元素cur.next= cur.child; 把当前元素的子元素置为空cur.child = null
    * 如果没有child，cur=cur.next
3. 如果存储child的数组长度大于0；则循环pop出node节点，保存node的上一个元素为cur，当前的下一个元素为node，循环cur.next不为null，这cur = cur.next;
4. 最后返回head

### 代码
```js
/**
 * @param {Node} head
 * @return {Node}
 */
var flatten = function(head) {
    let cur = head;
    let childArr = [];
    while(cur && (cur.child || cur.next)){
      if(cur.child){
        if(cur.next){
          childArr.push(cur.next)
        }
        cur.child.prev = cur
        cur.next = cur.child
        cur.child = null
      }
      cur = cur.next
    }
    while(childArr.length > 0){
      let node = childArr.pop();
      node.prev = cur
      cur.next = node;
      while(cur.next){
        cur = cur.next
      }
    }

    return head;
};
```

# 参考回答
