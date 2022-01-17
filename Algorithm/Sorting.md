### 정렬 문제

---

- 목표 : 배열에 저장된 값들을 오름차순으로 재배열하는 문제 (비교, 교환 횟수 최소화)

- 성질
  - **stable** vs. unstable (안정성) ⇒ 같은 값들의 순서가 정렬 후에도 변하지 않는 것
  - **in-place** vs. not in-place ⇒ 정렬 시 O(1) 정도의 추가 메모리만 사용하는 것 (변수, 배열 등)

<br/>

### 기본 정렬 알고리즘

---

- Selection, Insertion, Bubble 알고리즘

- 장점: 구현이 쉽고 간단함

- 단점: O(n^2)에 작동하는 느린 알고리즘

```python
def selection_sort(A):
    n = len(A)
    for i in range(n-1): # 총 n-1번의 round
        # (각 round마다 최소 or 최댓값 탐색 + 자리바꿈)
        least = i
        for j in range(i+1, n):
            if A[j] < A[least]:
                least = j
        A[i], A[least] = A[least], A[i] # 순서 바꿈
```

```python
def insertion_sort(A):
    n = len(A)
    for i in range (1, n): # 0번 인덱스는 정렬되어 있다고 가정
        key = A[i] # 삽입할 항목
        j = i - 1 # 바로 앞에 있는 항목(비교 시작)
        while j >= 0 and A[j] > key: # 음수 인덱스 전까지 비교(0까지)
            A[j + 1] = A[j] # 하나 뒤로 이동
            j -= 1 # 비교 대상 앞으로 이동
        A[j + 1] = key # 삽입할 항목 재할당
```

```python
def bubble_sort(A):
    n = len(A)
    for i in range(n-1, 0, -1): # 각 round마다 비교 범위가 줄어듦 (맨 뒤 정렬된 부분 제외)
        bChanged = False # 값이 자리이동했는지 여부

        for j in range(i):
            if A[j] > A[j+1]: # 인접한 값과 비교, 더 크면
                A[j], A[j+1] = A[j+1], A[j] # 자리이동
                bChanged = True # 한 번 이상 자리이동 함

        if not bChanged: break # 한번도 자리이동 안했으면 => 이미 정렬 완료됨
```
