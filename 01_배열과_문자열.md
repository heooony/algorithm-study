# 01 배열과 문자열
## Hash Table
효율적인 탐색을 위한 자료구조로, (Key, Value)에 대응되는 구조.
해시테이블을 구성하는 방식은 연결리스트와 해시코드 함수 두 가지만 있으면 된다.

값을 해시테이블에 넣을 때에는 다음의 과정을 거친다.

1. 키의 해시코드를 계산, 키의 자료형은 보통 int 혹은 long이 된다. 키의 개수는 무한하지만, int의 개수는 유한하기 때문에 서로 다른 두 개의 키가 같은 해시코드를 가리킬 수 있음

2. hash(key) % array_length의 방식으로 해시 코드를 이용해 배열의 인덱스를 구함.

3. 각 인덱스에는 키와 값으로 이루어진 연결리스트가 존재하기에 키와 값을 해당 인덱스에 저장. 충돌에 대비하여 반드시 연결리스트를 이용해야 함

## ArrayList와 가변 크기 배열
특정 언어에서 배열의 크기를 자동으로 조절할 쑤 있다. 데이터를 덧붙일 때마다 배열 혹은 리스트의 크기가 증가하며, 동적 가변 크기 기능이 내재되어 있는 배열과 비슷한 자료구조를 원할 때에는 보통 ArrayList를 사용한다. 이는 필요에 따라 크기를 변화시킬 수 있으면서도 O(1)의 접근 시간을 유지한다. 통상적으로 배열이 가득차는 순간 배열의 크기를 두 배로 늘린다.
```java
ArrayList merge(Stirng[] words, String[] more) {
    ArrayList sentence = new ArrayList();
    for (String w : words) sentence.add(2);
    for (String w : moew) sentence.add(2);
    return sentence;
}
```
## StringBuilder
문자열의 리스트가 주어졌을 때 이 문자열들을 하나로 이어 붙이려고 한다. 이때의 수행 시간은 상황에 따라 다르겠지만 O(xn^2)가 된다. StringBuilder는 이 복잡한 시간을 단순하게 가변 크기 배열을 이용하여 해결을 해준다.
```java
Stirng joinWords(String[] words) {
    StringBuilder sentence = new StringBuilder();
    for (String w : words) {
        sentence.append(w);
    }
    return sentence.toString();
}
```

오늘은 이 세 가지에 대해 문자열, 배열, 일반적인 자료구조를 연습해 보도록 한다.

---

> 1. 중복이 없는가: 문자열이 주어졌을 때, 이 문자열에 같은 문자가 중복되어 등장하는지 확인하는 알고리즘을 작성하라. 자료구조를 추가로 사용하지 않고 풀 수 있는 알고리즘 또한 고민하라.
```java
public class Test {
    public static void main(String[] args) {
        String sentence = "abcdefg";
        ArrayList sentenceList = new ArrayList();
        for(int i = 0; i < sentence.length(); i++) {
            for(int j = 0; j < sentenceList.size(); j++) {
                if(sentenceList.get(j).equals(sentence.charAt(i))) {
                    System.out.println("중복 발생");
                    break;
                }
            }
            sentenceList.add(sentence.charAt(i));
        }
    }
}
```

책의 해설
```java
package com.example.demo.config;

public class Test {
    public static void main(String[] args) {
        isUniqueChars("test");
    }
    
    public static boolean isUniqueChars(String str) {
        if(str.length() > 128) return false;
        boolean[] char_set = new boolean[128];
        for(int i = 0; i < str.length(); i++) {
            int val = str.charAt(i);
            if(char_set[val]) {
                return false;
            }
            char_set[val] = true;
        }
        return true;
    }
}
```

> 2. 순열 확인: 문자열 두 개가 주어졌을 때 이 둘이 서로 순열 관계에 있는지 확인하는 메서드를 작성하라.

> 3. URL화: 문자열에 들어 있는 모든 공백을 '%20'으로 바꿔 주는 메서드를 작성하라. 최종적으로 모든 문자를 다 담을 수 있을 만큼 충분한 공간이 이미 확보되어 있으며 문자열의 최종 길이가 함께 주어진다고 가정해도 된다(자바로 구현한다면 배열 안에서 작업할 수 있도록 문자 배열을 이용하길 바란다).
입력 : "Mr John Smith", 13
출력 : "Mr%20John%20Smith"

