# 재귀(Recursion)
- 함수 내부에서 자기 자신을 호출하는 방식으로 문제를 해결하는 방식
- 리턴되는 값을 가지고 계속 계산을 하면서 정답을 완성 = stack 메모리 사용
- 바닥조건(base case, 가장 기본이 되는 조건)일 경우 체크 → 수행 시간 = 상수시간 T(1)
- 재귀호출 → 수행 시간도 재귀적으로 정의 ⇒ n에 대한 점화식 전개 T(n)  

<br/>

### 예시

**1부터 n까지의 합 구하기**

- f(n) = 1 + 2 + 3 + 4 + 5 + 6 + ... + n = f(n-1) + n = f(n-2) + n-1 + n = ...

```python
def hap(n):
	if n == 1: return 1 # base case
return hap(n-1) + n
```

- 수행시간 T(n) = T(n-1) + c (1부터 n-1까지 더하는 데 걸리는 시간 + 상수 번의 기본 연산)
- = (T(n-2) + c) + c = T(n-2) + 2c = ... = T(n-(n-1)) + (n-1)c = T(1) + (n-1)c (T(1)은 상수시간 = c)
- = c + (n-1)c = c*n 따라서 T(n) = cn = O(n) n번의 덧셈과 같다  

<br/>

**a부터 b까지의 합 구하기 (a ≤ b)**

- h(3, 8) = (3 + 4 + 5) + (6 + 7 + 8) = h(3, 5) + h(6, 8) = ...

```python
def sum(a, b):
	if a == b: return a # 두 수가 같다면 자기 자신 호출
  if a > b: return 0  # 합이 존재하지 않으므로 0을 호출
	mid = (a+b) // 2    # 중간값 구하기
	return sum(a, mid) + sum(mid+1, b)
```
- 두 번의 재귀 호출로 이루어진 연산
- 수행시간 T(n) = T(n/2) + T(n/2) + c (절반 호출 + 절반 호출 + 더하기 연산) = 2T(n/2) + c
- n을 2의 제곱수라고 가정 (n = 2^k),  T(1) = c (상수시간)
- T(n) = 2T(n/2) + c = 2(2(T(n/2^2)) + c) + c = 2^2T(n/2^2) + 2c + c = 2^2T(n/2^2) + c(1 + 2)
- = ... = 2^kT(n/2^k) + c(1 + 2 + 2^2 + ... + 2^(k-1)) = 2^k * c + c (등비수열 계산)   
                                                                        + 등비수열 합 계산방법 = a1 * (r^n- 1) / (r - 1)
- = c * 2^k + c * 2^k - c = 2c2^k - c = 2cn - c = c(2n-1)
- 따라서 T(n) = c(2n-1) = O(n)  

<br/>

**리스트 값을 역순으로 재 배치하기**

1. method 1

```python
def reverse(A):
	if len(A) == 1: return A # 항목이 하나이면 그대로 리턴
	reverse(A[1:]) + A[:1]
```

- T(n) = T(n-1) + c = O(n)

2. method 2

```python
def reverse(A, start, stop):
	"""리스트 A에서 start부터 stop - 1까지의 항목 재배치"""
	if start < stop - 1: # 항목이 2개 이상일 경우에만
		A[start], A[stop - 1] = A[stop - 1], A[start]
		reverse(A, start + 1, stop - 1) # 범위를 줄여가면서 재귀 호출 
```

- T(n) = T(n-2) + c = T(n-4) + c + c = ... (항목이 두 개씩 줄어듦)
- = T(1) + c * (n/2) = O(n)
