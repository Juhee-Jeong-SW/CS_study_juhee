# 스케줄러의 종류 (장기, 중기, 단기)와 특성

<pre>프로세스를 스케줄링하기 위한 Queue에는 세 가지 종류가 존재한다. <br/>Job Queue : 현재 시스템 내에 있는 모든 프로세스의 집합 <br/>
Ready Queue : 현재 메모리 내에 있으면서 CPU를 잡아서 실행되기를 기다리는 프로세스의 집합 <br/>
Device Queue : Device I/O 작업을 대기하고 있는 프로세스의 집합<br/>
각 Queue에 프로세스들을 넣고 빼주는 스케줄러에도 크게 세 가지 종류가 존재한다 </pre>

# 📌 장기스케줄러

> 어떤 프로세스를 준비큐에 넣을 것인가?

(Long-term Scheduler / Job Scheduler)

메모리는 한정되어 있는데 많은 프로세스들이 한번에 메모리에 올라올 경우, 대용량 메모리(디스크)에 임시로 저장된다. 이 pool에 저장되어 있는 프로세스 중 어떤 프로세스에 메모리를 할당하여 ready queue로 보낼지 결정하는 역할을 한다.

- 메모리와 디스크 사이의 스케줄링 담당
- 프로세스에 memory를 할당
- 실행중인 프로세스 수 제어 (degree of Multiprogramming 제어)
- 프로세스 상태 : new → ready(in memory)

** 참고 : 메모리에 프로그램이 너무 많이 올라가도, 너무 적게 올라가도 성능이 좋지 않은 것.

time sharing에는 장기 스케줄러 없음. 그냥 바로 메모리에 올라가 ready 상태가 됨.

# 📌 중기스케줄러

> 메모리에 적재된 프로세스 수 관리

(Medium-term Scheduler / Swapper )

현 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러

- 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄(swapping)
- 프로세스에게서 메모리를 deallocate
- degree of Multiprogramming 제어
- 프로세스 상태 : ready → suspended

** suspended : 외부적인 이유로 프로세스의 수행이 정지된 상태로 내려간 상태. 프로세스 전부가 디스크로 swap-out됨. blocked 상태를 다른 I/O 작업을 기다리는 상태이기 때문에 스스로 ready state로 돌아갈 수 있지만 이 상태는 외부적인 이유로 suspending 되었기 때문에 스스로 돌아갈 수 없음.

# 📌 단기스케줄러

> 어떤 프로세스에게 CPU를 할당해 줄 것인가?

(Short-term scheduler or CPU scheduler)

CPU와 메모리 사이의 스케줄링 담당

- ready queue에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정.
- 일반적인 스케줄러를 의미.
- 프로세스에 CPU를 할당 (scheduler dispatch)
- 프로세스 상태 : ready → running → wating → ready

## + 프로세스 상태

![다운로드](https://user-images.githubusercontent.com/70262329/103193433-c9991a00-491f-11eb-9dcf-869f0eb30ffe.png)


사진 출처 : https://kosaf04pyh.tistory.com/191
