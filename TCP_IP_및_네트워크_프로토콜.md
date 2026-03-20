# TCP/IP 및 네트워크 프로토콜

## TCP/IP

인터넷에 연결된 서로 다른 기종의 컴퓨터들 간에 데이터를 주고받을 수 있도록 하는 표준 프로토콜. **TCP 프로토콜 + IP 프로토콜**로 구성.

### TCP (Transmission Control Protocol)

OSI 7계층의 **전송계층**에 해당한다. 신뢰성 있는 연결형 서비스를 제공하며, 패킷의 다중화, 순서 제어, 오류 제어, 흐름 제어 기능을 제공한다.

### IP (Internet Protocol)

OSI 7계층의 **네트워크 계층**에 해당한다. 데이터 그램을 기반으로 하는 비연결형 서비스를 제공하며, 패킷의 분해/조립, 주소지정, 경로선택 기능을 제공한다.

### 연결형 통신 (접속)

송·수신측 간을 논리적으로 연결한 후 데이터를 전송하는 **가상회선 방식**.

### 비연결형 통신 (비접속)

송·수신측 간에 논리적 연결 없이 데이터를 전송하는 **데이터그램 방식**.

---

## TCP/IP 계층 구조

| OSI 계층 | TCP/IP 계층 | 기능 |
|---|---|---|
| 응용 계층 | | 응용 프로그램 간의 데이터 송·수신 제공 |
| 표현 계층 | 응용 계층 | TELNET, FTP, SMTP, SNMP, DNS, HTTP 등 |
| 세션 계층 | | |
| 전송 계층 | 전송 계층 | 호스트들 간의 신뢰성 있는 통신 제공. TCP, UDP, RTCP, DCCP |
| 네트워크 계층 | 인터넷 계층 | 데이터 전송을 위한 주소지정, 경로 선정. IP, ICMP, IGMP, ARP, RARP, IPSec |
| 데이터 링크 계층 | 네트워크 엑세스 계층 | 실제 데이터를 송수신하는 역할. Ethernet, IEEE802, HDLC, ARQ 등 |
| 물리 계층 | | |

---

## 주요 프로토콜

### HTTP (HyperText Transfer Protocol)

웹에서 HTML로 작성된 하이퍼텍스트 문서를 전송하기 위한 표준 프로토콜. 1989년 버너스리(Berners-Lee)가 WWW를 고안하면서 설계.

- **HTTPS**: HTTP의 단점을 보완하고 안전한 통신을 위해 3-way handshake 방식을 사용해 보안을 강화한 버전. SSL/TLS 인증, 암호화 기능 지원.

### TELNET

멀리 연결되어 있는 컴퓨터에 접속하여 자신의 컴퓨터처럼 사용할 수 있게 해주는 서비스. 시스템 관리 작업을 할 수 있는 가상의 터미널 기능을 수행.

### FTP (File Transfer Protocol)

컴퓨터와 컴퓨터 또는 컴퓨터와 인터넷 사이에서 파일을 주고받을 수 있도록 하는 원격 파일 전송 프로토콜.

### SMTP (Simple Mail Transfer Protocol)

전자 우편을 교환하는 서비스.

### SNMP (Simple Network Management Protocol)

TCP/IP의 네트워크 관리 프로토콜. 라우터나 허브 등 네트워크 기기의 네트워크 정보를 네트워크 관리 시스템에 보내는 데 사용되는 표준 통신 규약.

### DNS (Domain Name System)

문자 상태의 도메인 네임을 숫자로 된 IP 주소로 매핑하는 시스템.

### SSH (Secure Shell)

다른 네트워크상의 컴퓨터에 원격 접속하거나 파일을 복사할 수 있게 해주는 응용 프로토콜. **22번 포트** 사용.

### UDP (User Datagram Protocol)

데이터 전송 전에 연결을 설정하지 않는 비연결형 서비스 제공. TCP에 비해 상대적으로 단순한 헤더 구조를 가져 오버헤드가 적고, 흐름제어나 순서제어가 없어 전송 속도가 빠름.

### RTCP (Real-Time Control Protocol)

RTP 패킷의 전송 품질을 제어하기 위한 제어 프로토콜. 데이터 전송을 모니터링하고 최소한의 제어와 인증 기능만을 제공.

### ICMP (Internet Control Message Protocol)

IP와 조합하여 통신 중에 발생하는 오류의 처리와 전송 경로 변경 등을 위한 제어 메시지를 관리하는 역할. 헤더는 8 Byte로 구성.

### IGMP (Internet Group Management Protocol)

멀티캐스트를 지원하는 호스트나 라우터 사이에서 멀티캐스트 그룹 유지를 위해 사용.

### Ping

특정 호스트가 현재 네트워크에 연결되어 정상적으로 작동하고 있는지 알아보는 서비스. ICMP를 사용하여 특정 호스트로의 연결 가능 여부를 확인.

---

## 주요 프로토콜 3

### ARP (Address Resolution Protocol)

호스트의 IP 주소를 호스트와 연결된 네트워크 접속 장치의 물리적 주소(MAC)로 변환.

### RARP (Reverse Address Resolution Protocol)

ARP와 반대로 물리적 주소(MAC)를 IP 주소로 변환하는 기능.

### DHCP (Dynamic Host Configuration Protocol)

IP 주소 부족 문제를 해결하기 위해 만들어진 프로토콜. IP 주소가 일정한 시간 동안 유효하도록 임대함으로써, 사용 가능한 IP 주소의 개수보다 더 많은 컴퓨터가 IP 주소를 활용할 수 있음.

### IPSec (IP Security)

네트워크 계층에서 암호화 기술을 이용하여 IP 패킷 단위의 데이터 변조 방지 및 은닉 기능을 제공하는 프로토콜.

### DCCP (Datagram Congestion Control Protocol)

메시지 지향적인 전송 계층 통신 프로토콜. UDP 기반에서 최소한의 혼잡 제어 기능을 가진 새로운 전송 프로토콜.

