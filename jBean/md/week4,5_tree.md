# Tree

# Tree

<aside>
📌  그래프의 한 종류로 사이클이 없고 데이터의 계층관계를 나타내는 자료구조

</aside>

## 🍃 특징

- DAG(Directed Acyclic Graphs, 방향성이 있는 비순환 그래프)의 한 종류로, **사이클이 없음**
- 계층 모델임
- 모든 정점이 간선으로 연결되어 있음
- 노드가 N개인 트리는 항상 N-1개의 간선(가지, edge)를 가짐
- 한 개의 루트 노드만 존재하고, 모든 자식 노드는 한 개의 부모 노드만을 가짐
- 모든 노드는 자료형으로 표현이 가능함
- 부모 - 자식 관계이므로 흐름은 top-bottom이나 bottom-up으로 이루어짐
- 루트에서 한 노드로 가는 경로는 유일함

예시) 컴퓨터의 directory

## 🌼 트리 관련 용어

- Node(노드)
    
    트리를 구성하는 각각의 요소
    
- Edge(간선, 가지)
    
    트리를 구성하기 위해 노드와 노드를 연결하는 선
    
- Root Node(루트 노드)
    
    트리 구조에서 최상위에 있는 노드
    
- Leaf Node(=Terminal Node, 단말 노드)
    
    하위에 다른 노드가 연결되어 있지 않은 노드
    
- Internal Node(내부 노드, 비단말 노드)
    
    단말 노드를 제외한 모든 노드로 루트 노드를 포함
    
- 깊이(Depth)
    
    루트 노드에서 특정 노드까지의 길이. 루트는 0!
    
- 높이(Height)
    
    루트 노드에서 가장 깊은 노드까지의 길이
    
- 차수(Degree)
    
    각 노드의 간선 개수. 노드가 갖는 자식의 수
    
- 트리의 차수(Degree of tree)
    
    모든 노드의 차수가 n 이하인 트리를 n진 트리라고 함. 
    
- 크기(Size)
    
    트리에 포함된 모든 노드의 개수
    
- 널 트리(Null tree)
    
    노드, 간선이 없는 트리
    
- 순서 트리, 무순서 트리
    
    형제 노드의 순서를 따지면 순서 트리(ordered tree), 따지지 않으면 무순서 트리(unordered tree)
    

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3ab3a4df-f9ac-4816-ae11-b5418289d1dc/Untitled.png)

### 예시

- 5번 노드의 깊이: 2
- 트리의 높이: 3
- 트리의 차수: 이진 트리

## 🔍 트리 순회 방법

### Preorder, 전위 순회 방법

각 루트를 순차적으로 먼저 방문하는 방식

- **Root → 왼쪽 자식 → 오른쪽 자식**

> 1 → 2 → 4 → 8 → 9 → 5 → 10 → 11 → 3 → 6 → 12 → 7
> 

### Inorder, 중위 순회 방법

왼쪽 하위 트리를 방문 후 루트를 방문하는 방식

- **왼쪽 자식 → Root → 오른쪽 자식**

> 8 → 4 → 9 → 2 → 10 → 5 → 11 → 1 → 12 → 6 → 3 → 7
> 

### Postorder, 후위 순회 방법

왼쪽 하위 트리부터 하위를 모두 방문 후 루트를 방문하는 방식

- **왼쪽 자식 → 오른쪽 자식 → Root**

> 8 → 9 → 4 → 10 → 11 → 5 → 2 → 12 → 6 → 7 → 3 → 1
> 

### 참고) Level order, 레벨 순회 방법

루트부터 계층별로 방문하는 방식

> 1 → 2 → 3 → 4 → … → 10 → 11 → 12
> 

## 💻 트리 Code

```java
public class Tree<T> {
    private Node<T> root;

    public Tree(T rootData) {
        root = new Node<T>();
        root.data = rootData;
        root.children = new ArrayList<Node<T>>();
    }

    public static class Node<T> {
        private T data;
        private Node<T> parent;
        private List<Node<T>> children;
    }
}
```

## 트리의 종류

### 이진 트리(Binary Tree)

<aside>
📌 모든 노드가 2개의 서브 트리를 가지고 있는 트리

</aside>

- 노드가 왼쪽 자식과 오른쪽 자식을 가지며, 각 노드의 자식은 2명 이하만 유지해야 한다.
- 루트 노드를 중심으로 두 개의 서브 트리(큰 트리에 속하는 작은 트리)로 나뉘어 진다. 또한 나뉘어진 두 서브 트리도 모두 이진 트리이다.
    - 이때, 널 트리도 이진 트리로 포함해야 재귀적으로 조건을 확인했을 때 조건이 맞는다!
- 배열로 구성된 이진 트리의 노드의 개수가 n, root가 1에서 시작할 경우 index
    - parent(i) = i/2
    - left child = i*2
    - right child = i*2 + 1

### 포화 이진 트리(Full Binary Tree)

<aside>
📌 트리의 각 레벨에 노드가 꽉 차있는 이진 트리

</aside>

### 완전 이진 트리(Complete Binary Tree)

