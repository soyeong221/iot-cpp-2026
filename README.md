# iot-cpp-2026

# C++ 학습 내용 정리

## 2026.03.06 (금) - C++ 기본 문법과 함수 기초

### 프로그래밍 언어의 Schema

![alt text](image-2.png)

프로그램은 기본적으로 다음 흐름으로 생각할 수 있다.

```text
Input → Processing → Output
```

- **Input**: 사용자, 파일, 센서 등으로부터 데이터를 입력받는다.
- **Processing**: 연산, 조건 판단, 반복 등의 로직으로 데이터를 처리한다.
- **Output**: 처리 결과를 화면이나 파일 등에 출력한다.

예를 들어 두 숫자를 입력받아 큰 값을 출력하는 프로그램이라면,

```text
숫자 입력 → 두 값 비교 → 큰 값 출력
```

과 같은 흐름이 된다.

> 프로그램을 작성하기 전에 **무엇을 입력받고 → 어떻게 처리하고 → 무엇을 출력할지** 먼저 나누면 코드 구조를 잡기 쉽다.

--- 

## 변수와 자료형

### Variable(변수): [소스](./Day0306-Solution/basic/01_variable.cpp)

- 변수는 프로그램 실행 중 사용할 데이터를 저장하는 공간이다.
- 변수: 선언 + 초기화 -> 할당

```cpp
int age = 25;
double height = 165.5;
bool isStudent = true;
char grade = 'A';
```

#### 주요 기본 자료형

| 자료형 | 의미 | 예 |
|---|---|---|
| `bool` | 참/거짓 | `true`, `false` |
| `char` | 문자 | `'A'` |
| `short` | 작은 범위 정수 | `100` |
| `int` | 일반적인 정수 | `1000` |
| `long`, `long long` | 큰 범위 정수 | 큰 정수값 |
| `float` | 단정밀도 실수 | `3.14f` |
| `double` | 배정밀도 실수 | `3.141592` |

`unsigned`가 붙으면 음수를 표현하지 않는 대신 양수 범위가 넓어진다.

```cpp
unsigned int count = 100;
```

#### 선언 / 초기화 / 대입

```cpp
int a;       // 선언
int b = 10;  // 선언과 동시에 초기화
a = 20;      // 대입
```

초기화하지 않은 지역 변수는 의미 없는 값이 들어 있을 수 있으므로 사용 전에 초기화하는 습관이 중요하다.

```cpp
int count = 0;
```

#### `const`

한 번 정한 값을 변경하지 않아야 할 때 사용한다.

```cpp
const double PI = 3.141592;
```

`PI = 3.0;`처럼 다시 대입할 수 없다.

#### 복습 포인트

- 변수 = 값을 저장하는 공간
- 자료형 = 저장할 데이터의 종류와 크기를 결정
- 지역 변수는 사용 전 초기화
- 변경되면 안 되는 값은 `const`

---

## 자료형 승격과 형 변환

### Casting(형변환): [소스](./Day0306-Solution/basic/02_casting.cpp)
    
- 데이터 타입을 다른 타입으로 바꾸는 것
- 암묵적: 컴파일러가 자동으로 타입 변환
    - x + y → 자동으로 double로 변환 (암묵적)
- 명시적: 직접 int로 변환
    - static_cast<int>(x)

서로 다른 자료형끼리 연산하면 컴파일러가 연산하기 적절한 자료형으로 자동 변환하기도 한다.

#### 암묵적 자료형 승격

대표적으로 작은 정수형은 연산 시 `int`로 승격될 수 있다.

```text
bool  ─┐
char  ─┼→ int
short ─┘
```

예:

```cpp
char a = 10;
char b = 20;

int result = a + b;
```

#### 명시적 형 변환

개발자가 직접 자료형을 지정하여 변환할 수도 있다.

```cpp
double value = 3.14;
int number = static_cast<int>(value);
```

결과는 `3`이다.

#### 주의

실수에서 정수로 변환하면 소수 부분이 사라진다.

```cpp
int n = static_cast<int>(3.99); // 3
```

#### 복습 포인트

> **자동으로 바뀌는 것 = 암묵적 변환**,  
> **개발자가 직접 바꾸는 것 = 명시적 변환**

#### 정리

- 상수 (Constant)
    - 한 번 값이 정해지면 변경할 수 없는 변수
    - 예: const double PI = 3.14; → PI는 항상 3.14

