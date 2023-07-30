## :round_pushpin: 정렬 - K번째수

***

<br>

### :pushpin: 코드

```java
import java.util.*;

class Solution {
    public List<Integer> solution(int[] array, int[][] commands) {
        List<Integer> answer = new ArrayList<Integer>(commands.length);
        
        for(int[] elem : commands){
            int[] temp = array.clone();
            Arrays.sort(temp, elem[0]-1, elem[1]);
            answer.add(temp[(elem[0])-1 + (elem[2])-1]);
        }
        return answer;
    }
}
```

<br>

