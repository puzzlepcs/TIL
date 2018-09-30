# Local Search
fringe: 지금까지 탐색했던 node를 기억하는 것.
Local search에서는 과거의 상태를 기억하지 않고, **현상태** 만 고려하는 것
## 1. Local search and Optimization
### 1.1 Local Search
  - keep track of single current state
  - Move only to neighboring states: 오로지 가능한 operation은 현재상태에 인접한 곳으로만 이동가능
  - Ignore paths
* 장점
  - Use very little memory
  - Can often find reasonable solutions in large or infinite (continuous) state spaces.
* "Pure optimization"
  - Property 1: All states have an objective or heuristic function
  - Property 2: Goal is to find state with max (or min) objective value
  - Property 3: Doesn't quite fit into path-cost/goal-state formulation
  - Property 4: Local search can do quire well on these problems

## 2. 대표적인 Local Search: Hill-climbing search
### 2.1 Hill-climbing search
* 알고리즘
  - 더 좋은 곳으로 이동함
  - 현재 상태보다 더 좋은 상태가 없다면 종료
  - 일종의 "greedy local best search"
* local maxima
  - 현재 상태보다 더 좋은 상태가 주변에 없다면 종료하기 때문에 local maxima에서 종료된다.
  - hill climbing is suboptimal
  - 이 자체로는 별로 도움이 되지 않는 정보가 아님  => random restart를 충분히 많이 한다면 global maximum을 찾을 수 있음
### 2.2 example: 8-queens problem

### 2.3 Hill-climbing with random restarts
- Different variations
  - Run a fixed number of N restarts
  - For each restart: run until termination
- Analysis
  - Optimality가 보장되지 않음
    - Optimality가 보장되야 하는 문제에서는 사용하지 말아야 함..
    - 그러나 대부분의 문제가 optimal하지 않아도 됨
  - Say each search has probability p of success
    - 124번(state space)
