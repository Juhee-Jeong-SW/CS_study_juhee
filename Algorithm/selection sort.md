# Selection Sort

## 📌 Selection Sort

### 설명

Selection Sort는 Bubble Sort과 유사한 알고리즘으로, **`해당 순서에 원소를 넣을 위치는 이미 정해져있고, 어떤 원소를 넣을지 선택하는 알고리즘`**이다.

→ 배열에서 **해당 자리를 선택하고 그 자리에 오는 값을 찾는 것**.

### 진행방식

1. 주어진 배열 중에 최소값을 찾는다.
2. 그 값을 맨 앞에 위치한 값과 교체. (Pass)
3. 맨 처음 위치를 뺸 나머지 배열을 같은 방법으로 교체함.

### 코드

```java
void selectionSort(int[] arr) {
    int indexMin, temp;
    for (int i = 0; i < arr.length-1; i++) {        // 1. 위치 선택
        indexMin = i;
        for (int j = i + 1; j < arr.length; j++) {  // 2. i+1 원소부터 선택한 위치의 값과 비교 시작
            if (arr[j] < arr[indexMin]) {           // 3. 오름차순이므로 현재 선택한 자리에 있는 값보다 순회하고 있는 값이 작다면, 위치를 갱신.
                indexMin = j;
            }
        }
        // 4. swap(arr[indexMin], arr[i]) : '2'번 반복문이 끝난 뒤에는 indexMin에 '1'번에서 선택한 위치에 들어가야 하는 값의 위치를
						// 갖고 있으므로 서로 교환함.
        temp = arr[indexMin];
        arr[indexMin] = arr[i];
        arr[i] = temp;
  }
  System.out.println(Arrays.toString(arr));
}
```

### 그림으로 간단히 이해하기

![selection-sort-001](https://user-images.githubusercontent.com/70262329/103340526-a4471000-4ac7-11eb-8d5a-ac68e9070df1.gif)

출처 : https://github.com/GimunLee/tech-refrigerator/blob/master/Algorithm/선택 정렬 (Selection Sort).md#선택-정렬-selection-sort

### 시간복잡도

최선, 평균, 최악 모두 **O(n^2)**

첫 번째 회전에서의 비교횟수 : 1 ~ (n-1) → n-1

두 번째 회전에서의 비교횟수 : 2 ~ (n-1) → n-2

(n-1) + (n-2) + (n-3) + ... + 2 + 1 ⇒ n(n-1)/2 이므로

비교하는 것이 상수 시간에 이루어진다는 가정 아래, n 개의 주어진 배열을 정렬하는데 O(n^2)만큼의 시간 소요.

### 공간복잡도

교환을 통한 정렬이 수행되므로 **O(n)**

### 장단점

[장점]

- 알고리즘 단순
- 정렬을 위한 비교 횟수는 많지만 Bubble sort에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료 상태에서는 비교적 효율적
- Bubble Sort 와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로 다른 메모리 공간 필요하지 않음 → 제자리 정렬 (in-place sorting)

[단점]

- 비효율적 → 시간복잡도 O(n^2)
- 불안정 정렬 (Unstable Sort)
