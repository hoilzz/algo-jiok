# longest palindrome

[leet longest palindrome](https://leetcode.com/problems/longest-palindromic-substring/)

소요시간: 1H
해결여부: O
또 풀어볼 가치가 있는가: O

문자열이 주어지고, 가장 긴 팰린드롬 찾는 문제다.

**해결해보자**

먼저, 팰린드롬을 찾기 위해서 모든 문자열을 하나하나 검사해야한다.

badab가 있다고 하자.

팰린 드롬을 찾으려면 0번째 인덱스부터(b) 하나씩 쌍이 맞는지 비교하면된다.

이 때 비교 방법은

1. 마지막 인덱스 ~ 시작 인덱스
2. 시작 인덱스 ~ 마지막 인덱스

이런 방식으로 0~n까지 비교하며 팰린드롬을 찾아가면 된다.
0~n까지 진행하며 비교한적 있는 인덱스들을 또 검사하게 되는데, 메모이징으로 해결하면 된다.

메모이징을 이용하려면 2번 방법보다는 1번이 낫다.
왜냐하면, 해당 인덱스 아래로는 더이상 팰린드롬이 아닌데 굳이 또 연산할 필요가 없기 때문인데, 이 점을 2번 방법으로는 이용할 수 없다.

```js
var memo;

function recurse(s, e, str) {
  if (s >= e) return true;

  if (memo[s][e]) {
    return memo[s][e];
  } else if (memo[s][e] === false) {
    return memo[s][e];
  }

  memo[s][e] = str[s] === str[e] ? recurse(s + 1, e - 1, str) : false;
  return memo[s][e];
}

var longestPalindrome = function(s) {
  if (!s) return '';

  memo = new Array(s.length).fill().map(() => new Array(s.length).fill());

  var answer = s[0];

  for (var i = 0; i < s.length; i++) {
    var newAnswer = '';

    for (var j = s.length - 1; j > i; j--) {
      var result = false;
      if (s[i] === s[j]) {
        var result = recurse(i + 1, j - 1, s);
      }
      if (result) {
        newAnswer = s.slice(i, j + 1);
      }
      if (newAnswer.length > answer.length) {
        answer = newAnswer;
      }
    }
  }
  return answer;
};
```

## 나를 힘들게 한거

- 메모이징할 때, 팰린드롬 false인 경우만 저장을 했다.
- 팰린드롬 true인 경우도 연산 횟수를 줄여준다고 생각을 못했다.
  - 왜냐하면 팰린드롬 발견시 바로 리턴하니까 라고 혼자 상상해서.. 요 문제는 **가장긴** 팰린드롬을 구하는건데..
  - 문제의 주어진 요구사항을 잊지말자..
