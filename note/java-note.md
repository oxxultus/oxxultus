### 자바 파일 작성 방법

#### 필수 요구
- **한 개 이상의 클래스**가 있어야 한다.
- **한 개 이상의 main 메소드**가 있어야 한다.
- 자바는 **모든 것이 클래스 안**에 있어야 한다.

#### 자바 명명 규칙

| 구분      | 케이스 유형     | 예시                                        |
| ------- | ---------- | ----------------------------------------- |
| **상수**  | UPPERCASE  | `public static final int MAX_SIZE = 100;` |
| **변수**  | lowercase  | `int age;`                                |
|         | camelCase  | `String studentName;`                     |
| **메서드** | camelCase  | `public void calculateSum() { ... }`      |
| **클래스** | PascalCase | `public class StudentInfo { ... }`        |
| **패키지** | lowercase  | `package com.example.myapp;`              |

#### 자바 키워드 순서 (PSF) 규칙

| 순서       | 구분     | 사용 가능한 키워드                       | 예시 코드                                      |
| -------- | ------ | -------------------------------- | ------------------------------------------ |
| **P**    | 접근 제어자 | `private`, `public`, `protected` | `public int age;`                          |
| **S**    | 기타 키워드 | `static`, `abstract`, ...        | `private static String name;`              |
| **F**    | 제한자    | `final`, `synchronized`, ...     | `protected final double PI = 3.14;`        |
| **Type** | 변수 형식  | `int`, `String`, `double`, 등     | `private static final int MAX_SIZE = 100;` |

예시) main 메서드 `public(P) static(S) void(Type) main(String []args){}`
- 자바 파일의 모든 것은 메인 메서드에서 시작함

#### Maven 프로젝트

##### Maven이란?
Maven은 Java 기반의 프로젝트 관리 및 빌드 도구로, 소프트웨어 프로젝트의 빌드, 문서화, 보고서 작성, 의존성 관리 등을 자동화하는 데 사용됩니다. Maven은 Apache 소프트웨어 재단에서 개발하였으며, 표준화된 프로젝트 구조와 빌드 프로세스를 제공하여 개발자들이 보다 쉽게 프로젝트를 관리할 수 있도록 돕습니다.

##### 주요 특징
1. **의존성 관리**: Maven은 프로젝트에서 사용하는 라이브러리와 프레임워크의 버전을 관리합니다. `pom.xml` 파일에 의존성을 선언하면 Maven이 해당 라이브러리를 자동으로 다운로드하고, 프로젝트에 포함시킵니다.

2. **표준화된 빌드 프로세스**: Maven은 일관된 빌드 생명 주기를 제공하여 복잡한 빌드 과정을 단순화합니다. Maven의 빌드 생명 주기에는 초기화, 컴파일, 테스트, 패키징, 배포 등 여러 단계가 포함됩니다.

3. **프로젝트 구조**: Maven은 특정한 프로젝트 구조를 권장하여 코드와 자원 파일들이 잘 정리될 수 있도록 합니다. 이 구조는 팀 내에서 일관성을 유지하는 데 도움이 됩니다.

4. **플러그인 시스템**: Maven은 다양한 플러그인을 통해 기능을 확장할 수 있습니다. 이러한 플러그인은 빌드, 테스트, 배포 및 문서화와 같은 작업을 지원합니다.

##### pom.xml의 주요 요소
- **groupId**: 프로젝트의 그룹 식별자.
- **artifactId**: 프로젝트의 아티팩트(산출물) 식별자.
- **version**: 프로젝트 버전.
- **dependencies**: 프로젝트에서 사용하는 외부 라이브러리의 목록.

#### 자바 파일 유형

| 유형      | 의미                      | 용도 및 설명                                                                                                                                                                  |
| ------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **JAR** | Java Archive            | - **Java** 프로그램과 관련된 클래스 파일 및 리소스를 하나로 묶은 압축 파일<br>- 일반적으로 라이브러리나 애플리케이션 배포에 사용됨<br>- 내부에 `META-INF` 디렉터리 포함 (메타데이터 및 매니페스트 파일 저장)                                       |
| **WAR** | Web Application Archive | - **JSP**(Java Server Pages) 기반 웹 애플리케이션을 배포하기 위한 압축 파일<br>- 웹 애플리케이션에 필요한 모든 파일(서블릿, JSP, HTML, CSS, JS 등)과 설정 파일 포함<br>- **웹 서버**나 **애플리케이션 서버**(예: Tomcat)에 배포할 때 사용됨 |



---
### 변수
#### 변수 종류

