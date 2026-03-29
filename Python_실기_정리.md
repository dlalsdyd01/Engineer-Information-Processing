# Python 실기 출제 유형 정리

정보처리기사 실기 파이썬 문제 대비 핵심 정리입니다.

---

## 1. 반복문 + 조건문

```python
a = 0
for i in range(1, 11):
    if i % 3 == 0:
        a += i
print(a)  # 18
```

- `range(1, 11)` : 1부터 10까지 (11은 포함 안 됨)
- `range(3)` : 0, 1, 2 (0부터 시작!)
- `%` : 나머지 연산자
- `+=` : 누적 더하기 (`a = a + i`)

### 주의사항
- `range(1, 11)`에서 **11은 포함 안 됨**
- **0은 짝수!** (`0 % 2 == 0`은 True)

---

## 2. 리스트 슬라이싱

```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(a[2:8:2])  # [3, 5, 7]
```

### 슬라이싱 문법: `a[시작:끝:간격]`

| 예시 | 의미 | 결과 |
|------|------|------|
| `a[1:4]` | 인덱스 1~3 | [2, 3, 4] |
| `a[:3]` | 처음~2 | [1, 2, 3] |
| `a[3:]` | 3~끝 | [4, 5, 6, 7, 8, 9] |
| `a[::-1]` | 전체 뒤집기 | [9, 8, 7, 6, 5, 4, 3, 2, 1] |
| `a[:-1]` | 마지막 빼고 | [1, 2, 3, 4, 5, 6, 7, 8] |
| `a[4:1:-1]` | 4에서 2까지 거꾸로 | [5, 4, 3] |

### 핵심
- 끝 값은 **항상 포함 안 됨**
- `a[:]` : 리스트 **복사** (서로 독립)
- 슬라이싱 → **리스트**, 인덱싱 → **값 하나** (`a[:1]` = [1], `a[0]` = 1)

---

## 3. 함수와 변수 범위

### global 있을 때
```python
x = 10
def func():
    global x
    x = 20
func()
print(x)  # 20 (바깥 x가 바뀜)
```

### global 없을 때
```python
x = 10
def func():
    x = 20
func()
print(x)  # 10 (바깥 x 그대로)
```

### 기본값 매개변수
```python
def func(a, b=5):
    return a * b

print(func(3))     # 15 (b는 기본값 5)
print(func(3, 2))  # 6  (b에 2를 넣음)
```

### *args (가변 인자)
```python
def func(*args):
    return sum(args)

print(func(1, 2, 3))  # 6 (몇 개든 다 받음)
```

---

## 4. 딕셔너리

```python
d = {'a': 1, 'b': 2, 'c': 3}
```

### 기본 조작

| 코드 | 의미 |
|------|------|
| `d['a'] = 5` | 값 수정 |
| `d['d'] = 4` | 새로운 키 추가 |
| `del d['b']` | 키 삭제 |
| `d.get('x', 0)` | 키가 없으면 0 반환 (에러 안 남) |
| `d.keys()` | 키만 꺼내기 |
| `d.values()` | 값만 꺼내기 |
| `d.items()` | 키+값 같이 꺼내기 |
| `d.update(d2)` | 합치기 (같은 키는 덮어쓰기) |

### dict + zip
```python
d = dict(zip(['a', 'b', 'c'], [1, 2, 3]))
# {'a': 1, 'b': 2, 'c': 3}
```

---

## 5. 재귀 함수

### 팩토리얼
```python
def func(n):
    if n <= 1:
        return 1
    return n * func(n - 1)

print(func(5))  # 120 (5! = 5*4*3*2*1)
```

### 피보나치
```python
def fib(n):
    if n <= 2:
        return 1
    return fib(n-1) + fib(n-2)

print(fib(7))  # 13
```

### 풀이 방법
1. 펼치기 (위에서 아래로)
2. 멈추는 곳 찾기 (if문)
3. 거꾸로 올라가기

---

## 6. 문자열 처리

```python
s = "Hello World"
```

| 코드 | 결과 | 의미 |
|------|------|------|
| `s.upper()` | "HELLO WORLD" | 대문자로 |
| `s.lower()` | "hello world" | 소문자로 |
| `s.replace("World", "Python")` | "Hello Python" | 교체 |
| `s.split()` | ["Hello", "World"] | 쪼개기 (리스트로!) |
| `s.find("World")` | 6 | 위치 찾기 |
| `s.count("l")` | 3 | 개수 세기 |
| `s[::-1]` | "dlroW olleH" | 뒤집기 |
| `s.capitalize()` | "Hello world" | 첫 글자만 대문자 |
| `len(s)` | 11 | 길이 |

### split과 join은 반대
```python
"a,b,c".split(",")      # ['a', 'b', 'c']  (문자열 → 리스트)
",".join(['a', 'b', 'c']) # "a,b,c"          (리스트 → 문자열)
```

---

## 7. 리스트 컴프리헨션