<aside>
📌 최대 두 개의 자녀노드를 가지는 이진 트리로, 마지막 레벨을 제외한 모든 레벨에 노드가 채워져있고 마지막 레벨은 왼쪽부터 빈 노드 없이 채워져 있는 트리

</aside>

### 이진 탐색 트리(Binary Search Tree, BST)

<aside>
📌 트리와 트리 내 모든 서브 트리의 루트 노드를 기준으로 값이 더 작은 노드는 왼쪽, 값이 더 큰 노드는 오른쪽에 위치하는 이진 트리

</aside>

- **값: 왼쪽 자식 노드 < 부모 노드 < 오른쪽 자식 노드**
- **같은 데이터 값을 가지는 노드는 없음(데이터 중복 X)**
    - 검색 목적 자료구조인데, 굳이 중복이 많은 경우에 트리를 사용하여 검색 속도를 느리게 할 필요가 없음. (트리에 삽입하는 것보다, 노드에 count 값을 가지게 하여 처리하는 것이 훨씬 효율적)
- 탐색 시간 복잡도
    - 균등 트리: **O(logN)** == O(log높이)
    - 편향 트리(worst): **O(N)**
- 삽입, 삭제시 시간 복잡도: **O(logN)**
    - 모두 탐색을 사용해야하고, 탐색은 각 노드를 대소비교하며 진행하기 때문에 트리의 높이 만큼의 시간복잡도가 걸림
- Inorder(중위 순회) 방식으로 탐색
- 단점: 루트노드를 기준으로 새로운 노드를 삽입하기 때문에 만약 루트노드보다 큰 값을 가진 노드가 계속해서 들어오면 불균형한 트리가 생성됨
- 편향된 트리의 경우 배열보다 많은 메모리를 사용하며 데이터를 저장했지만 탐색에 필요한 시간 복잡도가 같게 되는 비효율적인 상황이 발생
    
    →  해결: `Rebalancing` = 균형을 잡기 위한 트리 구조의 재조정
    이 기법을 구현한 트리 중 하나:  AVL Tree,  Red-Black Tree
    

### **생성**

1. 첫 번째 요소를 root에 삽입
2. 다음 요소를 읽고 root와 비교하여 작으면 왼쪽, 크면 오른쪽 하위 트리의 루트로 삽입
    
    ![스크린샷 2022-08-21 오전 4.35.08.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1bc0e4ed-80d8-485c-88df-1c9e52de13dd/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.35.08.png)
    

### 검색(=**탐색)**

- Inorder 방식
    1. 주어진 키 값이 루트 노드의 키 값과 같으면 탐색에 성공
    2. 주어진 키 값이 루트 노드의 키 값보다 작으면 왼쪽 서브트리를 탐색
    3. 주어진 키 값이 루트 노드의 키 값보다 크면 오른쪽 서브트리를 탐색
        
        ![스크린샷 2022-08-21 오전 4.34.49.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/711d16c7-3796-4d3d-96d3-b17a084a7eeb/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.34.49.png)
        

### **삽입**

- 
    
    ![스크린샷 2022-08-21 오전 4.39.01.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d772f52f-d8cf-4e5d-9001-aa99f5d7b758/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.39.01.png)
    
    1. root에서 시작
    2. 삽입 값을 root와 비교하여 작다면 왼쪽, 크다면 오른쪽으로 재귀
    3. 리프 노드에 도달한 후 노드보다 작으면 왼쪽, 크면 오른쪽에 삽입
- 탐색이 우선!
    - 즉, 탐색에 실패한 위치가 삽입될 위치
1. root에서 시작
2. 삽입 값을 root와 비교하여 작다면 왼쪽, 크다면 오른쪽으로 재귀
3. 리프 노드에 도달한 후 노드보다 작으면 왼쪽, 크면 오른쪽에 삽입
    
    ![스크린샷 2022-08-21 오전 4.39.01.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d772f52f-d8cf-4e5d-9001-aa99f5d7b758/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.39.01.png)
    
4. 삽입 값을 root와 비교하여 작다면 왼쪽, 크다면 오른쪽으로 재귀
5. 리프 노드에 도달한 후 노드보다 작으면 왼쪽, 크면 오른쪽에 삽입

### **삭제**

1. 자식이 없는 leaf 노드일 때
    
    → 그냥 삭제하기
    
    ![스크린샷 2022-08-21 오전 4.39.29.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3579c223-c2b3-4347-ab89-1dbb85724da9/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.39.29.png)
    
2. 자식이 1개인 노드일 때(= 하나의 subtree만 가진 경우)
    
    → 해당 노드 삭제 후 지워진 노드에 자식을 올리기자식이 2개인 노드일 때(= 두 개의 subtree를 가진 경우)
    
    ![스크린샷 2022-08-21 오전 4.39.44.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe6fc962-62b0-49be-acb7-edbc00bee7f4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.39.44.png)
    
    → 오른쪽 자식 노드에서 가장 작은 값 or 왼쪽 자식 노드에서 가장 큰 값을 찾아 삭제할 노드와 바꾼 후 삭제
    
