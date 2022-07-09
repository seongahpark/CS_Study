# Week 32 - Unrealengine

1. **Property Replication & RPC**

    #### Property Replication

    - 액터에 변수나 데이터들에 대해 서버랑 클라이언트가 공유하기 위해 사용하는 방식
    - 레플리케이션이 주로 사용되는 클래스 -> 액터
    - 서버는 해당 액터들의 리스트를 가지고 액터들이 가지고 있는 UI를 통해 클라리언트와 통신이 가능하다
    - 액터들의 포인터들을 해당 UI로 매칭하여 패킷을 주고받는 방식을 가짐
    - 해당 액터와 레플리케이션이 활성화돼있으면, 해당 액터가 보유한 컴포넌트에 대해서도 레플리케이션을 사용할 수 있다

    #### RPC (Remote Procedure Calls)

    - Client RPC : 서버에서 호출하지만 클라이언트에서 실행되는 RPC
    - Server RPC : 클라이언트에서 호출하지만 서버에서 실행되는 RPC
    - 비신뢰성 통신 방식인 UDP 형식 사용
    - Reliable UDP를 사용하는 경우 UDP 방식 + 비신뢰성 단점 커버.
        - 패키지가 무조건 가야하는 상황에서 붙여준다

2. **Role & Remote Role**

    > Actor에 대한 소유자를 판단할 수 있는 프로퍼티

    - Role은 Actor에 대한 Authority Owner Actor의 Replication 여부, Remote Role은 Replication Mode를 나타냄
    - 해당 액터가 서버/클라이언트가 보유하고 있는지 서버로부터 실행하는 리모트로 행동하는지 판단하는 것
    - Server와 Client는 Role과 Remote Role의 값이 반대이다

3. **Unreal Header Tool & Build Tool**

    #### Header Tool

    - 언리얼 오브젝트 클래스에 대해 작업하는 것
    - 컴파일 전에 클래스를 분석하여 언리얼 오브젝트 정보를 담은 메타 데이터 생성
    - 클래스명.generated.h 헤더를 만든다

    #### Build Tool

    - 다양한 빌드 구성으로 빌드 프로세스를 자동화시키는 커스텀 툴
    - 추상적인 소스 코드 구조를 만들고, 각 플랫폼에 맞게 프로젝트 재생성
    - 빌드툴이 실행되면 현재 프로젝트의 폴더 구조와 소스 파일들을 분석하고 플랫폼에 맞는 개발 도구 환경을 자동으로 생성

4. **UObject & Garbage Collegion**

    > 언리얼 오브젝트는 언리얼 엔진의 관리를 받는 객체

    - 이점
        - 클래스의 타입 체킹을 빠르고 간편하게 할 수 있다
        - 가비지 컬렉션을 자동으로 해줌
    - 특징
        - CDO : 객체의 초기 값을 자체적으로 관리
        - Reflection : 객체 정보를 런타임에서 실시간으로 조회 가능
        - GC : 참조되지 않는 객체를 메모리에서 자동 해제 가능
        - Serialization : 객체와 속성 정보를 통으로 안전하게 보관하고 로딩
        - Delegate : 함수를 묶어서 효과적으로 관리하고 호출 가능
        - Replication : 네트워크 상에서 객체간에 동기화 가능
        - Editor Integration : 언리얼 에디터 인터페이스를 통해 값 편집 가능

    #### GC
    - 언리얼에서는 더 이상 참조되지 않거나 명시적으로 소멸 예약을 한 UObject를 주기적으로 정리하는 가비지 컬렉션 스키마를 이용함
    - 루트셋에서 시작하는데, 트리 구조로 내려오면서 오브젝트가 트리 안에서 검색이 되면 사용이 되고, 검색이 되지 않으면 가비지 컬렉션이 된다
    - UI 만들 때, C++로 코드 작성 시 shared_ptr, weak_ptr을 많이 쓴다
