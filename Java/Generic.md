# 제네릭
## 제네릭을 사용하는 이유
* Java 5부터 제네릭이 지원이 되었으며 제네릭을 통해 잘못된 타입이 사용될 수 있는 문제를 컴파일 과정에서 제거할 수 있게 되었다

**제네릭의 장점**
* 컴파일 시 강한 타입 체크를 할 수 있다
* 타입 변환을 제거한다

```java
// Case 비제네릭
List list = new ArrayList();
list.add("hello");
String str = (String)list.get(0);   // 타입 변환을 반드시 해야한다


// Case 제네릭
List<String> list = new ArrayList<String>();
list.add("hello");
String str = list.get(0);
```
* 위에 예제처럼 제네릭으로 String을 지정하는 경우, List의 데이터 타입이 String으로 제한되기 때문에 별도의 타입 변환 작업을 거치지 않아도 된다

</br>

## 제네릭 타입
* 제네릭 타입은 클래스 또는 인터페이스 이름 뒤에 `<>` 부호가 붙고, 사이에 타입 파라미터가 위치한다
* 타입 파라미터는 변수명과 동일한 규칙에 따라 작성할 수 있지만, 일반적으로 대문자 알파벳 한 글자로 표현한다
* 제네릭 타입을 실제 코드에서 사용하려면 타입 파라미터에 구체적인 타입을 지정해야한다

        public class 클래스명<T> { ... }
        public interface 인터페이스명<T> { ... }

### 제네릭을 사용하는 이유에 대해 예시를 통해 자세히 알아보자
```java
public class Box {
    private Object object;
    public void set(Object object) { this.object = object; }
    public Object get() { return object; }
}
```

* Box클래스의 필드 타입이 Object인데, Object 타입으로 선언한 이유는 필드에 모든 종류의 객체를 저장하고 싶어서이다
* Object 클래스는 모든 자바 클래스의 최상위 부모 클래스이다
* 따라서 자식 객체는 부모 타입에 대입할 수 있다는 성질 때문에 모든 자바 객체는 Object 타입으로 자동 타입 변환되어 저장된다
* 위 예시에서 set() 메소드를 보면 Object 타입으로 매개값을 받아 모든 객체를 받을 수 있게 했고, 받은 매개값을 Object 필드에 저장시킨다
* get() 메소드는 Object타입으로 리턴한다
* 따라서 **get() 메소드를 호출하여 필드에 저장된 원래 타입의 객체를 얻으려면 강제 타입 변환을 해야한다**
* Object 타입을 사용하면 모든 종류의 자바 객체를 저장할 수 있다는 장점은 있지만
* 저장할 때 타입 변환이 발생하고, 읽어올 때에도 타입 변환이 발생한다
* 타입 변환이 빈번해지면 전체 프로그램 성능에 좋지 못한 결과를 가져올 수 있다
* 이런 타입변환의 문제를 해결하기 위해 `제네릭`을 사용하는 것이다
* 아래에 제네릭을 이용하여 Box 클래스를 수정해 보자

```java
public class Box<T> {
    private T t;
    public void set(T t) { this.t = t; }
    public T get() { return t; }
}
```
* 이제 Box 클래스를 사용해보자

```java
Box<String> box1 = new Box<String>();
Box<Integer> box2 = new Box<Integer>();
```
> Box<String> box = new Box<>(); 와 같이 new연산자 뒤에 붙는 제네릭에서는 Java 7부터 타입 생략이 가능하다</br>
> 컴파일러가 참조타입의 제네릭을 보고 유추할 수가 있기때문에 생략이 가능해졌다

* 타입 파리미터 T는 String과 Integer로 대체되어 아래처럼 Box 클래스의 내부를 자동으로 재구성한다

```java
// Box<String> box1 = new Box<String>();
public class Box<String> {
    private String t;
    public void set(String t) { this.t = t; }
    public String get() { return t; }
}

// Box<Integer> box2 = new Box<Integer>();
public class Box<Integer> {
    private Integer t;
    public void set(Integer t) { this.t = t; }
    public Integer get() { return t; }
}
```

</br>

## 멀티 타입 파라미터
* 제네릭 타입은 두 개 이상의 멀티 타입 파라미터를 사용할 수 있는데, 이 경우 각 타입 파라미터를 콤마로 구분한다

```java
public class Product<T, M> {
    private T kind;
    private M model;

    public T getKind() { return this.kind; }
    public M getModel() { return this.model; }

    public void setKind(T kind) { this.kind = kind; }
    public void setModel(M model) { this.model = model; }
}
```

