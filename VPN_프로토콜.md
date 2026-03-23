# VPN 프로토콜

---

## SSL (Secure Sockets Layer) — 전송계층

- 데이터를 송·수신하는 두 컴퓨터 사이에서 위치해 **TCP/IP 계층**과 애플리케이션 계층 사이에서 **인증, 암호화, 무결성**을 보장

---

## IPSec (IP Security) — 네트워크 계층

- 네트워크 계층에서 **IP 패킷 단위**의 데이터 변조 방지 및 은닉 기능 제공 프로토콜

---

## PPTP (Point to Point Tunneling Protocol) — 데이터링크 계층

- **마이크로소프트**가 제안한 VPN 프로토콜
- **PPP (Point to Point Protocol)** 에 기초하며 두 대의 컴퓨터가 직렬 인터페이스를 이용하여 통신

---

## L2F (Layer 2 Forwarding) — 데이터 링크 계층

- 미국 **시스코 시스템즈** 사가 개발한 VPN 프로토콜
- PPTP나 IPSec과 달리 데이터 링크층 수준에서 **캡슐화 가능**, IP 네트워크 이외에서도 이용 가능

---

## L2TP (Layer 2 Tunneling Protocol) — 데이터 링크 계층

- 터널링 프로토콜인 PPTP와 VPN의 구현에 사용하는 **L2F의 기술적 장점 결합**
- 자체적으로 암호화/인증 기능을 제공하지 않아 **다른 보안 프로토콜과 함께 사용**
