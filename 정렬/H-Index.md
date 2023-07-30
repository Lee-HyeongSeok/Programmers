## :round_pushpin: 정렬 - H-Index

***

<br>

### :pushpin: 코드

```java
import java.util.*;

class Solution {
    public int solution(int[] citations) {
        int N = citations.length;
        List<Integer> list = new ArrayList<Integer>(N);
        int answer = 0;
        
        for(int elem : citations){
            list.add(elem);
        }
        
        list.sort(new Comparator<Integer>(){
            public int compare(Integer s1, Integer s2){
                return s1-s2;
            }
        });
        
        int target=0, h_index=0, h=1;
        for(int i=0; i<N-1; i++){
            target = list.get(i);
            
            for(int j=i+1; j<N; j++){
                // h번 이상 인용된 논문 찾기
                if(target <= list.get(j)){
                    h++;
                }
            }
            if(target >= h && h >= N-h && h_index < h){
                h_index = h;
            }
            h = 1;
        }
        return h_index;
    }
}
```

<br>

