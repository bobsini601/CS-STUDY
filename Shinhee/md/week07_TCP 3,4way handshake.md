## 🖥 TCP 3 way handshake & 4 way handshake

---

<aside>
💡 TCP는 `3 way handshake` 과정을 통해 연결을 설정하고  `4 way handshake` 과정을 통해 세션을 종료합니다.

</aside>

## 📡 3 way handshake

---

<aside>
💡 TCP/IP 네트워크 환경에서 서버와 클라이언트를 연결하는데 필요한 프로세스

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/12327920-c26b-4574-aed4-e0ddc7b9afc4/Untitled.png)

### flow

- **STEP 1**
    
    <aside>
    👉 Client는 Server에 접속을 요청하는 SYN 패킷을 보낸다. 이 때 Client는 SYN을 보내고 SYN/ACK 응답을 기다리는 `SYN_SENT` 상태로 바뀌게 된다.
    
    </aside>
    
    - 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 숫자로 지정하고, SYN 플래그 비트를 1로 설정한 세그먼트를 전송한다.
    - PORT 상태
        - Client : `CLOSED` → `SYN_SENT`
        - Server : `LISTEN`

---

- **STEP 2**
    
    <aside>
    👉 Server는 SYN 요청을 받고 Client에게 요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 Client가 다시 ACK으로 응답하기를 기다린다. 이때 Server는 `SYN_RECEIVED` 상태가 된다.
    
    </aside>
    
    - ACK Number필드를 Sequence Number + 1 로 지정하고 SYN과 ACK 플래그 비트를 1로 설정한 새그먼트 전송
        
        step1. Client —(          SYN(a)        )→ Server
        
        step2. Client ←( SYN(b), ACK(a+1) )- Server 
        
    - PORT 상태
        - Client : `CLOSED`
        - Server : `SYN_RCV`

---

- **STEP 3**
    
    <aside>
    👉 Client는 Server에 ACK를 보내고 이후부터는 연결이 이루어지고 데이터가 오가게 되는 것이다. 이때 Server의 상태가 ESTABLISHED 이다.
    
    </aside>
    
    - 이때, 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있다.
    - PORT 상태
        - Client : `ESTABLISED`
        - Server : `SYN_RCV` ⇒ ACK ⇒ `ESTABLISED`

---

### ❓ Sequence #를 난수로 생성해서 설정하는 이유?

**Q. 초기 Sequence Number인 ISN을 0부터 시작하지 않고 난수를 생성해서 설정하는 이유?**

A. Connection을 맺을 때 사용하는 포트(Port)는 유한 범위 내에서 사용하고 시간이 지남에 따라 **재사용**된다. 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용하는 가능성이 존재한다. 서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 Number가 전송된다면 **이전의 Connection으로부터 오는 패킷으로 인식할 수 있다**. 이런 문제가 발생할 가능성을 줄이기 위해서 난수로 ISN을 설정한다.

> ref.
> 

[[TCP] 3-way-handshake & 4-way-handshake](https://asfirstalways.tistory.com/356)

### ❗ SYN Flooding

<aside>
💡 3way handshaking의 취약점을 이용해 서버를 공격하는 방법

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7b55485d-d3ce-47cc-87a8-cc9b1d334be7/Untitled.png)

`**Backlog Queue**` : Server가 접속자의 연결 요청을 대기할 때, 요청정보를 저장하는 공간

- 만약 정상 연결이 되었다면(ESTABLISHED), Backlog Queue 공간에서 연결 요청정보가 삭제되어 공간은 계속 유지
- 하지만, 연결 과정이 중간에 정상적으로 진행되지 않았다면, 정보가 계속 Backlog Queue에 남아있게 되고 Queue가 계속 쌓여서 가득 차게 된다면 다른 연결 요청 정보 저장을 할 수가 없다.

> **🤜 flow**
> 

---

