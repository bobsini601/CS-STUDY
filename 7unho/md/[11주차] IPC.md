# [11주차] IPC

날짜: 2022년 10월 8일
진행상황: Done
태그: OS

---

# IPC ( Inter Process Communication )

---

<aside>
💡 프로세스들 간의 의사소통이 이뤄지는 것을 뜻한다

</aside>

- 프로세스가 통신 가능하다는 것은 서로 데이터를 주고 받을 수 있다는 뜻이 되며, 동시에 접근 가능한 메모리
    
    **즉, 프로세스들이 공유하는 메모리가 필요하다**는 뜻이다.
    
- 컴퓨터 내부에서 보다 효율적으로 정보를 주고 받기 위한 통신의 일종이다.
    
    → **인터넷 통신을 IPC의 확장으로 이해할 수 있다.** ( 서버 - 클라이언트 간 통신과 유사하기 때문 )
    
- 프로세스간 통신을 위해 **[[2]. 파이프 ( Pipe )](%5B11%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%5D%20IPC%2025b5ccd87d414dceb686267ac2c25702.md)**와 같은 개념이 등장하게 되었다.
- **쓰레드 간 통신보다 프로세스 간 통신이 어려운 이유**
    
    ---
    
    ```python
    프로세스와 쓰레드의 차이를 알고 있다면 이해하기 쉽다. 우리는 **fork**와 같은 함수로 프로세스를
    pthread_create와 같은 함수로 쓰레드를 각각 생성해주는데, 이 과정에서 큰 차이가 존재한다.
    
    프로세스는 생성되면서 **PC를 포함하여 메모리 공간등을 복사하여 별도의 자원을 할당**한다.
    쓰레드는 **메모리 공간과 자원을 공유**한다.
    
    따라서, 프로세스는 통신할 수 있는 공간이 없기 때문에 **통신을 위한 별도의 공간을 만들어 줘야 하므로**
    쓰레드간 통신보다 어렵다고 할 수 있다.
    ```
    

![Untitled](%5B11%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%5D%20IPC%2025b5ccd87d414dceb686267ac2c25702/Untitled.png)

## IPC의 종류

---

### [1]. 공유 메모리 ( Shared Memory )

---

<aside>
💡 공유 메모리가 데이터 자체를 공유하도록 지원하는 설비

</aside>

![Untitled](%5B11%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%5D%20IPC%2025b5ccd87d414dceb686267ac2c25702/Untitled%201.png)

- **프로세스 간 메모리 영역을 공유해서 사용**할 수 있도록 한다.
- 프로세스가 공유 메모리 할당을 커널에 요청하면 **커널은 해당 프로세스에 메모리 공간을 할당**한다.
    
    이후, 어떤 프로세스든 해당 메모리 영역에 접근할 수 있다.
    
    → 공유 메모리가 각 프로세스에게 첨부( Attach )하는 방식으로 작동하게 된다.
    
        ( = 각 프로세스가 메모리 영역에 첨부됨 )
    
- **프로세스 간 Read, Write를 모두 필요로 할 때** 사용된다.
- **대량의 정보**를 **다수의 프로세스에게 배포 가능**하다.
- **중개자 없이 곧바로 메모리에 접근**할 수 있기 때문에 **모든 IPC중에서 가장 빠르게 작동할 수 있다.**

### [2]. 파이프 ( Pipe )

---

<aside>
💡 통신을 위한 메모리 공간( 버퍼 )을 생성하여 프로세스가 데이터를 주고 받게끔 한다.

</aside>

![Untitled](%5B11%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%5D%20IPC%2025b5ccd87d414dceb686267ac2c25702/Untitled%202.png)

- **[2] - 1. 익명 파이프 ( Anonymous PIPE )**
    
    ---
    
    - 일반적인 파이프
    - **통신할 프로세스가 명확하게 알 수 있는 경우 사용**
        
        → [부모 - 자식] 혹은 형제 간 통신에 사용
        
        → **외부 프로세스에서 사용할 수 없다.**
        
    - 파이프는 두 개의 프로세스를 연결한다.
        
        → 하나의 프로세스는 **데이터를 쓰기만**, 다른 하나는 **읽기만** 할 수 있다 : `**반이중 통신**`
        
    - 송/수신을 모두 하기 원한다면 두 개의 파이프를 만들어야 한다.
    - 간단하게 사용 가능하며 pipe 함수로 생성한다
    
    **단점**
    
    1. 반이중 통신 : 양방향 통신이 필요한 경우, PIPE 두 개를 만들어야 하므로 구현이 복잡해질 수 있다.
    2. 전이중 통신을 고려해야할 상황이라면 낭비가 심하기 때문에 좋은 선택이 아니다.
- **[2] - 2. 네임드 파이프 ( Named PIPE )**
    
    ---
    
    - 전혀 모르는 상태의 프로세스들 사이의 통신에 사용
    - 익명 파이프의 확장된 상태로 부모 프로세스와 무관한 다른 프로세스도 통신 가능
        
        — 프로세스 통신을 위해 이름이 있는 파일을 사용하기 때문에 가능하다.
        
        — FIFO라 불리는 특수 파일을 통해 서로 관련 없는 프로세스 간 통신에 사용한다.
        
            (= 외부 프로세스와 통신 가능 )
        
    - mkfifo 또는 mknod 함수로 생성한다
    
    **단점**
    
    1. 반이중 통신 → 전이중 통신을 위해서는 익명 파이프처럼 2개를 만들어야 한다.

