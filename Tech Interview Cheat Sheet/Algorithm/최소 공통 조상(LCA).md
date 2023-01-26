# 최소 공통 조상(Lowest Common Ancestor, LCA)

**최소 공통 조상(LCA)** 문제는 두 노드의 공통된 조상 중에서 가장 가까운 조상을 찾는 문제이다.

ex) `LCA(8, 15) = 2`

<img src="https://user-images.githubusercontent.com/66757141/214862314-5a0a5437-9ab7-48cb-932d-c271353c9c4a.PNG" alt="LCA" width="550px">

<br/>

## 기본 최소 공통 조상(LCA) 알고리즘

1. 모든 노드에 대한 `깊이(depth)`를 계산한다.
2. 두 타켓 노드를 확인하고, **높은 노드와 깊이와 같아질 때 까지** 낮은 노드의 부모로 거슬러올라간다.
   > 예시에서 8번 노드의 깊이는 3, 15번 노드의 깊이는 4로 더 아래에 있다. 따라서 깊이가 3인 15번의 부모 노드 11까지 거슬러 올라간다.
3. 높이가 같은 상황에서 반복해서 부모 방향으로 거슬러 올라간다.
   > 8번 노드와 11번 노드를 가리킨 상황에서, 각각의 부모 노드가 같을 때 까지 거슬러 올라간다.
   > 8의 부모 4 != 11의 부모 5 (부모로 올라가기)  
   > 4의 부모 2 == 5의 부모 2 (종료)

<img src="https://user-images.githubusercontent.com/66757141/214862679-d6c6b021-8579-42ea-8788-5f96585b893b.PNG" alt="Basic LCA" width="550px">

### 기본 최소 공통 조상(LCA) 알고리즘 시간복잡도

- 한 번의 LCA를 찾는 과정은 트리가 편향된 최악의 경우 **O(N)** 의 시간복잡도를 갖는다.
- LCA를 반복적으로 수행하는 경우 수행복잡도가 좋지 않다.

```python
import sys
sys.setrecursionlimit(int(1e5)) # 런타임 오류 피하기
n = int(input())

parent = [0] * (n+1) # 부모 노드 정보
d = [0] * (n + 1) # 각 노드까지의 깊이
c = [0] * (n + 1) # 각 노드의 깊이가 계산되었는지 여부
graph = [[] for _ in range(n+1)] # 양방향 그래프 정보

for _ in range(n - 1):
  a, b = map(int, input().split())
  graph[a].append(b)
  graph[b].append(a)

# 루트 노드부터 시작하여 깊이를 구하는 함수
def dfs(x, depth):
  c[x] = True
  d[x] = depth
  for y in graph[x]:
    if c[y]: # 이미 깊이를 구했다면 넘기기
      continue
    parent[y] = x
    dfx(y, depth + 1)

# A와 B의 최소 공통 조상을 찾는 함수
def lca(a, b):
  # 먼저 깊이가 동일하도록
  while d[a] != d[b]:
    if d[a] > d[b]:
      a = parent[a]
    else:
      b = parent[b]
  # 부모 노드가 같아지도록
  while a!=b:
    a = parent[a]
    b = parent[b]
  return a

dfs(1, 0) # 루트 노드는 1번 노드
a, b = map(int, input().split())
print(lca(a, b))
```

<br/>

## 개선된 최소 공통 조상(LCA) 알고리즘

기본 LCA 알고리즘에서 부모 노드로 거슬러 올라가는 단계를 빠르게 개선한 방법이다.

- `1`씩 거슬러 올라가는 것이 아니라 `2의 제곱` 형태로 거슬러 올라간다.
- DP를 활용한다. _(세그먼트 트리를 이용하는 방법도 존재한다.)_

1. 모든 노드에 대한 깊이(depth)를 계산한다.
2. 각 노드의 $2^i$ 번째 부모에 대한 정보를 기록한다. (DP)
   > 15의 $2^0$ 째 부모는 11  
   > 15의 $2^1$ 째 부모는 5