| 종류            | 설명                                                               | 예시 코드                                |
|----------------|--------------------------------------------------------------------|------------------------------------------|
| **매개변수 (Parameter)** | 메소드 호출 시 전달된 **인수(값)**를 받기 위해 사용되는 변수 | `public void setName(String name) { ... }` |
| **지역 변수 (Local Variable)** | 메소드 내부에서 선언되어 해당 **메소드 내에서만 유효**한 변수 | `void calculate() { int sum = 0; ... }` |
| **정적 변수 (Static Variable)** | 클래스에 **속한 변수**로 모든 인스턴스가 공유 | `static int counter = 0;`                |
| **인스턴스 변수 (Instance Variable)** | 객체마다 개별적으로 가지며, **객체의 상태**를 나타냄 | `private String studentName;`            |
#### 변수 종류와 특징

| 종류            | 선언 위치            | 초기화                                      | 예시 코드                                |
|----------------|---------------------|--------------------------------------------|------------------------------------------|
| **매개변수 (Parameter)**             | 메서드 정의 시 | 메서드 호출 시 **값 복사** <br>(호출 시 인자가 없으면 컴파일 오류 발생) | `public void setAge(int age) { ... }` |
| **지역 변수 (Local Variable)**       | 메서드 내      | 기본 초기값이 없음 (사용 전 초기화 필요)   | `void method() { int count = 0; }`      |
| **정적 변수 (Static Variable)**      | 클래스 내      | 클래스 로딩 시 초기화 가능 <br>모든 인스턴스에서 공유됨 | `static int counter = 0;`               |
| **인스턴스 변수 (Instance Variable)** | 클래스 내      | 기본 초기값이 있음 (`int` → 0, `String` → null 등) | `private String name;`                   |
#### == 비교 연산자

| 구분                 | 설명                            | 예시 코드                                                                                                                                                                                                                                                    |
| ------------------ | ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **원시값 비교**         | 두 원시 타입 변수의 값을 단순히 비교합니다.     | `int a = 5;`<br>`int b = 5;`<br>`System.out.println(a == b); // true`                                                                                                                                                                                    |
| **레퍼런스(참조 변수) 비교** | 두 참조 변수가 같은 객체를 참조하는지를 비교합니다. | `String str1 = new String("Hello");`<br>`String str2 = new String("Hello");`<br>`String str3 = str1;`<br>`System.out.println(str1 == str2); // false`<br>`System.out.println(str1.equals(str2)); // true`<br>`System.out.println(str1 == str3); // true` |

---
### 배열

| 구분          | 배열 유형                 | 배열 생성 및 초기화 예시                                                                                                                                              | 설명                                  |
| ----------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| **원시 변수**   | **정수형 배열 (int)**      | `int[] intArray = new int[5];` <br> `intArray[0] = 1;` <br> `intArray[1] = 2;` <br> `intArray[2] = 3;` <br> `intArray[3] = 4;` <br> `intArray[4] = 5;`      | 배열 크기를 지정하여 생성한 후, 각 요소를 개별적으로 초기화. |
|             |                       | `int[] intArray = {1, 2, 3, 4, 5};`                                                                                                                         | 배열 생성 시 초기값을 한 번에 제공하는 방법.          |
|             | **문자형 배열 (char)**     | `char[] charArray = new char[3];` <br> `charArray[0] = 'a';` <br> `charArray[1] = 'b';` <br> `charArray[2] = 'c';`                                          | 배열 생성 후 각 요소를 개별적으로 초기화.            |
|             |                       | `char[] charArray = {'a', 'b', 'c'};`                                                                                                                       | 배열 생성 시 초기값을 한 번에 제공하는 방법.          |
|             | **부동소수점 배열 (double)** | `double[] doubleArray = new double[4];` <br> `doubleArray[0] = 1.1;` <br> `doubleArray[1] = 2.2;` <br> `doubleArray[2] = 3.3;` <br> `doubleArray[3] = 4.4;` | 배열 생성 후 각 요소를 개별적으로 초기화.            |
|             |                       | `double[] doubleArray = {1.1, 2.2, 3.3, 4.4};`                                                                                                              | 배열 생성 시 초기값을 한 번에 제공하는 방법.          |
| **레퍼런스 변수** | **문자열 배열 (String)**   | `String[] strArray = new String[3];` <br> `strArray[0] = "Hello";` <br> `strArray[1] = "World";` <br> `strArray[2] = "Java";`                               | 배열 생성 후 각 요소를 개별적으로 초기화.            |
|             |                       | `String[] strArray = {"Hello", "World", "Java"};`                                                                                                           | 배열 생성 시 초기값을 한 번에 제공하는 방법.          |
|             | **객체 배열 (예: Person)** | `Person[] personArray = new Person[10];` <br> `personArray[0] = new Person();` <br> `personArray[1] = new Person();`                                        | 객체 배열 생성 후, 각 요소에 객체를 초기화.          |
|             |                       | `Person[] personArray = {new Person(), new Person()};`                                                                                                      | 배열 생성 시 초기값을 한 번에 제공하는 방법.          |

