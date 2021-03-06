# Week 4 - Operating System

**질문 정리**

- 경림

  - Context Switching 이란?
    - Context Switching은 언제 발생하는가?
    - Context Switching에는 어떤 측면에서 오버헤드가 따를까? : ``메모리와 시간 비용``
  - 다단계 큐 스케줄링에 대해 간단히 설명해보시오
    - 다단계 큐에서 사용되는 Time Quantum 이란? : ``CPU 점유 시간, 처리 시간``

- 성아

  - 선점 / 비선점 스케줄링에 대해 설명해보시오

    - 비선점 스케줄링의 종류를 말하고 간단하게 설명해보시오
    - FCFS 방식의 단점
    - FCFS 방식의 단점 보완을 위한 방법을 알고 있는가

  - IPC에 대한 설명과 예시

    - HTTP 통신과 소켓 통신의 차이

    > **HTTP 통신** : HyperText Transfer Protocol의 약자로, 클라이언트에서 서버로 요청을 보내고, 서버가 응답하는 방식으로 통신이 이루어짐. 응답에는 클라이언트 요청에 따른 결과를 반환한다. 
    >
    >  -> **클라이언트 요청이 있을 때 서버가 응답하는 단방향 통신**
    >
    > **소켓 통신** : 클라이언트도 서버로 요청을 보낼 수 있고, 서버도 클라이언트로 요청을 보낼 수 있다. 계속해서 Connection을 들고 있기 때문에 HTTP 통신에 비해 많은 리소스가 소모된다. 보통 스트리밍이나 실시간 채팅같이 실시간으로 데이터를 주고 받는 경우에 사용
    >
    > -> **서버와 클라이언트 양방향 연결이 이루어지는 통신**

- 현준

  - 프로세스의 특징을 설명

    ```
    - 프로세스는 각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당받음
    - 기본적으로 프로세스 당 최소 1개의 스레드를 가지고 있음
    - 각 프로세스는 별도의 주소 공간에서 실행, 한 프로세스는 다른 프로세스의 변수나 자료구조에 접근 X
    - 한 프로세스가 다른 프로세스의 자원에 접근하려면 IPC를 사용해야 함
    ```

  - CPU Scheduling 이란?

    ```
    CPU 하나는 동시에 여러개의 프로세스를 처리할 수 없어 한 순간에 어떤 프로세스가 CPU를 사용할 수 있게 하는지 결정하는 정책
    ```

    - CPU 스케줄링은 언제 발생하는가?

      ```
      - 실행 상태 -> 대기 상태 (EX. 입출력 요청) : 비선점
      - 실행 상태 -> 준비 상태 (EX. 인터럽트 발생) : 선점
      - 대기 상태 -> 준비 상태 (EX. 입출력 종료)
      - 종료될 때 (Terminated)
      ```

    - 선점 스케줄링과 비선점 스케줄링의 차이점

  - 문맥 교환 (Context Switching) 이란?

    ```
    프로세스 상태를 변경하는 것
    하나의 프로세스가 CPU를 사용 중인 상태에서 다른 프로세스가 CPU를 사용하도록 이전 프로세스의 상태를 보관하고 새 프로세스의 상태를 적재하는 작업
    ```

- 성진

  - PCB는 어떤 정보를 저장하고 있는가
    - PCB가 필요한 이유
    - Context Switching에서 PCB는 어떻게 이용되고 있는가
  - IPC란 무엇인가?
    - IPC의 종류 중 가장 빠르게 작동할 수 있는 방법에 대해 설명
  - CPU 스케줄링이 필요한 이유는?
    - 비선점 / 선점 스케줄링의 특징
    - 비선점 / 선점 스케줄링의 종류

<br>

---

**다음주 주제**

> **데드락(DeadLock)**
>
> **Race Condition**
>
> **세마포어(Semaphore) & 뮤텍스(Mutex)**

