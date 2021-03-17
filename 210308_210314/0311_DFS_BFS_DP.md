20210309\_TIL
==============
알고리즘 4화_ 풀이 유형별 개념 적용 (DFS, BFS, 동적계획법)
----------------------------------------


-   **난이도 중 ~ 중하의 알고리즘 문제에서 중요한 것은 문제별로 어떤 자료구조와 알고리즘을 적용할 것인지 판단하는 것이다. **판단이 맞다면, 선정한 자료구조와 알고리즘이 가장 일반적으로 사용하는 코드 구조와 코드가 크게 달라지지 않는다는 것을 문제풀이를 통해 알게 되었다.
-   어제 발견한 점은, 문제가 달라도 동일한 자료구조, 알고리즘을 적용하는 문제는 코드가 비슷하다는 사실이었다. 그래서 오늘은 문제에 어떤 자료구조와 알고리즘을 적용하겠다는 판단이 서면 해당 자료구조, 알고리즘의 코드 구조를 거의 유사하게 가져와 적용해봤다. 덕분에 빠른 시간 안에 문제를 해결할 수 있었다.

-   **다만 난이도 중상 이상의 알고리즘 문제는 위의 방법대로 자료구조, 알고리즘의 코드 구조를 그대로 적용해 해결할 수 없었다.** 예전에 수학 문제를 풀 때에도 최고난이도 문제는 뭔가 좀 '엣지'있게 규칙을 파악하는게 필요했던 것 같다. 따라서 자료구조, 알고리즘 유형별로 기본 코드 구조를 다 학습한 후, 어려운 문제를 많이 접해보는 식으로 익숙해져나가야 할 것 같다.

-   오늘은 알고리즘 문제 개념학습 마지막 날이다. 여태까지 학습한 자료구조와 알고리즘 개념을 아래에 리스트로 정리해두었다.

---


### **각 자료구조, 알고리즘의 대표 구조를 그대로 참고해 빠르게 푼 문제들**

---


**바이러스 2606번**

[백준 2606번: 바이러스](https://www.acmicpc.net/problem/2606)

알고리즘을 선정한 후 자료구조를 역선택하는 문제였다.

알고리즘: DFS 방식을 적용

자료구조: DFS 방식을 적용하기 위한 Graph(인접리스트), Stack 자료구조 사용이 필요

파이썬 언어: 인접리스트는 딕셔너리, Stack은 리스트 형태로 구현

접근 순서

**1\. DFS의 기본 구조 확인:**

  1) 인접 리스트 구현(Adj\_graph)이 필요

  2) 시작 노드가 들어있는 Stack, 방문한 노드를 저장해두기 위한 빈 Stack을 만들어 놓고 시작

  3) DFS 함수식 구현.

이렇게 세 가지가 내가 파악한 DFS의 기본 구조다.

**2\. DFS 기본 구조 적용: **

```python
import sys

# 그래프 만들기 (인접리스트로 구현) --> 이 방법 잘 외워두기
node = int(sys.stdin.readline().strip())
edge = int(sys.stdin.readline().strip())

adj = [[] for _ in range(node)]

for _ in range(edge):
    src, dest = map(int,sys.stdin.readline().strip().split())
    adj[src-1].append(dest)
    adj[dest-1].append(src)

# 인접리스트를 키 값을 가진 딕셔너리 형태로 변환, 이 과정 뺴고 해볼 수도 있겠음
adj_graph = dict()
for i in range(node):
    adj_graph[i+1] = adj[i]

# print(adj_graph)

# # DFS를 구현하는 함수식 만들기
def dfs_stack(adjacent_graph, start_node):
    # DFS 검사를 위한 stack, visited 리스트 만들기
    stack = [start_node]
    visited = []
    while stack:
        current_node = stack.pop()
        visited.append(current_node)
        for adjacent_node in adjacent_graph[current_node]:
            if adjacent_node not in visited:
                stack.append(adjacent_node)
    # 중복제거를 위한 set, 자식노드끼리도 간선이 연결되어 있어서 중복이 발생
    return set(visited)

# print(dfs_stack(adj_graph, 1))
print(len(dfs_stack(adj_graph, 1))-1)
```

주석으로 각각 DFS의 코드 구조 중 어느 부분을 구현한 것인지 달아 두었다.

이렇게 기본 알고리즘 구조만 충실히 구현해줘도 중~ 중하 문제까지는 해결이 가능한 듯하다.

---


**피보나치 함수 1003번**

