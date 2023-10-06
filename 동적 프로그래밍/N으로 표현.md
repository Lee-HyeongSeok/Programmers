## :round_pushpin: 동적 프로그래밍 - N으로 표현

***

사칙연산을 통해 number를 최소로 표현하는 N의 개수를 구하는 문제



- N을 최소 8번까지 사용 가능
- 우선 N을 1번 ~ 8번까지 사용해서 표현할 수 있는 집합을 먼저 생성
- 생성한 집합을 이용하여 사용할 수 있는 N의 개수로 또 다른 집합을 만드는게 핵심



### :pushpin: 초기 집합 생성

ex) N이 5라고 가정

- N을 1번 사용할 수 있는 경우
  - 1Set : 5
  - 2Set : 55
  - 3Set : 555
  - 4Set : 5555
  - 5Set : 55555
  - 6Set : 555555
  - 7Set : 5555555
  - 8Set : 55555555



### :pushpin: 초기 집합을 이용하여 사용할 수 있는 횟수에 따른 사칙연산 집합 생성

초기 집합은 표기하지 않겠음

- N을 1번 사용할 수 있는 경우
  - 5+5 (10)
  - 5-5 (0)
  - 5/5 (1)
  - 5*5 (25)
- N을 2번 사용할 수 있는 경우
  - 5+5+5 = 15
  - 5\*5\*5 = 125
  - 5-(5-5) = 5
  - 5/5/5 = 1

이를 합집합으로 표현한다면?

- N을 1번 사용할 수 있는 경우
  - 1Set
- N을 2번 사용할 수 있는 경우
  - 1Set + 1Set
- N을 3번..
  - 1Set + 2Set
  - 2Set + 1Set
- N을 4번...
  - 1Set + 3Set
  - 3Set + 1Set
  - 2Set + 2Set
- N을 5번..
  - 1Set + 4Set
  - 2Set + 3Set
  - 3Set + 2Set
  - 4Set + 1Set

결국, 이전에 구한 집합 결과로 다음 집합을 구하는 것



```c++
#include <iostream>
#include <string>
#include <vector>
#include <unordered_set>

using namespace std;

#define MAXN 8

vector<unordered_set<int>> memo(8);

void initSet(int N){
    int result = N;
    
    for(int i=1; i<8; ++i){
        result = (result*10)+N;
        memo[i].insert(result);
    }
}

int solution(int N, int number) {
    int answer = 0;
    
    if(N == number)
    {
        return 1;
    }
    
    memo[0].insert(N);
    initSet(N);
    
    for(int i=1; i<MAXN; ++i)
    {
        for(int j=0; j<i; ++j)
        {
            for(auto const& setX : memo[j])
            {
                for(auto const& setY : memo[i-j-1]) 
                {
                    memo[i].insert(setX + setY);
                    memo[i].insert(setX * setY);
                    
                    if(setX >= setY)
                    {
                        memo[i].insert(setX - setY);
                    }
                    
                    if(setY != 0)
                    {
                        memo[i].insert(setX / setY);
                    }
                }
            }
        }
        
        if(memo[i].find(number) != memo[i].end())
        {
            return i + 1;
        }
    }
    
    return -1;
}
```

