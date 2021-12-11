# 상속(Inheritance)
### 상속
* 상속은 부모 클래스의 기능을 자식 클래스에게 물려주는 것
* 같은 패키지 내에서 부모 클래스의 private 접근 제한자를 갖는 필드와 메소드를 제외한 나머지를 상속한다
* 다른 패키지라면 부모 클래스의 private와 default 접근 제한자를 갖는 필드와 메소드를 제외한 나머지들이 상속된다
* 다중 상속을 허용하지 않는다 (extends 뒤에는 하나의 부모 클래스만 올 수 있다)
* 상속을 통해 heap영역에 부모 객체가 먼저 생성이 되고 자식객체가 생성이 된다
* 동일한 기능을 반복하지 않게하여 코드의 재사용을 증가시킨다

```java
// 상속 방법
class ChildClassName extends ParentClassName {
  // field
  // constructor
  // method
}
```

```java
// Car.java
public Class Car {
  // field
  private String carName;
  private int maxSpeed;
  private int currentSpeed = 0;
  
  // constructor
  public Car(String carName, int maxSpeed) {
    this.carName = carName;
    this.maxSpeed = maxSpeed;
  }
  
  // method
  void drivingCar(int currentSpeed) {
    this.currentSpeed = currentSpeed;
  } 
}

// Sedan.java
public Class Sedan extends Car {
  public static void main(String[] args) {
    Car car = new Car();
    car.drivingCar(120);
    System.out.println("현재 속도는 " + car.drivingCar + "km/h 입니다");  // result : 현재 속도는 120km/h 입니다
  }
}
```

### 부모 생성자
* 모든 객체는 클래스의 생성자를 호출해야하며 상속한 부모 객체 또한 생성자를 호출 해줘야 한다
* 위 예시처럼 생성자를 명시적으로 선언하지 않았다면 기본 생성자를 생성해 낸다

 ```java
 public Sedan() {
  super();
 }
 ```
 
 * **super();는 부모의 기본 생성자를 호출한다**
 * 만약에 위 예시에서 있는 Car생성자를 호출 하고 싶다면
 ```java
 // 호출 방법
 AccessModifier ChildClassName(parameter1, ...) {
  super(parameter1, parameter2, ...);
 }
 
 
 // Example
 
 // Car.java
 // constructor
  public Car(String carName, int maxSpeed) {
    this.carName = carName;
    this.maxSpeed = maxSpeed;
  }
  
 // Sedan.java
public Class Sedan extends Car {
  public static void main(String[] args) {
    private int passengerCnt;
    public Sedan(String carName, int maxSpeed, int passengerCnt) {
      super(carName, maxSpeed); // 부모 클래스의 생성자 호출
      this.passengerCnt = passengerCnt;
    }
  }
}
```

* 만약에 super(carName, maxSpeed);를 생략한다면
* "Implicit super constructor Car() is undefined. Must explicitly invoke another constructor"이라는 컴파일 오류가 발생한다
* 부모 클래스에 기본 생성자가 없으니 다른 생성자를 명시적으로 호출 해야한다는 오류이다


### Override
상속된 메소드의 내용을 재정의 하는 것</br>
메소드 하나로 객체마다 Ovveride를 통해 다른 기능을 사용할 수 있다(**다형성**)</br>

```java
// Car.java
public class Car {
  void method1() { ... }
  void method2() { ... }
}

// Sedan.java
public class Sedan extends Car {
  @Override
  void method2() { ... }  // 부모클래스의 method2()를 Override
}

// CarExample.java
public class CarExample {
  public static void main(String[] args) {
    Sedan sedan = new Sedan();
    sedan.method1();  // Car 클래스의 method1() 호출
    sedan.method2();  // Sedan 클래스에서 Override된 method2() 호출
    super.method2();  // super를 통해 부모 클래스의 method2()를 호출
  }
}
```

* super는 부모 객체를 참조하고 있기 때문에 super를 통해 Override되었지만 부모 메소드를 접근 할 수 있다

**규칙**
* 부모의 메소드와 동일한 리턴타입, 메소드명, 매개변수를 갖고 재정의
* 접근 제한을 더 강하게 오버라이딩 할 수 없다(강 private > default > protected > public 약)
  *  반대로 확장은 가능하다
* 새로운 Exception을 throws할 수 없다
* 부모 클래스와 자식 클래스 사이에서만 성립된다
* static 메소드는 클래스에 속하는 메소드이기 때문에 상속되지도 않고 Override 되지 않는다
* private 접근제어자에 대해서는 상속되지 않기 때문에 Override 되지 않는다
* final로 지정된 메소드는 오버라이드 할 수 없다


### Abstract Class
* 공통되는 특성을 추출하여 선언한 클래스
* 추상 클래스와 실체 클래스는 상속 관계
* 추상 클래스의 모든 특성을 물려받고, 추가적인 특성을 갖을 수 있다
* 예를들어 Sedan.class, Suv.class, SportCar.class 등에서 실체 클래스에서 공통되는 필드와 메소드를 추출해 선언한 Car.class를 만들 수 있는데 이 Car.class를 추상클래스라고 볼 수 있다
* 추상 클래스는 상속관계이며 물려받은 내용을 이용하기 때문에 new 연산자를 사용해 인스턴스 생성을 할 수 없다
```java
public abstract class ClassName {
  // field
  // constructor
  // method
}
```

#### 추상 클래스의 용도
1. 실체 클래스들의 공통된 필드와 메소드의 이름을 통일할 목적
2. 실체 클래스를 작성할 때 시간을 절약 할 수 있다


## Refernce
> 이것이 자바다 - 신용권 지음</br>
[점프 투 자바 - 상속](https://wikidocs.net/280)</br>
[점프 투 자바 - 추상클래스](https://wikidocs.net/219)

