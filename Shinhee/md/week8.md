# 📌 HTTP란?

<aside>
💡 웹브라우저(**Client**)와 서버(**Server**)간의 웹페이지같은 자원/정보를 주고 받을 때 쓰는 통신 규약

</aside>

- 즉, HTTP는 인터넷에서 하이퍼텍스트를 교환하기 위한 통신 규약으로, `80번` 포트를 사용하고 있다. 따라서 HTTP 서버가 80번 포트에서 요청을 기다리고 있으며, 클라이언트는 80번 포트로 요청을 보내게 된다.
- HTTP는 상태를 가지지 않는 **stateless** 프로토콜이며 `Method`, `Path`, `Version`, `Headers`, `Body` 등으로 구성된다.
- HTTP는 Application 레벨의 프로토콜로 TCP/IP 위에서 작동한다.
- HTTP의 통신 방식은 기본적으로 요청/응답 (request/response) 구조로 되어있다.
    
    클라이언트가 HTTP request를 서버에 보내면 서버는 HTTP response를 보내는 구조.
    
    클라이언트와 서버의 모든 통신이 요청과 응답으로 이루어 진다.
    

## 📌 HTTP Request의 구조

- HTTP Request의 메세지는 크게 3 부분(`start line`, `headers`, `body`)으로 구성된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f278242c-8d6d-48af-9d2e-66f89d917636/Untitled.png)

### ▫ startline

- Method : 해당 request가 의도한 action을 정의한 부분
    - GET, POST, PUT, DELETE, OPTIONS, .. 이 있다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4be33eff-3fec-4c41-9092-d5ae7bfa085a/Untitled.png)
    
- Path (Request target) : 해당 request가 전송되는 목표 uri.
    - ex.  /login.
    
    <aside>
    💡 uri : 인터넷 상에서 특정 자원(파일)을  나타내는 유일한 주소 
    scheme :// host [:port][/path][?query]
    
    </aside>
    
- Version : 말 그대로 사용되는 HTTP version

### ▫ Header

- 해당 request에 대한 추가 정보를 담고 있는 부분
    
    ex. request 메시지 body 의 총 길이 (conent-length), .. 
    
- Key : Value 값으로 되어있다.
- 크게 3 부분으로 나뉜다. (general headers, request headers, entity headers)
- 자주 사용되는 Header 정보
    - `Host` : 요청이 전송되는 target의 host url: 예를 들어, google.com
    - `User-Agent` : 요청을 보내는 클라이언트의 대한 정보: 예를 들어, 웹브라우저에 대한 정보.
    - `Accept` : 해당 요청이 받을 수 있는 응답(response) 타입.
    - `Connection` : 해당 요청이 끝난후에 클라이언트와 서버가 계속해서 네트워크 컨넥션을 유지 할것인지 아니면 끊을것인지에 대해 지시하는 부분.
    - `Content-Type` : 해당 요청이 보내는 메세지 body의 타입. 예를 들어, JSON을 보내면 application/json.
    - `Content-Length` : 메세지 body의 길이.

### ▫ body

- 해당 reqeust의 실제 메세지/내용.
- Body가 없는 request도 많다.
- 예를 들어, GET request들은 대부분 body가 없는 경우가 많음.

## 📌 HTTP Response의 구조

- HTTP Response의 메세지는 크게 3 부분(`Statusline`, `headers`, `body`)으로 구성된다.

### ▫ Status Line

Response의 상태를 간략하게 나타내주는 부분 3부분으로 구성되어 있다.

> ex. `HTTP/1.1` `404` `Not Found`
> 
- HTTP 버젼
- Status code: 응답 상태를 나타내는 코드. 숫자로 되어 있는 코드.예를 들어, 200
- Status text: 응답 상태를 간략하게 설명해주는 부분.예를 들어, "Not Found"

### ▫ Headers

- Response의 headers와 동일하다.
- 다만 response에서만 사용되는 header 값들이 있다.
- 예를 들어, User-Agent 대신에 Server 헤더가 사용된다.

### ▫ Body

- Response의 body와 일반적으로 동일하다.
- Request와 마찬가지로 모든 response가 body가 있지는 않다. 데이터를 전송할 필요가 없을 경우 body가 비어있게 된다.

## 📌 자주 쓰이는 HTTP Methods

### ▫  GET

- 이름 그대로 어떠한 데이타를 서버로 부터 받아(GET)올때 주로 사용하는 Method.
- 데이터 생성/수정/삭제 없이 받아오기만 할 때 사용된다.
- 가장 간단하고 많이 사용되는 HTTP Method
- 언급한대로 주로 데이터를 받아올때 사용되기 때문에 request에 body를 안 보내는 경우가 많다.

