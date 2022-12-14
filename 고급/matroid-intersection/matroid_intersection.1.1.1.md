# Matroid Intersection

**사전 지식.** 아래 항목을 모두 깊이 이해하고 있을 필요는 없지만 친숙한 개념이 있다면 Matroid Intersection을 빠르게 잘 이해할 수 있다.

1. 집합론과 집합 연산의 기초
1. 그래프의 신장 트리(Spanning tree)
1. 이분 그래프의 매칭
1. 벡터 공간의 선형 독립
1. 벡터 집합의 랭크(Rank)와 기저(Basis)
1. 가우스 소거법
1. 크루스칼의 최소 신장 트리 알고리즘
1. 쿤의 이분 매칭 알고리즘
1. 이산 수학

## 매트로이드

매트로이드는 벡터 공간의 선형 독립 개념을 추상화하고 일반화한 구조이다.

형식적인 정의는 다음과 같다. 매트로이드는 순서쌍 $\left\langle X, I \right\rangle$으로 표현된다. $X$는 ground set이고 $I$는 $X$의 모든 독립 부분 집합으로 이루어진 집합이다. 다시 말해 매트로이드 $\left\langle X, I \right\rangle$는 $X$의 각 부분 집합이 *독립*인지 *종속*인지 ($I$에 포함되는지 또는 $I$에 포함되지 않는지) 분류를 정한다.

모든 매트로이드는 다음의 세 가지 성질을 만족한다.

1. 공집합은 독립이다.
1. 독립 집합의 부분 집합은 독립이다.
1. 독립 집합 $A$가 독립 집합 $B$보다 크기가 작다면, $A$가 독립임을 유지하면서 $A$에 추가할 수 있는 $B$의 원소가 적어도 하나 존재한다.

이것은 매트로이드의 *공리적 성질*이다. 매트로이드임을 증명하기 위해서는 일반적으로 위의 세 가지 성질을 증명해야 한다.

**기저.** 임의의 최대 크기의 독립 집합은 주어진 매트로이드의 기저이다. 다시 말해 독립을 유지하면서 기저에 추가될 수 있는 원소가 존재하지 않는다. 모든 기저의 크기는 동일하다 (그렇지 않다면 세 번째 공리적 성질에 의해 큰 기저에서 작은 기저로 무언가를 추가할 수 있다). 기저는 다른 기저의 부분 집합이 아니다. 임의의 독립 집합은 어떤 기저의 부분 집합이다 (세 번째 성질에 의해 어떤 기저에 도달할 때까지 집합의 크기를 증가시킬 수 있다), 따라서 매트로이드의 모든 기저를 아는 것은 매트로이드를 완전히 표현하기에 충분하다.

**회로.** 전체 집합을 제외한 모든 부분 집합이 독립인 종속 집합은 회로이다. 다시 말해, 회로는 어떤 원소를 제거해도 독립이 되는 종속 집합이다. 회로는 다른 회로의 부분 집합이 아니다 (그렇지 않다면 더 큰 회로에서 종속을 유지하면서 원소들을 제거할 수 있다). 각 종속 집합은 적어도 하나의 회로를 부분 집합으로 갖는다. 기저와 동일하게, 매트로이드의 모든 회로를 아는 것은 매트로이드를 완전히 표현하기에 충분하다.

회로에는 또 다른 중요한 성질이 있다. 두 회로의 합집합에서 임의로 하나의 원소를 제거해도 집합은 여전히 어떤 회로를 갖는다. 특정한 종류의 매트로이드는 더 엄격한 성질을 갖는다. 서로 다른 두 회로의 대칭차집합은 항상 하나의 회로를 갖는다. 두 집합의 대칭차집합은 둘 중 하나의 집합에만 포함되는 모든 원소의 집합이다 ($A \Delta B = (A \setminus B) \cup (B \setminus A)$). 예를 들어, 이 성질은 그래프의 사이클 공간과 관련되어 있다.

