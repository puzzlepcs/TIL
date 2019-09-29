# node2vec summary

Created By: cla kim  
Last Edited: Sep 29, 2019 1:06 PM  
Tags: Graph,Study,Summary  
[원문](https://cs.stanford.edu/~jure/pubs/node2vec-kdd16.pdf)


## 1. 연구 배경, 문제 정의
- 네트워크에서의 prediction task
    - node에 대한 label classification task (특히, Multi-Label classification task)
    - link prediction task (두 노드가 주어졌을 때 두 노드 사이에 edge가 있나 없나)
- 노드의 local neighborhood를 반영하는 objective
    - **[homophily]** : 노드가 어떤 communities에 소속되어 있는가
        - 서로 연결이 많이 되어 있고 비슷한 network cluster에 소속되어 있다면 embedded closely
    - **[structural role]** : 노드가 어떤 역할을 수행하고 있는가 (hub, bridge 등)
        - 연결 여부가 중요한 것은 아님.
        - 서로 연결되어 있지 않아도 비슷한 역할을 수행하고 있다면 embedded closely
- **node2vec**
    - semi-supervised algorithm for scalable feature learning in networks
    - 그래프 기반 objective function을 SGD을 통해 최적화.(Skipgram & Negative sampling)
    - 2nd-order random walk를 통해 노드의 neighborhood를 찾아냄.
        - homophily and/or structural equivalence를 **parameter 조정**을 통해 두 성질 **모두**를 반영하는 neighborhood를 Random Walk 과정을 통해 찾아냄.
        - 네트워크의 특성에 맞는 neighborhood를 탐색할 수 있다는 장점
    - 노드를 *d*-dimensional feature space에 표현.

## 2. Feature Learning Framework

- Objective function

    $$max_f ∑_u logPr(N_s(u)|f(u))$$

    - 두가지 가정
        - Conditional independence. 각 노드는 서로 독립적이라고 가정. ⇒ 확률을 곱해줌

        $$Pr(N_s(u)|f(u)) = ∏_{n_i\in{N_s(u)}} Pr(n_i|f(u))$$

        - Symmetry in feature space. pair 로 반영 ⇒ dot product의 softmax 함수를 활용

        $$Pr(n_i|f(u)) = \frac{exp(f(n_i)·f(u))}{∑_{v\in{V}} exp(f(v)·f(u))}$$

    - 따라서 Objective function을 다음과 같이 정리할 수 있음.

        $$max_f \sum_{u\in{V}} \left[ -logZ_u + \sum_{n_i\in{N_s(u)}}f(n_i)\cdot f(u) \right]$$

- Classic Search Strategies
    - BFS
        - local-view (micro)
        - structural equivalence 반영
        - variance가 작음
        - node가 비교적 중복적으로 뽑힘
    - DFS
        - global-view (macro)
        - homophily 반영
        - varience 가 큼
        - complex dependencies
- node2vec
    - **Random Walks** (2nd-Order)
        - BFS와 DFS의 interpolation을 통해 네트워크의 특성을 반영하는 neighborhood 샘플링
        - 각 노드마다 r번 walk. 각 walk의 길이는 l ⇒ 총 r * n개의 walk
        - 노드 *t*에서 노드 *v*로 진행 했을 때, 현재 노드 *v* 로부터 연결된 다음 노드로 진행할 확률

            $$\alpha _{pq}(t,x) = \begin{cases} \frac{1}{p}&\text{if } d_{tx} = 0 \\ 1 & \text{if } d_{tx} = 1 \\ \frac{1}{q} & \text{if } d_{tx} = 2 \end{cases} $$

            - Return parameter p (직전 노드로 돌아가기)
                - p > 1 : DFS, global, homophily
                - p < 1 : BFS, local, structural equivalence
            - In-out parameter q (진행하기)
                - q > 1: BFS, local , structural equivalence
                - q < 1: DFS, global, homophily
    - **Likelihood Optimization** → Skipgram + Negative Sampling
        - 각 walk에서 window size k만큼 (target,neighbor) pair 취득. (Skipgram)
        - (target, neighbor) pair에서 target을 input으로 했을 때 output이 neighbor와 최대한 비슷해 지도록 다음 Objective function을 사용하여 f를 업데이트.

            $$max_f \sum_{u\in{V}} \left[ -logZ_u + \sum_{n_i\in{N_s(u)}}f(n_i)\cdot f(u) \right]$$

            - 이때, 모든 노드의 경우를 더해서 업데이트 하는 것은 비효율적임. 따라서 전체 노드가 아닌 일부 노드(Z_u) 만을 계산해줌. (Negative Sampling)

## 3. 기타

- Multi-label vs Multi-Class
    - Multi-label classification: 한 객체가 여러개의 label을 가질 수 있음을 의미
    - Multi-class classification: 한 객체가 여러 종류의 label을 가질 수 있음 (label은 한개)
