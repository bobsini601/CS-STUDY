# Array, Linked List

# ๐ย Array

### ๐ย ํน์ง

- ๋ฐ์ดํฐ๋ฅผ ๋ฌผ๋ฆฌ์  ์ฃผ์์ ์์ฐจ์ ์ผ๋ก ์ ์ฅํ๋ ์๋ฃ๊ตฌ์กฐ
- ๋ผ๋ฆฌ์  ์ ์ฅ ์์์ ๋ฌผ๋ฆฌ์  ์ ์ฅ ์์๊ฐ ์ผ์นํจ
- ์๊ฐ ๋ณต์ก๋
    - ๊ฒ์: O(1)
    - ์ฝ์, ์ญ์  : O(N)

### ๐ย ์ฅ์ 

- ์ธ๋ฑ์ค๋ฅผ ์ด์ฉํ์ฌ ๋ฐ์ดํฐ์ random access ๊ฐ๋ฅ
    
    โ ๋ฐ์ดํฐ ์ ๊ทผ(ํ์, ์กฐํ)์ด ๋ง์ ๊ฒฝ์ฐ ์ฌ์ฉ
    

### ๐ ๋จ์ 

- ์ฝ์, ์ญ์ ๊ฐ ๋ฒ๊ฑฐ๋ก์
    - ๋ฐ์ดํฐ๋ฅผ ๋ฐฐ์ด์ ์ค๊ฐ์ ์ฝ์ํ๊ฑฐ๋ ์ญ์ ํ  ๊ฒฝ์ฐ, ๋ฐ์ดํฐ๋ฅผ ํ ์นธ์ฉ ๋ฐ๊ฑฐ๋ ์ญ์ ํด์ผํ๋ฏ๋ก ์ฐ๊ฒฐ๋ฆฌ์คํธ์ ๋นํด ๋๋ฆผ
- ์ด๊ธฐ์ ๋ฐฐ์ด์ ํฌ๊ธฐ๋ฅผ ์ง์ ํด์ผํ๊ณ , ๋ณ๊ฒฝํ  ์ ์์

### โจย ์์ ์ฝ๋

```java
// Java
// ๋ฐฐ์ด ์์ฑ
int[] arr = new int[3];

a[1] = 15;
a[2] = 20;

for(int i=0; i<a.length; i++)
    System.out.println("a["+i+"]="+a[i]);

/*
a[0] = 0 
a[1] = 15
a[2] = 20
*/
```

# ๐ย Linked List

![week1_0.png](../assets/week1_0.png)

### ๐ย ํน์ง

- ์ฐ์์ ์ธ ๋ฉ๋ชจ๋ฆฌ ์์น์ ์ ์ฅ๋์ง ์๋ ์ ํ ๋ฐ์ดํฐ ๊ตฌ์กฐ. ํฌ์ธํฐ๋ฅผ ์ด์ฉํ์ฌ ์ฐ๊ฒฐ๋จ
- ๋ธ๋: ๋ฐ์ดํฐ + ๋ค์ ๋ฐ์ดํฐ๋ฅผ ๊ฐ๋ฆฌํค๋ ํฌ์ธํฐ
- ์๊ฐ ๋ณต์ก๋
    - ๊ฒ์, ์ฝ์, ์ญ์  : O(N)

### ๐ย ์ฅ์ 

- ๋ฐ์ดํฐ๋ฅผ ์ค๊ฐ์ ์ฝ์ํ๊ฑฐ๋ ์ญ์ ํ๋ ๊ฒฝ์ฐ, ๋ธ๋๋ฅผ ๊ฐ๋ฆฌํค๋ ์ฃผ์์ ์์น๋ง ๋ฐ๊ฟ์ฃผ๋ฉด ๋๋ฏ๋ก ๋ฐฐ์ด์ ๋นํด ๋น ๋ฆ
    
    โ ๋ฐ์ดํฐ๋ฅผ ์์ (์ฝ์, ์ญ์ )์ด ๋ง์ ๊ฒฝ์ฐ ์ฌ์ฉ
    
- ๋์  ํฌ๊ธฐ

### ๐ ๋จ์ 

- ๋ฐ์ดํฐ ์ ๊ทผ์ ์ฒ์ ์์น๋ถํฐ ์ ๊ทผํด์ผ ํ๋ฏ๋ก ๋ฐฐ์ด์ ๋นํด ๋๋ฆผ.
    - ์ฆ, random access ๋ถ๊ฐ
- ํฌ์ธํฐ๊น์ง ์ ์ฅํด์ผํ๊ธฐ ๋๋ฌธ์ ๋ฉ๋ชจ๋ฆฌ ๋ญ๋น ์กด์ฌ

### โจย ์์ ์ฝ๋

**๐กย Node ๊ตฌํ**

```java
class Node<E>{
	E data;       // ๋ฐ์ดํฐ
	Node<E> next; // ๋ค์ ๋ธ๋๋ฅผ ๊ฐ๋ฆฌํค๋ ํฌ์ธํฐ
}
```

์ ๋ค๋ฆญ์ผ๋ก ๊ตฌํ๋ ๊ฒ์ด๋ฏ๋ก E๋ ์ฐธ์กฐํ! (์์์ ํด๋์ค ํ์ฉ)

