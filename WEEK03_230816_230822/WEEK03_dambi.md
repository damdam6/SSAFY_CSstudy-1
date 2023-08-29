# CS 2장 네트워크(2)


# 2장 네트워크

## 2.2 TCP/IP 4계층 모델

- 인터넷 프로토콜 스위트 internet protocol suite
    - 인터넷에서 컴퓨터들이 서로 정보를 주고받는 데 쓰이는 프로토콜의 집합
    - TCP/IP 4계층 모델
    - OSI 7계층 모델
    
    ⇒ 두 가지 방식으로 설명
    

### 2.2.1 계층 구조

|  | TCP/IP 4계층 | OSI 7계층 |
| --- | --- | --- |
| FTTP/HTTP/SSH/SMTP/DNS  | 애플리케이션 계층 | 애플리케이션 계층 |
|  |  | 프리젠테이션 계층 |
|  |  | 세션 계층 |
| TCP/UDP/QUIC | 전송 계층 | 전송 계층 |
| IP/ARP/ICMP | 인터넷 계층 | 네트워크 계층 |
| 이더넷 | 링크 계층 | 데이터 링크 계층 |
|  |  | 물리 계층 |

→ 특정 계층이 변경되었을 때 다른 계층이 영향을 받지 않도록 설계

- 애플리케이션 계층
    - 응용프로그램이 사용되는 프로토콜 계층
    - 웹 서비스, 이메일 등 서비스를 실질적으로 사람들에게 제공하는 층
    
    - FTP
        - 장치와 장치 간의 파일을 전송하는데 사용되는 표준 통신 프로토콜
    - SSH
        - 보안되지 않은 네트워크에서 네트워크 서비스를 안전하게 운영하기 위한 암호화 네트워크 프로토콜
    - HTTP
        - World Wide Web을 위한 데이터 통신의 기초이자 웹 사이트를 이용하는데 쓰는 프로토콜
    - SMTP
        - 전자 메일 전송을 위한 인터넷 표준 통신 프로토콜
    - DNS
        - 도메인 이름과 IP주소를 매핑해주느 서버
        - IP 주소가 바뀌어도 사용자들에게 똑같은 도메인 주소로 서비스 가능함.

- 전송 계층
    - 송신자와 수신자를 연결하는 통신 서비스를 제공하며 연결 지향 데이터 스트림 지원, 신뢰성, 흐름 제어를 제공할 수 있음
    - 애플리케이션과 인터넷 계층 사이의 데이터가 전달될 때 중계 역할
    - TCP : 패킷 사이의 순서를 보장하고 연결지향 프로토콜을 사용해서 연결을 하여 신뢰성을 구축해서 수신 여부를 확인하며 가상회선 패킷 교환 방식을 사용
    - UDP : 순서를 보장하지 않고 수신 여부를 확인하지 않으며 단순히 데이터만 주는 ‘데이터그램 패킷 교환 방식’을 사용
    
    - **가상회선 패킷 교환 방식**
        - 각 패킷에는 가상회선 식별자 포함 → 모든 패킷을 전송하면 가상회선 해제 → 패킷은 전송된 ‘순서대로’ 도착하는 방식
    - **데이터그램 패킷 교환 방식**
        - 패킷이 독립적으로 이동하며 최적의 경로를 선택하여 감
        - 하나의 메시지에서 분할된 여러 패킷 → 서로 다른 경로로 전송될 수 있음 → 도착한 ‘순서가 다를 수’ 있는 방식
        
    - **TCP 연결 성립 과정**
        - 3-웨이 핸드셰이크
            - SYN (연결 요청 플래그)
                - 클라이언트 → 서버 : 클라이언트의 ISN을 담아 SYN을 보냄
                - ISN은 새로운 TCP연결의 첫번째 패킷에 할당된 임의으 시퀀스 번호(장치마다 다름)
            - SYN + ACK
                - 서버는 클라이언트의 SYN을 수신
                - 서버의 ISN을 보냄 → 승인번호로 클라이언트의 ISN+1을 보냄
            - ACK (응답 플래그)
                - 클라이언트는 서버의 ISN+1한 값인 승인번호를 담아 ACK를 서버에 보냄
    - **TCP 연결 해제 과정**
        - TCP가 연결을 해제할 때 → 4-웨이 핸드셰이크 과정
            1. FIN으로 설정된 세그먼트(클라이언트가 연결을 닫으려고 할때)
                - 클라이언트 = FIN_WAIT_1 상태
            2. 서버 → 클라이언트 : ACK라는 승인 세그먼트를 보냄
                - 서버 = FIN_WAIT_2 상태
            3. 서버 → ACK를 보내고 일정시간 후 클라이언트 → FIN세그먼트 보냄.
            4. 클라이언트 = TIME_WAIT → 다시 서버로 ACK를 보냄
                - 서버 CLOSED 상태가 됨
                - 이후 클라이언트는 일정 시간 후 연결이 닫힘 - 모든 자원의 연결 해제됨
    
