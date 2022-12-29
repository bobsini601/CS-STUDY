> index
> 

---

## 📌 Promotion & Casting

<aside>
👉 묵시적 형 변환 : 작은 것 → 큰것 (변환 x )
명시적 형 변환 : 큰 것 → 작은것 (잘려서 속성이 바뀔 수 있음)

</aside>

### 🤜 Promotion (자동 형변환, 묵시적 형변환)

<aside>
💡 프로그램 실행 도중에 **자동적으로** 형변환(타입변환)이 일어나는 것

</aside>

- **작은** 메모리 크기의 데이터 타입을 **큰** 메모리 크기의 데이터 타입으로 변환하는 행위

```java
byte a = 10; // 정수 10을 byte 데이터 타입의 변수인 a에 저장
int b = a;   // byte 데이터 타입의 변수인 a를 int 데이터 타입의 변수인 b에저장
```

> 자동 형변환 (Promotion)이 이루어지는 순서
> 

---

![보시면, long 데이터 타입의 메모리 크기는 8byte이고, float 데이터 타입의 메모리 크기는 4byte인데, long 데이터 타입에서 float 데이터 타입으로 자동 형변환(Promotion)이 가능합니다. 그 이유는 **표현할 수 있는 값의 범위가 float가 더 크기 때문입니다.**](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd602e31-566a-4ea6-883d-71d121036b68/Untitled.png)

보시면, long 데이터 타입의 메모리 크기는 8byte이고, float 데이터 타입의 메모리 크기는 4byte인데, long 데이터 타입에서 float 데이터 타입으로 자동 형변환(Promotion)이 가능합니다. 그 이유는 **표현할 수 있는 값의 범위가 float가 더 크기 때문입니다.**

❗ **주의할 점**

메모리 크기가 큰 데이터 타입이라도, 타입 범위를 포함하지 못한다면 자동 형변환(Promotion) 이 불가능합니다.

- byte(1) 데이터 타입 -> char(2) 데이터 타입 : 자동 형변환 불가
- float(4) 데이터 타입 -> long 데이터 타입 : 자동 형변환 불가

| 자료형 | 메모리 크기 (byte) | 값의 범위 |
| --- | --- | --- |
| byte | 1 | -128 ~ 127 |
| char | 2 | 유니코드의 0 ~ 65535 |
| short | 2 | 32,768 ~ 32,767 |
| int | 4 | -2,147,483,648 ~ 2,147,483,647 |
| long | 8 | -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 |
| float | 4 | 1.40239846E-45f                                          ~ (표현 가능 양수 범위)                                          3.40282347E+38f |
| double | 8 | 4.94065645841246544E-324                                          ~ (표현 가능 양수 범위)                                          1.79769313486231570E+308 |
| boolean | 1 | true , false 2가지 |

### 🤜 Casting (강제 형변환, 명시적 형변환)

<aside>
💡 특정 조건을 갖추지 못했지만, 형변환을 하고 싶을때 사용하는 것

</aside>

```java
int intValue = 1;
byte byteValue = intValue;
```

![int에서 byte 데이터 타입 메모리 영역만 넣자니 앞에 있는 3byte 값이 날아갑니다. 
그러므로, 자동 형변환이 된다면 정상적이지 않은 값이 나올 수 있기 때문에 자동 형변환을 하지 않습니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e29a421-9046-4d79-a9e5-087f5235d340/Untitled.png)

int에서 byte 데이터 타입 메모리 영역만 넣자니 앞에 있는 3byte 값이 날아갑니다. 
그러므로, 자동 형변환이 된다면 정상적이지 않은 값이 나올 수 있기 때문에 자동 형변환을 하지 않습니다.

```java
int intValue = 1;
byte byteValue = (byte) intValue;
```

### 🤜 형변환 연산

+, -, *, / 과 같은 기본적인 사칙연산은 같은 타입의 피연산자 간에만 수행되기 때문에 서로 다른 데이터 타입의 피연산자가 있을 경우 두 피연산자 중 크기가 큰 타입으로 자동 형변환(Promotion)된 후 연산이 수행됩니다. 

예를 들어 `int` 데이터 타입의 피연산자와 `double` 타입의 피연산자를 덧셈하면 int 데이터 타입의 피연산자가 **double 데이터 타입으로** 자동 형변환(Promotion)되고 연산이 수행됩니다. 연산의 결과도 double 데이터 타입이 됩니다.