---
### 자바 입출력
#### 입력

#### 출력
##### 1. System.out.println()
- **설명**: 표준 출력으로 값을 출력하고, 자동으로 줄 바꿈을 수행합니다.
- **예시**:
``` java
System.out.println(name + " 안녕");
```
##### 2. System.out.print()
- **설명**: 표준 출력으로 값을 출력하지만 자동 줄 바꿈이 없습니다. 수동으로 줄 바꿈을 원할 경우 `\n` 또는 `%n`을 추가해야 합니다.
- **예시**:
``` java
System.out.print(name + " 안녕\\n");
```
##### 3. System.out.printf()
- **설명**: C 언어의 `printf`와 유사한 방식으로 문자열을 형식화하여 출력합니다. 자동으로 줄 바꿈이 되지 않으며, 줄 바꿈을 위해 `%n`을 사용합니다.
- **예시**:
``` java
System.out.printf("%s 안녕?%n", name);
```
##### 4. String.format()
- **설명**: 문자열을 형식화하여 새로운 문자열을 생성하는 정적 메서드입니다.
- **예시**:
``` java
String phrase = String.format("%s %s %s", name, name, name);
```


---
### 라이브러리

#### Stream
##### BufferedReader
- **설명**: `BufferedReader`는 문자 입력 스트림에서 버퍼링을 통해 텍스트를 읽는 클래스입니다.
- **특징**:
  - 문자 단위로 데이터를 효율적으로 읽을 수 있도록 버퍼를 사용합니다.
  - 파일 읽기 및 표준 입력 처리 시 사용됩니다.
  - 읽기 작업을 최적화하여 성능을 개선합니다.
- **사용 예**:
```java
  BufferedReader reader = new BufferedReader(new FileReader("file.txt"));
  String line;
  while ((line = reader.readLine()) != null) {
      System.out.println(line);
  }
  reader.close();
```
- charhachter input stream 문자 입력 흐름으로부터 버퍼링을 통해 텍스트를 읽는 클래스

##### InputStreamReader
- **설명**: `InputStreamReader`는 `InputStream` 객체가 생성하는 바이트 스트림을 문자 스트림으로 변환해주는 연결 클래스입니다.
- **특징**:
 - 바이트 기반 입력 스트림을 문자 기반 입력 스트림으로 변환합니다.
 - 주로 파일이나 표준 입력에서 바이트 데이터를 읽을 때 사용됩니다.
 - 특정 문자 인코딩을 지정하여 바이트를 문자로 변환할 수 있습니다.
```java
InputStreamReader isr = new InputStreamReader(System.in);
BufferedReader reader = new BufferedReader(isr);
String input = reader.readLine();
```

- **System.in**: 표준 입력 스트림으로, 주로 키보드 입력을 처리합니다.
- **System.out**: 표준 출력 스트림으로, 콘솔에 데이터를 출력합니다.
- **System.err**: 표준 오류 스트림으로, 오류 메시지를 출력하는 데 사용됩니다.

---
### TIPS

#### 리턴 값의  사용 여부
- 리턴 값의 사용 여부에는 전혀 신경 쓰지 않아도 됩니다. 
- 다만 메서드 정의 시 반환 값을 정의해둔 경우 사용하는 것이 좋습니다.

#### 전역 메서드에 관해
- 자바의 객체 지향 프로그래밍에서는 전역 변수나 전역 메서드의 개념이 존재하지 않습니다. 
- 대신, 클래스 메서드와 클래스 변수를 사용하여 이와 유사한 기능을 구현할 수 있습니다.
- **public static 메서드**: 클래스에 속하며, 인스턴스를 생성하지 않고도 호출할 수 있습니다. 다른 클래스에서 쉽게 접근할 수 있는 특징이 있습니다.
- **public static final(상수)**: 전역 변수를 대체하는 개념으로, 값이 변하지 않는 상수를 정의할 수 있습니다. 이러한 상수는 클래스의 모든 인스턴스에서 공유되며, 전역적으로 접근 가능합니다.

#### 형 변환과 overflow
- **작은 크기의 변수**를 **큰 크기의 변수**에 대입할 수 있다.  
  (예: `int` → `long`)
  
- **큰 크기의 변수**를 **작은 크기의 변수**에 대입할 때는 **오버플로우(Overflow)**가 발생할 수 있다.  
  - 예: `long` 값을 `int` 변수에 대입할 때 데이터 손실이 발생.

