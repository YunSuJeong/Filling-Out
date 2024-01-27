
# 계층별 프로토콜 종류 및 특징

[OSI 7계층 개념 정리](https://github.com/YunSuJeong/BOOK/blob/main/network/%EB%AA%A8%EB%91%90%EC%9D%98%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC(Network%20for%20everyone)/chap2.%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%20%EA%B8%B0%EB%B3%B8%EA%B7%9C%EC%B9%99.md)

## 7. Application Layer 
### HTTP(HyperText Transfer Protocol)
  - WWW(World Wide Web) 상에서 정보를 주고 받을 수 있는 프로토콜  
  - 주로 HTML문서를 주고 받는 데에 쓰임  
  - TCP와 UDP를 사용  
  - 80번 포트 사용  
### SMTP(Simple Mail Transfer Protocol)
  - 인터넷에서 이메일을 보내고 받기 위해 이용되는 프로토콜  
  - TCP 포트번호 25번 사용  
### FTP(File Transfer Protocol)
  - 컴퓨터 간 파일을 전송하는데 사용되는 프로토콜  
  - 데이터 전달 : 20번포트  
  - 제어정보전달 : 21번포트  
### TELNET
  - 인터넷이나 로컬 영역 네트워크 연결에 쓰이는 네트워크 프로토콜  
  - IETF STD 8로 표준화  
  - 보안문제로 사용이 감소하고 있으며, 원격제어를 위해 SSH로 대체  

## 6. Presentation Layer
### SSL(Secure Socket Layer)
  - 인증, 암호화, 무결성 보장하는 프로토콜  
  - 네트워크 레이어의 암호화 방식  
  - HTTP 뿐만 아니라, NNTP, FTP 등에도 사용  
### ASCII(American Standard Code for Information Interchange)
  - 문자를 사용하는 많은 장치에서 사용되며, 대부분의 문자 인코딩이 아스키에 기반  
  - 7비트 인코딩, 33개의 출력 불가능한 제어 문자들과 공백을 비롯한 95개의 출력 가능한 문자  
    
## 5. Session Layer
### NetBIOS
  - 네트워크의 기본적인 입출력을 정의한 규약  
### RPC(Remote Procedure Call)
  - Windows 운영 체제에서 사용하는 원격프로시저 호출 프로토콜  
### WinSock(Windows Socket)
  - 유닉스 등에서 TCP/IP 통신시 사용하는 Socket을 Windows에서 그대로 구현한 것  
    
## 4. Transport Layer
### TCP(Transmission Control Protocol)
  - 전송제어프로토콜, 네트워크의 정보전달을 통제하는 프로토콜  
  - 데이터의 전달을 보증하고 보낸 순서대로 받게 해줌  
  - 3 Way Handshaking와 4 Way Handshaking 등을 활용한 신뢰성 있는 전송 가능  
### UDP(User Datagram Protocol)
  - 비연결성이고 신뢰성이 없음  
  -  순서화되지 않은 Datagram 서비스 제공  
  -  TCP는 신뢰성이 낮은 프로그램에 적합  
    
## 3. Network Layer
### IP(Internet Protocol)
  - 패킷 교환 네트워크에서 정보를 주고받는데 사용하는 정보 위주의 규약  
  - 호스트의 주소지정과 패킷 분할 및 조립 기능을 담당  
### ICMP(Internet Control Message Protocol)
  - TCP/IP에서 IP 패킷을 처리할 때 발생되는 문제(오류 보고)를 알림  
  - 진단 등과 같이 IP계층에서 필요한 기타 기능들을 수행하기 위해 사용되는 프로토콜  
### IGMP(Internet Group Management Protocol)
  - IP 멀티캐스트를 실현하기 위한 통신 프로토콜  
  - PC가 멀티캐스트로 통신할 수 있다는 것을 라우터에 통지하는 규약  

## 2. Data Link Layer
### Ethernet
  - 비연결성(connectionless)모드, 전송속도 10Mbps 이상, LAN 구현 방식을 말함  
### HDLC(High-Level Data-Link Control)
  - 비트 전송을 기본으로 하는 범용의 데이터 링크 전송제어절차  
  - 고속 데이터 전송에 적합  
### PPP(Point-to-Point Protocol)
  - 전화선 같이 양단간 비동기 직렬 링크를 사용하는 두 컴퓨터간의 통신을 지원하는 프로토콜  

## 1. Physical Layer
### RS-232
  - 보통 15m이하 단거리에서 38400bps까지 전송을 위한 직렬 인터페이스  
### X.25
  - 패킷교환망에 대한 엑세스 표  
### X.21
  - 회선교환망에 대한 액세스 표준  
