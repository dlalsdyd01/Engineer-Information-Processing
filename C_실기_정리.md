# C 실기 출제 유형 정리

정보처리기사 실기 C언어 문제 대비 핵심 정리입니다.

---

## 1. 기본 출력과 연산자

```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 3;
    printf("%d\n", a / b);   // 3 (정수 나누기 → 소수점 버림!)
    printf("%d\n", a % b);   // 1 (나머지)
    printf("%d번\n", a);     // "10번"
    return 0;
}
```

### 정수 vs 실수 나누기

| 코드 | 결과 | 이유 |
|------|------|------|
| `10 / 3` | 3 | 정수끼리 → 정수 |
| `10.0 / 3` | 3.333... | 실수가 섞이면 → 실수 |
| `(double)10 / 3` | 3.333... | 캐스팅하면 → 실수 |

### 증감 연산자 (매우 자주 출제!)

```c
int a = 5;
printf("%d\n", a++);  // 5 (먼저 출력, 그 다음 증가)
printf("%d\n", a);    // 6
printf("%d\n", ++a);  // 7 (먼저 증가, 그 다음 출력)
```

| 연산자 | 의미 | 핵심 |
|--------|------|------|
| `a++` | 후위 증가 | **쓰고** 나서 +1 |
| `++a` | 전위 증가 | +1 **하고** 나서 쓰기 |
| `a--` | 후위 감소 | **쓰고** 나서 -1 |
| `--a` | 전위 감소 | -1 **하고** 나서 쓰기 |

### 삼항 연산자

```c
int a = 5;
char *result = (a > 3) ? "크다" : "작다";
// "크다" (조건 ? 참일때 : 거짓일때)
```

---

## 2. 반복문 + 조건문

### for문
```c
int sum = 0;
for (int i = 1; i <= 10; i++) {
    if (i % 3 == 0)
        sum += i;
}
printf("%d\n", sum);  // 18
```

### while문
```c
int i = 1, sum = 0;
while (i <= 10) {
    sum += i;
    i++;
}
printf("%d\n", sum);  // 55
```

### do-while문 (최소 1번은 실행!)
```c
int i = 10;
do {
    printf("%d\n", i);  // 10 (한 번은 실행됨!)
    i++;
} while (i < 5);
```

### break / continue

| 키워드 | 의미 |
|--------|------|
| `break` | 반복문 **탈출** |
| `continue` | 다음 반복으로 **건너뛰기** |

---

## 3. 배열

### 1차원 배열
```c
int a[5] = {1, 2, 3, 4, 5};
printf("%d\n", a[0]);                // 1 (인덱스 0부터!)
printf("%lu\n", sizeof(a)/sizeof(a[0]));  // 5 (배열 길이 구하기)
```

### 2차원 배열
```c
int a[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
printf("%d\n", a[1][2]);  // 6 (2행 3열)

// 대각선 합
int sum = 0;
for (int i = 0; i < 3; i++) {
    sum += a[i][i];  // a[0][0] + a[1][1] + a[2][2]
}
printf("%d\n", sum);  // 15 (1+5+9)
```

### 배열 순회
```c
int a[] = {1, 2, 3, 4, 5};
int len = sizeof(a) / sizeof(a[0]);

for (int i = 0; i < len; i++) {
    printf("%d ", a[i]);
}
```

### 핵심
- 배열 인덱스는 **0부터** 시작
- 배열 길이 = `sizeof(배열) / sizeof(원소)`
- `a[i][j]` : [행][열]

---

## 4. 문자열 (char 배열)

```c
#include <string.h>

char s[] = "Hello World";
```

| 함수 | 결과 | 의미 |
|------|------|------|
| `strlen(s)` | 11 | 길이 (널문자 제외) |
| `s[0]` | 'H' | 특정 위치 문자 |
| `strcpy(dst, src)` | | 문자열 복사 |
| `strcat(dst, src)` | | 문자열 연결 |
| `strcmp(s1, s2)` | 0 / 양수 / 음수 | 내용 비교 (0이면 같음) |
| `strchr(s, 'W')` | "World" 포인터 | 문자 찾기 |
| `strstr(s, "World")` | "World" 포인터 | 부분 문자열 찾기 |

### 문자열 비교: == vs strcmp

```c
char a[] = "hello";
char b[] = "hello";

if (a == b) { /* 거의 false (주소 비교!) */ }
if (strcmp(a, b) == 0) { /* true (내용 비교!) */ }
```

