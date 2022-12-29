## 📡 네트워크란?

---

<aside>
💡 Net + Work 의 합성어로써 컴퓨터들이 통신 기술을 이용하여 그물망처럼 연결된 통신 이용 형태

</aside>

- 2대 이상의 컴퓨터들을 연결하고 서로 통신(이야기)할 수 있는 것
- 어떤 연결을 통해 컴퓨터의 자원을 공유하는 것
- "몇 개의 독립적인 장치가 적절한 영역내에서 적당히 빠른 속도의 물리적 통신 채널을 통하여 서로가 직접 통신할 수 있도록 지원해 주는 데이타 통신 체계”  by IEEE

### 📌 **네트워크의 종류**

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d84d4635-8bb7-4654-8123-6e7ae501ca0c/Untitled.png)

- **PAN ( Personal Area Network )** : 가장 작은 규모의 네트워크
    
    약 5m 전후의 인접 통신. 예를 들어 아이폰과 맥에서 정보를 공유하는 형태
    
- **LAN ( Local Area Network )** : 근거리 영역 네트워크
    
    상대적으로 짧은 거리에 있는 컴퓨터를 연결. 예를 들어 사무실 , 학원, 병원의 모든 컴퓨터 연결 가능
    
- **MAN (Metropolitan Area Network)** : 대도시 영역 네트워크
    
    일반적으로 도시 및 정부기관이 소유, 관리함
    
- **WAN (Wide Ares Network)** : 광대역 네트워크
    
    지역 간 또는 대륙간의 넓은 지역의 컴퓨터를 연결. 인터넷은 전 세계 수십억 대의 컴퓨터를 연결하는 가장 큰 WAN.
    
- **VAN (Value Added Network)** : 부가가치 통신망 정보의 축적과 제공, 통신속도와 형식의 변화, 통신경로의 선택 등 여러 종류의 정보서비스가 부가된 통신망.

- **ISDN (Integrated Services Digital Network)** : 종합정보 통신망(=BISDN) 전화, 팩스, 데이터 통신, 비디오텍스 등 통신관련 서비스를 종합하여 다루는 통합서비스 디지털 통신망. 디지털 전송방식과 광섬유 케이블 사용. 꿈의 통신망이라 불립니다.

추가적인 네트워크 종류로는 WLAN, SAN, CAN, GAN, VPN, ISDN, Intranet, Extranet..등 분류하게 됩니다.

### 📌 **네트워크의 회선구성 방식**

---

회선 구성 방식은 컴퓨터와 여러대의 단말기들을 연결하는 방식을 말합니다.

- **포인트 투 포인트 방식** : 중앙 컴퓨터와 단말기를 일대일로 연결하여 언제든지 데이터 전송이 가능하게 한 방식입니다.
- **멀티 드롭 방식** : 멀티 포인트 방식이라고도 하며 다수의 단말기들을 한개의 통신 회선에 연결하여 사용하는 방식입니다.
- **회선 다중 방식** : 회선 다중방식은 다중화 방식이라고도 합니다. 여러대의 단말기들을 다중화 장치를 활용하여 중앙 컴퓨터와 연결하여 사용하는 방식입니다.

### 📌 **네트워크의 데이터 교환 방식**

---

- **회선 교환 방식** : 회선 교환 방식은 하며 통신을 원하는 두 지점을 교환기를 이용하여 물리적으로 접속시키는 방법을 말합니다. 음성 전화망이 대표적입니다. (ex. 음성 전화망)
- **공간 분할 교환 방식** : 기계식 접점과 전자교환기의 전자식 접점 등을 이용하여 교환을 수행하는 방식으로, 음성 전화용 교환기가 이에 속합니다. (ex. 음성 전화용 교환기)
- **시분할 교환 방식** : 전자부품이 갖는 고속성과 디지털 교환 기술을 이용하여 다수의 디지털 신호를 시분할적으로 동작시켜 다중화하는 방식을 말합니다.

### 📌 **네트워크 통신 방식**

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c52fec72-59ef-45e9-a578-77718b8758da/Untitled.png)