```java
int intValue = 10;
double doubleValue = 5.5;
double result = intValue + doubleValue; 
// intValue 변수값과 doubleValue 변수값을 더해서 double 타입의 result 변수에 저장
```

만약 int 데이터 타입의 연산 결과를 얻고 싶다면, 강제 형변환(Casting)를 통해 아래와 같이 작성해주시면 됩니다.

```java
int intValue = 10;
double doubleValue = 5.5;
int result = intValue + (int) doubleValue;
// intValue 변수값과 doubleValue변수값을 더해서 int 타입의 result 변수에 저장
```

# 📌 고유 락 (Intrinsic Lock)

### 🤜 **가시성(visiblity)**

동기화 프로그램의 이슈 중 하나는 **가시성 문제**이다. 

가시성 문제는 스레드가 변경한 값이 메인 메모리에 저장되지 않아서 다른 스레드가 이 값을 볼 수 없는 상황을 말한다. 

여러 개의 스레드가 동시에 같은 작업을 수행하지 않는다고 해도 여전히 가시성 문제는 남아있다. 

`cnt++`과 같은 연산을 수행할 때, 메모리에서 읽고, 증가시키고, 쓰는 과정이 이루어진다. 

read-modify-write 과정 동안 한 스레드가 쓴 값을 다른 스레드가 볼 수도 있고 그렇지 않을 수도 있기 때문이다. 가시성 문제를 해결하는 방법은 **`volatile`**이나 **`lock`**을 이용하는 방법이 있다.

### 🤜 **volatile이란?**

volatile이란 Java 변수를 **메인 메모리에서 바로 읽어(Read) 조작하고 메인 메모리에 반영(Write)하겠다고 명시하는 키워드**이다. volatile 키워드가 없는 변수는 값을 변경한 후 언제 다시 메인 메모리에 반영될지 보장할 수 없다.

```java
public volatile int cnt = 0;
```

스레드가 cnt 값을 증가시키는 작업을 수행할 때 다음 과정을 거친다.

