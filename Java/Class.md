# Class(클래스)
* 소프트웨어를 개발할 때에도 부품에 해당하는 객체들을 먼저 만들고, 이것들을 하나씩 조립해서 완성된 프로그램을 만드는 기법을 `객체 지향 프로그래밍(OOP: Object Oriented Programming)`이라고 한다
* `객체`란 자신의 속성을 가지고 있고 다른 것과 식별 가능한 것을 말한다
* 그리고 이 객체들간의 상호작용의 수단은 `메소드`이고 객체가 다른 객체의 기능을 이용하기 위해 `메소드를 호출`한다
* 객체는 다른 객체와 관계를 맺기도 하는데 집합 관계, 사용 관계, 상속 관계가 있다

### 객체 지향 프로그래밍의 특징
**캡슐화(Encapsulation)**
* `캡슐화`란 실제 구현 내용을 외부에서 알 수 없도록 감추는 것을 말한다
* 캡슐화를 하는 이유는 외부의 잘못된 사용으로 인해 객체가 손상되지 않도록 하는 것이다
* 이런 제어는 접근제한자를 통해 객체의 필드와 메소드의 사용 범위를 제한한다

**상속(Inheritance)**
* `상속`은 상위 객체가 가지고 있는 필드와 메소드를 하위 객체에게 물려주어 `하위 객체가 사용할 수 있도록` 해준다
* 상위객체를 `재사용`함으로써 하위 객체를 쉽고 빠르게 설계할 수 있도록 도와준다
* 재사용을 통해 새로운 객체를 만들기 때문에 `반복되는 코드의 중복을 줄여준다`

**다형성(Polymorphism)**
* `다형성`은 같은 타입이지만 실행 결과가 다양한 객체를 이용할 수 있는 성질을 말한다
* 자바는 다형성을 위해 부모 클래스 또는 인터페이스의 타입 변환을 허용한다
* 부모 타입에는 모든 자식 객체가 대입될 수 있고, 인터페이스 타입에는 모든 구현객체가 대입될 수 있다
* 다형성의 효과로 객체는 부품화가 가능하다

</br>

## 객체와 클래스
* 클래스에는 객체를 생성하기 위한 필드와 메소드가 정의되어 있다
* 클래스로부터 만들어진 객체를 해당 클래스의 `인스턴스`라고 한다

</br>

## 클래스 선언
    public class className {
    }

* 두 개 이상의 클래스가 선언된 소스 파일을 컴파일하면 바이트 코드 파일은 클래스를 선언한 갯수만큼 생긴다
* 결국 소스파일은 클래스 선언을 담고 잇는 저장 단위일 뿐이지 클래스 자체가 아니다

</br>

## 객체 생성과 클래스 변수
    className varName = new className();
* className 클래스를 new 연산자를 통해 메모리(Heap영역)에 객체를 생성하고 객체의 주소를 리턴한다
* 생성된 객체들은 className 클래스의 인스턴스이다
* 클래스의 용도
  * 라이브러리(API: Application Program Inteface)
  * 
* new 연산자를 사용한 만큼 객체가 메모리에 생성된다

```java
// Car.java
public class Car {
  // code skip
}

// CarExample.java
public class CarExample {
  public static void main(String[] args) {
    Car c1 = new Car();
    Car c2 = new Car();
  }
}
```
* Car클래스를 new 연산자를 통해 Heap영역에 객체를 생성하고 Stack영역에 c1, c2 이름을 갖는 변수가 Heap영역에 생성된 객체의 주소를 저장하며 참조한다
* 따라서, c1과 c2는 Car라는 클래스로부터 생성되지만 완전히 독립된 서로 다른 객체이다