3. 자식이 2개인 노드일 때(= 두 개의 subtree를 가진 경우)
    
    → 오른쪽 자식 노드에서 가장 작은 값 or 왼쪽 자식 노드에서 가장 큰 값을 찾아 삭제할 노드와 바꾼 후 삭제
    
- 즉, 삭제할 노드와 가장 근사한 값을 가진 노드를 가져옴
    
    ![스크린샷 2022-08-21 오전 4.40.38.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/961ad3e8-b6d0-4cc6-8f4c-4580f9db63d7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.40.38.png)
    

### Binary Heap

자료구조의 일종으로 Tree 의 형식을 하고 있으며, Tree 중에서도 배열에 기반한 Complete Binary Tree임

- 최대힙, 최소힙

### AVL 트리

<aside>
📌 트리의 불균형을 막기 위해 새로운 노드가 트리에 추가될 때마다 좌측 서브트리와 우측 서브트리의 높이의 차를 사용해 트리의 균형을 맞춘 트리

</aside>

1. 이진 탐색 트리의 속성을 가짐
2. 왼쪽, 오른쪽 subtree 높이 차이가 최대 1
3. 높이 차이가 1보다 커지면 회전(Rotation)을 통해 균형을 맞춰 높이 차이를 줄임
4. 삽입, 검색, 삭제 시간 복잡도 : O(log N) == O(높이)

- 균형잡힌 이진탐색트리. subtree의 높이를 제어해 균형된 트리를 만들어 높이를 줄이는 것
- 만약 불균형이 발견되면 세 루트노드 중 중간 값을 가진 노드를 루트 노드로 만들고 이를 기준으로 좌우에 서브트리를 위치시킴

**Balance Factor(BF)**

> BF(K) = K의 왼쪽 서브트리의 높이 - K의 오른쪽 서브트리의 높이
> 

![스크린샷 2022-08-21 오전 9.59.08.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d489b74f-21bf-4233-83a8-18dcc0fb02d5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_9.59.08.png)

- AVL 트리는 **BF가 -1, 0, 1 중 하나**
- 이를 벗어나면 균형이 깨졌음을 의미. → 회전

T1, T2..: subtree, 회전 기준: z노드

**우회전**

![스크린샷 2022-08-21 오전 10.04.22.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/640f4e94-99d8-4798-a13d-67d1f3daff83/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_10.04.22.png)

1. y노드의 오른쪽 자식 노드를 z 노드로 변경
2. z노드 왼쪽 자식 노드를 y노드의 오른쪽 subtree(T2)로 변경

**좌회전**

![스크린샷 2022-08-21 오전 10.06.33.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a01c447-7440-4946-a5f4-190be8ec6fb2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_10.06.33.png)

1. y노드의 왼쪽 자식 노드를 z노드로 변경
2. z노드 오른쪽 자식 노드를 y노드의 왼쪽 서브트리(T2)로 변경

> LL(Left Left)
> 

<aside>
📌 y는 z의 **왼쪽** 자식 노드이고, x는 y의 **왼쪽** 자식 노드인 경우 ⇒ **우회전**

</aside>

![스크린샷 2022-08-28 오전 1.52.55.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2355187e-c3e3-4766-b562-446411b4e106/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.52.55.png)

- y노드의 오른쪽 자식 노드를 z노드로 변경
- z노드 왼쪽 자식 노드를 y노드 오른쪽 subtree(T2)로 변경
- y가 새로운 루트 노드

> RR(Right Right)
> 

<aside>
📌 y는 z의 **오른쪽** 자식 노드이고, x는 y의 **오른쪽** 자식 노드인 경우 ⇒ **좌회전**

</aside>

![스크린샷 2022-08-28 오전 1.55.23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8cdfa5aa-2a66-4f1d-aaf2-dcb3d693bfc2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.55.23.png)

- y노드의 왼쪽 자식 노드를 z노드로 변경
- z노드 오른쪽 자식 노드를 y노드 왼쪽 subtree로 변경
- y는 새로운 루트 노드

> LR(Left Right)
> 

<aside>
📌 y는 z의 **왼쪽** 자식 노드이고, x는 y의 **오른쪽** 자식 노드인 경우 ⇒ **좌회전 후 우회전**

</aside>

![스크린샷 2022-08-28 오전 1.57.34.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/714449e2-14b0-41ad-934f-fd3050a0f828/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.57.34.png)

- 좌회전
    - x노드의 왼쪽 자식을 y노드로 변경
    - y노드 오른쪽 자식을 x노드 왼쪽 subtree로 변경
- 우회전
    - x노드의 오른쪽 자식을 z노드로 변경
    - z노드 왼쪽 자식을 x노드 오른쪽 subtree로 변경

```
**❗️그림이 잘못나온것 같아요**

두번째 그림에서 y의 subtree는 T1, T2, x의 자식은 y노드, subtree T3입니다.
세번째 그림에서 y의 subtree는 T1, T2, z의 subtree는 T3, T4입니다.
```

![스크린샷 2022-08-28 오전 2.21.07.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/693cd96b-a724-4c5f-b405-e82bd57d7f23/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.21.07.png)

