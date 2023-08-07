# Chapter07 객체지향 프로그래밍 2
*****
## 1. 상속
  + 상속이란?
    - 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것
  + 장점
    - 상속을 통해 클래스를 작성하면 보다 적은 양의 코드로 클래스를 작성할 수 있고
    - 코드 추가 및 변경에 매우 용이함
    - 코드의 재사용성을 높임
    - 중복되는 코드를 제거하여 프로그램의 생산성과 유지보수에 유리함
  + 사용
    ```java
    class Child extends Parent {
      //...
    }
    ```
  + 조상 클래스
    - 부모 클래스, 상위 클래스, 기반 클래스
  + 자손 클래스
    - 자식 클래스, 하위 클래스, 파생된 클래스
  + 자손 클래스는 조상 클래스의 모든 멤버를 상속받기 때문에 Child클래스는 Parent클래스의 멤버들을 포함한다고 할 수 있음
    ```java
    class Parent {
      int age;
    }
    class Child extends Parent {  }
    ```
  + 생성자와 초기화 블럭은 상속되지 않는다. 멤버만 상속된다.
  + 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다.
    
  + 클래스간의 관계 - 포함관계
    ```java
    class Car {
      Engine e = new Engine(); // 엔진
      Door[] d = new Door[4];  // 문, 문의 개수를 넷으로 가정
    }
    ```
    - Engine, Door과 같은 클래스를 미리 작성해 놓고, 이들을 Car의 멤버변수로 선언하여 포함관계를 맺어주면, 코드도 간결하고 코드 관리도 수월하다
  + 클래스간의 관계 결정하기
    - 상속관계를 맺어 줄 지 포함관계를 맺어 줄 지 결정해야 한다
    - 원(Circle)은 점(Point)이다 - 상속관계
      ```java
      class Circle extends Point {
        int r;
      }
      ```
      '~은 ~이다.' 라는 문장이 성립한다면, 서로 상속관계를 맺어준다
    - 원(Circle)은 점(Point)을 가지고 있다 - 포함관계
      ```java
      class Circle {
        Point c = new Point();
        int r;
      }
      ```
      '~은 ~을 가지고 있다.' 라는 문장이 성립한다면, 서로 포함관계를 맺어준다

  + 단일 상속(single inheritance)
    - 자바에서는 오직 단일 상속만 허용한다
    - 다중 상속을 허용하면 복합적인 기능을 가진 클래스를 쉽게 작성할 수 있게 되지만,
    - 클래스간의 관계가 매우 복잡해지며, 상속받은 멤버간의 이름이 같은 경우 구별할 수 있는 방법이 없다는 단점이 있다
  + Object클래스 - 모든 클래스의 조상
    - Object클래스는 모든 클래스 상속계층도에서 최상위에 있는 조상 클래스이다
    - 상속 받지 않는 모든 클래스들은 자동적으로 Object클래스를 상속받게 되어 있다
      ```java
      class TV (extends Object) {  /// 생략 되어 있는 것
        ...
      }
      ```
    - 자바의 모든 클래스들은 Object클래스의 멤버들을 상속 받기 때문에 Object클래스에 정의된 멤버들을 사용할 수 있는데
      이는 toString()이나 equals(Object o)와 같은 메서드를 사용할 수 있었던 이유이다
