# HTML 기초 문법(요소와 태그)

형태 

* (마크) 컨텐츠 (마크)

![1](C:\Users\차주원\Desktop\멋사 강의\3주차 HTML intro ~ 폼태그\1.PNG)

HTML을 통해 컴퓨터를 구조화 함



#### HTML 문서 구조

<!--실행 안되게 일부러   '  '  (따옴표) 넣어 놈-->

* <'DOCTYPE html'>

  문서의 형식을 정의

  HTML 코드는 아님

  HTML 문서에서 가장 처음와야 되고 반드시 있어야함

  

* <'html lang = "kr" >

  본격적인 태그의 시작, 사용하는 주 언어를 정의

  html 문서에서 딱 한번만 쓰여야함

  html 태그 밖에 다른 태그가 존재해서도 안됨

  언어 입력은 접근성과 관련있기 때문에 lang = "kr" 반드시 써줘야함

* head 태그

  위치는 html 바로 아래에 존재

  * meta태그

    문서와 관련된 정보를 담음

    브라우저만 읽을 수 있으며 다양한 정보들을 담고 있음

  * title 태그

    웹 페이지의 제목을 담는 태그

* body 태그

  html에서 실질적으로 보여지는 부분

  마찬가지로 문서 내에 하나만 존재해야함

  html 내부의 head 바로 아래에 위치함

정보) head 태그 body 태그 내부에 있는 태그들은 여러번 쓸 수 있다

#### 레이아웃과 관련된 기본 태그

* 시맨틱(Semantic) 태그

  의미를 가지고 있는 태그

  * header

    웹페이지 혹은 섹션의 소개나 제목을 담기 위해 사용되는 태그

  * nav 

    페이지 이동을 위한 메뉴를 주로 담고 있음

  * section

    기준에 맞게 구간을 나누는 곳

  * article

    주 내용을 담기 위한 태그

  * aside

    주변내용을 담기 위한 공간, 주로 광고

  * footer

    사이트 정보 등의 추가 정보를 담기 위해 사용되는 요소

 ![2](C:\Users\차주원\Desktop\멋사 강의\3주차 HTML intro ~ 폼태그\2.PNG)

배치는 CSS 를 따로 적용해야함