### ▫  POST

- 데이터를 생성/수정/삭제 할 때 주로 사용되는 Method.
- 데이터를 생성 및 수정 할 때 많이 사용하기 때문에 대부분의 경우 request body가 포함돼서 보내진다.

<aside>
💡 여기서 Method가 GET일 때에는 HTTP Request header에 path 정보 같은 게 들어있지만,
POST인 경우에는 id나 pwd같은 중요한 정보들은 body에 담아서 보낸다고 한다. 
하지만 이 같은 정보도 제 3자에게 보여질 수 있기 때문에, 결국에는 HTTPS를 사용

</aside>

## 📌 HTTP의 작동과정

<aside>
💡 클라이언트 즉, 사용자가 브라우저를 통해서 어떠한 서비스를 url을 통하거나 다른 것을 통해서 요청(request)을 하면 서버에서는 해당 요청사항에 맞는 결과를 찾아서 사용자에게 응답(response)하는 형태로 동작한다.

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/25845392-724c-4a67-9443-11f989c4ec59/Untitled.png)

1. `connect` : 클라이언트가 원하는 서버에 접속
2. `request` : 클라이언트가 이 서버에 요청.클라이언트가 서버에게 연락하는 것을 요청이라고 하며 요청을 보낼때는 요청에 대한 정보를 담아 서버로 보낸다.
3. `response` : 서버가 요청에 대한 응답결과를 클라이언트에게 보내는 것을 응답이라고 한다.응답이 끝나면 서버와 클라이언트 연결 끊기(Stateless)

## 📌 자주 쓰이는 HTTP Status Code

### ▫ 200 OK

- 가장 자주 보게 되는 status code.
- 문제없이 다 잘 실행 되었을때 보내는 코드.

### ▫ 301 Moved Permanently

- 해당 URI가 다른 주소로 바뀌었을때 보내는 코드.

```
HTTP/1.1 301 Moved Permanently
Location: http://www.example.org/index.asp
```

### ▫ 400 Bad Request

- 해당 요청이 잘못된 요청일때 보내는 코드.
- 주로 요청에 포함된 input 값들이 잘못된 값들이 보내졌을때 사용되는 코드.
- 예를 들어, 전화번호를 보내야 되는데 text가 보내졌을때 등등.

### ▫ 401 Unauthorized

- 유저가 해당 요청을 진행 할려면 먼저 로그인을 하거나 회원 가입을 하거나 등등이 필요하다는것을 나타내려 할때 쓰이는 코드.

### ▫ 403 Forbidden

- 유저가 해당 요청에 대한 권한이 없다는 뜻.
- 예를 들어, 오직 과금을 한 유저만 볼 수 있는 데이터를 요청 했을때 등.

### ▫ 404 Not Found

- 요청된 uri가 존재 하지 않는다는 뜻.

### ▫ 500 Internal Server Error

- 서버에서 에러가 났을때 사용되는 코드.

# 📌 HTTPS란?

<aside>
💡 인터넷 상에서 정보를 암호화하는 SSL(Secure Socket Layer)프로토콜을 이용하여 웹브라우저(클라이언트)와 서버가 데이터를 주고 받는 통신 규약

</aside>

- HTTPS는 **HTTP에 데이터 암호화가 추가된 프로토콜**이다. HTTPS는 HTTP와 다르게 `443번` 포트를 사용하며, 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화를 지원하고 있다.
- HTTP의 일반 텍스트(text)에 SSL이나 TLS 프로토콜을 씌워 데이터를 암호화하는 기법이며, 로그인이나 결제화면에서 주로 쓰입니다.

<aside>
💡 SSL : 웹 Server와 Client의 통신 암호화 프로토콜이다.

</aside>

## 📌 SSL 적용방식

---

1. 핸드 셰이킹
2. 데이터 전송
3. 세션 종료

---

- SSL 적용은 핸드 셰이킹 단계에서 발생이 된다.
    - SSL 핸드셰이킹 : 443 포트를 이용하여 서로의 상태를 파악하는 TCP 기반의 프로토콜
    - TCP 기반이기 때문에 SSL 핸드세이크 전에 TCP 3-way 핸드셰이크 또한 수행