#### 접근 제어자
| 접근 제어자        | 접근 가능성                  | 설명                                            |
| ------------- | ----------------------- | --------------------------------------------- |
| **public**    | 모든 클래스에서 접근 가능          | 어떤 클래스에서도 접근할 수 있으며, 다른 패키지에서도 가능.            |
| **protected** | 같은 패키지 및 자식 클래스에서 접근 가능 | 상속 관계에 있는 클래스에서 접근할 수 있으며, 패키지 내에서 허용.        |
| **default**   | 같은 패키지 내에서만 접근 가능       | 접근 제어자가 명시되지 않으면 기본적으로 적용되며, 다른 패키지에서는 접근 불가. |
| **private**   | 해당 클래스 내에서만 접근 가능       | 외부 클래스에서는 접근할 수 없으며, 데이터 은닉을 위해 사용됨.          |

| 접근 제어자           | 동일 클래스 | 동일 패키지 | 하위 클래스 | 전체 접근 |
| ---------------- | ------ | ------ | ------ | ----- |
| **private**      | 0      | X      | X      | X     |
| **default (기본)** | 0      | 0      | X      | X     |
| **protected**    | 0      | 0      | 0      | X     |
| **public**       | 0      | 0      | 0      | 0     |

#### 자바의 while() 구문
- **설명**: `while` 구문은 주어진 조건이 `true`인 동안 반복 실행되는 루프 구조입니다.
- **조건**: `while()` 괄호 안에는 반드시 **boolean 형**의 값이나 boolean 표현식이 들어가야 합니다. 이 조건이 `true`일 경우에만 반복문이 실행됩니다.
##### 구문
```java
while (조건) {
    // 반복 실행할 코드
}
```

---
### 핵심 정리

#### 2장
- 객체 지향 프로그래밍을 하면 제작과 테스트 과정이 끝난 코드를 건드리지 않고도 프로그램을 확장할 수 있습니다.
- 모든 자바 코드는 클래스 내에서 정의 됩니다
- 클래스 는 설계도와 같다고 할 수 있다.
- 사용자는 객체가 작업 처리하는 방법에 대해 신경 쓰지 않아도 됨
- 객체는 **알고 있는 것(상태: state)** 과 **할 수 있는 것(행동: behavior)** 이 있습니다.
- 객체가 자기 자신에 대해 알고 있는 것은 **인스턴스 변수(멤버 변수, 필드)** 라고 부릅니다. 객체의 **상태( state)** 를 나타낸다.
- 객체가 할 수 있는 것은 **메서드(멤버함수)** 라고 부릅니다. 객체의 **행동(behavior)** 을 나타냅니다
- 클래스를 새로 만들 때는 그 클래스 타입의 테스트용 클래스를 따로 만드는 것이 좋다
- 클래스에서는 덜 구체적인 상위 클래스로부터 인스턴스 변수와 메서드를 상속할 수 있다.

#### 3장
- 변수에는 원시 변수와 레퍼런스 변수가 있습니다.
- 변수를 선언할 때는 이름과 타입(유형)이 필요합니다.
- 원시 변수의 값은 그 값을 표시하는 비트로 구성됩니다.
- 레퍼런스 변수의 값은 힙에 들어있는 객체에 접근할 수 있는 방법을 나타내는 비트입니다.
- 레퍼런스 변수는 리모컨과 같습니다. 레퍼런스 변수에 대해 점 연산자를 사용하는 것은 리모컨을 버튼을 눌려서 메서드나 인스턴스 변수를 액세스 하는 것과 같습니다.
- 레퍼런스 변수가 아무 객체도 참조하지 않으면 그 값은 null이 됩니다.
- 모든 배열은 객체입니다.

#### 4장
- 클래스에는 객체가 하는 것(행동)과 객체가 아는 것(상태)을 정의합니다.
- 메서드에서 인스턴스 변수를 이용하여 같은 형식의 객체가 다른 식으로 행동하도록 할 수 있습니다.
- 메소드에서 매개변수를 사용할 수 있습니다. 즉 메서드에 한 개 이상의 값을 전달할 수 있습니다.
- 전달하는 값의 개수와 유형은 반드시 메서드 선언할 때 지정한 것과 같아야 하며 그 순서도 같아야 합니다
- 메서드 안팎으로 전달되는 값은 상황에 따라 자동으로 더 큰 유형으로 올라갈 수 있습니다. (자동 형 변환 및 강제 형 변환 타입 캐스팅 )
- 메서드에 인자를 전달할 때는 리터럴값(인스턴스, 메서드 이름) 을 사용할 수도 있고 선언된 매개변수 유형의 변수를 사용할 수 있습니다.
- 메서드를 선언할 때에는 반드시 리턴 유형을 지정해야 합니다. 리턴 유형을 void로 지정하면  아무것도 리턴 하지 않아도 됩니다.
- 메서드를 선언할 때 void 가 아닌 리턴 유형을 지정 했을 때는 반드시 선언된 리턴 유형과  호환 가능 한 값을 리턴 해야 합니다.

---