![https://github.com/Songwonseok/CS-Study/raw/main/Language/images/IntrinsicLock-1.png](https://github.com/Songwonseok/CS-Study/raw/main/Language/images/IntrinsicLock-1.png)

- 메인 메모리로 부터 자신의 cpu cache 영역에 값을 가져온 후
- 값을 증가시키고
- 변경된 값을 메인 메모리에 반영함

cnt를 증가시키는 작업을 하는 여러 개의 스레드가 있을 때, 한 스레드가 변경된 값을 아직 메인 메모리에 반영하기 전에 다른 스레드가 메인 메모리에서 값을 읽고 같은 연산을 수행한다면 잘못된 결과를 확인할 수 있다. 이러한 상황에서는 volatile 키워드로 가시성을 보장할 수 없다. 때문에 volatile 키워드로 가시성을 보장하는 것은 **하나의 스레드만 write**를 하고 **다른 스레드는 read**하는 상황일 때 적합하다. (둘다 write하는 연산을 할 수 없다는 것이네요)

### 🤜 **자바의 고유 락(IntrinsicRock)**

자바의 모든 객체는 고유의 락(intrinsic lock)을 가지고 있고, 이를 `모니터`, `모니터 락`, `뮤텍스`라고도 한다. 고유 락을 이용한 `synchronized` 블록은 동시성 문제를 해결하는 가장 간편한 방법이다.

```java
public class Counter {
  private int count;
  
  public int increase() {
    return ++count; // 스레드 안전하지 않은 연산.
  }
}
```

앞서 설명한 cnt 변수의 증가 예시처럼 `increase()` 함수는 동시성 문제가 있다. 이를 객체의 lock을 이용하는 `synchronized`를 통해 변수로 접근하는 스레드를 제어할 수 있다.

```java
public class Counter {
  private int count;
 
  public int increase() {
    synchronized(this) {
      return ++count;
    }
  }
}
```

synchronized가 increase() 메소드 전체를 감싸고 있는데 이런 경우에는 synchronized 키워드를 추가하는 것으로 더욱 간결하게 표현할 수 있다.

```java
public class Counter {
  private int count;
  
  public synchronized int increase() {
    return ++count;
  }
}
```

### 🤜 **재진입 가능성(Reentrancy)**

자바의 고유 락은 재진입 가능하다. 재진입 가능하다는 것은 락의 획득이 호출 단위가 아닌 스레드 단위로 일어난다는 것을 의미한다. 이미 락을 획득한 스레드는 같은 락을 얻기 위해 대기할 필요 없다.

```java
public class Reentrancy {
  public synchronized void a() {
    System.out.println("a");
    // b가 synchronized로 선언되어 있지만 a진입시 이미 락을 획득하였으므로,
    // b를 호출할 수 있다.
    b();
  }
  public synchronized void b() {
    System.out.println("b");
  }
  public static void main(String[] args) {
    new Reentrancy().a();
  }
}
```

b 메소드는 `synchronized`로 선언되어 있지만 a 메소드 내부에서 b를 호출하는 시점에는 이미 해당 객체의 락이 획득한 상태이므로 대기 없이 b를 호출할 수 있다. 만약 고유 락이 재진입이 불가능하다면 b를 호출하는 지점에서 데드락이 발생할 수 있다.

### 🤜 **구조적인 락(StructuredLock)**

`synchronized`를 이용한 동기화를 구조적인 락(structured lock)이라고 한다. `synchronized` 블록 단위로 락의 획득과 해제가 일어나므로 구조적이라고 한다. synchronized 블록을 진입할 때 락의 획득이 일어나고, 블록을 벗어날 때 락의 해제가 일어난다. 따라서 구조적인 락 A와 B가 있을 때 A 획득 -> B 획득 -> B 해제 -> A 해제는 가능하지만 A 획득 -> B 획득 -> A 해제 -> B 해제는 불가능 하다. 이런 순서로 락을 사용해야 하는 경우라면 `ReentrantLock`과 같은 명시적인 락을 사용해야 한다.

### 🤜 **명시적인 락(ReentrantLock)**

`synchronized`와 동일하게 가시성과 상호 배제 기능을 제공한다. 명시적인 락은 `synchronized`만으로 해결할 수 없는 복잡한 상황에서 사용하기 위한 방법이다.

```java
import java.util.concurrent.locks.ReentrantLock;

Lock lock = new ReentrantLock();
lock.lock();
try { // 임계영역
 .
 .  
 .
} finally {
    lock.unlock();
}
```

명시적인 락을 사용할 경우 `try`문에서 예외가 발생하면 락이 해제되지 않는 경우가 발생한다. 따라서 락이 해제될 수 있도록 `catch`,`finally` 블록에서 락을 해제하는 것이 중요하다.

- **공정성** ReentrantLock는 두 종류의 락 공정성 설정을 지원한다. 공정성은 스레드가 사용하고자하는 락을 이미 다른 스레드가 사용중일 때 대기하는 스레드를 처리하는 기준을 의미한다. `synchronized`는 스레드간의 락을 획득하는 순서를 보장해주지 않고, ReentrantLock는 **공정한 방법**과 **불공정한 방법**을 지원한다.
    - **공정한 방법**
        - 스레드가 락을 사용하고자 할 때, 해당 락이 이미 사용중이라면 스레드는 대기열 맨 뒤에 위치한다.
    - **불공정한 방법**
        - 스레드가 락을 사용하고자 할 때, 해당 락이 이미 사용중이라면 스레드는 대기열 맨 뒤에 위치한다.
        - 스레드가 락을 사용하고자 할 때, 그 순간 해당 락이 해제되었다면 대기열에 스레드가 있더라도 락을 확보한다.
    - **성능** 대부분의 경우 공정한 방법보다 불공정한 방법을 적용하는 것이 성능상의 이점이 크다. 그 이유는 대기 상태에 있던 스레드가 다시 실행 상태로 돌아가고, 실제로 실행되기까지 상당한 시간이 걸리기 때문이다.
- **명시적인 락을 사용해야하는 경우**
    - 락을 확보할 때 타임아웃을 지정해야 하는 경우
    - 대기 상태 큐 처리 방법을 공정하게 해야 하는 경우
        - ex) 스레드 간의 락 경쟁이 심하지 않거나, 락을 한 번 획득하면 상대적으로 오래 가지고 있는 경우
    - 동시성을 보장해야 하는 코드가 블록 형태를 넘어서는 경우