### [3]. 소켓 ( Socket )

---

<aside>
💡 Unix 도메인 소켓 또는 IPC 소켓은 동일한 호스트 운영 체제에서 실행되는

**프로세스 간 데이터를 교환하기 위한 데이터 통신 엔드 포인트**이다.

</aside>

![Untitled](%5B11%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%5D%20IPC%2025b5ccd87d414dceb686267ac2c25702/Untitled%203.png)

- 네트워크 소켓 통신을 위해 데이터를 공유한다.
    
    ---
    
    - 데이터 교환을 위해 양쪽 PC에서 각각 임의의 포트를 정하고 해당 포트 간의 대화를 통해 데이터를 주고받는 방식이다.
    - 이 때, 각 PC의 PORT를 담당하는 소켓은 각각 하나의 프로세스이다.
        
        → 즉, 해당 프로세스는 임의의 PORT를 맡아 데이터를 송수신하는 역할을 진행하는 프로세스
        
    
    **과정**
    
    ---
    
    1. 각각의 PC에서 프로세스를 통해 타 PC PORT에 연결하라는 명령 전송
    2. 두 프로세스는 서로 확인 과정을 거쳐 연결을 진행
    3. 연결 후 마치 PIPE와 같이 1 대 1로 데이터를 주고받는 방식이다.
    
- 클라이언트와 서버가 소켓을 통해서 통신하는 구조로, **원격에서 프로세스 간 데이터 공유 시 사용**
- `**전이중 통신**`이 가능하다.
- 서버-클라이언트 환경 구축에 용이하다.
    
    — 서버 : bind, listen, accept
    
    — 클라이언트 : connect
    
- 중대형 애플리케이션에서 주로 사용한다.

### [4]. 메시지 큐 ( Message Queue )

---

![Untitled](%5B11%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%5D%20IPC%2025b5ccd87d414dceb686267ac2c25702/Untitled%204.png)

- 입출력 방식은 [**[2] - 2. 네임드 파이프 ( Named PIPE )**](%5B11%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%5D%20IPC%2025b5ccd87d414dceb686267ac2c25702.md) 와 동일하다.
- **사용할 데이터에 번호**를 붙이면서 **여러 프로세스가 동시에 데이터를 쉽게** 다룰 수 있다.
- 메시지의 접근을 위해서는 `**Key**`가 필요하다.
- `**Named PIPE**` 와 다른점
    
    ---
    
    1. 메시지 큐는 파이프처럼 데이터의 흐름이 아니라 **메모리 공간**이다. (= 메모리를 사용한 PIPE )
    2. PIPE나 FIFO와 달리, **다수의 프로세스간 메시지를 전달**할 수 있다.

### [5]. 메모리 맵 ( Memory Map )

---

<aside>
💡 메모리 맵은 **열린 파일을 메모리에 매핑시켜서 공유**하는 방식 (= 공유 매개체가 파일 + 메모리 )

</aside>

![Untitled](%5B11%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%5D%20IPC%2025b5ccd87d414dceb686267ac2c25702/Untitled%205.png)

- 공유 메모리처럼 메모리를 공유해준다.
- 주로 **파일로 대용량 데이터를 공유해야 할 때 사용**한다.
- FIFO IO가 느릴 때 사용하면 좋다.
- 대부분 OS에서는 프로세스를 실행할 때 실행 파일의 각 세그먼트를 메모리에 사상하기 위해 메모리 맵  파일을 이용한다.
- 메모리 맵 파일은 **사용중에 파일의 크기를 바꿀 수 없다.**
    
    → 메모리 맵 파일을 사용하기 **이전, 또는 이후에만** 파일의 크기를 바꿀 수 있다.
    

### [6]. RPC ( Remote Procedure Call )

---

<aside>
💡 별도의 원격 제어를 위한 코딩 없이 **다른 주소 공간에서 함수나 `프로시저`를 실행할 수 있게**하는

**프로세스 간 통신 기술**

</aside>

- RPC 방법은 분산 네트워크 망에서 많이 사용된다.
- 분리된 PC의 데이터를 마치 내 PC에 존재하는 것처럼 데이터를 가져와 사용하는 통신방법이다.
    - `**스텁( Stub )**` 을 통해서 마치 자신의 디스크에 존재하는 것 처럼 착각을 일으켜 사용한다.
        
        `**스텁( Stub )**` : 리눅스에서 공유 라이브러리의 일부 중 하나
        
    - `**프로시저**` : 루틴, 서브루틴, 함수와 같은 뜻으로 사용되며 하나의 프로시저는 특정 작업을 수행하기 위한 프로그램의 일부이다.
    

# 🔗   참조 링크

---

[[OS] 프로세스 간 통신 방법(Inter Process Communication, IPC)](https://dar0m.tistory.com/233)