### 핵심
- C의 문자열은 **char 배열 + 끝에 '\0' (널문자)**
- 문자열 비교는 반드시 **`strcmp()`**
- `==`는 주소(포인터) 비교
- `<string.h>` 헤더 필수

---

## 5. 형변환 (캐스팅)

### 자동 형변환 (작은 → 큰)
```c
int a = 10;
double b = a;  // 10.0 (자동 변환)
```

### 강제 형변환 (큰 → 작은)
```c
double a = 3.14;
int b = (int) a;  // 3 (소수점 버림!)
```

### 문자와 숫자 변환
```c
char c = 'A';
int n = c;             // 65 (아스키코드)
char c2 = (char) 66;   // 'B'
```

### 주요 아스키코드

| 문자 | 코드 | 기억법 |
|------|------|--------|
| `'0'` | 48 | |
| `'A'` | 65 | |
| `'a'` | 97 | A + 32 |

### 문자열 ↔ 숫자 변환
```c
#include <stdlib.h>

char s[] = "123";
int n = atoi(s);         // 123 (문자열 → 정수)

char buf[20];
sprintf(buf, "%d", n);   // "123" (정수 → 문자열)
```

---

## 6. 구조체 (struct)

### 기본 구조
```c
struct Car {
    char name[20];
    int speed;
};

int main() {
    struct Car c = {"BMW", 200};
    printf("%s %d\n", c.name, c.speed);  // BMW 200
    return 0;
}
```

### typedef로 간단하게
```c
typedef struct {
    char name[20];
    int speed;
} Car;

Car c = {"BMW", 200};
c.speed = 250;   // 멤버 접근: . 사용
```

### 구조체 포인터
```c
Car c = {"BMW", 200};
Car *p = &c;

printf("%s\n", p->name);   // 포인터로는 -> 사용
printf("%d\n", (*p).speed); // 동일 (역참조 후 .)
```

### 핵심
- **`.`** : 구조체 변수로 접근
- **`->`** : 구조체 포인터로 접근 (`(*p).멤버`와 동일)

---

## 7. 포인터 (매우 중요!)

### 기본
```c
int a = 10;
int *p = &a;   // a의 주소를 p에 저장

printf("%d\n", a);    // 10 (값)
printf("%p\n", &a);   // 주소
printf("%p\n", p);    // 같은 주소
printf("%d\n", *p);   // 10 (역참조: 주소가 가리키는 값)
```

### 포인터 연산자

| 연산자 | 의미 |
|--------|------|
| `&a` | a의 **주소** |
| `*p` | p가 가리키는 **값** (역참조) |
| `p->m` | p가 가리키는 구조체의 멤버 m |

### Call by Value vs Call by Reference (자주 출제!)

```c
void swap(int a, int b) {    // 값 전달 (복사)
    int t = a; a = b; b = t;
}

void swap2(int *a, int *b) { // 주소 전달
    int t = *a; *a = *b; *b = t;
}

int main() {
    int x = 1, y = 2;
    swap(x, y);   // 안 바뀜! (1, 2)
    swap2(&x, &y); // 바뀜! (2, 1)
}
```

### 배열과 포인터
```c
int a[] = {10, 20, 30};
int *p = a;       // a는 배열의 첫 주소

printf("%d\n", *p);      // 10
printf("%d\n", *(p+1));  // 20
printf("%d\n", p[2]);    // 30 (포인터도 [] 사용 가능)
```

### 핵심
- **C 함수 인자는 기본 값 전달** → 원본 안 바뀜
- 원본 바꾸려면 **주소(`&`) 전달** + 함수 안에서 **`*`** 로 접근
- 배열명은 **첫 원소의 주소**

---

## 8. 함수

### 기본 구조
```c
int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(3, 5);  // 8
    return 0;
}
```

### void (반환값 없음)
```c
void greet(char *name) {
    printf("Hello, %s\n", name);
}
```

### 재귀 함수
```c
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
// factorial(5) = 120
```

### 핵심
- **선언 → 정의 → 호출** 순서
- main 위에 함수 정의하거나, **함수 프로토타입** 선언 필요

---

## 9. 전역변수 vs 지역변수

```c
int g = 100;   // 전역변수 (모든 함수에서 접근 가능)

void func() {
    int l = 50;   // 지역변수 (func 안에서만)
    g++;          // 전역 변경 가능
}
```

### static 변수 (함수 호출 간 유지!)
```c
void count() {
    static int cnt = 0;  // 한 번만 초기화, 값 유지
    cnt++;
    printf("%d\n", cnt);
}
// count() 3번 호출 → 1, 2, 3 출력
```