### 🤜 **읽기/쓰기 락(Read/Write Lock)**

명시적인 락은 한 시점에 하나의 스레드만 락을 확보할 수 있다. 이로인해 동시성을 보장해야하는 상황에서 스레드의 접근을 제한하기도 하지만 그럴 필요가 없는 경우에도 제한한다. 그 예로 read 연산은 락의 획득과 무관하게 여러 스레드가 동시에 접근해도 데이터의 일관성을 해치지 않지만 명시적인 락에서 제한된다. 명시적인 락을 사용하는 경우 read 연산을 수행하기 위해 다수의 스레드는 락을 획득하기 위해 대기해야한다. 이러한 문제를 해결한 기법이 Read/Write Lock이다.

- **동작 방식**
    - A 스레드가 read 연산을 수행하면 read-lock을 획득한다.
    - 객체가 read-lock 상태일 때 B 스레드가 read 연산을 수행하고 read-lock을 획득한다.
    - C 스레드가 write 연산을 수행하면 write-lock을 획득하고 모든 연산이 완료되어 write-lock이 해제될 때 까지 다른 스레드는 read/write lock을 획득할 수 없다.
- **성능**
    - 특정 상황에서 성능을 크게 높일 수 있다.
        - ex) 읽기 작업이 많고 쓰기 작업이 적은 구조에 사용하면 성능을 크게 높일 수 있음
- **고려사항**
    - 구현상의 복잡도가 높기 때문에 최적화된 상황이 아니면 명시적인 락에 비해 성능이 떨어지기도 한다.
    - read-write lock 적용 적합 여부는 성능 측정을 통해서만 알 수 있다.

[[읽고서] 자바 고유락과 Synchronization](https://brunch.co.kr/@kd4/156)

[Java의 고유 락(intrinsic lock)에 대해](http://happinessoncode.com/2017/10/04/java-intrinsic-lock/)

# 📌 Error & Exception

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/60c0f7bc-b6f5-4722-94b0-992f60d15dd4/Untitled.png)

## 🤜 **Error (오류)**

<aside>
💡 **컴퓨터 하드웨어의 오동작** 또는 **고장**으로 인해 응용프로그램에 이상이 생겼거나 JVM 실행에 문제가 생겼을 경우 발생하는 것 → 개발자가 미리 예측하여 처리할 수 없다.

</aside>

- 메모리 부족, stack overflow 와 같이 일단 발생하면 복구할 수 없는 상황
- 프로그램의 비정상적 종료를 막을 수 없음 → 디버깅 필요

![Error의 상속 관계도](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73cd3a01-3084-426b-9df7-f4ff206ff3bd/Untitled.png)

Error의 상속 관계도

> 대표적인 오류
> 

---

- StackOverflowError
    
    호출의 깊이가 깊어지거나 재귀가 지속되어 stack overflow 발생 시 던져지는 오류
    
- OutOfMemoryError
    
    JVM이 할당한 메모리의 부족으로 더 이상 객체를 할당할 수 없을 때 던져지는 오류
    
    이는 GC에 의해 추가적인 메모리가 확보되지 못하는 상황이기도 하다.
    

## 🤜 **Exception (예외)**

<aside>
💡 **개발자가 구현한 로직에서 발생한 실수나 사용자의 영향에 의해 발생**

</aside>

- 오류와 달리 개발자가 미리 **예측하여 방지할 수 있기에** 상황에 맞는 예외처리(Exception Handle)를 해야합니다.
- 읽으려는 파일이 없거나 네트워크 연결이 안되는 등 수습될 수 있는 비교적 상태가 약한 것들
- 프로그램 코드에 의해 수습될 수 있는 상황

throw의 의미 : 예외 전가

![Exception의 상속 관계도](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/36351a3a-8363-48b0-8d23-8f168efa1de6/Untitled.png)

Exception의 상속 관계도

### ◽ Checked Exception

<aside>
💡 예외에 대한 대처 코드가 없으면 컴파일이 진행되지 않음 → try-catch 꼭 써야 한다.

</aside>

- RuntimeExceptoin 클래스를 상속하지 않음!
- Complie Exception이라고도 하며 Exception을 바로 상속받습니다.
- 컴파일 시점에 예외를 catch 하는지 정적으로 확인합니다.
- 파일 시점에 예외에 대해 처리(try/catch) 하지 않는다면 컴파일 에러가 발생합니다.
- 트랜잭션 Rollback이 안된다는 속성도 있습니다.

### ◽ Unchecked Exception

<aside>
💡 예외에 대한 대처 코드가 없더라도 컴파일은 진행됨 → try-catch 안하고 넘어가겠다!

</aside>

- ⭐ RuntimeExceptoin 클래스를 상속!
- 조건문으로 충분히 해결 가능
- 컴파일 시점에 예외를 catch 하는지 확인하지 않습니다. → 컴파일 시점에 예외가 발생하는지 여부를 판단할 수 없습니다.
- 트랜잭션 Rollback이 된다는 속성도 있습니다.
- 예외가 발생하는 메서드에서 throws 예약어를 활용해 예외를 처리할 필요가 없습니다. 하지만 처리해도 괜찮습니다. 즉 명시적으로 예외처리를 강제하지 않습니다.
- ex.  `NullPointException`, `IllegalArgumentException`, `IndexOutOfBoundException`, `SystemException`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd642874-e4ab-4831-9182-236c98ac63c1/Untitled.png)