- 유니 캐스트 : 네트워크에 다수의 대상이 있을 때 그중 특정 대상이랑만 `1:1` 통신하는 방법
- 멀티 캐스트 : 네트워크에 다수의 대상이 있을 때, 그중 특정 대상들이랑만 `1:N` 통신하는 방법
- 브로드 캐스트 : 네트워크에 다수의 대상이 있을 때, 그 모든 대상과 통신하는 방법 `1:ㅈ`
- `ALL`

## 📡 OSI 7계층

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d886dced-3324-4d91-aeba-cbbb717dcb4f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2fca06c5-18ac-47ea-a0bb-cdde5e182244/Untitled.png)

### Layer 1. 물리계층 (Physical Layer)

---

<aside>
💡 0과 1로 되어있는 데이터를 전기신호로 바꿔주는 계층

</aside>

- 사용되는 통신 단위는 `**비트(bit)**`이며 이것은 1과 0으로 나타내어진다.
- 물리 계층에서는 주로 전기적, 기계적, 기능적인 특성을 이용하여 통신 케이블로 데이터를 전송한다.
- 단지 데이터를 전기적인 신호로만 변환해서 주고받는 기능만 한다.
    - 장비로는 **"통신 케이블", "리피터", "허브"**가 있다.
- 데이터 전송만 하고 어떤 에러가 있는지 신경 쓰지 않는다.
- 네트워크의 기본 네트워크로 하드웨어 전송 기술을 이룬다.(리피터, 케이블, 허브)
- 단지 데이터를 전기적인 신호로 변환해서 주고받는 기능을 진행(즉, 데이터를 전송하는 역할만 한다.)
- 논리 데이터 구조(높은 수준의 기능)를 기초로 하는 필수 계층이다.

### Layer 2. 데이터 링크 계층 ( DataLink Layer)

---

- 전송 단위는 `**Frame**`이다.(**프레임에 Mac 주소를 부여**하고 **에러검출, 재전송, 흐름제어** 진행)
- Point to Point 간 신뢰성있는 전송을 보장하기 위한 계층으로 CRC 기반의 **오류 제어**와 **흐름 제어**가 필요하다.
- 물리 계층으로 송수신되는 정보를 관리하여 안전하게 전달되도록 도와주는 역할
    - 장비로는 **“브릿지, 스위치”**가 있다.
- 데이터 링크 계층의 가장 잘 알려진 예는 이더넷이다.
- **주소 값을 물리적으로 할당**받는다.
- **Mac 주소**를 통해 통신한다.

### Layer 3. 네트워크 계층 (Network Layer)

---

<aside>
💡 **경로를 선택하고 IP주소를 정하고 경로에 따라 패킷을 전달(라우팅)해주는 계층**

</aside>

- 전송 단위는 `**Datagram (Packet)**`이다.
- 즉, 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능 (라우터, IP)
- **라우팅, 흐름 제어, 오류 제어, 세그멘테이션** 등을 수행한다.
- 에러 검사 X : 이미 DataLink 에서 하기 때문
- 라우터를 통해 이동할 경로를 선택하여 IP 주소를 지정하고, 해당 경로에 따라 패킷을 전달
- IP(논리적인 주소 구조)를 할당해 주는 역할
- 여러 개의 노드를 거칠 때마다 경로를 찾아주는 역할을 하는 계층으로 다양한 길이의 데이터를 네트워크들을 통해 전달하고, 그 과정에서 전송 계층이 요구하는 서비스 품질(QoS)를 제공하기 위한 기능적, 절차적 수단을 제공한다.

### Layer 4. 전송 계층 (Transport Layer)

---

<aside>
💡 전송을 위해서 포트번호를 정하는 계층

</aside>

- 전송 단위는 `**Segment**`이다.
- 양 끝단(end to end)의 사용자들이 신뢰성있는 데이터를 주고 받을 수 있도록 해주어, 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해준다.
- **TCP**(신뢰성, 연결지향적)와 **UDP**(비신뢰성, 비연결성, 실시간) 프로토콜을 통해 통신을 활성화한다.
- 포트를 열어두고, 프로그램들이 전송을 할 수 있도록 제공
- **시퀀스 넘버 기반의 오류 제어 방식**을 사용한다.
    - 시퀀스 넘버 기반?
        
        > 시퀀스 넘버 : 통신과 제어에서 데이터를 관리하기 위해 번호를 부여한다.(대표적인 전송 계층인 TCP로 예를 들면, TCP 패킷 헤더에 Sequence & Ack number라는 걸 채운다)
        > 
        > - 사용 이유 : 해당 번호는 순서 역전 방지, 중복 패킷 방지 등을 이유로 사용한다.
        > - 즉, 데이터를 패킷 단위로 나눠서 전송하는데, 이것들이 섞이거나 중복되지 않게 잘 전송될 수 있도록 한다.