- 인터넷 계층
    - 장치로부터 받은 네트워크 패킷을 IP 주소로 지정된 목적지로 전송하기 위해 사용되는 계층
    - IP, APR, ICMP 등이 있음
    - 패킷을 수신해야 할 상대의 주소를 지정하여 데이터를 보냄
- 링크 계층
    - 전선, 광섬유, 무선 등 → 실질적 데이터 전달
    - 장치간의 신호를 주고 받는 ‘규칙’을 정하는 계층 (==네트워크 접근 계층)
    - 두 개로 분리
        - 물리 계층 : 무선 LAN, 유선 LAN을 통해 0과 1보냄
        - 데이터 링크 계층 : 이더넷 프레임을 통해 에러 확인, 흐름 제어, 접근 제어 담당
- 유선 LAN(IEEE802.3)
    - IEEE802.3 프로토콜을 따름
    - 전이중화 통신 사용
        - 전이중화 통신 full duplex
            - 양쪽 장치가 동시에 송수신 할 수 있는 방식
            - 송신로와 수신로로 나눠서 데이터를 주고 받음 → 현대의 고속 이더넷
    - CSMA/CD
        - 이전에 사용한 반이중화 통신 중 하나
        - 데이터를 보낸 이후 충돌이 발생하면 일정 시간 이후 재전송
        - 한 경로를 기반으로 데이터를 보내서 → 충돌에 대비해야 했음.
    - 유선LAN을 이루는 케이블
        - TP 케이블 = 트위스트 페어 케이블
            - 여덟 개의 구리선을 두 개씩 꼬아서 묶은 케이블
            - 실드처리하지 않고 덮은 UTP / 실드 처리하고 덮은 STP
                - 자주 보는 LAN케이블 : UTP케이블
        - 광섬유 케이블
            - 광섬유로 만든 케이블
            - 레이저를 이용하여 통신 - 구리선과 비교 불가능한 장거리 고속 통신이 가능
            - 100Gbps의 데이터를 전송
            - 내부와 외부를 다른 밀도를 가지는 유리나 플라스틱 섬유로 제작 → 반사해서 계속 앞으로 감
- 무선 LAN(IEEE802.11)
    - 수신과 송신에 같은 채널 사용 → 반이중화 통신 half duplex
    - 반이중화 통신
        - 양쪽 장치는 서로 통신 가능 but 동시 통신 불가(한번에 한방향만)
            - 장치가 신호를 수신하기 시작하면 응답하기 전에 전송완료를 기다려야 함
        - CSMA
            - 반 이중화 통신 중 하나
            - 장치에서 데이터를 보내기 전에 캐리어 감지 등으로 사전에 가능한 충돌을 방지하는 방식
            1. 데이터를 송신하기 전에 무선 매체를 살핌
            2. 캐리어 감지 : 회선이 비어있는지 판단
            3. IFS(Inter FrameSpace) : 랜덤 값을 기반으로 정해진 시간만큼 기다림 - 무선 매체가 사용 중이면 점차 그 간격을 늘려가면서 기다림
            4. 이후 데이터 송신
    - 무선LAN을 이루는 주파수
        - Wireless Local Area Network : 무선 전달 방식을 이용하여 2대 이상의 장치를 연결하는 기술
        - 주파수 대역 : 2.4GHz or 5GHz
            - 2.4 : 장애물에 강하나, 전자레인지 무선 등 전파 간섭
            - 5 : 채널 수도 많고 동시 사용 가능 → 상대적으로 깨끗한 전파 환경
    - 와이파이
        - 무선 LAN 신호에 연결할 수 있게 하는 기술
        - 무선 접속 장치 AP (공유기)
        
        ⇒ 이외의 무선LAN : 지그비, 블루투스 등
        
    - BSS
        - Basic Service Set 기본 서비스 집합
        - BSS 내에 있는 AP들과 장치들이 서로 통신이 가능한 구조를 말함
    - ESS
        - Extended Service Set 하나 이상의 연결된 BSS 그룹
        - 장거리 무선 통신 제공
        - BSS보다 더 많은 가용성과 이동성 지원
- 이더넷 프레임
    - 링크 계층 : 이더넷 프레임을 통해 전달받은 데이터의 에러를 검출하고 캡슐화함
        
        Preamble(7바이트) → SFD(1바이트) → DMAC(6바이트) → SMAC(6바이트) → EtherType(2바이트) → Payload → CRC(4바이트)
        
        - Preamble 이더넷 프레임의 시작
        - SFD start fram delimiter : 다음 바이트부터 MAC 주소 필드가 시작됨
        - DMAC, SMAC 수신, 송신 MAC 주소를 말함
            - MAC 주소 : LAN카드의 식별번호 - 6바이트
        - EtherType : 데이터 계층 위의 계층인 IP 프로토콜 정의
        - Payload : 전달받은 데이터
        - CRC : 에러 확인 비트

