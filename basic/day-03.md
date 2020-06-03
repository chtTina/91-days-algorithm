# 1381.设计一个支持增量操作的栈

## 题目描述

```
请你设计一个支持下述操作的栈。

实现自定义栈类 CustomStack ：

CustomStack(int maxSize)：用 maxSize 初始化对象，maxSize 是栈中最多能容纳的元素数量，栈在增长到 maxSize 之后则不支持 push 操作。
void push(int x)：如果栈还未增长到 maxSize ，就将 x 添加到栈顶。
int pop()：弹出栈顶元素，并返回栈顶的值，或栈为空时返回 -1 。
void inc(int k, int val)：栈底的 k 个元素的值都增加 val 。如果栈中元素总数小于 k ，则栈中的所有元素都增加 val 。
 
示例：

输入：
["CustomStack","push","push","pop","push","push","push","increment","increment","pop","pop","pop","pop"]
[[3],[1],[2],[],[2],[3],[4],[5,100],[2,100],[],[],[],[]]
输出：
[null,null,null,2,null,null,null,null,null,103,202,201,-1]
解释：
CustomStack customStack = new CustomStack(3); // 栈是空的 []
customStack.push(1); // 栈变为 [1]
customStack.push(2); // 栈变为 [1, 2]
customStack.pop(); // 返回 2 --> 返回栈顶值 2，栈变为 [1]
customStack.push(2); // 栈变为 [1, 2]
customStack.push(3); // 栈变为 [1, 2, 3]
customStack.push(4); // 栈仍然是 [1, 2, 3]，不能添加其他元素使栈大小变为 4
customStack.increment(5, 100); // 栈变为 [101, 102, 103]
customStack.increment(2, 100); // 栈变为 [201, 202, 103]
customStack.pop(); // 返回 103 --> 返回栈顶值 103，栈变为 [201, 202]
customStack.pop(); // 返回 202 --> 返回栈顶值 202，栈变为 [201]
customStack.pop(); // 返回 201 --> 返回栈顶值 201，栈变为 []
customStack.pop(); // 返回 -1 --> 栈为空，返回 -1
 

提示：

1 <= maxSize <= 1000
1 <= x <= 1000
1 <= k <= 1000
0 <= val <= 100
每种方法 increment，push 以及 pop 分别最多调用 1000 次

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/design-a-stack-with-increment-operation
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/18#issuecomment-637990555

### 思路

首先定义一个数组来存储栈；
进栈判断是否超过最大值，超过则不如栈；
出栈判断是否为空，为空返回-1；
计算increment首先判断最大的循环次数，循环计算数组的值

### 代码
```js
    /*
    * @lc app=leetcode.cn id=1381 lang=javascript
    *
    * [1381] 设计一个支持增量操作的栈
    */

    // @lc code=start
    /**
     * @param {number} maxSize
     */
    var CustomStack = function(maxSize) {
      this.result = [];
      this.maxSize = maxSize;
    };

    /** 
     * @param {number} x
     * @return {void}
     */
    CustomStack.prototype.push = function(x) {
      if(this.result.length >= this.maxSize){
        return 
      }
      this.result.push(x)
    };

    /**
     * @return {number}
     */
    CustomStack.prototype.pop = function() {
      if(this.result.length === 0){
        return -1;
      }

      var top = this.result.pop();
      return top;
    };

    /** 
     * @param {number} k 
     * @param {number} val
     * @return {void}
     */
    CustomStack.prototype.increment = function(k, val) {
      var min = Math.min(k, this.result.length);
      for(let i = 0; i < min; i++){
        this.result[i] += val;
      }
    };

    /**
     * Your CustomStack object will be instantiated and called as such:
     * var obj = new CustomStack(maxSize)
     * obj.push(x)
     * var param_2 = obj.pop()
     * obj.increment(k,val)
     */
```

_Originally posted by @chtTina in https://github.com/leetcode-pp/91alg-1/issues/18#issuecomment-637990555_