### 핵심
- 지역변수: 함수 끝나면 사라짐
- **static 지역변수**: 프로그램 끝날 때까지 **값 유지**
- 전역변수: 어디서든 접근 가능

---

## 10. switch-case

```c
int a = 2;
switch (a) {
    case 1:
        printf("1\n");
        break;
    case 2:
        printf("2\n");
        // break 없음! → 아래로 떨어짐 (fall-through)
    case 3:
        printf("3\n");
        break;
    default:
        printf("기타\n");
}
// 출력:
// 2
// 3
```

### 핵심
- `break` 없으면 **다음 case로 떨어짐!** (fall-through, 매우 자주 출제!)
- `default` : 어디에도 해당 안 될 때
- switch에는 정수/문자만 가능 (문자열 불가)

---

## 11. 중첩 반복문

```c
// 구구단
for (int i = 2; i <= 9; i++) {
    for (int j = 1; j <= 9; j++) {
        printf("%d x %d = %d\n", i, j, i * j);
    }
}
```

### 별 찍기 (자주 출제!)
```c
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        printf("*");
    }
    printf("\n");
}
// *
// **
// ***
// ****
// *****
```

---

## 12. printf 서식 (C의 핵심!)

```c
int a = 95;
double b = 3.14159;
char s[] = "Kim";
char c = 'A';

printf("%d점\n", a);       // 95점
printf("%.2f\n", b);       // 3.14
printf("%s님\n", s);       // Kim님
printf("%c\n", c);         // A
printf("%5d\n", a);        //    95 (5자리, 오른쪽 정렬)
printf("%-5d끝\n", a);     // 95   끝 (왼쪽 정렬)
printf("%05d\n", a);       // 00095 (0으로 채움)
```

### 서식 기호

| 기호 | 의미 |
|------|------|
| `%d` | 정수 |
| `%f` | 실수 |
| `%.2f` | 소수점 2자리 |
| `%s` | 문자열 |
| `%c` | 문자 하나 |
| `%x` | 16진수 |
| `%o` | 8진수 |
| `%p` | 주소 |
| `%5d` | 5자리 (오른쪽 정렬) |
| `%-5d` | 5자리 (왼쪽 정렬) |
| `\n` | 줄바꿈 |
| `\t` | 탭 |

---

## 13. scanf (입력)

```c
int a;
scanf("%d", &a);   // 주소(&) 필요!

char s[100];
scanf("%s", s);    // 문자열은 배열명만 (배열명이 곧 주소)
```

### 핵심
- scanf는 **변수 주소(`&`) 전달**
- 문자열(char 배열)은 **`&` 없이** 배열명만

---

## 14. 비트 연산자

```c
int a = 5;  // 101
int b = 3;  // 011
```

| 연산자 | 의미 | 계산 | 결과 |
|--------|------|------|------|
| `a & b` | 둘 다 1이면 1 | 001 | 1 |
| `a \| b` | 하나라도 1이면 1 | 111 | 7 |
| `a ^ b` | 서로 다르면 1 | 110 | 6 |
| `~a` | 비트 반전 | | -6 |

### 비트 시프트

| 연산자 | 의미 | 쉽게 |
|--------|------|------|
| `<< 1` | 왼쪽으로 1칸 | **x 2** |
| `<< 2` | 왼쪽으로 2칸 | **x 4** |
| `>> 1` | 오른쪽으로 1칸 | **/ 2** |

### 핵심
- `~a` = **-(a+1)** (비트 반전 공식!)
- 계산은 2진수로, **답은 10진수로** 쓰기!

---

## 15. 자주 나오는 패턴

### 최댓값 찾기
```c
int a[] = {3, 7, 1, 9, 4};
int max = a[0];
for (int i = 1; i < 5; i++) {
    if (a[i] > max)
        max = a[i];
}
printf("%d\n", max);  // 9
```

### 배열 합계 / 평균
```c
int a[] = {10, 20, 30, 40, 50};
int sum = 0;
for (int i = 0; i < 5; i++) {
    sum += a[i];
}
printf("%d\n", sum);         // 150
printf("%d\n", sum / 5);     // 30 (정수 나누기!)
```

### 버블 정렬
```c
int a[] = {5, 3, 8, 1, 2};
int n = 5;
for (int i = 0; i < n - 1; i++) {
    for (int j = 0; j < n - 1 - i; j++) {
        if (a[j] > a[j + 1]) {
            int temp = a[j];
            a[j] = a[j + 1];
            a[j + 1] = temp;
        }
    }
}
// {1, 2, 3, 5, 8}
```

