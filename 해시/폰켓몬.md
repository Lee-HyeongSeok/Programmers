## :round_pushpin: 해시 - 폰켓몬

***

<br>



### :pushpin: 조건

- 사용자는 연구실에 있는 총 N 마리의 폰켓몬 중에서 N/2 마리를 가져갈 수 있다.
- 같은 종류의 폰켓몬은 같은 번호를 가질 수 있다.
- M/2 마리의 폰켓몬을 선택하는 방법중, 최대한 많은 종류의 폰켓몬을 가져가야 한다.



<br>

### :pushpin: 코드

```java
import java.util.HashSet;
import java.util.Arrays;

class Solution {
    public int selectCase(int[] nums){
        int selectionThreshold = nums.length/2; // 사용자가 가질 수 있는 폰켓몬 개수
        int caseOfNums=0;
        
        HashSet<Integer> tempList = new HashSet<Integer>(nums.length);
        
        for(int value : nums){ tempList.add(value); }
        caseOfNums = tempList.size();
        
        // 사용자가 가질 수 있는 최대 개수를 넘지 않도록 리턴
        // 만약 배열의 총 길이가 6개인데, 중복을 제거한 집합이 [3, 2, 4, 5] 라면
        // 최대 가질 수 있는 종류는 3개이지만, 종류는 4개인 상태
        // 여기서 4개의 종류 중 3종류만 가지면 되므로 사용자가 가질 수 있는 최대 종류를 반환
        // 반대로 배열의 총 길이가 6개인데, 중복을 제거한 집합이 [3, 2] 라면
        // 최대 가질 수 있는 종류는 3개이지만, 종류는 2개인 상태
        // 여기서 3개의 종류를 가질 수 있지만 2개의 종류를 선택해야 하는 상태가 되므로 집합에서 나올 수 있는
        // 최대 종류의 개수를 반환
        return selectionThreshold > caseOfNums ? caseOfNums : selectionThreshold;
    }
    public int solution(int[] nums) {
        int answer = 0;
        answer = selectCase(nums);

        return answer;
    }
}
```

