# 섬 개수 출력하기

[num of islands](https://leetcode.com/problems/number-of-islands/)

소요시간: 40m
해결여부: O
또 풀어볼 가치가 있는가: O

**해결해보자**

```
Input: grid[i][j]
11110
11010
11000
00000

Output: 1
```

연결된 섬이 몇개인지 구하는거.
'연결된'의 기준은 좌우상하(대각선제외)이다.

모든 경로를 탐색하며 다음 과정을 거쳐야 한다.

1. 방문한적 있니?

- Y: break;
- N: 2번으로

2. `grid[i][j]`가 섬('1') 이면

- Y: answer += 1; **방문시작**
- N: break;

방문함수

- 재귀적으로 함수를 호출하여 다음 case일 경우 함수 종료한다.
- base case
  - 경로 벗어남
  - 이미 방문
  - 섬이 아닌 경우: 섬이 아닌데 방문 함수 재귀호출할 필요가 없다.

## 나를 힘들게 한거

- 위 설계대로 했는데 시간이 오래걸린 이유는
- base case를 정의하는데 오래걸렸다.

## 리빙 포인트

- 2차원 배열 만들기

```js
const isVisited = new Array(rowLength)
  .fill()
  .map(() => new Array(colLength).fill(false));
```