- 핸드 셰이킹 순서
    1. Client hello
        
        <aside>
        💡 Client가 특정 주소에 접근하면 해당하는 서버에 요청을 보낸다.
        
        </aside>
        
        - ex) 브라우저 검색창에 도메인을 입력하는 것
        
        ![이러한 요청 정보를 보낸다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1454553f-82a6-4fa4-a59f-e8f4d186424d/Untitled.png)
        
        이러한 요청 정보를 보낸다.
        
        - 이때 클라이언트는 자신의 브라우저가 지원할 수 있는 암호화 방식(Cipher Suite)을 먼저 제시합니다. 그리고 랜덤 데이터를 생성하여 추가로 전송
        - **세션 아이디:** 이미 SSL 핸드쉐이킹을 했다면 비용과 시간을 절약하기 위해서 기존의 세션을 재활용하게 되는데 이때 사용할 연결에 대한 식별자를 서버 측으로 전송
    2. Server hello
        
        <aside>
        💡 Server가 Client hello 요청을 받으면 Client에 일종의 화답을 보낸다.
        
        </aside>
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/93c2b602-8c15-4de4-8ec3-d9f60764a3e9/Untitled.png)
        
        - 서버는 클라이언트가 제시한 암호화 방식 중 하나를 선정하여 알려줍니다.
        - 클라이언트와 마찬가지로 서버 측에서 생성한 랜덤 데이터 또한 전달
        - **인증서**의 정보와 함께, Server와의 암호화 통신을 위한 **Server 공개키**가 전달된다.
            
            → 인증서에 Server의 공개 키가 포함되어있다.
            
             서버의 공개키로 데이터를 암호화하면 Server는 이를 받아 개인키로 복호화하여 요청을 분석할 수 있다.
            
    3. Client key exchange
        - 인증서가 자신이 신용있다고 판단한 CA로부터 서명된 것인지 확인
            
            (또한 날짜가 유효한지, 그리고 인증서가 접속하려는 사이트와 관련되어 있는지 확인)
            
        - 클라이언트는 미리 주고받은 자신과 서버의 랜덤 데이터를 참고하여 서버와 암호화 **통신을 할 때 사용할 키(랜덤 대칭 암호화 키 Pre Master Secret Key )를 생성한 후 서버에게 전달**합니다.
        - 이때 키는 서버로부터 받은 공개키로 암호화되어 보내집니다.
    4. Finished
        - 마지막으로 핸드셰이크 과정이 정상적으로 마무리되면, 클라이언트와 서버 모두 “finished” 메시지를 보냅니다.
    5. 이후 전송단계로 넘어가서 클라이언트가 생성한 키를 이용하여 암호화된 데이터를 주고받게 됩니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/21969ebd-c7d0-4a88-a762-ba5ad38e8ff9/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/447e0467-293a-420c-844a-cbdbdaa9e365/Untitled.png)

- 핸드 쉐이킹 이후 데이터 전송 과정
    1. 클라이언트의 암호화한 데이터 전송
        - public key를 사용해서 랜덤 대칭 암호화키를 비롯한 URL, http 데이터들을 암호화해서 전송
    2. 웹서버의 복호화
        - private key를 이용해서 랜덤대칭 암호화키와 URL. http를 복호화
    3. 웹서버의 암호화 데이터 전송
        - 요청받은 URL에 대한 응답을 웹브라우저로부터 받은 랜덤 대칭 암호화키를 이용하여 암호화해서 브라우저로 전송
    4. 클라이언트의 복호화
        - 대칭 암호키를 이용해서 http 데이터와 html 문서를 복호화하고 화면에 뿌려줌

## 📌 SSL 인증서

<aside>
💡 SSL 인증서는 Client와 Server간의 통신을 제3자가 보증해주는 전자화된 문서

</aside>

