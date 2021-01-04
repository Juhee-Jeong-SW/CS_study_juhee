# Stack 과 Queue

```html
<pre>
💡 Stack 과 Queue 는 선형 자료구조이다.
</pre>
```



## 📌 Stack

> Last In First Out (LIFO) : 나중에 들어간 원소가 먼저 나온다.

### 특징

- 입력과 출력이 한 방향으로 제한.

- 차곡차곡 쌓이는 구조.

  → 먼저 Stack에 들어가게 된 원소는 맨 바닥에 깔림. 늦게 들어간 것은 그 위에 쌓이게 되고 호출 시 가장 위에 있는 게 호출됨.

### 사용하는 곳

- 함수의 콜스택
- 문자열 역순 출력
- 연산자 후위표기법

### 시간/공간 복잡도

- 시간 복잡도 : O(n)
- 공간 복잡도 : O(n)

### 구현

[sp]

```java
private int sp = -1;
```

- push/ pop 할 경우 해당 위치를 알고 있어야 하므로 이 위치를 기억하는 Stack Pointer가 필요함.
- 스택 포인터는 다음 값이 들어갈 위치를 가리키고 있음 ( default : -1 )

[push]

```java
public void push(Object o) {
    if(isFull(o)) {
        return;
    }
    
    stack[++sp] = o;
}
```

- 스택 포인터가 최대 크기와 같을 경우 return
- 그렇지 않다면 stack의 최상위 위치에 값을 넣는다.

[pop]

```java
public Object pop() {
    
    if(isEmpty(sp)) {
        return null;
    }
    
    Object o = stack[sp--];
    return o;
    
}
```

- 스택 포인터가 0이 되면 Null로 return
- 그렇지 않으면 최상위 위치의 값을 꺼내옴.

[isEmpty]

```java
private boolean isEmpty(int cnt) {
    return sp == -1 ? true : false;
}
```

- 입력 값이 최초 값과 같으면 true, 아니면 false

[isFull]

```java
private boolean isFull(int cnt) {
    return sp + 1 == MAX_SIZE ? true : false;
}
```

- sp + 1 의 값이 MAX_SIZE와 같다면 true, 아니면 false

## 📌 Queue

> First In First Out(FIFO) : 가장 먼저 들어온 것이 가장 먼저 나온다.

### 특징

- 입력과 출력을 한 쪽 끝으로 제한
- 큐의 가장 첫 원소 : front , 끝 원소 : rear
- 들어올 때 rear 로 들어오고, 나갈 때 fron 부터 빠짐
- 접근 방법은 가장 첫과 끝 원소로만 가능

### 사용하는 곳

- 버퍼
- 마구 입력된 것을 처리하지 못하는 상황
- BFS

### 시간/공간복잡도

- 시간복잡도 : O(n)
- 공간복잡도 : O(n)

### 구현

[기본값]

```java
private int size = 0; 
private int rear = -1; 
private int front = -1;

Queue(int size) { 
    this.size = size;
    this.queue = new Object[size];
}
```

[enQueue]

```java
public void enQueue(Object o) {
    
    if(isFull()) {
        return;
    }
    
    queue[++rear] = o;
}
```

- enQueue 시, 가득 찼다면 꽉 차 있는 상태에서 enQueue 했기 때문에 overflow 발생
- 그렇지 않다면, rear에 값 넣고 1 증가시킴

[deQueue]

```java
public Object deQueue(Object o) {
    
    if(isEmpty()) { 
        return null;
    }
    
    Object o = queue[front];
    queue[front++] = null;
    return o;
}
```

- deQueue 할 때, 공백이면 underflow 발생
- 그렇지 않다면, front에 위치한 값을 꺼내어 object에 넣어준 뒤, 꺼낸 위치는 null로 채워줌 ( 빼낸 거니까 )

[isEmpty]

```java
public boolean isEmpty() {
    return front == rear;
}
```

- front 와 rear가 같아지면 비어진 것

[isFull]

```java
public boolean isFull() {
    return (rear == queueSize-1);
}
```

- rear가 큐 사이즈 -1과 같아지면 가득찬 것

++ 원형큐는 따로 추가하기!