1. 공격자 서버에 연결요청 (SYN) 전송
2. 서버는 연결 요청에 응답 (SYN+ACK) 전송
3. 공격자가 ACK를 보내지 않음, **서버는 Backlog Queue에 정보 저장 후 대기중**
4. 공격자가 서버에 다시 연결 요청(SYN) 전송, 반복
5. 서버는 `Backlog Queue`에 공격자의 SYN 요청을 대기, 계속 Queue가 쌓임
6. 한정적인 `Backlog Queue`에 공격자의 Queue가 가득 채워 가용성 침해
7. 정상 Client 접속 시 연결요청(SYN)을 보내도 서버는 ESTABLISHED 할 수 없음

> 🤜 **Solution**
> 

---

1. Backlog Queue의 크기를 늘린다. (임시방편)
2. SYN Cookie를 설정한다.
    
    이 설정을 하게 되면, 클라이언트로부터 ACK를 받을 때까지 Backlog Queue에 연결 요청정보 저장 X
    
3. 방화벽의 동일 클라이언틑 IP에 대해 연결 요청(SYN) 임계치를 설정
4. TCP 연결 과정 대기시간을 줄인다.

## 📡 4 way handshake

---

<aside>
💡 TCP/IP 네트워크 환경에서 서버와 클라이언트를 연결을 해제(세션 종료)하는데 필요한 프로세스

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f373b36-e360-48bc-ba3c-8be0f31b221d/Untitled.png)

### flow

- **STEP 1   Client -(FIN+ACK)→ Server**
    
    <aside>
    👉 Client가 연결을 종료하겠다는 FIN플래그를 Server에 전송한다.
    
    </aside>
    
    - Server와 Client가 연결된 상태에서 Client가 close()를 호출하여 접속을 끊으려고 Server에 요청한다.
    - 이때, Client는 Server에게 연결을 종료한다는 `FIN` 플래그를 보낸다.
        - 이때 FIN 패킷에는 실질적으로 `ACK`도 포함되어있다. (아무래도 데이터를 주고 받고 있었으니까,,? 그 받은 데이터에 대한 ACK 아닐까,,? 물어보고싶어요 팀원들에게,, plz)
    - PORT 상태
        - Client : ‘ESTABLISHED’ -(FIN+ACK)→ ‘FIN_WAIT1’
        - Server : ‘ESTABLISHED’

---

- **STEP 2**  **Client ←(ACK)- Server**
    
    <aside>
    👉 FIN을 받은 Server는 일단 확인 메시지 `ACK`를 보내고 자신의 통신이 끝날때까지 기다린다.
    
    </aside>
    
    - Server(수신자)는 ACK Number 필드를 (Sequence Number + 1)로 지정하고, ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.
    - Server는 Client에게 응답을 보내고 **`CLOSE_WAIT` 상태**에 들어갑니다. 그리고 **아직 남은 데이터가 있다면 마저 전송을 마친 후에 close( )를 호출**
    - 클라이언트에서는 서버에서 ACK를 받은 후에 서버가 남은 데이터 처리를 끝내고 FIN 패킷을 보낼 때까지 기다리게 됩니다. (**`FIN_WAIT_2`)**
    - PORT 상태
        - Server : `ESTABLISHED` -(ACK 보냄)→ **`CLOSE_WAIT`**
        - Client : **`FIN_WAIT_1`**→ (ACK받음) → **`FIN_WAIT_2`**

---

- **STEP 3**  **Client ←(FIN)- Server**
    
    <aside>
    👉 Server가 통신이 끝났으면 연결이 종료되었다고 Client에게 FIN플래그를 전송한다.
    
    </aside>
    
    - 데이터를 모두 보냈다면, Server는 연결이 종료에 합의 한다는 의미로 `FIN` 패킷을 Client에게 보낸 후에, 승인 번호를 보내줄 때까지 기다리는 `LAST_ACK` 상태로 들어간다.
    - PORT 상태
        - Client : `FIN_WAIT2`
        - Server : `CLOSE_WAIT` → (FIN 보냄) → `LAST_ACK`

