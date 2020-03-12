# 1. 예외처리

## 1-1. 예외란?

- 프로그램에 문제가 있는 것을 말하며, 예외로 인해 시스템 동작이 멈추는 것을 방지하는 것을 **예외처리**라고 함
- *Exception* vs *Error*
  - Exception: 코드 구현상의 문제로 개발자가 대처할 수 있는 부분
    - Checked Exception : **반드시** 예외처리를 해야하는 경우로 컴파일이 되지 않음 (네트워크, 파일 시스템 등)
    - Unchecked Exception : 개발자의 **판단에 따라** 예외처리를 하는 경우 (데이터 오류 등)
  - Error: 물리적인 장애 요소가 생기는 경우로 개발자가 대처하기 어려운 부분

## 1-2. Exception 클래스

- `Exception` 클래스의 하위클래스로 `NullPointerException`, `ArrayIndexOutOfBoundException`, `NumberFormatException` 등이 존재

## 1-3. try ~ catch

- 개발자가 예외처리하기 가장 쉽고, 가장 많이 사용되는 방법
- `try { 예외가 발생할 수 있는 코드 } catch (Exception e) { 예외가 발생했을 때 처리할 코드 }` 

## 1-4. 다양한 예외처리

- Exception 및 하위 클래스를 이용해서 예외처리를 다양하게 할 수 있음

```java
try {...}
catch (InputMismatchException e) {...}
catch (ArrayIndexOutOfBoundsException e) {...}
catch (Exception e) {...}
```



## 1-5. finally

- 예외 발생 여부와 관계없이 반드시 실행
- `try {...} catch (Exception e) {...} finally {...}`

## 1-6. throws

- 예외 발생시 예외 처리를 직접 하지 않고 호출한 곳으로 넘겨줌

```java
public void firstMethod() throws Exception {
  secondMethod();
} // 연쇄적으로 error를 보냄

public void secondMethod() throws Exception {
  thirdMethod();
} // 연쇄적으로 error를 보냄

public void thirdMethod() throws Exception {
  System.out.println("10 / 0 = " + (10 / 0))
} // thirdMethod를 호출한 secondMethod로 error를 보냄

// MainClass
MainClass004 mainClass004 = new MainClass004();

try{
  mainClass004.firstMethod();
} catch (Exception e) {
  e.printStackTrace() // 전달받은 error를 처리함
}
```

# 2. 입력과 출력

## 2-1. 입/출력 이란?

- 다른 곳의 데이터를 가져오는 것을 입력이라 하고, 다른 곳으로 데이터를 내보내는 것을 출력이라고 함
- 프로그램과 입/출력 대상 사이에 데이터가 오고(입력) 가는(출력) 길을 stream 이라고 함

## 2-2. 입/출력 기본 클래스

- 입/출력에 사용되는 기본 클래스로는 1byte 단위로 데이터를 전송하는 `InputStream`, `OutputStream` 이 있음.
- InputStream
  - FileInputStream
  - DataInputStream
  - BufferedInputStream
- OutputStream
  - FileOutputStream
  - DataOutputStream
  - BufferedOutputStream

## 2-3. FileInputStream / FileOutputStream

- 파일에 데이터를 읽고/쓰기 위한 클래스로 `read()`, `write()` 메서드를 이용

- `FileInputStream`

  - `read();` 1byte 단위로 데이터를 읽어들임

  - `read(byte[]);` 매개변수로 바이트 배열을 주게 되면 배열 크기만큼씩 읽어들임

- `FileOutputStream`

  - `write(byte[] b);` 전체를 씀
  - `write(byte[], int off, int len);` off 부터 len 만큼 씀

```java
// 입력
InputStream inputStream = null;
try {
	inputStream = new FileInputStream(파일명);
  int data = 0;
  
  while(true){
    try{
      data = inputStream.read();
    } catch (IOException e) {
      e.printStackTrace();
    }
    if(data == -1) break;
    System.out.println(data);
  }
} catch (FileNotFoundException e) {
  e.printStackTrace();
} finally {
  try {
    if(inputStream != null) inputStream.close();
  } catch (IOException e) {
    e.printStackTrace();
  }
}
```



## 2-4. 파일 복사

- 파일 입/출력 클래스를 이용해서 복사

## 2-5. DataInputStream, DataOutputStream

- byte 단위의 입출력을 개선하여 문자열을 조금 더 편리하게 문자 단위로 다룰 수 있음

```java
String str = "Hello Java World!";
OutputStream outputStream = null;
DataOutputStream dataOutputStream = null;

try {
  outputStream = new FileOutputStream(파일명);
  dataOutputStream = new DataOutputStream(outputStream);
  
  dataOutputStream.writeUTF(str);
} catch (...) {...}
```



## 2-6. BufferedReader, BufferedWriter

- byte 단위의 입출력을 개선하여 문자열을 조금 더 편리하게 문자 단위로 다룰 수 있음

```java
String fileName = 파일명;

BufferedReader br = null;
FileReader fr = null;

try {
  fr = new FileReader(fileName);
  br = new BufferedReader(fr);
  
  String strLine;
  
  while((strLine = br.readLine()) != null){
    System.out.println(strLine);
  }
} catch (...) {...}
```

# 3. 네트워킹

## 3-1. 네트워크 데이터 입력 및 출력

- 네트워크 대상 (객체) 사이의 입출력(InputStream, OutputStream) 을 이용해서 데이터를 입력하고 출력

## 3-2. 소켓(Socket)

- 네트워크 상에서 데이터를 주고받기 위한 장치

## 3-3. Socket 클래스

- 서버는 클라이언트를 맞을 준비를 하고 있다가 클라이언트의 요청에 반응

```java
// ServerSocket : Java 기본 제공 클래스
serverSocket = new ServerSocket(포트번호);

socket = serverSocket.accept(); // 클라이언트에서 요청을 하면 서버 소켓의 accept() 메서드가 자동적으로 실행되면서 socket 을 반환
System.out.println(socket);


ServerSocket serverSocket = null;
Socket socket = null;

try {
  serverSocket = new ServerSocket(포트번호);
  System.out.println("클라이언트 맞을 준비 완료!");
  // 클라이언트 요청
  socket = serverSocket.accept();
  System.out.println("클라이언트 연결");
  System.out.println("socket: " + socket);
} catch (Exception e) {
  e.printStackTrace();
} finally {
  try {
    if (socket != null) socket.close();
    if (serverSocket != null) serverSocket.close();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```



## 3-4. Client 와 Server 소켓

- 서버에서 ServerSocket을 준비하고 클라이언트에서 Socket을 이용해 접속

```java
// 클라이언트
Socket socket = null;
try {
  socket = new Socket("localhost", 9000);
  System.out.println("서버 연결");
  System.out.println("socket: " + socket);
}

// 서버
ServerSocket serverSocket = null;
Socket socket = null;

try {
  serverSocket = new ServerSocket(9000);
  ...
  socket = serverSocket.accept();
  ...
}
```



## 3-5. 양방향 통신

- 클라이언트와 서버는 InputStream, OutputStream을 이용해서 양방향 통신 가능

# 끝.