[백준 1003번: 피보나치 함수](https://www.acmicpc.net/problem/1003)

알고리즘을 선정한 후 자료구조를 역선택하는 문제였다.

알고리즘: 반복 계산을 해야 하는 문제. 재귀 알고리즘을 사용하되, 효율성 재고를 위한 동적 계획법 활용이 필요

자료구조: 동적 계획법(Dynamic Programming)활용을 위한 저장소 생성 필요

파이썬 언어: 재귀 알고리즘을 구현을 위한 재귀 함수 사용, DP를 위한 저장소는 key값과 value값을 넣을 수 있는 딕셔너리 형태로 구현

접근 순서

**1\. 동적계획법(DP) 코드 구조 확인:**

  1) DP를 위한 저장소 생성 필요 (대게 딕셔너리 형태로 진행)

  2) DP 함수 구현 필요

이렇게 두 가지가 내가 파악한 DP의 기본 코드 구조다.

**2\. DFS 코드 구조 적용: **

```python
import sys

case = int(sys.stdin.readline().strip())

# DP를 위한 저장소 생성
memo_0 = {
    0: 1,
    1: 0
}

memo_1 = {
    0: 0,
    1: 1
}

# DP 함수식 구현
def dynamic_programming(n, fibo_memo):
    if n in fibo_memo:
        return fibo_memo[n]

    nth_fibo = dynamic_programming(n - 1, fibo_memo) + dynamic_programming(n - 2, fibo_memo)
    fibo_memo[n] = nth_fibo
    return nth_fibo

case_list = []
for _ in range(case):
    input = int(sys.stdin.readline().strip())
    case_list.append(input)

for case in case_list:
    print(dynamic_programming(case, memo_0),dynamic_programming(case,memo_1))


```

주석으로 각각 DP의 코드 구조 중 어느 부분을 구현한 것인지 달아 두었다.

---


### **난이도가 있어 변형이 필요했던 문제들**

---


****토마토 7576번****

[백준 7576번: 토마토](https://www.acmicpc.net/problem/7576)

풀이를 보면 이해는 되나.. 풀 수 있게 되려면 좀 시간이 걸리는 문제다.

**응용이 들어가야 하는 부분**

1\. BFS 문제인데, 대게 노드 갯수, 간선 갯수, 간선이 연결하고 있는 노드들에 대한 정보를 주는 중~중하 문제와 달리 제공하는 데이터부터 형태가 달랐다.

2\. 노드가 이어지는 것 뿐만 아니라 '노드의 상태가 변화 (=토마토가 익는다) ' 한다는 조건 때문에 그 부분에서 응용이 더 들어가야 했다.

---


****가장 긴 증가하는 부분 수열 11053번****

[백준 11053번: 가장 긴 증가하는 부분 수열](https://www.acmicpc.net/problem/11053)

이것 역시..! 동적 계획법(DP) 관련 문제인데 응용이 더 들어가야 했다.

동적 계획법 구현 방법은 탑다운과 바텀업 방식 두 가지가 있다.

-   Top-down : 큰 문제부터 시작해서 작은 문제로 분할해가며 푼다. 위에서 아래로 진행
-   Bottom-up : 작은 문제들을 쌓아 올려 큰 문제를 푼다. 아래에서 위로 진행

위에서 언급한 피보나치 수열은 Top-down 형식이다. 큰 문제를 작은 문제로 나누고, 작은 문제를 푼다. 대게 동적 계획법 개념 설명에서도 탑다운 형태로 재귀 함수를 사용해 구현하는 법을 알려주는 게 일반적이다. 그래서 **Top-down 동적 계획법 구조만 알고 있어서 문제를 봤을 때 동적 계획법을 적용해 풀 수 없었다.**

사실 이 문제는 Bottom-up 방식으로, 작은 문제부터 해결해 문제 크기를 점점 키워나가 반복하여 가장 큰 문제를 푸는 형식이다. 동적 계획법의 기본 구조라 생각했던 재귀함수와 메모이제이션 기법은 Top-down 문제에만 국한되어 사용된다. Bottom-up 방식은 대게 반복문 형태로 구현된다고 한다.

**Bottom-up 방식의 DP 구조도 알아두어야 겠다!**

---


### **2주차 때 익힌 자료구조와 알고리즘 개념들**

****자료구조****

\- 정수

\- 실수

\- 문자

\- 문자열

\- 스택

\- 큐

\- 트리 (일반 트리, 이진 트리)

\- 그래프 (무방향 그래프)


****알고리즘****

\- 정렬 (버블, 선택, 삽입, 병합, 힙)

\- 재귀 알고리즘

\- 선형탐색 / 이분탐색 / 해쉬법

\- BFS/DFS

\- Dynamic Programming (동적계획법)


### **더 공부해야 하는 개념들**

******자료구조******

\- 순차 리스트

\- 연결 리스트 (단순연결리스트, 이중, 원형)

\- 덱

\- 그래프 (방향그래프)


****알고리즘****

\- 그리디

\- 정렬(퀵)

\+ 추가 예정 ...!