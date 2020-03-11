# 1. 객체 지향 프로그래밍이란

> 모듈화, 확장성 등을 특장점으로 갖는 프로그래밍 기법

## 1-1. 객체란?

- 세상에 존재하는 모든 것을 뜻하며, 프로그래밍에서는 **속성과 기능을 가지는 프로그램 단위**
- 예시
  - 날씨 프로그램 (객체)
    - 속성: 온도, 미세먼지 농도
    - 기능: 날씨 예보
  - 사칙연산 프로그램 (객체)
    - 속성: +, -, *, /
    - 기능: 연산기능

## 1-2. 클래스란?

- 객체를 생성하기 위한 **틀**로, 모든 객체는 클래스로부터 생성 ~~(와플 틀)~~

  \* 사용이 끝난 객체는 GC가 회수

## 1-3. 클래스 구성요소

- **속성(멤버 변수)**와 **기능(메서드)**
- 예시
  - 자전거
    - 속성(멤버 변수): 안장, 핸들, 바구니, 기어, 페달, 바퀴
    - 기능(메서드): 기어 변속, 가속, 브레이크

# 2. 클래스 제작과 객체 생성

## 2-1. 클래스 제작

- 구성: 멤버 변수(속성), 메서드(기능), 생성자(constructor) 등

```java
// 패키지: 연관된 클래스끼리 구분
package vehicle
  // public: 접근 제한자 (추후 다루게 됨)
  public class Grandeur {
    // 멤버 변수
    public String color;
    public String gear;
    public int price;

    // 생성자 : 클래스명과 동일한 이름을 가지며, 객체 생성시 가장 먼저 호출되는 메서드, 반환형 x
    public Grandeur() { 
      System.out.println("Grandeur constructor");
    }

    // 메서드
    public void run() {
      System.out.println("-- run --");
    }
    public void stop() {
      System.out.println("-- stop --");
    }
    public void info() {
      System.out.println("color: " + color);
      System.out.println("gear: " + gear);
      System.out.println("price: " + price);
    }
  }
```



## 2-2. 객체 생성

- `new` 를 통해 클래스로부터 객체를 생성

```java
// MainClass

// myCar1은 "레퍼런스"라고 하며, 생성된 Grandeur 객체의 주소를 담고 있는 변수임
Grandeur myCar1 = new Grandeur(); 
myCar1.color = "black";
myCar1.gear = "auto";
myCar1.price = 30000000;

myCar1.run();
myCar1.run();
myCar1.info();

System.out.println();

Grandeur myCar2 = new Grandeur();
myCar2.color = "white";
myCar2.gear = "manual";
myCar2.price = 25000000;

myCar2.run();
myCar2.run();
myCar2.info();
```



## 2-3. 생성자

- 클래스로 객체를 생성할 때 가장 먼저 호출
- 생성자는 1개 이상 존재 가능 (default constructor + alpha)

```java
public class Bicycle {
  public String color;
  public int price;
  
  // default 생성자
  public Bicycle() {
    System.out.println("Bicycle  constructor I");
  }
  
  // 사용자 정의 생성자
  public Bicycle(String c, int p) {
    System.out.println("Bicycle constructor II");
    
    // this: 해당 객체
    this.color = c;
    this.price = p;
  }
  
  public void info() {
    System.out.println("color: " + color);
    System.out.println("price: " + price);
  }
}

// MainClass
Bicycle myBicycle1 = new Bicycle();
myBicycle1.color = "red";
myBicycle1.price = 100;
myBicycle1.info();

Bicycle myBicycle2 = new Bicycle("green", 200);
myBicycle2.info();

myBicycle2.color = "yellow";
myBicycle2.info();
```

# 3. 메서드

## 3-1. 메서드 선언과 호출

- 메서드도 변수와 같이 선언 및 정의 후 필요시에 호출하여 사용
- 선언 `public void getInfo() {...}`
  - `public`: 접근자
  - `void`: 반환형 
  - `getInfo`: 메서드명 (convention: camel case & 동사+명사)
  - `()`: 매개변수
  - `{...}`: 메서드 정의
- 호출 `객체명.getInfo()`



## 3-2. 매개변수 (parameter)

- 메서드를 호출할 때 데이터를 전달

```java
public class ChildClass {
  public String name;
  public String gender;
  public int age;
  
  public ChildClass() {
    System.out.println("ChildClass constructor");
  }
  
  public void setInfo(String n, String g, int a) {
    System.out.println("setInfo() START");
    
    this.name = n;
    this.gender = g;
    this.age = a;
  }
  
  public void getInfo() {
    System.out.println("getInfo() START");
    
    System.out.println("name: " + name);
    System.out.println("gender: " + gender);
    System.out.println("age: " + age);
  }
}

// MainClass
ChildClass child = new ChildClass();
child.setInfo("jenny", "M", 17);
child.getInfo();
```



## 3-3. 중복 메서드 (overloading)

- 이름은 같고, 매개변수의 개수 또는 타입이 다른 메서드를 만들 수 있음



## 3-4. 접근자

- 메서드를 호출할 때 접근자에 따라서 호출이 불가할 수 있음
- public, private, protected 등 존재
  - `public` : 메서드를 외부에서 호출할 수 있음
  - `private` : 메서드를 **외부에서 호출할 수 없음**

# 4. 객체와 메모리

## 4-1. 메모리에서 객체 생성 (동적 생성)

- 객체는 메모리에서 동적으로 생성되고, 객체가 더 이상 필요없게 되면 GC에 의해서 제거
- **어떠한 레퍼런스와도 관계가 없는 객체**는 더 이상 필요없는 객체로 인식됨

