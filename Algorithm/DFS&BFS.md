## DFS & BFS

#### 작성자 : [박지원](@pjw5521)

### 대표문제 
백준 1260 [DFS와 BFS](https://www.acmicpc.net/problem/1260)

</br>

### 탐색이란?
- 많은 양의 데이터 중에서 원하는 데이터를 찾는 과정 
- 대표적인 탐색 알고리즘 : DFS, BFS

### 스택과 큐 
- 스택(Stack) : 선입후출 구조, append(). pop() 메소드 이용
- 큐(Queue) : 선입선출 구조, deque 라이브러리 사용, append(). popleft() 메소드 이용

### 재귀함수
- 자기 자신을 다시 호출하는 함수
- 종료 조건을 반드시 명시

### 그래프 표현 방식
- 인접 행렬 : 2차원 배열로 그래프의 연결관계를 표현하는 방식
- 인접리스트 : 리스트로 그래프의 연결 관계를 표현하는 방식
- Python은 인접리스트를 이용해 그래프를 표현할 때도 2차원 리스트를 이용하면 됨 

### **DFS (깊이 우선 탐색)**
- 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
- 재귀함수 사용
- 모든 노드를 방문하는 경우(특정 조건이 될 때까지 탐색하는 경우)에 사용
- 시간복잡도(인접 행렬) : O(V^2)
    ```python
    def dfs(v):
        visited[v] = True
        print(v,end=" ")
        for i in range(1, n+1):
            if graph[v][i] == 1 and not visited[i]:
                dfs(i) 
    ```
    
### **BFS (너비 우선 탐색)**
- 가까운 노드부터 탐색하는 알고리즘
- queue 사용
- 최소 비용 문제(최단 경로 문제), 간선의 가중치 1 일 때 사용
- 시간복잡도(인접 행렬) : O(V^2)
    ```python
    def bfs(v):
        q = deque()
        q.append(v)
        visited[v] = True
        
        while q:
            v = q.popleft()
            print(v,end=" ")
            for i in range(1,n+1):
                if graph[v][i] == 1 and not visited:
                    q.append(i)
                    visited[i]=True
    ```