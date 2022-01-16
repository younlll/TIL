# 참조 타입
* `참조 타입`이란 객체의 번지를 참조하는 타입으로 배열, 열거, 클래스, 인터페이스 타입을 말한다

```java
int age = 26; // 기본타입
String name = "youn"; // 참조타입
```

    기본타입과 참조타입 둘 다 변수는 Stack영역에 생성된다
    참조타입의 객체는 Heap영역에 생성된다
    따라서 Stack영역에 생성된 참조타입의 변수는 Heap영역에 생성된 객체의 주소값을 갖는다

## 메모리 사용 영역
### 메소드 영역
* 클래스들을 클래스 로더로 읽어 클래스별로 런타임 상수 풀, 필드 데이터, 메소드  데이터, 메소드 코드, 생성자 코드 등 분류해서 저장한다
* 모든 쓰레드가 공유하는 영역이다

### 힙 영역
* 객체와 배열이 생성되는 영역이다
* 힙 영역의 객체와 배열은 JVM 스택 영역의 변수나 다른 객체의 필드에서 참조된다
* 만약 참조되는 변수나 필드가 없다면 쓰레기 객체로 보고 GC를 실행시켜 메모리에서 해제시킨다

### 스택 영역
* 각 쓰레드마다 하나씩 존재한다
* JVM 스택은 메소드를 호출할 때마다 Frame을 추가하고 메소드가 종료되면 해당 Frame을 제거하는 동작을 수행한다

</br>

## 참조 변수의 동등비교 연산
* 참조 타입 변수들간의 동등비교(==, !=) 연산은 주소값을 비교한다

<img src="https://user-images.githubusercontent.com/62369538/148268144-ed87184d-d2d8-410a-81aa-0e0daf4b4210.PNG" width="350" height="250"/>

    var1 == var2 → true / 같은 주소를 바라봄
    var1 == var3 → false / 다른 주소를 바라봄
    var1 != var3 → tru

</br>

## null과 NullPointerException
* 참조 타입 변수가 null을 가지고 있을 경우, 참조할 객체의 주소값이 없는 것이므로 참조 타입 변수를 사용할 수 없다
* null값의 주소를 참조하는 변수를 사용하게 되면 NullPointerException이 발생한다

</br>

## String 타입
    String 변수 = "문자열";
    변수 = "문자열";

* 변수는 Stack영역에 문자열 객체의 주소값을 갖으면서 생성된다
* 주소값에 대한 String 객체는 Heap영역에 생성된다
* String도 참조 타입이므로

    String str1 = "Youn";
    String str2 = "Youn";

* 위처럼 선언된 경우 `str1 == str2`와 같이 비교하게 되면 두 변수에 담겨있는 주소값을 비교하는 것이다
* 변수가 갖는 문자열이 같은지 비교하고 싶다면 `equals()` 메소드를 이용해 비교해야한다

    str1.equals(str2);

* String과 같이 new를 사용하지 않고 리터럴을 사용한 객체는 **consant pool을 이용하게 된다**
* 그래서 **상수풀에 동일한 문자열이 있으면 그 주소값을 반환**하게 되어 다른 변수이지만 같은 주소값을 갖게 되고 이런경우 == 연산자로 비교하면 같은 주소값이므로 true가 반환된다

</br>

## 배열 타입
* 배열은 같은 타입의 데이터를 연속된 공간에 나열시키고, 각 데이터에 인덱스(index)를 부여한 자료구조이다
* 각 인덱스는 각 항목의 데이터를 읽거나 저장하는데 사용된다

### 배열 선언
    dataType[] varName;
    dataType varName[];
    dataType[] varName = new dataType[arraySize];
    
    int[] intArray1;
    int intArray2[];
    int[] intArray3 = new int[5]; // 크기가 5인 int 타입을 갖는 배열을 생성
    
    // 값 초기화
    dataType[] varName = {val1, val2, val3, ...};

* 참조할 배열 객체가 없다면 배열 변수를 null로 초기화 할 수 있다
* 위와 같이 배열 항목에 저장될 값의 목록을 만들어 준다면 아래처럼 스택 영역과 힙 영역에 변수와 객체가 생성이 될 것이다

<img src="https://user-images.githubusercontent.com/62369538/148271756-4e92ba37-b571-4bc1-b541-a83b7680a716.PNG" height="300" width="400"/>

* 배열은 변수를 이미 선언한 후에는 중괄호를 사용해 배열 생성을 할 수 없다
  * `varName = {val1, val2, val3, ...};` 컴파일 에러 발생

* 배열 변수를 선언한 후에 목록을 넣어주려면 new 연산자를 이용해야한다
  * `varName = new dataType[] {val1, val2, val3, ...};`

### 배열 길이
* 배열 길이는 length 필드를 읽으면 되고 사용은 `배열변수.length`와 같이 작성하여 사용하면 된다
* length 필드는 읽기 전용 필드이기 때문에 값의 변경을 할 수 없다

### 커맨드 라인 입력
* Java의 main 메소드를 보면 `public static void main(String[] args) {...}`로 구성되어 있다
* 여기서 String[] args는 커맨드 창에서 `java 클래스명`으로 프로그램을 실행시키면
* JVM은 길이가 0인 배열을 먼저 생성하고 main() 메소드를 호출할 때 매개값으로 전달한다
* 만약 `java 클래스명` 뒤에 공백으로 구분된 문자열 목록을 주고 실행시키면 문자열 목록으로 구성된 String[] 배열이 생성되고
* main() 메소드를 호출할 때 매개변수 값으로 전달된다