## 4-2. 레퍼런스

- 생성한 **객체의 주소**를 변수에 저장하는 것을 레퍼런스라고 함

- `ChildClass child = new ChildClass();` 에서 **child** 가 레퍼런스

## 4-3. 자료형이 같아도 다른 객체

- 자료형이 같아도 다른 공간에 존재하는 객체는 서로 다른 객체임

```java
public class ObjectClass {
}

// MainClass
ObjectClass obj1 = new ObjectClass();
ObjectClass obj2 = new ObjectClass();
ObjectClass obj3 = new ObjectClass();

// 주소 출력 : 모두 다른 공간에 존재
System.out.println("obj1: " + obj1);
System.out.println("obj2: " + obj2);
System.out.println("obj3: " + obj3);
```



## 4-4. null과 NullPointException

- 레퍼런스에 `null` 이 저장되면 객체의 연결이 끊기게 되며, 더 이상 객체를 이용할 수 없음
- 객체의 연결이 끊긴 객체를 이용하려고 할 때 `NullPointException` 발생

```java
public class ObjectClass {
  public void getInfo() {
    System.out.println("getInfo() START");
  }
}

// MainClass
ObjectClass obj1 = new ObjectClass();
ObjectClass obj2 = new ObjectClass();

obj1.getInfo();

obj2 = null;
obj1.getInfo();
obj2.getInfo();
```



# 5. 생성자와 소멸자 그리고 this 키워드

## 5-1. default 생성자

- `new`를 통해 객체가 생성될 때 **가장 먼저 호출**되는 생성자로, 만약 개발자가 명시하지 않더라도 컴파일 시점에 자동으로 생성됨
  - 자동 생성 : `public 클래스명() {}`

## 5-2. 사용자 정의 생성자

- default 생성자 외에 특정 목적에 의해 개발자가 만든 생성자로, 매개변수에 차이가 있음

## 5-3. 소멸자

- 객체가 GC에 의해 메모리에서 제거될 때 `finalize()` 메서드가 호출ehla
- 일반적으로 `finalize()` 메서드는 직접 정의하지 않음

```java
ObjectEx obj = new ObjectEx();
obj = new ObjectEx();
```



## 5-4. this 키워드

```java
public class ObjectClass {
	public int x;
  public int y;
  
  public ObjectClass(int x, int y) {
    // this: 클래스로부터 만들어지는 해당 객체를 가리킴
    this.x = x;
    this.y = y;
  }
  
  public void getInfo() {
    System.out.println("x: " + x);
    System.out.println("y: " + y);
  }
}

// MainClass
ObjectClass obj = new ObjectClass(10, 20);
obj.getInfo();
```

# 6. 패키지와 static

## 6-1. 패키지

- java 프로그램은 많은 클래스로 구성되고, 이러한 **클래스를 폴더 형식으로 관리**하는 것을 패키지라고 함
- 패키지 작명 요령
  - 패키지 이름은 패키지에 속해 있는 클래스가 최대한 다른 클래스와 중복되는 것을 방지하도록 작명
  - 패키지 이름은 일반적으로 도메인(unique)을 거꾸로 이용
  - 개발 중에 패키지 이름과 구조는 변경 가능
  - 패키지 이름만 보고도 해당 패키지 안에 있는 클래스가 어떤 속성과 기능을 가지고 있는지 예상할 수 있도록 작명

```java
// 패키지 내에 클래스 만들 때
package 패키지명
  
public class Employee {
}
```



## 6-2. import

- 다른 패키지에 있는 클래스를 사용하기 위해서는 import 키워드 이용
  - `import 패키지명.클래스명;`
  - `import 패키지명.*;` : 해당 패키지의 모든 클래스



## 6-3. static

- 클래스의 속성과 메서드에 static 키워드를 사용하면 어디서나 속성과 메서드 공유 가능

```java
public class EmployeeBank {
  String name;
  static int amount = 0;
  
  public EmployeeBank(String name) {
    this.name = name;
  }
  
  public void saveMoney(int money) {
    amount += money;
    System.out.println("amount: " + amount);
  }
  
  public void spendMoney(int money) {
    amount -= money;
    System.out.println("amount: " + amount);
  }
  
  public void getBankInfo() {
    System.out.println("Employee name: " + this.name);
    System.out.println("amount: " + amount);
  }
}
```

# 7. 데이터 은닉

> 객체가 가지고 있는 데이터를 외부로부터 변질되지 않게 보호하는 방법

## 7-1. 멤버 변수의 private 설정

- 멤버 변수(속성)는 주로 private으로 설정해서, 외부로부터 데이터가 변질되는 것을 방지

## 7-2. setter, getter

- 멤버 변수를 외부에서 변경할 수 있도록 하는 메서드

```java
// Student 클래스

public Class Student {
  private String name;
  private int score;
  
  public Student(String n, int s) {
    this.name = n;
    this.score = s;    
  }
  
	public void getInfo() {
    System.out.println("getInfo() START");
    System.out.println("name: " + name);
    System.out.println("score: " + score);
  }
  
  // 우클릭 - Source - Generate Getters and Setters 으로 자동완성 가능
  public String getName() {
    return name;
  }
  
  public int getScore() {
    return score;
  }
  
  public void setScore(int score) {
    if (score >= 0) this.score = score;  
  }
}
```

```java
// MainClass

public class MainClass {
  public static void main(String[] args) {
    
    Student student1 = new Student("홍길동", 90);
    student1.getInfo();
    
    student1.setScore(100);
    student1.getInfo();
    
  } 
}
```

# 끝.