- 전역변수 (Global Variable)
    - 프로그램 시작 시 자동으로 기본값으로 초기화

- 지역변수 (Local Variable)
    - 자동 초기화되지 않음
    - 사용 전에 반드시 초기화해야 함
    - 초기화하지 않으면 **쓰레기값(garbage value)**이 들어 있음

    - 왜 변환을 할까: cpu가 효율적으로 처리할 수 있는 기본 정수 단위가 보통 32비트(int)이기 때문

---

### Processing(연산): [소스](./Day0306-Solution/basic2/03_operator.cpp)
    
- 입력 데이터를 가지고 계산, 비교, 논리 판단, 값 변경 등 프로그램이 처리하는 모든 활동


#### 산술 연산자

```cpp
a + b;
a - b;
a * b;
a / b;
a % b;
```

`%`는 나머지를 구할 때 사용한다.

```cpp
10 % 3 // 1
```

짝수 판별에도 사용할 수 있다.

```cpp
if (number % 2 == 0)
```

#### 관계 연산자

```cpp
==  !=  >  <  >=  <=
```

결과는 `true` 또는 `false`.

#### 논리 연산자

```cpp
&&  // AND
||  // OR
!   // NOT
```

예:

```cpp
if (age >= 20 && age < 30)
```

#### 대입과 복합 대입

```cpp
a = 10;
a += 5; // a = a + 5
a -= 5;
a *= 2;
```

#### 증감 연산자

```cpp
i++;
i--;
```

#### 삼항 연산자

```cpp
조건 ? 참일_때_값 : 거짓일_때_값
```

예:

```cpp
int max = (a > b) ? a : b;
```

#### 비트 연산자

```cpp
& | ^ ~ << >>
```

정수 데이터를 비트 단위로 처리할 때 사용한다.

---

#### 출력 형식 제어

`<iomanip>`의 기능을 이용하면 출력 형태를 조정할 수 있다.

```cpp
#include <iomanip>
```

#### 폭 지정

```cpp
cout << setw(5) << 10;
```

#### 빈 공간 채우기

```cpp
cout << setfill('*') << setw(5) << 10;
```

출력:

```text
***10
```

#### 실수 자릿수

```cpp
cout << fixed << setprecision(2) << 3.14159;
```

출력:

```text
3.14
```

#### 진수

```cpp
cout << hex << 255; // ff
cout << oct << 255; // 377
cout << dec << 255; // 255
```

---

### Condition(조건): [소스](./Day0306-Solution/basic2/04_condition.cpp)
    
    - 조건은 true/false 값
    - 조건이 참이면 if 블록 실행, 거짓이면 else 블록 실행
    - 여러 조건 → else if
    - 한 줄 조건 → 삼항 연산자
    - 여러 정수/문자 조건 → switch

조건문은 조건에 따라 실행할 코드를 선택한다.

#### `if`

```cpp
if (score >= 60) {
    cout << "합격";
}
```

#### `if - else`

```cpp
if (score >= 60) {
    cout << "합격";
} else {
    cout << "불합격";
}
```

#### `else if`

```cpp
if (score >= 90) {
    cout << "A";
} else if (score >= 80) {
    cout << "B";
} else {
    cout << "C";
}
```

#### `switch`

하나의 값에 따라 여러 경우를 나눌 때 편리하다.

```cpp
switch (menu) {
case 1:
    cout << "등록";
    break;
case 2:
    cout << "조회";
    break;
default:
    cout << "잘못된 메뉴";
}
```

#### 복습 포인트
- 범위나 복잡한 조건 → `if`
- 하나의 값으로 여러 경우 구분 → `switch`

---

### Loop(반복)

반복문은 같은 작업을 여러 번 수행할 때 사용한다.

- 규칙 찾기
- 초기값, 조건, 증가

1. for문 → 반복 횟수 정해짐: [소스](./Day0306-Solution/basic2/05_for.cpp)
2. while문 → 조건이 참이면 반복: [소스](./Day0306-Solution/basic2/06_while.cpp)
3. do while 문 → 최소 1번 실행 
4. break → 반복문 종료: [소스](./Day0306-Solution/basic2/07_break_continue.cpp)
5. continue → 다음 반복 진행
6. return → 함수 종료

#### `for`

