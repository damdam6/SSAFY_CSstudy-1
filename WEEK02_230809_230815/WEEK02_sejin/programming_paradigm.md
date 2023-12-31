

# 프로그래밍 패러다임(programming paradigm)

프로그래머에게 프로그래밍 관점을 갖게 해주는 역할을 하는 개발 방법론

- 예
    - 객체지향 프로그래밍은 프로그래머들이 프로그램을 상호 작용하는 객체들의 집합으로 볼 수 있게 함
    - 함수형 프로그래밍은 상태 값을 지니지 않는 함수 값들의 연속으로 생각할 수 있게 함


> 💡 <b>분류</b>
>
> - 선언형
>     - 함수형
> - 명령형
>     - 객체지향형
>     - 절차지향형


## 선언형과 함수형 프로그래밍

- 선언형 프로그래밍(declarative programming)
    - ‘무엇을’ 풀어내는가에 집중하는 패러다임
    - “프로그램은 함수로 이루어진 것이다”
- 함수형 프로그래밍(functional programming)
    - 선언형 패러다임의 일종
    - 작은 ‘순수 함수’들을 블록처럼 쌓아 로직을 구현하고 ‘고차 함수’를 통해 재사용성을 높인 프로그래밍 패러다임
    - 예 : 자바스크립트
        - 함수가 일급 객체이기 때문에 객체지향 프로그래밍보다는 함수형 프로그래밍 방식이 선호
    - 커링, 불변성


> 💡 <b>순수 함수</b>
>
> - 출력이 입력에만 의존하는 것



> 💡 <b>고차 함수</b>
>
> - 함수가 함수를 값처럼 매개변수로 받아 로직을 생성할 수 있는 것
> - 고차 함수를 쓰기 위해서는 해당 언어가 `일급 객체`라는 특징을 가져야 함
>     - 변수나 메서드에 함수를 할당할 수 있음
>     - 함수 안에 함수를 매개변수로 담을 수 있음
>     - 함수가 함수를 반환할 수 있음


## 객체지향 프로그래밍(OOP, Object-Oriented Programming)

객체들의 집합으로 프로그램의 상호 작용을 표현하며 데이터를 객체로 취급하여 객체 내부에 선언된 메서드를 활용하는 방식

- 설계에 많은 시간이 소요
- 처리 속도가 다른 프로그래밍 패러다임에 비해 상대적으로 느림

### 특징

- 추상화(abstraction)
    - 복잡한 시스템으로부터 핵심적인 개념 또는 기능을 간추려내는 것
- 캡슐화(encapsulation)
    - 객체의 속성과 메서드를 하나로 묶고 일부를 외부에 감추어 은닉하는 것
- 상속성(inheritance)
    - 상위 클래스의 특성을 하위 클래스가 이어받아서 재사용하거나 추가, 확장하는 것
- 다형성(polymorphism)
    - 하나의 메서드나 클래스가 다양한 방법으로 동작하는 것
    - 오버로딩(overloading)
        - 같은 이름을 가진 메서드를 여러 개 두는 것
        - 메서드의 타입, 매개변수의 유형, 개수 등으로 여러 개를 둘 수 있으며 컴파일 중에 발생하는 ‘정적’ 다형성
    - 오버라이딩(overriding)
        - 상위 클래스로부터 상속받은 메서드를 하위 클래스가 재정의
        - 런타임 중에 발생하는 ‘동적’ 다형성

### 설계 원칙(SOLID 원칙)

- 단일 책임 원칙(SRP, Single Responsibility Principle)
    - 모든 클래스는 각각 하나의 책임만 가져야 함
- 개방-폐쇄 원칙(OCP, Open Closed Principle)
    - 유지 보수 사항이 생긴다면 코드를 쉽게 확장할 수 있도록 하고 수정할 때는 닫혀 있어야 함
- 리스코프 치환 원칙(LSP, Liskov Substitution Principle)
    - 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 함
    - 부모 객체에 자식을 객체를 넣어도 시스템이 문제없이 돌아가게 만드는 것
- 인터페이스 분리 원칙(ISP, Interface Segregation Principle)
    - 하나의 일반적인 인터페이스보다 구체적인 여러 개의 인터페이스를 만들어야 하는 원칙
- 의존 역전 원칙(DLP, Dependency Inversion Principle)
    - 자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 변하기 쉬운 것의 변화에 영향받지 않게 하는 원칙
    - 상위 계층은 하위 계층의 변화에 대한 구현으로부터 독립해야 함
        - 타이어를 갈아끼울 수 있는 틀을 만들어 놓은 후 다양한 타이어를 교체할 수 있어야 함

## 절차형 프로그래밍

- 로직이 수행되어야 할 연속적인 계산 과정으로 이루어짐
- 일이 진행되는 방식으로 그저 코드를 구현하기만 하면 되기 때문에 코드의 가독성이 좋으며 실행 속도가 빠름
- 계산이 많은 작업 등에 쓰임
- 예 : 포트란(fortran)을 이용한 대기 과학 관련 연산 작업, 머신 러닝의 배치 작업
- 단점 : 모듈화하기 어렵고 유지 보수성이 떨어짐

## 패러다임의 혼합

- 가장 좋은 패러다임은 없음
- 비즈니스 로직이나 서비스의 특징을 고려해서 패러다임을 정해야 함
- 여러 패러다임을 조합하여 상황과 맥랑에 따라 패러다임 간의 장점만 취해 개발
