---
title: "15. 네트워크"
nav_order: 21
layout: default
---


# 15. 네트워크

## 네트워크란?

* 네트워크는 두 대 이상의 컴퓨터나 장치가 데이터를 주고받을 수 있도록 연결된 시스템이다.
* 정보 공유, 자원 공유, 통신 등의 목적으로 사용된다.


## IP 주소 (IP Address)

* 인터넷에 연결된 모든 장치에는 고유한 IP 주소가 부여된다.

### IP 주소 체계

* **IPv4**: 32비트 주소. 예: `192.168.0.1`
* **IPv6**: 128비트 주소. 예: `2001:0db8::0370:7334`

### 공인 IP와 사설 IP

* **공인 IP**: ISP가 할당하며 전 세계에서 유일한 주소.
* **사설 IP**: 로컬 네트워크 전용 주소. 아래와 같은 대역이 예약되어 있다.

| 사설 IP 대역         | 비고      |
| ---------------- | ------- |
| `10.0.0.0/8`     | Class A |
| `172.16.0.0/12`  | Class B |
| `192.168.0.0/16` | Class C |

* 사설 IP는 NAT(Network Address Translation)를 통해 공인 IP로 변환되어 외부와 통신한다.


## 포트 (Port)

* 하나의 IP 주소에서 여러 서비스가 동작할 수 있도록 구분해주는 논리적 번호이다.
* 포트 번호는 0부터 65535까지 사용 가능하다.

| 포트 범위       | 설명                    | 예시                            |
| ----------- | --------------------- | ----------------------------- |
| 0–1023      | Well-known ports      | 22(SSH), 80(HTTP), 443(HTTPS) |
| 1024–49151  | Registered ports      | 사용자 정의 서비스                    |
| 49152–65535 | Dynamic/private ports | 임시 연결 등에 사용                   |


## DNS (Domain Name System)

* 사람이 이해할 수 있는 도메인 이름을 IP 주소로 변환하는 시스템이다.

예: `www.google.com` → `142.250.206.68`


## 프로토콜 (Protocol)

* 네트워크 통신을 위한 약속(규약)이다.

| 프로토콜      | 설명                   |
| --------- | -------------------- |
| **TCP**   | 연결 기반. 신뢰성 있는 데이터 전송 |
| **UDP**   | 비연결. 빠른 전송 (예: 스트리밍) |
| **HTTP**  | 웹 페이지 전송용 프로토콜       |
| **HTTPS** | 보안이 적용된 HTTP         |
| **FTP**   | 파일 전송용 프로토콜          |
| **SMTP**  | 이메일 전송용 프로토콜         |
| **SSH**   | 안전한 원격 접속            |
| **SCP**   | SSH 기반 파일 전송         |


## 네트워크 정보 확인 명령어


### 1. `ifconfig`

* 네트워크 인터페이스의 상태 및 IP 정보를 확인한다.

```bash
ifconfig
```

예시 출력:

```text
eth0      Link encap:Ethernet  HWaddr 00:0c:29:6b:57:ad
          inet addr:192.168.1.10  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::20c:29ff:fe6b:57ad/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500
          RX packets:12345  TX packets:12345
```

> 주요 항목
>
> * `inet addr`: IPv4 주소
> * `inet6 addr`: IPv6 주소
> * `HWaddr`: MAC 주소
> * `RX/TX packets`: 수신/송신 패킷 정보



### 2. `ip addr`

* 현대적인 네트워크 설정 확인 명령어.

```bash
ip addr show
```

예시 출력:

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    link/ether 00:0c:29:6b:57:ad brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.10/24 brd 192.168.1.255 scope global dynamic eth0
    inet6 fe80::20c:29ff:fe6b:57ad/64 scope link
```

> 주요 항목
>
> * `inet`: IPv4 주소
> * `inet6`: IPv6 주소
> * `link/ether`: MAC 주소
> * 상태 플래그: `UP`, `LOWER_UP`, `MULTICAST` 등



### 3. `netstat`

* 현재 열려 있는 포트, 네트워크 연결 상태 등을 확인한다.

```bash
netstat -tuln
```

예시 출력:

```text
Proto Recv-Q Send-Q Local Address   Foreign Address   State
tcp   0      0      0.0.0.0:22      0.0.0.0:*         LISTEN
udp   0      0      0.0.0.0:68      0.0.0.0:*
```

> 주요 항목
>
> * `Proto`: 프로토콜
> * `Local Address`: 자신의 IP 및 포트
> * `State`: 연결 상태 (`LISTEN`, `ESTABLISHED` 등)



### 4. `ping`

* 네트워크 대상 호스트에 도달 가능한지 확인한다.

```bash
ping 8.8.8.8
```

> 종료: `Ctrl + C`

예시 출력:

```text
64 bytes from 8.8.8.8: icmp_seq=1 ttl=56 time=23.4 ms
```

> * `icmp_seq`: 전송 횟수
> * `ttl`: Time to Live
> * `time`: 응답 속도(ms)



### 5. `traceroute`

* 목적지까지 가는 경로(홉)를 추적한다.

```bash
traceroute 8.8.8.8
```

예시 출력:

```text
1  192.168.1.1  1.123 ms
2  10.0.0.1     2.345 ms
3  8.8.8.8      23.456 ms
```

> * 각 줄은 하나의 라우터(홉)를 의미
> * 지연 시간(ms)을 통해 네트워크 병목을 추적할 수 있다



### 6. `telnet`

* 특정 IP와 포트로 접속이 가능한지 확인하는 데 사용한다.

```bash
telnet [호스트] [포트]
```

> 종료: `Ctrl + ]` → `quit`

예:

```bash
telnet 8.8.8.8 53
```

## 참고

[번외] [네트워크 용어 정리](extra/network.md)
