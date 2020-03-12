# 1. 상속

## 1-1. 상속이란?

- 부모 클래스를 상속받은 자식 클래스는 부모 클래스의 속성과 기능도 이용 가능

## 1-2. 상속의 필요성

- 기존의 검증된 class를 이용해서 빠르고 쉽게 새로운 class를 만들 수 있음

## 1-3. 상속 구현

- `public class ChildClass extends ParentClass {...}`
  - ChildClass 생성시 **ParentClass 가 먼저 생성됨**
- **Java 는 다중 상속을 지원하지 않음**

## 1-4. 부모 클래스의 private 접근자

- 자식 클래스는 부모 클래스의 모든 자원을 사용할 수 있지만 private 접근자의 속성과 메서드는 사용 불가함

# 2. 상속 특징

## 2-1. 메서드 오버라이드(override)

- 부모 클래스의 기능을 자식 클래스에서 재정의해서 사용

```java
// parent
public class ParentClass {
  public void makeJJajang() {
    System.out.println("makeJJajang() START");
  }
}

// child
public class ChildClass extends ParentClass {
  @Override // 작성하지 않아도 무방하지만 가독성을 위해 작성
  public void makeJJajang() {
    System.out.println("more delicious makeJJajang() START");
  }
}
```



## 2-2. 자료형(타입)

- 기본 자료형처럼 클래스도 자료형
- 자식 클래스의 타입은 자식 클래스 자신일 수도 있지만 부모 클래스가 될 수도 있음

```java
// parent
public class ParentClass {
  public ParentClass() {
    System.out.println("ParentClass constructor");
  }
  public void makeJJajang() {
    System.out.println("makeJJajang() START");
  }
}

// FirstChild
public class FirstChildClass extends ParentClass {
  public FirstChildClass() {
    System.out.println("FirstChildClass constructor");
  }
  @Override // 작성하지 않아도 무방하지만 가독성을 위해 작성
  public void makeJJajang() {
    System.out.println("FirstChildClass's makeJJajang() START");
  }
}

// SecondChild
public class SecondChildClass extends ParentClass {
  public SecondChildClass() {
    System.out.println("SecondChildClass constructor");
  }
  @Override // 작성하지 않아도 무방하지만 가독성을 위해 작성
  public void makeJJajang() {
    System.out.println("SecondChildClass's makeJJajang() START");
  }
}

// MainClass
ParentClass[] pArr = new ParentClass[2];

ParentClass fch = new FirstChildClass;
ParentClass sch = new SecondChildClass;

pArr[0] = fch;
pArr[1] = sch;
```



## 2-3. Object 클래스

- **모든 클래스의 최상위 클래스는 Object 클래스**
  - `ctrl + t` : 상속관계 단축키

## 2-4. super 클래스

- 상위 클래스를 호출할 때 `super` 키워드 이용 ~~(this 키워드와 유사)~~

```java
// ParentClass
int openYear = 1995;
  
public void makeJJajang() {
  System.out.println("makeJJajang() START");
}

// ChildClass
int openYear = 2000;
  
public void getOpenYear() {
  System.out.println("ChildClass's Open year: " + this.openYear);
    System.out.println("ParentClass's Open year: " + super.openYear);
}

// MainClass
ChildClass c = new ChildClass();
c.getOpenYear();
	// ChildClass's Open yar: 2000
	// ParentClass's Open yar: 1995
```

# 3. 내부 클래스와 익명 클래스

## 3-1. 내부 (inner) 클래스

- 클래스 안에 또 다른 클래스를 선언하는 것으로 이렇게 하면 두 클래스의 멤버에 쉽게 접근 가능
- ~~잘 사용되지는 않음~~

```java
public class OuterClass {
  int num = 10;
  String str1 = "java";
  static String str11 = "world";
  
  public OuterClass() {
    System.out.println("OuterClass constructor");
  }
  
  class InnerClass {
    int num = 100;
    String str2 = str1;
    
    public InnerClass() {
      System.out.println("InnerClass constructor");
    }
  }
  
  static class SInnerClass {
    int num = 1000;
    String str3 = str11;
    
    public SInnerClass() {
      System.out.println("static InnerClass constructor");
    }
  }
}

// MainClass
OuterClass oc = newOuterClass();
System.out.println("oc.num: " + oc.num);
System.out.println("oc.str1: " + oc.str1);

System.out.println();

OuterClass.InnerClass in = oc.new InnerClass();
System.out.println("in.num: " + in.num);
System.out.println("in.str2: " + in.str2);

System.out.println();

OuterClass.SInnerClass si = new OuterClass.SInnerClass();
System.out.println("si.num: " + si.num);
System.out.println("si.str3: " + si.str3);

System.out.println();
```



