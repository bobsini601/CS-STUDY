> index
> 

# 📌 동기화 문제 (Synchronization problem)

## 📍 동기화 문제

---

동시에 공유 자원에 접근하는 것은 데이터의 일관성을 해칠 수 있다. **프로세스들의 실행 순서를 정하여 공유 자원의 일관성을 보장**하는 것을 동기화(Synchronization)라고 한다.

동기화 문제 : 공유 데이터의 동시 접근으로 인해 발생하는 데이터의 불일치 문제

## 📍 경쟁 상태 (race_condition)

---

<aside>
💡 **여러 프로세스들의 공유 자원에 동시에 접근하려고 하는 상황**

</aside>

어떤 프로세스가 마지막으로 데이터에 접근했는지에 따라 데이터의 상태가 달라지게 된다. 즉, 데이터의 일관성을 보장할 수 없어진다.

이런 경쟁 상태의 문제를 해결하기 위해 프로세스들은 동기화(Synchronized)되어야 한다.

## 📍 임계 영역 (Critical Section)

---

<aside>
💡 공유 자원에 접근할 때 순서 등의 이유로 결과가 달라지는 영역

</aside>

공유되는 자원, 즉 동시접근하려고 하는 그 자원 (ex. 연필, 노트) 에서 문제가 발생하지 않게 독점을 보장해줘야 하는 영역을 임계 영역이라고 한다.

임계 영역을 구현하기 위해서는 3가지 조건을 충족해야 한다.

1.  `**상호배제 (Mutual Exclusion)**`

<aside>
👉 한 프로세스가 임계 영역에 들어갔을 때 다른 프로세스는 들어갈 수 없다.
**오직 하나의 process/thread만 진입 가능하게 한다!!**

</aside>

프로세스 P가 해당 임계 영역을 수행 중이라면, 다른 프로세스들은 해당 임계영역을 수행 해서는 안된다.
 

2.  `**진행 (Progress)**`

<aside>
👉 임계 구역에 들어간 프로세스가 없는 상태에서 들어가려 하는 프로세스가 여러개라면 어느 것이 들어갈지 결정해줘야 한다.

</aside>

3.  `**한정 대기 (Bounded Waiting)**`

<aside>
👉 임계 구역으로 진입하기 위해서 대기 중인 process/thread들은 대기하면서 **bound를 설정**해야 한다.

</aside>

한 프로세스만 계속 임계영역을 수행하는 기아(Starvation)문제를 방지하기 위해, 한 번 임계 영역에 들어간 프로세스는 한정(bound)을 두어 다른 프로세스도 해당 임계 영역을 수행 할 수 있도록 해야한다.

프로세스가 임계 구역으로 들어가기 위해서 요청을 한 후 대기를 할 때 언제까지 대기를 해야할지 bound 를 설정해줘야 무한정 기다리는 경우가 생기지 않기 때문에 필요합니다.

# 📌 프로세스 제어 블록 (Process Control Block)

> Process Management
> 

---

CPU에 프로세스가 여러 개일 때, CPU 스케줄링을 통해 관리하는 것을 말합니다.

이때, CPU는 각 프로세스들이 누군지 알아야 관리가 가능합니다.

이러한 프로세스들의 특징을 갖고 있는 것이 바로 **Process Metadata**입니다.

Process Metadata에는 다음과 같은 정보들이 있습니다.

- `Process ID` : PID(Process Identification Number) 라고도 합니다.
    
    : 프로세스 고유 식별 번호
    
- `Process State` (프로세스 상태)
    
    : 프로세스의 현재 상태(준비, 실행, 대기 상태)를 기억시킵니다.
    
- `Process Priority` (스케줄링 정보)
    
    : 프로세스 우선순위 등과 같은 스케줄링 관련 정보를 기억시킵니다.
    
- `CPU Registers`
    
    : 프로세스의 레지스터 상태를 저장하는 공간 등. CPU 내 범용 레지스터(AX, BX, CX, DX), 데이터 레지스터(SP, BP, SI, DI), 세그먼트 레지스터(CS, DS, ES, SS) 등이 갖고 있는 값을 기억시킵니다.
    
- `Owner` (계정 정보)
    
    : CPU 사용시간의 정보(Quantum), 각종 스케줄러에 필요한 정보를 기억시킵니다.
    