### 클래스의 구성
```java
public class ClassName {
  // 1. 필드
  type filedName;
  
  // 2. 생성자
  ClassName() {
    // ...
  }
  
  // 메소드
  returnType methodName() {
    // ...
  }
}
```
#### 1. 필드
* 필드는 객체의 고유 데이터, 부품 객체, 상태 정보를 저장하는 곳이다.
* 변수 != 필드
* 변수는 생성자와 메소드 내에서만 사용되고 생성자와 메소드가 실행 종료되면 자동 소멸된다
* 필드는 생성자와 메소드 전체에 사용되며 객체가 소멸되지 않는 한 객체와 함께 존재한다
* 도트(.) 연산자는 객체 접근 연산자로 객체가 가지고 있는 필드나 메소드를 사용하고자 할때 사용된다
* 필드는 기본 초기값으로 자동 설정되고 다른 값으로 초기화를 원하는 경우 `필드 선언시 초기화`를 하거나 `생성자에서 초기값을 주는 방법`
<table>
  <tr>
    <td colspan="2">분류</td>
    <td>데이터 타입 -> 초기값</td>
  </tr>
  <tr>
    <td rowspan="3">기본 타입</td>
    <td>정수 타입</td>
    <td>byte -> 0</br>char -> 공백</br>short -> 0</br>int -> 0</br>long -> 0L</td>
  </tr>
  <tr>
    <td>실수 타입</td>
    <td>float -> 0.0F</br>double -> 0.0</td>
  </tr>
  <tr>
    <td>논리 타입</td>
    <td>boolean -> false</td>
  </tr>
  <tr>
    <td colspan="2">참조 타입</td>
    <td>Array -> null</br>class(include String) -> null</br>interface -> null</td>
  </tr>
</table>

```java
// Car.java
public class Car {
  // Filed
  String modelName;
  int maxSpeed;
}

// BMW.java
public class BMW {
  // Object create
  Car myBmwCar = new Car();
  
  // Change filed value
  modelName = "BMW 3series";
  maxSpeed = 235;
}
```

#### 2. 생성자
* 객체 생성 시 초기화 역할을 담당한다
* 생성자의 규칙
  * 클래스명과 메소드명이 동일하다
  * 리턴타입을 정의하지 않는다
**default 생성자**
모든 클래스는 생성자가 반드시 존재하며, 하나 이상을 갖을 수 있다
```java
public class Bmw {
  public void accelerate() {
    // ...
  }
}
```

* 클래스에 생성자가 없다면 자동으로 **defalt 생성자( public BMW() {} )** 를 추가해준다
* 클래스에 생성자를 선언하지 않아도 new 연산자 뒤에 기본 생성자를 호출해서 객체를 생성시킬 수 있다

    Car myCar = new Car();  // new Car()를 하면서 Car()를 통해 기본 생성자를 호출하여 객체를 

* 생성자를 작성한다면
```java
className (parameter1, parameter2, ...) {
  // 객체의 초기화 
}
```

**생성자 오버로딩**
* 하나의 클래스에 여러개의 입력항목이 다른 생성자를 만들 수 있다
* `매개 변수의 타입, 개수, 순서가 다르게 선언`
```java
public class Car {
  public Car(String name) {
      this.setName(name);
  }
  
  public Car(int type) {
    if (type == 1) {
      this.setType("SUV");
    } else if (type == 2) {
      this.setType("sedan");
    }
  }
  
  public static void main(Stringp[] args) {
    Car bmw = new Car("bmw 3series");   // parameter type이 String이면서 갯수가 1개인 생성자 호출
    Car carType = new Car(2);           // parameter type이 int이면서 갯수가 1개인 생성자 호출
  }
}
```

* 클래스에서 다른 생성자를 호출하고 싶을 경우 this(매개변수1, 매개변수2, ...); 

#### 3. 메소드
* 객체의 동작에 해당한다
* 몇 개의 매개 변수가 입력될지 모르는 경우 `매개 변수를 배열 타입 int func(int[] params) { ... }`으로 선언한다
* 그런데 배열로 선언하게 되면 배열을 생성해야하는 불편한 점이 있어
* 매개 변수를 `···`를 사용해서 선언`int func2(int ··· params) { ... }`하게 되면, 메소드 호출 시 넘겨준 값의 수에 따라 자동으로 배열이 생성되고 매개값으로 사용된다

**메소드 오버로딩**
* 클래스 내에 같은 이름의 메소드를 여러개 선언하는 것
* 메소드 오버로딩 조건은 **매개변수의 타입과 개수가 달라야한다**
* 리턴타입은 무관하며 메소드이름은 같다

