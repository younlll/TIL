 # 예외처리(Exception)
 
예외란 사용자의 잘못된 조작 또는 개발자의 잘못된 콛3ㅣㅇ으로 인해 발생하는 프로그램 오류를 말한다</br>
예외는 예외처리를 통해 프로그램을 종료하지 않고 정상 실행 상태가 유지되도록 할 수 있다</br>
**예외종류**
* 일반예외(Exception) : 자바 소스를 컴파일하는 과정에서 예외 처리 코드가 필요한지 검사
* 실행예외(RuntimeException) : 컴파일 과정에서 예외처리 코드를 검사하지 않는 예외
* 두 예외 모두 java.lang.Exception 클래스를 상속받는다

### 실행예외(RuntimeException)
#### NullPointExceptoin
* null 값을 갖는 참조 변수로 객체 접근 연산자인 도트(.)를 사용햇을 때 발생한다
        
        String str = null;
        System.out.println(data.toString());
        // NullPointException 에러 발생

#### ArrayIndexOutOfBoundsException
* 배열 인덱스의 범위를 초과하여 사용할 경우 발생

        int[] arr = new int[3];
        for(int i = 0; i < 3; i++) {
         arr[i] = i;
        }
        System.out.println("int[3]: " + arr[3]);
        // ArrayIndexOutOfBoundsExceptin 에러 발생
        
#### NumberFormatException
* 형변환 시, 숫자로 변환될 수 없는 문자가 포함된 경우 에러 발생

        String str = "A60";
        int val = Integer.parseInt(str);  // NumberFormatException 에러 발생
        
#### ClassCastException
* 상위 클래스와 하위 클래스 간에 발생하고 구현 클래스와 인터페이스 간에도 발생
* 이 외의 관계에서는 다른 클래스로 타입변환을 할 수 없다
* 억지로 타입변환을 시도하려 하는 경우, ClassCastException 에러 발생


### 예외처리코드
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

### 예외 발생시키기
#### throws
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




