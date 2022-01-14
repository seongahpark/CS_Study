# Week 9 - Data Structure

[출처 : gyoogle](https://gyoogle.dev/blog/computer-science/data-structure/Array.html)

### 목차

[1. 배열 (Array)](#배열-(Array))

[2. 연결 리스트 (Linked List)](#연결-리스트-(Linked-List))

[3. 스택 & 큐](스택-&-큐)

[4. 힙 (Heap)](#힙-(Heap))

---

<br>

## 배열 (Array)

> 고정 길이 데이터 구조

- 선언 시 크기와 데이터 타입을 지정해야 함
- 장점
  - index로 빠르게 값을 찾는 것이 가능
  - 크기가 고정
- 단점
  - 새로운 요소를 삽입하는 것이 어렵다

- **ArrayList** 

  - 가변 길이 데이터 구조, 동적할당
  - Java에서 이용 가능
  - C++에서는 Vector가 유사한 자료구조
  - 데이터를 찾는 것은 빠르다(인덱스 사용)
  - 데이터의 삽입 및 삭제가 느리다

  

### 배열 관련 알고리즘

> C++ 배열 사이즈 구하는 방법
>
> ``` c++
> int n = sizeof(arr) / sizeof(arr[0]);
> ```



#### 배열 회전 프로그램

1. 기본적인 알고리즘

   - tmp를 이용해 첫 번째 인덱스를 저장한 후 한 칸씩 값을 당겨오는 것

   ```c++
   void leftRotatebyOne(int arr[], int n){
   	int tmp = arr[0];
   	for(int i=0; i<n-1; i++){
   		arr[i] = arr[i+1];
   	}	
   	arr[i] = tmp;	
   }
   ```

   - 원하는 회전 수 만큼 for 문을 돌려야 함

   

2. 저글링 알고리즘

   - 최대공약수 gcd를 이용해 집합을 나누어 여러 요소를 한꺼번에 이동

   ```c++
   int gcd(int a, b){
       if(b == 0) return a;
       else return gcd(b, a%b);
   }
   
   void leftRotate(int arr[], int d, int n){
       for(int i=0; i<gcd(d,n); i++){
           int tmp = arr[i];
           int j = i;
           
           while(1){
               int k = j+d;
               if(k >= n) k -= n;
               
               if(k == i) break;
               
               arr[j] = arr[k];
               j = k;
           }
           arr[j] = tmp;
       }
   }
   ```

   

3. 역전 알고리즘

   - 회전시키는 수를 기준으로 구간을 나누어 reverse로 구현
   - d = 2 이면, 1,2 / 3~7로 구간을 나눈다
   - 각 구간을 reverse하고 합친 후 다시 reverse

   ```c++
   #include <algorithm>
   
   void reverseArr(int arr[], int start, int end){
       //swap을 이용한 reverse
       while(start < end){
           arr[start] = arr[end];
           start++;
           end--;
       }
   }
   
   void rotateLeft(int arr[], int d, int n){
       reverseArr(arr, 0, d-1);
       reverseArr(arr, d, n-1);
       reverseArr(arr, 0, n-1);
   }
   ```

   

#### 배열의 특정 최대 합 구하기

- arr[i]에서 i*arr[i]의 Sum이 가장 큰 값을 출력하라 (회전하면서 탐색)

- 접근방법

  > arr[i]의 전체 합과 i*arr[i]의 전체 합을 저장할 변수 선언
  >
  > 최종 가장 큰 sum 값을 저장할 변수 선언
  >
  > 배열을 회전시키며 i*arr[i]의 합의 값을 저장하고, 가장 큰 값을 마지막에 출력

- 점화식을 이용한 해결법

  ```cpp
  회전 없이 i*arr[i]의 sum을 저장한 값
  R0 = 0*arr[0] + 1*arr[1] + ... + (n-1)*arr[n-1]
  
  1번 회전 후 i*arr[i]의 sum을 저장한 값
  R1 = 0*arr[n-1] + 1*arr[0] + ... + (n-1)*arr[n-2]
  
  두 개를 빼줌
  R1-R0 = arr[0] + arr[1] + ... + arr[n-2] - (n-1)*arr[n-1]
  
  2번 회전 후 i*arr[i]의 sum을 저장한 값
  R2 = 0*arr[n-2] + 1*arr[n-1] + ... + (n-1)*arr[n-3]
  
  1번 회전한 값과 빼면?
  R2 - R1 = arr[0] + arr[1] + ... + arr[n-3] - (n-1)*arr[n-2] + arr[n-1]
  
  여기서 규칙을 찾으면
  Rj - Rj-1 = arrSum - n*arr[n-j]
  ```

  ```c++
  #include <iostream>
  using namespace std;
  
  int maxVal(int arr[], int n){
      int arrSum = 0; // arr의 전체 합
      int curSum = 0; // i*arr[i]의 전체 합
      
      for(int i=0; i<n; i++){
          arrSum += arr[i];
          curSum += i*arr[i];
      }
      
      int maxSum = curSum;
      
      for(int j=0; j<n; j++){
          curSum = curSum + arrSum - n*arr[n-j];
          maxSum = max(maxSum, curSum);
      }
      
      return maxSum;
  }
  ```



#### 특정 배열을 arr[i] = i로 재배열

주어진 배열에서 arr[i] = i 가 가능한 것만 재배열 시키고 없으면 -1로 채움

```c++
Input : arr = {-1, -1, 6, 1, 9, 3, 2, -1, 4, -1}
Output : [-1, 1, 2, 3, 4, -1, 6, -1, -1, 9]
```

- 접근 방법

  > arr[i]가 -1이 아니고 arr[i]이 i가 아닐 때가 우선 조건
  >
  > 해당 arr[i] 값을 저장해두고, 이 값이 x 일 때, arr[x]를 탐색
  >
  > arr[x] 값을 저장해두고(y), arr[x]가 -1이 아니면서 arr[x]가 x가 아닌 동안을 탐색
  >
  > arr[x]를 x값으로 저장하고 기존의 x를 y로 수정

  ```c++
  int fix(int arr[], int len){
  	for(int i=0; i<len; i++){
  		if(arr[i] != -1 && arr[i] != i){
              int x = arr[i];
              
              while(arr[x] != -1 && arr[x] != x){
                  int y = arr[x];
                  arr[x] = x;
                  
                  x = y;
              }
              
              arr[x] = x;
              if(arr[i] != i) arr[i] = -1;
          }
  	}
  }
  ```

<br>

## 연결 리스트 (Linked List)

> 연속적인 메모리 위치에 저장되지 않는 선형 데이터 구조
>
> 포인터를 사용해서 연결 함
>
> 각 노드는 **데이터 필드**와 **다음 노드에 대한 참조**를 포함하는 노드로 구성

![img](https://www.geeksforgeeks.org/wp-content/uploads/gq/2013/03/Linkedlist.png)

- 장점

  - 동적 크기
  - 삽입 / 삭제 용이하고 빠름

- 단점

  - 임의로 액세스가 불가능하다. 첫 번째 노드부터 순차적으로 액세스 해야됨 -> 이진 검색 수행 불가능

    > **이진 검색** : 중간의 임의의 값을 선택해 비교

  - 포인터의 여분의 메모리 공간이 각 요소마다 필요

- 노드 구현

  ```c++
  struct Node{
  	int data;
      struct Node *next;
  };
  ```

- 노드 추가 구현

  - 앞 쪽에 노드 추가

    ```c++
    void push(struct Node** head_ref, int new_data){
        struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
        
        new_node->data = new_data;
        new_node->next = (*head_ref);
        
        (*head_ref) = new_node;
    }
    ```

  - 특정 노드 다음에 추가

    ```c++
    void insertAfter(struct Node* prev_node, int new_data){
        if(prev_node == NULL) return;
        struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
        
        new_node->data = new_data;
        new_node->next = prev_node->next;
        
        prev_node->next = new_node;
    }
    ```

  - 끝 쪽에 노드 추가

    ```c++
    void append(struct Node** head_ref, int new_data){
        struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
        struct Node *last = *head_ref;
        new_node->data = new_data;
        new_node->next = NULL;
        
        if(*head_ref == NULL){
            *head_ref = new_node;
            return;
        }
        
        while(last->next != NULL){
            last = last->nex;
        }
        last->next = new_node;
        return;
    }
    ```

    

## 스택 & 큐 (Stack & Queue)

### 스택 (Stack)

> 입력과 출력이 한 곳으로 제한
>
> **LIFO (Last In First Out, 후입선출)** : 가장 나중에 들어온 것이 먼저 나옴

- 사용 용도
  - 함수 콜스택
  - 문자열 역순 출력
  - 연산자 후위 표기
  - 뒤로가기 구현
  - OS에서 메모리를 가지고오는 구조
- 스택 구현
  - 데이터를 넣음 : push()
  - 데이터의 최상위 값을 뺌 : pop()
  - 비어있는지 확인 : isEmpty()
  - 꽉차있는지 확인 : isFull()
  - 스택 포인터(SP) : 다음값이 들어갈 위치를 가리키고 있음. 기본값은 -1
- 동적 배열 스택 : Java의 arraycopy를 활용하여 동적 배열 스택 구현. 또는, 스택을 연결리스트로 구현.
- 시간 복잡도 : O(1)



### 큐 (Queue)

> 입력과 출력을 한쪽 끝(front, rear)로 제한
>
> **FIFO (First In First Out, 선입선출)** : 가장 먼저 들어온 것이 가장 먼저 나옴

- 사용 용도
  - 버퍼 (ex. 프린트 버퍼)
  - 마구 입력된 것을 처리하지 못하는 상황
  - BFS
  - 들어온 패킷 먼저 수행

- 큐 구현
  - 들어올 때는 **rear**, 나올 때는 **front**부터 빠짐
  - 데이터 삽입 : enQueue(), rear가 enQueue 할 위치 기억
  - 데이터 뺌 : deQueue(), front가 deQueue 할 위치 기억
  - 비어있는지 확인 : isEmpty()
  - 꽉차있는지 확인 : isFull

- 일반 큐의 단점 : 큐에 빈 메모리가 남아도 rear가 끝에 도달시 꽉찬 것으로 오인할 수 있음
- **원형 큐**
  - 일반 큐의 단점을 개선하기 위한 방법
  - 처음과 끝이 연결된 것으로 간주
  - 공백, 포화 상태를 쉽게 구분하기 위해 자리 하나를 항상 비워둠
  - (index+1) % size 순환
  - 단점 : 메모리 공간은 잘 활용하지만 **배열**로 구현돼있어 큐의 크기가 제한 -> 연결리스트 큐로 크기 제한이 없고 삽입/삭제가 편리한 큐 구현
- 시간 복잡도 : O(1)



## 힙 (Heap)

> 완전 이진 트리의 일종
>
> 최대값과 최소값을 빠르게 찾기 위해 만들어진 구조

#### 우선순위 큐

> 데이터들이 우선순위를 가지고 있음. 우선순위가 높은 데이터가 먼저 나감

- 사용 용도
  - 시뮬레이션 시스템
  - 작업 스케줄링
  - 수치해석 계산

#### 힙 (Heap)

- 힙 종류
  - 최대 힙 (Max heap) : 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
  - 최소 힙 (Min Heap) : 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
- 구현
  - 배열 사용
  - 첫 번째 인덱스인 0은 사용하지 않음
  - 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변화 X
  - 왼쪽 자식 : 부모 * 2, 오른쪽 자식 : 부모 * 2 + 1의 구조
- 힙의 삽입
  - 새로운 노드를 힙의 마지막 노드에 삽입
  - 새로운 노드를 부모 노드들과 교환
- 힙의 삭제
  - 최대 힙에서 최대값은 루트 노드이므로 루트 노드가 삭제 (최대 힙에서의 삭제 연산은 최대값 요소 삭제)
  - 삭제된 루트 노드에는 힙의 마지막 노드를 가져옴
  - 힙 재구성
- 시간 복잡도 :  O(logn) / 힙 정렬 시간 복잡도 : O(nlogn) 