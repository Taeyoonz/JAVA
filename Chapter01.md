# Chapter01 자바를 시작하기 전에
*****
## 1. 자바
  + 객체 지향 프로그래밍 언어
  + 운영체제에 독립적
  + 풍부한 클래스 라이브러리 제공
  + 배우기 쉬움
  + 자동 메모리 관리(Garbage Collection)
  + 네트워크와 분산처리 지원
  + 멀티쓰레드 지원
  + 동적 로딩 지원
  + JVM(Java Virtual Machine)
## 2. 자바개발환경 구축하기
  + JDK 설치
  + Java API 문서 설치
## 3. 자바로 프로그램 작성하기
  + Hello.java
    - Hello.java 작성
    - javac.exe로 컴파일
    - Hello.class 생성
    - java.exe.로 실행
    - "Hello, world." 출력
    ```java
    class Hello {
      public static void main(String[] args) {
        System.out.println("Hello, world.");
      }
    }
    ```
  + 자주 발생하는 에러와 해결방법
    - cannot find symbol 또는 cannot resolve symbol
      지정된 변수나 메서드를 찾을 수 없다는 뜻
    - ';' expected
      세미콜론이 필요한 곳에 없다는 뜻
    - Exception in thread "main" java.lang.NoSuchMethodError: main
      main 메서드를 찾을 수 없다는 뜻
    - Exception in thread "main" java.lang.NoClassDefFoundError: Hello
      Hello라는 클래스를 찾을 수 없다는 뜻
    - illegal start of expression
      문장의 앞부분이 문법에 맞지 않는다는 뜻
    - class, interface, or enum expeted
      키워드 class나 interface 또는 enum이 없다는 뜻, 괄호의 개수가 일치하지 않는 경우
  + 자바 프로그램의 실행과정
    1. 프로그램의 실행에 필요한 클래스(*.class파일)을 로드한다.
    2. 클래스파일을 검사한다.(파일형식, 악성코드 체크)
    3. 지정된 클래스(Hello)에서 main(String[] args)를 호출한다.
  + 주석
    - 범위 주석 - /* */
    - 한 줄 주석 - //
