# 380.常数时间插入、删除和获取随机元素

## 题目描述

```
设计一个支持在平均 时间复杂度 O(1) 下，执行以下操作的数据结构。

insert(val)：当元素 val 不存在时，向集合中插入该项。
remove(val)：元素 val 存在时，从集合中移除该项。
getRandom：随机返回现有集合中的一项。每个元素应该有相同的概率被返回。
示例 :

// 初始化一个空的集合。
RandomizedSet randomSet = new RandomizedSet();

// 向集合中插入 1 。返回 true 表示 1 被成功地插入。
randomSet.insert(1);

// 返回 false ，表示集合中不存在 2 。
randomSet.remove(2);

// 向集合中插入 2 。返回 true 。集合现在包含 [1,2] 。
randomSet.insert(2);

// getRandom 应随机返回 1 或 2 。
randomSet.getRandom();

// 从集合中移除 1 ，返回 true 。集合现在包含 [2] 。
randomSet.remove(1);

// 2 已在集合中，所以返回 false 。
randomSet.insert(2);

// 由于 2 是集合中唯一的数字，getRandom 总是返回 2 。
randomSet.getRandom();

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/insert-delete-getrandom-o1
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答
https://github.com/leetcode-pp/91alg-1/issues/23#issuecomment-640075761


### 思路

1. 初始化一个数组；
2. insert的时候循环遍历数组是否存在val，如果存在直接return false，否则遍历结束把val推到数组里return true；
3. remove的时候循环遍历是否存在val，如果存在裁剪数组return true，否则return false；
4. getRandom使用Math.random得到一个0-1的值，要获取min-max的随机数公式为 parseInt(Math.random()*(max+1-min) + min),直接返回数组对应的下标;


### 代码
```js
/**
 * Initialize your data structure here.
 */
var RandomizedSet = function() {
  this.result = [];
};

/**
 * Inserts a value to the set. Returns true if the set did not already contain the specified element. 
 * @param {number} val
 * @return {boolean}
 */
RandomizedSet.prototype.insert = function(val) {
  let length = this.result.length;
  for(let i = 0; i < length; i++ ){
    if(this.result[i] == val){
      return false;
    }
  }

  this.result.push(val);
  return true;
};

/**
 * Removes a value from the set. Returns true if the set contained the specified element. 
 * @param {number} val
 * @return {boolean}
 */
RandomizedSet.prototype.remove = function(val) {
  let length = this.result.length;
  for(let i = 0; i < length; i++ ){
    if(this.result[i] == val){
      this.result.splice(i,1);
      return true;
    }
  }
  return false;
};

/**
 * Get a random element from the set.
 * @return {number}
 */
RandomizedSet.prototype.getRandom = function() {
  let indexCount = this.result.length - 1
  let randomIndex = parseInt(Math.random()*(indexCount+1))
  console.log(randomIndex, 'index');
  return this.result[randomIndex]
};
```

# 参考回答

