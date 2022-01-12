Git의 기초를 연습한 사이트

[https://www.codecademy.com/learn](https://www.codecademy.com/learn)
이 사이트에서 git을 검색한 후 무료버전으로 연습을 했다.

이 사이트에서 설명하기를

> Git is a software that allows you to keep track of changes made to a project over time.

Git은 프로젝트의 변경사항을 기록하고 그 변경사항들을 추적할수 있는 소프트웨어라는 것이다.

#### git init

-   itit은 초기화를 뜻한다
-   git이 프로젝트 변경 사항을 추적하기 시작하는데 필요한 모든 도구를 설정한다

[##_Image|kage@bgazDS/btrp6xfTzUr/0JJyK5i7Hh9XEOIuO42iK0/img.png|CDM|1.3|{"originWidth":1419,"originHeight":431,"style":"alignCenter","width":666,"height":202,"caption":"git init 실습"}_##]

Git은 기본적으로 3단계를 갖는다

-   Directory: 작업이 수행되는 곳
-   Staging Area: 변경사항들이 있는 곳
-   Repository: 변경사항을 저장하는 곳

#### git status

-   status(상태)라는 단어 뜻 그대로 git의 상태를 확인 할 수 있다

#### git add

-   `git add filename`을 통해서 staging area에 명시한 파일을 추가할 수 있다

#### git diff

-   `git diff filename`을 통해서 변경된 내용을 확인 해볼수 있다

#### git commit

-   git commit은 마지막 단계이다
-   commit은 repository 내에 staging area의 변경 내용을 영구적으로 저장한다
-   commit 명령어 뒤에는 -m 이라니 옵션이 붙는다
-   commit message의 기본 규칙
    -   쌍따옴표로 묶어서 적는다
    -   현재 시제로 적는다
    -   50자 이내로 간략하게 적는다

#### git log

-   git log를 통해서 repository에 시간순대로 저장된 변경이력을 볼 수 있다
    -   40자로 된 SHA라고 불리는 식별 코드
    -   commit 작성자
    -   commit을 한 일자와 시간
    -   commit 메시지
-   이렇게 4가지의 정보를 볼 수 있다
