## TCP와 UDP
1. TCP의 특징을 설명해 보세요.
- 전송 계층에 속한 네트워크 프로토콜인 TCP는 송신부와 수신부의 연결을 확인하는 연결형 서비스로, 패킷의 수신 여부와 전송 순서를 보장한다. 그리고 패킷 교환 방식으로 가상 회선 방식을 이용하여 정해진 회선으로 패킷이 전송되며 1:1 통신을 한다. TCP는 데이터의 무손실을 보장하므로 신뢰성은 높지만 전송 속도는 느리다. 
2. TCP의 연결 및 해제 과정을 설명해 보세요.
- TCP는 연결을 시작할 때 3-way 핸드 셰이킹을, 해제시 4-way 핸드셰이킹을 한다. 각 핸드셰이킹 과정에서는 다음과 같이 플래그 값을 주고 받는다. 데이터를 주고받기 전 상대방 컴퓨터와 세션을 수립하기 위해 행해지는 3-way 핸드셰이킹에서 송신부는 SYN(N)을 수신부에게 전송하고, 이를 받은 수신부는 ACK(N+1)과 SYN(M)을 송신부에게 전송한다. 송신부가 이를 받으면 수신부에게 ACK(M+1)를 보내고, 이를 수신부가 받으면 연결이 성립한다. 그 다음, 4-way 핸드셰이킹에서 송신부는 FIN을 수신부에게 전송하고, 수신부는 이를 받으면 ACK을 보낸다. 그리고 수신부는 연결을 종료할 준비를 마치면 송신부에게 FIN을 보낸다. 송신부가 이를 받으면 ACK을 보내며 연결이 종료된다.
3. TCP에서 데이터의 신뢰성을 보장하기 위한 방법을 설명해 보세요.
- TCP에서 데이터의 신뢰성을 보장하기 위해 흐름 제어, 혼잡 제어, 오류 제어 방법을 사용한다. 흐름 제어는 수신부와 송신부의 데이터 전송 속도 차이 때문에 발생하는 데이터 손실을 방지하는 방법으로, 수신부로부터 ACK 메시지를 받기 전까지 연결하지 못하는 정지-대기 방식과 수신 여부와 상관 없이 일정 크기의 데이터를 연속적으로 보내는 슬라이딩 윈도우 방식이 있다. 혼잡 제어는 송신부의 데이터 전달 속도와 네트워크의 속도 차이로 데이터 손실이 발생하는 것을 방지하기 위한 방법으로 혼잡 윈도우의 크기를 조절해 혼잡에 대응한다. 오류 제어는 통신 중 데이터에 오류 또는 유실이 발생할 때 데이터의 신뢰성을 보장하기 위해 오류를 제어하는 방식으로, 송신한 패킷에 대한 ACK 메시지를 일정시간 동안 받지 못해 타임아웃이 발생하면 해당 패킷을 다시 보내는 정지-대기 방식과 누락단 데이터가 있을 때 해당 데이터부터 재전송하는 Go-Back-N ARQ 방식, 누락된 데이터만 재정송을 요청하는 Selective-Repeat ARQ 방식이 있다.
4. UDP의 특징을 설명해 보세요.
- UDP는 송신부와 수신부의 연결이 보장되지 않는 비연결형 서비스로, 전송 계층의 네트워크 프로토콜이다. 데이터그램 형태의 통신을 지원하는UDP는 핸드셰이킹 과정 없이 바로 패킷을 송수신하며, 1:1, 1:N, N:N 통신이 가능하다. 패킷 교환 방식으로는 데이터그램 방식을 이용하여 패킷 전송 순서가 보장되지 못한다. 그래서 데이터의 신뢰성은 낮지만 데이터 전송 속도는 빠르다.
5. TCP와 UDP의 차이점을 설명해 보세요.
- TCP는 연결형 서비스지만 UDP는 비연결형 서비스이다. UDP는 핸드셰이킹 과정을 거쳐 세션을 수립한 후 패킷을 전송하는 TCP와 달리 바로 데이터를 전송한다. TCP는 데이터 전송 회선이 정해진 가상회선방식을 이용하여 데이터 전송 순서가 보장되는 반면, UDP는 패킷이 서로다른 회선으로 교환될 수 있는 데이터그램 방식을 이용하므로 데이터의 패킷 순서가 보장되지 못한다.
6. UDP에서 오류 검출 방법을 설명해 보세요.
- UDP는 체크섬을 이용하여 오류를 검출한다. 송신부는 UDP 헤더, IP 헤더의 일부 정보, 데이터를 모두 합하는데 이때 오버플로되는 캐리를  떼서 다시 데이터에 더한 후 1의 보수를 취하여 체크섬 값을 구한다. 그리고 송신부는 이를 UDP 헤더의 체크섬 영역에 넣어 수신부에 전송하고, 이를 받은 수신부는 데이터와 체크섬을 더하여 비트가 모두 1이 나오는지 확인한다.

