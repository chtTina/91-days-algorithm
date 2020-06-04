<!--
 * @Descripttion: 
 * @version: 
 * @Author: tina.cai
 * @Date: 2020-06-02 20:38:12
 * @LastEditors: tina.cai
 * @LastEditTime: 2020-06-04 23:48:13
--> 
# 66.加一

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

https://github.com/leetcode-pp/91alg-1/issues/1#issuecomment-636581894

### 思路

js可以把数组合并成字符串加一再拆分成数组的方法，但是因为数字是有最大安全整数（9007199254740991(2^53-1)）这个概念的，超出这个数精度就会丢失；使用BigInt，应用程序不再需要变通方法或库来安全地表示Number.MAX_SAFE_INTEGER和Number.Min_SAFE_INTEGER之外的整数。 现在可以在标准JS中执行对大整数的算术运算，而不会有精度损失的风险。所以这里的思路是把数组合成的字符串转成BigInt类型再加一，再把结果转换成数组


### 代码
```
js
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
    var num = BigInt(digits.join('')) + 1n;
    return (num + '').split('');
};
```

### 参考答案

https://github.com/leetcode-pp/91alg-1/issues/1#issuecomment-636883697

_Originally posted by @chtTina in https://github.com/leetcode-pp/91alg-1/issues/1#issuecomment-636581894_