> 대표적인 오류
> 

---

- NullPointerException
    
    객체가 필요한 경우에 null을 사용하려고 시도할 경우 던져지는/ 던져질 수 있는 예외
    
- IllegalArgumentException
    
    메서드가 허가되지 않거나 부적절한 argument를 받았을 경우에 던져지는/ 던져질 수 있는 예외
    

### 📍  예외 처리 방법1. 예외 복구

<aside>
💡 예외 상황을 파악하고 문제를 해결하여 정상 상태로 돌려놓는 방법

</aside>

- 예외 상황을 파악하고 문제를 해결해서 정상 상태로 돌려놓는 방법
- 예외를 잡아서 일정 시간, 조건만큼 대기하고 다시 재시도를 반복한다.
- 최대 재시도 횟수를 넘기게 되는 경우 예외를 발생시킨다.

```java
final int MAX_RETRY = 100;
public Object someMethod() {
    int maxRetry = MAX_RETRY;
    while(maxRetry > 0) {
        try {
            ...
        } catch(SomeException e) {
            // 로그 출력. 정해진 시간만큼 대기한다.
        } finally {
            // 리소스 반납 및 정리 작업
        }
    }
    // 최대 재시도 횟수를 넘기면 직접 예외를 발생시킨다.
    throw new RetryFailedException();
}
```

### 📍 예외 처리 방법2. 예외 회피

<aside>
💡 예외 처리를 직접 담당하지 않고 호출한 메서드로 위임해 회피하는 방법

</aside>

- 그래도 예외 처리의 필요성이 있다면 어느 정도는 처리하고 던지는 것이 좋다.
- 긴밀하게 역할을 분담하고 있는 관가 아니라면 예외를 그냥 던지는 것은 무책임하다.

```java
// 예시 1
public void add() throws SQLException {
    // ...생략
}

// 예시 2
public void add() throws SQLException {
    try {
        // ... 생략
    } catch(SQLException e) {
        // 로그를 출력하고 다시 날린다!
        throw e;
    }
}
```

### 📍 예외 처리 방법3. 예외 전환

<aside>
💡 예외 회피와 비슷하게 메서드 밖으로 예외를 던지지만, 그냥 던지지 않고 적절한 예외로 전환해서 넘기는 방법

</aside>

- 조금 더 명확한 의미를 전달하기 위해 적합한 의미를 가지는 예외로 **변경**
- 예외 처리를 단순하게 만들기 위해 포장(wrap)할 수도 있다.

```java
// 조금 더 명확한 예외로 던진다.
public void add(User user) throws DuplicateUserIdException, SQLException {
    try {
        // ...생략
    } catch(SQLException e) {
        if(e.getErrorCode() == MysqlErrorNumbers.ER_DUP_ENTRY) {
            throw DuplicateUserIdException();
        }
        else throw e;
    }
}

// 예외를 단순하게 포장한다.
public void someMethod() {
    try {
        // ...생략
    }
    catch(NamingException ne) {
        throw new EJBException(ne);
        }
    catch(SQLException se) {
        throw new EJBException(se);
        }
    catch(RemoteException re) {
        throw new EJBException(re);
        }
}
```