## HTTP와 HTTPS
7. HTTP에 대해 설명해 보세요.
- HTTP는 응용 계층에서 사용하는 프로토콜로, 서버가 클라이언트의 상태를 저장하지 못하는 무상태와 클라이언트의 요청으로 서버가 응답을 보내면 바로 연결이 끊어지는 비연결성을 특징으로 지닌다.
8. HTTP Keep Alive와 TCP Keep Alive를 설명해 보세요.
- HTTP Keep Alive는 클라이언트가 헤더에 일정 시간 연결 유지 정보를 담아 보내면 클라이언트와 서버 간의 연결을 일정 시간 유지하는 방법이다. TCP Keep Alive은 연결을 원하는 쪽에서 TCP Keep Alive 패킷을 날려 패킷에 대한 응답을 받으면 연결 시간을 처음부터 다시 측정하는 것을 말한다.
9. 쿠키와 세션의 차이점을 설명해 보세요.
- 쿠키는 클라언트 웹 브라우저에 저장하는 데이터이고, 세션은 서버에서 클라이언트와의 연결 정보를 저장하는 것, 쿠키보다 보안에 강하지만 접속자가 많을 경우 서버에 과부하가 올 수 있다.
10. HTTP와 HTTPS의 차이점을 설명해 보세요.
- HTTPS는 HTTP와 달리 보안 계층인 SSL/TLS를 이용하여 보안을 강화하였다.
11. HTTPS에서 사용하는 암호화 방식을 설명해 보세요.
- HTTPS의 암호화 방식으로는 대칭키 암호화 방식과 공개키 암호화 방식이 있다. 대칭키 암호화 방식은 데이터의 암호화와 복호화에 모두 같은 키인 대칭키를 이용하는 반면, 공개키 암호화 방식은 암호화시 공개키를, 복호화시 비밀키를 이용한다.
12. 사용자가 URL을 입력한 후 화면이 출력되기까지의 과정을 설명해 보세요.
- 사용자가 URL을 입력시 DNS 서버에 연결할 IP를 요청하게 되고, DNS는 IP 주소를 웹브라우저에게 응답으로 전송한다. 웹브라우저는 IP를 통해 웹 서버와 TCP/IP연결을 하고 HTTP 요청을 보내며 이를 받은 웹서버는 HTTP 요청에 대한 응답으로 웹페이지와 필요한 리소스를 전송한다. 그리고 웹브라우저는 이를 바탕으로 웹페이지를 보여준다.
13. REST의 장담점을 설명해 보세요.
- REST는 인프라를 구축할 필요가 없다는 장점을 지니지만 정해진 HTTP 메서드를 통해서 자원에 대한 연산을 처리하므로 동작이 한정적이라는 단점을 지닌다.
14. GET에 바디를 넣어서 보내면 나타날 결과를 설명해 보세요.
- GET은 바디가 필요하지 않은 메서드지만, REST API의 서버를 어떻게 구현했는지에 따라 다양한 결과가 나타날 수 있습니다. 첫 번째로 GET에 대한 요청이 왔을 때 바디를 무시하고 자원에 대한 데이터를 Read할 수 있습니다. 두 번째로 GET에 바디를 넣어 요청을 보냈을 때 예외 처리를 할 수 있습니다. 이는 HTTP 메서드의 명시적 사용을 위한 방법입니다. 마지막으로 바디가 있으면 POST와 동일하기 처리하는 경우가 있습니다. 이런 경우에는 데이터를 Read하는 것이 아니라 Create하게 처리합니다.
## 네트워크 프로토콜
15. OSI 7계층과 TCP/IP 4계층의 차이점은 무엇인가요?
- OSI 7계층은 네트워크 통신이 이뤄지는 과정을 7단계로 나눈 네트워크 표준 모델이고, TCP/IP 4계층은 TCP/IP에 맞춰 OSI 7계층을 단순화한 것으로, 인터넷에서 데이터를 주고받기 위한 네트워크 프로토콜이다.
16. HTTP/2를 설명하고 장점 두 가지를 설명하세요.
- 멀티플렉싱을 통하여 단일 연결을 통해 병렬로 여러 요청, 응답 주고 받을 수 있으므로, 특정 스트림의 패킷이 손실되었다고 하더라도 해당 스트림에만 영향을 미치고 나머지 스트림은 멀쩡하게 동작할 수 있다. 허프만 알고리즘을 통하여 헤더를 압축하여 HTTP/1.x와 달리 헤더가 크지 않고, 클라이언트 요청 없이 서버가 바로 리소스를 푸시 가능하다. HTTPS 위에서 작동하므로 전송 계층에서 제공하는 보안 프로토콜을 통하여 클라이언트와 서버가 통신할 때 SSL/TLS를 통해 제3자가 메시지를 도청하거나 변조하지 못하도록 한다.
## 웹 주소 입력
17. www.naver.com을 주소창에 입력하면 어떻게 될까요?
    1. 먼저 리다이렉트가 있다면 리다이렉트를 진행하고 없다면 그대로 해당 요청에 대한 과정이 진행된다.
    2. 캐싱 단계에서는 해당 요청의 캐싱 가능 여부를 파악한다. 캐싱이 이미 된 요청이라면 캐싱된 값을 반환하며, 캐싱이 되지 않은 새로운 요청이라면 그 다음 단계로 넘어간다.
    3. DNS (Domain Name System)은 도메인 구조로 분산된 데이터 베이스를 이용한 시스템으로, FQDN을 인터넷 프로토콜의 IP로 바꿔주는 시스템이다. www.naver.com에 DNS 쿼리가 오면 주소의 역순인  [Root DNS] → [.com DNS]  →  [.naver DNS]  →  [.www DNS] 과정을 거쳐 완벽한 주소(FQDN)를 매핑한다.
    4. 해당 IP를 기반으로 라우팅, ARP 과정을 거쳐 실제 서버를 찾는다.
    5. 브라우저가 TCP 3-way 핸드셰이킹 및 SSL 연결 등을 통해 연결을 설정한다. 이후 요청을 보낸 후 드디어 해당 요청한 서버로부터 응답을 받는다.
    6. 요청한 컨텐츠를 서버로부터 다운 받는다.
    7. 받은 데이터를 바탕으로 브라우저 엔진이 브라우저 렌더링 과정을 거쳐 화면을 만든다.
