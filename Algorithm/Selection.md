# 선택(selection) 문제

- 입력: n개의 값과 k값(1 ≤ k ≤ n)
- 출력: k번째로 작은 입력 값
- 목표: 비교 횟수의 최소화 (upper bound를 낮추기)

- 항상 n번 이하의 비교로 충분히 문제 해결 가능한 경우 → 비교 횟수 n = 상한(upper bound)
- 반드시 최소한 n번 이상의 비교가 필요한 경우 → 비교 횟수 n = 하한(lower bound)

<br/>
<br/>

## Quick select 알고리즘

- 구현방법

  1. 기준값 p(pivot)를 고른다 (random or 첫 번째 항목 or 마지막 항목 ...)
  2. p보다 작은 값들(A)과 p보다 큰 값들(B), p와 같은 값들(M)을 각각 비교해서 구분(n-1번 비교)
  3. A에 들어있는 값의 개수가 k보다 크면 (if |A| > k: )

     k번째 값은 무조건 A안에 존재함! ⇒ A안에서 k번째로 작은 값을 찾아야 함(재귀적으로!)

  4. A값의 개수 + M값의 개수가 k 보다 작다면 (elif |A| + |M| < k: )

     k번째 값은 무조건 B안에 존재함! ⇒ B안에서 (k - |A| - |M|)번째 값을 찾아야 함

  5. k가 M에 존재한다면 (else: )

     k번째 값은 p와 같으므로 return p

<br/>

```python
def quick_select(L, k):
	"""리스트 L에서 정수 k번째 값을 찾아서 리턴하는 함수"""
	p = L[0]                  # pivot = 첫번째 항목으로 설정

	A, B, M = [], [], []      # 각 값을 비교해서 저장할 리스트
	for x in L:               # 각각의 항목에 대해서
		if p > x: A.append(x)   # p보다 작은 값
    elif p < x: B.append(x) # p보다 큰 값
		else: M.append(x)       # p와 같은 값

	if len(A) >= k: return quick_select(A, k)
	elif len(A) + len(M) < k: return quick_select(B, k-len(A)-len(M))
	else: return p
```

- worst case : 값이 A 또는 B쪽으로 몰리는 경우 (p가 최대 or 최솟값) → 재귀 호출이 n-1번 필요

      비교 횟수 T(n) = T(n-1) + n = (T(n-2) + n-1) + n = ... = T(1) + (2+3+4+... + n-1 + n) = O(n^2)

- best case: A와 B가 비슷한 크기로 나눠지는 경우 → 재귀 호출 횟수의 최소화

      비교 횟수 T(n) = T(n/2) + n = (T(n^2^2) + n/2) + n = ... = T(1) + n(1/2^(k-1) + .. + 1/2 + 1) = O(n)

- average case: O(n)

<br/>

### <참고> QuickSort 알고리즘

```python
def QuickSort(A):
	if len(A) <= 1: return A # 정렬 필요 없음
	S, M, L = [], [], []
	p = A[0] # pivot
	for a in A:
		if a < p: S.append(a)
		elif a > p: L.append(a)
		else: M.append(a)
	return QuickSort(S) + M + QuickSort(B)
```

<br/>
<br/>

## MoM (Median of Medians) 알고리즘

- Quick select 알고리즘의 문제점: pivot을 잘못 고르면 값들이 불균등하게 나눠져서 효율이 떨어진다! (worst case)
- MoM 알고리즘 = pivot을 신중하게 골라서 사용하는 선택 알고리즘

<br/>

- 좋은 pivot의 조건
  - A와 B에 들어있는 값의 개수가 각각 n/c개를 넘지 않아야 함 (c는 1 이상의 상수)
  - |A| ≤ n/c , |B| ≤ n/c
  - ⇒ A 또는 B를 재귀 호출 했을 때 n개에 대한 탐색이 아닌 n/c에 대한 비교탐색 문제로 줄어들기 때문 (n → n/c → n/c^2 → ... → n/c^k=1)
  - ⇒ 재귀 호출의 횟수가 log n만큼 발생
  - 한 번 호출할 때의 수행시간 = pivot을 고르는 시간 P + 모든 값과의 비교 시간 (n번 → n/c번 → ...)
  - 따라서 총 (P + n) * log n 정도의 시간이 걸림 ⇒ O(n*log n)
  - |A| ≤ n/c , |B| ≤ n/c의 조건을 만족한다면 O(n\*log n)의 시간을 보장!

<br/>

- 구현 방법
  1. 리스트 값들에 대해서 5개씩 그룹을 나눔 (총 n/5개의 그룹)
  2. 각 그룹의 중간값(median)을 구함 (5개의 항목에 대하여 6번 정도 비교하면 구할 수 있음 ⇒ 총 (n/5) \* 6번 비교)
  3. medians (= 각 그룹의 중간값들) 끼리 비교해서 그 중 중간값을 구함 (재귀, n/5개에 대한 비교 = T(n/5) = P)
  4. m\*(재귀적으로 구한 MoM = pivot)을 기준으로 모든 값 n번 비교
  5. k번째 항목이 A, M, B 중 어디에 있는지 판단 후 재귀호출(T(|A|) or T(|B|) 인데 이 둘은 최대 T(n/c)) 또는 return m\*
  - 결국 수행시간 T(n) = 6n/5 + T(n/5) + n + T(n/c) = T(n/c) + T(n/5) +11n/5

<br/>

- 상수 c값은?

  - 각 그룹의 중간값을 기준으로 리스트의 모든 값을 나열하여 m\*을 기준으로 4개의 그룹(X, Y, Z, W, 각각 최소 n/4개씩)으로 나눔
  - X에 들어있는 모든 값은 m\*보다 작음이 보장됨
  - W에 들어있는 모든 값은 m\*보다 큼이 보장됨
  - Y, Z는 모름

  - 따라서 n/4 ≤ |A| ≤ 3n/4 (=n/c), n/4 ≤ |B| ≤ 3n/4 (=n/c)
  - A와 B의 최대 항목 수가 3n/4이므로 c는 3/4의 역수인 4/3이다.
  - 그렇게 되면 |A|와 |B| 모두 전체 개수 n의 25% 이상 75% 이하임이 보장됨 (m\*을 pivot으로 사용하면 값들이 비교적 균등하게 나눠짐이 확인!)

<br/>

```python
def find_median_five(A):
  """정렬과정 없이 리스트 A의 중간값 리턴하는 함수"""
	if len(A) % 2 == 0: # 짝수 개
		while len(A) > 2:
			A.remove(max(A)); A.remove(min(A))
		return min(A)
	else: # 홀수 개
		while len(A) > 1:
			A.remove(max(A)); A.remove(min(A))
		return A[0]


def MoM(A, k):
  """리스트 A의 값 중에서 k번째로 작은 수 리턴하는 함수"""
	if len(A) == 1: # no more recursion
		return A[0]
	i = 0
	S, M, L, medians = [], [], [], []
	while i+4 < len(A):
		medians.append(find_median_five(A[i: i+5]))
		i += 5

	if i < len(A) and i+4 >= len(A): # 마지막 그룹으로 5개 미만의 값으로 구성
		medians.append(find_median_five(A[i:]))

	mom = MoM(medians, len(medians) // 2)
	for v in A:
		if v < mom:
			S.append(v)
		elif v > mom:
			L.append(v)
		else:
			M.append(v)

	if len(S) >= k : return MoM(S, k)
	elif len(S) + len(M) < k: return MoM(L, k-len(S)-len(M))
	else: return mom
```