반복 횟수를 알 때 많이 사용한다.

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << endl;
}
```

구조:

```text
초기식 → 조건 확인 → 본문 → 증감식 → 조건 확인 ...
```

#### `while`

조건이 참인 동안 반복한다.

```cpp
while (count < 5) {
    count++;
}
```

#### `do-while`

본문을 최소 한 번 실행한다.

```cpp
do {
    cin >> menu;
} while (menu != 0);
```

#### `break` / `continue`

```cpp
break;    // 반복문 자체를 종료
continue; // 현재 반복만 건너뛰고 다음 반복 진행
```

#### 복습 포인트

> `break` = 반복문 밖으로 나감  
> `continue` = 이번 차례만 건너뜀  
> `return` = 함수 자체를 종료

---

## 2026.03.09 (월) - 함수 심화와 객체지향 프로그래밍

### 함수

함수는 특정 작업을 하나의 단위로 묶은 것이다.

```cpp
반환자료형 함수이름(매개변수) {
    실행문;
    return 값;
}
```

예:

```cpp
int add(int a, int b) {
    return a + b;
}
```

#### 함수를 사용하는 이유

1. 코드 재사용
2. 기능 분리
3. 가독성 향상
4. 오류 확인 및 유지보수 용이

#### 함수 프로토타입

함수 구현이 `main()`보다 아래에 있으면 먼저 함수의 존재를 알려줄 수 있다.

```cpp
int add(int a, int b);

int main() {
    cout << add(3, 5);
}

int add(int a, int b) {
    return a + b;
}
```

#### 반환값과 매개변수

```cpp
void print();          // 반환 X, 매개변수 X
void print(int n);     // 반환 X, 매개변수 O
int getNumber();       // 반환 O, 매개변수 X
int add(int a, int b); // 반환 O, 매개변수 O
```

---

### Pass-by-Value

값 전달은 변수 자체가 아니라 **값의 복사본**을 함수에 넘긴다.

```cpp
void change(int x) {
    x = 100;
}

int main() {
    int a = 10;
    change(a);

    cout << a; // 10
}
```

함수의 `x`와 `main()`의 `a`는 서로 다른 변수다.

#### 핵심

```text
a = 10
 ↓ 값 복사
x = 10

x를 변경해도 a에는 영향 없음
```

### Pass-by-Pointer

변수의 주소를 함수에 전달한다.

```cpp
void change(int* ptr) {
    *ptr = 100;
}

int main() {
    int a = 10;
    change(&a);

    cout << a; // 100
}
```

관계:

```text
a
↑
&a → ptr → *ptr
```

- `&a` : a의 주소
- `ptr` : 주소 저장
- `*ptr` : 주소가 가리키는 실제 값

포인터는 `nullptr`일 가능성이 있으므로 확인이 필요하다.

```cpp
if (ptr == nullptr)
    return;
```

---

### Pass-by-Reference

C++에서는 참조를 이용하여 원본 변수를 직접 다룰 수 있다.

```cpp
void change(int& value) {
    value = 100;
}
```

호출:

```cpp
int a = 10;
change(a);
```

#### 세 전달 방식 비교

| 방식 | 함수 선언 | 원본 변경 | 특징 |
|---|---|---:|---|
| 값 | `void f(int x)` | X | 복사본 사용 |
| 포인터 | `void f(int* x)` | O | 주소 전달, `nullptr` 가능 |
| 참조 | `void f(int& x)` | O | 원본의 별칭, 문법 간결 |

#### 기억

> 원본을 변경할 필요가 없다면 값 전달,  
> 원본을 직접 변경하려면 포인터 또는 참조를 사용할 수 있다.

---

### 함수 반환 방식

#### Return-by-Value

```cpp
int add(int a, int b) {
    return a + b;
}
```

결과값을 복사하여 반환한다.

#### Return-by-Reference

```cpp
int global = 10;

int& getValue() {
    return global;
}
```

실제 변수의 참조를 반환한다.

```cpp
getValue() = 100;
```

이 경우 `global`도 `100`이 된다.

#### 주의

함수 종료 후 사라지는 지역 변수의 참조를 반환하면 안 된다.

```cpp
int& wrong() {
    int value = 10;
    return value; // 위험
}
```

---

### 함수 오버로딩

같은 이름의 함수를 매개변수를 다르게 하여 여러 개 정의할 수 있다.

```cpp
int max(int a, int b);
double max(double a, double b);
```

구분 기준:

- 매개변수 자료형
- 매개변수 개수
- 매개변수 순서

구분 기준이 아닌 것:

- 반환 자료형

```cpp
int get();
double get(); // 반환형만 달라서 불가능
```

---

### Scope와 Shadowing

변수는 선언된 영역에 따라 사용할 수 있는 범위가 다르다.

```cpp
int x = 10;

