---
layout: post
title: HTTP and Network Basic chapter.1
description: "웹과 네트워크 기본"
categories: BookReader
image: roon3.jpeg
---

## 기본적인 웹 통신 과정
브라우저 (Client) 에서 URL을 입력하여 목적지 (Server)로 송신.   
Server에서 응답이 돌아오면 웹 페이지가 표시 됨.

## HTTP
HyperText Transfer Protocol   
클라이언트에서 서버까지 웹 통신 일련의 흐름을 결정

---

## 네트워크의 기본은 TCP/IP

### Protocol
규칙. 규약. 서로 다른 하드웨어나 운영체제 등을 가지고 통신을 하기 위해 필요한 규칙.

### TCP/IP
인터넷 통신과 관련된 프로토콜의 집합.   
다음과 같은 4개 레이어로 나뉘어져 있다.   
* Application Layer
* Transport Layer
* Datalink Layer
* Link Layer

#### Application Layer
애플리케이션에서 사용하는 통신 움직임을 결정   
FTP, DNS, HTTP 등을 말함

#### Transport Layer
네트워크에 접속되어 있는 컴퓨터 간의 데이터 흐름을 제공   
TCP (Transmission Control Protocol)   
UDP (User Data Protocol)

#### Network Layer
네트워크상에서 패킷 이동을 담당함   
어떤 경로를 거쳐 상대의 컴퓨터까지 패킷을 보낼지 결정   

* `패킷` 전송하는 데이터의 최소 단위

#### DataLink Layer
네트워크에 접속하는 하드웨어적인 면을 다룬다.   

### TCP/IP 통신의 흐름
![TCP/IP 통신의 흐름]({{ site.baseurl }}/content/images/BookReader/2015-11-23-23-05-http.jpeg)

---

## HTTP와 관계가 깊은 TCP/IP/DNS

### 배송을 담당하는 IP
_IP (Internet Protocol)_   
인터넷을 사용하는 거의 대부분의 시스템이 IP를 사용.   
패킷을 상대방에게 전달하는 단순한 역할을 가지고 있음.   

_MAC (Media Access Control address)_    
각 네트워크 카드(디바이스)에 할당된 고유 주소. 변경 할 수 없음.

__통신은 ARP를 이용하여 MAC 주소에서 진행 된다.__   
IP 통신은 MAC 주소에 의존해서 통신한다.   
네트워크 통신을 진행할 때 MAC주소를 사용하여 패킷의 목적지를 찾아 전송하는데,   
이 때 수신지의 IP 주소를 바탕으로 MAC 주소를 찾기 위해 ARP가 사용된다.

_ARP (Address Resolution Protocol)_   
IP주소를 바탕으로 해당 IP주소가 가르키는 MAC 주소를 알려줌

### 신뢰성 있는 전송을 담당하는 TCP
_TCP (Transfer Control Protocol)_   
신뢰성 있는 바이트 스트림 서비스를 제공.   
용량이 큰 데이터 패킷을 TCP Segment라 불리는 단위 패킷으로 작게 분해해서 관리한다.   
대용량의 데이터를 보내기 쉽게 작게 분해하여 상대방에게 보내고 그것이 정확히 도착했는지 확인하는 역할을 수행.

TCP통신은 3-way handshake로 이루어진다.   
SYN - SYN/ACK - ACK 로 패킷 전송을 준비한 뒤 데이터를 전송한다.   

### 이름을 담당하는 DNS
_DNS (Domain Name System)_   
Application Layer에서 도메인 이름과 IP 주소 이름 확인을 담당한다.   
사용자가 쉽게 알아볼 수 없는 IP 주소 대신 영어나 숫자를 사용하여 명확하게 제공하는 주소가 바로 Domain이다.   
하지만, 컴퓨터는 숫자로 이루어진 IP 주소를 더 쉽게 이해하므로 DNS가 그 중간에서 IP와 Domain을 연결하는 역할을 담당한다.   
클라이언트가 DNS에게 Domain을 넘기면, DNS는 해당하는 Domain의 IP 주소를 찾아 되돌려준다.   
이를 받은 클라이언트는 해당 IP 주소로 통신을 시작하는 것이다.

---

## URI와 URL

### URI
_Uniform Resource Identifier_   
통합 리소스 구분자.   
스키마를 나타내는 리소스를 식별하기 위한 식별자.   
리소스를 식별하기 위한 문자열 전체를 나타냄.   

* 스키마 : 리소스를 얻기 위한 수단에 이름을 붙이는 방법.   
ex) http, ftp, mailto, telnet 등

### URL
_Uniform Resource Locator_   
리소스가 위치한 경로를 나타내는 URI   

* 절대 URL   
`http://user:pass@www.example.com:80/dir/index.htm?uid=1` 과 같이 전체적인 절대 경로를 표현하는 URL

* 상대 URL   
`*/image/log.gif` 와 같이 root directory를 기준으로 리소스가 위치한 곳을 상대 주소로 표현하는 URL
