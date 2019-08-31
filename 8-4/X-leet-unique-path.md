# unique path

[unique path](https://leetcode.com/problems/unique-paths/)

소요시간: 1h
해결여부: X
또 풀어볼 가치가 있는가: O

0,0에서 시작하여 m,n까지 오른쪽/아래 로만 이동할 수 있는 경우의 수 구하기.

---

첨에 걍 무식하게 다 구하려고함.
재귀함수로 오른쪽, 아래로 이동하며 도착 카운팅.

```C
int pathLength;
int m,n;
void moveOne(int row, int col) {
    if(row == n && col == m) {
        pathLength += 1;
        return;
    }
    if(row > n || col > m) {
        return;
    }

    moveOne(row, col + 1);
    moveOne(row + 1, col);
}

moveOne(1,1);
```

위 코드 제출시 시간초과 난다. 이유는,

방문했던 곳을 또 방문하는 경우가 생긴다.
문제에서 최대 (100,100) 크기의 2차원 배열이라고 주어졌다.

---

메모이징을 하려 했는데 컨셉을 잘못잡았다..

해당칸에서 m,n의 방문 여부를 판단하려 했다. 이렇게 되면 작은 문제로 큰 문제를 풀어가면서 메모이징할 수 있는 DP를 이용할 수 없다.

왜냐하면 우리는 목적지에 갈 수 있는 경우의수를 구하는 거니까..

모든 경우의 수를 구하는 거고, 점화식을 다시 생각해보면 쉽게 풀 수 있다.

**해결해보자**

`D[row][col]`을 (row,col) 까지 올 수 있는 경우의 수라고 해보자.

`D[row][col] = D[row-1][col] + D[row][col-1]` 이다.

이것을 0,0부터 1행 M열, 2행 M열까지 차례로 진행하면된다.

초기값은 (M,0) / (0,N) 은 전부 1이다.
왜냐하면 0,0까지 올 수 있는 경우의수는 1이고
0,1까지 올 수 있는 경우의 수도 1이다. 왜냐하면 왼쪽에서만 올 수 있고 위에서는 올 수 없기 때문이다.

```C
int memo[100][100];

class Solution {
public:
    int uniquePaths(int m, int n) {
        // moveOne(1,1, m, n);
        int memo[m][n];

        for(int i = 0; i<m; i++){
            for(int j = 0; j<n; j++) {
                if(i==0 || j==0) {
                    memo[i][j] = 1;
                    continue;
                }
                memo[i][j] = memo[i-1][j] + memo[i][j-1];
            }
        }

        return memo[m-1][n-1];
    }
};
```

## 나를 힘들게 한거

- 위와 같이 모든 경우의 수(특히 경로)는 브루트포스(DFS, BFS)거나 DP로 풀 수 있다.
- 주어지는 인풋의 공간복잡도가 보통 엄청 크기 때문에 DP로 메모이징 하면서 풀면 시간초과 없이 풀 수 있다.

## 리빙 포인트

- DP 같으면 특정 점화식으로 구하기 어려운 경우.. 점화식을 다시 세워보자..
