## 분할정복

- 큰 문제를 작은 문제로 분할해서 재귀적으로 해결

<br/>

### 예시

**a의 n승 구하기**

1. power1(a, n) = a \* power(a, n-1)

```python
def power1(a, n):
	if n == 1: return a
	else: return power(a, n-1) * a
```

- T(n) = T(n-1) + c , T(1) = c → O(n)

<br/>

2. power2(a, n) = power(a, n/2) \* power(a, n/2) (이 경우 n이 짝수 or 홀수에 따라 연산 달라짐)

```python
def power2(a, n):
	if n == 1: return a # a의 1승 = 자기 자신을 리턴
	if n == 0: return 1

	if n % 2 == 0: # 짝수이면
		return power2(a, n//2) * power2(a, n//2)
	else: # 홀수이면
		return power2(a, n//2) * power2(a, n//2) * a
```

- T(n) = 2\*T(n/2) + c, T(1) = c → O(n)

<br/>

3. 더 효율적인 방법: 재귀 호출은 하지만 그 횟수가 적어짐

```python
def power3(a, n):
	if n == 0: return 1
	x = power3(a, n//2) # 필요한 값을 미리 계산
	if n % 2 == 0: # 짝수이면
		return x * x
	else: # 홀수이면
		return x * x * a
```

- T(n) = T(n/2) + c, T(1) = c (n = 2^k) → O(log n)

      T(n) = T(n/2) + c

      = T(n/2^2) + c + c

      = T(n/2^(2^2)) + c + c + c

       ...

      = T(n/2^k) + k*c = T(1) + k*c = c + k*c = k(1 + c)

      이때 k = log 2의 n 이므로 T(n) = log n * (상수) = O(log n)

- 이때의 재귀 호출은 n에 대한 재귀 호출이 아닌 n의 절반에 대한 호출
- ✨어떤 재귀 호출이냐에 따라 수행 시간이 크게 달라진다!

<br/>

---

<br/>

### 피보나치 수

- 피보나치 수열: F(0) = 0, F(1) = 1, F(2) = 1, F(3) = 2, ... F(n) = F(n-1) + F(n-2)로 정의됨

<br/>

1. 피보나치의 정의를 그대로 재귀함수로 구현하는 방법

```python
def fibo_1(n):
	if n <= 1: return n
	return fibo_1(n-1) + fibo_1(n-2)
```

- 비효율적인 방법: 같은 내용의 재귀 호출이 반복됨 (값의 재사용 x)
- T(n) = T(n-1) + T(n-2) + c = O(g^n), g = golden ratio(황금률, 1.618...)
- ⇒ n이 커짐에 따라 수행 시간이 기하급수적으로 커짐(exponential time, 지수 시간)

<br/>

2. 세 변수만을 이용해서 n번째 수를 계산하는 방법

```python
def fibo_2(n):
	f1 = 0; f2 = 1 # F(0), F(1)은 미리 정의
	for i in range(2, n+1):
		f3 = f1 + f2
		f1 = f2
		f2 = f3
	return f2
```

- O(n)

<br/>

3. 배열에 0번째 피보나치 수부터 n번째 수까지 차례대로 채워나가는 방법

```python
def fibo_3(n):
	F = [0, 1] # F(0), F(1)은 미리 포함
	for i in range(2, n+1):
		F.append(F[i-1] + F[i - 2])
	return F[n]
```

- O(n)

<br/>

4. 행렬 곱셈식을 이용한 방법

- 앞서 봤던 power3(a, n) 방법 이용
- O(log n)

<br/>

---

<br/>

### 최대 구간 합 구하기

- prefix sum

```python
def max_sum(A):
	p = []
	for i in range(len(A)):
		p.append(sum(A[:i+1])) # A[0]부터 A[i]까지의 합 저장
	
	hap = -100 # 아무거나 초기화 (답이 음수일 수도 있음)
	for i in range(len(p)):
		for j in range(i, len(p)):
			if i == 0: hap = max(hap, p[j])
			else: hap = max(hap, p[j] - p[i-1])
	# 최대 구간 합 리턴
	return hap
```

<br/>

- 분할 정복

```python
def max_sum(A, left, right):
	if left == right: return A[left] # 둘 중 아무거나
	
	m = (left + right) // 2 # 중간값
	
	# 1. 최대 합이 왼쪽에 존재하는 경우 or 2. 오른쪽에 존재하는 경우
	result = max(max_sum(A, left, m), max_sum(A, m+1, right))
	
	# 3. 양쪽에 걸치는 경우 (최대 합 = 왼쪽 끝 + 오른쪽 시작부분의 합)
	l_hap = 0; l = -100; r_hap = 0; r = -100; # 초기화
	for i in range(m, 0, -1):
		l_hap += A[i] # A[m]부터 하나씩 더함
		l = max(l, l_hap) # A[m]에서 끝나는 왼쪽 최대구간
	
	for i in range(m+1, right+1):
		r_hap += A[i] # A[m+1]부터 하나씩 더함
		r = max(r, r_hap) # A[m+1]로 시작하는 오른쪽 최대구간
	both = l + r
	
	# A[left], ..., A[right] 중 최대 구간 합 리턴
	return max(result, both)
```