### 읽는 순서: 반복 → 조건 → 결과
```python
a = [i * 2 for i in range(1, 6) if i % 2 == 1]
#    ③결과    ①반복              ②조건
# [2, 6, 10]
```

### if만 있으면 → 골라내기
```python
[i for i in a if i > 3]  # 조건에 맞는 것만
```

### if~else 있으면 → 전부 포함, 다르게 처리
```python
[x * 2 if x % 2 == 0 else x for x in a]
```

### 2차원 리스트에서 꺼내기
```python
a = [["kim", 80], ["lee", 90], ["park", 70]]
b = [x[0] for x in a if x[1] >= 80]
# ['kim', 'lee']
```

---

## 8. 클래스와 상속

### 기본 구조
```python
class Car:
    def __init__(self, name, speed):
        self.name = name
        self.speed = speed

    def info(self):
        print(self.name, self.speed)

a = Car("BMW", 200)
a.info()  # BMW 200
```

### 상속과 오버라이딩
```python
class Parent:
    def func(self):
        print("Parent")

class Child(Parent):
    def func(self):
        print("Child")

c = Child()
c.func()  # Child (자식 것이 우선!)
```

### super()
```python
class B(A):
    def __init__(self):
        super().__init__()  # 부모의 __init__ 호출
```

### 클래스 변수 (공유)
```python
class Counter:
    count = 0
    def __init__(self):
        Counter.count += 1

a = Counter()
b = Counter()
c = Counter()
print(Counter.count)  # 3
```

### 핵심
- `__init__` : 객체 만들 때 자동 실행
- `self` : 자기 자신
- 점(.) : "의" 라고 읽기 (`d.name` = d의 이름)
- 자식에 같은 함수가 있으면 → 자식 것 (오버라이딩)
- 없으면 → 부모 것

---

## 9. 람다 / map / filter

### 람다 = 한 줄 함수
```python
f = lambda x, y: x * y + 1
print(f(3, 4))  # 13
```

### map = 각 요소에 함수 적용 (변환)
```python
list(map(lambda x: x * 2, [1, 2, 3]))
# [2, 4, 6]
```

### filter = 조건에 맞는 것만 골라내기
```python
list(filter(lambda x: x % 2 == 0, [1, 2, 3, 4, 5]))
# [2, 4]
```

### map vs filter
| 함수 | 의미 | 개수 |
|------|------|------|
| `map` | 전부 **변환** | 원래와 같음 |
| `filter` | 조건에 맞는 것만 **골라내기** | 줄어듦 |

### 주의: 리스트 * 2 vs map
```python
[1, 2, 3] * 2                           # [1, 2, 3, 1, 2, 3] (반복!)
list(map(lambda x: x * 2, [1, 2, 3]))   # [2, 4, 6] (각각 계산!)
```

---

## 10. 중첩 반복문

```python
result = 0
for i in range(1, 4):
    for j in range(1, 4):
        if i == j:
            result += i
print(result)  # 6 (1+2+3)
```

### 2차원 리스트 대각선
```python
a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
result = 0
for i in range(3):
    result += a[i][i]    # 대각선: a[0][0], a[1][1], a[2][2]
print(result)  # 15 (1+5+9)
```

### a[i][j] = [행][열]
- 첫 번째 = 행 (세로)
- 두 번째 = 열 (가로)

---

## 11. while / break / continue

### while
```python
i = 0
while i < 5:     # 조건이 참인 동안 반복
    print(i)
    i += 1
```

### break = 반복문 완전히 멈추기
```python
while True:
    if i == 3:
        break     # 멈춤!
```

### continue = 건너뛰고 다음 반복으로
```python
for i in range(5):
    if i == 2:
        continue  # 2만 건너뜀
    print(i)      # 0 1 3 4
```

| 키워드 | 의미 |
|--------|------|
| `break` | 반복문 **탈출** |
| `continue` | 다음 반복으로 **건너뛰기** |
| `pass` | **아무것도 안 함** (자리 채우기용) |

---

## 12. try-except (예외 처리)

```python
try:
    a = 10 / 0        # 에러 발생!
    print("성공")      # 실행 안 됨
except:
    print("에러")      # 에러나면 여기로
finally:
    print("끝")        # 무조건 실행
```

### 주요 에러
| 에러 | 원인 |
|------|------|
| `ZeroDivisionError` | 0으로 나누기 |
| `IndexError` | 리스트 범위 초과 |
| `KeyError` | 딕셔너리 키 없음 |
| `ValueError` | 값 변환 실패 (`int("hello")`) |

### 핵심
- `try` : 먼저 해봐
- `except` : 에러나면 이거 해
- `finally` : 에러든 아니든 **무조건 실행**

---

