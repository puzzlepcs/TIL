# Lexical Analysis - Part 2
## 1. How does Lex Work?
### 1.1 Overview
- input: REs for Tokens
- Flex 내부에서의 과정
  1. RE -> NFA
  2. NFA -> DFA
  3. optimize DFA
  4. DFA Simulation : Character Stream 으로 시뮬레이션 진행
- output: Token streams(and errors)

### 1.2 Regular Expressionto NFA
* Thompson's construction algorithm
  - build the NFA inductively
  - base RE에 대해서 define rule
  - Combine for more complex REs

### 1.3 NFA to DFA
과거를 저장하지 않기 위해서 DFA로 바꿔주는 작업이 필요(현상태만 저장)
같은 input으로 다른 states로 가는 transitions와 eps transitions을 제거해줘야 함
* problem 1. Multiple transitions
  - 여러개의 state를 묶어서 하나의 state로 만들어주기
  - 문제점: 복잡함
* problem 2: eps transitions
  - eps-closure : 하나의 state로 부터 eps transition을 사용해 갈 수 있는 state들을 묶어서 하나의 state로 만들기
  - 문제점: accpeting state가 계속 늘고, 복잡함

### 1.4 NFA to DFA Optimizations
