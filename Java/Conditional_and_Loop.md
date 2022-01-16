# 조건문과 반복문
## 조건문
### if문
* `if` 조건문은 조건식의 값이 true이면 조건문 내의 내용을 실행시키고 다르다면 내부에 있는 실행문을 수행하지 않고 지나간다
* `if-else`조건문은 if의 조건식의 결과가 true라면 if 내부의 코드를 실행하고 else 내부는 수행하지 않는다
* 반대로 if의 조건식의 결과가 false라면 if문은 지나치고  else에 있는 코드를 수행한다
* `if-else if-else`조건문은 if와 else if로 이루어진 조건식들을 위에서부터 순차적으로 검사를 한다
* 검사도중 조건식이 true인 최초의 경우의 코드를 실행한다
* 만약 모든 조건식을 검사할때까지 true인 조건식이 없다면 else문의 코드를 실행시킨다
* `중첩 if문`은 말그대로 if문이 중첩된 경우를 말하며 중첩된 if문 또한 위에 설명된 if문과 동일하게 처리된다

![image](https://user-images.githubusercontent.com/62369538/149642737-f205a23d-b558-4030-8d3c-1bcef4420759.png)

* 위 예제를 보면 score 변수에 97이라는 값이 들어가 있고
* **if문에서 score == 100라는 조건식에 false를 산출**받기 때문에 **if문의 중괄호 안에 있는 내용은 실행되지 않는다**
* else if문으로 넘어와 **score >= 90 조건식에서 true를 리턴**받기 때문에 **else if문의 중괄호 안의 식을 실행**한다
* 만약, **if문과 모든 else if문에서 false를 리턴받았다면 else문을 실행**하게 된다

### switch문
* `switch`조건문은 switch(변수)에 있는 변수의 값을 순차적으로 case문에 있는 값과 같은지 비교하며 수행한다
* 같은 값이 있는 case문에 대해서만 코드를 수행시킨다
* default를 통해 모든 case문의 값과 같지 않은 경우에 대해 수행할 코드를 작성할 수 있다

</br>

## 반복문
### for문
    for(초기화식; 조건식; 증감식) {
      수행할 코드 작성;
    }

```java
// Ex1.
int sum = 0;
for(int i = 1; i <= 100; i++) {
    sum = sum + i;
}
System.out.pirntln("1~100까지의 합: " + sum);
/*************************
 * output:               *
 * 1~100까지의 합: 5050   *
 *************************/
```

* 초기화식을 통해 초기화된 변수의 값이 증감식을 통해 조건식을 만족할때까지 반복하여 코드를 수행한다
* 식이 2개 이상이 있을수도 있다
  * `for(int i = 0, j = 100; i <= 50 && j >= 50; i++, j--) { ... }`

### while문
    while(조건식) {
      수행할 코드 작성;
    }

```java
Ex2.
public class WhilePrimetExample {
  public static void main(String[] args) {
    int i = 1;
    while(i <= 10) {
      System.out.print(i + " ");
      i++;
    }
  }
}

/************************
 * output:              *
 * 1 2 3 4 5 6 7 8 9 10 *
 ************************/
```

* 조건식의 결과값이 true일때까지 반복하여 코드를 수행한다
* 처음부터 조건식의 결과값이 false라면 코든는 while문의 내부 코드는 한번도 수행되지 않는다

![image](https://user-images.githubusercontent.com/62369538/149643086-03e154f2-9448-4ca8-a86a-3a06feb9f7b7.png)


### do-while문
    do {
      수행할 코드 작성;
    } while(조건식)

* 조건식의 결과값이 true일때까지 반복하여 코드를 수행한다
* while문과 달리 먼저 코드를 수행하고 다음 반복을 수행할지를 조건식을 통해 확인한다

### break문
* break문은 반복문을 중지시킬 때 사용된다
* break문은 가장 가까운 반복문만 중지시키므로 중첩된 경우, 바깥쪽 반복문은 중지되지 않는다
* 바깥쪽 반복문까지 종료7시키려면 바깥쪽 반복문의 이름을 붙이고 `break 이름;`을 사용하면 된다

```java
// Reference : 이것이 자바다 - 신용권 지음
Outter:for(char upper = 'A'; upper <= 'Z'; upper++) {
  for(char lower = 'a'; lower <= 'z'; lower++) {
    if(lower == 'g') {
      break Outter;
    }
  }
}
```

### continue문
* 반복문에서만 사용되며 블록 내부에서 continue문이 실행되면 continue문 이후의 코드는 수행되지 않고 반복문의 조건식으로 이동하여 다시 코드가 실행된다

</br></br>

### Reference
> 이것이 자바다 - 신용권 지음
