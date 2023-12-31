# 디자인 패턴

프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 하나의 ‘규약’ 형태로 만들어 놓은 것.

1. [싱글톤 패턴](#싱글톤-패턴singleton-pattern)
2. [팩토리 패턴](#팩토리-패턴-factory-pattern)
3. [전략 패턴](#전략-패턴-strategy-pattern)
4. [옵저버 패턴](#옵저버-패턴-observer-pattern)
5. [프록시 패턴과 프록시 서버](#프록시-패턴과-프록시-서버)
6. [이터레이터 패턴](#이터레이터-패턴iterator-pattern)
7. [노출 모듈 패턴](#노출-모듈-패턴-revealing-module-pattern)
8. [MVC 패턴](#mvc-패턴)
9. [MVP 패턴](#mvp-패턴)
10. [MVVM 패턴](#mvvm-패턴)


## 싱글톤 패턴(Singleton pattern)

: 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴.

- 하나의 클래스를 기반으로 단 하나의 인스턴스를 만들어 이를 기반으로 로직을 만듦
- 데이터베이스 연결 모듈에 많이 사용
- 장점 : 인스턴스를 생성할 때 드는 비용 감소
- 단점 : 의존성이 높아짐
    - TDD(Test Driven Development)할 때 단위 테스트를 주로 하는데, 단위 테스트는 서로 독립적이어야 하며 테스트를 어떤 순서로든 실행할 수 있어야 하는데 싱글톤 패턴은 미리 생성된 인스턴스를 기반으로 구현하는 패턴이므로 테스트마다 독립적인 인스턴스를 만들기 어렵다.
    - 모듈 간의 결합을 강하게 만들 수 있다. → 의존성 주입(DI, Dependency Injection)을 통해 해결 가능!
        - 의존성 (=종속성) : A가 B에 의존성이 있다 = B의 변경 사항에 대해 A 또한 변해야 된다.
        - 의존성 주입의 장점
            1. 모듈들을 쉽게 교체할 수 있는 구조가 되어 테스팅하기 쉽고 마이그레이션하기도 수월
            2. 구현할 때 추상화 레이어를 넣고 이를 기반으로 구현체를 넣어주므로 애플리케이션 의존성 방향이 일관되고, 애플리케이션을 쉽게 추론할 수 있으며, 모듈 간의 관계들이 명확해짐
        - 의존성 주입의 단점
            1. 모듈들이 더욱더 분리되므로 클래스 수가 늘어나 복잡성 증가
            2. 약간의 런타임 페널티 발생
        - 의존성 주입 원칙
            
            “상위 모듈은 하위 모듈에서 어떠한 것도 가져오지 않아야 합니다. 또한 둘 다 추상화에 의존해야 하며, 이때 추상화는 세부 사항에 의존하지 말아야 합니다.”

## 팩토리 패턴 (Factory pattern)

: 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴.

- 특징
    - 상위 클래스와 하위 클래스가 분리되기 때문에 느슨한 결합을 가짐
    - 상위 클래스에는 인스턴스 생성 방식에 대해 전혀 알 필요가 없기 때문에 더 많은 유연성을 가짐
    - 객체 생성 로직이 따로 떼어져 있기 때문에 코드를 리팩터링하더라도 한 곳만 고칠 수 있게 되니 유지 보수성이 증가

❓ **의존성 주입**

## 전략 패턴 (Strategy pattern)

= 정책 패턴 (policy pattern).
객체의 행위를 바꾸고 싶은 경우 직접 수정하지 않고 전략이라고 부르는 캡슐화한 알고리즘을 컨텍스트 안에서 바꿔주면서 상호 교체가 가능하게 만드는 패턴.

- 컨텍스트 : 상황, 맥락, 문맥을 의미. 개발자가 어떠한 작업을 완료하는 데 필요한 모든 관련 정보.

## 옵저버 패턴 (Observer pattern)

: 주체가 어떤 객체(subject)의 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 디자인 패턴. 주체와 객체를 따로 두지 않고 상태가 변경되는 객체를 기반으로 구축하기도 함.

- 주체 : 객체의 상태 변화를 보고 있는 관찰자
- 옵저버 : 이 객체의 상태 변화에 따라 전달되는 메서드 등을 기반으로 ‘추가 변화 사항’이 생기는 객체들

MVC(Model-View-Controller)패턴에도 사용됨

## 프록시 패턴과 프록시 서버

- 프록시 객체 : 어떠한 대상의 기본적인 동작(속성 접근, 할당, 순회, 열거, 함수 호출 등)의 작업을 가로챌 수 있는 객체.
    - target : 프록시할 대상
    - handler : target 동작을 가로채고 어떠한 동작을 할 것인지가 설정되어 있는 함수

### 프록시 패턴(proxy pattern)

: 대상 객체(subject)에 접근하기 전 그 접근에 대한 흐름을 가로채 대상 객체 앞단의 인터페이스 역할을 하는 디자인 패턴.

객체의 속성, 변환 등을 보완하며 보안, 데이터 검증, 캐싱, 로깅에 사용

- 프록시 서버에서의 캐싱
    : 캐시 안에 정보를 담아두고, 캐시 안에 있는 정보를 요구하는 요청에 대해 다시 저 멀리 있는 원격 서버에 요청하지 않고 캐시 안에 있는 데이터를 활용하는 것. 불필요하게 외부와 연결하지 않기 때문에 트래픽을 줄일 수 있다.
    

### 프록시 서버(proxy server)

: 서버와 클라이언트 사이에서 클라이언트가 자신을 통해 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 컴퓨터 시스템이나 응용 프로그램.

## 이터레이터 패턴(Iterator pattern)

: 이터레이터(iterator)를 사용하여 컬렉션(collection)의 요소들에 접근하는 디자인 패턴.

순회할 수 있는 여러 가지 자료형의 구조와는 상관없이 이터레이터라는 하나의 인터페이스로 순회 가능.

## 노출 모듈 패턴 (revealing module pattern)

: 즉시 실행 함수를 통해 private, public같은 접근 제어자를 만드는 패턴.

## MVC 패턴

: 모델(Model), 뷰(View), 컨트롤러(Controller)로 이루어진 디자인 패턴.

### 모델

: 애플리케이션의 데이터인 데이터베이스, 상수, 변수 등

### 뷰

: 사용자 인터페이스 요소. 모델을 기반으로 사용자가 볼 수 있는 화면

- 모델이 가지고 있는 정보를 따로 저장하지 않아야 하며 단순히 사각형 모양 등 화면에 표시하는 정보만 가지고 있어야 함.

### 컨트롤러

: 하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할을 하며 이벤트 등 메인 로직을 담당.

모델과 뷰의 생명주기 관리.

모델이나 뷰의 변경 통지를 받으면 이를 해석하여 각각의 구성 요소에 해당 내용에 대해 알려줌

## MVP 패턴

: MVC 패턴에서 파생 → C가 P(프레젠터, presenter)로 교체된 패턴.

뷰와 프레젠터는 일대일 관계이기 때문에 MVC 패턴보다 더 강한 결합을 지닌 디자인 패턴

## MVVM 패턴

: MVC패턴에서 파생 → C가 VM(뷰 모델, View Model)로 교체된 패턴.

뷰 모델은 뷰를 더 추상화한 계층. MVC 패턴과는 다르게 커맨드와 데이터 바인딩을 가지는 것이 특징.

뷰와 뷰 모델 사이의 양방향 데이터 바인딩을 지원

UI를 별도의 코드 수정 없이 재사용할 수 있고 단위 테스팅하기 쉽다.