#### 4. 인스턴스 멤버와 this
* 인스턴스 멤버 : **객체를 생성한 후 사용할 수 잇는 필드와 메소드**
* this : 객체내부에서 인스턴스 멤버에 접근하기 위해 사용
```java
// ex1
Car(String model) {
  this.model = model;
}

// ex2
void setModel(String model) {
  this.model = model;
}
```
* 매개변수 model의 값을 필드 model에 저장하는 경우이다

#### 5. 정적멤버와 static
* 정적 멤버는 클래스에 고정된 멤버로서 객체를 생성하지 않고 사용할 수 있는 필드와 메소드
* 항상 값이 변하지 않는 경우, `static`을 사용(→ 메모리 이점)
```java
public class ClassName {
  // static field
  static typeName filedName;
  
  // static method
  static returnType methodName(parameter1, parameter2, ...) {
    // ...
  }
}
```
* 정적 필드와 정적 메소드는 클래스에 고정된 멤버로 `클래스 로더가 바이트코드를 로딩해서 메소드 메모리영역에 적재할 때 클래스별로 관리`된다
* 클래스의 로딩이 끝나면 바로 사용할 수 있다
* 객체마다 가지고 있어야할 데이터라면 인스턴스 필드, 공용적인 데이터라면 정적 필드를 선언하는 것이 좋다
```java
public class Car {
  int speed;
  static int wheelCnt = 4;
  
  void setMaxSpeed(int speed) {
    this.speed = speed;
  }
  static int driveStop() {
    this.speed = 0;
    return speed;
  }
}
```
* 정적필드는 선언과 동시에 초기값을 설정하는 것이 보통이다
* 자동차의 최고속력은 모두 다르다 = 인스턴스 필드
* 자동차의 바퀴는 어떠한 자동차든 4개를 갖고있다 = static 필드
* 자동차마다 최고속력은 다르기 때문에 최고속력을 저장하는 setMaxSpeed()는 인스턴스 메소드이다
* 모든 자동차는 주행을 멈추면 속력이 0이기 때문에 driveStop()은 static 메소드이다

* 정적 필드와 정적 메소드는 객체 참조 변수로 접근이 가능하지만 **원칙적으로 클래스 이름으로 접근해야 한다**
* 정적 메소드와 정적 블럭은 객체가 없어도 실행이 되는 특징 때문에, 내부에 인스턴스 필드나 인스턴스 메소드를 사용할 수 없다
* 객체 자신의 참조인 this 키워드도 사용이 불가능하다


#### 6. 싱글톤(Singleton)
* 단 하나의 객체만 만드는 경우
* 싱글톤은 외부에서 생성자를 호출하지 못하도록 private로 지정해야한다
```java
public class Singleton {
  private static Singleton instance = new Singleton();
  
  private Singleton() {
    // 생성자는 외부에서 호출되지 못하도록 private로 지정
  }
  
  public static Singleton getInstance() {
    return instance;
  }
}
```

* 외부에서 객체를 이용하려면 **ClassName var1 = ClassName.getInstance()** 를 이용해야 한다
* 또한, 외부 여러곳에서 참조하게 되더라도 getInstance()메소드는 단 하나의 객체만 return하기 때문에 동일한 객체를 참조하게 된다

**장점**
<ul>
ⓐ new연산자를 통해 한번만 객체를 생성하므로 고정된 메모리 영역을 사용하게 되기 때문에 메모리 낭비를 방지할 수 있다
ⓑ 생성된 인스턴스를 활용하게 되므로 속도 측면에서도 이점이 있다
ⓒ 다른 클래스간에 데이터 공유가 쉽다
</ul>

**단점**
<ul>
ⓐ 여러 클래스의 인스턴스에서 싱글톤 인스턴스의 데이터에 동시에 접근할 수 있어 동시성 문제가 발생 할 수 있다</br>
ⓑ 자원을 공유하고 있기 때문에 테스트가 어렵다</br>
ⓒ SOLID원칙 중 DIP를 위반</br>
ⓓ 자식클래스를 만들수 없고, 내부 상태를 변경하기 어렵다</br>
</ul>