{
    int x = 20;
    cout << x; // 20
}

cout << x; // 10
```

안쪽 블록의 `x`가 바깥쪽 `x`를 가리는 것을 **Shadowing**이라고 한다.

---

### `static` 지역 변수

일반 지역 변수:

```cpp
void count() {
    int n = 0;
    n++;
    cout << n;
}
```

호출할 때마다 다시 `0`에서 시작한다.

정적 지역 변수:

```cpp
void count() {
    static int n = 0;
    n++;
    cout << n;
}
```

세 번 호출하면:

```text
1
2
3
```

#### 핵심

> 지역 변수처럼 함수 내부에서만 접근하지만 **수명은 프로그램이 끝날 때까지 유지**된다.

---

### 클래스와 객체

클래스는 객체를 만들기 위한 설계도라고 생각하면 쉽다.

```text
Class = 설계도
Object = 설계도로 만든 실제 객체
```

예:

```cpp
class Person {
private:
    string name;
    int age;

public:
    void introduce() {
        cout << name << "/" << age;
    }
};
```

객체 생성:

```cpp
Person p1;
Person p2;
```

`p1`과 `p2`는 같은 `Person` 클래스로 만들었지만 각각 별도의 데이터를 가진다.

---

### 데이터 멤버와 멤버 함수

```cpp
class Account {
private:
    int money;           // 데이터 멤버

public:
    void setMoney(int m); // 멤버 함수
    int getMoney() const;
};
```

- 데이터 멤버 = 객체의 상태/속성
- 멤버 함수 = 객체가 수행하는 기능

---

### 접근 제한자

| 접근 제한자 | 같은 클래스 | 자식 클래스 | 외부 |
|---|---:|---:|---:|
| `private` | O | X | X |
| `protected` | O | O | X |
| `public` | O | O | O |

일반적으로 데이터는 `private`, 외부에 제공할 기능은 `public`으로 구성한다.

---

### 클래스 내부 구현 vs 외부 구현

#### 클래스 내부

```cpp
class Member {
public:
    void print() {
        cout << "Member";
    }
};
```

#### 클래스 외부

```cpp
class Member {
public:
    void print();
};

void Member::print() {
    cout << "Member";
}
```

`Member::print()`에서 `::`는 `print()`가 `Member` 클래스 소속이라는 뜻이다.

---

### `static` 멤버

#### 정적 멤버 변수

모든 객체가 공유하는 데이터다.

```cpp
class Player {
public:
    static int count;
};

int Player::count = 0;
```

일반 멤버 변수:

```text
p1 → 자신의 값
p2 → 자신의 값
```

정적 멤버 변수:

```text
p1 ─┐
p2 ─┼→ 하나의 공유 값
p3 ─┘
```

#### 정적 멤버 함수

객체 없이 호출 가능하다.

```cpp
Math::add(10, 20);
```

---

### 생성자

객체가 생성될 때 자동 호출되는 특별한 함수다.

```cpp
class Circle {
public:
    Circle() {
        cout << "생성";
    }
};
```

특징:

- 클래스 이름과 동일
- 반환형 없음
- 객체 생성 시 자동 실행

#### 매개변수가 있는 생성자

```cpp
Circle(double r) {
    radius = r;
}
```

#### 복사 생성자

```cpp
Circle(const Circle& other);
```

기존 객체를 이용하여 새로운 객체를 생성할 때 사용한다.

---

### 생성자 초기화 리스트

```cpp
Circle(double r)
    : radius(r) {
}
```

대입:

```cpp
radius = r;
```

과 달리 초기화 리스트는 객체 멤버가 **생성되는 순간 바로 초기화**한다.

특히 다음과 같은 경우 중요하다.

```cpp
const double PI;
```

`const` 멤버는 생성 이후 대입할 수 없으므로 초기화 리스트에서 값을 넣어야 한다.

```cpp
Circle() : PI(3.14) {}
```

---

### Singleton Pattern

프로그램 전체에서 특정 클래스의 객체를 하나만 사용하도록 제한하는 패턴이다.

핵심 구조:

```cpp
class Singleton {
private:
    Singleton() {}

public:
    static Singleton& getInstance() {
        static Singleton instance;
        return instance;
    }
};
```

외부에서 생성자를 호출할 수 없게 `private`으로 만든다.

```cpp
Singleton s; // 불가능
```

대신:

```cpp
Singleton& s = Singleton::getInstance();
```

복사까지 막으려면:

```cpp
Singleton(const Singleton&) = delete;
Singleton& operator=(const Singleton&) = delete;
```

---

### 소멸자

객체가 소멸될 때 자동으로 호출된다.

```cpp
~Circle() {
    // 자원 정리
}
```

특히 동적으로 할당한 자원이 있다면 정리하는 데 사용한다.

```cpp
delete ptr;
```

### 생성자와 소멸자

```text
객체 생성 → 생성자 실행
      ↓
   객체 사용
      ↓
