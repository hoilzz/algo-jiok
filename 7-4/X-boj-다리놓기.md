## 1010번 다리놓기

[다리놓기](https://www.acmicpc.net/problem/1010)

소요시간: 1h30m
해결여부: O
또 풀어볼 가치가 있는가: O, 왜냐하면 너무 오래걸려서 풀었다.

맞췄는데 1시간 반걸려서.. 다시 풀어보려고 한다.

오래걸린 이유는.. 풀이 방법을 Combination(조합)으로 풀면 되겠다라고 생각하고

다음과 같이 구현하였다.

```C
unsigned long long factorial(unsigned long long n, unsigned long long until) {
  unsigned long long result = 1;
  while(n>until) {
    result *= n;
    n--;
  }
  return result;
}

unsigned long long combination(unsigned long long n, unsigned long long r) {
  unsigned long long nFac = factorial(n, r);
  unsigned long long rFac = factorial(r, 0);
  return nFac / rFac;
}
```

n은 30!까지 표현되는데 이 값이 unsigned long long의 최대값을 벗어난다..

그래서 뭔가 재귀형태로 쪼개야될 거 같았는데.. 조합을 쪼개서 푸는 거에 대해 오래걸렸다.

---

**조합 DP로 풀기**

조합의 반복되는 작은 문제, 그 작은 문제를 통해 큰 문제를 풀 수 있는 패턴을 찾자.

1,2,3 3개의 숫자에서 2개를 고르자.

1,2 / 1,3
2,3

요렇게 나온다.

1,2,3,4 4개의 숫자에서 3개를 고르자.

1,2,3 / 1,2,4 / 1,3,4
2,3,4가 나온다.

**두가지 에시에서 첫번째 줄은**

1을 선택 후 나머지 숫자에서 2가지를 고르고 있다.

**두번째 줄은**

1을 선택하지 않고 나머지 숫자에서 3가지를 고르고 있다.

즉, 첫번째 예시는

3C2 = 2C1 + 2C2

두번째 예시는

4C3 = 3C2 + 3C3

---

nCr = (n-1)Cr-1 + (n-1)Cr 과 같은 점화식을 구할 수 있다.

```C
int combination(int n, int r) {
    if(n==r) {
        return 1;
    } else if(r==1) {
        return n;
    }
    return combination(n-1,r-1) + combination(n-1, r);
}

int main(int argc, const char * argv[]) {

    int n;
    cin>>n;

    for(int i = 0; i<n; i++) {
        int n, r;
        cin>>n>>r;
        cout<<combination(r, n)<<endl;
    }

    return 0;
}
```
