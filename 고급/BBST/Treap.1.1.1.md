# Treap (Cartesian Tree)

Treap은 이진 트리와 이진 힙이 합쳐진 자료구조이다 (Tree + Heap $\Rightarrow$ Treap).

Treap은 순서쌍 $(X, Y)$를 이진 트리에 저장하는데, 이때 $X$를 기준으로는 이진 탐색 트리가 되고 $Y$를 기준으로는 이진 힙이 된다. 만약 트리의 어떤 정점이 값 $(X_0, Y_0)$를 갖는다면, 왼쪽 서브트리의 모든 정점에 대해서는 $X \leq X_0$가 성립하고 오른쪽 서브트리의 모든 정점에 대해서는 $X_0 \leq X$가 성립한다. 그리고 양쪽 서브트리의 모든 정점에 대해서 $Y \leq Y_0$가 성립한다.

Treap은 데카르트 좌표계에 쉽게 나타낼 수 있기 때문에 "Cartesian Tree"라고도 불린다.

![](https://upload.wikimedia.org/wikipedia/commons/e/e4/Treap.svg)

Treap은 1989년에 Raimund Siedel과 Cecilia Argon이 제안하였다.

## Treap의 데이터 저장 방식이 가지는 장점

이러한 구현 방식에서 $X$값은 키(동시에 Treap에 저장된 값)이고 $Y$값은 **속성**이다. 속성이 없으면 Treap은 $X$를 기준으로 한 평범한 이진 탐색 트리이다. $X$값들의 집합은 서로 다른 다양한 트리에 대응된다. 그 중 어떤 것들은 연결 리스트와 같은 형태를 만들기도 해서 매우 느리다 (주요 연산들이 $O(N)$ 시간 복잡도를 가지게 된다).


