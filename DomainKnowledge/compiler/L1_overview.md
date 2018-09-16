# Overview
## 1. Why Compilers?
* Compiler
  * Translator 라고도 함. general 하게 하나의 프로그램 랭귀지를 다른 랭귀지로 바꿔주는 것
  * 소스의 의미를 보존해야함.
  * target language로 만들어진 결과물이 efficient해야 함. (최적화 필요)
* In the beginning , there was machine language
  * 디버깅 하기 어렵고, 코드를 작성하는 것 자체도 어려움
  * (스크립트 랭귀지: 코드 전체를 컴파일 하지 않고 중간중간 인터피리터가 번역해줌)
  * 하드웨어가 복잡해지고, 소프트웨어 관리가 low-level로 관리하기가 어려워짐.

* 왜 중요함?
  * computer architecture
  * CAD tools
  * Software developers

## 2. Compiler Structure
Source Program -> Translator -> Object Program -> Loader, Linker, and Run-time System -> output
* Source language
  - 컴파일러가 프로그램만 만드는 것은 아님
* Target language
  - Machine code, assembly
  - High-level languages, simply actions
  - high level -> high level 해주는 컴파일러는?
    - C to C compiler? : 고도화된 전처리기로서 사용
    - 전처리기 -> find and replace! 작업. 일종의 C-to-C 컴파일러라고 할 수 있음.
    - 전처리기는 문법을 체크해주지는 않음.
* Compile time vs run time
  - 컴파일 타임
  - 런 타임
    - variable latency: load latency는 가변적임. 어디에 그 변수가 저장되어 있는지 알 수 없기 때문
    - history를 알 수 없음! 이러한 정보는 run-time에서만 알 수 있음
      - (jit)just-in-time compile: 러닝 타임중에 컴파일 하는 것. 가장 효율적이지 않음. 오버헤드가 상당히 크다. 한사이클 그냥 돌리는게 효율적일 수 있음. 언제 컴파일 해야하는지 체크해야 하는 작업이 추가적으로 필요함.
      - 프로파일링 : 일부 컴파일을 하고 그 정보를 점검하는 방식. 대표성의 문제~ 코드의 어느 부분을 점검하는지가 중요. 인풋에 따른 결과가 다를 수 있음.
```
int a, b, c, d;
double d,e,f;
c = a+b      // 1)
f = d+e      // 2) 오래 걸리니까 최대한 먼저 해줘야 함!! 1번보다 먼저 해주기
g = c+(int)f // 3)
```

* Front-end vs Back-end
  - Front-end: Machine independent
  - Back-end: Machine dependent


## 3. Front end
### 3.1 Lexical Analysis(Scanner)
* Extracts and identifies lowest level lexical elements form a source stream
  - extract한 정보가 Pre-defined된 중요한 정보인지 체크
  - 하나하나 token으로 만들어줌
* 주석을 인지하고 제거해줌
* implemented with a finite state automata

### 3.2 Lex/Flex
* Automatic generation of scanners
* Lex/Flex
  - output: lexical analysis를 해주는 프로그램
  - input: 나의 문법

### 3.3 Parser
* 문법적으로 맞는지 틀리는지 확인해줌
* 자동화 되어 있음.
  - Parser를 만드는 프로그램을 사용
* Yacc(yet another compiler compiler)/bison
  - Given a context free grammer
  - Generate a parser for that language(agian a C program)

**시험문제~ 어떤 에러인지 찾아내기 syntax인지 semantics인지**

### 3.4 Static Semantic Analysis
* Several distinct actions to perform
  - Check definition of identifiers, ascertain that the usage is correct
  - Disambugyate overloaded operators

## 4. Backend
* frontend를 거치면
  - 어샘블리어
* 최적화되어 있지 않음.(redunent함)
  - 리소스가 얼마나 있는지 알 수 없음
  - 하드웨어가 어떤지 알 수 없음
* 따라서 Backend의 목표는 이러한 일을 해주는 것!
  - Optimize code quality
  - Map applicationto real hardware

### 4.1 Dataflow and Control Flow Analysis
머신과 상관 없이 코드를 수정해주는 작업
* Dataflow analysis
  - 문법적으로 틀리지 않아도, 사용되지 않는 부분
* Control flow analysis


### 4.2 Optimization
* Machine dependent하게 코드를 수정해줌
