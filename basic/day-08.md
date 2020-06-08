# 430.扁平化多级双向链表

## 题目描述

```
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:

输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
示例 2:

输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/plus-one
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
