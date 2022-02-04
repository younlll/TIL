# 중첩 클래스와 중첩 인터페이스
## 중첩 클래스와 중첩 인터페이스란?
* `중첩 클래스(Nested Class)란` 클래스 내부에 선언한 클래스
* 중첩 클래스를 사용하면 두 클래스의 멤버들을 서로 쉽게 접근할 수 있다
* 외부에는 불필요한 관계 클래스를 ㅍ감춤으로써 코드 복잡성을 줄일 수 있다

        class ClassName {
            class NestedClassName {

            }
        }

* 인터페이스도 중첩이 가능하고 이것을 중첩 인터페이스라고 한다

        class ClassName {
            interface NestedInterfaceName {

            }
        }


</br>

## 중첩 클래스
<table style="border-collapse: collapse; width: 80%;" border="1" data-ke-align="alignLeft">
    <tbody>
        <tr>
            <td style="width: 32%;" colspan="2">선언 위치에 따른 분류</td>
            <td style="width: 18%;">선언 위치</td>
            <td style="width: 30%;">설명</td>
        </tr>
        <tr>
            <td style="width: 11.6%;" rowspan="2">멤버 클래스</td>
            <td style="width: 20.4%;">인스턴스 멤버 클래스</td>
            <td style="width: 18%;">class A { </br> &nbsp;&nbsp;&nbsp;&nbsp; class B { ... } </br> }</td>
            <td style="width: 30%;">A 객체를 생성해야만 사용할 수 있으며 A 클래스나 객체가 사용 중이라면 언제든지 재사용 가능하다</td>
        </tr>
        <tr>
            <td style="width: 20.4%;">정적 멤버클래스</td>
            <td style="width: 18%;">class A { </br> &nbsp;&nbsp;&nbsp;&nbsp; static class B { ... } </br> }</td>
            <td style="width: 30%;">A 클래스로 바로 접근할 수 있으며 A 클래스나 객체가 사용중이라면 언제든지 재사용 가능하다</td>
        </tr>
        <tr>
            <td style="width: 32%;" colspan = "2">로컬 클래스</td>
            <td style="width: 18%;">class A { </br> &nbsp;&nbsp;&nbsp;&nbsp; void method() { </br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class B { ... } </br> &nbsp;&nbsp;&nbsp;&nbsp; } </br> }</td>
            <td style="width: 30%;">method()가 실행할 때만 사용할 수 있으며 메소드가 종료되면 B 클래스도 없어진다</td>
        </tr>
    </tbody>
</table>

### 인스턴스 멤버 클래스
* 인스턴스 멤버 클래스는 인스턴스 필드와 메소드만 선언이 가능하고 정적 필드와 메소드는 선언할 수 없다
* 외부에서 인스턴스 멤버 클래스의 객체를 생성하려면 상위 클래스 객체 먼저 생섣을 해야한다

### 정적 멤버 클래스
* 인스턴스 멤버 클래스와 달리 모든 종류의 필드와 메소드를 선언할 수 있다

### 로컬 클래스
* 로컬 클래스는 접근제한자 및 static을 붙일 수 없다(→ 메소드 내부테서만 사용되기 때문이다)
* 로컬 클래스 내부에서는 인스턴스 필드와 메소드만 선언이 가능하다

</br>

## 중첩 클래스의 접근 제한
* 인스턴스 멤버 클래스
  * 바깥에서 인스턴스 필드와 인스턴스 메소드에서만 사용이 가능하다</br>(즉, 정적 필드 초기화와 정적 메소드에서 호출이 불가하다)
  * 바깥의 모든 필드와 메소드에 접근이 가능하다
* 정적 멤버 클래스
  * 모든 바깥 필드와 메소드에서 접근이 가능하다
  * 반면에, 바깥에 선언된 인스턴스 필드와 인스턴스 메소드는 접근할 수 없다</br>(즉, 바깥에 static으로 선언된 필드와 메소드는 접근이 가능하다)


</br></br>
### Reference
> 이것이 자바다 - 신용권 지음