**랭크. 랭크 함수.** 매트로이드의 랭크는 해당 기저의 크기이다. 그러나 랭크 대신 기저의 크기라고 직접 부를 수 있다면 랭크에 대한 구체적인 정의가 왜 필요할까? 랭크는 실제로 유연하지 않다 (랭크 대신 기저의 크기로 언급할 수 있다). 랭크를 더 유연하게 만들기 위해서 랭크 함수 $r(S)$를 정의할 수 있다. 이 함수는 ground set의 어떤 부분 집합 $S$의 최대 독립 집합의 크기를 알려준다. 어떤 부분 집합의 랭크 함수 값은 매트로이드에서 해당 부분 집합의 랭크라고 부를 수 있다. 부분 집합의 이러한 정보는 여러 상황에서 매우 우용하다. 랭크 함수의 성질은 다음과 같다.

1. 부분 집합의 랭크는 해당 부분 집합의 크기보다 클 수 없다.
1. 독립 집합의 랭크는 해당 부분 집합의 크기이다.
1. 전체 ground set의 랭크는 매트로이드의 랭크와 같다. 공집합의 랭크는 $0$이다.
1. 집합 $S$의 임의의 부분 집합의 랭크는 $S$의 랭크보다 크지 않다.
1. 집합에 하나의 원소를 추가하는 것은 집합의 랭크를 $1$만큼 증가시키거나 바꾸지 않고 유지한다. (어떤 집합 $S$와 원소 $x \notin S$에 대해서 $r(S) \leq r(S \cup \{x\}) \leq r(S)+1$이다.)
1. 매트로이드의 랭크 함수는 submodular이다. 두 집합 $A$와 $B$가 있고, $B$에 있지만 $A$에 없는 모든 원소를 $B$에서 $A$로 옮기는 것은 두 집합의 랭크의 합을 증가시키지 않는다. $r(A) + r(B) \geq r(A \cup B) + r(A \cap B)$이다.