๐ก**Linked list ํด๋์ค**

```java
import java.util.Comparator;

public class LinkedList<E>{
  //๋ธ๋
  class Node<E>{
    E data;
    Node<E> next;

    //์์ฑ์
    Node(E data, Node<E> next){
      this.data = data;
      this.next = next;
    }
  }

  private Node<E> head;   //๋จธ๋ฆฌ ๋ธ๋
  private Node<E> crnt;   //์ ํ ๋ธ๋
}
```

๐ก**LinkedList** **์์ฑ์**

```java
public LinkedList(){
  head = crnt = null;
}
```

๋ธ๋๊ฐ ํ๋๋ ์๋ ๋น์ด ์๋ ์ฐ๊ฒฐ๋ฆฌ์คํธ ์์ฑ

๐กย **Linked list ํ๋จ**

- Linked list๊ฐ ๋น์ด ์์ ๋
    - head == null
- ๋ธ๋๊ฐ ํ ๊ฐ์ผ ๋
    - head.next == null
- ๊ผฌ๋ฆฌ ๋ธ๋์ธ์ง ํ๋จํ  ๋
    - p.next == null

**๐กย ๋ฉ์๋**

1. **๊ฒ์**
    - ํ์ ๋ฐฉ๋ฒ
        
        Linked list ์ฒ์๋ถํฐ ์์๋๋ก ๋ธ๋๋ฅผ ์ค์บํ๋ค.
        
    - ์ข๋ฃ ์์ 
        - data๋ฅผ ์ฐพ์
        - ์ฐพ์ง ๋ชปํ๊ณ  ๊ผฌ๋ฆฌ ๋ธ๋๊น์ง ๋๋ฌ์
    
    ```java
    public E search(E obj, Comparator<? super E> c){
      Node<E> ptr = head;
    
      while(ptr!=null){
        if(c.compare(obj, ptr.data)==0){ // ๊ฒ์ ์ฑ๊ณต
          crnt = ptr;
          return ptr.data;
        }
        ptr = ptr.next;                  // ๋ค์ ๋ธ๋ ์ ํ
      }
      return null;                       // ๊ฒ์ ์คํจ
    }
    ```
    
2. **์ฝ์**
    - ๋จธ๋ฆฌ์ ๋ธ๋๋ฅผ ์ฝ์ํ  ๋
        - ๋ฆฌ์คํธ๊ฐ ๋น์ด ์์ ๊ฒฝ์ฐ, ๋ฆฌ์คํธ๊ฐ ๋น์ด ์์ง ์์ ๊ฒฝ์ฐ ๋ชจ๋ ํด๋น
        
        ![Untitled](../assets/week1_1.png)
        
        - ๋ธ๋ ์์ฑ
            - ์ฝ์๋  ๋ธ๋์ ํฌ์ธํฐ: ๋งจ ์ฒ์ ๋ธ๋๋ก ์ค์ 
        - head๋ฅผ ์ฝ์๋  ๋ธ๋๋ฅผ ๊ฐ๋ฆฌํค๋๋ก ์ค์ 
    
    - ์ค๊ฐ์ ๋ธ๋๋ฅผ ์ฝ์ํ  ๋(๊ผฌ๋ฆฌ ๋ธ๋ ์ฝ์ ํฌํจ)
        
        ![Untitled](../assets/week1_2.png)
        
        - ๋ธ๋ ์์ฑ
        - ์ฝ์๋  ์์น ์ด์ ๊น์ง ํ์
        - ์ฝ์๋  ์์น ์ด์  ๋ธ๋์ ํฌ์ธํฐ๋ฅผ ์ฝ์๋  ๋ธ๋๋ก ์ค์ 
        - ์ฝ์๋  ๋ธ๋์ ํฌ์ธํฐ: ์ฝ์๋  ์์น ์ด์  ๋ธ๋์ ํฌ์ธํฐ๊ฐ ์ฐธ์กฐํ๋ ๋ธ๋๋ก ์ค์ 
    
    ```java
    //๋จธ๋ฆฌ์ ๋ธ๋ ์ฝ์
    public void addFirst(E obj){
      Node<E> ptr = head;
      head = crnt = new Node<E>(obj, ptr);
    }
    
    //๊ผฌ๋ฆฌ์ ๋ธ๋ ์ฝ์
    public void addLast(E obj){
      if(head == null)
        addFirst(obj);
      else{
        Node<E> ptr = head;
        while(ptr.next!=null)   // while๋ฌธ ์ข๋ฃ์ ptr์ ๊ผฌ๋ฆฌ ๋ธ๋๋ฅผ ๊ฐ๋ฆฌํด
          ptr = ptr.next;
        ptr.next = crnt = new Node<E>(obj, null);
      }
    }
    ```
    
