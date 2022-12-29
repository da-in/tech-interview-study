# 깊이우선탐색(DFS)와 너비우선탐색(BFS)
코딩테스트의 출제율이 가장 높다고 생각하는 알고리즘 중 하나인데..<br/>
무슨 알고리즘인지 알아보자.

우선, 두 알고리즘은 모두 그래프를 탐색하는 알고리즘이다.<br/>
※그래프 : 정점(node)와 그 정점을 연결하는 간선(edge)으로 이루어진 자료구조의 일종

그래프를 탐색한다는 것은 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문한다는 것!

## 깊이 우선 탐색 (Depth-First-Search)
루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방식!

![img](https://user-images.githubusercontent.com/50827930/209961641-b2bba803-a288-420b-b494-28fb698d484a.gif)
```javascript
const graph = {
  A: ["B", "C"],
  B: ["A", "D"],
  C: ["A", "G", "H", "I"],
  D: ["B", "E", "F"],
  E: ["D"],
  F: ["D"],
  G: ["C"],
  H: ["C"],
  I: ["C", "J"],
  J: ["I"]
};
const visited = [];
const DFS = (graph, curNode) => {
  if (curNode === null) return; // 여기 중단 조건
  visited.push(curNode);
  for (let nextNode of graph[curNode]) {
    if(visited.includes(nextNode)) continue;
    DFS(graph, nextNode);
  }
};
DFS(graph, "A")
```


## 너비 우선 탐색 (Breadth-First-Search)
루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방식!<br/>
시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법

![img (1)](https://user-images.githubusercontent.com/50827930/209961679-b8e2a430-f6fc-49da-82d7-2d5e2986fa13.gif)

```javascript
const graph = {
  A: ["B", "C"],
  B: ["A", "D"],
  C: ["A", "G", "H", "I"],
  D: ["B", "E", "F"],
  E: ["D"],
  F: ["D"],
  G: ["C"],
  H: ["C"],
  I: ["C", "J"],
  J: ["I"]
};

const BFS = (graph, startNode) => {
  const visited = []; // 탐색을 마친 노드들
  const queue = []; // 탐색해야할 노드들

  queue.push(startNode); // 노드 탐색 시작
  visited.push(startNode);

  while (queue.length > 0) { // 탐색해야할 노드가 남아있다면
    const node = needVisit.shift(); // queue이기 때문에 선입선출, shift()를 사용한다.
    for (let nextNode of graph[node]) {
      if(visited.includes(nextNode)) continue;
      queue.push(nextNode)
      visited.push(nextNode)
    }
  }
};
BFS(graph, "A")
```

## 깊이 우선 탐색(DFS)과 너비 우선 탐색(BFS) 비교
| DFS(깊이우선탐색) | BFS(너비우선탐색) |
| :--------------- | :---------------|
|현재 정점에서 갈 수 있는 점들을 깊게 들어가면서 탐색 | 현재 정점에 연결된 가까운 점들부터 탐색 |
|스택 또는 재귀함수로 구현 | 큐를 이용해서 구현 |
### 시간복잡도
- 두 방식 모두 조건 내의 모든 노드를 탐색한다는 점에서 시간 복잡도는 동일
- DFS와 BFS 둘 다 다음 노드가 방문된 상태인지 확인하는 시간과 각 노드를 방문하는 시간을 합하면 된다.
- 그래프를 구현한 형식에 따라 시간 복잡도가 다름

  - 인접 리스트 : O(N+E)
  - 인접 행렬 : O(N^2)
  - 일반적으로 E(간선)의 크기가 N^2에 비해 상대적으로 적기 때문에 인접 리스트 방식이 효율적임!
### 활용하기 좋은 문제
- 단순히 그래프의 모든 정점을 방문하는 것이 중요한 문제의 경우 : DFS / BFS 둘 중 편한거 암거나
- 최단거리 구해야하는 문제 : BFS가 유리! (깊이 우선탐색으로 탐색할 경우 최선이 아닐 수 있음)

## Reference
- https://devuna.tistory.com/32
- https://velog.io/@sangbooom/JS-BFS-DFS
