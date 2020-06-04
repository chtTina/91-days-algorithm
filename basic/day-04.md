# 394.字符串解码

## 题目描述

```
给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

示例:

s = "3[a]2[bc]", 返回 "aaabcbc".
s = "3[a2[c]]", 返回 "accaccacc".
s = "2[abc]3[cd]ef", 返回 "abcabccdcdcdef".

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/decode-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

## 我的回答

https://github.com/leetcode-pp/91alg-1/issues/20#issuecomment-638928819

### 思路

1. 定义一个数组用来存放处理s字符串；
2. 遍历s字符串；
3. s[i]遇到不为']'，判断是否为数字
    * 如果为数字，定义一个临时字符串，循环到不为数字并把所有数拼接，再把当前字符串数字塞入result数组；
    * 如果不为数字，直接把该字符push到result数组；
4. s[i]遇到']'，从result尾部开始遍历不为'['用一个str存起来，当为'['把result的'['pop出来，再把result.pop一次得到数字，
    调用repeat的函数把对应的相加，再把处理好的push到result里；
5. 最后把result数组转成字符串返回即可；

### 代码
```js
    /**
     * @param {string} s
     * @return {string}
     */

    var decodeString = function(s) {
      let result = [];
      let res = '';
      
      for(let i = 0; i < s.length; i++){
        if(s[i] !== ']'){
          if(parseInt(s[i])){
            let num = '';
            while(!isNaN(parseInt(s[i]))){
              num += s[i];
              i++;
            }
            result.push(num);
            i--;
          }else{
            result.push(s[i]);
          }
        }else if(s[i] == ']'){
          let j = result.length - 1;
          let str = [];
          while(result[j] !== '['){
            str.push(result.pop());
            j--;
          }
          result.pop();
          
          let num = parseInt(result.pop());

          result.push(repeat(str.reverse().join(''), num));
        }
      }
      res = result.join('');
      return res;
    };



    function repeat(string, num){
      let res = '';
      for(let i = 0; i < num; i++){
        res += string
      }

      return res;
    }

    console.log(decodeString("3[a]2[bc]"))
    console.log(decodeString("3[a2[c]]"))
    console.log(decodeString("2[abc]3[cd]ef"))
    console.log(decodeString("100[leetcode]") )
    console.log(decodeString("3[z]2[2[y]pq4[2[jk]e1[f]]]ef"))

```

### 参考答案

https://github.com/leetcode-pp/91alg-1/issues/20#issuecomment-638800071


_Originally posted by @chtTina in https://github.com/leetcode-pp/91alg-1/issues/20#issuecomment-638928819_