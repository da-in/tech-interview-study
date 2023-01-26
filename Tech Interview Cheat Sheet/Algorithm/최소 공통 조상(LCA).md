# 최소 공통 조상(Lowest Common Ancestor, LCA)

**최소 공통 조상(LCA)** 문제는 두 노드의 공통된 조상 중에서 가장 가까운 조상을 찾는 문제이다.

ex) `LCA(3, 5) = 1`

<img src="" alt="" width="">

## 기본 최소 공통 조상(LCA) 알고리즘

1. 모든 노드에 대한 깊이(depth)를 계산한다.
2. 두 타켓 노드를 확인하고, 높은 노드와 깊이가 같아질 때 까지 낮은 노드의 부모로 거슬러올라간다.
3. 높이가 같은 두 노드에서 반복해서 부모 방향으로 거슬러 올라간다.

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

## 개선된 최소 공통 조상(LCA) 알고리즘

기본 LCA 알고리즘에서 부모 노드로 거슬러 올라가는 단계를 빠르게 개선한 방법이다.

- `1`씩 거슬러 올라가는 것이 아니라 `2의 제곱` 형태로 거슬러 올라간다.
- DP를 활용한다.

1. 모든 노드에 대한 깊이(depth)를 계산한다.
2. 각 노드의 $2^i$ 번째 부모에 대한 정보를 기록한다.
3. 두 타켓 노드를 확인하고, 높은 노드와 깊이가 같아질 때 까지 낮은 노드의 부모로 거슬러올라간다.
   - $2^i$ 중 가능한 가장 큰 값 만큼 먼저 올라간다.
4. 높이가 같은 두 노드에서 반복해서 부모 방향으로 거슬러 올라간다.
   - $2^i$ 중 가능한 가장 큰 값 만큼 먼저 올라간다.

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
    dfx(y, depth + 1)

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
  # 부모 노드가 같아지도록
  if a == b:
    return a
  for i in range(LOG - 1, -1, -1):
    # 조상을 향해 거슬러 올라가기
    if parent[a][i] != parent[b][i]:
      a = parent[a][i]
      b = parent[a][i]
  return parent[a][0]

set_parent()
a, b = map(int, input().split())
print(lca(a, b))

---

## Reference

▶️ [Youtube 동빈나 최소 공통 조상(Lowest Common Ancestor, LCA) 알고리즘 10분 정복](https://www.youtube.com/watch?v=O895NbxirM8)
📄 https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/solutions/194159/official-solution/
```
