# 가장 긴 부분 팰린드롬 찾기

[longest-palindrome](https://leetcode.com/problems/longest-palindromic-substring/)

소요시간: 1H
해결여부: O
또 풀어볼 가치가 있는가: O.. leet코드에서 js환경 적응할겸 다른 풀이 방법으로 해결해볼겸..

**해결해보자**

팰린드롬은 너무나 유명한 DP문제라.. DP로 풀려고함.

일단 전체케이스를 조사해야한다. 그래서 시작점과 끝점을 정해서 반복문을 돌아야한다.

(0,k(=length)-1) / (0, k-2) / (0, k-3) (k>=시작점)

위 과정에서 문자를 비교하며 k가 length - 1될 때까지 반복한다.
이걸 그대로 제출하면 시간초과가 난다.

기존에 비교한 위치를 다른 케이스를 조사하면서 또 조사하는 불필요한 연산을 한다.
메모이징 해주자.

```js
// const memo = new Array(1000).fill().map(() => new Array(1000).fill());

function checkleehyolee(str, s, e, memo) {
  if (s >= e) {
    return true;
  }
  if (memo[s][e]) {
    return true;
  } else if (memo[s][e] === false) {
    return false;
  }

  if (str[s] === str[e]) {
    memo[s][e] = checkleehyolee(str, s + 1, e - 1, memo);
    return memo[s][e];
  } else {
    memo[s][e] = false;
    return memo[s][e];
  }
}
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
  const memo = new Array(1000).fill().map(() => new Array(1000).fill());

  const len = s.length;
  let answerIndex = [-1, -1];

  for (let i = 0; i < len - 1; i++) {
    for (let j = len - 1; j > i; j--) {
      let isAnswer = checkleehyolee(s, i, j, memo);

      if (isAnswer) {
        const prevAnswerLen = answerIndex[1] - answerIndex[0];
        const currentAnswerLen = j - i;

        if (currentAnswerLen > prevAnswerLen) {
          answerIndex = [i, j];
        }
      }
    }
  }
  return s.substr(answerIndex[0], answerIndex[1] - answerIndex[0] + 1);
};
```

---

**다른 사람 풀이**

더 쉽고 명확하다.

바텀업으로 각 길이 별로 팰린드롬을 구하면서 가장긴 팰린드롬을 찾는 방식이다.

```js
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
  let answer;

  const memo = new Array(1000).fill().map(() => new Array(1000).fill());

  const last = s.length - 1;
  for (let i = 0; i <= last; i++) {
    for (let j = 0; j + i <= last; j++) {
      if (i == 0 || (i == 1 && s[i] == s[j])) {
        memo[j][j + i] = true;
      } else {
        if (memo[j + 1][j + i - 1] && s[j] == s[i]) {
          memo[j][j + i] = true;
        }
      }
      if (memo[j][j + i]) {
        const candidate = i;
        if (!answer || candidate > answer[1] - answer[0]) {
          answer = [j, j + i];
        }
      }
    }
  }
  return s.substr(answer[0], answer[1]);
};
```

## 나를 힘들게 한거

- 이 문장이 이해가 안갔다.

## 리빙 포인트

- 릿코드에서 js의 코드 에디터 부분은 함수 스코프가 아니다.. 전역 스코프다. 당연히 함수 스코프일줄 알았는데.. memo값이 말도 안되게 저장되서.. 디버그 찍어봤더니.. 전역에 있는 memo가 초기화되지않고 재활용 되고 있었다.