> RL(Right Left)
> 

<aside>
📌 y는 z의 **오른쪽** 자식 노드이고, x는 y의 **왼쪽** 자식 노드인 경우 ⇒ **우회전 후 좌회전**

</aside>

![스크린샷 2022-08-28 오전 2.04.27.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72641c7a-7251-4720-aace-3e53614035d3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.04.27.png)

- 우회전
    - x노드의 오른쪽 자식을 y노드로 변경
    - y노드의 왼쪽 자식을 x노드 오른쪽 subtree로 변경
- 좌회전
    - x노드의 왼쪽 자식을 z노드로 변경
    - z노드의 오른쪽 자식을 x의 왼쪽 subtree로 변경

- AVL 트리 삽입, 삭제 과정 확인해보는 사이트

[AVL Tree](https://www.cs.usfca.edu/~galles/visualization/AVLtree.html)

### Red-Black 트리(RBT)

<aside>
📌 BST로 자가 균형 이진 탐색 트리

</aside>

**특징**

- Binary Search Tree 이므로 BST 의 특징을 모두 갖는다.
- Root node 부터 leaf node 까지의 모든 경로 중 최소 경로와 최대 경로의 크기 비율은 2 보다 크지 않다. 이러한 상태를 `balanced` 상태라 함
- 모든 노드는 **Red** 또는 **Black**
- **루트노드와 리프노드**는 항상 **Black**
    - 노드의 child 가 없을 경우 child 를 가리키는 포인터는 NIL 값을 저장한다. 이러한 NIL 들을 leaf node라 함
- **Red 노드**의 **자녀노드는 모두 Black**(=No Double Red. 빨간색 노드가 연속으로 나올 수 없음)
- 루트노드에서 어떤 리프노드까지의 경로에 있는 Black 노드의 수는 모두 동일
    - 모든 리프 노드에서 Black Depth는 같음
- 탐색, 삽입, 삭제 시간복잡도: O(logN)
- Java Collection 에서 TreeMap 도 내부적으로 RBT 로 이루어져 있고, HashMap 에서의 Seperate Chaining에서도 사용됨.

**삽입**

<aside>
📌 삽입 시 새로운 노드는 항상 **Red**

</aside>

![스크린샷 2022-08-21 오전 10.18.18.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1f69a22f-2049-4379-8865-581b10ccd6ac/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_10.18.18.png)

<aside>
🔥 Double Red 발생! → 해결: Restructuring, Recoloring

</aside>

1. 삼촌 노드가 **Black or NIL** → Restructuring
2. 삼촌 노드가 **Red** → Recoloring

- 삽입할 노드: N, 부모 노드: P, 조상 노드: G, 삼촌 노드: U

![스크린샷 2022-08-21 오전 10.20.20.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3165aa69-5001-4b72-9f39-9fcd401a9647/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_10.20.20.png)

> **Restructuring**
> 

```
1. 새로운 노드(N), 부모 노드(P), 조상 노드(G)를 오름차순으로 정렬한다.
2. 셋 중 중간값을 부모로 만들고 나머지 둘을 자식으로 만든다.
3. 새로 부모가 된 노드를 **Black**으로 만들고 나머지 자식들을 **Red**로 만든다.
```

![스크린샷 2022-08-21 오전 10.23.14.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e98fdc3f-7f1e-4fcc-9c4c-d02674145c60/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_10.23.14.png)

1. 새로운 노드 N과 부모 P, 조상 G를 오름차순으로 정렬한다. 그러면 3이 중간값이 된다.
2. 중간값인 3을 부모 노드로 바꾸고 나머지 2와 5를 자식 노드로 바꾼다. 원래 5의 자식 노드였던 7은 딸려가게 된다.
3. 새롭게 부모가 된 3을 **Black**으로 바꿔주고 나머지 두 자식인 2, 5의 색을 **Red**로 바꿔주면 된다.

> **Recoloring**
> 

```
1. 새로운 노드(N)의 부모(P)와 삼촌(U)을 **Black**으로 바꾸고 조상(G)을 **Red**로 바꾼다.
   1-1. 조상(G)이 루트 노드라면 **Black**으로 바꾼다.
   1-2. 조상(G)을 빨간색으로 바꿨을 때 또다시 Double Red가 발생한다면 또다시 Restructuring 혹은 Recoloring을 진행해서 Double Red 문제가 발생하지 않을 때까지 반복한다.
```

![스크린샷 2022-08-21 오전 10.26.27.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d83c39eb-f7ae-48b9-ade2-7114f7a0754f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_10.26.27.png)

1. 부모(P)와 삼촌(U)을 **Black**으로 바꾸고, 조상(G)을 **Red**로 바꾼다.
2. 루트 노드를 **Black**으로 바꾸면 된다.

- 난이도 조금 올라간 케이스

❗️가장 마지막 Step에 오타로 Node 8 -> Node 10으로 바뀌었습니다.

![스크린샷 2022-08-28 오전 2.55.24.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/36b8f2b4-9751-4231-a3cc-728d630a7d5c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2.55.24.png)

- 스스로 파악해보고 확인해보기!🙌
    - `RED 노드가 연속적으로 나올 수 없다` 규칙을 위반했습니다.
    - 삽입된 노드의 부모의 형제 색깔이 RED인 경우에 해당됩니다.
        - Recoloring으로 규칙을 위반하지 않게 조정합니다.
        - 삽입된 노드의 부모와 부모 형제노드를 BLACK으로 부모의 부모노드를 RED로 Coloring합니다.
    - Recoloring이 끝난 이후에 보니 Double Red가 재발생했습니다.
        - 25 노드의 부모의 형제 색깔이 BLACK이기 때문에 Restructuring으로 진행합니다.
            - 삽입된 노드, 부모, 부모의 부모(Grand Parent) 오름차순으로 정렬합니다.
            - 중앙 값을 부모 노드로 만들고 나머지 노드를 자식으로 변환합니다.
            - 부모 노드가 된 노드를 BLACK 나머지 노드를 RED로 Coloring합니다.

**삭제**

- 삭제 방식은 일반적인 BST와 동일, 삭제 후 RBT 속성 위반 여부 확인
- **Black** 노드를 삭제할 때는 삭제 연산으로 RB 트리의 속성이 깨지지 않도록 해야함
    - child node가 **Red** → 해당 노드 삭제 후 child node **Black**으로 변경
    - 삭제 노드 및 child node가 **Black**
        - 문제 발생: leaf 노드까지의 black node 개수는 모두 일정하다는 속성 위반
- **Red** 노드를 삭제할 때는 그냥 삭제! → RBT 속성 위반 발생 안 하기 때문

> 문제 Case 살펴보기
> 

💡 x 노드는 삭제할 노드 m의 자식 노드. 즉, m과 x 모두 Black 일 경우 문제를 살펴보자!

<aside>
☝ Case 1. 부모 노드가 **Red**

</aside>

1. p와 s노드의 색상을 교환!
- x에 이르는 경로상에 Black 추가 ⇒ x에 이르는 경로에서 노드가 하나 모자란 문제 해결
- 루트에서 s 지나는 경로의 Black 노드 수 변화 없음

![스크린샷 2022-08-28 오전 3.29.43.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f83b415a-8e89-4f92-bd77-73cf9a3431f6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_3.29.43.png)

<aside>
🤞 Case 2. 부모 노드가 **Black**

</aside>

2-1

1. p를 중심으로 왼쪽으로 회전(p는 Black, Red 관계 없음)
2. p와 s 색상 교환
3. r의 색상을 Black으로 변경
- x에 이르는 경로상에 Black 추가 ⇒ x에 이르는 경로에서 노드가 하나 모자란 문제 해결
- subtree 1, 2, 3 ⇒ 루트에서 지나는 경로의 Black 노드 수 변화 없음

![스크린샷 2022-08-28 오전 3.36.07.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/efe52805-42fb-4aff-b76e-959ac1b6b559/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_3.36.07.png)

2-2

1. s를 중심으로 오른쪽으로 회전
2. l과 s 색상 교환
3. 2-1 케이스로 재귀

![스크린샷 2022-08-28 오전 4.11.41.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3a42e5d9-afe3-47fc-8727-3a4df4bc7bdc/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.11.41.png)

2-3

1. s를 Red로 변경
    - s를 지나가는 경로에서도 Black 노드가 하나 부족하게 되어 p를 지나가는 경로 전체에서 Black 노드가 하나 부족
    - x에서 발생된 문제와 같은 문제가 p에서도 발생
2. p를 문제 발생 노드로 하여 재귀적으로 처리

![스크린샷 2022-08-28 오전 4.13.05.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/867f5a19-0b73-44be-8063-2aaab2af496e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.13.05.png)

2-4

1. p를 중심으로 왼쪽으로 회전
2. p와 s의 색상 교환
    - x의 부모 노드 색상이 Red로 변경됨 → Case 1과 상황이 같아짐
3. Case 1처럼 해결

![스크린샷 2022-08-28 오전 4.16.33.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/90db6eaf-e712-466a-92e8-289cefc4ec9e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.16.33.png)

### AVL tree vs Red-Black tree

- AVL Tree가 Red Black Tree보다 빠른 Search 가능
    - AVL Tree가 더 엄격한 Balanced를 유지하기 때문
- Red Black Tree은 AVL Tree보다 빠른 삽입과 삭제 가능
    - AVL Tree보다 Balanced를 느슨하게 유지하고 있기 때문
- Red Black Tree는 AVL Tree보다 색깔을 저장하기 위해 더 많은 Space Complexity가 필요
- Red Black Trees는 대부분의 언어의 map, multimap, multiset에서 사용
- AVL tree는 조회에 속도가 중요한 Database에서 사용

### B-Tree

<aside>
📌 탐색 성능을 높이기 위한 **균형이진탐색트리**의 일종

</aside>

- 데이터베이스, 파일 시스템에서 널리 사용됨
- 이진 트리를 확장하여 더 많은 수의 자식을 가질 수 있게 일반화 시킴
- 자식 수에 대한 일반화를 진행하면서, 하나의 레벨에 더 저장되는 것 뿐만 아니라 트리의 균형을 자동으로 맞춰줌
- B Tree라고도 불림

```
대량의 데이터를 처리해야 할 때, 검색 구조의 경우 하나의 노드에 많은 데이터를 가질 수 있다는 점은 상당히 큰 장점이다.

대량의 데이터는 메모리보다 블럭 단위로 입출력하는 하드디스크 or SSD에 저장해야하기 때문!

ex) 한 블럭이 1024 바이트면, 2바이트를 읽으나 1024바이트를 읽으나 똑같은 입출력 비용 발생. 따라서 하나의 노드를 모두 1024바이트로 꽉 채워서 조절할 수 있으면 입출력에 있어서 효율적인 구성을 갖출 수 있다.

→ B-Tree는 이러한 장점을 토대로 많은 **데이터베이스 시스템의 인덱스 저장 방법으로 애용**하고 있음
```

**👀 규칙**

- 노드의 자료수가 N이면, 자식 수는 N+1이어야 함
- 각 노드의 자료는 정렬된 상태여야함
- 루트 노드는 적어도 2개 이상의 자식을 가져야함
- M차 트리일 때, 루트 노드를 제외한 모든 노드는 최소 ⌈M/2⌉개의 자식 노드를 가지고 있어야함(최대 M개)
- 외부 노드로 가는 경로의 길이는 모두 같음.
- 입력 자료는 중복 될 수 없음

![3차 B트리 예시](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bf8d6271-4a58-4127-a86a-f7cc9d1c87c7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.59.07.png)

3차 B트리 예시

**검색 (원하는 값: K)**

```
1. root node부터 탐색을 시작한다.
2. node의 key를 순회하여 K가 존재하면 탐색을 종료한다.
3. k가 존재하지 않는다면, 어떤 이웃한 두 key 사이에 K가 들어가는 경우 사이의 포인터를 통해 자식 node로 내려간다.
4. leaf node까지 2~3을 반복한다.
```

**삽입**

```
1. 빈 트리인 경우 root node를 만들어 K를 삽입한다. root node가 가득 찬 경우 node를 분할하여 leaf node를 생성한다.
2. K가 들어갈 leaf node를 검색 과정과 동일하게 탐색한다.
3. 해당 leaf node에 자리가 남아있다면 정렬을 유지하도록 알맞은 위치에 삽입하고, leaf node가 꽉 차 있다면 K를 삽입한 후 해당 node를 분할한다.
4. node가 분할되는 경우 node의 중앙값을 기준으로 분할한다. 중앙값은 부모 node로 합쳐지거나 새로운 node로 생성되고, 중앙값을 기준으로 왼쪽의 key는 왼쪽 자식, 오른쪽의 key는 오른쪽 자식으로 생성된다.
```

**삭제**

```
<경우의 수>
**1. 삭제할 key가 leaf node에 있는 경우** 
	1-1) 현재 node의 key 수가 최소보다 큰 경우
	1-2) 현재 node의 key 수가 최소이고, 왼쪽 또는 오른쪽 형제 node의 key 수가 최소보다 큰 경우 
	1-3) 현재 node와 왼쪽, 오른쪽 형제 node의 key 수가 최소이고, 부모 node의 key 수가 최소보다 큰 경우 
	1-4) 현재 node와 왼쪽, 오른쪽 형제 node, 부모 node 모두 key 수가 최소인 경우
**2. 삭제할 key가 leaf node를 제외한 node에 있는 경우** 
	2-1) 현재 node 또는 자식 node의 key 수가 최소보다 큰 경우 
	2-2) 현재 node와 자식 node 모두 key 수가 최소인 경우
```

```
<편의상 용어 설명>
Lmax := 현재 node의 왼쪽 자손 중 가장 큰 key
Rmin := 현재 node의 오른쪽 자손 중 가장 작은 key
par := 현재 node를 가리키는 부모 node의 포인터의 오른쪽에 있는 key. 가장 우측에 있는 포인터인 경우 왼쪽에 있는 key
K := 삭제할 key
```

**1-1) 현재 node의 key 수가 최소보다 큰 경우**