- 전송 계층은 특정 연결의 유효성을 제어하고, 일부 프로토콜은 **상태 개념이 있고(stateful) 연결 기반(connection oriented)이다.**
    - 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 **다시 전송**한다는 것을 뜻한다.
- 종단간(end-to-end) 통신을 다루는 최하위 계층으로 종단간 신뢰성 있고 효율적인 데이터를 전송하며, 기능은 오류검출 및 복구와 흐름제어, 중복검사 등을 수행한다.

> 정리 : 패킷 생성(Assembly/Sequencing/Deassembly/Error detection/Request repeat/Flow control) 및 전송을 한다.
> 

### Layer 5. 세션 계층 (Session Layer)

---

<aside>
💡 양 끝단의 응용 프로세스가 데이터 통신(송수신)을 관리하기 위한 방법을 제시하는 계층

</aside>

- 세션 계층의 단위는 `**DATA`/ `Message`**
- 데이터가 통신하기 위한 논리적 연결을 담당한다.(API, Socket)
- 동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full Duplex)의 통신과 함께 체크 포인팅과 종료, 다시시작 과정 등을 수행한다.
    - 단방향 : 한쪽만 전달이 가능
    - 반이중(half-duplex) : 상대방이 연락을 할 수 없음
    - 전이중(Full Duplex) : 전화와 같이 동시에 전달 가능
- [TCP/IP](https://velog.io/@hidaehyunlee/%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B0%80-%EC%A0%84%EB%8B%AC%EB%90%98%EB%8A%94-%EC%9B%90%EB%A6%AC-OSI-7%EA%B3%84%EC%B8%B5-%EB%AA%A8%EB%8D%B8%EA%B3%BC-TCPIP-%EB%AA%A8%EB%8D%B8)세션을 만들고 없애는 역할
- TCP/IP는 인터넷 프로토콜 중 가장 중요한 역할을 하는 TCP와 IP의 합성어로 데이터의 흐름 관리, 정확성 확인, 패킷의 목적지 보장을 담당한다.
    - **데이터의 정확성 확인은 TCP가, 패킷을 목적지까지 전송하는 일은 IP가 담당한다.**

### Layer 6. 표현 계층 (Presentation Layer)

---

<aside>
💡 응용 계층에서 내린 명령, 발송한 데이터 등을 어떻게 표현할지 정해주는 계층

</aside>

- 표현 계층의 단위는 `**DATA`/ `Message`**
- 데이터 표현에 대한 독립성을 제공하고 **암호화**하는 역할을 담당(JPEG, MPEG 등)
- 코드 간의 번역을 담당하여 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어준다.
- MIME 인코딩이나 암호화 등의 동작이 이루어진다.
- 압축과 암호를 담당

### Layer 7. 응용 계층 (Application Layer)

---

<aside>
💡 사용자가 보는 소프트웨어의 UI, 네트워크 서비스, 사용자의 입출력 부분 등을 담당하는 계층
ex,우리가 사용하는 웹 브라우저, 어플 등등에서 하는 활동

</aside>

- 응용 계층의 단위는 `**DATA`/ `Message`**
- 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다.(HTTP, FTP, DNS 등)
- 사용자 인터페이스, 전자우편, 데이터베이스 관리 등의 서비스를 제공한다.
- 편지를 발송하는 과정 중 편지를 작성하는 과정을 응용계층에서 담당

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7d34c610-ccab-4516-8394-2c555b48b9dc/Untitled.png)

## 📡 TCP/IP 5계층

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7e8c87ab-8eeb-4503-acd6-d13641b44b25/Untitled.png)

