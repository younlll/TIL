# 람다식
## 람다식이란
* 함수적 프로그래밍 지원을 위해 Java 8부터 람다식을 지원하였다
* 람다식을 사용하면 코드가 매우 간결해지고, 컬렉션의 요소를 필터링하거나 매핑해서 원하는 겨로가를 쉽게 집계할 수 있기 때문이다
* 람다식의 현태는 매개변수를 가진 코드 블럭이지만 런타임 시에는 익명 구현 개체를 생성한다
* Runnable 인터페이스로 람다식을 살펴보자면

```java
Runnable runnable = new Runnable() {
    public void run() { ... }
};

// 위의 익명 구현 객체를 람다식으로 표현하면
Runnable runnable = () -> { ... }
```

</br>

## 람다식 기본 문법
        (타입 매개변수, ...) -> { 실행문; ... }

* (타입 매개변수, ...)은 실행문을 수행하기 위해 필요한 값을 제공하는 역할을 한다
* 매개 변수 타입은 런타임 시, 자동으로 인식 할 수 있기때문에 생략한다
* 하나의 매개 변수만 있는 경우에는 ()를 생략할 수 있다(매개 변수가 없는 경우에는 괄호룰 반드시 작성해야한다)
* 하나의 실행문만 있다면 {}를 생략할 수 있다

</br>

## 타겟 타입과 함수적 인터페이스
### 함수적 인터패이스
* 람다식이 하나의 메소드를 정의하기 때문에 두 개 이상의 추상 메소드가 선언된 인터페이스는 람다식을 이용해서 구현 객체를 생성할 수 없다
* 하나의 추상 메소드가 선언된 인터페이스만 람다식의 타겟 타입이 될 수 있다
* 이러한 인터페이스를 `함수적 인터페이스`라고 한다
* 함수적 인터페이스를 작성할 때 두 개 이상의 추상 메소드가 선언되지 않도록 컴파일러가 확인하는 기능이 있는데. 인터페이스 선언 시 @FunctionalInterface 어노테이션을 붙이면 된다

```java
@FunctionalInterface
public interface MyFunctionalInterface {
    public void method();
    public void otherMethod();  // 컴파일 오류 발생
}
```

### 매개 변수와 리턴값이 없는 람다식
```java
@FunctionalInterface
public interface MyFunctionalInterfaace {
    public void method();
}
```

```java
public class MyFunctionalInterfaceExample {
    public static void main(String[] args) {
        MyFunctionalInterface fi;

        fi = () -> {
            String str = "method call1"l
            System.out.println(str);
        };
        fi.method();

        fi = () -> { System.out.println("method call2"); };
        fi.method();

        fi = () -> System.out.println("method call3");
        fi.method();
    }
}
```

### 매개 변수가 있는 람다식
```java
@FunctionalInterface
public interface MyFunctionalInterface {
    public void method(int x);
}
```

```java
public class MyFunctionalInterfaceExample {
    public static void main(String[] args) {
        MyFunctionalInterface fi;

        fi = (x) -> {
            int result = x + 5;
            System.out.println(result);
        };
        fi.method(2);

        fi = (x) -> { System.out.println(x*5); }
        fi.method(2);

        fi = x -> System.out.println(x*5);
        fi.method(2);
    }
}
```

### 리턴값이 있는 람다식
```java
@FunctionalInterface
public interface MyFunctionalInterface {
    public int method(int x, int y);
}
```

```java
public class MyFunctionalInterfaceExample {
    public static void main(String[] args) {
        MyFunctionalInterface fi;

        fi = (x, y) -> {
            int result = x + y;
            return result;
        };
        System.out.println(fi.method(2, 5));

        fi = (x, y) -> { return x + y; };
        System.out.println(fi.method(2, 5));

        fi = (x, y) -> sum(x, y);
        System.out.println(fi.method(2, 5));
        
    }

    public static int sum(int x, int y) {
        return (x + y);
    }
}
```

</br>

## 클래스 멤버와 로컬 변수 사용
### 클래스의 멤버 사용
* 클래스의 멤버인 필드와 메소드를 제약 사향 없이 사용할 수 있다
* 람다식에서 this는 람다식을 실행한 객체의 참조이다

<img src="./image/lambda_01.png">

</br></br>

### Reference
> 이것이 자바다 - 신용권지음