## 3-2. 익명 (annonymous) 클래스

- 이름이 없는 클래스로 주로 메서드를 재정의하는 목적으로 사용되며, 주로 인터페이스나 추상클래스에서 이용됨

```java
public class AnonymousClass {
  
  public AnonymousClass() {
    System.out.println("AnonymousClass constructor");
  }
 	public void method() {
        System.out.println("AnonymousClass's method START");
  }
}

// MainClass
// 이름이 없는 객체를 생성 후 재정의한 메서드를 바로 실행
new AnonymousClass() {
  @Override
  public void method() {
        System.out.println("AnonymousClass's Override method START");
  };
}.method();
```



# 4. 인터페이스

## 4-1. 인터페이스란?

- 클래스와 달리 객체를 생성할 수는 없으며, 클래스에서 구현해야 하는 작업 명세서임
- 인터페이스는 실제로 정의되지 않은 기능들이 선언만 되어 있으며, 클래스에서 인터페이스가 갖고 있는 이러한 기능들을 구현하는 과정을 거친 뒤에 객체를 생성하게 됨

![스크린샷 2020-03-12 오후 2.08.49](/Users/eunjung/Documents/java_learning/images/스크린샷 2020-03-12 오후 2.08.49.png)

## 4-2. 인터페이스를 사용하는 이유

- 인터페이스를 사용하는 이유는 많지만, 가장 큰 이유는 객체가 다양한 자료형(타입)을 가질 수 있게 되기 때문

![스크린샷 2020-03-12 오후 2.10.36](/Users/eunjung/Documents/java_learning/images/스크린샷 2020-03-12 오후 2.10.36.png)



## 4-3. 인터페이스 구현

```java
// InterfaceA
public interface Interface A {
  public void funcA();
}

pupblic interface Interface B {...}

// ImplementClass
public class ImplementClass implements InterfaceA, InterfaceB {
  
  public ImplementClass() {
    System.out.println("ImplementClass constructur");
  }
    
  @Override
  public void funcA() {
    System.out.println("funcA()")
  }
  
  @Override
  public void funcB() {...}
}

// MainClass
InterfaceA ia = new ImplementClass(); // InterfaceA 에 선언된 메서드에만 접근 가능
InterfaceB ib = new ImplementClass(); // InterfaceB 에 선언된 메서드에만 접근 가능
```



## 4-4. 장난감 인터페이스

```java
// Toy interface
public interface Toy {
  public void walk();
  public void run();
  public void alarm();
  public void light();
}

// ToyAirplane class
public class ToyAirplane implements Toy {
  @Override
  public void walk(){...};
  @Override
  public void run(){...};
  ...
}

// ToyRobot class
public class ToyRobot implements Toy {
  @Override
  public void walk(){...};
  @Override
  public void run(){...};
  ...
}
```

# 5. 추상클래스

- 인터페이스와 비슷한 형태로 구체화되지 않은 멤버를 이용하여 클래스를 만듦

## 5-1. 추상클래스란?

- 클래스의 공통된 부분을 뽑아서 별도의 클래스(추상클래스)로 만들어 놓고, 이것을 상속해서 사용함

![스크린샷 2020-03-12 오후 2.30.15](/Users/eunjung/Documents/java_learning/images/스크린샷 2020-03-12 오후 2.30.15.png)

- 추상클래스의 특징
  - 멤버 변수를 가짐
  - 추상클래스를 상속하기 위해 `extends` 이용
  - 실제로 구현되지 않은 추상메서드를 가지며, 이는 상속한 클래스에서 구현해야 함
  - 일반 메서드도 가질 수 있음
  - 일반 클래스와 마찬가지로 생성자도 있음

## 5-2. 추상클래스 구현

