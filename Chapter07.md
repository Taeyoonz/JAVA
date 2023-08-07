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
    - 클래스, 변수 또는 메서드의 선언부에 함께 사용되어 부가적인 의미를 부여하는 것
    - 접근 제어자 : public, protected, default, private
    - 그 외 : static, final, abstract, native, transient, synchronized, volatile, strictfp
  + static - 클래스의, 공통적인
    - static은 '클래스의' 또는 '공통적인' 의미를 가지고 있다
    - 클래스변수(static멤버변수)는 인스턴스에 관계없이 같은 값을 갖는다 - 하나의 변수를 모든 인스턴스가 공유하기 때문
    - static이 붙은 멤버변수와 메서드, 초기화 블럭은 인스턴스가 아닌 클래스에 관계된 것이기 때문에 인스턴스를 생성하지 않고도 사용할 수 있다
    - <table style="height: 153px; margin-left: auto; margin-right: auto;" width="583" cellspacing="3">
      <tbody>
      <tr>
      <td style="width: 194px;">제어자</td>
      <td style="width: 194px;">대상</td>
      <td style="width: 194px;">의미</td>
      </tr>
      <tr>
      <td style="width: 194px;" rowspan="5">static</td>
      <td style="width: 194px;" rowspan="3">멤버변수</td>
      <td style="width: 194px;">-모든 인스턴스에 공통적으로 사용되는 클래스 변수가 된다.</td>
      </tr>
      <tr>
      <td style="width: 194px;">-클래스 변수는 인스턴스를 생성하지 않고도 사용 가능하다.</td>
      </tr>
      <tr>
      <td style="width: 194px;">-클래스가 메모리에 로드될 때 생성된다.</td>
      </tr>
      <tr>
      <td style="width: 194px;" rowspan="2">메서드</td>
      <td style="width: 194px;">-인스턴스를 생성하지 않고도 호출이 가능한 static메서드가 된다.</td>
      </tr>
      <tr>
      <td style="width: 194px;">-static메서드 내에서는 인스턴스멤버들을 직접 사용할 수 없다.</td>
      </tr>
      </tbody>
      </table>
  + final - 마지막의, 변경될 수 없는
    - final은 '마지막의' 또는 '변경될 수 없는'의 의미를 가지고 있다
    - <table style="height: 153px; margin-left: auto; margin-right: auto;" width="583" cellspacing="3">
      <tbody>
      <tr style="height: 23px;">
      <td style="width: 194px; height: 23px;">제어자</td>
      <td style="width: 194px; height: 23px;">대상</td>
      <td style="width: 194px; height: 23px;">의미</td>
      </tr>
      <tr style="height: 43px;">
      <td style="width: 194px; height: 255px;" rowspan="4">final</td>
      <td style="width: 194px; height: 129px;">클래스</td>
      <td style="width: 194px; height: 43px;">
      <p>변경될 수 없는 클래스, 확장될 수 없는 클래스가 된다.</p>
      <p>그래서 final로 지정된 클래스는 다른 클래스의 조상이 될 수 없다.</p>
      </td>
      </tr>
      <tr style="height: 63px;">
      <td style="width: 194px; height: 126px;">메서드</td>
      <td style="width: 194px; height: 63px;">변경될 수 없는 메서드, final로 지정된 메서드는 오버라이딩을 통해 재정의 될 수 없다.</td>
      </tr>
      <tr style="height: 63px;">
      <td style="width: 194px; height: 126px;">멤버변수</td>
      <td style="width: 194px; height: 63px;" rowspan="2">변수 앞에 final이 붙으면, 값을 변경할 수 없는 상수가 된다.</td>
      </tr>
      <tr style="height: 63px;">
      <td style="width: 194px; height: 126px;">지역변수</td>
      </tr>
      </tbody>
      </table>
    - 생성자를 이용한 final멤버 변수의 초기화
      ```java
      class Card {
        final int NUMBER;
        final String KIND;
        static int width = 100;
        static int height = 250;

        Card(String kind, int num) {
          KIND = kind;
          NUMBER = num;
        }
        Card() {
          this("HEART", 1);
        }
        public String toString() {
          return KIND + " " + NUMBER;
        }
      }

      class FinalCardTest {
        public static void main(String args[]) {
          Card c = new Card("HEART", 10);
          // c.NUMBER = 5;  // 에러
          System.out.println(c.KIND);                                    // HEART
          System.out.println(c.NUMBER);                                  // 10
          System.out.println(c);  // System.out.println(c.toString());   // HEART 10
        }
      }
      ```
  + abstract - 추상의, 미완성의
    - abstract는 '미완성'의 의미를 가지고 있다
    - <table style="height: 153px; margin-left: auto; margin-right: auto;" width="583" cellspacing="3">
      <tbody>
      <tr style="height: 23px;">
      <td style="width: 194px; height: 23px;">제어자</td>
      <td style="width: 194px; height: 23px;">대상</td>
      <td style="width: 194px; height: 23px;">의미</td>
      </tr>
      <tr style="height: 43px;">
      <td style="width: 194px; height: 255px;" rowspan="2">abstract</td>
      <td style="width: 194px; height: 129px;">클래스</td>
      <td style="width: 194px; height: 43px;">
      <p>클래스 내에 추상 메서드가 선언되어 있음을 의미한다.</p>
      </td>
      </tr>
      <tr style="height: 63px;">
      <td style="width: 194px; height: 126px;">메서드</td>
      <td style="width: 194px; height: 63px;">선언부만 작성하고 구현부는 작성하지 않은 추상 메서드임을 알린다.</td>
      </tr>
      </tbody>
      </table>
    - ???
  + 접근 제어자(access modifier)
    - 멤버 또는 클래스에 사용되어, 외부에서 접근하지 못하도록 제한하는 역할을 한다
    - |제어자|범위|
      |--|--|
      |private|같은 클래스 내에서만 접근이 가능하다|
      |default|같은 패키지 내에서만 접근이 가능하다|
      |protected|같은 패키지 내에서, 그리고 다른 패키지의 자손클래스에서 접근이 가능하다|
      |public|접근 제한이 전혀 없다|
    - 범위가 넓은 순으로 나열
      * public > protected > (default) > private
    - 접근 제어자를 사용하는 이유
      * 외부로부터 데이터를 보호하기 위해서
      * 외부에는 불필요한, 내부적으로만 사용되는 부분을 감추기 위해서
  + 제어자(modifier)의 조합
    - |대상|사용가능한 제어자|
      |--|--|
      |클래스|public, (default), final, abstract|
      |메서드|모든 접근 제어자, final, abstract, static|
      |멤버변수|모든 접근 제어자, final, static|
      |지역변수|final|
    - 주의사항
      * 메서드에 static과 abstract를 함께 사용할 수 없다
        >static메서드는 몸통이 있는 메서드에만 사용할 수 있기 때문이다
      * 클래스에 abstract와 final을 동시에 사용할 수 없다
        >클래스에 사용되는 final은 클래스를 확장할 수 없다는 의미이고 abstract는 상속을 통해서 안성되어야 한다는 의미이므로 서로 모순된다 
      * abstract메서드의 접근 제어자가 private일 수 없다
        >abstract메서드는 자손클래스에서 구현해주어야 하는데 접근 제어자가 private이면, 자손클래스에서 접근할 수 없기 때문이다
      * 메서드에 private와 final을 같이 사용할 필요는 없다
        >접근 제어자가 private인 메서드는 오버라이딩될 수 없기 때문이다. 이 둘 중 하나만 사용해도 의미가 충분하다