3. 두 타켓 노드를 확인하고, 높은 노드와 깊이와 같아질 때 까지 낮은 노드의 부모로 거슬러올라간다.
   > loc(13, 15)의 예시에서, 13과 깊이가 같은 15의 부모 11까지 올라간다.
4. 높이가 같은 두 노드에서 반복해서 부모 방향으로 거슬러 올라간다.
   > 11과 13을 가리킨 상태에서 공통 부모를 향해 거슬러 올라간다.

3번과 4번 과정에서 부모 노드로 올라갈 때, 사전에 저장해놓은 부모에 대한 정보를 사용한다.

- 최소 공통 조상보다 먼 부모 노드들은 항상 값이 같다
- 그러므로 값이 다르고 가장 먼 부모를 반복해서 찾으면 최소 공통 조상에 가까워질 수 있다.
  <img src="" alt="LCA" width="600px">
  > 11 부모 노드 정보 : `[5, 2, 0, 0...]`  
  > 13 부모 노드 정보 : `[7, 3, 0, 0...]`  
  > 값이 다르고 가장 먼 부모는 2, 3 이다.  
  > 2와 3의 부모를 리턴한다.

<img src="https://user-images.githubusercontent.com/66757141/214862797-7668c52a-6a9c-43f3-baea-8f397aa17f06.PNG" alt="Improved LCA" width="550px">

### 개선된 최소 공통 조상(LCA) 알고리즘 시간복잡도

- DP(Dynamic Programming)을 이용해 시간 복잡도를 개선할 수 있다.
- 한 번의 LCA를 찾는 과정은 트리가 편향된 최악의 경우 **O(logN)** 의 시간복잡도를 갖는다.

```python
import sys
sys.setrecursionlimit(int(1e5)) # 런타임 오류 피하기
LOG = 21 # 2^20 = 1,000,000
n = int(input())

parent = [[0] * LOG for _ in range(n+1)] # 부모 노드 정보
d = [0] * (n + 1) # 각 노드까지의 깊이
c = [0] * (n + 1) # 각 노드의 깊이가 계산되었는지 여부
graph = [[] for _ in range(n+1)] # 양방향 그래프 정보

for _ in range(n - 1):
  a, b = map(int, input().split())
  graph[a].append(b)
  graph[b].append(a)

# 루트 노드부터 시작하여 깊이를 구하는 함수
def dfs(x, depth):
  c[x] = True
  d[x] = depth
  for y in graph[x]:
    if c[y]: # 이미 깊이를 구했다면 넘기기
      continue
    parent[y][0] = x
    dfs(y, depth + 1)

# 전체 부모 관계를 설정하는 함수
def set_parent():
  dfs(1, 0) # 루트 노드는 1번 노드
  for i in range(1, LOG):
    for j in range(1, n+1):
      parent[j][i] = parent[parent[j][i-1]][i-1]

# A와 B의 최소 공통 조상을 찾는 함수
def lca(a, b):
  # b가 더 깊도록 설정
  if d[a] > d[b]:
    a, b = b, a
  # 먼저 깊이가 동일하도록
  for i in range(LOG - 1, -1, -1):
    if d[b] - d[a] >= (1 << i):
      b = parent[b][i]
  # 부모 노드가 같아지도록 올라가기
  if a == b:
    return a
  for i in range(LOG - 1, -1, -1):
    # 최소 공통 조상보다 먼 부모 노드들은 항상 값이 같다
    # 그러므로 값이 다르고 가장 먼 부모를 반복해서 찾으면 최소 공통 조상에 가까워질 수 있다
    if parent[a][i] != parent[b][i]:
      a = parent[a][i]
      b = parent[a][i]
  return parent[a][0]

set_parent()
a, b = map(int, input().split())
print(lca(a, b))
```

<br/>

---

## Reference

▶️ [Youtube 동빈나 최소 공통 조상(Lowest Common Ancestor, LCA) 알고리즘 10분 정복](https://www.youtube.com/watch?v=O895NbxirM8)  
📄 https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/solutions/194159/official-solution/
