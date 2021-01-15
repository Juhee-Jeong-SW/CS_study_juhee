# [Java] Collection api

## 📌 Collection api

Java Collection 에는 `List`, `Map`, `Set` 인터페이스를 기준으로 여러 구현체가 존재한다. 이에 더해 `Stack`과 `Queue` 인터페이스도 존재한다. 왜 이러한 Collection 을 사용하는 것일까? 그 이유는 다수의 Data 를 다루는데 표준화된 클래스들을 제공해주기 때문에 DataStructure 를 직접 구현하지 않고 편하게 사용할 수 있기 때문이다. 또한 배열과 다르게 객체를 보관하기 위한 공간을 미리 정하지 않아도 되므로, 상황에 따라 객체의 수를 동적으로 정할 수 있다. 이는 프로그램의 공간적인 효율성 또한 높여준다.

- List`List` 인터페이스를 직접 `@Override`를 통해 사용자가 정의하여 사용할 수도 있으며, 대표적인 구현체로는 `ArrayList`가 존재한다. 이는 기존에 있었던 `Vector`를 개선한 것이다. 이외에도 `LinkedList` 등의 구현체가 있다.
- Map대표적인 구현체로 `HashMap`이 존재한다. (밑에서 살펴볼 멀티스레드 환경에서의 개발 부분에서 HashTable 과의 차이점에 대해 살펴본다.) key-value 의 구조로 이루어져 있으며 Map 에 대한 구체적인 내용은 DataStructure 부분의 hashtable 과 일치한다. key 를 기준으로 중복된 값을 저장하지 않으며 순서를 보장하지 않는다. key 에 대해서 순서를 보장하기 위해서는 `LinkedHashMap`을 사용한다.
- Set대표적인 구현체로 `HashSet`이 존재한다. `value`에 대해서 중복된 값을 저장하지 않는다. 사실 Set 자료구조는 Map 의 key-value 구조에서 key 대신에 value 가 들어가 value 를 key 로 하는 자료구조일 뿐이다. 마찬가지로 순서를 보장하지 않으며 순서를 보장해주기 위해서는 `LinkedHashSet`을 사용한다.
- Stack 과 Queue`Stack` 객체는 직접 `new` 키워드로 사용할 수 있으며, `Queue` 인터페이스는 JDK 1.5 부터 `LinkedList`에 `new` 키워드를 적용하여 사용할 수 있다. 자세한 부분은 DataStructure 부분의 설명을 참고하면 된다.

### 리스트

List 인터페이스는 Collection 인터페이스를 상속한다. 리스트자료 구조는 삽입 순서(Insertion order)가 유지되며, 동기화 미지원(Non synchronized) 이라는 공통점을 가진다. 또한 리스트는 중복 값을 포함할 수 있고, 복수의 Null 값을 포함할 수 있다. 아래에서 List 인터페이스를 구현하는 ArrayList와 LinkedList에 대해 다루겠다.

------

**구조**

