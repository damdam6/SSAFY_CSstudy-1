
# ✅ 인덱스

# 인덱스의 필요성

- `인덱스`는 데이터를 빠르게 찾을 수 있는 하나의 장치
- 인덱스를 설정하면 테이블 안에 내가 찾고자 하는 데이터를 빠르게 찾을 수 있음

# B-트리

- 인덱스는 보통 `B-트리`라는 자료 구조로 이루어져 있음
- 루트 노드, 브랜치 노드, 리프 노드로 나뉨
- 트리 탐색은 맨 위 루트 노드부터 탐색이 일어나며 브랜치 노드를 거쳐 리프 노드까지 내려옴
- 정렬된 값을 기반으로 탐색

## 인덱스가 효율적인 이유

- 효율적인 단계를 거쳐 모든 요소에 접근할 수 있는 균형 잡힌 트리 구조와 트리 깊이의 `대수확장성` 때문

## 대수확장성

- `대수확장성`이란 트리 깊이가 리프 노드 수에 비해 매우 느리게 성장하는 것
- 기본적으로 인덱스가 한 깊이씩 증가할 때마다 최대 인덱스 항목의 수는 4배씩 증가

# 인덱스 만드는 방법

## MySQL

- 클러스터형 인덱스와 세컨더리 인덱스가 있으며, 클러스터형 인덱스는 테이블당 하나 설정 가능
- 하나의 인덱스만 생성할 것이라면 클러스터형 인덱스를 만드는 것이 세컨더리 인덱스를 만드는 것보다 성능이 좋음
- 세컨더리 인덱스는 보조 인덱스로, 여러 개의 필드 값을 기반으로 쿼리를 많이 보낼 때 생성해야 하는 인덱스

## MongoDB

- 도큐먼트를 만들면 자동으로 ObjectID가 형성되며, 해당 키가 기본키로 설정됨
- 세컨더리키도 부가적으로 설정해서 기본키와 세컨더리키를 같이 쓰는 복합 인덱스를 설정 가능

# 인덱스 최적화 기법

## 1. 인덱스는 비용이다

- 인덱스 리스트, 그다음 컬렉션 순으로 탐색 → 두 번 탐색하도록 강요
- 컬렉션이 수정되었을 때 인덱스도 수정되어야 함
    - 이때 B-트리의 높이를 균형 있게 조절하는 비용도 들고, 데이터를 효율적으로 조회할 수 있도록 분산시키는 비용도 들게 됨
- 따라서
    - 쿼리에 있는 필드에 모두 인덱스 설정X
    - 컬렉션에서 가져와야 하는 양이 많을수록 인덱스를 사용하는 것은 비효율적

## 2. 항상 테스팅하라

- 서비스에서 사용하는 객체의 깊이, 테이블의 양 등이 다름 → 인덱스 최적화 기법은 서비스 특징에 따라 달라짐 → 항상 테스팅하는 것이 중요
- explain() 함수를 통해 인덱스를 만들고 쿼리를 보낸 이후에 테스팅을 하며 걸리는 시간을 최소화

## 3. 복합 인덱스는 같음, 정렬, 다중 값, 카디널리티 순이다

- 보통 여러 필드를 기반으로 조회를 할 때 복합 인덱스를 생성하는데, 이 인덱스를 생성할 때는 순서가 있고 생성 순서에 따라 인덱스 성능이 달라짐
1. 어떠한 값과 같음을 비교하는 `==`이나 `equal`이라는 쿼리가 있다면 제일 먼저 인덱스로 설정
2. 정렬에 쓰는 필드라면 그다음 인덱스로 설정
3. 다중 값을 출력해야 하는 필드, 즉 쿼리 자체가 `>`이거나 `<` 등 많은 값을 출력해야 하는 쿼리에 쓰는 필드라면 나중에 인덱스를 설정
4. `카디널리티`가 높은 순서를 기반으로 인덱스를 생성

```
💡 카디널리티

- 유니크한 값의 정도
```