# 📌 java 8 & java 11 차이

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/acaa6f14-f880-4ac3-914c-3436bb339cd0/Untitled.png)

※ 애플릿(Applet)이란?: 패널(Panel)을 상속하는 클래스로 웹브라우저에 담겨서 실행되는 작은 응용프로그램을 말함.

- AppletViewer : 자바 애플릿을 실행하기 위함이지만, 2015년-2016년 사이에 지원을 종료하였고, 이제와서 굳이 사용할일이 없기때문에 자바11부터는 지원하지 않음.
- AWTUtilities: GUI를 지원하기 위한 라이브러리. 오류가 많아서 자바8부터 사용 안하는것을 권장.
- *****String 클래스에 새로운 메소드 추가 [Java11]*****
    - isBlank() : 문자열이 비거나 공백일 경우 true 반환
    - lines() : 문자열을 줄 단위로 쪼개어 스트림 반환
    - repeat(n) : 문자열에 대해 n번 반복하여 붙여 반환
        
        ```java
        String str = "ABC";    
        String repeated = str.repeat(3); // "ABCABCABC"  - stripLeading() : 문자열 앞 공백 제거  
        ```
        
    - stripTrailing() : 문자열 뒤 공백 제거
    - strip() : 양쪽 공백 제거
- *****람다에서 로컬 변수 Var 사용 [Java11]*****
    
    람다는 타입을 스킵 할 수 있는데 이걸 사용하는 이유는 @Nullable 등의 어노테이션을 사용하기 위해 타입을 명시해야 할때. var를 사용하려면 괄호를 써야하며, 모든 파라미터에 사용해야 하고, 다른 타입과 혼용하거나 일부 스킵은 불가능함. 
    
    ```java
    (var n1, var n2) -> n1 + n2(var s1, s2) -> s1 + s2 // 불가. s2에도 var 필요
    (var s1, String x) -> s1 + x // 불가. String과 혼용 불가
    var s1 -> s1 // 불가. 괄호 필요.
    Function<String, String> toLowerCase = (var input) -> input.toLowerCase();
    ```
    
- *****java.nio.file.Files 클래스에 새로운 메소드 추가 [Java11]*****
    - writeString() : 파일에 문자열을 쓰고 경로로 반환
    - readString() : 파일 내용을 String으로 반환
    - isSameFile() : 서로 같은 파일을 바라보는지 확인. 같은 파일일 경우 true. 아니면 false
- *****자바 파일 실행 [Java11]*****
    
    javac를 통해 컴파일 하지 않고도, 바로 java 파일을 실행할 수 있게 되었다.
    
    ```
    // Java 11 이전
    $ javac HelloWorld.java
    $ java Helloworld
    Hello Java 8!
    
    // Java 11 이후
    $ java HelloWorld.java
    Hello Java 11!
    ```
    
- ***패턴 인식***
    
    Java 8에서는 asPredicate()를 통해 주어진 문자열에서 패턴을 찾을 수 있는지 테스트 하기 위해 '조건자'를 반환. Java 11에서는 asMatchPredicate()를 통해 패턴이 주어진 문자열과 일치하는지 테스트하기 위해 '술어' 반환함.
    
- ***Garbage Collector***
    
    Java 8의 Default GC는 Paralle GC이다. 
    Java 11의 Default GC는 G1 GC이다.
    

- **Lambda [Java8]**
    
    Java 8 이전 익명 클래스의 사용을 람다를 이용하여 더욱 간결하고 직관적으로 구현 가능
    
    ```java
    Runnable runnable = new Runnable(){
       @Override
       public void run(){
         System.out.println(*"Hello world !"*);
       }
     };
    ```
    
    ```java
    Runnable runnable = () -> System.out.println(*"Hello world two!"*);
    ```
    
- **Stream [Java8]**
    
    자바 8은 스트림 API를 통해 컬렉션을 처리하면서 발생하는 `모호함과 반복적인 코드 문제`와 `멀티코어 활용 어려움`이라는 두 가지 문제를 모두 해결
    
    ```java
    List<String> list = Arrays.asList(*"franz"*, *"ferdinand"*, *"fiel"*, *"vom"*, *"pferd"*);
    list.stream()
        .filter(name -> name.startsWith(*"f"*))
        .map(String::toUpperCase)
        .sorted()
        .forEach(System.out::println);
    ```
    

