## :round_pushpin: 해시 - 완주하지 못한 선수

***

<br>



### :pushpin: 조건

- 단 한명의 선수를 제외하고는 모든 선수가 마라톤을 완주했다.
- 완주자는 참가자보다 1 작다.
- 모든 이름은 알파벳 소문자로 이루어져 있다.
- 참가자 중에는 동명이인이 있다.



<br>

### :pushpin: 코드

```java
import java.util.Map;
import java.util.HashMap;

class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        HashMap<String, Integer> participant_maps = new HashMap<String, Integer>(participant.length);
        
        for(String element : participant){
            if(participant_maps.containsKey(element)){
                participant_maps.put(element, participant_maps.get(element)+1);
            }
            else{
                participant_maps.put(element, 1);
            }
        }
        for(String element : completion){
            participant_maps.put(element, participant_maps.get(element)-1);
        }
        
        for(HashMap.Entry<String, Integer> entry : participant_maps.entrySet()){
            if(entry.getValue() > 0){
                answer = entry.getKey();
                return answer;
            }    
        }
        return answer;
    }
}
```

