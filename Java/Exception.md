 # 예외처리(Exception)
 
예외란 사용자의 잘못된 조작 또는 개발자의 잘못된 코딩으로 인해 발생하는 프로그램 오류를 말한다</br>
예외는 예외처리를 통해 프로그램을 종료하지 않고 정상 실행 상태가 유지되도록 할 수 있다</br>
**예외종류**
* 일반예외(Exception) : 자바 소스를 컴파일하는 과정에서 예외 처리 코드가 필요한지 검사
* 실행예외(RuntimeException) : 컴파일 과정에서 예외처리 코드를 검사하지 않는 예외
* 두 예외 모두 java.lang.Exception 클래스를 상속받는다

</br>

## 실행예외(RuntimeException)
### NullPointExceptoin
* null 값을 갖는 참조 변수로 객체 접근 연산자인 도트(.)를 사용했을 때 발생한다
        
        String str = null;
        System.out.println(data.toString());
        // NullPointException 에러 발생

### ArrayIndexOutOfBoundsException
* 배열 인덱스의 범위를 초과하여 사용할 경우 발생

        int[] arr = new int[3];
        for(int i = 0; i < 3; i++) {
         arr[i] = i;
        }
        System.out.println("int[3]: " + arr[3]);
        // ArrayIndexOutOfBoundsExceptin 에러 발생
        
### NumberFormatException
* 형변환 시, 숫자로 변환될 수 없는 문자가 포함된 경우 에러 발생

        String str = "A60";
        int val = Integer.parseInt(str);  // NumberFormatException 에러 발생
        
### ClassCastException
* 상위 클래스와 하위 클래스 간에 발생하고 구현 클래스와 인터페이스 간에도 발생
* 이 외의 관계에서는 다른 클래스로 타입변환을 할 수 없다
* 억지로 타입변환을 시도하려 하는 경우, ClassCastException 에러 발생

</br>

## 예외처리코드
예외처리 코드는 **try-catch-finally** 를 이용한다
```java
try {
  // 예외 발생 가능 코드
} catch(Exception e) {
  // 예외처리
} finally {
  // 예외가 발생하더라도 반드시 실행되는 부분
}
```

### 다중 catch
  * 발생되는 예외별로 예외처리 코드를 다르게 하는 경우 여러개의 catch문을 작성하면 된다
  * catch문이 여러개라도 예외가 발생한 순간 프로그램은 멈추기 때문에 해당 예외를 처리하는 catch블럭으로 이동하게 되므로 하나의 catch문만 실행된다
  * 상위 예외 클래스가 하위 예외 클래스보다 나중에 작성되어야 한다

### 멀티 catch
  * 자바7부터 catch 블록에서 여러 개의 예외를 처리할수 있도록 멀티 catch 기능이 추가되었다

</br>

## 자동 리소스 닫기
* 자바 6 까지는 close() 메소드를 호출해 리소스를 해제해주었다

```java
FileInputStream fis = null;
try {
  fis = new FileInputStream("file.txt");
  ...
} catch(IOException e) {
  ...
} finally {
  if(fis != null) {
    try {
      fis.close();
    } catch (IOException) { }
  }
}
```

* 자바 7 이후부터는 try 블록이 정상적으로 실행을 완료했거나 도중에 예외가 발생하게 되면 자동으로 close() 메소드가 호출된다

```java
try(FileInputStream fis = new FileInputStream("file.txt")) {
  ...
} catch(IOException e) {
  ...
}
```

* try-with-resources를 사용하기 위해서는 조건이 있는데, 리소스 객체는  java.lang.AutoCloseable 인터페이스를 구현하고 있어야 한다.
* AutoCloseable에는 close() 메소드가 정의되어 있는데 try-with-resources는 바로 이 close() 메소드를 자동 호출한다

</br>

## 예외 떠넘기기
* 예외에 대한 처리를 경우에 따라 메소드를 호출한 곳으로 떠넘길 수 있다
* throws 키워드를 통해 떠넘긴다

</br>

## 사용자 정의 예외와 예외 발생
* 자바 표준 API에서 제공하는 예외 클래스 이외에  예외처리가 필요할 때 사용한다
* 애플리케이션 서비스와 관련된 예외를 Application Exception 이라 한다

### 예외 발생시키기
**throws**
* 예외를 여기서 처리하지 않고 다른 녀석에게 예외처리를 넘긴다

```java
public static void divide(int a, int b) throws ArithmeticException {
  if(b == 0) {
    throw new ArithmeticException("0으로 숫자를 나눌 수 없습니다");
  }
  System.out.println(a/b);
}

public class ExceptoinThrowExample {
  public static void main(String[] args) {
    try {
      dvide(a, b);
    } catch(ArithmeticException e) {
      e.getMessage();
      e.printStackTrace();
    }
  }
}
```

* throw는 Exception을 발생시킬 때 사용하는 키워드
* throws는 메소드를 정의할 때 사용하며, 이 메소드에서 발생할 수 있는 Exception을 명시적으로 정의할 때 사용

</br>

## 예외 정보 얻기
* 모든 예외는 Exception 클래스를 상속하고 여기서 getMessage()와 printStackTrace() 메소드를 가장 많이 사용하여 예외 객체를 호출한다

```java
try {
  ...
} catch (예외클래스 e) {
  String msg = e.getMessage();  // 예외가 가지고 있는 message 얻기
  e.printStackTrace();  // 예외의 발생 경로 추적
}
```


### Reference
> 이것이 자바다 - 신용권 지음</br>
[codehcacha-trhow와 throws의 차이점](https://codechacha.com/ko/java-throw-and-throws/)</br>
[점프 투 자바-예외처리](https://wikidocs.net/229)

