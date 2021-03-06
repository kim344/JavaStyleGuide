
# JavaStyleGuide

Java 코드를 이해하기 쉽고 명확하게 작성하기 위한 스타일 가이드입니다. 추후 내용이 추가되거나 변경될 수 있습니다.  

본 문서에 나와있지 않은 규칙은 아래 문서를 따릅니다.

- [Oracle Code Conventions for Java TM Programming Language](https://www.oracle.com/technetwork/java/javase/documentation/codeconvtoc-136057.html)
- [한글 번역 본 PDF 다운로드](https://greencode.tistory.com/attachment/cfile6.uf@131F18425154F16735F48A.pdf)


## 목차

- [개요](#개요)
- [파일 이름](#파일-이름)
    - [파일 확장자](#파일-확장자)
    - [공통으로 사용되는 파일 이름](#공통으로-사용되는-파일-이름)
- [파일 구조](#파일-구조)
    - [자바 소스 파일](#자바-소스-파일)
        - [시작 주석](#시작-주석)
        - [Package 문과 Import 문](#Package-문과-Import-문)
- [들여쓰기](#들여쓰기)
    - [한 줄의 길이](#한-줄의-길이)
    - [줄 나누기](#줄-나누기)
- [주석](#주석)
    - [구현 주석 형식](#구현-주석-형식)
        - [블록(Block) 주석](#블록(Block)-주석)
        - [한줄(Single-Line) 주석](#한줄(Single\-Line)-주석)
        - [꼬리(Trailing) 주석](#꼬리(Trailing)-주석)
        - [줄 끝(End-Of-Line) 주석](#줄-끝(End\-of\-Line)-주석)
    - [문서화(Documentation) 주석](#문서화(Documentation)-주석)
- [선언](#선언)
    - [한 줄당 선언문의 수](#한-줄당-선언문의-수)
    - [초기화](#초기화)
    - [배치](#배치)
    - [클래스와 인터페이스 선언](#클래스와-인터페이스-선언)
- [문 (Statements)](#문-(Statements))
    - [간단한 문](#간단한-문)
    - [복합문](#복합문)
    - [return 문](#return-문)
    - [if, if-else, if else-if else 문](#if,-if\-else,-if-else\-if-else-문)
    - [for 문](#for-문)
    - [while 문](#while-문)
    - [do-while 문](#do-while-문)
    - [switch 문](#switch-문)
    - [try-catch 문](#try\-catch-문)
- [빈 공간](#빈-공간)
    - [한 줄 띄우기 (Blank Lines)](#한-줄-띄우기-(Blank-Lines))
    - [공백 (Blank Spaces)](#공백-(Blank-Spaces))
- [명명(Naming) 규칙](#명명(Naming)-규칙)
    - [Packages](#Packages)
    - [Classes](#Classes)
    - [Interfaces](#Interfaces)
    - [Methods](#Methods)
    - [Variables](#Variables)
    - [Constants](#Constants)



## 개요
- 소프트웨어를 개발하는 일련의 모든 과정에 들어가는 비용 중 80%가 유지보수에 쓰여진다.
- 소프트웨어의 직접 개발한 개발자가 그 소프트웨어의 유지보수를 담당하는 경우는 거의 보기 힘들다.
- 코딩 규칙을 지키면 다른 개발자가 그 소스 코드를 처음 보았을 때, 더 빠른 시간 안에 완벽하게 이해할 수 있도록 도와주기 때문에, 소프트웨어의 가독성이 높아진다.
- 개발자가 자신의 소스 코드를 제품으로 팔려고 한다면, 자신이 작성한 다른 소스 코드들과 잘 어울리도록 패키지(package)를 적절하게 구성할 필요가 있다.

## 파일 이름
- 이 장에서는 흔하게 사용되는 파일 확장자와 파일 이름을 설명한다.
### 파일 확장자
- 자바 소프트웨어는 다음의 파일 확장자를 사용한다.

| 파일형태 | 확장자 |
|---|:---:|
| `자바 소스` | .java |
| `자바 바이트 코드` | .class

### 공통으로 사용되는 파일 이름
- 공통으로 다음과 같은 파일 이름을 사용한다

| 파일 이름 | 사용 |
|---|:---:|
| `GNUmakefile` | make 파일 이름으로 사용, 소프트웨어를 빌드할 때는 gnumake 명령어를 사용 |
| `README` | 특정 디렉토리의 내용을 요약하는 파일 이름으로 사용

## 파일 구조
- 파일은 빈 줄이나 다른 구역임을 나타내주는 주석으로 나누어지는 여러 구역(section)들로 구성되어 있다.
- 2,000 라인을 넘는 파일은 이해하기가 쉽지 않기 때문에 될 수 있으면 피해야 한다.
- 적절하게 구성된 자바 프로그램의 예제는 아래 "11장의 1절 자바 소스파일 예제" 에서 볼 수 있다.

### 자바 소스 파일
각각의 자바 소스 파일은 하나의 public 클래스 또는 인터페이스를 가진다. private 클래스들과 인터페이스들이 public 클래스와 연결되어 있을 때, public 클래스와 같은 파일에 private 클래스들과 인터페이스들을 넣을 수 있다. public 클래스는 파일에서 첫 번째 클래스 또는 인터페이스이어야 한다.

자바 소스 파일은 다음과 같은 순서를 가진다.

- 시작 주석
- Package 문과 Import 문
- Class와 Interface 선언

#### 시작 주석

모든 소스 파일은 클래스 이름, 버전 정보, 날짜, 저작권 주의를 보여주는 C 스타일의 주석과 함께 시작한다.

```java
/*
* 클래스 이름
*
* 버전 정보 
* 
* 날짜 
* 
* 저작권 주의 
*/
```

#### Package 문과 Import 문

대부분의 자바 소스 파일에서 주석이 아닌 첫 번째 줄은 Package 문이다. 그 후에 Import 문이 뒤따라 나온다. 예를들면 다음과 같다 ↓

```java
package java.awt; 
import java.awt.peer.CanvasPeer;
```

## 들여쓰기

- 4개의 빈 칸(space)를 들여쓰기 단위로 사용한다. 들여쓰기의 정확한 구현(빈 칸을 사용하거나 탭을 사용하거나)은 정해져 있지 않다. 탭은 4개의 빈 칸이 아니라, 8개의 빈 칸으로 설정하는 것이 좋다.

### 한 줄의 길이
- 한 줄에 80자 이상 쓰는 것은 대부분의 터미널(terminal)과 툴에서 다룰 수 없기 때문에 피해야 한다.
- \* 문서화 주석을 가지고 문서를 만들 때, 일반적으로 한 줄에 70자 이상을 가지지 않는다.

### 줄 나누기
하나의 식이 한 줄에 들어가지 않을 때에는, 다음과 같은 일반적인 원칙들을 따라서 두 줄로 나눈다.

- 콤마 후에 두 줄로 나눈다.
- 연산자(operator) 앞에서 두 줄로 나눈다.
- 레벨이 낮은 원칙보다는 레벨이 높은 원칙에 따라 두 줄로 나눈다.
- 앞줄과 같은 레벨의 식(expression)이 시작되는 새로운 줄은 앞줄과 들여쓰기를 일치시킨다.
- 만약 위의 원칙들이 코드를 더 복잡하게 하거나 오른쪽 끝을 넘어간다면, 대신에 8개의 빈 칸을 사용해 들여쓴다.

여기 메서드 호출을 두 줄로 나누어 쓰는 몇 가지 예제들이 있다.
```java
someMethod(longExpression1, longExpression2, longExpression3,
longExpression4, longExpression5);

var = someMethod1(longExpression1,
        someMethod2(longExpression2,
        longExpression3));
```
다음은 수학 표현식을 두 줄로 나누어 작성하는 두 개의 예제이다. 첫번째 예제가 괄호로 싸여진 표현식 밖에서 줄 바꿈이 일어나고 더 높은 레벨이기 때문에 첫번째 예제를 더 많이 사용한다.
```java
// 일반적인 들여쓰기 
someMethod(int anArg, Object anotherArg, String yetAnotherArg,
Object andStillAnother) { 
... 
} 

// 너무 멀리 들여쓰는 것을 피하기 위해 8개의 빈 칸으로 들여쓰기 
private static synchronized horkingLongMethodName(int anArg,
Object anotherArg, String yetAnotherArg,
Object andStillAnother) { 
... 
}
```
일반적으로 메서드 본문이 시작할 때 4개의 빈 칸을 사용하므로, 메서드 본문과 구분하기 위해서 줄을 나누는 경우의 들여쓰기는 일반적으로 8개의 빈 칸 원칙을 사용하자 예를 들면 다음과 같다.
```java
// 아래와 같은 들여쓰기는 사용하지 말자.
if ((condition1 && condition2)
|| (condition3 && condition4)
||!(condition5 && condition6)) { // 좋지 않은 들여쓰기 
doSomethingAboutIt(); // 메서드 본문 시작이 명확하지가 않다. 
} 
// 대신에 아래와 같은 들여쓰기를 사용한다. 
if ((condition1 && condition2)
|| (condition3 && condition4)
||!(condition5 && condition6)) { 
doSomethingAboutIt(); 
} 
// 또는 아래와 같은 들여쓰기를 사용한다. 
if ((condition1 && condition2) || (condition3 && condition4)
||!(condition5 && condition6)) {
doSomethingAboutIt(); 
}
```

다음은 삼항식(ternary expression)에서 사용 가능한 세 가지 방법이다.
```java
alpha = (aLongBooleanExpression) ? beta : gamma;

alpha = (aLongBooleanExpression) ? beta
                        : gamma;

alpha = (aLongBooleanExpression)
? beta
: gamma;
```

## 주석

자바 프로그램은 두 가지 종류의 주석을 가진다.

- 구현 주석
- 문서화 주석

### 구현 주석 형식

프로그램은 다음과 같은 4가지 형식의 구현 주석을 포함할 수 있다.

- 블록(Block) 주석
- 한 줄(Single-Line) 주석
- 꼬리(Trailing) 주석
- 줄 끝(End-Of-Line) 주석

#### 블록(Block) 주석
블록 주석은 파일, 메서드, 자료구조, 알고리즘에 대한 설명을 제공할 때 사용된다. 블록 주석은 각각의 파일이 시작될 때와 메서드 전에 사용된다. 또한 메서드 안에서와 같이 다른 장소에서 사용될 수도 있다. 메서드 안에 존재하는 블록 주석은 주석이 설명하는 코드와 같은 단위로 들여쓰기를 해야한다.

블록 주석은 다른 코드들과 구분하기 위해서 처음 한 줄은 비우고 사용한다.

```java
/*
* 여기에 블록 주석을 작선한다.
*/
```
블록 주석의 들여쓰기를 다시 고치지 못하도록 하기 위한 특별한 블록 주석은 /*- 으로 시작할 수 있다.
```java
/*-
* 여기에 들여쓰기를 무시하는 특별한
* 블록 주석을 작성한다.
* * one
* two
* three
*/
```
#### 한줄(Single-Line) 주석
짧은 주석은 뒤따라 오는 코드와 같은 동일한 들여쓰기를 하는 한 줄로 작성할 수 있다. 만약 주석이 한 줄에 다 들어가지 않는다면, 블록 주석 형식을 따라야 한다. 한 줄 주석은 빈 줄로 시작되어야 한다.
```java
if (condition) {
/* 이 조건을 만족하면 실행된다. */
...
}
```
#### 꼬리(Trailing) 주석
아주 짧은 주석이 필요한 경우 주석이 설명하는 코드와 같은 줄에 작성한다. 하지만 실제 코드와는 구분될 수 있도록 충분히 멀리 떨어뜨려야 한다.

```java
if (a == 2) {
return TRUE;
/* 특별한 경우 */
} else {
return isPrime(a); /* a 가 홀수인 경우 */
}
```

#### 줄 끝(End-Of-Line) 주석
주석 기호 // 는 한 줄 모두를 주석 처리하거나 한 줄의 일부분을 주석 처리해야 할 때 사용할 수 있다. 긴 내용을 주석에 포함하기 위해서 연속되는 여러 줄에 이 주석을 사용하는 것은 안되지만, 어떤 코드의 일부분을 주석 처리하기 위해서 여러 줄에 연속해서 사용하는 것은 허락된다.

```java
if (foo > 1) {

// double-flip을 실행한다.
...
} else {
return false; // 이유를 여기에 설명한다.
} 
//if (bar > 1) { 
//
//   // double-flip을 실행한다.
// ...
//}
//else {
// return false;
//}
```

### 문서화(Documentation) 주석
여기에 나오는 주석들은 아래 "11장 1절 자바 소스 파일 예제" 를 참고하기 바란다.

문서화 주석은 다음 5가지를 설명한다.

- 자바 클래스
- 인터페이스
- 생성자
- 메서드
- 필드

각각의 문서화 주석은 주석 경계 기호인 /** ... */ 안으로 들어간다. 그리고 각각의 문서화 주석은 클래스, 인터페이스 그리고 멤버 당 하나씩 가진다. 문서화 주석은 선언 바로 전에 나와야 한다. 다음 예제를 살펴보자

```java
/**
* Example 클래스는 ...
*/ 
public class Example { ...
```

처음 나오는 클래스와 인터페이스들은 들여쓰지 않는 반면에 그들의 멤버들은 들여쓰기를 한다. 클래스에 대한 문서화 주석(/**)의 첫 번째 줄은 들여쓰지 않는다. 그 다음에 나오는 문서화 주석은 별표를 수직으로 맞추기 위해 각각 1개의 빈 칸을 들여쓰기를 한다. 생성자를 포함한 멤버들은 문서화 주석 첫 줄에서는 4개의 빈 칸을 들여쓰기 하고, 그 이후에는 5개의 빈 칸으로 들여쓰기를 한다.

만약 클래스, 인터페이스, 변수 또는 메서드에 대한 어떤 정보를 제공하고 싶지만 문서화 주석에 어울리지 않는다고 생각된다면, 클래스 선언 바로 후에 블록 주석("5장 1.1절 블록(Block) 주석") 또는 한 줄 주석("5장 1.2절 한 줄(Single-Line) 주석")을 사용한다. 예를 들어, 클래스의 구현에 대한 세부 사항들은 클래스에 대한 문서화 주석이 아니라, 클래스 선언문 다음에 블록 주석을 사용해야 한다.

자바는 문서화 주석을 주석 이후에 처음 나오는 선언문과 연결시키기 때문에 문서화 주석은 메서드 또는 생성자 구현 안에 위치해서는 안 된다.

## 선언

### 한 줄당 선언문의 수

한 줄에 하나의 선언문을 쓰는 것이 주석문 쓰는 것을 쉽게 해주기 때문에 한 줄에 하나의 선언문을 쓰는 것이 좋다.

```java
int level; // 들여쓰기 단위
int size; // 테이클 크기
```

위와 같이 쓰는 것이 아래와 같이 쓰는 것보다 좋다.

```java
int level, size;
```

같은 줄에 서로 다른 타입을 선언하면 안 된다.

```java
int foo,  fooarray[]; //절대 이렇게 사용하지 말자
```

위의 예제는 타입과 변수 이름사이에 하나의 space를 두었다. 또 다른 사용 가능한 방법은 다음과 같이 탭을 사용하는 것이다.

```java
int         level;                // 들여쓰기 단위
int         size;                 // 테이블 크기
Object      currentEntry;         // 테이블에서 현재 선택된 데이터
```

### 초기화

지역 변수의 경우, 지역 변수를 선언할 때 초기화 하는 것이 좋다. 변수의 초기화 값이 다른 계산에 의해서 결정되는 경우라면, 변수를 선언할 때 초기화 하지 않아도 괜찮다.

### 배치

선언은 블록의 시작에 위치해야 한다(보통 블록은 중괄호 "{ }" 로 둘러싸인 코드를 의미한다). 변수를 처음 사용할 때까지 변수의 선언을 미루지 말자. 이러한 경우 부주의한 프로그래머들은 혼돈에 빠질 수 있고, 영역내에서 코드를 이동해야 하는 경우에 문제를 야기시킬 수 있다.

```java
void myMethod() {
    int int1 = 0; // 메서드 블록의 시작

    if (condition) {
        int int2 = 0; // "if" 블록의 시작
        ... 
    } 
}
```

이러한 원칙에도 예외는 존재한다. 그 중 하나가 for 문에서 선언하는 반복문을 위한 인데스이다.

```java
for (int i = 0; i < maxLoops; i++) { ... }
```

상위 영역에서 선언된 것을 숨기기 위해서 블록의 처음 부분에서 다시 선언하는 것은 피해야 한다. 예를들어, 블록 안의 블록에서 동일한 변수 이름을 사용해서 선언하지 말아야 한다.

```java
int count;
...
myMethod() {
    if (condition) {
        int count = 0; // 이렇게 사용하지 말 것!
        ...
    }
    ...
}
```

### 클래스와 인터페이스의 선언

자바 클래스와 인터페이스를 선언할 때, 다음 3가지 원칙을 따르도록 하자

 - 메서드 이름과 그 메서드의 파라미터 리스트의 시작인 괄호 "(" 사이에는 빈 공간이 없어야 한다.
 - 여는 중괄호 "{" 는 클래스/인터페이스/메서드 선언과 동일한 줄의 끝에 사용하자
 - 닫는 중괄호 "}" 는 여는 중괄호 "{" 후에 바로 나와야 하는 null 문의 경우를 제외하고는, 여는 문장과 동일한 들여쓰기를 하는 새로운 줄에서 사용하자
 - 메서드들을 구분하기 위해서 각 메서드들 사이에는 한 줄을 비우도록 하자

 ```java
 class Sample extends Object {
    int ivar1;
    int ivar2;
 
    Sample(int i, int j) {
        ivar1 = i;
        ivar2 = j;
    }
 
    int emptyMethod() {}
 
    ...
}
 ```

## 문 (Statements)

### 간단한 문

각각의 줄에는 최대한 하나의 문(statement)만 사용하도록 한다.

```java
argv++;       // 올바른 사용법
argc--;       // 올바른 사용법  
argv++; argc--;       // 이렇게 작성하는 것은 피해라
```

### 복합 문

복합문은 중괄호 "{ statements }" 로 둘러싸여진 문들의 리스트를 포함하는 문이다. 이 리스트에 포함될 수 있는 문들은 다음 절에서부터 하나 하나 예를들어 설명하겠다. 다음 원칙을 따르자

- 둘러싸여진 문들은 복합문보다 한 단계 더 들여쓰기를 한다.
- 여는 중괄호 "{" 는 복합문을 시작하는 줄의 마지막에 위치해야 한다.
- 닫는 중괄호 "}" 는 새로운 줄에 써야하고, 복합문의 시작과 같은 들여쓰기를 한다.
- 중괄호들이 if-else 문이나 for 문 같은 제어 구조의 일부분으로 사용되어질 때에는 중괄호들이 모든 문들(단 하나의 문일 경우에도)을 둘러싸는데 사용되어져야 한다(이렇게 사용하는 것이 중괄호를 닫는 것을 잊어버리는 것 때문에 발생하는 버그를 만들지 않고, 문을 추가하는 것에 큰 도움을 준다).

### return 문

값을 반환하는 return 문은 특별한 방법으로 더 확실한 return 값을 표현하는 경우를 제외하고는 괄호를 사용하지 않는 것이 좋다.

```java
return;
return myDisk.size();
return (size ? size : defaultSize);
```

### if, if-else, if else-if else 문

if-else 문을 사용할 때는 다음과 같이 작성한다.

```java
if (condition) {
    statements; 
} 

if (condition) {
    statements;
} else {
    statements; 
}

if (condition) {
    statements; 
} else if (condition) {
    statements; 
} else {
    statements;
}
```

\* if 문은 항상 중괄호를 사용한다. 다음과 같은 에러가 발생할 수 있는 상황은 피해야 한다.

```java
if (condition) // 이렇게 중괄호 {}를 생략해서 사용하지 말자
    statement;
```

### for 문

for 문은 다음과 같이 작성한다.

```java
for (initialization; condition; update) {
    statements;
}
```

빈 for 문(모든 작업이 initialization, condition, update 에서 완료되는)은 다음과 같은 형태를 가져야 한다.

```java
for (initialization; condition; update);
```

for 문의 initialization 또는 update 부문에서 콤마(,) 연산자를 사용할 때에는 세개 이상의 변수들을 사용하는 복잡성은 피해야 한다. 만약 필요하다면, for 문 이전에 문을 분리시켜 사용(initialization절의 경우)하거나 for 문의 마지막에 문을 분리시켜 사용(update절의 경우)한다.

### while 문

while 문은 다음과 같이 작성한다.

```java
while (condition) {
    statements;
}
```

빈 while 문은 다음과 같이 작성한다.

```java
while (condition);
```

### do-while 문

do-while 문은 다음과 같이 작성한다.

```java
do {
    statements;
} while (condition);
```

### switch 문

switch 문은 다음과 같이 작성한다.

```java
switch (condition) {
case ABC:
    statements;
    /* 다음줄로 계속 진행한다. */
  
case DEF:
    statements;
    break;
  
case XYZ:
    statements;
    break;
  
default:
    statements;
    break;
}
```

모든 case를 수행해야 하는 경우에는 break 문을 사용하지 않으면 된다. 이러한 경우는 위의 예제 코드의 첫번째 case에서 볼수 있다.

모든 switch 문은 default case를 포함해야 한다. 위의 예제와 같이, 어떤 경우에 default case에서 break는 중복적이지만, 이후에 또 다른 case가 추가되어질 경우 에러를 방지할 수 있다.

### try-catch 문

try-catch 문은 다음과 같이 작성한다.

```java
try {
    statements;
} catch (ExceptionClass e) {
    statements;
}
```

try-catch 문은 try 블록이 성공적으로 완료되든지, 아니면 중간에 에러가 발생하든지에 상관없이 실행되어야 하는 부분을 추가하기 위해서 finally 부분을 사용할 수 있다.

```java
try {
    statements;
} catch (ExceptionClass e) {
    statements;
} finally {
    statements;
}
```

## 빈 공간

### 한 줄 띄우기 (Blank Lines)

한 줄을 띄우고 코드를 작성하면, 논리적으로 관계가 있는 코드들을 쉽게 구분할 수 있기 때문에 코드의 가독성(readability)을 향상시킨다.

다음과 같은 경우에는 한 줄을 띄어서 코드를 작성한다.

- 메서드들 사이에서
- 메서드 안에서의 지역 변수와 그 메서드의 첫 번째 문장 사이에서
- 블록(Block) 주석 또는 한 줄(Single-Line) 주석 이전에
- 가독성을 향상시키기 위한 메서드 내부의 논리적인 섹션들 사이에

다음과 같은 경우에는 두 줄을 띄어서 코드를 작성한다.

- 소스 파일의 섹션들 사이에서
- 클래스와 인터페이스의 정의 사이에서

### 공백 (Blank Spaces)

공백은 다음과 같은 경우에 사용한다.

- 괄호와 함께 나타나는 키워드는 공백으로 나누어야 한다.

```java
while (true) {
...
}
```

- 메서드 이름과 메서드의 여는 괄호 사이에 공백이 사용되어서는 안 된다는 것을 명심하자. 이렇게 하는 것은 메서드 호출과 키워드를 구별하는데 도움을 준다.

- 공백은 인자(argument) 리스트에서 콤마 이후에 나타나야 한다.

- .을 제외한 모든 이항(binary) 연산자는 연산수들과는 공백으로 분리되어져야 한다. 공백은 단항 연산자(++ 혹은 --)의 경우에는 사용해서는 안 된다.

```java
a += c + d;
a = (a + b) / (c * d);

while (d++ = s++) {
    n++;
}
printSize("size is " + foo + "\n");
```

- for 문에서 사용하는 세 개의 식(expression) 들은 공백으로 구분해서 나누어야 한다.

```java
for (expr1; expr2; expr3)
```

- 변수의 타입을 변환하는 캐스트(cast)의 경우에는 공백으로 구분해야 한다.

```java
myMethod((byte) aNum, (Object) x);
myMethod((int) (cp + 5), ((int) (i + 3)) + 1);
```

## 명명(Naming) 규칙

명명 규칙, 즉 이름을 정하는 규칙은 프로그램을 더 읽기 쉽게 만들어 줌으로써 더 이해하기 쉽게 만들어 준다. 또한 식별자(identifier)를 통해서 기능에 대한 정보도 얻을 수 있다. 예를 들자면, 그것이 상수인지 패키지인지 클래스인지를 알 수 있도록 도와준다. 이러한 정보는 코드를 이해하는데 큰 도움이 된다.

본 장에서 소개할 명명 규칙의 식별자 타입은 다음 6가지이다.

- Packages
- Classes
- Interfaces
- Methods
- Variables
- Constants

### Package

명명 규칙은 다음과 같다.

- 패키지 이름의 최상위 레벨은 항상 ASCII 문자에 포함되어 있는 소문자로 쓰고, 가장 높은 레벨의 도메인 이름 중 하나이어야 한다.
- 현재는 com, edu, gov, mil, net, org, 또는 1981년 ISO Standard 316에 명시된 영어 두 문자로 표현되는 나라 구별 코드가 사용된다.
- 패키지 이름의 나머지 부분은 조직 내부의 명명 규칙을 따르면 된다. 이러한 규칙을 따라 만들어진 이름은 디렉토리 구조에서 디렉토리 이름으로도 사용된다.
- 예를 들면 부서명, 팀명, 프로젝트명, 컴퓨터 이름, 또는 로그인 이름 등이다.

예제는 다음과 같다.

- com.sun.eng
- com.apple.quicktime.v2
- edu.cmu.cs.bovik.cheese

### Classes

명명 규칙은 다음과 같다.

- 클래스 이름은 명사이어야 하며, 복합 단어일 경우 각 단어의 첫 글자는 대문자이어야 한다.
- 클래스 이름은 간단하고 명시적으로 작성해야 한다.
- 완전한 단어를 사용하고 두 문자어와 약어는 피하도록 한다(만약, 약어가 URL이나 HTML과 같이 더 많이 ,더 넓게 사용되고 있다면 약어를 사용하는 것도 괜찮다).

예제는 다음과 같다.

- class Raster;
- class ImageSprite;

### Interfaces

명명 규칙은 다음과 같다.

- 인터페이스 이름도 클래스 이름과 같은 대문자 사용 규칙을 적용해야 한다.

예제는 다음과 같다.

- interface RasterDelegate;
- interface Storing;

### Methods

명명 규칙은 다음과 같다.

- 메서드의 이름은 동사이어야 하며, 복합 단어일 경우 첫 단어는 소문자로 시작하고 그 이후에 나오는 단어의 첫 문자는 대문자로 사용해야 한다.

예제는 다음과 같다.

- run();
- runFast();
- getBackground();

### Variables

명명 규칙은 다음과 같다.

- 변수 이름의 첫 번째 문자는 소문자로 시작하고, 각각의 내부 단어의 첫 번째 문자는 대문자로 시작해야 한다.
- 변수 이름이 언더바 (_) 또는 달러 표시 문자로 시작하는 것이 허용되기는 하지만, 이 문자들로 시작하지 않도록 주의하자.
- 이름은 짧지만 의미 있어야 한다.
- 이름의 선택은 그 변수의 사용 의도를 알아낼 수 있도록 의미적이어야 한다.
- 한 문자로만 이루어진 변수 이름은 암시적으로만 사용하고 버릴 변수일 경우를 제외하고는 피해야 한다.
- 보통의 임시 변수들의 이름은 integer 일 경우에는 i, j, k, m, n을 사용하고, character 일 경우에는 c, d, e를 사용한다.

예제는 다음과 같다.

- int i;
- char c;
- float myWidth;

### Constants

명명 규칙은 다음과 같다.

- 클래스 상수로 선언된 변수들과 ANSI 상수들의 이름은 모두 대문자로 쓰고 각각의 단어는 언더바("_")로 분리 해야 한다.
- 디버깅을 쉽게 하기 위해서 ANSI 상수들의 사용은 자제하도록 한다.

에제는 다음과 같다.

- static final int MIN_WIDTH = 4;
- static final int MAX_WIDTH = 999;
- static final int GET_THE_CPU = 1;