객체 소멸 → 소멸자 실행
```

---

### `this` 포인터

멤버 함수가 실행되고 있는 **현재 객체 자신**을 가리킨다.

```cpp
void setRadius(double radius) {
    this->radius = radius;
}
```

- `this->radius` = 객체의 데이터 멤버
- `radius` = 함수 매개변수

---

### 캡슐화

객체의 데이터를 직접 노출하지 않고 정해진 기능을 통해 접근하도록 만드는 것이다.

```cpp
class Person {
private:
    int age;

public:
    int getAge() {
        return age;
    }

    void setAge(int value) {
        if (value > 0)
            age = value;
    }
};
```

외부에서는:

```cpp
person.age = -100; // 직접 접근 불가
```

대신:

```cpp
person.setAge(20);
```

#### 목적

- 정보 은닉
- 데이터 보호
- 잘못된 값 입력 방지
- 유지보수성 향상
- 결합도 감소

---

## 2026.03.10 (화) — 클래스 관계와 상속

**관련 이미지:** `image-36.png` ~ `image-42.png`

### 클래스 관계

객체지향에서는 클래스가 서로 어떤 관계를 가지는지가 중요하다.

```text
IS-A   : ~은 ~이다
HAS-A  : ~은 ~을 가지고 있다
USES-A : ~은 ~을 사용한다
```

예:

```text
Taxi IS-A Vehicle
Car HAS-A Engine
```

---

### 상속 — IS-A

기존 클래스의 특성을 새로운 클래스가 이어받는다.

```cpp
class Vehicle {
public:
    void move() {}
};

class Taxi : public Vehicle {
};
```

`Taxi`는 `Vehicle`의 기능을 사용할 수 있다.

```cpp
Taxi taxi;
taxi.move();
```

#### 용어

- 부모 클래스 = Base Class / Super Class
- 자식 클래스 = Derived Class / Sub Class

#### 왜 사용하는가?

공통 기능을 부모에 정의하면 자식 클래스에서 중복 구현하지 않아도 된다.

```text
        Vehicle
       /       \
     Taxi      Bus
```

`move()` 같은 공통 기능은 `Vehicle`에 둘 수 있다.

---

### `private`와 `protected`

부모의 `private` 멤버는 자식 클래스에서도 직접 접근할 수 없다.

```cpp
class Parent {
private:
    int value;
};
```

자식에서:

```cpp
value = 10; // 직접 접근 불가
```

`protected`라면 자식 클래스에서 접근할 수 있다.

```cpp
class Parent {
protected:
    int value;
};
```

#### 기억

> `private` = 클래스 내부만  
> `protected` = 클래스 내부 + 자식  
> `public` = 외부까지

---

### Overloading vs Overriding

이 둘은 이름이 비슷해서 꼭 구분해야 한다.

| 구분 | Overloading | Overriding |
|---|---|---|
| 관계 | 같은 범위에서도 가능 | 상속 관계 필요 |
| 함수 이름 | 같음 | 같음 |
| 매개변수 | 달라야 함 | 부모 함수와 대응 |
| 목적 | 같은 이름으로 여러 기능 | 부모 기능 재정의 |

#### Overloading

```cpp
void print(int value);
void print(double value);
```

#### Overriding

```cpp
class Animal {
public:
    virtual void sound() {
        cout << "Animal";
    }
};

