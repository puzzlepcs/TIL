# Informed/Heuristic Search
## 1. Best-first Search
* Idea: use an **evaluation function** f(n) for each node
  - 현재 상태가 얼마나 좋은가 나타내는 함수
  - 좋으면 좋을수록 먼저 꺼내는 방식
* Implementation
  - Order the nodes in fringe by f(n) (by desirability, lowest f(n) first)

## 2. Heuristic function
* Heuristic : "using *rules of thumb* to find answers"
  - 검증가능하지 않지만 상당히 유용한 정보
  - knowledge vs heuristic
    - knowledge(지식): 검증가능고, 증명가능하며, 항상 참인 정보
    - heuristic: 검증하지 않고, 증명가능하지 않고, 항상 참이라는 보장이 없는 불확실한 정보
* Heuristic function h(n)
  - Estimate of (optimal) cost from n to goal
  - h(n) = 0 if n is a goal node
    - (goal 과의 difference를 설정할 수 있음)
  - Example: straight line distance from n to Bucharest

* 8-puzzle
  - h1 = the number of misplaced tiles
    - 일종의 hamming distance
    - 문제의 타일을 뽑아서 옮길 수 없다는 제약 조건을 relax 한 경우
  - h2 = the sum of the distances of the tiles from their goal positions (Manhattan distance).
    - 적어도 h2만큼은 움직여야 Goal state에 도달함 (실제 걸리는 turn 의 수는 h2보다 항상 크거나 같다)
    - 다른 타일 위에 올라갈 수 없다는 제약 조건을 relax한 경우
  - h2가 더 좋음! 실제 거리와 더 유사하기 때문

## 3. Greedy best-first Search
* Special case of best-first search
  - Uses h(n) = heuristic function as its evaluation function
  - Expand the node that appears closest to goal

* `0 <= h <= h*`을 만족하는 h를 사용하면 그 답이 optimal 함을 보장한다. (h*: 실제 minimum distance)

### 3.1 Properties of greedy best-first search
* Complete?
  - Not unless it keeps track of all states visited
    - Otherwise can get stuck in loops(just like DFS)
* Optimal?
  - NO! 항상 optimal하다는 것을 보장할 수 없음
  - Greedy 한 알고리즘; 지금까지 왔던 길을 합해야 함
* Time?
  - O(b^m), can generate all nodes at depth m before finding solution
  - m = maximum depth of search space

## 4. A* search
### 4.1 A* search 정의
* A Serach: Heuristic만 사용하면 지금까지 온 거리의 정확한 값을 알 수 없음
* 따라서 Evaluation function에 연산을 추가함
* Evaluation function `f(n) = g(n) + h(n)`
  - g(n) = cost so far to reach n
  - h(n) = estimated cost from n to goal
  - f(n) = estimated total cost of path through n to goal

* h(n)을 0으로 설정하면 uniform cost search와 같음

* A* serach: `*`는 optimality가 항상 보장된다는 의미
  - `0 < h < h*(n)`인 h(n)을 사용한 경우

### 4.2 Admissible heuristics
* A heuristic *h(n)* is **admissible** if for every node *n*, h(n) <= h*(n), where h*(n) is the true cost to reach the goal state from n.
* An admissible heuristic never overestimates the cost to reach the goal,

### 4.3 Properties of A*
* Complete?
  - YES (unless there are infinitely many nodes with f <= f(G))
* Optimal?
  - YES
  - Also optimally efficient
    - No other optimal algorithm sill expand fewer nodes, for a given heuristic
* Time?
  - Exponential in worst case
* Space?
  - Expoenetial in worst case

### 4.4 heuristic 찾기
#### 4.4.1 Notion of dominance
- 모든 n에 대해 `h2(n) >= h1(n)` 이면 h2가 h1을 **dominate** 하다고 한다.
- 위와 같은 경우 h2를 사용하는 것이 더 좋다.
* heuristic을 잘 정의되면 search space를 줄일 수 있어서(branch factor를 줄임) 효율적인 서치가 가능하다

#### 4.4.2 Inventinc heuristics cia "relaxed problems"
제일 작은 제약조건을 제거하면서 heuristic 함수를 찾는 방법

* 8-퍼즐의 경우
  * h1함수는 타일을 뽑아서 제자리에 놀 수 없다는 제약조건을 relax 해준 것임.
  * h2함수는 다른 타일 위에 올라갈 수 없다는 제약조건을 relax 해준 것임.
