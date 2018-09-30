# Uninformed Search Algoritms
마구잡이로 찾는 방식

## 1. Time and space complexity are measure in terms of
- *b*: maximum branching factor of the search tree
- *d*: depth of the least-cost solution
- *m*: maximum depth of the state space (무한대일 수 있음)
## 2. BFS vs DFS
### 2.1 Breadth-First Search(BFS)
- Expand shallowest unexpanded node
- Fringe: nodes waiting in a queue to be explored, also called **OPEN**
- Implementation:
  - For BFS, *fringe* is a frist-in-first-out queue
  - new successors go at end of the queue
- Repeated status?
  - Simple strategy: do not add parent of a node as a leaf
- Properties
  - Complete? Yes
  - Optimal? YES
  - Time complexity O(b^d)
  - Space complexity O(b^d)
- Drawback : Expoenetial space complexity

### 2.2 Depth-First Search (DFS)
- Expand deepest unexpanded node
- Implementation:
  - For DFS, *fringe* is a Last-in-first-out (LIFO) stack
  - new succeossors go at beginning of the stack
- Repeated nodes?
  - Simple strategy: Do not add a state as a leaf if that state is on the path from the root to the current node
- Properties
    - Complete? Not complete if tree has unbounded depth
    - Optimal? NO
    - Time complexity O(b^m)
    - Space complexity O(bm)
- Drawback : Expoenetial space complexity
- DFS with a depth-limit L
  - 일반적인 DFS이지만 특정 depth-limit L 보다 더 깊이 탐색하지 않는 경우
  - solves problem of infinitely deep paths with no solutions
    - But will be incomplete if solution is below depth-limit
  - Depth-limit L can be selected based on problem knowledge
    - E.g. diameter of state-space
      - E.g. max number of steps btw 2 cities
    - But typically not known ahead of time in practice

### 2.3 비교
- 시간복잡도: SAME, but
  - In the worst-case BFS is always better than DFS
  - Sometime, on the avg DFS is better if:
    - many goals, no loops and no infinite path
- BFS는 메모리 낭비가 심함!!
- In general
  - BFS is better if
    - goal is not deep
    - infinite paths
    - many loops
    - small search space
  - DFS is better if
    - many goals,
    - not many loops
  - DFS is much better in terms of memory


## 3. Iterative deepening search (IDS)
- Run multiple DFS searches with increasing depth-limits
- Algorithm
  - L = 1
  - While no solution, do
    1. DFS from initial state S0 with cutoff L
    2. If found goal, stop and return solution
    3. else, increment depth limit L
* Space complexity = O(bd)
* Time complexity = O(b^d)
* completeness 가 보장됨. 무한정으로 깊어지는 경우 없음
* optimality : 보장됨(depth가 최소가 되는 것을 보장)
- DFS의 적은 메모리 사용, BFS의 completeness 를 combine한 방법!

### 3.1 DFS와의 비교: Isn't IDS wasteful?
*  최악의 경우 탐색하는 노드의 갯수
  * IDS : (b) + (b+b^2) + .... + (b + ... + b^d)
  * DFS : 1 + b + b^2 + ... +  b^d = (b^(d+1) -1)/ b-1
  * 생각보다 redundancy가 크지 않음을 확인할 수 있다.
- IDS는 large search space를 가지고 unknown solution depth를 갖는 경우 많이 사용된다.

## 4. Uniform Cost Search (UCS)
weighted graph일 경우에 사용되는 방법.
Priority queue(heap)을 사용 (우선순위가 높은 순으로 빼내는 자료구조)

* g(n) = cost from start state S to node n
* algorithm
  * Always expand the node on the fringe with minimum cost g(n)
* optimality
  * weight 값이 항상 양수라는 보장이 없음. weight 값이 음수가 있다면 optimality가 보장이 되지 않음
  - path found = lowest cost
* completeness : 무한 state로 들어가지 않음. (무한 state는 비용도 무한적으로 커진다는 이야기..) 유한 거리 안에 goal이 있다면 무조건 찾아줌.
  * weight가 모두 같은 숫자라면 bfs와 동일해짐

- complexity of Uniform Cost
  - Let C* be cost of the optimal solution
  - Assume that every step costs at least eps > 0
  - Worst-case time and space complexity is:
    `O(b^[1+floor(C*/eps)])`
    - `floor(C*/eps)` : depth of solution if all costs are approximately equal


## 5. Summary
- A review of search
  - a search space consists of states and operators: It is a graph
  - a search tree represents a paticular exploration of search space
- Uninformed search
  - Breadth-first
  - depth-first
  - iterative deepening
  - uniform cost search

Criterion|BFS|Uniform-cost|DFS|Depth-Limited|Iterative Deepening
---------|---|------------|---|-------------|-------
complete?|Yes|Yes|No|No|Yes
Time|`O(b^(d+1))`|`O(b^[C*/eps])`|`O(b^m)`|`O(b^l)`|`O(b^d)`
Space|`O(b^(d+1))`|`O(b^[C*/eps])`|`O(bm)`|`O(bl)`|`O(bd)`
Optimal?|Yes|Yes|No|No|Yes