class Dog : public Animal {
public:
    void sound() override {
        cout << "Dog";
    }
};
```

---

### HAS-A 연관 관계

한 클래스가 다른 객체를 보유하거나 참조하는 관계다.

```cpp
class Company {
private:
    vector<Employee*> employees;
};
```

의미:

```text
Company HAS-A Employee
```

상속이 **종류 관계**라면 HAS-A는 **포함/보유 관계**다.

#### 복습 포인트

`Car`는 `Engine`의 한 종류가 아니다.

```text
Car IS-A Engine   X
Car HAS-A Engine  O
```

따라서 무조건 상속을 사용하는 것이 아니라 실제 관계에 따라 설계해야 한다.


## 2026.03.11 (수) - 객체 관계와 다형성

* 다형성
- C++에서 다형성은 부모 클래스 포인터로 자식 객체를 다루면서, virtual 함수를 통해 객체에 맞는 함수가 실행되는 것이다.

![alt text](image-44.png)

- 슬라이싱(Object Slicing)은 자식 객체를 부모 객체에 값으로 복사할 때 자식 부분이 잘려나가는 현상이다.

![alt text](image-47.png)

![alt text](image-48.png)

* 추상클래스, 인터페이스 ,다중 상속

- 추상 클래스 (Abstract Class)
    - 일부 기능은 구현되어 있고, 일부는 자식 클래스가 반드시 구현해야 하는 클래스.
    - 예: Animal 클래스는 eat()은 구현돼 있지만 speak()는 Dog, Cat이 각각 구현.

- 인터페이스 (Interface)
    - 기능의 이름(규칙)만 정의하고 구현은 전혀 없는 클래스.
    - 예: Flyable 인터페이스에 fly()만 정의 → Bird, Airplane이 각각 다르게 구현.

![alt text](image-49.png)           

- 다중 상속 (Multiple Inheritance)
    - 한 클래스가 여러 부모 클래스로부터 동시에 상속받는 것.
    - 예: Bird 클래스가 Animal과 Flyable을 둘 다 상속받음 → 동물의 특징도 가지고 날 수도 있음.
    - 다이아몬드 문제: D가 A에서 상속받은 멤버를 두 번 갖게 되는 문제

![alt text](image-50.png)  

- 믹스인클래스(mixin class)
    - 순수 가상 함수를 가져서 인스턴스화는 안되지만, 다른 클래스에 데이터 멤버를 추가해주는 클래스를 의미함.
    - 딸기 와플, 포도 와플에 생크림 토핑을 준다고 할 때 토핑은 믹스인 클래스에 해당함. 

* 예외처리
    -  try → 예외 발생 가능 코드
    -  throw → 예외 발생
    -  catch → 예외 처리
    -  여러 타입 예외 가능, 순서 주의
    -  상속 구조를 활용하면 공통 처리 가능

    ![alt text](image-51.png)

---

### 일반 객체와 동적 객체

일반 객체:

```cpp
Base b;
```

블록이 끝나면 자동으로 소멸한다.

동적 객체:

```cpp
Base* ptr = new Base();
```

사용 후 직접 해제해야 한다.

```cpp
delete ptr;
```

#### 접근 방법

```cpp
b.show();     // 일반 객체
ptr->show();  // 포인터
```

---

### 다형성

다형성은 하나의 부모 타입을 통해 서로 다른 자식 객체를 다룰 수 있게 하는 객체지향 특성이다.

```cpp
Base* ptr = new Child();
```

변수 타입은 `Base*`지만 실제 객체는 `Child`다.

---

### `virtual`과 동적 바인딩

```cpp
class Base {
public:
    virtual void show() {
        cout << "Base";
    }
};

class Child : public Base {
public:
    void show() override {
        cout << "Child";
    }
};
```

```cpp
Child child;
Base* ptr = &child;

ptr->show();
```

결과:

```text
Child
```

`virtual`이 없으면 부모 포인터를 기준으로 부모 함수가 호출될 수 있다.

#### 핵심

> `virtual`은 **실행 시점에 실제 객체가 어떤 타입인지 확인하여 호출할 함수를 결정**하게 한다.

이를 동적 바인딩이라고 한다.

---

### 객체 슬라이싱

```cpp
Child child;
Base base = child;
```

자식 객체를 부모 객체에 **값으로 복사**하면 부모 부분만 남는다.

```text
Child
├── Base 부분  → 복사됨
└── Child 부분 → 잘림
```

이를 Object Slicing이라고 한다.

따라서 다형성을 사용할 때는 보통 포인터나 참조를 사용한다.

```cpp
Base* ptr = &child;
Base& ref = child;
```

---

### 구성 관계

```cpp
class Car {
private:
    Wheel* wheels[4];

public:
    Car() {
        for (int i = 0; i < 4; i++)
            wheels[i] = new Wheel();
    }

