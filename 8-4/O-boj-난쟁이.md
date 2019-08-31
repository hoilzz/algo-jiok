# 7난쟁이

[7난](https://www.acmicpc.net/problem/2309)

소요시간: 30m
해결여부: O
또 풀어볼 가치가 있는가: x

9개의 값이 주어지는데 이 중 7개를 선택하여 합이 100이 되는 수들을 오름차순 출력.

**해결해보자**

오름차순 출력 위해 리스트들 오름차순 정렬.

9개의 값중 7개를 선택해야해서 9C7은 되게 작은 수니까 걍 하면 되겠구나 했는데..
9C7에 대한 모든 경우의수를 코드로 작성하자니 머리가 안돌아감.

그래서
각 숫자에 대해 선택/미선택에 대해 함수를 호출하며 합이 100이면서 고른 숫자의 개수가 7일 때 고른 숫자 리스트 출력하고자 함.(문제의 조건은 9개 숫자중 7개 선택시 무조건 합이 100이되는 숫자들이 있다.)

이걸 전부 다, 끝까지 (n개까지) 호출하면 비효율적이기 때문에, 재귀함수에서 조건에 안맞는 얘들은 일찍 리턴하여 함수 종료했다.

```C
int candidate[10];
int n = 9;
void goSum(int index, vector<int> selected, int sum) {
    if(selected.size() == 7 && sum == 100) {
        for(int i = 0; i<selected.size(); i++) {
            cout<<selected[i]<<endl;

        }
        exit(0);
        return;
    }

    if(index >= n || selected.size() >= 7) {
        return;
    }

    goSum(index + 1, selected, sum);
    selected.push_back(candidate[index]);
    goSum(index + 1, selected, sum + candidate[index]);
    // 처음에 선택된 숫자 제거 안해줘서.. 계속 틀렸다..
    // selected는 포인터니까 값이 계속 유지되기 때문에, 함수 수행 후 요 라인에 들어왔을 때 선택된 얘를 빼줘야한다.
    selected.pop_back();
}

int main(int argc, const char * argv[]) {

    for(int i = 0; i<n; i++) {
        cin>>candidate[i];
    }

    sort(candidate, candidate + 9);
    vector<int> selected;

    goSum(0, selected, 0);


    return 0;
}
```

## 리빙 포인트

- 모든 경우의 수를 구할 때, 참조값을 이용할 경우
  - 어떤 경우의 수가 답이 아니어서 재귀함수 호출 후 돌아왔을 때, 반영된 경우의 수를 참조값에서 제거 및 초기화해주자.
