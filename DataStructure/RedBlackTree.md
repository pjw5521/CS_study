## Red Black Tree

![rbt1](https://user-images.githubusercontent.com/67946662/167283223-72a6f714-2562-4449-8b21-9a8bdd8b7251.png)

- 자가 균형 이진 탐색 트리(self-balancing binary search ree)
- 대표적으로 연관배열(associative array)를 구현하는데 쓰이는 자료구조
- O(logn)의 시간복잡도로 삽입, 삭제, 검색을 할 수 있다.
- 동일한 노드의 개수일 때, depth를 최소화하여 시간 복잡도를 줄이는 것이 핵심 아이디어
    - 동일한 노드의 개수일 때, depth가 최소가 되는 경우는 tree가 complete binary tree인 경우이다.

### 레드 블랙 특성

1. 각 노드는 `Red` or `Black`이라는 색깔을 갖는다.
2. 루트 노드는 Black이다.
3. 모든 리프(NIL : null leaf, 자료를 갖지 않고 트리의 끝을 나타내는 노드)은 Black이다.
4. 노드가 Red이면, 그 노드의 자식은 반드시 Black이다. == No Double Red
5. 각 노드에 대해서 노드로부터 descendant leaves 까지의 단순 경로는 모두 같은 수의 black nodes 들을 포함하고 있다. 이를 해당 노드의 `Black-Height`라고 한다. 
*cf) Black-Height: 노드 x 로부터 노드 x 를 포함하지 않은 leaf node 까지의 simple path 상에 있는 black nodes 들의 개수*

### **Red-Black Tree 의 특징**

1. Binary Search Tree 이므로 BST 의 특징을 모두 갖는다.
2. Root node 부터 leaf node 까지의 모든 경로 중 최소 경로와 최대 경로의 크기 비율은 2 보다 크지 않다. 이러한 상태를 `balanced` 상태라고 한다.
    
    ⇒ 삽입, 삭제, 검색 시 최악의 경우에서의 시간 복잡도가 트리의 깊이에 따라 결정되기 때문에 보통의 이진 검색 트리에 비해 효율적이다.
    
3. 노드의 child 가 없을 경우 child 를 가리키는 포인터는 NIL 값을 저장한다. 이러한 NIL 들을 leaf node 로 간주한다.

![rbt2](https://user-images.githubusercontent.com/67946662/167283227-e0fc96d1-f874-4589-beff-6855b966bf01.png)


모든 NIL 리프 마다 하나씩의 노드를 할당하는 방법도 있으나 불편한 점이 많다. 이대신, 노드 하나를 할당하여 이를 리프로 정하고 모든 NIL 리프에 대한 포인터가 이 노드를 가리키도록 하면 된다. 공간도 절약할 수 있을뿐더러 경계 조건을 다루기도 편리해진다. 

### 삽입

![https://blog.kakaocdn.net/dn/blkAJy/btrpiHjqbii/tj9F3pQv8oZwVgD7ffX4w1/img.png](https://blog.kakaocdn.net/dn/blkAJy/btrpiHjqbii/tj9F3pQv8oZwVgD7ffX4w1/img.png)

레드-블랙 트리에 새로운 노드를 삽입할 때 **새로운 노드**는 항상 **빨간색**으로 삽입한다.

이렇게 되면 3번 조건이 위배되는 상황이 발생한다. 즉, **빨간색 노드가 연속으로 2번 나타날 수 있다(Double Red)**

레드 블랙 트리는 이러한 Double Red 문제를 해결하기 위해 2가지 전략을 사용한다.

![https://blog.kakaocdn.net/dn/bYG3yV/btrpoxGRp6g/fBAd1VvrqdWy6QRRSKTX3k/img.png](https://blog.kakaocdn.net/dn/bYG3yV/btrpoxGRp6g/fBAd1VvrqdWy6QRRSKTX3k/img.png)

새로 삽입할 노드를 **N**(New), 부모 노드를 **P**(Parent), 조상 노드를 **G**(Grand Parent), 삼촌 노드를 **U**(Uncle)라고 하자. 

Double Red가 발생했을 때

- 삼촌 노드가 검은색이라면 -> Restructuring을 수행하면 된다.
- 삼촌 노드가 빨간색이라면 -> Recoloring을 수행하면 된다.

**1) Restructuring**

![restructuring](https://user-images.githubusercontent.com/67946662/167283215-583a8d3b-b71a-43da-80ee-7795eed4833e.png)


1. 새로운 노드(N), 부모 노드(P), 조상 노드(G)를 오름차순으로 정렬한다.

2. 셋 중 중간값을 부모로 만들고 나머지 둘을 자식으로 만든다.

3. 새로 부모가 된 노드를 검은색으로 만들고 나머지 자식들을 빨간색으로 만든다.

**2) Recoloring**

![recoloring](https://user-images.githubusercontent.com/67946662/167283217-75588705-551a-4eac-a4a6-1c60d4e71d29.png)


1. 새로운 노드(N)의 부모(P)와 삼촌(U)을 검은색으로 바꾸고 조상(G)을 빨간색으로 바꾼다.

2. 조상(G)이 루트 노드라면 검은색으로 바꾼다.

3. 조상(G)을 빨간색으로 바꿨을 때 또다시 Double Red가 발생한다면 또다시 Restructuring 혹은 Recoloring을 진행해서 Double Red 문제가 발생하지 않을 때까지 반복한다.

### **삽입**

우선 BST 의 특성을 유지하면서 노드를 삽입을 한다. 그리고 삽입된 노드의 색깔을 **RED 로** 지정한다. Red 로 지정하는 이유는 Black-Height 변경을 최소화하기 위함이다. 삽입 결과 RBT 의 특성 위배(violation)시 노드의 색깔을 조정하고, Black-Height 가 위배되었다면 rotation 을 통해 height 를 조정한다. 이러한 과정을 통해 RBT 의 동일한 height 에 존재하는 internal node 들의 Black-height 가 같아지게 되고 최소 경로와 최대 경로의 크기 비율이 2 미만으로 유지된다.

### **삭제**

삭제도 삽입과 마찬가지로 BST 의 특성을 유지하면서 해당 노드를 삭제한다. 삭제될 노드의 child 의 개수에 따라 rotation 방법이 달라지게 된다. 그리고 만약 지워진 노드의 색깔이 Black 이라면 Black-Height 가 1 감소한 경로에 black node 가 1 개 추가되도록 rotation 하고 노드의 색깔을 조정한다. 지워진 노드의 색깔이 red 라면 Violation 이 발생하지 않으므로 RBT 가 그대로 유지된다.

Java Collection 에서 TreeMap 도 내부적으로 RBT 로 이루어져 있고, HashMap 에서의 `Separate Chaining`에서도 사용된다. 그만큼 효율이 좋고 중요한 자료구조이다.