    ~Car() {
        for (int i = 0; i < 4; i++)
            delete wheels[i];
    }
};
```

`Car`가 `Wheel`을 직접 생성하고 제거한다.

```text
Car 생성 → Wheel 생성
Car 소멸 → Wheel 소멸
```

객체의 생명주기가 강하게 연결되어 있는 HAS-A 관계다.

---

### 의존 관계 — USES-A

특정 기능을 수행할 때만 다른 객체를 사용하는 관계다.

```text
A USES-A B
```

상속이나 구성에 비해 비교적 약한 관계이다.

---

#### 부모 타입으로 여러 객체 처리

```cpp
class Product {
public:
    int getPrice() const;
};

class Tv : public Product {};
class Computer : public Product {};
```

`Customer`가 부모 타입을 받도록 하면:

```cpp
void buy(Product& product) {
    money -= product.getPrice();
}
```

다음처럼 서로 다른 상품을 같은 함수로 처리할 수 있다.

```cpp
customer.buy(tv);
customer.buy(computer);
```

이것이 다형성의 실용적인 장점이다.

---

#### 추상 클래스

순수 가상 함수를 하나 이상 가진 클래스다.

```cpp
class Shape {
public:
    virtual double getArea() = 0;
};
```

`Shape` 자체로는 객체를 만들 수 없다.

```cpp
Shape shape; // 불가능
```

자식이 반드시 기능을 구현해야 한다.

```cpp
class Circle : public Shape {
public:
    double getArea() override {
        // ...
    }
};
```

---

### 인터페이스 개념

공통된 기능의 **규칙**을 정해 놓는 역할을 한다.

예를 들어 모든 도형이 넓이를 계산해야 한다면:

```cpp
virtual double getArea() = 0;
```

자식 클래스마다 계산 방법은 다르지만 `getArea()`라는 공통 규칙을 따르게 할 수 있다.

---

### 다중 상속

하나의 클래스가 여러 부모 클래스를 상속받는 것이다.

```cpp
class Child : public Father, public Mother {
};
```

여러 부모가 같은 조상을 공유하면 다이아몬드 구조가 만들어질 수 있으므로 이름 충돌과 중복 상속 문제를 주의해야 한다.

---

### 예외처리

실행 중 발생할 수 있는 예상 가능한 오류 상황을 처리한다.

```cpp
try {
    throw 10;
}
catch (int e) {
    cout << "예외: " << e;
}
```

흐름:

```text
try
 ↓
문제 발생
 ↓
throw
 ↓
알맞은 catch에서 처리
```

#### 사용하는 이유

- 프로그램의 갑작스러운 종료 방지
- 정상 코드와 오류 처리 코드 분리
- 하위 함수에서 발생한 오류를 상위 함수에서 처리 가능

---

## 2026.03.12 (목) - 배열·Template·STL·파일 입출력·Thread

### 배열 기초

배열은 같은 자료형의 데이터를 연속적으로 저장한다.

```cpp
int arr[5] = {1, 2, 3, 4, 5};
```

인덱스는 `0`부터 시작한다.

```text
arr[0] = 1
arr[1] = 2
...
arr[4] = 5
```

### 장점

- 여러 데이터를 하나의 이름으로 관리
- 반복문과 함께 사용하기 편리

### 한계

- 크기가 고정됨
- 같은 자료형만 저장

![alt text](image-52.png)

---

### 배열 초기화

```cpp
int arr[5] = {1, 2, 3, 4, 5};
```

부분 초기화:

```cpp
int arr[5] = {1, 2};
```

나머지는 `0`으로 초기화된다.

전체 0 초기화:

```cpp
int arr[5] = {0};
```

크기 자동 결정:

```cpp
int arr[] = {1, 2, 3};
```

배열 크기는 `3`.

---

### 배열 순회

반복문과 함께 많이 사용한다.

```cpp
int numbers[] = {10, 20, 30, 40};

