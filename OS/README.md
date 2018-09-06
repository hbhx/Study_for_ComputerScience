# 운영체제
  - [프로세스와 스레드의 차이](#프로세스와-스레드의-차이)
  - [Multi Programming, Multi Processing, Multi Threading의 차이](#multi-programming,-multi-processing,-multi-threading의-차이)
  - [인터럽트](#인터럽트)
  - [스케줄러의 종류](#스케줄러의-종류)
    - 장기 스케줄러
    - 단기 스케줄러
    - 중기 스케줄러
  - [CPU 스케줄러](#cpu-스케줄러)
    - FCFS(
    - SJF
    - SRT
    - Priority Scheduling
    - RR(Round Robin)
  - [동기 / 비동기](#동기-/-비동기)
  - [프로세스 동기화](#프로세스-동기화)
  - [동기화 기법](#동기화-기법)
    - 세마포어(Semaphore)
    - 모니터(Monitor)
    - 뮤텍스(Mutex)
  - [데드락](#데드락)
    - Deadlock Prevention
    - Deadlock Avoidance
    - Deadlock Detection and Recovery
    - Deadlock Ignorance
  - [가상메모리](#가상메모리)
  - [페이지 교체 알고리즘](#페이지-교체-알고리즘)
    - Optimal Algorithm
    - FIFO(First In First Out)
    - LRU(Least Recently Used)
    - LFU(Least Frequency Used)
    - Clock Algorithm(LRU Approximation Algorithm)

<br/><br/>

# 프로세스와 스레드의 차이

**프로세스(Process)**
>Process is a program in execution

즉, 프로세스는 현재 사용중인 프로그램을 의미하고, <br>
스레드는 하나의 프로세스 내에서 생성되는 실행 주체이다.

**스레드(Thread)**
>A Thread is a unit of CPU utilization

**Benefits of Threads**
- Responsiveness
- Resource Sharing
- Economy
- Utilization of MP(Multi Processor) Architectures

<br>

# Multi Programming, Multi Processing, Multi Threading의 차이?

**Multi Programming**
- 하나의 프로세스에서 다른 프로세스로 CPU 제어권이 넘어감으로 여러 프로그램을 교대로 수행함
- Interactive한 방식

**Multi Processing**
- 1개 이상의 프로세서가 협력하여 작업을 처리함
- 여러 프로세서가 작업을 병렬처리함

**Multi Threading**
- 프로세스는 IPC(InterProcess Communication)을 통해 자원을 공유함
- 하지만 스레드는 하나의 공유메모리를 사용하여 자원을 공유함

<br>

# 인터럽트

> 프로그램을 수행하는 도중에 예기치 않은 상황이 발생<br>
  Register와 PC(Program Counter)를 저장한 후, CPU 제어권을 인터럽트 처리 루틴에 넘겨줌

**인터럽트(Interrupt) 종류**
- H/W 인터럽트 (Interrupt) : Timer, I/o
- S/W 인터럽트 (Trap) : System Call, Exception

**Interrupt Call**
- Timer Interrupt : CPU가 한 프로세스가 독점하여 차지하는 것을 방지
- I/O Interrupt : I/O작업을 요청하는 Interrupt

**System Call**
- 사용자 프로그램이 S/W적으로 Inerrupt를 요청
- 사용자 프로그램은 직접 O/S에 직접 요청을 할 수 없음
- Mode bit(0 : Kernel mode , 1 : User mode) 가 1인 경우 System call을 통해 mode bit를 0으로 만듬

<br>

# 스케줄러의 종류

**문맥교환 (Context Switch)**
- CPU를 한 프로세스에서 다른 프로세스로 넘겨주는 과정
- CPU 제어권을 넘겨줄 때 프로세스의 상태를 PCB에 저장함
- PCB(Process Control Block) : OS가 프로세스들을 관리하기 위해 각 프로세스당 유지하는 정보

**프로세스를 스케줄링하기 위한 큐**
- Job Queue : 현재 시스템 내에 있는 모든 프로세스의 집합
- Ready Queue : 현재 메모리 내에 있으면서 CPU를 얻어서 실행되기를 기다리는 프로세스의 집합
- Device Queue : I/O 처리를 기다리는 프로세스의 집합

**장기 스케줄러 (Long-term Scheduler, Job Scheduler)**
- 시작 프로세스 중에서 어떤 것을 Ready Queue로 보낼지 결정하는 스케줄러
- 프로세스에 Memory를 주는 문제
- 시분할에서는 장기 스케줄러가 없음 (모든 프로세스가 Ready Queue로 보내짐)

**단기 스케줄러 (Short-term Scheduler, CPU Scheduler)**
- 어떤 프로세스에게 CPU를 줄 것인가 결정하는 스케줄러
- 충분히 빨라야함!

**장기 스케줄러 (Medium-term Scheduler, Swapper)**
- 여유 공간을 마련하기 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄
- 프로세스에게서 Memory를 뺏는 문제

<br>

# CPU 스케줄러

**FCFS**
- 프로세스의 도착 순서에 따라 스케줄링
- Convoy Effect(Short Process가 오래 기다림) 문제 발생

**SJF**
- 실행시간이 가장 짧은 프로세스부터 스케줄링

**SRT**
- 현재 수행중인 프로세스의 남은 burst time보다 짧은 프로세스가 도착하면 CPU를 넘겨줌
- Starvation(Preemption의 경우 Long Process가 무한히 기다림) 문제 발생

**Priority Scheduling**
- SJF는 일종의 우선순위 스케줄링
- Aging으로 Starvation 문제를 해결
> Aging :  As time progresses increase the priority of the process.

**RR(Round Robin)**
- Time Quantum(할당 시간)을 가짐
- 할당 시간이 끝나면 CPU를 Preemption 당하고 Ready Queue로 이동
- 할당시간이 크면 FCFS
- 할당시간이 작으면 Overhead 증가

<br>

# 동기 / 비동기

**Sync(동기) vs Async(비동기)**

- 메소드를 실행시킴과 동시에 반환값이 기대되는 경우를 **동기** 라고 표현하고<br>
그렇지 않은 경우에 대해서 **비동기** 라고 한다.

- 동시에라는 말은 실행되었을 때 값이 반환되기 전까지는 blocking 되어 있었다는 것을 의미한다.<br>
비동기의 경우, blocking 되지 않고 이벤트 큐에 넣거나 백그라운드 스레드에게 해당 task를 위임하고 바로 다음 코드를 실행하기 때문에 값이 바로 반환되지 않는다!!

> 📛 Blocking<br>
\- 요청한 작업을 마칠 때까지 계속 대기 <br>
\- 리턴값을 받아야 끝이남

> 📛 Non-Blocking<br>
\- 요청한 작업을 즉시 마칠 수 없으면 그냥 리턴

<br>

# 프로세스 동기화

**Race Condition**
- 여러 프로세스들이 동시에 공유데이터에 접근하면 일관성(Consistency) 문제 발생
- race condition을 막기 위해서 Concurrent Process는 동기화(Synchronize)되어야 한다!

**Critical Sectoin (임계 구역)**
- 각 Process의 Code 에서 공유데이터에 접근하는 Section

<br>

# 동기화 기법

**동기화 기법**
- 한정적인 공유자원에 여러 스레드가 동시에 접근하면 문제가 발생
- 이를 방지하기 위해, 스레드들에게 하나의 자원에 대한 처리 권한을 주거나 순서를 조정해 주는 기법
- 뮤텍스, 모니터와 세마포어의 차이는 전자는 상호배제(Mutual Exclusion)를 함으로써 임계구역에 하나의 스레드만 들어갈 수 있고 후자는 하나의 스레드만 들어가게 할 수 있고 (Binary Semaphore), 여러개의 스레드가 들어가게 할 수 있다 (Counting Semaphore)

**세마포어(Semaphore)**
- 동기화 기법 중, 추상적인 방법
- 세마포어는 여러 프로세스들에 의해 공유되는 변수로 정의
- 이 변수는 오직 P와 V라는 Atomic한 연산에 의해서만 접근가능
- 리소스의 상태를 나타내는 카운터라고 생각하면됨

> 📛 P(S)<br>
\- 자원을 획득<br>
\- S가 0보다 작으면 자원을 기다림<br>
\- 자원을 획득한 후에 S--

> 📛 V(S)<br>
\- 자원을 반납<br>
\- 자원을 반납한 후에 S++

- Busy / Wait (= Spin Lock) : 자원이 모두 사용 중일때 대기함
- Block / Wake up (= Sleep Lock) : 자원이 모두 사용중이라면 Blocked 상태로 전환

**모니터(Monitor)**
- 모니터 내에서는 한번에 하나의 프로세스만 활동 가능
- 프로그래머가 동기화 제약 조건을 명시적으로 코딩할 필요가 없음
- Condition Variable (프로세스가 모니터 안에서 기다릴 수 있도록)
- Condition Variable은 Wait/Signal 연산에 의해서만 접근가능
- x.wait() 상태의 프로세스는 다른 프로세스가 x.signal()을 하기 전까지 suspend 된다 (signal은 정확히 하나의 suspend된 프로세스를 깨움)

**뮤텍스(Mutex)**
- 임계구역을 가진 스레드들의 Running Time이 겹치지 않게 각각 단독으로 실행되게 하는 기술
- 스레드가 Mutex를 소유하여 해제할 수 있다 (해제는 반드시 Mutex를 소유한 스레드가 해야함!)
- 상태가 0,1 뿐인 Binary Semaphore

---

> 📛 Monitor vs Semaphore<br>
\- 모니터는 자체적으로 하나의 프로세스만 처리<br>
\- 반면 세마포어는 직접 Lock을 걸고 해제해야 한다

> 📛 Mutex vs Semaphore<br>
\- 뮤텍스는 오직 동기화 대상이 하나인 반면, 세마포어는 동기화 대상이 하나 이상이다

<br>

# 데드락

**데드락(Deadlock) 발생 조건**
- Mutual Exclusion(상호 배제)
- No Preemption(비선점)
- Hold and Wait(점유 대기)
- Circular Wait(순환 대기)

**해결 방법**
- Deadlock Prevention
  <br> : 자원 할당 시, 데드락 발생 조건 중 하나라도 만족되지 않게 하는 것
  -  Preemption (Save&Restore 가능한 자원에서 사용)
  - Request all resources Initially (프로세스 시작 시 모든 자원을 할당)
  - 자원이 필요한 경우 보유 자원을 놓음
  - Order resources numerically (할당 순서를 정하여 정해진 순서대로만 자원할당)
- Deadlock Avoidance
  - 자원 요청에 대한 부가적인 정보를 이용해서 deadlock의 가능성이 없는 경우에만 자원할당
  - 프로세스들이 필요로 하는 각 자원별 최대 사용량을 미리 선언

  <!-- - ![single_instance](../assets/images/SingleInstance.png) -->
  <!-- - ![Multiple_instance](../assets/images/MultipleInstance.png) -->

- Deadlock Detection & Recovery
<br> : 데드락을 탐색하고 복구하는 방법
  - Recovery 1. Process Termination
    - 프로세스를 종료한다
  - Recovery 2. Resource Preemption
    - 비용을 최소화할 Victim Process를 선정하여 자원을 선점한다

- Deadlock Ignore
  - Deadlock이 일어나지 않을 것을 가정하고 아무런 조치를 취하지 않는다
  - 만약 발생 시, 사용자가 직접 프로세스를 죽이는 방법으로 대처한다

<br>

# 가상메모리

**가상메모리(Virtual Memory)의 배경**
- 실행되는 코드의 전부를 메모리에 존재시켜야 했고, 메모리 용량보다 큰 프로그램은 실행시킬 수 없었다
- **프로그램의 일부분만 메모리에 올릴 수 없을까?** 라는 생각을 가지고 만들어 진게 가상메모리

**가상메모리가 하는일**
- 실제의 물리 메모리 개념과 사용자의 논리 메모리 개념을 분리한 것
- 작은 메모리를 가지고 얼마든지 큰 가상 주소 공간을 프로그래머에게 제공할 수 있음

<br>

# 페이지 교체 알고리즘

**페이지 부재(Page Fault)**
- Invalid Page에 접근을 하면 MMU(Memory Management Unit)가 Trap을 발생시킴
- 물리 메모리에 Page를 적재해야함
- 만약 Free Frame이 없다면 페이지 교체를 수행해야함

**Optimal Algorithm**
- 가장 먼 미래에 참조되는 페이지를 교체
- 미래를 예측해야하기 때문에 구현이 어렵지만 성능이 좋음

**FIFO(First In First Out)**
- 가장 먼저 들어온 페이지를 교체
- FIFO Anomaly : 프레임 수가 늘어났는데도 Page Fault 증가

**LRU(Least Recently Used)**
- 가장 오랫동안 참조되지 않은 페이지를 교체
- Linked List로 구현하여 O(1) Complexity를 가짐

**LFU(Least Frequency Used)**
- 참조횟수가 가장 적은 페이지를 교체
- Heap으로 구현하여 O(log n) Complexity를 가짐

**Clock Algorithm(LRU)**
- NRU(Not Recently Used)
- H/W에 의해 조작되며 O/S는 Reference bit를 참고하여 Victim 결정
- Reference bit = 1 (최근사용), Reference bit = 0 (최근사용X)
- 시계방향으로 움직이며 Reference bit가 1이면 0으로 바꾸고, 한바퀴를 돌고와서 0인 페이지를 교체
