# 중복 문자 없는 가장 긴 섭스트링

[알고 사이트 문제 링크](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

소요시간: 10m
해결여부: O
또 풀어볼 가치가 있는가: X

**해결해보자**

걍 0~n까지 문자 하나씩 검사하면서 중복 발생하기 전까지 count 올리면서 진행한다.
n까지 반복문 진행하며 count를 비교하며 최대값만 리턴한다.

```js
var lengthOfLongestSubstring = function(s) {
  var memo = {};
  var ans = 0;

  for (var i = 0; i < s.length; i++) {
    memo[s[i]] = true;

    var idx = 1;

    for (var j = i + 1; j < s.length; j++) {
      if (memo[s[j]]) {
        break;
      }
      memo[s[j]] = true;
      idx += 1;
    }
    if (idx > ans) {
      ans = idx;
    }
    memo = {};
  }

  return ans;
};
```
