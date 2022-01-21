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
	if first >= last: return  # 정렬할 값이 없음 -> 종료
	
	p = A[first] # pivot
	left, right = first + 1, last
	
	while left <= right: # 비교할 항목이 존재하는 동안
		while left <= last and A[left] < p: # p보다 큰 값을 만날 때까지
			left += 1 # 오른쪽으로 한 칸씩 이동
		while A[right] > p: # p보다 작은 값을 만날 때까지
			right -= 1 # 왼쪽으로 한 칸씩 이동
		
		#현재 left는 pivot보다 큰 값, right는 pivot보다 작은 값임 (right < left)
		if left <= right: # left 위치가 right보다 왼쪽에 있으면
			A[left], A[right] = A[right], A[left] # 자리 바꿈
			left += 1; right -= 1

	A[first], A[right] = A[right], A[first] # 마지막으로 pivot 값을 가운데로 이동
	quick_sort2(A, first, right-1) # 현재 right 위치에 pivot값이 들어있음 -> pivot보다 작은 값들에 대하여 재귀호출
	quick_sort2(A, right+1, last) # pivot보다 큰 값에 대하여 재귀호출
```

<br/>
<br/>

### Merge sort 알고리즘

---

- pivot에 의존하지 않고 강제로 배열을 반반씩 나누자!
- 각각 재귀적으로 정렬(sorting)하고 최종적으로 하나의 배열로 병합(merge)
- not in-place 알고리즘 : 주어진 배열과 같은 크기의 새로운 배열(추가 메모리)을 사용

```python
def merge_sort(A, first, last):
	"""A[first]부터 A[last]까지 정렬"""
	if first >= last: return # 정렬할 값이 없음 -> 종료
	mid = (first + last) // 2 # 중간값
	# 중간값을 기준으로 반씩 나눠서 각각 재귀호출
	merge_sort(A, first, mid)
	merge_sort(A, mid+1, last)
	
	B = [] # A와 크기가 같은 새로운 리스트
	i, j = first, mid+1 # 반으로 나눈 두 리스트의 시작 인덱스
	while i <= mid and j <= last: # 처음부터 끝까지 하나씩 비교
		if A[i] < A[j]: B.append(A[i]); i += 1
		else: B.append(A[j]); j += 1
	
	# 비교하고 남은 값들 한꺼번에 append (두 for문 중 값이 남아있는 하나만 돌아감)
	for i in range(i, mid+1): B.append(A[i])
	for j in range(j, last+1): B.append(A[j])

	# 최종적으로 정렬된 B의 값들을 A로 옮겨줌 (A를 정렬하는 문제이기 때문에)
	for k in range(first, last+1): # 처음부터 끝까지
		A[k] = B[k-first] # B의 값을 A로 복사	(first의 값이 0이 아닐 수 있기 때문에 인덱스 조정이 필요함)
```
<br/>

- T(n) = 2T(n/2) + cn (두 배열을 하나로 합치는 과정 = 모든 값을 한번씩 비교+다른 배열로 이동)
- 위 수행시간은 worst/average/best 상관없이 Quick sort의 best case와 같다 (무조건 절반으로 나누기 때문에) = O(n*log n)
- 가장 완전한 형태의 정렬 알고리즘 (가장 빠르고 이상적인 수행시간)

<br/>
<br/>

### Tim 정렬

---

- 파이썬에서의 sort 함수..!!! 효율성이 검증되면서 Java, JavaScript 등에서도 사용됨
- **insertion sort와 merge sort를 결합**한 하이브리드 sorting 알고리즘. 비교횟수와 이동/교환 횟수를 최소화하고자 한 형태이다.
- 정렬해야 할 배열의 값들 중 **이미 정렬된 상태인 일부**를 활용해서 더 빠른 시간 내에 정렬하려는 알고리즘이다.