## 13. set (집합)

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
```

| 연산자 | 의미 | 결과 |
|--------|------|------|
| `a & b` | 교집합 (둘 다 있는 것) | {3, 4} |
| `a \| b` | 합집합 (전부 합치기) | {1, 2, 3, 4, 5, 6} |
| `a - b` | 차집합 (a에만 있는 것) | {1, 2} |
| `a ^ b` | 대칭차집합 (한쪽에만 있는 것) | {1, 2, 5, 6} |

### 집합 메서드
| 코드 | 의미 |
|------|------|
| `a.add(5)` | 추가 |
| `a.remove(3)` | 삭제 |
| `a.update({6, 7})` | 합집합 |

### 핵심
- 집합은 **중복 없음, 순서 없음**
- `sorted(set(a))` → 중복 제거 후 **리스트로** 정렬

---

## 14. 비트 연산자

### 숫자에 쓰면 비트 연산, 집합에 쓰면 집합 연산!

```python
a = 5   # 101
b = 3   # 011
```

| 연산자 | 의미 | 계산 | 결과 |
|--------|------|------|------|
| `a & b` | 둘 다 1이면 1 | 001 | 1 |
| `a \| b` | 하나라도 1이면 1 | 111 | 7 |
| `a ^ b` | 서로 다르면 1 | 110 | 6 |

### 비트 시프트

| 연산자 | 의미 | 쉽게 |
|--------|------|------|
| `<< 1` | 왼쪽으로 1칸 | **x 2** |
| `<< 2` | 왼쪽으로 2칸 | **x 4** |
| `>> 1` | 오른쪽으로 1칸 | **/ 2** |

### 핵심
- 계산은 2진수로, **답은 10진수로** 쓰기!
- `>> 1` = 나누기 2 (소수점 버림)

---

## 15. print 서식

### 세 가지 방식
```python
name = "Kim"
age = 25

# f-string (가장 많이 출제)
print(f"{name}은 {age}살")

# format
print("{}점".format(95.5))

# % 서식
print("%s의 나이는 %d" % (name, age))
```

### % 기호
| 기호 | 의미 |
|------|------|
| `%s` | 문자열 |
| `%d` | 정수 |
| `%f` | 실수 |
| `%.2f` | 소수점 2자리 |

### print 구분자
| 코드 | 결과 |
|------|------|
| `print(a, b)` | 공백으로 구분 |
| `print(a, end=" ")` | 줄바꿈 대신 공백 |
| `print(a, end="")` | 붙여서 출력 |

---

## 16. enumerate / zip

### enumerate = 번호 매기기
```python
a = ["apple", "banana", "cherry"]
for i, v in enumerate(a):
    print(i, v)
# 0 apple
# 1 banana
# 2 cherry

# 1번부터 시작
for i, v in enumerate(a, 1):
    # i = 1, 2, 3
```

### zip = 짝짓기
```python
a = ["kim", "lee"]
b = [90, 80]
for name, score in zip(a, b):
    print(name, score)
# kim 90
# lee 80

# 딕셔너리로 만들기
d = dict(zip(a, b))  # {"kim": 90, "lee": 80}
```

---

## 17. 리스트 메서드

| 코드 | 의미 |
|------|------|
| `a.append(5)` | 맨 뒤에 추가 |
| `a.insert(2, 10)` | 인덱스 2에 끼워넣기 |
| `a.pop()` | 맨 뒤에서 빼기 (값 반환) |
| `a.pop(0)` | 인덱스 0에서 빼기 |
| `a.remove(3)` | 값 3 삭제 |
| `a.sort()` | 오름차순 정렬 |
| `a.sort(reverse=True)` | 내림차순 정렬 |
| `a.reverse()` | 뒤집기 |
| `sorted(a)` | 정렬 (원본 안 바뀜, 리스트 반환) |
| `list(reversed(a))` | 뒤집기 (원본 안 바뀜) |

### append vs insert
- `append(값)` : **맨 뒤**에 추가
- `insert(위치, 값)` : 그 위치에 **끼워넣기** (기존 값은 뒤로 밀림)

---

## 18. 자주 나오는 패턴

### 최댓값 찾기
```python
result = a[0]
for i in a:
    if i > result:
        result = i    # 더 큰 값으로 교체
```

### 최솟값 찾기
```python
result = a[0]
for i in a:
    if i < result:
        result = i    # 더 작은 값으로 교체
```

### 2진수 변환
```python
# % 2, // 2 가 같이 나오면 → 2진수 변환!
while n > 0:
    result = str(n % 2) + result
    n = n // 2
```

### 글자 수 세기
```python
d = {}
for c in "banana":
    d[c] = d.get(c, 0) + 1
# {'b': 1, 'a': 3, 'n': 2}
```

---

## 19. 시험 팁

1. 코드를 **위에서 아래로** 한 줄씩 따라가기
2. 재귀는 **노가다** - 펼치고 거꾸로 올라가기
3. `print`에 `end` 있는지 확인
4. 슬라이싱 끝 값은 **포함 안 됨**
5. **0은 짝수!**
6. `a[0]`은 값, `a[:1]`은 리스트
7. `split()`은 **리스트**로 만듦
8. `print(a, b)` → **공백**으로 구분
9. `global` 유무 확인
10. `append`는 추가, `=`은 덮어쓰기
