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

- arr[i]에서 i*