### 팩토리얼 (재귀)
```c
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
// factorial(5) = 120
```

### 피보나치 (재귀)
```c
int fib(int n) {
    if (n <= 2) return 1;
    return fib(n - 1) + fib(n - 2);
}
// fib(7) = 13
```

### 순위 매기기
```c
int arr[] = {77, 32, 10, 99, 50};
int result[5];
for (int i = 0; i < 5; i++) {
    result[i] = 1;
    for (int j = 0; j < 5; j++) {
        if (arr[i] < arr[j]) result[i]++;
    }
}
// result = {2, 4, 5, 1, 3}
```

---

## 16. 동적 메모리 할당

```c
#include <stdlib.h>

int *p = (int *) malloc(sizeof(int) * 5);  // 정수 5개 할당

p[0] = 10;
p[1] = 20;

free(p);   // 해제 필수!
```

### 핵심
- `malloc` : 메모리 할당
- `free` : 해제 (**안 하면 메모리 누수**)
- `sizeof(타입)` : 타입 크기
- `<stdlib.h>` 헤더 필요

---

## 17. 전처리기

```c
#include <stdio.h>       // 표준 라이브러리 포함
#include "myheader.h"    // 사용자 헤더

#define PI 3.14           // 상수 정의 (매크로)
#define SQUARE(x) ((x)*(x))  // 함수형 매크로

int main() {
    printf("%f\n", PI);         // 3.14
    printf("%d\n", SQUARE(5));  // 25
    return 0;
}
```

### 핵심
- `#include` : 헤더 파일 포함
- `#define` : 상수/매크로 정의 (**세미콜론 없음!**)
- 전처리기는 **컴파일 전**에 치환됨

---

## 18. 자주 나오는 함정

### ① swap은 값 전달이라 안 바뀜
```c
void swap(int a, int b) { int t=a; a=b; b=t; }
// → 원본 안 바뀜! (주소 전달해야 바뀜)
```

### ② switch의 break 빠뜨리기
```c
// fall-through 주의!
```

### ③ 정수 나누기는 소수점 버림
```c
int avg = 10 / 3;   // 3 (3.333이 아님!)
```

### ④ 문자열 비교는 strcmp
```c
if (s1 == s2) { ... }          // 주소 비교 (거의 false)
if (strcmp(s1, s2) == 0) { ... } // 내용 비교 ✅
```

### ⑤ scanf에 & 빼먹기
```c
int a;
scanf("%d", a);   // ❌ 런타임 에러
scanf("%d", &a);  // ✅
```

### ⑥ 배열 길이 구할 때 sizeof
```c
int a[10];
int len = sizeof(a) / sizeof(a[0]);  // 10
```

---

## 19. C vs Java 비교

| 항목 | C | Java |
|------|-----|------|
| 출력 | `printf("%d\n", a)` | `System.out.println(a)` |
| 입력 | `scanf("%d", &a)` | `Scanner sc = ...; sc.nextInt()` |
| 문자열 | `char s[]` / `char *s` | `String s` |
| 문자열 비교 | `strcmp(a, b) == 0` | `a.equals(b)` |
| 문자열 길이 | `strlen(s)` | `s.length()` |
| 배열 길이 | `sizeof(a)/sizeof(a[0])` | `a.length` |
| 객체 | 구조체 (`struct`) | 클래스 (`class`) |
| 멤버 접근 | `.` 또는 `->` (포인터) | `.` 만 |
| 메모리 해제 | `free()` 필수 | GC 자동 |
| 포인터 | **있음** (`*`, `&`) | 없음 (참조만) |
| null | `NULL` | `null` |
| 세미콜론 | **필수** (`;`) | **필수** (`;`) |

---

## 20. 헤더별 주요 함수

| 헤더 | 주요 함수 |
|------|---------|
| `<stdio.h>` | `printf`, `scanf`, `puts`, `gets` |
| `<string.h>` | `strlen`, `strcpy`, `strcat`, `strcmp`, `strstr` |
| `<stdlib.h>` | `malloc`, `free`, `atoi`, `atof`, `rand`, `exit` |
| `<math.h>` | `sqrt`, `pow`, `abs`, `floor`, `ceil` |
| `<ctype.h>` | `isdigit`, `isalpha`, `toupper`, `tolower` |