![https://blog.kakaocdn.net/dn/DMaAd/btqzktoEmDr/op3q4Js38nwxR0Jsp6twmk/img.jpg](https://blog.kakaocdn.net/dn/DMaAd/btqzktoEmDr/op3q4Js38nwxR0Jsp6twmk/img.jpg)

어레이 리스트와 연결 리스트의 메모리 할당 구조

어레이 리스트는 RandomAccess 마커 인터페이스를 상속하여 구현된다. 모든 원소는 각자의 인덱스와 실제 데이터 값을 가진다. 이 인덱스를 가지고 해당 데이터로 바로 접근할 수 있다. 그러므로 Get 오퍼레이션 시의 시간 복잡도는 O(1)이 된다.

연결 리스트는 노드값이외에 앞 뒤 포인터 값을 저장하고 있는 자료구조이며, 랜덤 접근(Random Access)이 아닌 순차 접근(Sequential Access) 방식을 따르므로 어레이 리스트처럼 바로 해당 데이터로 접근할 수가 없다. 위의 그림에서 연결 리스트의 가장 말단에 저장된 데이터를 조회하려고 할 때에는 순차적으로 노드의 다음 값을 따라가며 0, 1, 2, 3번째를 거쳐 4번째에서야 해당 데이터를 조회하게 된다. 리스트의 저장 개수인 n에 비례하여 조회해야 하는 데이터 개수도 늘어나게 된다. 따라서 Get 오퍼레이션 시 시간 복잡도는 O(n)이 된다.

**메모리 점유율 면에서는 어레이 리스트가 연결 리스트보다 더 효율적**이다. 어레이 리스트는 실제 데이터와 인덱스만 저장하는 반면, 연결 리스트의 각각의 노드는 데이터와 앞 뒤의 원소의 포인터값까지 저장함으로써 더 많은 메모리를 점유하기 때문이다.

![https://blog.kakaocdn.net/dn/b6wnl3/btqzk67n3Du/vcSXAqP8ReG7kQewouloF1/img.jpg](https://blog.kakaocdn.net/dn/b6wnl3/btqzk67n3Du/vcSXAqP8ReG7kQewouloF1/img.jpg)

어레이 리스트와 연결 리스트 삽입/삭제 오퍼레이션 시간복잡도

어레이 리스트는 인덱스가 순차적으로 존재해야하는 구조 특성상, 한 원소를 삽입/삭제 시 배열의 나머지 원소들의 인덱스 참조값을 수정해야 하게 된다. 따라서 추가/삭제 오퍼레이션의 시간 복잡도는 O(n)이 된다. 위의 그림의 어레이 리스트 배열을 보자.  총 6개의 인덱스를 가지던 배열에서 3번 원소를 삭제하면, 4, 5, 6번째 원소는 각각 3, 4, 5번으로 수정되어야 하므로 한 칸씩 당겨진다.

연결 리스트는 노드값이외에 앞 뒤 포인터 값을 저장하고 있는 자료구조이므로, 삭제와 삽입시 해당 노드 앞 뒤의 포인터 값만 수정하여주면 추가/삭제가 완료된다. 따라서 시간 복잡도는 전체 데이터 수에 종속되지 않으므로 O(1)이다. 물론 삭제, 추가할 위치를 알고 있다는 가정하의 효율값이고 모른다면 검색이 필요하므로 시간 복잡도는 O(n)이 된다. (그러나 보통 알고 있다고 가정하여 O(1)으로 정의한다.)

------

**성능**

[제목 없음](https://www.notion.so/2379c41de46d4ff2819ef7476baabb3e)

------

**사용 용도**

데이터 조회가 자주 이루어질 때 ArrayList를 사용하는 것이 유리하다.

데이터의 삽입, 삭제가 빈번히 일어날 때 LinkedList를 사용하는 것이 유리하다.

------

# 셋

Set 인터페이스는 Collection 인터페이스를 상속한다. Set은 중복값을 허용하지 않는 선형 콜렉션으로, 이미 셋 안에 존재하는 값을 add() 메소드로 삽입하려고 시도하면 False 값을 리턴시킨다. Set에서 인덱스를 이용한 랜덤 접근은 불가하지만, 원소의 정렬 순서는 Set의 구현방법에 따라 유지될 수도 있고, 유지되지 않을 수도 있다.

------

**구조**

해쉬셋은 해시함수를 사용함으로써 뛰어난 성능을 보인다. 해시함수란, 어떤 가변 값의 key를 input으로 해시함수에 넣으면 output으로 고정된 hash값이 나오게 하는 것이다. 예를 들어, 내부 로직이 f(x)= x % 10 인 해시함수가 있다고 가정했을 때 84, 123, 27의 해쉬값은 각각 4, 3, 7이 되고, 이 해쉬값의 값에 따라 정렬하여 저장한다. 즉, 3:123, 4:84, 7:27의 순서대로 저장이 되게 된다.

![https://blog.kakaocdn.net/dn/olSrY/btqzklR2far/fDLyNQXhw5kqlIUlolwjaK/img.png](https://blog.kakaocdn.net/dn/olSrY/btqzklR2far/fDLyNQXhw5kqlIUlolwjaK/img.png)

해시함수에 의해 해시로 변환됨

그런데, input은 거의 무한대의 가변값인데 반해 hash는 고정값을 가지므로, 중복 hash값이 발생할 수 있다. 가령 위의 해시함수에 223이라는 값을 input으로 넣어도 123을 넣었을 때와 같은 hash값(3)을 얻게 된다. 이러한 현상을 해시 충돌(hash collision)이라고 하는데, 이때에는 동일한 해쉬값에 대해 LinkedList로 저장된다.

![https://blog.kakaocdn.net/dn/nQESZ/btqzkQX7Gmi/Sdrgofkb5PLBsgbPQwZm7k/img.png](https://blog.kakaocdn.net/dn/nQESZ/btqzkQX7Gmi/Sdrgofkb5PLBsgbPQwZm7k/img.png)

해시 충돌에 의해 88이 538 뒤에 저장되었다

트리셋은 이진 탐색 트리에 자료를 저장하는 자료구조이다.

![https://blog.kakaocdn.net/dn/bMQnOD/btqzkrYK0Jp/bpk90L4Btbnlfjms3g75a0/img.png](https://blog.kakaocdn.net/dn/bMQnOD/btqzkrYK0Jp/bpk90L4Btbnlfjms3g75a0/img.png)

Treeset: 이진 트리 구조

------

**성능**

[제목 없음](https://www.notion.so/6accf7ca8ae14094a20a75081a5ed039)

해쉬셋과 연결해쉬셋은 해쉬값으로 호출/삭제/삽입을 하므로 모든 연산에 있어 O(1)의 시간 효율성을 가진다.

트리셋은 이진 탐색 트리를 사용하므로, 검색/삽입/삭제의 시간 효율성은 log(n)을 가지게 된다.

------

**비교**

아래에서 Set 인터페이스를 구현하는 HashSet, Linked-HashSet, TreeSet을 비교한다.

[제목 없음](https://www.notion.so/1ea9f442a1754768a66a4a481fda88bf)

------

# 맵

맵은 (Key, Value) 페어 구조의 데이터를 저장할 때에 쓰이는 자료구조이다. Key 값이 유일값이라면 Value 값은 중복이 되어도 상관없다. 저장 순서는 Map의 구현 방법에 따라 유지될 수도 있고, 유지되지 않을 수도 있다.

------

**구조**

리스트, 셋, 큐 등의 인터페이스들이 Collection 인터페이스를 상속하는 것과 달리, 맵 인터페이스는 Collection 인터페이스를 상속하지 않는다. K-V 페어 형태를 가지는 맵의 구조가 다른 자료구조들과 다르기 때문이다.

![https://blog.kakaocdn.net/dn/vUMGr/btqzklR2GOI/fsx9STXRSbeYJtlk3Qf45k/img.jpg](https://blog.kakaocdn.net/dn/vUMGr/btqzklR2GOI/fsx9STXRSbeYJtlk3Qf45k/img.jpg)

Collection 인터페이스를 상속하는 Set, List, Queue

------

**성능**

[제목 없음](https://www.notion.so/73b94fa457464648aac760cbfdc127b1)

------

**비교**

Map 인터페이스를 구현하는 HashTable, HashSet, Linked-HashSet, TreeSet의 비교

[제목 없음](https://www.notion.so/8423c0669022487cb1970775e33d444c)

------

[[JAVA Collections API\] 자료구조 요약: 구조/성능/용도](https://gem1n1.tistory.com/97)