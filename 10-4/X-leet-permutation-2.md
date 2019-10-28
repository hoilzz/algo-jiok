# 순열2

[permutation ii](https://leetcode.com/problems/permutations-ii)

소요시간: 1H 10m
해결여부: O
또 풀어볼 가치가 있는가: O

보통 순열문제는 중복 숫자가 없다.
이건 중복 숫자가 있다.

**해결해보자**

모든 경우의 순열을 구한다.
이 때, 이미 추가된 순열을 해시테이블을 통해 관리한다. key는 물론 추가된 순열이다. 값은 boolean이다.

```js
var ans, res, hash, len;
var hashAns;

function dfs(num, nums) {
  if (num === len) {
    var tmp = res.map(function(item) {
      return item;
    });

    if (hashAns[tmp.toString()]) return;

    hashAns[tmp.toString()] = true;
    ans.push(tmp);
    return;
  }

  for (var i = 0; i < len; i++) {
    if (hash[i]) continue;
    hash[i] = true;
    res.push(nums[i]);
    dfs(num + 1, nums);
    hash[i] = false;
    res.pop();
  }
}

var permuteUnique = function(nums) {
  (len = nums.length), (ans = []), (res = []), (hash = []), (hashAns = []);

  dfs(0, nums);
  return ans;
};
```

## 나를 힘들게 한거

-

## 리빙 포인트

- 이걸 알아두면 담에 시간이 절약될 거 같다.
