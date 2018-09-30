# Adversarial search
### 게임에 관한 가정
- 턴을 주고 받는 2명의 player가 있음
- Utility values for each agent are the opposite of the other
  - If a utility value increases for one playter, then it decreases for the other player
  - 이 상황이 adversarial situation을 만든다
- In game theory terms:
  - Deterministic
  - Tunr-taking
  - Zero-sum games
  - Perfect information
    - 명확히 상대방의 정보를 모두 볼 수 있음

### Serach vs. Games
- Search : no adversary
  - Solution is a method for finding goal or a path to goal
  - Some Heuristics techniques can find optimal solution
  - Evaluation function is an estimate of cost from start to goal through a given node
  - Ex: path finding, 8-puzzle

- Games: adversary
  - 적대적!
  - Ex: chess, checkers, Othello, Go

### Game Setup
- Tow players(MAX and MIN)
- MAX moves first and they take turns until the game is over
- Games as search: 4 components
  1. Initial state
  2. Successor function: list of legal moves at the current game state
  3. Terminal test
  4. Utility function
- So, MAX uses a sually very big search tree to determine next move

## Minimax strategy
- 적이 항상 optimal strategy를 사용한다는 가정 (나에게 가장 불리한 수를 둔다고 가정)
- Min 값중에 Max값을 선택하기

### What happens if MIN does not play optimally?
- 항상 optimal 하게 두지 않더라도 이 방법이 통할까?
  - 상대방이 optimal 하게 두지 않더라도 내 점수가 더 높아지는 꼴
  - 더 좋아지면 좋아지지 나빠질 일이 없다~

## Multiplayer games
vector값을 뱉는 utility 함수를 정의해줘야 한다.
### Aspects of multiplayer games
- Standard minimax assumes that each player operates to maximize only their own utility
- 실제로는 alliances를 형성하는 경우가 있다.
- If game is not zero-sum then alllainces can be useful even with 2 players

#### cf 주사위를 사용하는 경우
주사위 레이어와 내가 선택하는 경우의 수를 나타내는 플래이어 레이어가 한 레이어처럼 작동하면 된다. (일반적으로는 자신의 수를 볼때에는 주사위값이 결정 된 후 선택하는 경우의 수만 따진다.)

점수와 확률을 곱하여 점수를 올린다. (Weighted sum, Weighted average)