![https://velog.velcdn.com/images%2Fswhan9404%2Fpost%2F3aee5da6-caa9-49d6-9e23-68f1cb09078e%2Fimage-20210818223039378.png](https://velog.velcdn.com/images%2Fswhan9404%2Fpost%2F3aee5da6-caa9-49d6-9e23-68f1cb09078e%2Fimage-20210818223039378.png)

- 언제 검증하는가?
    - 클라이언트가 서버에 접속한 직후에 서버는 클라이언트에게 이 인증서 정보를 전달하게 됩니다.클라이언트는 이 인증서 정보가 신뢰할 수 있는 것인지를 검증 한 후에 다음 절차를 수행하게 됩니다.
- SSL 인증서의 역할
    1. 클라이언트가 접속한 서버가 신뢰할 수 있는 서버임을 보장
    2. SSL 통신에 사용할 공개키를 클라이언트에게 제공
- 인증서의 내용
    1. 서비스의 정보 (인증서를 발급한 CA, 서비스의 도메인 등등)
        - 클라이언트가 접속한 서버가 신뢰할 수 있는 서버임을 보장하는 역할에 사용
    2. 서버 측 공개키 (공개키의 내용, 공개키의 암호화 방법)
        - 서비스의 도메인, 공개키와 같은 정보는 서비스가 CA로부터 인증서를 구입할 때 제출하고, CA에 의해 암호화해서 저장(CA는 CA 공개키를 이용해서 서버가 제출한 인증서를 암호화)

## 📌 대칭키 암호화 vs 비대칭키 암호화

HTTPS는 대칭키 암호화 방식과 비대칭키 암호화 방식을 **모두** 사용한다.

### ▫ 대칭키 암호화

<aside>
💡 양쪽 당사자가 공통 비밀 키를 공유 (클라이언트와 서버가 동일한 키를 사용)

</aside>

- 대칭형 방식은 양쪽 당사자가 공유한 시크릿에 의존
    - 전송자는 정보를 암호화하는 데 사용하고
    - 수신자는 동일한 방식과 키를 사용해 복호화한다.
    
- 이 방법의 문제는 양쪽 당사자가 서로 물리적인 만남 없이 시크릿을 협상(교환)하는 방법이라서 일종의 보안 통신 채널이 필요하다.
    - 그래서, SSL 통신을 통하여 보안 통신채널을 만드는 것
- 장점
    - 공개키 암호화 방식에 비해 암호화 및 복호화가 빠르다는 장점이 있다. (**연산 속도가 빠름**)
- 단점
    - 암호화 통신을 하는 사용자끼리 같은 대칭키를 공유해야만 한다는 단점이 있다.
        - 대칭키를 사용자끼리 물리적으로 직접 만나서 전달하지 않는한, **대칭키를 전달하는 과정에서 해킹의 위험에 노출**될 수 있기 때문
    - 대칭키는 데이터를 전송하는 쌍마다 필요하기 때문에, 통신을 총 n명이 한다면 nC2=n(n-1)/2 만큼의 대칭키 생성작업이 필요하다.
        - 즉, 키 관리가 힘들다.

### ▫ 비대칭키 암호화

<aside>
💡 당사자 중 한쪽이 비밀 키와 공개 키의 쌍, 공개 키 인프라(PKI) 기반을 갖는다.

</aside>

- 공개 키와 개인 키의 개념을 기반
    - 두 가지 키 중 하나로 평문을 암호화(공개키를 통한 암호화)하면 다른 보완 키를 사용해야만 복호화(개인 키를 통한 복호화)할 수 있다.
- 단점
    - **암복호화가 매우 복잡하다는 점**이다. 암복호화가 복잡한 이유는, **암호화하는 키와 복호화하는 키가 서로 다르기 때문**
        - 즉, 메세지의 크기가 크면 암호화하는데 느리다. (연산속도가 느림)

## 📌 HTTPS 동작 과정

<aside>
💡 HTTPS는 **대칭키 암호화와 비대칭키 암호화를 모두 사용해 빠른 연산 속도와 안정성을 모두 얻는다.**

</aside>

Hand-Shaking 과정에서는 먼저 서버와 클라이언트간 세션키를 교환한다. 여기서 세션키는 주고받는 데이터를 암호화하기 위해 사용되는 대칭키이다.데이터 간 교환에는 빠른 연산 속도가 필요하므로 **세션키는 대칭키**로 만들어진다.

**처음 연결을 성립해 안전하게 세션키를 공유하는 과정에서 비대칭키**가 사용된다.이후 **데이터를 교환하는 과정에서 빠른 연산 속도를 위해 대칭키**가 사용된다.

### ▫ 연결 흐름

1. 클라이언트가 서버로 최초 연결 시도
2. 서버는 공개키를 브라우저에게 넘김
3. 브라우저는 인증서의 유효성을 검사하고 세션키 발급
4. 브라우저는 세션키를 보관하며 추가로 서버의 공개키로 세션키를 암호화해 서버로 전송
5. 서버는 개인키로 암호화된 세션키를 복호화하여 세션키를 얻음
6. 클라이언트와 서버는 동일한 세션키를 공유하므로 데이터를 전달할 때 세션키로 암호화/복호화를 진행

- 공개키: 모두에게 공개가능한 키
- 개인키: 나만 가지고 알고 있어야 하는 키

# 📌 HTTP vs HTTPS

---

HTTP는 암호화가 추가되지 않았기 때문에 보안에 취약한 반면, HTTPS는 안전하게 데이터를 주고받을 수 있다. 하지만 HTTPS를 이용하면 암호화/복호화의 과정이 필요하기 때문에 HTTP보다 속도가 느리다. (물론 오늘날에는 거의 차이를 못느낄 정도이다.) 또한 HTTPS는 인증서를 발급하고 유지하기 위한 추가 비용이 발생하다.그렇다면 언제 HTTP를 쓰고, 언제 HTTPS를 쓰는 것이 좋겠는가?개인 정보와 같은 민감한 데이터를 주고 받아야 한다면 HTTPS를 이용해야 하지만, 노출이 되어도 괜찮은 단순한 정보 조회 등 만을 처리하고 있다면 HTTP를 이용하면 된다.

# 📌 CS 질문

# **HTTP**

### **1. Http와 Https 통신 방식의 차이에 대해 설명해주세요.**

HTTP는 Hyper Text Transfer Protocol의 약자로, **서버/클라이언트 간 웹페이지 같은 자원을 주고받을 때 쓰는 통신 규약**으로, WWW상에서 웹페이지나 이미지 같은 정보를 요청과 응답에 의해 주고받는 프로토콜입니다. 단순 텍스트를 주고받기 때문에 누군가 네트워크에서 신호를 가로채 본다면 내용이 노출되며, 이러한 **보안상 문제**를 해결해주는 프로토콜이 HTTPS입니다.

HTTPS는 **인터넷 상에서 정보를 암호화하는 SSL(Secure Socket Layer) 프로토콜**을 이용해 웹브라우저(클라이언트)와 서버가 데이터를 주고받는 통신 규약입니다.

정리하면, HTTPS는 HTTP 메시지(텍스트)를 암호화하는 것이며, S는 **Secure Socket**, **통신 보안망**을 말하며, **공개키 암호화 방식**을 거친다.

**공개키 암호화 방식**은

1. 애플리케이션 서버 측에서 공개키와 개인키를 만듭니다.
2. 그다음 신뢰성 있는 CA(Certificate Authority) 공개키 저장소를 선택해, 공개키 관리를 위한 계약을 합니다.
3. CA기업은 CA기업만의 공개키와 개인키가 있는데, CA 기업의 이름과 서버 측의 공개키, 공개키의 암호화 방법 등을 담은 인증서를 만들어, CA기업의 개인키로 암호화해서 서버 측에 제공합니다.
4. 이제 서버 측은 공개키로 암호화된 HTTPS 요청이 아닌 요청이 오면 이 암호화된 인증서를 클라이언트에게 전달합니다.
5. 신뢰할 수 있는 공개키는 브라우저가 이미 알고 있는데, 브라우저가 CA 기업 리스트 탐색하면서, 해당 기업 이름이 같으면 해당 기업의 공개키를 이미 알고 있기 때문에 브라우저는 인증서를 해독해 서버의 공개키를 얻습니다.
6. 그 후, 해당 서버와 통신할 때마다 해당 공개키로 암호화해서 요청을 날리게 됩니다.

자체적으로 인증서 발급을 할 수 있고, 신뢰할 수 없는 CA기업에서 인증서 발급을 받는 경우도 있기 때문에, HTTPS를 지원한다면 무조건 안전한 건 아닙니다. 그런 경우, '주의 요함', '안전하지 않은 사이트'라고 알림이 뜹니다.

### **2. HTTP 프로토콜에 대해 설명해주세요.**

HTTP는 Hyper Text Transfer Protocol의 약자로, 서버/클라이언트 간 웹페이지 같은 자원을 주고받을 때 쓰는 통신 규약으로, WWW상에서 웹페이지나 이미지 같은 정보를 요청과 응답에 의해 주고받는 프로토콜입니다. 단순 텍스트를 주고받기 때문에 누군가 네트워크에서 신호를 가로채 본다면 내용이 노출되는 보안상 위험이 존재합니다.

> ref
> 

[HTTP 구조 및 핵심 요소](https://velog.io/@teddybearjung/HTTP-%EA%B5%AC%EC%A1%B0-%EB%B0%8F-%ED%95%B5%EC%8B%AC-%EC%9A%94%EC%86%8C)

[[Web] HTTP와 HTTPS의 개념 및 차이점](https://mangkyu.tistory.com/98)

[HTTP와 HTTPS 차이 구분하기](https://velog.io/@swhan9404/HTTP%EC%99%80-HTTPS-%EC%B0%A8%EC%9D%B4-%EA%B5%AC%EB%B6%84%ED%95%98%EA%B8%B0)

[[CS] CS 면접 질문 정리](https://velog.io/@dbsrud11/CS-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-%EC%A0%95%EB%A6%AC)

[HTTP vs. HTTPS (HTTP와 HTTPS 차이점)](https://hyeran-story.tistory.com/159)