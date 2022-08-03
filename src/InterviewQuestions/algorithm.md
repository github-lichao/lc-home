### 求最长的公共字符串

### 只出现一次的数字

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素

```js
let num = [2,2,1]
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    // var a = [];
    // for(var i = 0; i< nums.length; i++){
    //     if(nums.indexOf(nums[i]) === nums.lastIndexOf(nums[i])){
    //         a.push(nums[i])
    //     }
    // }
    var a = 0;
    for(const i in nums){
      a ^= nums[i]
    }
    return a;
};
// 1
```

### 多数元素

返回出现次数最多的值

```js
let nums = [2,2,1,1,1,2,2];
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
  return nums.sort((a, b) => a - b)[Math.floor(nums.length / 2)];
};
// 2
```

### 最长公共前缀

直接拿第一个字符串来作为参考，因为既然是公共前缀，那所有字符串都应该有第一个字符串的字符
```js
let strs = ["flower","flow","flight"];
const longestCommonPrefix = function(strs) {
    let res = ''
    for(let i=0;i<strs[0].length;i++){
        for(let j=1;j<strs.length;j++){
            if(strs[j][i]!== strs[0][i]) return res
        }
        res+=strs[0][i]
    }
    return res
};
// fl
```

### 回文数
>回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

```js
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
  // 方法1
  if(x < 0 || (!(x % 10) && x) ) return false;
  let x1 = x, res = 0;
  while(x1){
    res = res * 10 + x1 % 10;
    x1 = Math.floor(x1 / 10);
  }
  return res == x;
  // 方法2
  // let y = x.toString().split('').reverse().join('');
  // return Number(y) === x
};
```