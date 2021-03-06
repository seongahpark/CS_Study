# Week1 - Software Engineering

[출처 - gyoogle](https://github.com/gyoogle/tech-interview-for-developer)

## 클린코드와 리팩토링

#### 클린코드

클린코드란, 가독성이 높은 코드를 말한다.

- 클린 코드를 위한 구현 방법
  - 네이밍이 잘 되어야 함
  - 오류가 없어야 함
  - 중복이 없어야 함
  - 의존성을 최대한 줄여야 함
  - 클래스 혹은 메소드가 한 가지 일만 처리해야 함

- 예시

  ```c++
  public int AAA(int a, int b){
  	return a+b;
  }
  ```

  - 함수의 네이밍만 봐서 무슨 역할을 하는 함수인지 알 수 없다.

  ```c++
  public int sum(int a, int b){
  	return a+b;
  }
  ```

  - 함수의 네이밍만 보고도 합을 구하는 함수인지 알 수 있다.



#### 리팩토링

프로그램의 외부 동작은 그대로 둔 채, 내부의 코드를 정리하면서 개선하는 것을 말함.

리팩토링 작업은 코드의 가독성을 높이고, 향후 이루어질 유지보수에 큰 도움이 된다. 

```
리팩토링은 성능을 최적화시키는 것이 아닌,
코드를 이해하기 쉽고, 수정하기 쉽도록 만들어
코드를 신속하게 개발할 수 있게 만들어주고, 코드 품질을 개선한다.
```

- 리팩토링이 필요한 코드
  - 중복 코드
  - 긴 메소드
  - 거대한 클래스
  - Switch 문
  - 절차지향으로 구현한 코드

```c++
switch 문을 지양해야하는 이유 : 객체지향 특징일 살리기 위해
switch 문 리팩토링 -> 오버라이드로 변경
```



#### 클린코드와 리팩토링의 차이점

클린코드 -> 단순히 가독성을 높이기 위한 작업

리팩토링 -> 유지보수를 위한 코드 개선

즉, 리팩토링은 클린코드를 포함한 개념이다.

> 리팩토링
>
> > 클린코드

클린코드는 설계부터 잘 이루어져 있는 것이 중요하고, 리팩토링은 결과물이 나온 이후 유지보수가 진행될 때 개선해나가는 것이 올바른 방향이다.