- 계층 간 데이터 송수신 과정
    - 캡슐화
        - 상위 계층의 헤더와 데이터를 하위 계층의 데이터 부분에 포함시키고 해당 계층의 헤더를 삽입하는 과정
        
        | 애플리케이션 → 전송계층 | 세그먼트 or 데이터그램화 |
        | --- | --- |
        | → 인터넷 계층 | IP(L3)헤더 ⇒ 패킷화 |
        | → 링크 계층 | 프레임 헤더, 프레임 트레일러 ⇒ 프레임화 |
    - 비캡슐화
        - 하위 계층에서 상위 계층으로 가며 각 계층의 헤더 부분을 제거하는 과정
        - 캡슐화와 반대 개념
    

---

### 2.2.2 PDU

- PDU
    - 네트워크의 계층에서 계층으로 데이터가 전달될 때 한 덩어리의 단위
    - 헤더 : 제어 관련 정보를 포함
    - 페이로드 : 데이터
    - 계층마다 부르는 명칭이 다름
        - 메시지
        - 세그먼트(TCP) 데이터그램(UDP)
        - 패킷
        - 프레임(데이터링크계층) 비트(물리계층)

---

## 2.3 네트워크 기기

### 2.3.1 네트워크 기기의 처리 범위

- 계층 별로 처리 범위를 나눌 수 있음
    - 애플리케이션 계층 : L7스위치
    - 인터넷 계층 : 라우터 L3스위치
    - 데이터 링크 계층 : L2스위치, 브리지
    - 물리 계층 : NIC, 리피터, AP

### 2.3.2 애플리케이션 계층을 처리하는 기기

- L7 스위치
    - 여러 장비를 연결하고 데이터 통신을 중재 → 목적지가 연결된 포트로만 전기 신호를 보내 데이터를 전송하는 통신 네트워크 장비
    - 로드밸런서 → 서버의 부하를 분산하는 기기
    - URL 서버 캐시 쿠키들을 기반으로 트래픽 분산 → 바이러스, 불필요한 외부 데이터 등을 걸러내는 필터링 기능
- L4스위치 L7스위치
    - L4 스위치
        - 전송 계층을 처리 하는 기기
        - 스트리밍 관련 서비스에서는 사용할 수 없음 / 메시지 기반으로 인식 하지 못하고 IP와 포트 기반으로 트래픽 분산
    - L7 스위치
        - IP와 포트 외에도 URL, HTTP 헤더, 쿠키 등을 기반으로 트래픽 분산
    - 클라우드 서비스 등에서
        - L7 스위치의 로드밸런싱 - ALB(application load balancer) 컴포넌트
        - L4 스위치의 로드밸런싱 - NLB(Network Load Balancer)컴포넌트
- 헬스 체크
    - 정상 서버 또는 비정상 서버 판별
    - 전송 주기와 재전송 횟수 등을 설정한 후 반복적으로 서버에 요청을 보내는 것
    - 서버가 부하되지 않도록 요청 횟수가 적절해야
- 로드밸런서를 이용한 서버 이중화
    - 서버 이중화 : 2대 이상의 서버를 기반으로 가상의 IP제공 → 안정적인 서비스 제공
    

---

### 2.3.3 인터넷 계층을 처리하는 기기

- 라우터
    - 여러 개의 네트워크를 연결, 분할, 구분시켜주는 역할
    - 다른 네트워크에 존재하는 장치끼리 서로 데이터를 주고 받을 때 패킷 소모를 최소화하고 경로를 최적화하여 최소 경로로 패킷을 포워딩
- L3 스위치
    - L2스위치의 기능과 라우팅 기능을 갖춘 장비
    - 하드웨어 기반의 라우팅을 담당하는 장치

---

### 2.3.4 데이터 링크 계층을 처리하는 기기

- L2 스위치
    - 장치들의 MAC 주소를 MAC주소테이블을 통해 관리 → 연결된 장치로부터 패킷이 왔을 때 패킷 전송 담당
    - 브리지
        - 두 개의 근거리 통신망을 상호 접속할 수 있도록 하는 통신망 연결 장치
        - 포트와 포트 사이의 다리 역할

---

### 2.3.5 물리 계층을 처리하는 기기

- NIC
    - LAN 카드
    - 네트워크 인터페이스 카드
- 리피터
    - 들어오는 약하신 신호를 증폭하여 다른 쪽으로 전달하는 장치
    - 현재는 잘 안쓰임(광케이블이 생겨서)
- AP
    - Access Point
    - 패킷을 복사하는 기기