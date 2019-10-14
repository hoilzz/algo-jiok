# 카펫

[https://programmers.co.kr/learn/courses/30/lessons/42842?language=javascript](https://programmers.co.kr/learn/courses/30/lessons/42842?language=javascript)

소요시간: 30m
해결여부: O
또 풀어볼 가치가 있는가: X

카펫은 Red, Brown 영역으로 구성된 사각형(2차원 배열)이다.

Red와 Brown 개수만 주어지고 이 개수로 구성된 전체 카펫의 가로,세로 길이를 구해야한다.

**처음에 헷갈렸던거는**

Red영역이 사각형이 아니어도 되는가? 였는데 문제 내용에 없었고, 예시에도 없었다. (그래서 사각형이 아닌 경우도 구하다가 너무나 어려워서 일단 무조건 사각형이 경우만 생각하고 작성했다. 그래서 쉽게 맞았다. 또, Brown영역은 Red를 둘러싸고 길이가 1이다. 선분만 있는 큰 사각형이라고 가정.)

---

**해결해보자**

Red 영역이 사각형이면, 문제의 패턴은 1가지다.

Red영역을 (row,col) 길이를 가진 사각형이라고 하면
전체영역은 (row + 2, col + 2)다.

이것을 통해 다음 식을 구할 수 있다.

```
RedRow, RedCol 변수가 주어지면,
TotalRow = RedRow + 2;
TotalCol = RedCol + 2;

// if XXCount는 XX영역의 전체 타일 개수
RedCount = RedRow * RedCol;
TotalCount = TotalRow * TotalCol;

TotalCount = RedCount + BrownCount
TotalCount - RedCount = BrownCount
```

여튼 모든 경우의 수를 따지며 마지막 식이 일치하는 경우에 정답을 찾은거다.

---

이제 그럼 모든 경우의 수를 알아보자.

카펫의 영역이(Red든 Brown이든) 사각형이라고 가정했을 때,

row, col의 경우의 수는 타일의 총 개수를 2개의 약수로 나눠지는 경우의 수와 같다.
뭔말이냐하면 Red가 24개 일 때

```
if RedCount = 24

(1,24)
(2,12)
(3,8)
(4,6)
```

> 가장 큰 약수는 N을 제외한 N의 절반 크기, 요기까지만 경우의 수 구하면된다.

그래서 정리하면,

1. RedCount를 통해 `i*i<=RedCount`(i=1,2...)까지 RedCount의 약수를 구한다.

- 이 약수를 통해 (RedRow,RedCol)을 알 수 있다.
- totalRow,totalCol = (RedRow+2, RedCol+2)다. (사각형이고, Red를 길이가 1인 상태로 둘러싸고만 있을 때)

2. totalCount - redCount === brownCount 일 경우에 정답 리턴.

요것만 코드로 작성하면된다.

```js
function solution(brown, red) {
  for (var i = 1; i * i <= red; i++) {
    var row = i;

    if (red % row > 0) continue;

    var col = red / row;

    var totalRow = row + 2;
    var totalCol = col + 2;

    var totalCount = totalRow * totalCol;

    if (totalCount - red === brown) {
      return [totalCol, totalRow];
    }
  }
}
```

## 나를 힘들게 한거

- 없다. 문제를 내가 이해못했거나 문제가 잘못 나를 이해시켰거나,,
