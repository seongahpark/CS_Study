# Week 5 - Operating System

[출처 : gyoogle](https://gyoogle.dev/blog/computer-science/operating-system/DeadLock.html)

### 목차

[1. 데드락(DeadLock)](#데드락(DeadLock))

[2. 경쟁 상태(Race Condition)](#경쟁-상태(Race-Condition))

[3. 세마포어와 뮤텍스](#세마포어와-뮤텍스)

---

<br>

## 데드락(DeadLock)

1. **데드락** : 프로세스가 자원을 얻지 못해 다음 처리를 하지 못하는 상태. ``교착상태``라고도 함. 시스템적으로 한정된 자원을 여러 곳에서 사용하려고 할 때 발생

2. **데드락이 주로 발생하는 경우**

   > - 멀티 프로그래밍 환경에서 한정된 자원을 얻기 위해 서로 경쟁하는 상황 발생
   > - 한 프로세스가 자원을 요청했을 때, 동시에 그 자원을 사용할 수 없는 상황이 발생할 수 있음. 이 때 프로세스는 대기 상태로 들어감
   > - 대기 상태로 들어간 프로세스들이 실행 상태로 변경될 수 없을 때 ``교착 상태`` 발생

3. **데드락 발생 조건**

   >**4가지 모두 성립해야 데드락 발생 -> 하나라도 성립하지 않으면 데드락 해결 가능**
   >
   >1) **상호 배제(Mutual Exclusion)**
   >2) **점유 대기(Hold and Wait)**
   >3) **비선점(No Preemption)**
   >4) **순환 대기(Circular Wait)**

4. 

   

