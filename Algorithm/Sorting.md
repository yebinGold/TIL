### 정렬 문제

---

- 목표 : 배열에 저장된 값들을 오름차순으로 재배열하는 문제 (비교, 교환 횟수 최소화)

- 성질
  - **stable** vs. unstable (안정성) ⇒ 같은 값들의 순서가 정렬 후에도 변하지 않는 것
  - **in-place** vs. not in-place ⇒ 정렬 시 O(1) 정도의 추가 메모리만 사용하는 것 (변수, 배열 등)

<br/>
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

<br/>
<br/>

### Quick sort 알고리즘

---

- 가장 유명한 알고리즘 중 하나

- 최악의 경우 O(n^2)로 꽤 느리지만, 실제로 동작해보면 가장 빠름

- Quick select와 유사함 (pivot을 기준으로 세 개의 배열로 나눠서 각각 정렬)

<br/>

```python
def quick_sort(A):
	if len(A) < 2: return A # 정렬할 게 없음

	p = A[0] # pivot
	S, M , L = [], [], []
	for x in A:
		if x < p: x.append(S)
		elif x > p: x.append(L)
		else: x.append(M)

	return quick_sort(S) + M + quick_sort(L) # 정렬된 리스트를 하나로 리턴
```

<br/>

- stable한 알고리즘 = 주어진 순서대로 비교해서 append하기 때문에 순서 바뀌지 않음
- not in-place 알고리즘 = n개의 항목을 각각 copy해서 새로운 배열에 저장 (입력 크기 O(n)에 비례하는 추가 메모리를 사용)

<br/>

- T(n) = T(|S|) + T(|L|) + cn (A 나눌 때 n-1번 비교)
- S와 L이 어떻게 나뉘냐에 따라 수행 시간이 달라짐
  - worst case: S와 L 중 하나에만 값이 몰리는 경우 (이미 정렬된 경우)
    - ⇒ T(n) = T(n-1) + cn = O(n^2)
  - best case: S와 L이 균등하게 나눠지는 경우
    - ⇒ T(n) = T(n/2) + T(n/2) + cn = 2T(n/2) + cn = O(n\*log n)
  - 하지만 worst case와 같은 경우의 입력은 자주 일어나지 않는다.
  - 평균(average case) = O(n\*log n) 으로 굉장히 빠름

<br/>
<br/>

### in-place Quick sort 알고리즘

---

- 새로운 리스트를 (S, M, L) 사용하지 않고, 주어진 리스트 A의 범위를 이용하는 알고리즘
- A안에서 항목들을 재배치

<br/>

```python
def quick_sort2(A, first, last):
	"""A[first]부터 A[last]까지 정렬"""
	p = A[first] # pivot
	left = first + 1; right = last

	while left <= right: # 비교할 항목이 존재하는 동안
		while left <= last and A[left] < p: # p보다 큰 값을 만날 때까지
			left += 1 # 오른쪽으로 한 칸씩 이동
		while A[right] > p: # p보다 작은 값을 만날 때까지
			right -= 1 # 왼쪽으로 한 칸씩 이동

		if left <= right:
			A[left], A[right] = A[right], A[left] # 자리 바꿈
			left += 1; right -= 1

	A[first], A[right] = A[right], A[first] # 마지막으로 pivot 값을 가운데로 이동
```
