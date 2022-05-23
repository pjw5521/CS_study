## ****LCA(Lowest Common Ancestor) 알고리즘****

---

최소 공통 조상 알고리즘

⇒ 두 노드의 공통된 조상 중 가장 가까운 조상을 찾는 알고리즘

![lca](https://user-images.githubusercontent.com/67946662/168473528-c1365763-9b92-4303-9810-53adfdb4bde6.png)


### 동작순서

1. 모든 노드에 대한 깊이를 계산한다.
2. 최소 공통 조상을 찾을 두 노드를 확인한다.
3. 먼저 두 노드의 깊이가 동일하도록 거슬러 올라간다.
4. 부모가 같아질 때까지 반복적으로 두 노드의 부모 방향으로 거슬러 올라간다.
5. 모든 LCA(a, b) 연산에 대하여 3~4번의 과정을 반복한다.

```python
// 두 정점의 depth 확인하기
while True:
	if (depth가 일치):
		if (두 정점의 parent 일치?): LCA 찾음(종료)
        else: 두 정점을 자신의 parent 정점 값으로 변경
    else: // depth 불일치
        더 depth가 깊은 정점을 해당 정점의 parent 정점으로 변경(depth가 감소됨)
}
```

### 시간복잡도

- 매 쿼리마다 부모 방향으로 거슬로 올라가기 위해 최악의 경우 *O*(*N*)의 시간 복잡도가 요구됩니다. (한쪽에 치우쳐서 일렬로 된 노드인 경우)
- 따라서 모든 쿼리(M)를 처리할 때의 시간 복잡도는 *O*(*NM*)입니다.


### LCA 알고리즘 구현

[https://www.acmicpc.net/problem/11437](https://www.acmicpc.net/problem/11437)

```python
import sys
sys.setrecursionlimit(int(1e5)) # 런타임 오류를 피하기 위한 재귀 깊이 제한 설정

n = int(input())

parent = [0] * (n + 1) # 부모 노드 정보
d = [0] * (n + 1) # 각 노드까지의 깊이
c = [0] * (n + 1) # 각 노드의 깊이가 계산되었는지 여부
graph = [[] for _ in range(n + 1)] # 그래프(graph) 정보

for _ in range(n - 1):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)

# 루트 노드부터 시작하여 깊이(depth)를 구하는 함수
def dfs(x, depth):
    c[x] = True
    d[x] = depth
    for y in graph[x]:
        if c[y]: # 이미 깊이를 구했다면 넘기기
            continue
        parent[y] = x
        dfs(y, depth + 1)

# A와 B의 최소 공통 조상을 찾는 함수
def lca(a, b):
    # 먼저 깊이(depth)가 동일하도록
    while d[a] != d[b]:
        if d[a] > d[b]:
            a = parent[a]
        else:
            b = parent[b]
    # 노드가 같아지도록
    while a != b:
        a = parent[a]
        b = parent[b]
    return a

dfs(1, 0) # 루트 노드는 1번 노드

m = int(input())

for i in range(m):
    a, b = map(int, input().split())
    print(lca(a, b))
```
