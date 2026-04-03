# Java 실기 출제 유형 정리

정보처리기사 실기 자바 문제 대비 핵심 정리입니다.

---

## 1. 기본 출력과 연산자

```java
public class Main {
    public static void main(String[] args) {
        int a = 10;
        int b = 3;
        System.out.println(a / b);   // 3 (정수 나누기 → 소수점 버림!)
        System.out.println(a % b);   // 1 (나머지)
        System.out.println(a + "번"); // "10번" (문자열 연결)
    }
}
```

### 정수 vs 실수 나누기

| 코드 | 결과 | 이유 |
|------|------|------|
| `10 / 3` | 3 | 정수끼리 → 정수 |
| `10.0 / 3` | 3.333... | 실수가 섞이면 → 실수 |
| `(double)10 / 3` | 3.333... | 캐스팅하면 → 실수 |

### 증감 연산자 (매우 자주 출제!)

```java
int a = 5;
System.out.println(a++);  // 5 (먼저 출력, 그 다음 증가)
System.out.println(a);    // 6
System.out.println(++a);  // 7 (먼저 증가, 그 다음 출력)
```

| 연산자 | 의미 | 핵심 |
|--------|------|------|
| `a++` | 후위 증가 | **쓰고** 나서 +1 |
| `++a` | 전위 증가 | +1 **하고** 나서 쓰기 |
| `a--` | 후위 감소 | **쓰고** 나서 -1 |
| `--a` | 전위 감소 | -1 **하고** 나서 쓰기 |

### 삼항 연산자

```java
int a = 5;
String result = (a > 3) ? "크다" : "작다";
// "크다" (조건 ? 참일때 : 거짓일때)
```

---

## 2. 반복문 + 조건문

### for문
```java
int sum = 0;
for (int i = 1; i <= 10; i++) {
    if (i % 3 == 0)
        sum += i;
}
System.out.println(sum);  // 18
```

### while문
```java
int i = 1, sum = 0;
while (i <= 10) {
    sum += i;
    i++;
}
System.out.println(sum);  // 55
```

### do-while문 (최소 1번은 실행!)
```java
int i = 10;
do {
    System.out.println(i);  // 10 (한 번은 실행됨!)
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
```java
int[] a = {1, 2, 3, 4, 5};
System.out.println(a[0]);      // 1 (인덱스 0부터!)
System.out.println(a.length);  // 5
```

### 2차원 배열
```java
int[][] a = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
System.out.println(a[1][2]);  // 6 (2행 3열)

// 대각선 합
int sum = 0;
for (int i = 0; i < 3; i++) {
    sum += a[i][i];  // a[0][0] + a[1][1] + a[2][2]
}
System.out.println(sum);  // 15 (1+5+9)
```

### 배열 순회
```java
// 일반 for
for (int i = 0; i < a.length; i++) {
    System.out.println(a[i]);
}

// 향상된 for (for-each)
for (int x : a) {
    System.out.println(x);
}
```

### 핵심
- 배열 인덱스는 **0부터** 시작
- `a.length` : 배열 길이 (괄호 없음!)
- `a[i][j]` : [행][열]

---

## 4. 문자열 (String)

```java
String s = "Hello World";
```

| 코드 | 결과 | 의미 |
|------|------|------|
| `s.length()` | 11 | 길이 (괄호 있음!) |
| `s.charAt(0)` | 'H' | 특정 위치 문자 |
| `s.substring(0, 5)` | "Hello" | 부분 문자열 (0~4) |
| `s.substring(6)` | "World" | 6번부터 끝까지 |
| `s.toUpperCase()` | "HELLO WORLD" | 대문자로 |
| `s.toLowerCase()` | "hello world" | 소문자로 |
| `s.replace("World", "Java")` | "Hello Java" | 교체 |
| `s.indexOf("World")` | 6 | 위치 찾기 |
| `s.contains("Hello")` | true | 포함 여부 |
| `s.equals("Hello World")` | true | 내용 비교 |
| `s.trim()` | 앞뒤 공백 제거 | |
| `s.split(" ")` | {"Hello", "World"} | 쪼개기 (배열로!) |

### 문자열 비교: == vs equals

```java
String a = new String("hello");
String b = new String("hello");

