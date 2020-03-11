[<인프런 자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!>]([https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94_java-renew](https://www.inflearn.com/course/실전-자바_java-renew))

# 1. Java 프로그래밍이란?

## 1-1. 프로그래밍이란?

- 컴퓨터에 일을 시키는 것
- 개발자 - 소스코드 - 컴파일러/인터프리터 - 기계어

## 1-2. Java 언어의 탄생

- 1995년 제임스 고슬링(James Gosling)
- 오크(Oak) 언어에서 시작해서 발전
- 가전제품에 탑재할 수 잇는 프로그램을 개발하기 위한 목적으로 탄생하였으나, 웹 중심의 언어로 확산되었음

## 1-3. Java 언어의 특징

- 초창기 Java 단점
  - 기존 C/C++에 비해 속도가 굉장히 느림
    - C/C++ 은 메모리에 직접 접근하여 제어할 수 있는 반면 Java는 중간 매개체를 거쳐야 하기 때문
  - 리소스(메모리, CPU)를 많이 사용
- 현재 Java 장점
  - 객체 지향 언어로 모듈화 가능
  - JRE를 이용하여 운영체제로부터 자유로움
  - 웹 및 모바일(안드로이드) 프로그래밍이 쉬움
  - GC(garbage collector)를 통한 자동 메모리 관리 지원
  - 실행 속도 개선

## 1-4. Java 프로그래밍을 위한 기본 준비물

- [JDK (Java Development Kit) 설치](https://oracle.com)
  - *Download Java SE for developer*
  - JVM < API < JRE < JDK
    - JVM (Java Virtual Machine): JVM을 실행함으로써 실제 Java 프로그램을 실행
    - API: JVM 컴파일을 위한 API
    - JRE (Java Runtime Environment): Java 프로그램이 실행될 수 있는 환경 마련
      - **Java 프로그램 사용자는 JRE만 설치하면 됨** 
      - OS 별로 다른 JRE 설치해야 함
    - JDK: Java 프로그램을 개발을 위해 필요
- [IDE (Integrated Development Environment): **Eclipse** 설치](https://eclipse.org)
  - *Eclipse IDE for Java EE developers*
  - 프로그래밍 과정을 편리하게 해주는 툴

## 1-5. Hello Java World!

- Project Explorer 우클릭 - New - Project - Java Project - [프로젝트명 입력] 

  - `src`: 소스코드 파일
  - `bin`: 컴파일 된 파일

- src 우클릭 - New - Class - Name 란 "MainClass" 입력

  - Java 프로젝트를 실행하면 프로젝트 내 여러 파일 중에서 main 메서드를 찾아서 가장 먼저 실행

  - 저장하는 순간 컴파일됨

```java
package [프로젝트명]
 
public class MainClass {
  public static void main(String[] args){
    System.out.println("Hello Jave World!");
  }
}
```

- 프로젝트명 우클릭 - run as - java application

# 끝.

