# 암호 만들기

[암호 만들기](https://www.acmicpc.net/problem/1759)

소요시간: 1H
해결여부: O
또 풀어볼 가치가 있는가: O

암호는 L개의 알파벳으로 구성되어있고 최소 한 개의 모음과 최소 두 개의 자음으로 구성되어있다.
이 때 비번은 정렬된 알파벳이다.

암호에 사용됐을 법한 문자의 종류는 C가지가 있다고 하자. (3<=L<=C<=15)

위 조건을 만족하는 알파벳을 사전순으로 모두 출력하자.

**해결해보자**

걍 브루트포스다.
모든 경우의수를 구해서 조건에 맞는 것만 출력해주면된다.

```C
int totalLen;

bool isValid(string str) {
    bool isMo = false;
    int cntJa = 0;
    for(int i = 0; i<str.length(); i++) {

        char ch = str[i];

        if(ch == 'a' || ch =='e' || ch =='i' ||ch=='o' || ch == 'u') {
            isMo = true;
        } else {
            cntJa += 1;
        }

        if(isMo && cntJa >= 2) {
            return true;
        }
    }
    return false;

}

void printValidStr(int index, int pwLen, string currentPw, string str) {
    if(index >= totalLen) {
        return;
    }
    if(currentPw.length() == pwLen) {
        if(isValid(currentPw)) {
            cout<<currentPw<<endl;
        }

        return;
    }

    printValidStr(index + 1, pwLen, currentPw + str[index + 1], str);
    printValidStr(index + 1, pwLen, currentPw, str);
}

int main(int argc, const char * argv[]) {

    int pwLen;
    char str[16];
    cin>>pwLen>>totalLen;

    for(int i = 0; i<totalLen; i++) {
        cin>>str[i];
    }

    string tempStr(str);

    sort(tempStr.begin(), tempStr.end());

    printValidStr(-1, pwLen, "", tempStr);

    return 0;
}
```

## 나를 힘들게 한거

브루트포스인줄을 알았는데 문자열을 모든 경우의수를 나타내기 위해 문자열을 어떻게 선택할지 몰랐다.
for문을 어떻게 돌릴지 계속 고민하다가 답이 안나와서.. 떠오른게 문자 하나씩 선택하며 재귀를 돌면서 basecase에서 재귀 종료하도록 작성했다.
