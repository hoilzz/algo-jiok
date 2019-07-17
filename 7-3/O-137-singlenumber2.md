# 137 singlenumber 2

소요시간: 3m
해결여부: yyyy
또 풀어볼 가치가 있는가: nnnn

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
  const obj = {};
  nums.forEach(n => {
    if (!obj[n]) obj[n] = 1;
    else if (obj[n]) {
      if (obj[n] < 2) {
        obj[n] += 1;
      } else {
        delete obj[n];
      }
    }
  });

  return Object.keys(obj)[0];
};
```
