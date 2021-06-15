# MTV패턴

**Model Template View**



#### Template

* 사용자가 보이는 영역

  * HTML

  * CSS

  * 템플릿 언어

    

#### Model

* DataBase가 저장되는 곳

  

#### View

* 데이터를 처리하는 곳
* MTV중 핵심



![MTV가 어디쪽인지](C:\Users\차주원\Desktop\멋사 강의\Django 강의\교육 마크다운 필기\MTV가 어디쪽인지.PNG)



# Django 실습



**APP**

* Django 프로젝트를 이루는 작은 단위

* 각각의 서비스별로 분류를 해놓은 것

  ex) 검색 전용 , 메일 전용



**그냥 앱을 만들어주기만 해서는 프로젝트가 방금만든 앱이 자신의 앱인지 인식을 못함**

**--> project 설정 폴더에 있는 setting.py 에 들어가서 자신의 앱이라는 것을 등록해 준다**

​	  **--> INSTALLED APPS에 자신이 추가한 앱 이름을 적어줘야함**



**웹사이트 구동 순서**

1. 사용사가 서버에 요청
2. 서버의 view는 model에게 요청에 필요한 데이터를 받음
3. view는 받은 데이터를 적절하게 처리해서 template으로 넘김
4. template은 받은 정보를 사용자에게 보여줌



#### 앱 제작 순서

1. App을 생성

2. template 만들기

   

3. 데이터를 처리할 view 만들기

   * views.py에서 해줌

   

4. URL과 View 함수 연결

   * 프로젝트 설정폴더에서 해줌

   * URL 등록하는 방법 : urls.py에서

   * views.py를 urls.py에서 쓸 수 있게 import 하는 코드

* ```
  from firstapp import views
  ```



# Django와 데이터베이스



* **ORM** : SQL로 데이터베이스에 명령을 내리지 않아도 파이썬의 객체지향적인 방법으로 데이터베이스에 데이터를 생성, 삭제, 수정 할 수 있음. 

  오로지 파이썬 만으로 웹 어플리케이션을 만들 수 있다.



 * 데이터 베이스 :

   이렇게 생김

![데이터 베이스](C:\Users\차주원\Desktop\멋사 강의\Django 강의\교육 마크다운 필기\데이터 베이스.PNG)

![image-20210615190645796](C:\Users\차주원\AppData\Roaming\Typora\typora-user-images\image-20210615190645796.png)



# Model 실습

* 필요한 필드를 그때 그때 찾아 쓰기

  ![필드](C:\Users\차주원\Desktop\멋사 강의\Django 강의\필드.PNG)



* 필드 옵션 -> 이것도 많기 때문에 필요한거 검색해서 찾아쓰기



# CRUD

본격적으로 블로그를 만드는 단계

데이터베이스의 정보를 CRUD하는 것



* **Read (읽다)**

Path-converter : 영상을 참고하자

primary Key : 데이터베이스에서 데이터들을 식별하기 위한 ID값 (ID = PK)



* **Create (생성하다)**

```
[사용함수]

new : new.html 보여줌

create : 데이터베이스에 저장
```

http요청방식 : Get과 Post

-> Get : 데이터를 얻기 위한 요청

 데이터가 url에 보임

-> Post : 데이터를 생성하기 위한 요청

 데이터가 url에 안보임

 Csrf 공격 방지 -> 사이트 간 요청 위조 / 서버가 공격자에 의해 수정, 삭제를 하는 것



* **Update (수정하다)**  
  * 수정할 데이터의 id값을 받아야함

```
[사용함수]

edit : edit.html보여줌

update : 데이터베이스에 적용
```



* **Delete (삭제하다)**

html은 따로 안만들어도 됨

