# 146. LRU缓存机制

## 题目描述

```
运用你所掌握的数据结构，设计和实现一个 LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果关键字 (key) 存在于缓存中，则获取关键字的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字/值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

示例:

LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得关键字 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得关键字 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/lru-cache
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/31#issuecomment-643739816

### 思路

思路：
1. 定义一个数组用来存储对应数据；
2. 调用get时循环遍历这个数组是否有对应的item.key等于对应的key，如果有则把这个item插入到数组的最前面，否则返回-1；
3. 调用put的时候循环遍历是否有当前key，如果有则把当前key从数组删除插入到最前，如果没有判断数组列表长度是否大于capacity，如果不大于则直接插入到数组最前面，如果大于等于则把数组最后一个元素删除，并把当前元素插入到数组最前面；

### 代码
```js
/**
 * @param {number} capacity
 */
var LRUCache = function(capacity) {
  this.data = [];
  this.capacity = capacity
};

/** 
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function(key) {
  let res = -1;
  let index = -1;
  this.data.forEach((item, i) => {
    if(item.key === key){
      res = item.value,
      index = i
    }
  })

  if(index > -1){
    this.data.splice(index, 1);
    this.data.unshift({key, value: res})
  }

  return res;
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function(key, value) {
  let index = this.data.findIndex(item => {
    return item.key === key
  })

  if(index > -1){
    this.data.splice(index, 1);
    this.data.unshift({key, value: value})
  }else{
    if(this.data.length === this.capacity){
      this.data.splice(this.data.length - 1, 1);
      this.data.unshift({key, value})
    }else{
      this.data.unshift({key, value})
    }
  }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * var obj = new LRUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */
```

# 参考回答