- 단순히 삭제해도 무방

**1-2) 현재 node의 key 수가 최소이고, 왼쪽 또는 오른쪽 형제 node의 key 수가 최소보다 큰 경우**

- K를par로 바꿔준다. 그리고 par를 왼쪽 형제 node의 key 수가 최소보다 크다면 Lmax로, 오른쪽 형제 node의 key 수가 최소보다 크다면 Rmin로 바꿔준다.

**1-3) 현재 node와 왼쪽, 오른쪽 형제 node의 key 수가 최소이고, 부모 node의 key 수가 최소보다 큰 경우** 

- K를 삭제하고,par를 부모 node에서 분할하여 형제 node와 합쳐준다. 그러면 부모 node의 key 수가 하나 줄고, 자식 node의 수도 하나 줄어들어 B-Tree 조건을 유지한다.

**1-4) 현재 node와 왼쪽, 오른쪽 형제 node, 부모 node 모두 key 수가 최소인 경우**

- 부모 node가 root인 subtree의 높이가 줄어들기 때문에 트리의 재구조화가 필요하다.

**2-1) 현재 node 또는 자식 node의 key 수가 최소보다 큰 경우** 

- K의 Lmax 또는 Rmin과 자리를 바꿔준다. 그 후엔 leaf node 에서의 K삭제와 동일해짐

