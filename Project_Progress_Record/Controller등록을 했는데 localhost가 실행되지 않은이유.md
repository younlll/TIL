# Controller를 등록해줬지만 localhost:8080 입력시 Whitelabel Error Page가 뜬 경우

<img src="https://user-images.githubusercontent.com/62369538/156370362-fad1a644-f8d6-4d9c-9926-56a99ad27c85.png" width="750" />
<img src="https://user-images.githubusercontent.com/62369538/156371527-13469048-7248-489c-87dc-77dfd19abd92.png" width="550" />

* 첨부된 이미지를 참고해서 보면 스프링부트가 정상적으로 실행되었고 내장된 톰캣 서버가 8080포트로 정상적으로 실행된 것을 볼 수 있다
* 아무 웹페이지도 없이 **실행만 테스트한 경우라면 Whitelabel Error Page가 나오는 것은 정상** 이지만
* Controller를 통해서 localhost:8080 페이지를 만들어 줬기 때문에 현재 보이는 Whitelabel Error Page가 오류로 발생한 것임을 알수 있다

<br>

## 발생 원인
* Controller를 컴포넌트 스캔이 이루어지는 패키지 하위에 만들지 않고 바깥에 생성함 _(바보같은 실수...)_

_(인프런 스프링 -김영한님 강의로 알고 있었는데 이상한 위치에 Controller 클래스를 선언해서 발생했다...)_

<br>

### 정리할 내용
* 메인 클래스는 project.develpmentcomunity 하위에 있으며 메인 클래스를 열어서 보면 `@SpringBootApplication`이 붙어 있다
* @SpringBootApplication을 따라가보면 `@ComponentScan`이 나오고  `@Filter`를 통해 반복하여 컴포넌트들을 스캔하고 스프링에 등록한다는 것을 알수 있다
* 만들어준 loginPageController 클래스를 들어가서 보면 `@Controller만 있고 스캔 대상이 @Component 어노테이션이 없다`고 보일 수 있지만
* @Controller를 들어가서 보면
* `@Component` 어노테이션이 있는 것을 알 수 있다

<img src="https://user-images.githubusercontent.com/62369538/156373889-7aaa0905-01dd-4bd4-82df-ec67b1530844.png" width="773"/>
<img src="https://user-images.githubusercontent.com/62369538/156374021-14f8eda2-ca17-43ee-9edc-9855798fab78.png" />


<br>
## 해결
* DevelopmentComunityApplication 클래스에 있는 패키지 하위로 loginPageController 클래스 위치를 이동시킴으로 해결
