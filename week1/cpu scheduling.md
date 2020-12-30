# CPU 스케줄링

FCS, SJF, SRT, Priority Scheduling

스케줄링 대상은 Ready Queue 에 있는 프로세스들이다.

## 📌 FCFS

> First Come First Served

### 특징

- 먼저 온 순서대로 처리.

- 비선점형 스케줄링 (뻇기지 않는다.)

  → 일단 CPU 를 잡으면 CPU burst 가 완료될 때까지 CPU를 반환하지 않음. 할당되었던 CPU가 반환될 때만 스케줄링이 이루어짐.

### 문제점

- Convoy Effect

  → 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생한다.

## 📌 SJF

> Shortest Job First

### 특징

- 다른 프로세스가 먼저 도착했어도 CPU burst time이 짧은 프로세스에게 우선으로 할당
- 비선점형 스케줄링

### 문제점

- Starvation

  → 효율성을 추구하는 게 가장 중요하지만, 특정 프로세스가 지나치게 차별받으면 안됨.

  이 스케줄링은 극단적으로 CPU 사용이 짧은 job을 선호함. 그래서 사용 시간이 긴 프로세스는 거의 영원히 CPU 를 할당받을 수 없다.

## 📌 SRT

> Shortest Remaining time First

### 특징

- 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어짐.

- 선점형 스케줄링

  → 현재 수행중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU 를 뺏긴다.

### 문제점

- Starvation
- 새로운 프로세스가 도달할 때마다 스케줄링을 다시 하기 때문에 CPU Burst time (CPU 사용시간)을 측정할 수 없다.

## 📌 Priority Scheduling

### 특징

- 우선순위가 가장 높은 프로세스에게 CPU를 할당하는 스케줄링.

  - 우선순위 : 정수로 표현하게 되고, 작은 숫자가 우선 순위가 높다.

- 선점형 스케줄링

  → 더 높은 우선 순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.

- 비선점형 스케줄링

  → 더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.

### 문제점

- Starvation

- 무기한 봉쇄 (Indefinite blocking)

  → 실행 준비는 되어 있으나, CPU 를 사용 못하는 프로세스를 CPU 가 무기한 대기하는 상태

### 해결책

- aging

  → 아무리 우선순위가 늦은 프로세스라도 오래 기다리면 우선순위를 높여주도록 함.