for (int i = 0; i < 4; i++) {
    cout << numbers[i] << endl;
}
```

배열과 반복문은 여러 데이터를 일괄 처리할 때 기본적으로 함께 사용된다.

---

### Template과 Generic Programming

같은 로직인데 자료형만 다른 함수를 여러 개 만들면 코드가 중복된다.

```cpp
int add(int a, int b);
double add(double a, double b);
```

Template을 사용하면:

```cpp
template <typename T>
T add(T a, T b) {
    return a + b;
}
```

다음처럼 사용할 수 있다.

```cpp
add<int>(3, 4);
add<double>(3.5, 4.5);
```

#### 핵심

> Template = 자료형을 매개변수처럼 다루어 코드를 재사용하는 방법

---

### STL
![alt text](image-54.png)

STL은 C++에서 제공하는 검증된 자료구조와 알고리즘의 모음이다.

#### 주요 컨테이너

| 컨테이너 | 특징 |
|---|---|
| `vector` | 크기를 동적으로 변경할 수 있는 배열 |
| `list` | 연결 리스트 |
| `stack` | LIFO |
| `queue` | FIFO |
| `deque` | 앞뒤 삽입·삭제 |
| `set` | 중복 없는 데이터 |
| `map` | Key-Value 데이터 |

#### `vector`

```cpp
vector<int> numbers;

numbers.push_back(10);
numbers.push_back(20);
```

일반 배열과 달리 필요에 따라 크기를 늘릴 수 있다.

#### `stack`

```text
입력: A → B → C
출력: C → B → A
```

LIFO(Last In First Out).

#### `queue`

```text
입력: A → B → C
출력: A → B → C
```

FIFO(First In First Out).

#### `set`

중복 데이터를 허용하지 않는 집합에 적합하다.

#### `map`

```text
Key → Value
```

형태로 데이터를 관리한다.

예:

```cpp
map<string, int> scores;
scores["Kim"] = 90;
```

---

### 파일 입출력

![alt text](image-55.png)


프로그램이 종료되어도 데이터를 유지하려면 파일 등에 저장해야 한다.

#### 파일 쓰기

```cpp
#include <fstream>

ofstream file("members.txt");

if (file.is_open()) {
    file << "1,Kim,010-1234-5678";
    file.close();
}
```

#### 파일 읽기

```cpp
ifstream file("members.txt");
string line;

while (getline(file, line)) {
    cout << line << endl;
}

file.close();
```

#### 파일 스트림

| 클래스 | 역할 |
|---|---|
| `ifstream` | 읽기 |
| `ofstream` | 쓰기 |
| `fstream` | 읽기 + 쓰기 |

기본 흐름:

```text
open
 ↓
is_open 확인
 ↓
read / write
 ↓
close
```

---

### Thread

![alt text](image-56.png)


Thread는 하나의 프로그램 안에서 실행되는 작업 흐름이다.

```cpp
void work() {
    cout << "작업 실행";
}

int main() {
    thread t(work);
    t.join();
}
```

#### `join()`

생성한 Thread가 끝날 때까지 현재 Thread가 기다린다.

```text
main
 ├── Thread 실행
 │      ↓
 │     work()
 │      ↓
 └── join()에서 대기
        ↓
   Thread 종료
        ↓
   main 계속 실행
```

Thread는 서버의 여러 요청 처리, 화면 처리와 백그라운드 작업 등 여러 작업을 함께 처리할 때 활용할 수 있다.

---

## test: 학생 관리 프로그램 만들기 

![alt text](image-59.png)

[소스](./Day0312-Solution/evaluation/memMng_psy.cpp)

학습한 C++ 내용을 종합하여 **콘솔 기반 회원관리 애플리케이션**을 구현하였다.

### 클래스 구성

```text
Member
├── int id
├── string name
├── string phone
└── string email
```

`Member`는 회원 한 명의 데이터를 담당한다.

`MemberManager`는 여러 회원과 회원관리 기능을 담당한다.

```text
MemberManager
├── 등록
├── 전체조회
├── 검색
├── 수정
├── 삭제
└── 파일 저장/불러오기
```

### 메뉴

```text
1. 등록
2. 전체조회
3. 검색
4. 수정
5. 삭제
Q. 종료
```

### 파일 저장

회원 데이터는:

```text
members.txt
```

에 저장한다.

이를 통해 프로그램을 종료한 뒤 다시 실행해도 데이터를 유지할 수 있다.

### 이 실습에서 연결되는 학습 개념

```text
조건문
   ↓
메뉴 처리

반복문
   ↓
프로그램 반복 실행 / 회원 탐색

함수
   ↓
등록·검색·수정·삭제 기능 분리

클래스
   ↓
Member / MemberManager 역할 분리

캡슐화
   ↓
회원 데이터 보호

STL
   ↓
여러 회원 데이터 관리

파일 입출력
   ↓
members.txt 영구 저장
```

즉, 단순한 콘솔 프로그램이 아니라 앞에서 배운 **C++ 문법과 객체지향 개념을 하나의 프로그램에 종합 적용하는 실습**이다.