- 클래스 상속과 마찬가지로 `extends` 키워드를 이용해서 상속하고 추상메서드를 구현함
- 추상클래스 내 추상메서드는 `public abstract void func();` 와 같이 선언함

## 5-3. Bank 추상클래스

- ~~생략~~

## 5-4. 인터페이스 vs 추상클래스

- 공통점
  - 추상 메서드를 가짐
  - 객체 생성이 불가하며 자료형(타입)으로 사용됨
- 차이점
  - 인터페이스
    - 상수, 추상메서드만 가짐
    - 추상 메서드를 구현만 하도록 함
    - 다형성을 지원
  - 추상클래스
    - 클래스가 갖는 모든 속성과 기능을 가짐
    - 추상 메서드 구현 및 상속의 기능을 가짐
    - 단일 상속만 지원

# 6. 람다식

- 기존의 객체 지향이 아닌 함수 지향의 프로그래밍 방법

## 6-1. 람다식이란?

- 익명 함수(anonymous function)를 이용해서 익명 객체를 생성하기 위한 식

## 6-2. 람다식 구현

- 람다식은 인터페이스를 활용하여 함수를 만들어 사용한다고 생각하면 됨

```java
public interface LambdaInterface1 {
  public void method(String s1,String s2, String s3);
}

// MainClass
LambdaInterface1 li1 = (String s1, String s2, String s3) -> { System.out.println(s1 + " " + s2 + " " + s3); };
li1.method("Hello", "Java", "World");
```

- 매개변수가 1개이거나 자료형(타입)이 같을 때는 자료형을 생략할 수 있음
- 매개변수와 실행문이 1개일 때, `()` 와 `{}` 를 생략할 수 있음
- 매개변수가 없을 때, `()` 만 작성함

```java
public interface LambdaInterface2 {
  public int method(int x, int y);
}

// MainClass
LambdaInterface2 li2 = (x, y) -> {
  int result = x + y;
  return result;
};
System.out.println(li2.method(10, 20)); // 30

li2 = (x, y) -> {
  int result x * y;
  return result;
};
System.out.println(li2.method(10, 20)); // 200
```

# 7. 문자열 클래스

## 7-1. String 객체와 메모리

- 문자열을 다루는 String 객체는 데이터가 변할 때 메모리상의 변화가 많아 속도가 느림
  - 문자열 변경시 기존의 객체를 버리고, 새로운 객체를 메모리에 생성하게 되며, 기존 객체의 메모리는 GC가 회수함

## 7-2. StringBuffer, StringBuilder

- String 클래스의 단점을 보완한 클래스로, 데이터 변경시 메모리에서 기존 객체를 활용함
- `StringBuffer` 와 `StringBuilder` 는 거의 동일함
  - 속도는 `StringBuilder` 가 조금 더 빠름
  - 데이터 안정성은 `StringBuffer` 가 조금 더 좋음

```java
StringBuffer sf = new StringBuffer("JAVA");
System.out.println(sf);
sf.append(" World"); // 맨 뒤에 연결
System.out.println(sf);
System.out.println(sf.length()); // 길이
sf.insert(sf.length(), "!!!"); // 특정 위치에 삽입
System.out.println(sf);
sf.delete(1, 2) // 해당 위치 삭제
System.out.println(sf);
```

# 8. Collections

## 8-1. List

- `List`는 인터페이스이며, 이를 구현한 클래스(`Vector`, **`ArrayList`**, `LinkedList`)는 index를 이용해 데이터를 관리함
- 선언 `ArrayList<String> list = new ArrayList<String>();`
- 메서드
  - `.add(요소)`, `.add(인덱스, 요소)`, `.set(인덱스, 요소)`, `.get(인덱스)`, `.remove(인덱스)`, `.clear()`, `.isEmpty()`, `.size()`



## 8-2. Map

- `Map` 은 인터페이스이며, 이를 구현한 클래스(**`HashMap`**)는 **key (중복 불가)**를 이용해서 데이터를 관리함
- 선언 `HashMap<Integer, String> map = new HashMap<Integer, String>();`
- 메서드
  - `.size()`, `.put(키, 값)`, `.get(키)`, `.remove(키)`, `.containskey(키)`, `.containsValue(값)`, `.clear()`, `.isEmpty()`

# 끝.