**2-2) 현재 node와 자식 node 모두 key 수가 최소인 경우**

- K를 삭제하는 경우 B-Tree 조건을 만족하기 위해 트리의 높이를 줄여야 한다. → 트리 재구조화

```
<재구조화>
1. K를 삭제하고K의 양쪽 자식을 하나로 합친다. 합쳐진 node를 n1이라고 하자.
2. K의 par를 K의 형제 node에 합쳐준다. 합쳐진 node를 n2라고 하자.
3. n1을 n2의 자식이 되도록 연결한다.
4-1. 만약 n2의 key 수가 최대보다 크다면 key 삽입 과정과 동일하게 분할을 한다.
4-2. 만약 n2의 key 수가 최소보다 작다면 2.로 돌아가서 동일한 과정을 반복한다. (n2의 par를 n2의 형제 node에 합쳐준다)
```

- 자세한 과정 살펴보기

[[DB] 10. B-Tree (B-트리)](https://rebro.kr/169)

- B-Tree를 직접 만들어보며 볼 수 있는 사이트

[B-Tree Visualization](https://www.cs.usfca.edu/~galles/visualization/BTree.html)

- 데이터베이스 인덱스로 B-Tree를 택한 이유에 대한 블로그(읽어보시면 진짜 좋을 것 같아요!)

[데이터베이스 인덱스는 왜 'B-Tree'를 선택하였는가](https://helloinyong.tistory.com/296)

![스크린샷 2022-08-28 오후 7.00.26.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1376c543-7958-40c6-a9a7-ec3614ae9a60/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_7.00.26.png)

출처

[B 트리](https://wlswoo.tistory.com/62)

### B+Tree

<aside>
📌 B-Tree의 단점을 개선시킨 자료구조

</aside>

- B-Tree는 탐색을 위해 노드를 찾아서 이동해야하는 단점이 존재
- 이러한 단점을 해결하기 위해 B+Tree는 **같은 레벨의 모든 키값들이 정렬**되어 있고, **같은 레벨의 형제 노드는 연결리스트 형태**로 이어져 있음
- 특정 값을 찾아야 한다면, leaf node에 모든 자료들이 존재하고, 그 자료들이 연결리스트로 연결되어 있어 탐색에 있어 매우 유리함!
- **leaf node가 아닌 노드 = 인덱스 노드**
    - value에는 다음 노드를 가리킬 수 있는 **포인터 주소** 존재
- l**eaf node 자료 = 데이터 노드**
    - value값에 **데이터** 존재
- 따라서 **키값은 중복 가능**하고(인덱스 노드와 데이터 노드 동시에 존재 가능), **데이터 검색**을 위해서는 반드시 **leaf node까지 내려와야함**
- index 부분과 leaf 노드로 구성된 순차 데이터 부분으로 이루어짐.
    - 인덱스 부분의 key 값은 leaf에 있는 key 값을 직접 찾아가는데 사용.
- 대부분의 데이터베이스 시스템은 검색속도가 중요하기 때문에 B+Tree 구조를 채택

![스크린샷 2022-08-28 오후 6.44.54.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/69b7b354-9c46-425e-8c2c-ec53670f8fec/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.44.54.png)

**👀 규칙**

- 데이터 노드의 자료는 정렬됨
- 데이터 노드에서는 데이터가 중복되지 않음
- 모든 leaf node는 같은 레벨에 있음
- leaf node가 아닌 node의 키값의 수는 그 노드의 서브트리수보다 하나가 적음
- 모든 leaf node는 연결리스트로 연결되어 있음

👍 **장점**

1. leaf node를 제외하고 데이터를 저장하지 않기 때문에 메모리를 더 확보 가능. 따라서 하나의 node에 더 많은 포인터를 가질 수 있기 때문에 트리의 높이가 더 낮아지므로 검색 속도를 높일 수 있음
2. B+Tree는 leaf node에만 데이터가 linked list 형태로 저장되어 있기 때문에 범위 탐색시 선형 시간이 소모. B-Tree는 모든 node를 확인해야함

**👎 단점**

B-Tree의 경우 최상 케이스에서는 루트에서 끝날 수 있지만, B+tree는 무조건 leaf 노드까지 내려가봐야 함

**삽입**

1. key 수가 최대보다 적은 leaf node에 삽입하는 경우
    - leaf node의 가장 앞이 아닌 곳은 단순 삽입
    - leaf node의 가장 앞에 삽입되는 경우, 해당 node를 가리키는 부모 node의 포인터의 오른쪽에 위치한 key를 K로 바꿔줌. 또한 삽입된 key에 linked list로 연결

1. key의 수가 최대인 leaf node에 삽입하는 경우 → 분할 필요
    - 중간 node에서 분할이 일어나는 경우 B-Tree와 동일하게 해주기
    - leaf node에서 분할이 일어나는 경우, 중간 key를 부모 node로 올려주는데, 오른쪽 node에 중간 key를 붙여 분할한다. 그리고 분할된 두 node를 Linked list로 연결.

**삭제**

1. 삭제할 key가 leaf node의 가장 앞에 있지 않은 경우
    - B-Tree와 동일한 방법으로 삭제

1. 삭제할 key가 leaf node의 가장 앞에 위치한 경우
    - leaf node가 아닌 node에 key가 중복해서 존재. 따라서 해당 key를 노드보다 오른쪽에 있으면서 가장 작은 값으로 바꿔주기

- 자세한 과정

[]()

[[DB] 11. 인덱스(Index) - (1) 개념, 장단점, B+Tree 등](https://rebro.kr/167?category=484170)

- B+Tree 생성 확인하기

[B+ Tree Visualization](https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html)

### B-Tree vs B+Tree

![스크린샷 2022-08-28 오후 7.03.38.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de82f41d-0b6a-455e-ab46-b86973c009e1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_7.03.38.png)

### 트라이(Trie)

<aside>
📌 문자열에서 검색을 빠르게 도와주는 tree 형태의 자료구조

</aside>

- 정수형에서 BST를 사용하면 시간복잡도가 O(logN)
- 하지만, 문자열에 적용할 경우 문자열 최대 길이가 M이면 시간복잡도가 O(MlogN)이 됨
- 트라이 활용시 O(M)으로 문자열 검색 가능
- 하지만, 각 노드에서 자식들에 대한 포인터들을 배열로 저장하여 저장 공간의 크기가 크다. (메모리 측면에서 비효율적)
    - 문자열이 모두 영소문자로 이루어져 있다고 해도, 자식 노드를 가리키는 26개의 포인터를 저장해야함
    - 최악의 경우, 집합에 포함되는 문자열들의 길이의 총합만큼 노드가 필요하므로, 총메모리는 O(포인터 크기 * 포인터 배열 개수 * 총노드의 개수)
    - 만약, 1000자리의 문자열이 1000개만 들어온다고 하더라도 100만 개의 노드가 필요하고, 포인터의 크기가 8byte라고 하면 약 200MB의 메모리가 필요하게 된다.
- 이를 해결하기 위해 map이나 vector를 이용하여 필요한 노드만 메모리를 할당하는 방식을 이용.

🔍 사용

- 자동완성 기능, 사전 검색 등 문자열 탐색

![스크린샷 2022-08-28 오전 4.30.45.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/33eefade-1880-4f44-949e-564c35c209b1/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-28_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_4.30.45.png)

- 집합에 포함된 문자열의 접두사들에 대응되는 노드들이 서로 연결된 트리
- 한 문자열에서 다음에 나오는 문자가 현재 문자의 자식 노드가 되고, 빨간색으로 나타낸 노드는 한 문자열의 끝을 의미
- 문자열 탐색시 문자열의 끝에 도달했을때, 해당 노드가 빨간 노드라면 찾고자 하는 문자열이 집합에 포함되어 있는 것

M: 문자열들의 수, L: 가장 긴 문자열의 길이

| 생성 | O(M*L) |
| --- | --- |
| 삽입 | O(L) |
| 탐색 | O(L) |

- Code
    
    ```java
    static class Trie {
        boolean end;
        boolean pass;
        Trie[] child;
    
        Trie() {
            end = false;
            pass = false;
            child = new Trie[10];
        }
    
        public boolean insert(String str, int idx) {
    
            //끝나는 단어 있으면 false 종료
            if(end) return false;
    
            //idx가 str만큼 왔을때
            if(idx == str.length()) {
                end = true;
                if(pass) return false; // 더 지나가는 단어 있으면 false 종료
                else return true;
            }
            //아직 안왔을 때
            else {
                int next = str.charAt(idx) - '0';
                if(child[next] == null) {
                    child[next] = new Trie();
                    pass = true;
                }
                return child[next].insert(str, idx+1);
            }
    
        }
    }
    ```
    

## 참고 자료

- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Data Structure/Tree.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Tree.md)
- [https://yoongrammer.tistory.com/71](https://yoongrammer.tistory.com/71)
- [https://code-lab1.tistory.com/61](https://code-lab1.tistory.com/61)
- [https://code-lab1.tistory.com/62](https://code-lab1.tistory.com/62)
- [https://yoongrammer.tistory.com/72](https://yoongrammer.tistory.com/72)
- [https://nesoy.github.io/articles/2018-08/Algorithm-RedblackTree](https://nesoy.github.io/articles/2018-08/Algorithm-RedblackTree)
- [http://kocw-n.xcache.kinxcdn.com/data/document/2021/konyang/choijinmyung0121/7-6.pdf](http://kocw-n.xcache.kinxcdn.com/data/document/2021/konyang/choijinmyung0121/7-6.pdf)
- [https://ssocoit.tistory.com/217](https://ssocoit.tistory.com/217)