### 다차원 배열
* `int[][] scores = new int[2][3];`과 같이 선언하면 2X3 행렬 구조를 갖는 다차원 배열이 생성된다

    int[][] scores = new int[2][];
    scores[0] = new int[2];
    scores[1] = new int[3];

* 위와같이 각 행마다 열의 갯수가 다르게 선언할 수 있다

<img src="https://user-images.githubusercontent.com/62369538/148273745-32c6b69c-e60c-417f-922b-0e45047b5021.PNG" height="300" width="450"/>

* Stack 영역에 생성된 변수는 배열 객체의 행 정보를 담고 있는 주소값을 바라보며
* Heap 영역의 배열 객체는 각 행의 인덱스마다 열 정보를 담고 잇는 주소값을 가리킨다

### 객체를 참조하는 배열
* 기본타입(byte, char, short, itn, long, float, double, boolean) 배열은 각 항목에 직접 값을 갖고 있지만
* 참조타입(클래스, 인터페이스) 배열은 각 항목에 객체의 주소값을 갖고 있다

```java
String strArray = new String[3];
strArray[0] = "Java";
strArray[1] = "C++";
strArray[2] = "C#";
```

<img src="https://user-images.githubusercontent.com/62369538/148274626-8720a8ae-f4da-4f12-a81b-438fe3880883.PNG" height="300" width="450"/>

### 배열 복사
* 배열 간의 항목 값들을 복사하려면 for문을 사용하거나 System.arraycopy() 메소드를 사용하면 된다
* 여기서 arraycopy()메소드는 `System.arraycopy(원복배열, 복사를 시작할 인덱스, 붙여넣을 새 배열, 붙여넣기 시작할 인덱스, 복사할 갯수)`

**얕은 복사(shallow copy)**
* 배열 복사가 되면 복사되는 값이 객체의 주소값이므로 새 배열의 항목은 이전 배열의 항목이 참조하는 객체와 동일한 경우이다
* 주소값이 복사되므로 값이 변경되면 해당 주소를 참조하는 모든 배열들의 값이 변경된다

```java
int[] arr1 = new int[2];
arr1[0] = 1;
arr1[1] = 2;

int[] arr2 = arr1;

arr2[0] = 3;
arr2[1] = 4;

System.out.println(arr1[0] + ", " + arr1[1]);
```

![image](https://user-images.githubusercontent.com/62369538/148275533-172e5279-3716-4784-b46c-4a09f83c3e91.png)
<img src="https://user-images.githubusercontent.com/62369538/148275705-f41f56b9-2bfb-459e-94cc-469a40e1fbc2.PNG" height="300" width="450"/>

**깊은 복사(deep copy)**
* 참조하는 객체도 별도로 생성되는 것을 말한다
* 새로운 메모리 공간에 값을 복사하는 것이므로 한쪽 값을 수정해도 다른 배열에 영향을 끼치지 않는다

<img src="https://user-images.githubusercontent.com/62369538/148276023-0ff3f815-9ce6-4f88-a5e2-1cc3dc1d6dec.PNG" height="300" width="450"/>

### 향상된 for문
* for문의 증감식을 사용하지 않는 방식이다
* 배열에 가져올 값이 있는 경우, 타입 변수에 담아서 실행문으로 전달한다
* 가져올 항목이 없을 경우, 배열을 빠져나간다

     for(타입 변수 : 배열) {
      실행문;
     }

![image](https://user-images.githubusercontent.com/62369538/149644007-ed651696-91e5-4446-8312-7b2177d0cd98.png)


</br>

## 열거 타입
* 한정된 값만을 갖는 데이터 타입이 열거 타입이다
* 열거타입을 선언하는 벙법은 `public enum 열거타입변수명 {...}`으로 public enum 키워드가 열거 타입을 선언하기 위한 키워드이다

    public enum Week { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY }

* 열거타입 변수는 `열거타입 변수 = 열거타입.열거상수`를 사용하면 된다
* 열거 객체의 메소드를 상용 할 수 있는 이유는 모든 열거 타입은 컴파일 시에 Enum 클래스를 상속하게 되어 있기 때문이다

**name()**
* 열거 객체가 갖고 있는 문자열 리턴

**ordinal()**
* 전체 열거된 객체 중 몇번째 열거 객체인지 알려준다

        Week today = Week.SUNDAY;
        int ordinal = today.ordinal();  // output: 6

**compareTo()**
* 매개 값으로 주어진 열거 객체를 기준으로 전후로 몇 번째 위치하는지 비교
* `enumVar1.compareTo(enumVar2);`로 비교하며 enumVar1과 enumVal2의 순번 차이를 계산하게 되고
* enumVar1이 enumVar2보다 앞에 있는 경우 음수의 결과가
* enumVar1이 enumVar2보다 뒤에 있는 경우 양수의 결과를 얻을 수 있다

**valueOf()**
* 매개 값으로 주어지는 문자열과 동일한 문자열을 가지는 열거 객체를 리턴

**values()**
* 열거 타입의 모든 열거 객체들을 배열로 만들어 리턴

</br>

### Reference
> 이것이 자바다 - 신용권 지음
