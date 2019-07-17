# 136-singlenumber

소요시간 : 10m

[leetcode single number](https://leetcode.com/problems/single-number/)

배열에 숫자들이 있다. 숫자들 중에 1개를 제외하고 2번 나타난다.
1번만 나타난 숫자를 `O(n)` 안에 찾아라.

**해결해보자**

for-loop 한 바퀴만 돌 수 있다..

일단 **몇번 나타났는지 어떤 자료구조에 저장을 해야한다.**

불특정 숫자(key)가 몇번 나타났는지(value) 를 담기 위해 map형태의 자료구조만이 떠올랐다.

그리고 N번 회전 후에 기록만 하면, 값이 1인 key를 찾기 위해 N번 돌아야 한다

그래서 2번 나타났을 때 해당 키를 지워주면 1번만 나타난 key를 찾을 수 있다.

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
  const obj = {};
  nums.forEach(n => {
    if (!obj[n]) obj[n] = 1;
    else if (obj[n]) delete obj[n];
  });

  return Object.keys(obj)[0];
};
```