- `기억장치 관리 정보`
    
    : 프로그램이 적재될 기억 장치의 상한치, 하한치, 페이지 테이블 등의 정보를 기억시킵니다.
    
- `입출력 정보`
    
    : 프로세스 수행 시 필요한 주변 장치, 파일들의 정보를 기억시킵니다.
    
- `프로그램 카운터` (계수기)
    
    : 다음에 실행되는 명령어의 주소를 기억시킵니다.
    

이러한 정보들이 담긴 메타데이터는 프로세스가 생성되면 **PCB(Process Control Block)**이라는 곳에 저장이 됩니다.

> PCB (Process Controll Block)
> 

---

<aside>
💡 운영체제에서 프로세스에 대한 메타데이터(pid, process state, ..)를 저장한 ‘데이터’

</aside>

프로세스가 생성되면 운영체제는 해당 PCB를 생성합니다. 하나의 PCB 안에는 하나의 프로세스의 정보가 담겨있습니다.

![https://raw.githubusercontent.com/Songwonseok/CS-Study/main/OS/images/PCBContextSwitching-1.png](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/OS/images/PCBContextSwitching-1.png)

**프로그램 실행 → 프로세스 생성 → 프로세스 주소 공간에 (코드, 데이터, 스택) 생성 → 이 프로세스의 메타데이터들이 PCB에 저장**

프로그램이 실행되면 프로세스가 생성되고 프로세스 주소값들에 앞서 설명한 스택, 힙 등의 구조를 기반으로 메모리가 할당됩니다. 그리고 이 프로세스의 메타데이터들이 PCB에 저장되어 관리됩니다. 이는 프로세스의 중요한 정보를 포함하고 있기 때문에 일반 사용자가 접근하지 못하도록 커널 스택의 가장 앞부분에서 관리됩니다.

> PCB(Process Control Block) 상세 구조
> 

---

![https://raw.githubusercontent.com/Songwonseok/CS-Study/main/OS/images/PCBContextSwitching-2.png](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/OS/images/PCBContextSwitching-2.png)

- Process id
- Process state
    
    프로세스 상태(`Create`, `Ready`, `Running`, `Block`, `terminated`)
    
- Program counter
    
    다음 실행할 명령어의 주솟값
    
- CPU register
    
    CPU에서 사용한 레지스터의 값을 잃지 않기 위해 PCB에 그 값을 저장
    
- CPU scheduling information
    
    프로세스의 우선순위, 최종 실행 시간, 스케줄링 큐를 가리키는 포인터 등
    
- Memory management information
    
    레지스터, 페이지 테이블, 세그먼트 테이블의 base, limit값에 대한 정보
    
- Accounting information
    
    CPU 사용 시간, 실제 사용된 시간, 시간 제한 등
    
- I/O status information
    
    프로세스에 할당된 I/O기기에 해당하는 정보
    

> PCB가 필요한 이유?
> 

---

CPU에서는 프로세스의 상태에 따라 교체 작업이 이루어집니다. (인터럽트가 발생해서 할당받은 프로세스가 Block 상태가 되고 다른 프로세스를 running으로 바꿀 때)

**이때, 앞으로 다시 수행할 Block 상태의 프로세스의 상태값을 PCB에 저장해두는 것**입니다.

> PCB의 관리 방식
> 

---

- **Linked List** 방식으로 관리가 됩니다. PCB List Head에 PCB들이 생성될 때마다 붙게 됩니다. 주솟값으로 연결이 이루어져 있는 연결 리스트 형태로, **삽입 삭제가 용이**합니다.
    
    **즉, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스 완료 시 제거가 됩니다.**
    
- 이렇게 수행 중인 프로세스를 변경할 때, **CPU의 레지스터 정보가 변경되는 것**을 **Context Switching이라고 합니다.**

# 📌 문맥교환 (Context Switching)

<aside>
💡 CPU가 현재 작업 중인 프로세스에서 다른 프로세스로 넘어갈 때 지금까지의 프로세스 상태를 PCB에 저장하고, 새 프로세스의 저장된 상태를 PCB에서 읽어 다시  레지스터에 적재하는 작업

PCB를 교환하는 과정

</aside>

> Context Switching의 뜻
> 

---

- **CPU가 현재 실행하고 있는 Task(Process, Thread)의 상태를 저장하고, 다음 진행할 Task의 상태 및 Register 값들에 대한 정보(Context)를 읽어 새로운 Task의 Context 정보로 교체하는 과정**
- 다르게 말하면, **CPU가 이전의 프로세스 상태를 PCB에 보관하고, 또 다른 프로세스의 정보를 PCB에서 읽어서 레지스터에 적재하는 과정**
- 또 다르게 말해보면 **다중 프로그래밍 시스템에서 CPU가 할당되는 프로세스를 변경하기 위해 현재 CPU를 사용하여 실행되고 있는 프로세서의 상태 정보를 저장하고 제어권을 인터럽트 서비스 루틴(ISR)에게 넘기는 작업**
- 여기서 Context란 CPU가 다루는 Task(Process / Thread)에 대한 정보를 말하고, 대부분의 정보는 Register에 저장되고 PCB로 관리됩니다.
- 인터럽트가 발생하거나, 실행 중인 CPU 사용 허가 시간을 모두 소모하거나, 입출력을 위해 대기해야 하는 경우 Context Switching이 발생합니다.
    
    즉, Context Switching은 프로세스가 `Ready -> Running` , `Running -> Ready` , `Running -> Block` 처럼 상태 변경 시에 발생합니다.
    

한 프로세스에 할당된 시간이 끝나거나 인터럽트에 의해 발생합니다. 컴퓨터는 많은 프로그램을 동시에 실행하는 것처럼 보이지만 어떠한 시점에서 실행되고 있는 프로세스는 단 1개이며, 많은 프로세스가 동시에 구동되는 것처럼 보이는 것은 다르 프로세스와의 컨텍스트 스위칭이 아주 빠른 속도로 실행되기 때문입니다.

참고로 사실 현대 컴퓨터는 멀티코어의 CPU를 가지기 때문에 한 시점에 1개의 프로그램이라는 설명은 틀린 설명입니다. 하지만 컨텍스트 스위칭을 설명할 때는 싱글 코어를 기준으로 설명합니다.

> Context Switching이 필요한 이유
> 

---

만약 컴퓨터가 매번 하나의 Task만 처리할 수 있다면?

- 다음 Task를 처리하기 위해서 현재 Task가 끝날 때까지 기다려야 합니다.
- 반응속도가 매우 느리고 사용하기 불편합니다.

**다양한 사람들이 동시에 사용하는 것처럼 하기 위해서 Context Switching이 필요하게 되었습니다.**

- 컴퓨터 멀티태스킹을 통해 빠른 반응속도로 응답 가능합니다.
- 빠르게 Task를 바꾸면서 실행하기에 사람은 실시간처리가 되는 것처럼 보입니다.
- CPU가 Task를 바꿔가며 실행하기 위해 Context Switching이 필요하게 되었습니다.

> Context Switching 수행 과정
> 

---

1. Task의 대부분 정보는 Register에 저장되고 PCB(Process Control Block)로 관리가 되고 있습니다.
2. 현재 실행하고 있는 Task의 PCB 정보를 저장하게 됩니다.(Process Stack, Ready Queue)
3. 다음 실행할 Task의 PCB 정보를 읽어 Register에 적재하고 CPU가 이전에 진행했던 과정을 연속적으로 수행할 수 있게 됩니다.

![CA6F71A9-875A-4DBE-94F1-38F5B86C8190.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d0eb16d-e22a-4873-82eb-65b8bbc7723b/CA6F71A9-875A-4DBE-94F1-38F5B86C8190.jpeg)

1개의 프로세스 A가 실행하다 멈추고, 프로세스 A의 PCB를 저장하고 다시 프로세스 B를 로드하여 실행합니다. 그리고 다시 프로세스 B의 PCB를 저장하고 프로세스 A의 PCB를 로드합니다. 컨텍스트 스위칭이 일어날 때 앞의 그림처럼 유휴시간 (idle-time)이 발생하는 것을 볼 수 있습니다. 이 뿐만 아니라 이 컨텍스트 스위칭에 드는 비용이 더 있습니다. 바로 `캐시미스` 입니다.

- ContextSwitching이 발생하는 시간 : 유휴 시간 (idle time)

**비용 : 캐시미스

컨텍스트 스위칭이 일어날 때 프로세스가 가지고 있는 메모리 주소가 그대로 있으면 잘못된 주소 변환이 생기므로 캐시클리어 과정을 겪게 되고 이 때문에 캐시미스가 발생합니다.

> Process vs Thread
> 

---

컨텍스트 스위칭은 스레드에서 일어납니다.

- context switching 비용 : 프로세스 > 스레드

그 이유는 Thread는 Stack 영역을 제외한 모든 메모리를 공유하기에 Context Switching 발생 시 Stack 영역만 변경하면 됩니다. 따라서, 스레드 컨텍스트 스위칭의 경우 **비용이 더 적고** **시간이 더 적게** 걸립니다.

> Context Switching Cost
> 

---

Context Switching이 발생하게 되면 다음과 같은 Cost가 소요됩니다.

1. Cache 초기화
2. Memory Mapping 초기화
3. 메모리의 접근을 위해서 Kernel은 항상 실행되어야 합니다.

따라서 잦은 Context Switching은 성능 저하를 가져옵니다.

> Context Switching과 Interrupt
> 

---

CPU는 하나의 프로세스 정보만을 기억합니다. 여러 개의 프로세스가 실행되는 다중 프로그래밍 환경에서 CPU는 각각의 프로세스의 정보를 저장했다 복귀하고 다시 저장했다 복귀하는 일을 반복합니다. 

프로세스의 저장과 복귀는 프로세스의 중단과 실행을 의미합니다. 

프로세스의 중단과 실행 시 인터럽트가 발생하므로, 문맥 교환이 많이 일어난다는 것은 인터럽트가 많이 발생한다는 것을 의미합니다.

> Context Switching과 시간 할당량
> 

---

프로세스들의 `**시간 할당량**`은 시스템 성능의 중요한 역할을 합니다. 시간 할당량이 적을수록 사용자 입장에서는 여러 개의 프로세스가 거의 동시에 수행되는 느낌을 갖지만 인터럽트의 수와 문맥 교환의 수가 늘어납니다. 프로세스의 실행을 위한 부가적인 활동을 오버헤드(간접 부담 비용)이라고 하는데, 이 또한 문맥 교환 수와 같이 늘어나게 됩니다. 정리하자면 다음과 같습니다.

- 시간 할당량이 적어지면 : 문맥 교환 수, 인터럽트 횟수, 오버헤드가 증가하지만 여러 개의 프로세스가 동시에 수행되는 느낌을 갖는다.
- 시간 할당량이 커지면 : 문맥 교환 수, 인터럽트 횟수, 오버헤드가 감소하지만 여러 개의 프로세스가 동시에 수행되는 느낌을 갖지 못한다.

# 🤜 CS 질문

## Q. PCB는 뭔가요?

PCB는 운영체제에서 프로세스에 대한 메타데이터를 저장한 ‘데이터’를 말합니다. 프로세스 제어 블록이라고도 합니다. 프로세스가 생성되면 운영체제는 해당 PCB를 생성합니다.

프로그램이 실행되면 프로세스가 생성되고 프로세스 주소값들이 앞서 설명한 스택, 힙 등의 구조를 기반으로 메모리가 할당됩니다. 그리고 이 프로세스의 메타데이터들이 PCB에 저장되어 관리됩니다. 이는 프로세스의 중요한 정보를 포함하고 있기 때문에 일반 사용자가 접근하지 못하도록 커널 스택의 가장 앞부분에서 관리됩니다.

## Q. **Context Switching이란?**

하나의 프로세스가 CPU를 사용 중인 상태에서 다른 프로세스가 CPU를 사용하도록 하기 위해, 이전의 프로세스 상태를 보관하고 새로운 프로세스의 상태를 적재하는 작업

한 프로세스의 문맥은 그 프로세스의 PCB에 기록됨

> ref
> 

---

[[운영체제] 동기화 문제(Synchronization problem), 경쟁 상태(Race Condition), 임계 영역(Critical Section)](https://code-lab1.tistory.com/50?category=1213006)

[CS-Study/PCB Context Switching.md at main · Songwonseok/CS-Study](https://github.com/Songwonseok/CS-Study/blob/main/OS/PCB%20Context%20Switching.md)

[면접을 위한 CS 전공지식 노트 - YES24](http://www.yes24.com/Product/Goods/108887922)