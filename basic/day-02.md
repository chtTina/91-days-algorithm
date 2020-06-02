# 75. 颜色分类

## 题目描述

```
给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

注意:
不能使用代码库中的排序函数来解决这道题。

示例:

输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
进阶：

一个直观的解决方案是使用计数排序的两趟扫描算法。
首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
你能想出一个仅使用常数空间的一趟扫描算法吗？

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/sort-colors
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/15#issuecomment-637457464

### 思路

思路一： 计数排序➕遍历数组

1.先用计数排序得出每个key的总数；
2.遍历计数数组，当key的总数大于0就去替换当前数组；

思路二：双指针

1.定义左右当前三个变量，循环当前key小于最有的数组；
2.判断数组当前值，0: 当前跟最左边交换，左移左指针及当前指针；1: 左移当前指针；2:当前跟最右边交换，右移右指针；


### 代码

代码一：

```
js

var sortColors = function(nums) {
    var count = [];
    for(var i of nums){
        if(count[i]){
            count[i]++;
        }else{
            count[i] = 1;
        }
    }

    let j = 0;
    for(let i = 0; i < count.length; i++){
        while(count[i] > 0){
            nums[j++] = i;
            count[i]--;
        }
    }
    return nums;
};
```

代码二：
```
var sortColors = function(nums) {
    var left = 0,
        right = nums.length - 1,
        cur = 0;
    
    while(cur <= right){
        if(nums[cur] === 0){
            [nums[cur], nums[left]] = [nums[left], nums[cur]];
            left++;
            cur++;
        }else if(nums[cur] === 1){
            cur++;
        }else if(nums[cur] === 2){
            [nums[cur], nums[right]] = [nums[right], nums[cur]];
            right--;
        }
    }
    return nums;
};
```


_Originally posted by @chtTina in https://github.com/leetcode-pp/91alg-1/issues/15#issuecomment-637457464_