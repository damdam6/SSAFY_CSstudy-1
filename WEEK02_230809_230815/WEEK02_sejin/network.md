

# 🌐 네트워크의 기초

## 네트워크

- 컴퓨터 등의 장치들이 통신 기술을 이용하여 구축하는 연결망
- 노드(node)와 링크(link)가 서로 연결되어 있거나 연결되어 있으며 리소스를 공유하는 집합
- 좋은 네트워크
    - 많은 처리량
    - 짧은 지연시간
    - 적은 장애 빈도
    - 좋은 보안


> 💡 <b>노드</b>
> 
> - 서버, 라우터, 스위치 등 네트워크 장치



> 💡 <b>링크</b>
> 
> - 유선 또는 무선을 의미


## 처리량(throughput)

링크를 통해 전달되는 단위 시간당 데이터양

- 단위 : bps(bits per second)
    - 초당 전송 또는 수신되는 비트 수
- 사용자들이 많이 접속할 때마다 커지는 트래픽, 네트워크 장치 간의 대역폭, 네트워크 중간에 발생하는 에러, 장치의 하드웨어 스펙에 영향을 받음


> 💡 <b>대역폭</b>
> 
> - 주어진 시간 동안 네트워크 연결을 통해 흐를 수 있는 최대 비트 수


## 지연 시간(latency)

요청이 처리되는 시간을 말하며 어떤 메시지가 두 장치 사이를 왕복하는데 걸린 시간

- 매체 타입(무선, 유선), 패킷 크기, 라우터의 패킷 처리 시간에 영향을 받음



## 네트워크 토폴로지(network topology)

노드와 링크가 어떻게 배치되어 있는지에 대한 방식이자 연결 형태 (네트워크의 구조)

- 병목 현상을 찾을 때 중요한 기준이 됨


> 💡 <b>병목(bottleneck) 현상</b>
> 
> - 전체 시스템의 성능이나 용량이 하나의 구성 요소로 인해 제한을 받는 현상
> - 서비스에서 이벤트를 열었을 때 트래픽이 많이 생기고 그 트래픽을 잘 관리하지 못하면 병목 현상이 생겨 사용자는 웹 사이트로 들어가지 못함
> - 주된 원인
>     - 네트워크 대역폭
>     - 네트워크 토폴로지
>     - 서버 CPU, 메모리 사용량
>     - 비효율적인 네트워크 구성


### 트리(tree) 토폴로지

계층형 토폴로지라고 하며 트리 형태로 배치한 네트워크 구성

- 노드의 추가, 삭제가 쉬움
- 특정 노드에 트래픽이 집중될 때 하위 노드에 영향을 끼칠 수 있음

### 버스(bus) 토폴로지

중앙 통신 회선 하나에 여러 개의 노드가 연결되어 공유하는 네트워크 구성

- 근거리 통신망(LAN)에서 사용
- 장점
    - 설치 비용이 적음
    - 신뢰성이 우수
    - 중앙 통신 회선에 노드를 추가하거나 삭제하기 쉬움
- 단점
    - 스푸핑이 가능


> 💡 <b>스푸핑</b>
> 
> - LAN상에서 송신부의 패킷을 송신과 관련 없는 다른 호스트에 가지 않도록 하는 스위칭 기능을 마비시키거나 속여서 특정 노드에 해당 패킷이 오도록 처리하는 것


### 스타(star, 성형) 토폴로지

중앙에 있는 노드에 모두 연결된 네트워크 구성

- 장점
    - 노드를 추가하거나 에러를 탐지하기 쉽고 패킷의 충돌 발생 가능적이 적음
    - 어떠한 노드에 장애가 발생해도 쉽게 에러를 발견할 수 있음
    - 장애 노드가 중앙 노드가 아닐 경우 다른 노드에 영향을 끼치는 것이 적음
- 단점
    - 중앙 노드에 장애가 발생하면 전체 네트워크를 사용할 수 없음
    - 설치 비용이 고가

### 링형(ring) 토폴로지

각각의 노드가 양 옆의 두 노드와 연결하여 전체적으로 고리처럼 하나의 연속된 길을 통해 통신을 하는 망 구성 방식

- 데이터는 노드에서 노드로 이동, 각각의 노드는 고리 모양의 길을 통해 패킷을 처리
- 장점
    - 노드 수가 증가되어도 네트워크상의 손실이 거의 없음
    - 충돌이 발생되는 가능성이 적음
    - 노드의 고장 발견을 쉽게 찾을 수 있음
- 단점
    - 네트워크 구성 변경이 어렵고 회선에 장애가 발생하면 전체 네트워크에 영향을 크게 끼침

### 메시(mesh) 토폴로지

망형 토폴로지라고도 하며 그물망처럼 연결되어 있는 구조

- 장점
    - 한 단말 장치에 장애가 발생해도 여러 개의 경로가 존재하므로 네트워크를 계속 사용할 수 있고 트래픽도 분산 처리 가능
- 단점
    - 노드의 추가가 어려움
    - 구축 비용과 운용 비용이 고가



## 네트워크 분류

규모를 기반으로 분류

### LAN(Local Area Network)

근거리 통신망

- 같은 건물이나 캠퍼스 같은 좁은 공간에서 운영
- 전송 속도가 빠르고 혼잡하지 않음

### MAN(Metropolitan Area Network)

대도시 지역 네트워크

- 도시 같은 넓은 지역에서 운영
- 전송 속도는 평균이며 LAN보다는 더 많이 혼잡

### WAN(Wide Area Network)

광역 네트워크

- 국가 또는 대륙 같은 더 넓은 지역에서 운영
- 전송 속도는 낮으며 MAN보다 더 혼잡



## 네트워크 성능 분석 명령어

### ping(Packet INternet Groper)

네트워크 상태를 확인하려는 대상 노드를 향해 일정 크기의 패킷을 전송하는 명령어

- 해당 노드의 패킷 수신 상태와 도달하기까지 시간 등을 알 수 있으며 해당 노드까지 네트워크가 잘 연결되어 있는지 확인 가능
- TCP/IP 프로토콜 중에 ICMP 프로토콜을 통해 동작
    - ICMP 프로토콜을 지원하지 않는 기기를 대상으로는 실행할 수 없음
    - 네트워크 정책상 ICMP나 traceroute를 차단하는 대상의 경우 불가

### netstat

접속되어 있는 서비스들의 네트워크 상태를 표시하는데 사용되며 네트워크 접속, 라우팅 테이블, 네트워크 프로토콜 등 리스트를 보여줌

- 주로 서비스의 포트가 열려 있는지 확인할 때 씀

### nslookup

DNS에 관련된 내용을 확인하기 위해 쓰는 명령어

- 특정 도메인에 매핑된 IP를 확인하기 위해 사용

### tracert/traceroute

목적지 노드까지 네트워크 경로를 확인할 때 사용하는 명령어

- 목적지 노드까지 구간들 중 어느 구간에서 응답 시간이 느려지는지 등을 확인



## 네트워크 프로토콜

다른 장치들끼리 데이터를 주고받기 위해 설정된 공통된 인터페이스

- IEEE 또는 IETF라는 표준화 단체가 프로토콜을 정함