---

- **STEP 4**  **Client -(ACK)→ Server**
    
    <aside>
    👉 Client는 확인했다는 메시지 `ACK`를 보낸다.
    
    </aside>
    
    - Client는 FIN을 받고, 확인했다는 `ACK`를 Server에게 보낸다.아직 Server로부터 받지 못한 데이터가 있을 수 있으므로 `TIME_WAIT`을 통해 기다린다. (실질적인 종료과정 `CLOSED`에 들어가게 된다.)이때 `TIME_WAIT` 상태는 **의도치 않은 에러로 인해 연결이 데드락으로 빠지는 것을 방지**
    - 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 `CLOSED`로 들어갑니다.
    - PORT 상태
        - Client : `TIME_WAIT`
        - Server : ,,,
- 서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)
- TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed)

---

### TCP FLAG

| FLAG | 설명 |
| --- | --- |
| SYN
(연결 요청 플래그) | - TCP에서 세션을 성립할 때 가장먼저 보내는 패킷, 시퀀스 번호를 임의적으로 설정하여  세션을 연결하는 데에 사용되며 초기에 시퀀스 번호를 보내게 된다. |
| ACK
(응답플래그) | - 상대방으로부터 패킷을 받았다는 걸 알려주는 패킷- 다른 플래그와 같이 출력되는 경우도 있습니다.- 받는 사람이 보낸 사람 시퀀스 번호에 TCP 계층에서 길이 또는 데이터 양을 더한 것과 같은  ACK를 보냅니다.(일반적으로 +1 하여 보냄)- ACK 응답을 통해 보낸 패킷에 대한 성공, 실패를 판단하여재전송 하거나 다음 패킷을 전송한다. |
| FIN
(연결종료 플래그) | - 세션 연결을 종료시킬 때 사용되며 더이상 전송할 데이터가 없음을 나타낸다. |
| RST
(연결 재설정 플래그) | - 재설정(Reset)을 하는 과정이며 양방향에서 동시에 일어나는 중단 작업이다. - 비 정상적인 세션 연결 끊기에 해당한다.- 이 패킷을 보내는 곳이 현재 접속하고 있는 곳과 즉시 연결을 끊고자 할 때 사용한다 |
| PSH
(밀어넣기) | - TELNET과 같은 상호작용이 중요한 프로토콜의 경우 빠른 응답이 중요한데, 이 때 받은 데이터를 즉시 목적지인 OSI 7 Layer 의 Application 계층으로 전송하도록 하는 FLAG.- 대화형 트랙픽에 사용되는 것으로 버퍼가 채워지기를 기다리지 않고 데이터를 전달한다.- 데이터는 버퍼링 없이 바로 위 계층이 아닌 7 계층의 응용프로그램으로 바로 전달한다. |
| URG
(긴급 데이터 플래그) | - Urgent pointer 유효한 것인지를 나타낸다.- Urgent pointer란 전송하는 데이터 중에서 긴급히 전당해야 할 내용이 있을 경우에 사용한다.- 긴급한 데이터는 다른 데이터에 비해 우선순위가 높아야 한다. -  EX) ping 명령어 실행 도중 Ctrl+c 입력 |

[TCP Flag란 ?](https://hongpossible.tistory.com/entry/TCP-Flag%EB%9E%80)

> ref
> 

---

[[네트워크] TCP/UDP와 3 -Way Handshake & 4 -Way Handshake](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake)

[[ 네트워크 쉽게 이해하기 22편 ] TCP 3 Way-Handshake & 4 Way-Handshake](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)

[TCP SYN Flooding 공격 이란?](https://crossjin.tistory.com/entry/TCP-SYN-Flooding-%EA%B3%B5%EA%B2%A9-%EC%9D%B4%EB%9E%80)