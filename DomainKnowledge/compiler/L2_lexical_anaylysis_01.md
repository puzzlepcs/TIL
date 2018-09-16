# Lexical Analysis - Part 1
스마트 스캐너 같은 기능이라고 생각하면 됨.
컴파일러의 처음 단계
소스코드를 읽어주고 space와 주석 등을 제거, 특정 단어들을 조합해줌

## Frontend Structure
* Language Preprocessor: find and replace
  - Note: `gcc -E foo.c -o foo.i` to invoke just the preprocessor

## 1. Lexical Analysis
### 1.1. Specification, Recognition, and Automation
* Specification: How to specify lexical patterns?
  - In C, identifiers are strings like `x, xy, match0, _abc`.
  - Numbers are strings like `3, 12, 0.012, 3.5E4`.
  - *regular expressions*: 이러한 표현들을 정규식으로 잡아줌
* Recognition(인식): how to recognize the lexical patterns?
  - `int match0;` 이 코드에서 lexical analysis 단계에서는 `int`와 `match0`, 그리고 `;`를 뽑아냄. (다음단계인 syntax에서 이러한 것들이 어떤 의미인지 분석함.)
  - Recognisze `match0` as an identifier.
  - Recognisze `512` as a number.
  - *deterministic finite automata*: 하나하나 읽으면서 state를 바꾸면서 갈 수 없는 state로 가면 error를 발생시키고, 아니면 계속 진행하는 식으로 검사.

* Automation: how to automatically generate string recognizers from string recognizers from specifications?
  - Thompson's construction and subset construction
  - 손으로 모두 짤 수 있지만, flex등의 프로그램을 사용해서 자동으로 dfa를 만들어줄 수 있음

### 1.2. Lexical Analysis Process
- Preprocessed source code, read char by char
- Lexical analysis
    - Transform multi-character input stream to token stream
    - Reduce length of program representation(remove space)
## 2. Tokens
### 2.1.Token의 종류
* identifiers: x y11 elsex
* keywords: if else while for break
* Integers: 2 100 -20
* Floating-point: 2.0 -0.0010 .02 1e5
* Symbols: + * {} ++ << < <= []
    - cf. 주석처리 시 `/*`가 등장하면 주석 state로 넘어갔다가 `*/`가 다시 등장했을 때 원래 state로 돌아가기
* Strings: "x" "He saind,\"I luv comiler\""

### 2.2. How to Describe Tokens
* Use regular expressions to describe programming language tokens
* A regular expression (RE) is defined inductively

### 2.3. How to Break up Text
- REs alone not enough, need rule for choosing when get multiple matches
  - Longest matching token wins
  - Ties in length resolved by priorities
  - RE's + priorities + longest matching token rule = definition of a lexer

## 3. Automatic Generation of Lexers
### 3.1  개괄
- Bell Lab에서 Unix에서 사용하기 위해 70년대 중반 개발한 2가지 프로그램
  - Lex
  - Yacc/bison
- Input to lexer generator
  - List of RE in priority order
  - Associatied action with each RE
- Output
  - Program that reads input stream and breaks it up into tokens according to the REs

### 3.2 Lex Specification
lex file always has 3 sections: definition section, rules section, user function section
* Definition Section
* Rules Section
* User function Section

### 3.3 How Does Lex Work?
처음에 NFA를 만듦 (사람이 생각하기 쉬운 구조) -> DFA로 변환 -> 이를 실행할 수 있는 프로그램 작성
Regular Expression을 C code로 변환해줌
#### 3.3.1 FSA
* FSA(Finite State Automation)을 기반으로 함
  - REs generate regular sets
  - FSAs recognize regular sets
* informal def of FSA
  - finite set of states
  - Transitions btw states
  - An initial state
  - A set of final states(accepting states)
#### 3.3.2 2 kinds of FSA
* NFA (Non-deterministic finite automata)
  - multiple possible transitions or some transitions that do not require an input(eps transitions)
  - 이런 경우 컴퓨터가 해결하기 힘듦 (여러가지의 가능성이 있기 때문)
  - May have choice at each step
  - Accepts string if there is ANY path to an accepting state
  - Not obvious how to implement this
* DFA (Deterministic finite automata)
  - transition이 단 한가지로 결정되어 있거나, 아예 진행 할 수 없음
  - eps transition이 없음
  - Action on each input is fully determined
  - Implement using table-driven approach
  - More states generally required to implement RE