## 2. 오버라이딩(overriding)
  + 오버라이딩이란?
    - 조상클래스로부터 상속받은 메서드의 내용을 변경하는 것
    - 상속받은 메서드를 그대로 사용하는 경우도 있지만, 자손 클래스 자신에 맞게 변경하는 경우도 있는데, 이 경우를 오버라이딩한다고 한다
      ```java
      class Point {
        int x;
        int y;
        String getLocation() {
          return "x : " + x + ", y : " + y;
        }
      }
      ```
      ```java
      class Point3D extends Point {
        int z;
        String getLocation() {
          return "x : " + x + ", y : " + y + ", z : " + z;
        }
      }
      ```
  + 오버라이딩의 조건
    - 오버라이딩은 메서드의 내용만을 새로 작성하는 것이므로 메서드의 선언부는 조상의 것과 완전히 일치해야 한다
    - 조건
      * 메서드 이름이 같아야 한다
      * 매개변수가 같아야 한다
      * 반환타입이 같아야 한다
    - 접근 제어자와 예외 처리의 제한된 조건
      * 접근 제어자를 조상 클래스의 메서드보다 좁은 범위로 변경할 수 없다
      * 예외는 조상 클래스의 메서드보다 많이 선언할 수 없다
      * 인스턴스 메서드를 static 메서드로 또는 그 반대로 변경할 수 없다
  + 오버로딩 vs 오버라이딩
    - 오버로딩(overloading), 기존에 없는 새로운 메서드를 정의하는 것(new)
    - 오버라이딩(overriding), 상속받은 메서드의 내용을 변경하는 것(change, modify)
      ```java
      class Parent {
        void parentMethod() {}
      }
      class Child extends Parent {
        void parentMethod() {}        // 오버라이딩
        void parentMethod(int i) {}   // 오버로딩 

        void childMethod() {}        
        void childMethod(int i) {}    // 오버로딩
        void childMethod() {}         // 에러, 중복정의
      }
      ```
  + super
    - 자손 클래스에서 조상 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조 변수
    - ```java
      class SuperTest {
        public static void main(String args[]) {
          Child c = new Child();
          c.method();
        }
      }
      class Parent {
        int x = 10;
      }
      class Child extends Parent {
        void method() {
          System.out.println("x=" + x);              // x=10
          System.out.println("this.x=" + this.x);    // this.x=10
          System.out.println("super.x=" + super.x);  // super.x=10
        }
      }
      ```
    - ```java
      class SuperTest {
        public static void main(String args[]) {
          Child c = new Child();
          c.method();
        }
      }
      class Parent {
        int x = 10;
      }
      class Child extends Parent {
        int x = 20;
        void method() {
          System.out.println("x=" + x);              // x=20
          System.out.println("this.x=" + this.x);    // this.x=20
          System.out.println("super.x=" + super.x);  // super.x=10
        }
      }
      ```
  + super() - 조상 클래스의 생성자
    - this()와 같이 super() 역시 생성자이다
    - 조상 클래스의 생성자를 호출하는데 사용
    - Object 클래스를 제외한 모든 클래스의 생성자는 첫 줄에 반드시 자신의 다른 생성자 또는 조상의 생성자를 호출해야 한다
    - 그렇지 않으면 컴파일러는 생성자의 첫 줄에 'super();'를 자동적으로 추가한다
    - ????
## 3. package와 import
  + 패키지
    - 패키지란, 클래스의 묶음이다
    - 서로 관련된 클래스들끼리 효율적으로 관리할 수 있도록 그룹 단위로 묶어 놓은 개념
      ex) String클래스 -> java.lang.String
    - 클래스가 물리적으로 하나의 클래스파일(.class)인 것과 동일하게 패키지는 물리적으로 하나의 디렉토리이다
      ex) String클래스는 java.lange 패키지에 속하는 String.class 파일이다
  + 패키지의 선언
    - 선언
      ```java
      package 패키지명;
      ```
    - 자바에서는 기본적으로 이름없는 패키지(unnamed package)를 제공한다
    - 소스파일에 자신이 속할 패키지를 지정하지 않은 클래스는 이름없는 패키지에 속하게 되고 즉, 지정하지 않은 모든 클래스는 같은 패키지에 속하게 되는 셈이다
   
  + import문
    - import문으로 사용하고자 하는 클래스의 패키지를 미리 명시해주면 소스코드에 사용되는 클래스이름에서 패키지명은 생략할 수 있다
    - import문의 역할은 컴파일러에게 소스파일에 사용된 클래스의 패키지에 대한 정보를 제공하는 것
   
  + import문의 선언
    - 소스파일의 구성 순서
      1. package문 선언
      2. import문 선언
      3. 클래스 선언
    - import문 선언방법
      ```java
      import 패키지명.클래스명;
      또는
      import 패키지명.*;
      ```

  + static import문
    - static멤버를 호출할 때 클래스 이름을 생략할 수 있다
      ```java
      import static java.lang.System.out;
      import static java.lang.Math.*;

      class StaticImportEx1 {
        public static void main(String[] args) {
          // System.out.println(Math.random());
          out.println(random());

          // System.out.println("Math.PI : " + Math.PI);
          out.println("Math.PI : " + PI);
        }
      }
      ```
## 4. 제어자(modifier)
  + 제어자란
    - 클래스, 변수 또는 메서드의 선언부에 함께 사용되어 부가적인 의미를 부여하는 
    - 접근 제어자 : public, protected, default, private
    - 그 외 : static, final, abstract, native, transient, synchronized, volatile, strictfp