죄송합니다… 너어ㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓㅓ무 많아서 아래 참조링크 걸어뒀어요,, 참고해주시면 감사하겠습니다.

### 📍 Java 8의 사용 이유

**1. 외부 개발 툴과의 연동성**

웹서비스를 구동할 때, 자바 애플리케이션 외에 툴들이 필요한 경우가 있는데요. 이런 툴과의 연동성 문제에서 가장 안정적이라 생각해요. Java 11 부터 요금 정책이 바뀌었기 때문에, Oracle JDK가 아닌 Open JDK를 사용해야 하면서 생기는 이슈들이 꽤 있었어요.

**2. Java 11에서의 변경사항이 크게 없음**

메서드, 기능들이 어느정도 추가됐지만, Java8에서와 크게 차이가 나지 않기 때문에, Java 11을 사용해야하는 큰 이유를 찾지 못햇어요.
또한, Java 8 → Java 11에서의 문제가 크게 없기 때문에. 이후 릴리즈가 지원을 하지 않을 때, 버전 업그레이드를 한다 해도 괜찮다 생각해요.

# 📌 Access Modifier (접근 제어자)

변수나 메소드의 사용 권한은 다음과 같은 접근 제어자를 사용하여 설정할수 있다.

<aside>
👉 접근 제한 범위에 순으로 나열하면, public > protected > default > private

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/39ee7bac-bc3c-4448-abba-cf8ba077770a/Untitled.png)

1. private
    
    같은 클래스에서만 접근이 가능
    
    제일 제한이 큰 접근제어자
    
2. default
    
    같은 패키지, 해당 클래스를 상속 받은 다른 패키지의 자손 클래스에서 접근이 가능
    
    접근제어자를 설정하지 않았을 때 값이 default로 설정
    
3. protected
    
    같은 패키지에서만 접근이 가능
    
4. public
    
    패키지, 클래스의 제약이 없다.
    

### 🤜 **접근 제어자의 대상 ⇒** 클래스, 메서드, 멤버변수

- 클래스 → public, default
- 메서드 → public, private, protected, default (ALL)
- 멤버변수 → public, private, protected, default (ALL)
- 지역변수 → default

### 🤜 접근 제어자를 사용하는 이유

`#보안` , `#정보은닉` 

- 클래스 외부로의 불필요한 데이터 노출을 방지
- 외부로부터 데이터가 임의로 변경되지 않도록 막을 수 있다

# 📌 Wrapper class

<aside>
💡 8개의 기본 타입에 해당하는 데이터를 객체로 포장해 주는 클래스

</aside>

- 프로그램에 따라 기본 타입의 데이터를 객체로 취급/표현해야 하는 경우가 있습니다. 그럴 경우, 기본 자료타입(primitive type)을 객체로 다루기 위해서 사용하는 클래스를 래퍼 클래스 라고 합니다.
    
    (예를 들어, 메소드의 인수로 객체 타입만이 요구되면, 기본 타입의 데이터를 그대로 사용할 수는 없습니다. 이때에는 기본 타입의 데이터를 먼저 객체로 변환한 후 작업을 수행해야 합니다.)
    
- 각각의 타입에 해당하는 데이터를 인수로 전달받아, 해당 값을 가지는 객체로 만들어 줍니다.
- java.lang 패키지에 포함되어 제공

![[Java의 기본 타입에 대응하여 제공하고 있는 wrapper class]
❗ 래퍼 클래스 중에서 Integer 클래스와 Character 클래스만이 자신의 기본 타입과 이름이 다름을 주의](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eeb807a1-f9fb-4162-832e-2b3fc6c9aa0e/Untitled.png)

[Java의 기본 타입에 대응하여 제공하고 있는 wrapper class]
❗ 래퍼 클래스 중에서 Integer 클래스와 Character 클래스만이 자신의 기본 타입과 이름이 다름을 주의

### 🤜 Wrapper Class 구조도

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/861e7da7-68fd-4231-b483-47b67da9df86/Untitled.png)

### 🤜 박싱(Boxing)과 언박싱(Unboxing)