System.out.println(a == b);      // false (주소 비교!)
System.out.println(a.equals(b)); // true  (내용 비교!)
```

### 핵심
- 문자열 비교는 반드시 **`equals()`** 사용!
- `==`는 주소(참조)를 비교하므로 다를 수 있음
- `substring(시작, 끝)` : 끝은 **포함 안 됨** (파이썬 슬라이싱과 같음)

---

## 5. 형변환 (캐스팅)

### 자동 형변환 (작은 → 큰)
```java
int a = 10;
double b = a;  // 10.0 (자동으로 변환)
```

### 강제 형변환 (큰 → 작은)
```java
double a = 3.14;
int b = (int) a;  // 3 (소수점 버림!)
```

### 문자와 숫자 변환
```java
char c = 'A';
int n = c;           // 65 (아스키코드)
char c2 = (char) 66; // 'B'
```

### 주요 아스키코드

| 문자 | 코드 | 기억법 |
|------|------|--------|
| `'0'` | 48 | |
| `'A'` | 65 | |
| `'a'` | 97 | A + 32 |

### 문자열 ↔ 숫자 변환
```java
String s = "123";
int n = Integer.parseInt(s);   // 123 (문자열 → 정수)
String s2 = String.valueOf(n); // "123" (정수 → 문자열)
```

---

## 6. 클래스와 객체

### 기본 구조
```java
class Car {
    String name;
    int speed;

    Car(String name, int speed) {  // 생성자
        this.name = name;
        this.speed = speed;
    }

    void info() {
        System.out.println(name + " " + speed);
    }
}

public class Main {
    public static void main(String[] args) {
        Car c = new Car("BMW", 200);
        c.info();  // BMW 200
    }
}
```

### 핵심
- **생성자** : 클래스 이름과 같은 메서드, 객체 만들 때 자동 실행
- **this** : 자기 자신 (파이썬의 self와 같음)
- **new** : 객체 생성 키워드

---

## 7. 상속과 오버라이딩

### 상속
```java
class Parent {
    void func() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    void func() {  // 오버라이딩!
        System.out.println("Child");
    }
}

public class Main {
    public static void main(String[] args) {
        Child c = new Child();
        c.func();  // Child (자식 것이 우선!)
    }
}
```

### super
```java
class Child extends Parent {
    void func() {
        super.func();  // 부모의 func() 호출
        System.out.println("Child");
    }
}
// 출력:
// Parent
// Child
```

### 업캐스팅 (자주 출제!)
```java
Parent p = new Child();  // 부모 타입으로 자식 객체 생성
p.func();  // Child (오버라이딩된 메서드는 자식 것 실행!)
```

### 핵심
- `extends` : 상속 키워드
- 자식에 같은 메서드 있으면 → **자식 것** (오버라이딩)
- 없으면 → **부모 것**
- `super` : 부모를 가리킴
- 업캐스팅해도 오버라이딩된 메서드는 **자식 것** 실행

---

## 8. 오버로딩 vs 오버라이딩

### 오버로딩 (같은 이름, 다른 매개변수)
```java
class Calc {
    int add(int a, int b) {
        return a + b;
    }
    double add(double a, double b) {  // 오버로딩!
        return a + b;
    }
    int add(int a, int b, int c) {    // 오버로딩!
        return a + b + c;
    }
}
```

### 구분

| | 오버로딩 (Overloading) | 오버라이딩 (Overriding) |
|---|---|---|
| 의미 | 같은 이름, **다른 매개변수** | 같은 이름, **같은 매개변수** |
| 위치 | **같은 클래스** 안 | **부모-자식** 사이 |
| 목적 | 편의성 | 기능 재정의 |

---

## 9. 추상 클래스와 인터페이스

### 추상 클래스 (abstract)
```java
abstract class Animal {
    abstract void sound();  // 구현 없음! (자식이 반드시 구현)