![](https://codeforces.com/predownloaded/e2/32/e232071f8639629598a69d5d6210d2f9960c3ce0.png)

**Independence oracle.** 부분 집합의 분류를 각 부분 집합의 정보를 저장하는 것으로 다룰 수는 없다 (메모리 사용량이 지수적으로 증가한다). 부분 집합의 독립/종속을 확인하기 위한 다른 도구가 필요하다. 만약 매트로이드가 어떤 다른 구조 원소간의 관계의 결과로서 정의된다면, 다항 시간에 동작하는 부분 집합의 독립성을 판단하는 알고리즘을 대부분의 경우 찾을 수 있다. 매트로이드의 개념을 추상화하고 내부적인 독립성 매커니즘에 관계없이 사용하고 싶으므로, 부분 집합의 독립성을 검사하기 위한 서브루틴으로 *independence oracle*을 정의한다. 그리고 어떤 알고리즘의 수행 시간을 *oracle call*의 횟수로 구할 수 있다. (그러나 실제로는 알고리즘 최적화 때문에 내부 매커니즘을 완전히 잊을 수는 없다.)

## 매트로이드의 예시

매트로이드에는 다양한 종류가 있다. 그 중 일부를 소개하면 다음과 같다.

**Uniform matroid.** 부분 집합 $S$의 크기가 어떤 상수 $k$($|S| \leq k$)보다 크지 않을 때, $S$를 독립으로 여기는 매트로이드이다. 가장 단순한 형태의 매트로이드로, Uniform matroid는 ground set의 원소를 구별하지 않고 원소의 개수만을 고려한다. 크기가 $k$인 모든 부분 집합은 이 매트로이드의 기저이고, 크기가 $(k+1)$인 모든 부분 집합은 이 매트로이드의 회로이다. 다음과 같이 Uniform matroid의 특이한 경우를 정의할 수 있다.

1. Trivial matroid. $k = 0$. 공집합만이 독립으로 간주된다. ground set의 모든 원소는 종속이다 (결과적으로 ground set 원소의 어떤 조합도 종속이다).
1. Complete matroid. $k = |X|$. ground set을 포함한 모든 부분 집합이 독립이다.

**Linear (algebra) matroid.** Ground set이 벡터 공간의 벡터로 이루어져 있다. 벡터의 집합은 선형 독립일 경우 (어떤 벡터도 다른 벡터의 조합으로 표현될 수 없는 경우) 독립으로 여겨진다. 벡터 집합의 선형 기저는 메트로이드의 기저이다. 이 메트로이드의 회로는 임의의 벡터가 다른 모든 벡터의 조합으로 표현될 수 있는 벡터의 집합이다. 이 매트로이드의 independence oracle은 가우스 소거법을 기반으로 한다.

**Colorful matroid.** Ground set이 색칠된 원소들로 이루어져 있다. 각 원소는 오직 하나의 색을 갖는다. 집합에 같은 색을 가지는 원소 쌍이 없을 경우 독립이다. 집합의 랭크는 집합에 포함된 서로 다른 색의 개수이다. 이 매트로이드의 기저는 각 색의 원소를 하나씩만 가지고 있는 집합이다. 이 매트로이드의 회로는 동일한 색 원소의 모든 쌍이다.

**Graphic matroid.** 무향 그래프의 간선에 대해 정의된다. 간선의 집합은 사이클을 가지지 않을 경우 독립이다. 연결 그래프에서 기저는 그래프의 스패닝 트리이다. 연결 그래프가 아니라면 기저는 각 컴포넌트의 스패닝 트리로 이루어진 포레스트이다. 단순 사이클은 회로이다. 이 매트로이드의 independence oracle은 DFS/BFS 또는 DSU를 사용하여 구현할 수 있다.

![](https://codeforces.com/predownloaded/fb/da/fbdabffaebd62a6f71b3e9cffac0f8ce09eedf8f.png)

**Truncated matroid.** 매트로이드의 성질을 잃지 않고 모든 매트로이드의 랭크를 $k$로 제한할 수 있다. 예를 들어, truncated colorful matroid의 기저는 $k$개 이하의 서로 다른 색을 한 번씩만 사용하는 집합이다. Truncated graphic matroid의 기저는 $(n-k)$개 이상의 연결 요소로 이루어진 사이클이 존재하지 않는 그래프의 간선의 집합이다 ($n$은 그래프의 정점의 개수이다). 이는 매트로이드의 세 번째 성질이 매트로이드의 기저 뿐 아니라, 매트로이드의 모든 독립 집합에 적용되기 때문이다. 크기가 $k$보다 큰 독립 집합이 연속적으로 제거된다면, 크기가 $k$인 독립 집합이 새로운 기저가 된다. 그리고 그보다 작은 독립 집합은 여전히 추가할 원소를 기저로부터 찾을 수 있다.

**Ground set의 부분 집합 매트로이드.** 매트로이드의 성질을 잃지 않고 ground set의 부분 집합으로 ground set을 제한할 수 있다. 이는 종속성 법칙이 ground set의 특정한 원소에 의존하지 않기에 가능하다. 그래프에서 간선 하나를 제거해도 이는 유효한 그래프이다. 집합(벡터 집합 또는 색칠된 원소의 집합)에서 하나의 원소를 제거해도 같은 종류의 원소로 구성되고 동일한 규칙이 적용되는 집합을 얻는다. 따라서 ground set이 자신의 부분 집합으로 제한된 매트로이드의 랭크는 매트로이드의 부분 집합의 랭크와 같다.

**Expanded matroid. Direct matroid sum.** 두 매트로이드가 있을 때, 첫 번째 매트로이드의 ground set의 원소가 독립/종속에 영향을 주지 않으며 두 번째 매트로이드의 ground set의 원소와 중복이 없고 이것이 역으로도 성립한다면 어려움 없이 두 매트로이드를 하나의 큰 매트로이드로 생각할 수 있다. 두 개의 연결 그래프인 두 개의 graphic matroid를 생각해보자. 두 개의 연결 요소로 이루어진 그래프가 되도록 두 그래프를 합칠 수 있다. 여기서 하나의 연결 요소의 간선을 포함하는 것은 다른 연결 요소에 아무런 영향을 주지 않는다. 이것을 *direct matroid sum*이라고 한다. $M_1 + M_2 = \left\langle X_1 \cup X_2, I_1 \times I_2 \right\rangle$으로 표기하며, $\times$는 두 집합의 데카르트 곱을 의미한다. 다양한 종류의 많은 매트로이드를 제약 없이 합칠 수 있다.

## Rado-Edmonds Algorithm

매트로이드 $M = \left\langle X, I \right\rangle$의 기저를 효율적으로 찾는 방법을 살펴본다.

매트로이드의 세 번째 성질에 의해서, 기저의 크기보다 작은 크기의 독립 집합 $S$가 있다면 $S$가 독립임을 유지하면서 $S$에 추가할 수 있는 원소 $x$를 찾을 수 있다. 그러므로 독립임이 보장된 공집합에서 시작해서 ground set에서 다음으로 추가할 원소를 선형 탐색하며 하나씩 원소를 추가한다. Ground set $X$의 크기를 $n$, 매트로이드 $M$의 랭크를 $r$이라 할 때, 알고리즘은 $\mathcal{O}(r \cdot n)$번의 *oracle call*에 동작한다.

어떤 원소 $x$가 $S$에 추가되지 않았다면 $x$는 앞으로도 $S$에 추가되지 않는다. 만약 $S \cup \{x\}$가 종속이라면 어떤 회로 $C$를 포함할 것이고 이 알고리즘에서 원소를 제거하지 않기 때문에 미래에도 $S \cup \{x\}$는 회로 $C$를 포함하며 종속이다. 따라서 단 한번의 탐욕적인 탐색으로 기저를 찾을 수 있다 (그 순간 $S$에 원소를 추가해도 독립이라면 $S$에 원소를 추가한다). 이로서 알고리즘의 수행 시간을 $\mathcal{O}(n)$으로 향상시킬 수 있다.

Ground set의 각 원소 $x$가 가중치 $w(x)$를 가질 때, 가중치 합이 최소가 되는 매트로이드의 기저를 구해보자.

크루스칼의 최소 신장 트리 알고리즘은 사실 graphic matroid에 대해 위 문제를 해결하는 알고리즘이다. 따라서 크루스칼 알고리즘과 유사하게 증명할 수 있다.

$A$를 크기가 $k$인 최소 가중치 독립 집합, $B$를 크기가 $(k+1)$인 최소 가중치 독립 집합이라고 하자. 매트로이드의 세 번째 성질에 의해서, $A$가 독립임을 유지하면서 $A$에 추가할 수 있는 $B$의 원소 $y$가 적어도 하나 존재한다. 따라서 크기가 $k$인 집합 $B \setminus \{y\}$와 크기가 $(k+1)$인 집합 $A \cup \{y\}$가 존재한다. 최소 가중치 집합이 무엇인지 알고 있기 때문에 다음과 같이 적을 수 있다.

$A \leq B \setminus \{y\}$

$B \leq A \cup \{y\}$

첫 번째 부등식의 양 변에 $y$를 더한다.

$A \cup \{y\} \leq (B \setminus \{y\}) \cup \{y\}$

$A \cup \{y\} \leq B$

식을 정리하면 다음과 같다.

$B \leq A \cup \{y\} \leq B$

이는 다음과 필요충분조건이다.

$B = A \cup \{y\}$

크기가 $k$인 최소 가중치 독립 집합에 독립성을 깨지 않는 어떤 원소 $y$를 추가하는 것으로 크기가 $k+1$인 최소 가중치 독립 집합을 얻을 수 있다. 가능한 $y$가 여러개 있다면 가중치가 가장 작은 $y$를 선택한다.

앞선 결과들로 가중치 합이 최소가 되는 기저를 구하는 알고리즘을 나타낼 수 있다.

1. Ground set의 원소를 가중치의 오름차순으로 정렬한다.
1. 공집합 $S$로부터 시작한다.
1. 정렬된 순서로 ground set의 원소를 순회한다. $S$가 독립임을 유지한다면 현재 원소를 $S$에 추가한다.

시간 복잡도의 경우 $\mathcal{O}(n \cdot log(n))$번의 단위 연산을 정렬에 필요로 하며, $\mathcal{O}(n)$번의 *oracle call*을 요구한다.

이것이 Rado-Edmonds 알고리즘이다. 특정 매트로이드에 대한 예시로 위에서 언급한 크루스칼의 최소 신장 트리 알고리즘이 있다.

만약 임의의 매트로이드의 기저를 탐욕적으로 구할 수 있고 매트로이드가 일반화를 위한 것이라면, 모든 그리디 문제를 어떤 매트로이드의 기저를 찾는 것으로 환원할 수 있지 않을까? 아쉽게도 그렇지는 않다.

탐욕적 해답의 경우 원소를 정렬할 뿐 아니라, 과정 중에 추가적인 원소를 생성하거나, 특별한 비교 연산자를 사용하거나, 조건문을 활용한다. 가중치가 아니라 다른 제약 조건을 가하더라도, 특정한 경우에만 매트로이드를 사용할 수 있다. 일반적으로 매트로이드를 적용할 수 있는지 증명하기 위해서는 매트로이드의 공리적 성질을 증명해야 한다.

## Matroid Intersection

Matroid intersection은 두 개의 매트로이드의 교집합에서 가장 큰 공통 독립 집합을 찾는 문제이다. 두 개의 매트로이드 $M_1 = \left\langle X, I_1 \right\rangle$과 $M_2 = \left\langle X, I_2 \right\rangle$가 주어졌을 때 $\max\limits_{S \in I_1 \cap I_2} |S|$를 만족하는 집합 $S$를 찾아야 한다. 다시 말해 두 매트로이드에서 모두 독립으로 여겨지는 가장 큰 $S$를 찾아야 한다.

Matroid intersection의 예시는 다음과 같다.

**Colorful spanning tree.** 그래프가 주어지고 그래프의 각 간선에는 색이 칠해져 있다. 이 그래프에서 각 색상이 많아야 한 번 사용된 스패닝 트리를 찾아야 한다. 매트로이드 분류는 "같은 색상이 한 번 이하로 사용된 간선의 집합"과 "사이클을 가지지 않는 간선의 집합"이다.

**Colorful linear basis.** 어떤 벡터 공간의 벡터 집합이 주어지고 각각의 벡터에는 색이 칠해져 있다. 각 색삭이 많아야 한 번 사용된 벡터 집합의 기저를 찾아야 한다. Linear matroid와 colorful matroid가 적용된다.

**Bipartite graph maximum matching.** 많이 알려진 이분 그래프의 최대 매칭 문제이다. 이분 그래프가 주어질 때, 서로 다른 두 간선이 하나의 정점을 공유하지 않는 가장 큰 간선들의 집합을 찾아야 한다. 문제를 조금 쉽게 변형하여 기존 문제 대신 간선의 왼쪽 정점을 공유하지 않도록 하는 문제를 해결해보자. 이 문제는 왼쪽의 각 정점에 대해 간선을 하나씩 선택하는 것으로 쉽게 해결할 수 있다. 탐욕적 접근이 가능하고 적절한 매트로이드를 형성한다. 이분 그래프이므로, 두 번째 매트로이드를 오른쪽 정점들에 대해 대칭적으로 정의하고 matroid intersection으로 해결한다.