<aside>
💡 박싱 : 기본 타입의 값을 포장 객체로 만드는 과정
언박싱 : 반대로 포장 객체에서 기본 타입의 값을 얻어내는 과정

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8ad18436-0816-4191-82ec-826cfed09144/Untitled.png)

```java
public class Wrapper_Ex {
    public static void main(String[] args)  {
        Integer num = new Integer(17); // 박싱
        int n = num.intValue(); //언박싱
        System.out.println(n);
    }
}
```

### 🤜 ****자동 박싱(AutoBoxing)과 자동 언박싱(AutoUnBoxing)****

기본타입 값을 직접 박싱, 언박싱하지 않아도 자동적으로 박싱과 언박싱이 일어나는 경우가 있습니다. 

- JDK 1.5부터는 박싱과 언박싱이 필요한 상황에서 자바 컴파일러가 이를 자동으로 처리
- 자동 박싱의 포장 클래스 타입에 기본값이 대입될 경우에 발생
    
    (예를 들어 int타입의 값을 Integer클래스 변수에 대입하면 자동 박싱이 일어나 힙 영역에 Integer객체가 생성)
    

```java
public class Wrapper_Ex {
    public static void main(String[] args)  {
        Integer num = 17; // 자동 박싱
        int n = num;      //자동 언박싱
        System.out.println(n);

				Character ch = 'X'; // Character ch = new Character('X'); : 오토박싱
				char c = ch;        // char c = ch.charValue();           : 오토언박싱
				System.out.println(c);
    }
}
```

# CS 질문

### **java 접근제어자에 대해서 설명해주세요.**

자바 접근제어자는 클래스, 인터페이스, 멤버변수, 함수 등의 접근을 제어하는 지시어를 말합니다.접근제어자를 사용함으로써, 외부 객체의 무분별한 접근으로부터 내부 데이터를 보호할 수 있습니다(데이터 무결성).

### synchronized란?

Java에서 지원하는 synchronized 키워드는 여러 쓰레드가 하나의 자원을 이용하고자 할 때, 한 스레드가 해당 자원을 사용중인 경우, 데이터에 접근할 수 없도록 막는 키워드입니다. synchronized 키워드를 이용하면 병렬 상황에서 자원의 접근을 안전하게 하지만, 자원을 이용하지 않는 쓰레드는 락에 의한 병목현상이 발생하게 됩니다.메소드 synchronized: 한 시점에 하나의 쓰레드만이 해당 메소드를 실행할 수 있다.변수 synchronized: 한시점에 하나의 쓰레드만이 해당 변수를 참조할 수 있다.

### Java8

Java8에서는 함수형 프로그래밍을 위해  함수형 인터페이스와 람다와 함께 stream API가 추가되었고, Null-safe한 작업을 위한 Optional API, Date와 Time을 함께 처리하기 위한 LocalDateTime API 등이 추가되었습니다.

### ***Java 8에서 새로 추가된 기능을 설명하라.***

- Heap Permanent Generation 제거
- 인터페이스에 디폴트 메소드와 정적 메소드 추가
- 함수형 인터페이스, 람다 표현식, 메소드 참조 기능 추가
- 스트림 API 도입
- 새로운 날짜 관련 라이브러리 추가
- Optional 지원
- 병렬 처리 지원

### ***Java 11에서 새로 추가된 기능을 설명하라.***

- Spring에 새로운 메소드 추가
- Files 클래스에 새로운 메소드 추가
- 컬렉션 인터페이스에 새로운 메소드 추가
- Predicate 인터페이스에 새로운 메소드 추가
- 람다에서 로컬 변수 Var 사용
- 자바 파일 실행 방식 단순화

### 인터페이스와 추상 클래스(abstract)의 차이점

> ref
> 

---

[CS-Study/Promotion&Casting.md at main · Songwonseok/CS-Study](https://github.com/Songwonseok/CS-Study/blob/main/Language/Java/Promotion%26Casting.md)

[CS-Study/Intrinsic Lock.md at main · Songwonseok/CS-Study](https://github.com/Songwonseok/CS-Study/blob/main/Language/Java/Intrinsic%20Lock.md)

> Java 8 vs Java 11 차이점, 특징
> 

---

[[Java] Java7과 Java8의 특징](https://livenow14.tistory.com/73)

[[Java] Java 8 vs Java 11](https://steady-coding.tistory.com/598)