<aside>
💡 위에서 ISO(국제표준화기구)가 데이터 통신의 규격과 프로토콜을 통일하려고 OSI 참조 모델을 만들었다고 했다. 사실 이 시도는 실패하였고, 현재 세계에서 표준으로 받아들여지는 것은 TCP/IP 모델이다.

</aside>

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/478b35bd-25ef-465d-871f-5bbf101892f6/Untitled.png)

### 📌 L5 | Application

<aside>
💡 통신 서비스를 실현하는 계층

</aside>

- 프로그램 구현체와 사용자 인터페이스를 의미한다.
- OS에서 제공하는 L4 API를 활용해 통신 프로그램이 구현된다.
- 다양한 어플리케이션마다 HTTP, FTP, SSH, SMTP, POP 등 다양한 프로토콜이 활용된다.
    - 파일을 송수신하는 FTP
    - 원격지 접속을 하는 Telnet
    - 전자 우편을 주고받는 SMTP
    - 하이퍼텍스트를 지원하는 HTTP등

---

### 📌 L4 | Transport

### process-to-process delivery

- Port 번호를 사용하여 최종 도착지인 프로세스까지 데이터를 전달한다.
- OS 커널에 구현되어 있다.
- 패킷 전송 프로토콜로는 TCP와 UDP가 있다.
    - TCP는 데이터를 안전하고 확실하게 전달하는 것을 목적으로 정확성이 요구되는 서비스에 사용된다.
    - UDP는 데이터를 빠르게 전송하는 것이 목적으로 TCP보다 절차가 단순하고 속도가 빠르다.UDP는 데이터의 전송속도가 중요한 서비스에 사용된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4f1674f-5637-40ed-9b67-106babc437cc/Untitled.png)

### Port Number

- 컴퓨터는 `2-byte` 길이의 port 번호를 가진다.
- Well-known port (1~1000)는 OS와 주요 프로토콜에서 사용하기 때문에, 사용자 어플리케이션은 그 외의 port 번호를 사용한다.

---

### 📌 L3 | Network

### host-to-host delivery

- Routing & Forwarding을 수행해서 목적지 IP 주소까지 패킷을 전달한다.
- OS 커널에 구현되어 있다.
- URL이 주어지면 DNS(Domain Name Resolution)을 통해 IP 주소를 찾고, 실제 패킷은 IP 주소를 향해 전송된다.
- 패킷이 Host에 도착하면, IP 주소의 광역대에 따라 Routing Table에 지정된 경로로 패킷을 Forwarding한다.

### IP Address

- Internet Protocol Address
- Host의 논리적 주소로, 전 세계의 네트워크 상에서 유일하다.
- `IPv4`는 `4-byte`, `IPv6`는 `8-byte` 주소를 갖는다.

---

### 📌 L2 | Data-Link

### 1-hop delivery

- Routing & Forwarding을 수행해서 목적지 MAC 주소까지 프레임을 전달한다.
- Reliable delivery between adjacent nodes
- Ethernet Card에 구현되어 있다.

### MAC Address

- Media Access Control Address
- Ethernet Card의 물리적 주소로, 로컬 네트워크 안에서만 유일하다.
- Gateway(라우터)는 Ethernet Card를 2개 가지고 있어서 LAN과 WAN을 연결한다.
- `48-bit` 주소를 갖는다.

### ARP

- Address Resolution Protocol
- LAN 내부의 ARP Table을 참조하여 IP 주소를 MAC 주소로 변환한다.

---

### 📌 L1 | Physical

- Encoding: 0과 1의 나열을 아날로그 신호로 변환해서 전송한다.
- Decoding: 아날로그 신호를 받으면 0과 1로 해석한다.
- 물리적, 기계적, 전기적 기능으로 HW에 구현되어 있다.

> ref
> 

---

네트워크란

---

[[Network] 네트워크란 무엇인가? 네트워크의 정의와 종류 총정리](https://coding-factory.tistory.com/340)

OSI 7계층

---

[[CS] 📕 Network](https://velog.io/@soosungp33/CS-Network)

> OSI 5계층
> 

[OSI 7계층 & TCP/IP 5계층](https://velog.io/@jwkim/cs-nw-osi-tcp-ip)