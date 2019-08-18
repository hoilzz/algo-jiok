# 스티커

[스티커](https://www.acmicpc.net/problem/9465)

소요시간: 1h 30m
해결여부: X
또 풀어볼 가치가 있는가: O

---

점화식을 찾아내기 위해 0번 index부터 조건에 맞게 최대값을 구하면서 나아감.

3번째 인덱스에서 최대값 구할 때, 다음과 같은 경우의 수를 발견함.

```C
// N은 입력받은 열의 길이.
memo[2][N];

sIndex = 0;
rIndex = 1; // sIndex와 겹치지 않기 위해 선언한 변수

memo[sIndex][i] = memo[rIndex][i-1];    // case 1
memo[sIndex][i] = max(memo[sIndex][i], memo[0][i-2]); // case 2
memo[sIndex][i] = max(memo[sIndex][i], memo[1][i-2]); // case 3

memo[sIndex][i] += arr[sIndex][i];
```

_case 1_
X O
O X

_case 2_
O X O
X X X

_case 3_
X X O
O X X

이케하면 예제는 맞는데.. 제출하면 틀린다.

최대값을 구할 수 있는 경우의수에서 뭔가 빠진 케이스가 있다는건데..

**해결해보자**

문제의 조건에 따르면, 1개 아이템을 선택하면 상하좌우 아이템을 선택하지 못한다.
위 케이스는 현재 아이템을 선택했을 경우의 케이스만 포함한다.

1가지 빠뜨린게 있는데, 최대값은 `memo[sIndex][i-1]`에서 나올 수 있다. 왜냐하면 현재 열의 스티커를 선택하지 않고 그 앞열에 최대크기의 값이 있을 수 있기 때문이다.

## 나를 힘들게 한거

- 이 문장이 이해가 안갔다.

## 리빙 포인트

- 이걸 알아두면 담에 시간이 절약될 거 같다.