3. **์ญ์ **
    
    
    - ๋จธ๋ฆฌ ๋ธ๋ ์ญ์ 
        
        ![Untitled](../assets/week1_3.png)
        
        - head๋ฅผ ์ญ์ ํ  ๋ธ๋์ ๋ค์ ๋ธ๋๋ฅผ ๊ฐ๋ฆฌํค๊ฒ ํจ
        - ์ญ์ ํ  ๋ธ๋ ํด์ 
        
    - ์ค๊ฐ ๋ธ๋ ์ญ์ (๊ผฌ๋ฆฌ ๋ธ๋ ์ญ์  ํฌํจ)
        
        ![Untitled](../assets/week1_4.png)
        
        - ์ญ์ ํ  ๋ธ๋ ์ด์  ๋ธ๋๊น์ง ํ์
        - ์ด์  ๋ธ๋์ ํฌ์ธํฐ๋ฅผ ์ญ์ ํ  ๋ธ๋๊ฐ ์ฐธ์กฐํ๋ ๋ธ๋๋ก ๋ณ๊ฒฝ
        - ์ญ์ ํ  ๋ธ๋ ํด์ 
        
    
    ```java
    //๋จธ๋ฆฌ ๋ธ๋ ์ญ์ 
    public void removeFirst(){
      if(head!=null)
        head = crnt = head.next;
    }
    
    //๊ผฌ๋ฆฌ ๋ธ๋ ์ญ์ 
    public void removeLast(){
      if(head!=null){
        if(head.next==null)
          removeFirst();
      }
      else{
          Node<E> ptr = head;   // ์ค์บ ์ค์ธ ๋ธ๋
          Node<E> pre = head;   // ์ค์บ ์ค์ธ ๋ธ๋์ ์์ชฝ ๋ธ๋
    
          while(ptr.next!=null){
            pre = ptr;
            ptr = ptr.next;
          }
          pre.next = null;    // pre๋ ์ญ์  ์์ ํ์ ๊ผฌ๋ฆฌ ๋ธ๋
          crnt = pre;
      }
    }
    ```
    
    ```java
    //๋ธ๋ p ์ญ์ 
    public void remove(Node p){
      if(head!=null){
        if(p==head)
          removeFirst();
      }
      else{
        Node<E> ptr = head;
    
        while(ptr.next!=p){
          ptr = ptr.next;
          if(ptr==null) return;   // p๊ฐ ๋ฆฌ์คํธ์ ์์
        }
        ptr.next = p.next;
        crnt = ptr;
      }
    }
    
    //์ ํ ๋ธ๋๋ฅผ ์ญ์ 
    public void removeCurrentNode(){
      remove(crnt);
    }
    
    //๋ชจ๋  ๋ธ๋ ์ญ์ 
    public void clear(){
      while(head!=null)   //๋ธ๋์ ์๋ฌด๊ฒ๋ ์์ ๋ ๊น์ง ๋จธ๋ฆฌ๋ธ๋๋ฅผ ์ญ์ 
        removeFirst();
      crnt = null;
    }
    ```
    

## ๐ Doubly Linked List

![Untitled](../assets/week1_5.png)

### ๐ย ํน์ง

- Linked List์ ๋จ์ ์ธ ๋ฌด์กฐ๊ฑด ์ฒ์๋ถํฐ ํ์ํด์ผ ํ๋ ๊ฒ์ ๋ณด์
- ์์ชฝ์ ํฌ์ธํฐ๊ฐ ์์

### ๐ย ์ฅ์ 

- ๋ธ๋๋ฅผ ํ์ํ  ๋ ์๋ฐฉํฅ์ด ๊ฐ๋ฅ

### ๐ ๋จ์ 

- ๋ฉ๋ชจ๋ฆฌ๋ฅผ ์ฐจ์งํ๋ ๊ฒ์ด ๋ ๋์ด๋จ
- ์ฝ๋ ๊ตฌํ์ด ๋ณต์กํด์ง

## ๐ ๊ธฐํ Linked List

- ์ํ ๋ฆฌ์คํธ
- ์ํ ์ด์ค ์ฐ๊ฒฐ ๋ฆฌ์คํธ


### ๊ทธ๋ฆผ ๋ฐ ์ฝ๋ ์ถ์ฒ:

[https://github.com/HyeminNoh/Tech-Stack/blob/master/docs/DataStructure/LinkedList.md](https://github.com/HyeminNoh/Tech-Stack/blob/master/docs/DataStructure/LinkedList.md)

### ์ฐธ๊ณ  ์๋ฃ
    - [https://freestrokes.tistory.com/84](https://freestrokes.tistory.com/84)
    - [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Data Structure/Linked List.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Linked%20List.md)
    - [https://github.com/kho903/CS_STUDY/tree/master/Data Structure/02. ์ฐ๊ฒฐ ๋ฆฌ์คํธ](https://github.com/kho903/CS_STUDY/tree/master/Data%20Structure/02.%20%EC%97%B0%EA%B2%B0%20%EB%A6%AC%EC%8A%A4%ED%8A%B8)
    - [https://github.com/jeonyeohun/Getting-Ready-For-Interview/blob/main/DataStructure/01_Array.md](https://github.com/jeonyeohun/Getting-Ready-For-Interview/blob/main/DataStructure/01_Array.md)
    - [https://cocoon1787.tistory.com/705?category=831125](https://cocoon1787.tistory.com/705?category=831125)