```java
public class ProductExample {
    public static void main(String[] args){
        Product<Tv, String> product1 = new Product<Tv, String>();
        product1.setKind(new Tv());
        product1.setModel("스마트Tv");
        Tv tv = product1.getKind();
        String tvModel = product1.getModel();

        Product<Car, String> product2 = new Product<Car, String>();
        product2.setKind(new Car());
        product2.setModel("디젤");
        Car car = product2.getKind();
        String carModel = product2.getModel();
    }
}
```
* 위 예제 역시 Java 7부터는 `Product<Tv, String> product1 = new Product<>();`와 같이 생략이 가능하다

</br>

## 제네릭 메소드
* `제네릭 메소드`란? 매개 타입과 리턴 타입으로 타입 파라미터를 갖는 메소드르 ㄹ말한다
        public <타입 파라미터, ...> 리턴타입 메소드명(매개변수, ...) { ... }
* 제네릭 메소드를 호출할 때는

        - 구체적인 타입 명시
            리턴타입 변수 = <구체적타입> 메소드명(매개값);
        - 매개값을 보고 컴파일러가 구체적인 타입을 추정
            리턴타입 변수 = 메소드명(매개값);

```java
public class Util {
    public static <T> Box<T> boxing(T t) {
        Box<T> box = new Box<T>();
        box.set(t);
        return box;
    }
}
```

```java
public class BoxingMethodExample {
    public static void main(String[] args) {
        Box<Integer> box1 = Util.<Integer>boxing(100);
        int intValue = box1.get();

        Box<String> box2 = Util.boxing("홍길동");
        String strValue = box2.get();
    }
}
```

* 이해한 내용을 글로 풀어서 적어보자면
  * \<T> 를 통해 리턴타입과 매개변수 타입이 T 라는 정보를 알 수 있다
  * Box\<Integer> box1 → 리턴타입은 Box\<Integer>이고
  * \<Integer>boxing(100) → 매개변수 타입은 Integer라는 것을 알 수 있다
  * Util.boxing("홍길동")을 보면 위와같이 매개변수 타입이 없는데 이것은 컴파일러가 "홍길동"을 보고 타입을 추정하여 수행된다

```java
public class Util {
    public static <K, V> boolean compare(Pair<K, V> p1, Pair<K, V> p2) {
        boolean keyCompare = p1.getKey().equals(p2.getKey());
        boolean valueCompare = p1.getValue().equals(p2.getValue());
        return keyCompare && valueCompare;
    }
}
```

</br>

## 제한된 타입 파라미터
* 제한된 타입 파라미터만 선언 되어야하는 이유
  * 숫자만 연산하는 제네릭 메소드는 매개값으로 Number 타입 또는 하위 클래스 타입의 인스턴스만 가져야 한다

```java
public <T extends Number> int compare<T t1, T t2> {
    double v1 = t1.doubleValue();
    double v2 = t2.doubleValue();
    return Double.compare(v1, v2);
}
```

</br>

## 와일드 타입
* `?`을 와일드카드라고 부른다
  * 제네릭타입<?>: 모든 클래스나 인터페이스 타입이 올 수 있다
  * 제네릭타입<? extends 상위타입>: 상위 타입이나 하위 타입만 올 수 있다
  * 제네릭타입<? supter 하위타입>: 하위타입이나 상위 타입이 올 수 있다

```java
public class Cource<T> {
    private String name;
    private T[] students;

    public Cource(String name, int capacity) {
        this.name = name;
        students = (T[]) (new Object(capacity));
    }

    public String getName() { return name; }
    public T[] getStudents() { return students; }
    public void add(T t) {
        for(int i = 0; i < students.length; i++) {
            if(students[i] == null) {
                students[i] = t;
                break;
            }
        }
    }
}
```

* Person 하위 클래스로 Worker와 Student가 있고, Student 하위 클래스로 HighStudent가 있다고 가정해보자
  * Course<?> : 수강생은 모든 타입이 될 수 있다
  * Course<? extends Student> : 수강생은 Student와 HighStudent만 될 수 있다
  * Course<? super Worker> : 수강생은 Worker와 Person만 될 수 있다

</br>

## 제네릭 타입의 상속과 구현
        pubilc class ChildProduct<T, M> extends Product<T, M> { ... }
        public class ChildProduct<T, M, C> extends Product<T, M> { ... }

* 자식 제네릭 타입은 추가적으로 타입 파라미터를 가질 수 있다

</br></br>

### Reference
> 이것이 자바다 - 신용권 지음
  