# Interface(인터페이스)
* 자바 인터페이스는 추상메서드의 모음이다
* 여러 구현체에서 공통적인 부분을 추상화 한것이다(다형성)
* 개발 코드와 객체가 서로 통신하는 접점 역할
* 객체의 내부 구조를 알 필요가 없고 인터페이스의 메소드만 알고 있으면 된다
* 개발 코드가 직접 객체의 메소드를 호출하지 않고 인터페이스를 사용하는 이유는 객체 내부에 메소드를 직접 구현했다면 상황에 따라 개발 코드를 수정해야 하는 일이 발생할 수 있지만
* 인터페이스를 통해 개발 코드를 수정하지 않고 사용하는 객체를 변경할 수 있도록 하기 위해서 이다
* 인터페이스는 하나의 객체가 아니라 여러 객체들과 사용이 가능하므로 어떤 객체를 사용하느냐에 따라 실행 내용과 리턴값이 다를 수 있다
* 따라서 개발코드 측면에서 코드 변경 없이 실행 내용과 리턴값을 다양화 할 수 있다는 장점을 갖게 된다

```java
public interface InterfaceName {
  // constant
  type constantName = value;
  
  // abstract method
  type methodName(parameter1, ...);
  
  // default method
  default type methodName(parameter1, ...){
    // ...
  };
  
  // static method
  static type methodName(parameter1, ...){
    // ...
  };
}
```

* **Consstant Field**
  * 인터페이스 내에 데이터를 저장할 수 있는 필드 선언은 안되지만 상수 필드는 선언이 가능하다
  * public static final type fieldName = value; // public static final을 생략하더라도 컴파일 과정에서 생성해준다
* **Astract Method**
  * 구현부가 없는 메소드이다
  * 인터페이스를 구현하기로 한 클래스는 반드시 인터페이스에 명시되어 있는 모든 추상메서드들을 구현해야 한다
  
  ```java
  public class Dog implements Walkable {
    @Override
    public void walk() {
      // ...
    }
  }
  ```
  
* **Default Method**
  * Java 8버전 이상부터는 인터페이스에서 default 접근 제어자를 사용할 수 있다 → 기존 인터페이스를 확장해서 새로운 기능을 추가하기 위함
  * public default returnType method1(paramter1, ...) { ... } → public은 생략 가능하면 compile 과정에서 생성해준다
  * 실제 구현내용까지 작성
  * 실제 구현내용이 작성되어 있지만 Override를 통해서 재작성 할 수 있다
  * 라이브러리를 업데이트 할 때, 인터페이스에 추가된 기능이 있다면 구현한 클래스 역시 해당 메소드를 구현해주어야 하지만 사용자가 해당 인터페이스를 사용하면서 메소드를 구현하지 않아 컴피일 에러가 발생할 것이다
  * 이러한 불편함을 해소하기 위해 default 키워드를 지원하였다
* **Static Method**
  * Java 8버전 이상부터는 인터페이스에서 static 접근 제어자를 사용할 수 있다
  * public static returnType method1(paramter1, ...) { ... } → public은 생략 가능하면 compile 과정에서 생성해준다


### 인터페이스 구현
    public class ClassName implements InterfaceName {
      // 인터페이스에 선언된 추상 메소드 구현
    }
    
```java
public class BMW immplenments Car {
  @Override
  public String getManufacturer() {
    return "BMW";
  }
  
  @Override
  public String getSeries() {
    return "The new 5";
  }
}
```

* 인터페이스의 모든 메소드는 기본적으로 public 접근제한자를 갖기 때문에 public보다 낮은 접근 제한으로 작성 할 수 없다
* public을 생략하면 "Cannot reduce the visibility of the inherited method"라는 컴파일 에러가 발생한다
* 인터페이스의 추상 메소드를 작성하지 않는다면 구현 클래스는 자동으로 추상클래스가 되기 때문에 **abstract** 키워드를 추가해야한다
* 또한, 인터페이스는 상속과 달리 다중 인터페이스를 지원한다

    public abstract class ClassName implements InterfaceName {
      public void method1() {};
    }

### 익명 구현 객체
* **일회성의 구현 객체** 를 위해 소스 파일을 만들고 클래스를 선언하는 것은 비효율적이다
* 따라서 소스파일을 만들지 않고 구현 객체를 만들 수 있는 방법을 제공하는 것이 익명 구현 객체 이다
* 하나의 실행문이므로 끝에 세미콜론을 붙여야한다

    InterfaceName var = new InterfaceName() {
      // 인터페이스에 선언된 추상 메소드 구현
    };
    
```java
public interface Car {
  int MAX_SPEED = 230;
  void getManufacturer();
}

public class Sedan {
  public static void main(String[] args) {
    Car car = new Car() {
      public void getManufacturer() {
        // 구현
      }
    };
  }
}
```

### Reference
> 이것이 자바다 - 신용권 지음</br>
[점프 투 자바 - 인터페이스](https://wikidocs.net/217)</br>
[SungBum Park - 인터페이스](https://velog.io/@codemcd/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4Interface)
