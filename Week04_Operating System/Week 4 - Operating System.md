# Week 4 - Operating System

[출처 : gyoogle](https://gyoogle.dev/blog/computer-science/operating-system/PCB%20&%20Context%20Switching.html)

### 목차

[1. PCB와 Context Switching](#PCB와-Context-Switching)

[2. IPC(Inter Process Communication)](#IPC(Inter-Process-Communication))

[3. CPU 스케줄링](#CPU-스케줄링)

---



## PCB와 Context Switching

**Process Management** : CPU가 프로세스가 여러개일 때, CPU 스케줄링을 통해 관리하는 것

**Process Metadata** : 프로세스들의 특징을 갖고있어 CPU가 어떤 프로세스인지 알 수 있도록 해줌

> ex) Process ID, Process State, Process Priority, CPU Registers, Owner, CPU Usage, Memory Usage

**PCB(Process Control Block)** : 프로세스 메타 데이터를 저장. 한 PCB 안에는 한 프로세스의 정보가 담김

- PCB의 필요성 : CPU에서 프로세스의 상태에 따라 교체작업이 이루어질 때, 앞으로 다시 수행할 대기 중인 프로세스에 관한 저장 값을 PCB에 저장.

  > CPU의 교체작업 : 인터럽트가 발생하여 할당받은 프로세스가 waiting 상태가 되고, 다른 프로세스를 running으로 바꿔 올리는 경우

- PCB 관리 방법 : Linked List 방식. 프로세스가 생성되면 해당 PCB가 생성되고 완료시 제거된다. 주고값으로 연결된 연결리스트라 삽입 / 삭제가 용이.

![img](https://t1.daumcdn.net/cfile/tistory/25673A5058F211C224)

> **PCB에 저장되기까지 과정**
>
> 프로그램 실행 -> 프로세스 생성 -> 프로세스 주소 공간에 (코드, 데이터, 스택) 생성 -> 프로세스의 메타데이터들이 PCB에 저장

**Context Switching **: 수행 중인 프로세스를 변경할 때, CPU가 이전의 프로세스 상태를 PCB에 보관하고, 또 다른 프로세스의 정보를 PCB에 읽어 레지스터에 적재하는 과정

- 발생 과정 : 인터럽트가 발생, 실행 중인 CPU 사용 허가시간을 모두 소모, 입출력을 위해 대기해야되는 경우.

  ```프로세스가 Ready -> Running, Running -> Ready, Running -> Waiting처럼 상태가 변경할 때```

- Context Switching의 OverHead (과부하) : CPU가 놀지 않도록 계속 프로세스를 수행시키도록 하기 위해 다른 프로세스를 실행시키고 Context Switching 하다보면 OverHead를 감수해야 하는 상황이 발생할 수 있다.

<br>

<br>

## IPC(Inter Process Communication)

**IPC 통신** : 독립적 구조를 가진 프로세스가 커널이 제공하는 IPC 설비를 이용해 프로세스 간의 통신을 가능하도록 하는 것. 프로세스 간 데이터를 동기화하고 보호하기 위해 세마포어와 뮤텍스 사용.

> **커널** : 운영체제의 핵심적인 부분, 다른 모든 부분에 여러 기본적인 서비스를 제공

**IPC 종류**

>**1. 익명 PIPE**
>
>> 파이프로 두 프로세스를 연결하면 한 프로세스는 데이터를 쓰기만, 다른 하나는 데이터를 읽기만 할 수 있다.
>>
>> **한쪽 방향으로만 통신이 가능한 반이중 통신**이 특징이다.
>>
>> 양쪽으로 송/수신을 하고 싶으면 2개의 파이프를 설치해야 한다.
>>
>> - 장점 : 간단하게 사용 가능, 단순한 데이터 흐름 시 효율적
>>
>> - 단점 : 전이중 통신을 위해 2개를 만들 때 구현이 복잡
>
>---
>
>**2. Named PIPE(FIFO)**
>
>> 익명 파이프는 통신할 프로세스를 명확히 알 수 있는 경우에 사용 (ex. 부모-자식 프로세스 간 통신)
>>
>> Named 파이프는 익명 파이프의 확장된 형태로, 전혀 모르는 상태의 프로세스들 사이 통신에 사용
>>
>> - 장점 : 부모 프로세스와 무관한 다른 프로세스도 통신이 가능
>> - 단점 : 전이중 통신을 위해 2개를 만들어야 함
>
>---
>
>**3. Message Queue**
>
>> 입출력 방식은 Named 파이프와 동일
>>
>> 다른 점은 파이프처럼 데이터의 흐름이 아니라 메모리 공간인 것
>>
>> 사용할 데이터에 번호를 붙이며 여러 프로세스가 동시에 데이터를 쉽게 다룰 수 있음
>
>---
>
>**4. 공유 메모리**
>
>> 파이프, 메시지 큐가 통신을 이용한 설비라면, 공유 메모리는 프로세스 간 메모리 영역을 공유하여 **데이터 자체를 공유하도록 지원하는 설비**
>>
>> 프로세스가 공유 메모리 할당을 커널에 요청 -> 커널이 해당 프로세스에 메모리 공간 할당 -> 모든 프로세스는 해당 메모리 영역에 접근 가능
>>
>> **중개자 없이 곧바로 메모리에 접간 가능 -> IPC 중 가장 빠르게 작동**
>
>---
>
>**5. 메모리 맵**
>
>> 공유 메모리처럼 메모리 공유, **열린 파일을 메모리에 맵핑시켜 공유**.
>>
>> 공유 매개체가 파일 + 메모리
>>
>> 파일로 대용량 데이터를 공유할 때 사용
>
>---
>
>**6. 소켓**
>
>> 네트워크 소켓 통신을 통해 데이터 공유
>>
>> 클라이언트와 서버가 소켓을 통해 통신
>>
>> 원격에서 프로세스 간 데이터를 공유할 때 사용
>>
>> 서버(bind, listen, accept), 클라이언트(connect)

<br>

<br>

## CPU 스케줄링

1. **스케줄링** : CPU를 잘 사용하기 위해 프로세스를 효율적으로 배정하는 것

   - 조건 : 오버헤드 ↓ / 사용률 ↑ / 기아 현상 ↓

   - 목표

     > 1. **Batch System** : 가능하면 많은 일을 수행. 시간(time) 보단 처리량(throughout)이 중요
     > 2. **Interactive System** : 빠른 응답 시간. 적은 대기 시간.
     > 3. **Real-Time System** : 기한(deadline) 맞춤.

2. **선점 / 비선점 스케줄링**

   - 선점 (preemptive) : OS가 CPU의 사용권을 선점할 수 있는 경우, 강제 회수하는 경우
   - 비선점 (nonpreemptive) : 프로세스 종료 or I/O 등의 이벤트가 있을 때까지 실행 보장 (처리시간 예측이 어려움)

3. **프로세스 상태**

   ![download (5)](https://user-images.githubusercontent.com/13609011/91695344-f2dfae80-eba8-11ea-9a9b-702192316170.jpeg)

- 비선점 스케줄링 : ```Inrterrupt```, ```Scheduler Dispatch```
- 선점 스케줄링 : ``I/O or Event Wait``

---

> **프로세스의 상태 전이**
>
> - **승인 (Admitted)** : 프로세스 생성이 가능하여 승인
> - **스케줄러 디스패치 (Scheduler Dispatch)** : 준비 상태에 있는 프로세스 중 하나를 선택하여 실행시키는 것
> - **인터럽트 (Interrupt)** : 예외, 입출력, 이벤트 등이 발생해 현재 실행 중인 프로세스를 준비 상태로 바꾸고, 해당 작업을 먼저 처리하는 것
> - **입출력 또는 이벤트 대기 (I/O or Event Wait)** : 실행 중인 프로세스가 입출력이나 이벤트를 처리해야 하는 경우, 입출력/이벤트가 모두 끝날 때 까지 대기 상태로 만드는 것
> - **입출력 또는 이벤트 완료 (I/O or Event Completion)** : 입출력/이벤트가 끝난 프로세스를 준비 상태로 전환하여 스케줄러에 의해 선택될 수 있도록 만드는 것

<br>

<br>

4. **CPU 스케줄링의 종류**

   >- 비선점 스케줄링
   >
   > 	1. FCFS (First Come First Served)
   >     - 큐에 도착한 순서대로 CPU 할당
   >     - 실행 시간이 짧은 게 뒤로 가면 평균 대기 시간이 길어짐
   >	2. SJF (Shortest Job First)
   >    - 수행시간이 가장 짧다고 판단되는 작업을 먼저 수행
   >    - FCFS 보다 평균 대기 시간 감소, 짧은 작업에 유리
   >	3. HRN (Highest Response-ratio Next)
   >    - 우선순위를 계산하여 점유 불평등을 보완한 방법 (SJF의 단점 보완)
   >    - 우선순위 = (대기시간 + 실행시간) / (실행시간)

   

   >- 선점 스케줄링
   >  1. Priority Scheduling
   >     - 정적/동적으로 우선순위를 부여하여 우선순위가 높은 순서대로 처리
   >     - 우선 순위가 낮은 프로세스가 무한정 기다리는 Starvation 이 생길 수 있음
   >     - Aging 방법으로 Starvation 문제 해결 가능
   >  2. Round Robin
   >     - FCFS에 의해 프로세스들이 보내지면 각 프로세스는 동일한 시간의 ```Time Quantum``` 만큼 CPU를 할당 받음
   >     - 할당 시간 (``Time Quantum``)이 크면 FCFS와 같게 되고, 작으면 Context Switching이 잦아져 오버헤드가 증가한다.
   >     - ``Time Quantum`` or ``Time Slice`` : 실행 최소 단위 시간
   >  3. Multilevel-Queue (다단계 큐)
   >     - 작업들을 여러 종류의 그룹으로 나누어 여러 개의 큐를 이용하는 기법
   >     - 우선순위가 낮은 큐들이 실행 못하는 걸 방지하고자 각 큐마다 다른 ``Time Quantum``을 설정해주는 방식 사용
   >     - 우선순위가 높은 큐는 작은 ``Time Quantum`` 할당. 낮은 큐는 큰 ``Time Quantum`` 할당.
   >  4. Multilevel-Feedback-Queue (다단계 피드백 큐)
   >     - 다단계 큐에서 자신의 ``Time Quantum``을 다 채우는 프로세스는 밑으로 내려가고 다 채우지 못한 프로세스는 원래 큐 그대로 -> 다 채운 프로세스는 CPU Burst 프로세스로 판단하기 때문이다
   >     - 짧은 작업에 유리, 인터럽트가 잦은 입출력 위주 작업에 우선권을 줌
   >     - 처리 시간일 짧은 프로세스를 먼저 처리하기 때문에 Turnaround 평균 시간을 줄여줌
   >

   <br>

   <br>

5. **CPU 스케줄링 척도**
   - Response Time : 작업이 처음 실행되기까지 걸린 시간
   - Turnaround Time : 실행 시간과 대기 시간을 모두 합한 시간으로 작업이 완료될 때 까지 걸린 시간
