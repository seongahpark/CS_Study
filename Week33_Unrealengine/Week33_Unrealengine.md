# Week 33 - Unrealengine

1. **Animation Instance & Animation Blueprint**

    #### Animation Instance

    - 애니메이션을 만들기 위해 사용되는 데이터들과 그에 대한 명령어 세트를 모아둔 오브젝트 인스턴스
    - Facade 디자인 패턴을 사용해서 만들어진 오브젝트로써, 현재 실행되고 있는 애니메이션과 애니메이션 몽타주들을 관리하는 오브젝트
    - Animation Instance를 통해 Animation Blueprint로 짜여진 구조에 명령을 내리거나, 애니메이션, 애니메이션 몽타주를 실행하고, 실행에 따른 여러 옵션들을 설정할 수 있다

    #### Animation Blueprint

    - 복잡한 애니메이션 동작을 만들고 제어하는 데 사용되는 비주얼 스크립트

2. **Animation Sequence & Animation Montage**

    #### Animation Sequence

    - 스켈레탈 메시에 재생할 수 있는 단일 애니메이션 에셋
    - 일정 시점에서의 본의 위치, 회전, 스케일 값을 나타내는 키프레임이 들어간다
    - 스켈레탈 메시의 본에 부드러운 애니메이션을 줄 수 있다
    - 각 애니메이션 시퀀스 에셋은 특정 스켈레톤을 타깃으로 하며, 딱 그 스켈레톤에서만 재생할 수 있다

    #### Animation Montage

    - 폭 넓은 애니메이션 이펙트가 가능해지는 다목적 툴
    - 코드를 통해서나 블루프린트 비주얼 스크립트 안에서 애니메이션 컨트롤을 노출시키는 데 관련되어 있다
    - 다양한 애니메이션 이펙트를 만드는 데 사용 가능하다

3. **RootMotion**

    - 스켈레톤의 루트 본의 애니메이션을 기준으로 하는 캐릭터의 동작
    - 애니메이션의 루트 모션은 재생 도중 시각화시켜 볼 수 있다

4. **Skeleton & SkeletalMesh**

    - 캐릭터의 본이나 조인트를 정의하는 데 사용되는 디지털 계층구조식 프레임워크로, 여러가지 면에서 생물학적 스켈레톤과 닮아있다
    - 스켈레탈 메시는 스켈레탈 메시의 표면을 구성하는 폴리곤 세트, 폴리곤의 버텍스 애니메이션에 사용할 수 있는 계층형 상호연결 본 세트로 이루어져 있다
    - 스켈레탈 메시의 주 용도는 캐릭터나 기타 애니메이트 오브젝트를 나타내는 데 쓰인다
    - 3D 모델, 리깅, 애니메이션은 (3DSMax, Maya, Softimage 등) 외부 모델링 / 애니메이션 어플리케이션으로 만든 다음, 언리얼 에디터의 콘텐츠 브라우저를 사용하여 언리얼 엔진 4로 임포트한 뒤 패키지에 저장한다

5. **Skeleton Retargeting**

    - 스켈레톤 애셋을 공유하나 비율이 크게 다른 캐릭터간에 애니메이션을 재사용할 수 있도록 해 주는 기능
    - 리타겟팅을 통해 애니메이션이 적용될 스켈레톤에 모양이 다른 캐릭터의 애니메이션을 사용할 경우, 일부분이 손실되거나 불필요하게 변형되지 않도록 할 수 있다
    - 다른 스켈레톤 을 사용하는 캐릭터끼리도 특정 조건 하에 애니메이션을 공유할 수 있다