#### 7. final필드와 상수
**final필드**
* final필드는 초기값이 저장되면 프로그램 실행 도중에 변경이 불가하다
* 초기화 방법은 필드 선언시에 주는 방법과 생성자에서 주는 방법 2가지 이다
```java
public class FinalField {
  final String field1 = "Init";
  final String field2;
  
  pubilc FinalField(String field2) {
    this.field2 = field2;
  }
}
```

#### 상수
* 상수: 불변의 값
* Q. final은 한번 초기화하면 값의 변경을 할 수 없다고 했는데 이 자체만으로도 상수의 의미에 부합하는게 아닌지라는 의문을 갖게 되었다
* 불변의 값이라는 것은 객체마다 저장할 필요가 없으며 여러 값으로 초기화 될 수 없어야하기 때문이다
* 하지만 final 필드는 객체마다 저장되고 생성자를 통해 객체마다 다른 값을 갖도록 초기화가 가능하기 때문에 final 필드를 상수라고 부르지 않는다
* 따라서 `상수는 static이면서 final`이어야 한다


```java
static final type var1 = init_value;
static final type var2;
static {
  val2 = init_calculation_formula;
  // 복잡한 초기화의 경우, 정적블록에서 초기화를 하기도 한다
}
```


#### 8. 접근제한자
|접근 제한|적용 대상|접근할 수 없는 클래스|
|--------|--------|--------------------|
|public|class, field, constructor, method|x|
|protected|field, constructor, method|자식 클래스가 아닌 다른 패키지에 소속된 클래스|
|default|class, field, constructor, method|다른 패키지에 소속된 클래스|
|private|field, constructor, method|모든 외부 클래스|
```java
// default
class ClassNamae {
  //...
}

//public
public class ClassName {
  //...
}
```

#### 9. Getter and Setter
**Setter**
* 객체 지향 프로그래밍에서는 객체의 무결성이 깨질수 있기 때문에 외부에서 직접 접근하는 것을 막는다
* 이러한 문제점을 해결하기 위해 메소드를 통해 데이터를 변경하는 방법을 선호한다
* 메소드는 공개해서 매개변수로 받는 값을 검증해 유효한 값만 데이로 저장 할 수 있기 때문이다
* 이러한 역할을 **Setter** 가 한다
**Getter**
* 외부에서 데이터를 읽을 때도 메소드를 사용한다
```java
private type fieldName;

// Getter
// Boolean type의 경우 get대신에 is를 붙여 isFieldName으로 하는 것이 관례이다
public returnType getFieldName() {
  return fieldName;
}

// Setter
public void setFieldName(type fieldName) {
  this.fieldName = fieldName;
}
```

#### 10. Annotation
* Annotation은 metadata로 볼 수 있다
* metadata란 컴파일 과정과 실행 과정에서 코드를 어떻게 컴파일하고 처리할 것인지 알려주는 정보이다
* **@AnnotationName** → 이러한 형태로 사용된다

**용도**
<ul>
  ⓐ 컴파일러에게 코드 문법 에러를 체크하도록 정보를 제공</br>
  ⓑ 소프트웨어 개발 툴이 빌드나 배치 시 코드를 자동으로 생성할 수 있도록 정보를 제공</br>
  ⓒ 실행 시 특정 기능을 실행하도록 정보를 제공</br>
</ul>

**어노테이션 타입 정의와 적용**
```java
public @interface AnnotationName {
  type elemntName() \[default value\];
}
```

* default값을 설정하지 않는 경우 **@Annotation(elementName = value);** 형태로 값을 지정해줘야하며 default값이 정의된 경우에는 해당 형태로 값을 넣어줘도 되고 생략해도 된다
* Annotation은 class, field, method에만 적용할 수 있다(생성자에는 적용이 불가하다)
* 

### Reference
> 이것이 자바다 - 신용권 지음</br>
> [05-5. 생성자 - 점프 투 자바](https://wikidocs.net/281)