    void breathe() {
        System.out.println("숨쉬기");  // 일반 메서드도 가능
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("멍멍");
    }
}
```

### 인터페이스 (interface)
```java
interface Flyable {
    void fly();  // 모든 메서드가 추상
}

class Bird implements Flyable {
    public void fly() {
        System.out.println("날다");
    }
}
```

### 구분

| | 추상 클래스 | 인터페이스 |
|---|---|---|
| 키워드 | `abstract class` | `interface` |
| 상속 | `extends` | `implements` |
| 일반 메서드 | 가능 | 불가 (Java 8 이전) |
| 다중 상속 | 불가 | **가능** |
| 변수 | 일반 변수 가능 | 상수만 가능 |

---

## 10. 접근 제어자

| 제어자 | 같은 클래스 | 같은 패키지 | 자식 클래스 | 전체 |
|--------|:-----------:|:-----------:|:-----------:|:----:|
| `public` | O | O | O | O |
| `protected` | O | O | O | X |
| `default` (없음) | O | O | X | X |
| `private` | O | X | X | X |

### 핵심
- `public` : 어디서든 접근 가능
- `private` : 같은 클래스에서만 접근 가능 (캡슐화!)
- 아무것도 안 쓰면 → `default` (같은 패키지까지만)

---

## 11. static

```java
class Counter {
    static int count = 0;  // 클래스 변수 (공유!)

    Counter() {
        count++;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter a = new Counter();
        Counter b = new Counter();
        Counter c = new Counter();
        System.out.println(Counter.count);  // 3
    }
}
```

### 핵심
- `static` 변수 : 모든 객체가 **공유** (하나만 존재)
- `static` 메서드 : 객체 없이 **클래스명.메서드()** 로 호출 가능
- `static` 메서드에서 일반 변수 사용 **불가**

---

## 12. 예외 처리

```java
try {
    int a = 10 / 0;          // 에러 발생!
    System.out.println("성공"); // 실행 안 됨
} catch (ArithmeticException e) {
    System.out.println("에러"); // 에러나면 여기로
} finally {
    System.out.println("끝");   // 무조건 실행
}
```

### 주요 예외

| 예외 | 원인 |
|------|------|
| `ArithmeticException` | 0으로 나누기 |
| `ArrayIndexOutOfBoundsException` | 배열 범위 초과 |
| `NullPointerException` | null 참조 |
| `ClassCastException` | 잘못된 형변환 |
| `NumberFormatException` | 숫자 변환 실패 |

### 핵심
- `try` : 먼저 해봐
- `catch` : 에러나면 이거 해
- `finally` : 에러든 아니든 **무조건 실행**
- 파이썬의 `try-except-finally`와 같은 구조

---

## 13. 중첩 반복문

```java
// 구구단
for (int i = 2; i <= 9; i++) {
    for (int j = 1; j <= 9; j++) {
        System.out.println(i + " x " + j + " = " + (i * j));
    }
}
```

### 별 찍기 (자주 출제!)
```java
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    System.out.println();
}
// *
// **
// ***
// ****
// *****
```

### print vs println

| 메서드 | 의미 |
|--------|------|
| `System.out.print()` | 줄바꿈 **없이** 출력 |
| `System.out.println()` | 출력 후 **줄바꿈** |
| `System.out.printf()` | **서식** 지정 출력 |

---

## 14. switch-case

```java
int a = 2;
switch (a) {
    case 1:
        System.out.println("1");
        break;
    case 2:
        System.out.println("2");
        // break 없음! → 아래로 떨어짐 (fall-through)
    case 3:
        System.out.println("3");
        break;
    default:
        System.out.println("기타");
}
// 출력:
// 2
// 3
```

### 핵심
- `break` 없으면 **다음 case로 떨어짐!** (fall-through, 매우 자주 출제!)
- `default` : 어디에도 해당 안 될 때

---

## 15. 생성자

### 기본 생성자
```java
class Dog {
    String name;

    Dog() {  // 기본 생성자
        this.name = "멍멍이";
    }

    Dog(String name) {  // 매개변수 있는 생성자
        this.name = name;
    }
}

