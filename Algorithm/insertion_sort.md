# 삽입정렬 (Insertion Sort)

## 📌 Insertion sort

### 설명

Insertion Sort는  Selection Sort과 유사하지만 좀 더 효율적인 알고리즘으로, **`해당 2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬하는`** 알고리즘이다.

→ 새로운 카드를 기존의 정렬된 카드 사이에 올바른 자리를 찾아 삽입한다.

### 진행방식

1. 정렬은 2번째 위치(index)의 값을 standard에 저장
2. standard 와 이전에 있는 원소들과 비교하여 자리를 바꾸며 삽입해 나감.
3. 1번으로 돌아가서 다음 위치(index)의 값을 standard에 저장하고 이 과정을 반복.

### 코드

```java
private static void sort(int[] arr) {
        for (int i = 1; i < arr.length; i++) { // 1
            int standard = arr[i]; // standard = temp
            int index = i - 1; // index = prev 

            while ((0 <= index) && standard < arr[index]) {//2
                arr[index + 1] = arr[index];
                index--;
            }
            arr[index + 1] = standard; // 3

            print(arr, i);
        }
    }

    private static void print(int[] arr, int step) {
        System.out.print(step + "단계 : ");
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }

        System.out.println();
    }
// 단계별 결과.
1단계 : 6 7 2 4 3 9 1 
2단계 : 2 6 7 4 3 9 1 
3단계 : 2 4 6 7 3 9 1 
4단계 : 2 3 4 6 7 9 1 
5단계 : 2 3 4 6 7 9 1 
6단계 : 1 2 3 4 6 7 9
```

- 상세
  1. 첫 번째 원소 앞(왼쪽)에는 어떤 원소도 갖고 있지 않기 때문에, 두 번째 위치(index)부터 탐색을 시작합니다. temp에 임시로 해당 위치(index) 값을 저장하고, prev에는 해당 위치(index)의 이전 위치(index)를 저장합니다.
  2. 이전 위치(index)를 가리키는 prev가 음수가 되지 않고, 이전 위치(index)의 값이 '1'번에서 선택한 값보다 크다면, 서로 값을 교환해주고 prev를 더 이전 위치(index)를 가리키도록 합니다.
  3. '2'번에서 반복문이 끝나고 난 뒤, prev에는 현재 **temp 값보다 작은 값들 중 제일 큰 값의 위치(index)** 를 가리키게 됩니다. 따라서, (prev+1)에 temp 값을 삽입해줍니다.

### 그림으로 간단히 이해하기

![insertion-sort-001](https://user-images.githubusercontent.com/70262329/103495110-f5b31e80-4e7c-11eb-9774-60f723574347.gif)


출처 : https://github.com/GimunLee/tech-refrigerator/blob/master/Algorithm/삽입 정렬 (Insertion Sort).md#삽입-정렬-insertion-sort

### 시간복잡도

- 최악의 경우(역으로 정렬되어 있을 경우)

  Selection Sort와 마찬가지로, (n-1) + (n-2) + (n-3) + ... + 2 + 1 ⇒ n(n-1)/2 이므로 **O(n^2)**

- 최선 (모두 정렬되어 있는 경우)

  한 번씩 비교하므로 **O(n)**

- 평균 : **O(n^2)**

### 공간복잡도

주어진 배열 안에서 교환(swap)을 통한 정렬이 이루어지므로 **O(n)**

### 장단점

[장점]

- 알고리즘 단순
- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적
- 제자리 정렬 (In-place sorting)
- 안정 정렬 (Stable Sort)
- Selection / Bubble Sort와 같은 O(n^2) 알고리즘에 비교하여 상대적으로 빠름

[단점]

- 비효율적 → 평균,최악 시간복잡도 O(n^2)
- Bubble/Selection sort와 마찬가지로 배열의 길이가 길어질수록 비효율적

### 결론

```html
Selection과 Insertion은 K번째 반복 이후, 첫번째 K 요소가 정렬된 순서로 온다는 점에서 유사.
하지만,
Selection Sort는 K+1번째 요소를 찾기 위해 나머지 모든 요소들을 탐색하지만
Insertion Sort는 K+1번째 요소를 배치하는 데 필요한 만큼의 요소만 탐색하기 때문에 훨씬 더 효율적으로 실행된다는 차이가 있음.
```

