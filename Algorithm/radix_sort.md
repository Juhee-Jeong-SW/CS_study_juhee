# 기수 정렬(Radix Sort)

## 📌 Radix **Sort**

`낮은 자리수부터 비교하여 정렬`해가는 알고리즘.

비교 연산을 하지 않고 정렬 속도가 빠르지만, 데이터 전체 크기에 기수 테이블의 크기만한 메모리가 추가로 필요함.

*기수란?*

주어진 데이터를 구성하는 기본 요소. 이 기수를 이용해 정렬 진행.

하나의 기수마다 하나의 버킷을 생성하여 분류한 뒤 버킷 안에서 또 정렬을 하는 것.

### 정렬 방식

1. 0~9 까지의 bucket (Queue 자료구조)을 준비한다.
2. 모든 데이터에 대하여 가장 낮은 자리수에 해당하는 Bucket에 차례대로 데이터를 둔다.
3. 0부터 차례대로 버킷에서 데이터를 다시 가져온다.
4. 가장 높은 자리수를 기준으로 하여 자리수를 높여가며 2,3번 과정을 반복한다.

### 그림으로 이해하기

![1](https://user-images.githubusercontent.com/70262329/104424927-5d771100-55c3-11eb-94f5-a446426a01d2.png)

**아래의** **8개 데이터에 대하여 기수 정렬을 시도해 보겠습니다. 위의 그림과 같이 각 숫자에 해당하는 Queue공간을 할당하고 진행합니다.**

![2](https://user-images.githubusercontent.com/70262329/104424935-5ea83e00-55c3-11eb-91c7-5cba652df8e5.png)

**먼저 1의 자리 숫자부터 시도를 합니다. 데이터 순서대로 각 1의 자리에 해당되는 Queue에 데이터가 들어가게 됩니다. 15같은 경우는 1의 자리가 5이므로 Queue 5에 들어가는 방식입니다.**

![3](https://user-images.githubusercontent.com/70262329/104424937-5f40d480-55c3-11eb-80c0-993013eada2c.png)

**위의 그림처럼** **다시 0번 Queue부터 차례대로 데이터를 가지고 와서 원래의 배열에 넣어주게 됩니다.**

**1의 자리에 대한 정렬이 완료되었습니다. 다음으로는 10의 자리에 대하여 같은 작업을 반복합니다.**

![4](https://user-images.githubusercontent.com/70262329/104424939-5f40d480-55c3-11eb-9d1c-e29416674b59.png)

**마찬가지로 각 데이터의 10의 자리에 해당되는 Queue에 데이터를 위치 시킵니다. 그런 다음 0번 Queue부터 차례대로 다시 데이터를 가지고 옵니다.**

![5](https://user-images.githubusercontent.com/70262329/104424943-5fd96b00-55c3-11eb-8605-b7631fb36b0c.png)

**최종적으로 정렬이 완료가 됩니다.**

### **시간 복잡도**

- O(d *(n + b)) = **O(n) , O(dn)**

  → d : 정렬할 숫자의 자릿수, b : 10(k와 같으나 10으로 고정되어 있음.)

### 장단점

[장점]

- 장점 : 문자열, 정수 정렬 가능

[단점]

- 자릿수가 없는 것은 정렬 불가. Ex ) 부동 소숫점
- 중간 결과를 저장할 bucket 공간 필요
- 적용할 수 있는 범위가 제한적 → 범위는 데이터 길이에 의존하게 됨. 즉, 정렬하고자 하는 데이터의 길이가 동일하지 않은 데이터에 대해서는 좋은 성능을 내는 데 불가

### LSD / MSD

[LSD]

- Least Significant Digit

  덜 중요한 숫자부터 정렬하는 방식.

  → 숫자를 정렬한다고 가정했을 때, 일의 자리부터 정렬하는 방식

[MSD]

- Most Significant DIgit

  중요한 숫자부터 정렬하는 방식

  → 세 자리 숫자면 백의 자리부터 정렬하는 방식

** 두 방식의 시간 복잡도는 동일하다. 하지만 주로 기수정렬을 할 때는 **LSD**

LSD는 중간에 정렬 결과를 볼 수 없고, 무조건 일의 자리부터 백의 자리까지 모두 정렬이 끝나야 결과를 확인할 수 있다.

MSD는 정렬 중간에 정렬이 될 수 있음. 그러므로 정렬하는 데 시간을 줄일 수 있지만, 정렬이 완료됐는지 확인하는 과정이 필요해 메모리를 더 사용하게 된다. 또한, 상황마다 일관적인 정렬 알고리즘을 사용하여 정렬하는데 적용할 수 없으므로 불편하다.

### 소스코드

```cpp
void countSort(int arr[], int n, int exp) {
	int buffer[n];
    int i, count[10] = {0};
    
    // exp의 자릿수에 해당하는 count 증가
    for (i = 0; i < n; i++){
        count[(arr[i] / exp) % 10]++;
    }
    // 누적합 구하기
    for (i = 1; i < 10; i++) {
        count[i] += count[i - 1];
    }
    // 일반적인 Counting sort 과정
    for (i = n - 1; i >= 0; i--) {
        buffer[count[(arr[i]/exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }
    for (i = 0; i < n; i++){
        arr[i] = buffer[i];
    }
}

void radixsort(int arr[], int n) {
     // 최댓값 자리만큼 돌기
    int m = getMax(arr, n);
    
    // 최댓값을 나눴을 때, 0이 나오면 모든 숫자가 exp의 아래
    for (int exp = 1; m / exp > 0; exp *= 10) {
        countSort(arr, n, exp);
    }
}
int main() {
    int arr[] = {170, 45, 75, 90, 802, 24, 2, 66};
    int n = sizeof(arr) / sizeof(arr[0]);			// 좋은 습관
    radixsort(arr, n);
    
    for (int i = 0; i < n; i++){
        cout << arr[i] << " ";
    }
    return 0;
}
```

[06 정렬 알고리즘 - 기수 정렬(Radix Sort)](https://lktprogrammer.tistory.com/48)
