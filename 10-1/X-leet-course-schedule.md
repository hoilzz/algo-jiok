# 강의 스케줄

[leet course schedule](https://leetcode.com/problems/course-schedule/)

소요시간: 1H 30m
해결여부: O
또 풀어볼 가치가 있는가: O

N개의 강의가 있고, 이 강의는 먼저 들어야할 강의가 있다. 즉, 어떤 강의를 들으려면 먼저 들어야 하는 강의가 있다.
input은 다음과 같다.

```
3, [[0,1],[0,2],[1,2]]
```

[강의 번호, 선수 강의 번호]

위와 같이 input이 주어질 때, 강의를 전부 수강가능할지 boolean값을 리턴하면된다.

강의를 전부 못 듣는 케이스는 다음과 같다.

왜냐하면 0을 들으려면 1을 들어야하고, 1을 들으려면 0을.. 들어야한다.

```
2 [[0,1], [1,0]]
```

**해결해보자**

안되는 케이스를 보고 떠오른건 순환이 발생하는 것이다.

왠지 문제 자체는 cycle이 발생여부에 대해 묻는거 같다.

그래서 각 디펜던시(2번째 인풋)에 대해 그래프를 떠올렸다.

**그래프를 모든 강의에 대해 탐색(DFS)하며, 사이클이 발생하는지 파악하면된다.**

그래프 탐색은 시작점만 설정해주고, 시작점에 대해 디펜던시가 있다면 탐색 진행을 계속 하면된다.

이 때, 사이클 발생여부는 해당 노드 방문 여부로 따진다. 왜냐하면 탐색 중에 한번 방문한곳을 또 방문하면 왕복이 가능 즉, 사이클이 있다는 뜻이다.

```js
var courseGraph;

function getIsCycle(start, isVisited) {
  if (isVisited[start]) {
    return true;
  }

  isVisited[start] = true;

  for (var i = 0; i < courseGraph[start].length; i++) {
    if (getIsCycle(courseGraph[start][i], isVisited)) return true;
    // IMPORTANT: DFS로 탐색하며 조사하고(리커시브 호출) 방문여부를 초기화해준다.
    // 왜냐하면 탐색을 다 마치고 돌아왔기 때문이다.
    isVisited[courseGraph[start][i]] = false;
  }
  return false;
}

var canFinish = function(numCourses, prerequisites) {
  var preCourses = prerequisites;

  courseGraph = new Array(numCourses).fill().map(() => []);

  for (var i = 0; i < preCourses.length; i++) {
    courseGraph[preCourses[i][0]].push(preCourses[i][1]);
  }

  for (i = 0; i < numCourses; i++) {
    var isVisited = new Array(numCourses).fill(false);
    if (getIsCycle(i, isVisited)) {
      return false;
    }
  }

  return true;
};
```

## 나를 힘들게 한거

- 해결방법은 찾았는데, 그래프 탐색시 방문여부 초기화를 생각하지 못해서 너무 오래걸렸다.

## 리빙 포인트

- 그래프 탐색시(DFS, BFS) 특정 노드에서 갈 수 있는 곳을 배열로 관리한다.
- 그래서 특정노드의 갈 수 있는 경로들을 반복문을 통해 전부 반복한다.
- 이 때 사이클 탐지를 해야한다면, 방문여부[전체노드수]로 해야하는데
- 리커시브하게 특정 노드를 방문하고 나서, 방문여부[특정노드번호] = false 초기화 해주자.
