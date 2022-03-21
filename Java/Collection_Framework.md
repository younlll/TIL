# 컬렉션 프레임워크
# 컬렉션 프레임워크

## 컬렉션 프레임워크 소개

- 어플리케이션을 개발하다 보면 다수의 객체를 저장하고 필요할 때 꺼내서 사용해야 하는 경우가 많다
- 이에 쉽게 생각할 수 있는 방법은 배열이 있다
- 하지만 배열은 크기가 생성 시 정해지는 문제가 있고 배열 크기를 크게 설정한다 하는 것도 좋은 해결 방법은 아니다
- 또한, 삭제를 하거나 중간중간 인덱스가 비게 되는 경우, 어디가 비어있는지 확인하는 로직이 필요하다는 문제가 있다
- 이러한 문제점을 해결할 수 있는것이 `컬렉션 프레임워크`이다
- 컬렉션 프레임워크 주요 인터페이스로는 List, Set, Map이 있다
    
    
<img src="image/commec">
    

- List
    - 순서를 유지하고 저장
    - 중복 저장 가능
    - ArrayList, Vector, LinkedList
- Set
    - 순서를 유지하지 않고 저장
    - 중복 저장 안됨
    - HashSet, TreeSet
- Map
    - 키와 값의 쌍으로 저장
    - 키는 중복 저장 안됨
    - HashMap, Hashtable, TreeMap, Properties

## List 컬렉션

![collectino_02.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cc2d1b68-273c-4adb-a892-be119926368d/collectino_02.png)

- 객체 추가
    - boolean add(E e) : 객체를 맨 끝에 추가
    - void add(int index, E element) : 인덱스에 객체를 추가
    - E set(int index, E element) : 인덱스에 저장된 객체를 주어진 객체로 바꿈
- 객체 검색
    - boolean contains(Object o) : 객체가 저장되어 있는지 여부
    - E get(int index) : 주어진 인덱스에 저장된 객체를 리턴
    - boolean isEmpty() : 컬렉션이 비어 있는지 조사
    - int size() : 저장되어 있는 전체 객체 수를 리턴
- 객체 삭제
    - void clear() : 저장된 모든 객체를 삭제
    - E remove(int index) : 인덱스에 저장된 객체를 삭제
    - boolean remove(Object o) : 주어진 객체를 삭제

### ArrayList

- List인터페이스의 구현 클래스
- 저장 용량(capacity)을 초과한 객체들이 들어오면 자동적으로 저장 용량(capacity)이 늘어난다
- 객체가 저장될 때 Object로 변환되어 저장되므로 모든 종류의 객체가 저장이 가능하다
- 객치를 반환할 때는 원래 타입으로 변환해야 하므로 실제 성능에 좋지 못한 영향을 미친다
    - 객체를 찾아올 때 자바 5를 기준으로 차이가 있다
        
        ```java
        // 자바 4
        List list = new ArrayList();
        list.add("홍길동");
        Object obj = list.get(0);    // 컬렉션에서 객체를 검색
        String name = (String) obj;  // 타입 변환 후 홍길동을 얻을 수 있음
        
        // 자바 5
        List<String> list = new ArrayList<String>();
        list.add("홍길동");
        String name = list.add(0);    // 컬렉션에서 객체 검색 이후 홍길동을 바로 얻을 수 잇음
        ```
        
- 특정 인덱스의 객체를 제거하면 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 당겨진다
- 특정 인덱스에 객체를 삽입하면 해당 인덱스부터 마지막 인덱스까지 모두 1씩 밀려난다

### Vector

- Vector는 ArrayList와 동일한 내부 구조를 가지고 있다
- 동기화된 메소드로 구성되어 있기 때문에 멀티 쓰레드 환경에서 안전하게 객체를 추가, 삭제 할 수 있다

### LinkedList

- ArrayList와 사용법은 같지만 구조가 다르다
- ArrayList는 인덱스로 관리되지만 LinkedList는 인접 참조를 링크로 연결하여 관리한다
    
    ![collectino_03.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70f838da-62c7-4216-ab99-2b5d8d52c94d/collectino_03.png)
    

### ArrayList vs LinkedList

| 구분 | 순차적으로 추가/삭제 | 중간에 추가/삭제 | 검색 |
| --- | --- | --- | --- |
| ArrayList | 빠르다 | 느리다 | 빠르다 |
| LinkedList | 느리다 | 빠르다 | 느리다 |

## Set 컬렉션

- 마치 수학의 집합처럼 순서는 보장이 되지 않으며 중복은 허용되지 않는다
- 객체 추가
    - boolean add(E e) : 객체 저장
- 객체 검색
    - boolean contains(Object o) : 객체가 저장되어 있는지에 대한 여부
    - boolean isEmpty() : 컬렉션이 비어있는지 확인
    - Iterator<E> interator() : 저장된 객체를 한 번씩 가져오는 반복자 리턴
        - hasNext() : 가져올 객체가 있으면 true, 없으면 false를 반환
        - next() : 컬렉션에서 하나의 객체를 가져온다
        - remove() : Set 컬렉션에서 객체를 제거
    - int size() : 저장되어 있는 전체 객체 수 리턴
- 객체 삭제
    - void clear() : 저장된 모든 객체 삭제
    - boolean remove(Object o) : 주어진 객체 삭제

### HashSet

```java
Set<E> set = new HashSet<E>();
```

- 저장 프로세스
    
    ![collectino_04.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9da3001b-e12b-4889-a511-384949d98e4f/collectino_04.png)
    

## Map 컬렉션

- key와 value로 구성된 Entry 객체를 저장하는 구조
    
    ![collectino_05.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f3814c29-7fb7-450c-9841-3fb3bb5246ff/collectino_05.png)
    

- 객체 추가
    - V put(K key, V value) : 주어진 키로 값을 저장
- 객체 검색
    - boolean containsKey(Object key) : 주어진 키가 있는지 여부
    - boolean containsValue(Object value) : 주어진 값이 있는지 여부
    - Set<Map.Entry<K,V>> entrySet() : 키와 값의 쌍으로 구성된 모든 Map.Entry 객체를 Set에 담아서 리턴
    - V get(Object key) 주어진 키가 있는 값을 리턴
    - boolean isEmpty() 컬렉션이 비어 있는지 여부
    - Set<K> keySet() : 모든 키를 Set 객체에 담아서 리턴
    - int size() : 저장된 키의 총 수를 리턴
    - Collection<V> values() : 저장된 모든 값을 Collection에 담아서 리턴
- 객체 삭제
    - void clear() : 모든 Map.Entry(카와 값)를 삭제
    - V remove(Object key) : 주어진 키와 일치하는 Map.Entry를 삭제하고 값을 리턴

### HashMap

- HaspMap의 키로 사용할 객체는 hashCode()와 equals() 메소드를 재정의해서 동등 객체가 될 조건을 정해야 한다
    
    ```java
    Map<K, V> map = new HashMap<String, Integer>();
    Map<String, Integer> map = new HashMap<String, Integer>();
    ```
    

### Hashtable

- 동기화된 메소드로 구성되어 있기 때문에 멀티 스레드가 동시에 메소드를 실행할 수  없고, 하나의 스레드가 실행을 완료해야만 다른 스레드를 실행할 수 있다
    
    ```java
    Map<K, V> map = new Hashtable<String, Integer>();
    Map<String, Integer> map = new Hashtable<String, Integer>();
    ```
    

### Properties

- Properties는 Hashtable의 하위 클래스이기 때문에 Hashtable의 모든 특징을 그대로 가지고 있다
- 키 값이 String으로 제한되어 있다