Dog d1 = new Dog();        // name = "멍멍이"
Dog d2 = new Dog("바둑이"); // name = "바둑이"
```

### 생성자 체이닝
```java
class Person {
    String name;
    int age;

    Person() {
        this("홍길동", 20);  // 다른 생성자 호출
    }

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### 핵심
- 생성자 이름 = **클래스 이름**
- 반환 타입 **없음**
- `this()` : 같은 클래스의 다른 생성자 호출
- `super()` : 부모 클래스의 생성자 호출

---

## 16. 자주 나오는 패턴

### 최댓값 찾기
```java
int[] a = {3, 7, 1, 9, 4};
int max = a[0];
for (int i = 1; i < a.length; i++) {
    if (a[i] > max)
        max = a[i];
}
System.out.println(max);  // 9
```

### 배열 합계 / 평균
```java
int[] a = {10, 20, 30, 40, 50};
int sum = 0;
for (int x : a) {
    sum += x;
}
System.out.println(sum);              // 150
System.out.println(sum / a.length);   // 30 (정수 나누기!)
```

### 버블 정렬
```java
int[] a = {5, 3, 8, 1, 2};
for (int i = 0; i < a.length - 1; i++) {
    for (int j = 0; j < a.length - 1 - i; j++) {
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
```java
static int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
// factorial(5) = 120
```

### 피보나치 (재귀)
```java
static int fib(int n) {
    if (n <= 2) return 1;
    return fib(n - 1) + fib(n - 2);
}
// fib(7) = 13
```

---

## 17. printf 서식

```java
int a = 95;
double b = 3.14159;
String s = "Kim";

System.out.printf("%d점\n", a);       // 95점
System.out.printf("%.2f\n", b);       // 3.14
System.out.printf("%s님\n", s);       // Kim님
System.out.printf("%5d\n", a);        //    95 (5자리, 오른쪽 정렬)
System.out.printf("%-5d끝\n", a);     // 95   끝 (왼쪽 정렬)
```

### 서식 기호

| 기호 | 의미 |
|------|------|
| `%d` | 정수 |
| `%f` | 실수 |
| `%s` | 문자열 |
| `%c` | 문자 하나 |
| `%.2f` | 소수점 2자리 |
| `%5d` | 5자리 (오른쪽 정렬) |
| `\n` | 줄바꿈 |

---

## 18. 비트 연산자

```java
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
- 파이썬과 동일한 연산자

---

## 19. 컬렉션 (ArrayList)

```java
import java.util.ArrayList;

ArrayList<Integer> list = new ArrayList<>();
list.add(10);       // 추가
list.add(20);
list.add(30);
list.get(0);        // 10 (인덱스로 접근)
list.set(1, 25);    // 인덱스 1을 25로 변경
list.remove(0);     // 인덱스 0 삭제
list.size();        // 크기
list.contains(25);  // 포함 여부 → true
```

### 배열 vs ArrayList

| | 배열 | ArrayList |
|---|---|---|
| 크기 | **고정** | **가변** |
| 선언 | `int[] a = new int[5]` | `ArrayList<Integer> a = new ArrayList<>()` |
| 접근 | `a[0]` | `a.get(0)` |
| 길이 | `a.length` | `a.size()` |

---

## 20. Java vs Python 비교

| 항목 | Java | Python |
|------|------|--------|
| 출력 | `System.out.println()` | `print()` |
| 변수 선언 | `int a = 10;` | `a = 10` |
| 문자열 비교 | `s.equals("abc")` | `s == "abc"` |
| 배열/리스트 길이 | `a.length` / `list.size()` | `len(a)` |
| for-each | `for (int x : a)` | `for x in a:` |
| 상속 | `extends` | `class Child(Parent):` |
| 인터페이스 | `implements` | 없음 (덕타이핑) |
| 세미콜론 | **필수** (`;`) | 없음 |
| 중괄호 | **필수** (`{}`) | 들여쓰기로 구분 |
| null | `null` | `None` |
| 형변환 | `(int) 3.14` | `int(3.14)` |
| 논리 연산자 | `&&` `\|\|` `!` | `and` `or` `not` |

