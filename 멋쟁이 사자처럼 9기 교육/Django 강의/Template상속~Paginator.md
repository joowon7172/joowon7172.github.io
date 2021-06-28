# Template 상속

* 중복되는 코드를 base.html에 만들어 놓고 이 html 파일을 다른 html 파일에 상속시켜 쓸 수 있는 것

```
base.html 에
<div class="container">
	{% block content %}
	{% endblock %} 입력

위의 코드를 적용할 다른 html 파일에 아래와 같이 기입
{% extends 'base.html' %}
{% block content %}
사이의 내용(적용시킬 코드)
{% endblock %}

그 다음 settings.py파일 Template에 
'DIRS' : ['base.html파일 경로'] 적어주기
```

urls.py 관리

-> 복잡하니 강의 보고 실습



# Static

* 장고에서 다루는 파일

* **정적 파일** : 미리 서버에 저장되어 있는 파일, 서버에 저장된 그대로를 서비스해주는 파일

* **동적 파일** : 서버의 데이터들이 어느정도 가공된다음 보여지는 파일 (상황에 따라 달라질 수 있음)



##### 정적파일

* **static** : 개발자가 서버를 개발할 때 미리 넣어놓은 정적파일(img, js, css)

* **media** : 사용자가 업로드 할 수 있는 파일

* **static_dirs** : 현재 static파일들이 어디에 있는지 알려주는 명령어

* **static_root** : static 파일을 어디에 모을건지 알려주는 명령어

# media

* **static** : 사용자가 사진을 요청 -> 서버는 이미 가지고 있음 -> 사용자에게 보여줌

* **media** : 사용자가 서버에 사진을 올림 -> 서버는 사진을 저장해놓놓음 -> 사용자가 서버에 사진을 요청 -> 저장한 사진 꺼냄 -> 보여줌

두가지 모두 사진 원본이 아니라 url을 보내주는 형식임

* **MEDIA_ROOT** : 이용자가 업로드한 파일을 모으는 곳

* **MEDIA_URL** : 미디어 파일에 url설정하는 것

* **upload_to** : settings.py에 업로드할 폴더를 지정하는 것 MEDIA_URL로 지정해둔 media폴더안에 blog 폴더를 만들어서 관리하겠다는 설정

새로운 테스트 데이터들을 넣기 전에 기존에 있던 데이터들를 삭제해야 오류가 안뜸

blog -> migrations -> initial삭제

blog -> migrations -> pycache -> initial 삭제

blog전 폴더(프로젝트 폴더) -> db.sqlite3삭제

실습 과정 다시 보기



# FORM

내가 생각하는 그 form 맞음 , **입력 공간**을 뜻함

**forms.py의 장점**:  forms.py를 이용하면 데이터베이스의 모델이 변할 때마다 바꾸는 작업을 하지 않아도 됨. 유효성 검사를 더 편하게 사용할 수 있다

**실습 영상 다시 보기**

# User 확장과 인증

**CRUD만큼 중요함.** 

**이걸 잘해야 웹서비스 다운 웹서비스 만들수 있음**

* 장고에서 제공해주는 user 

* user을 대체할 테이블을 만들자!

  우리가 설정한 유저보다 더 많은 컬럼이 필요한 경우가 있는데 그 경우에 사용

* 장고에서 제공해주는 auth(authentication: 인증) 

  ex) 회원가입(회원정보) 요청 -> 서버의 user테이블에 데이터 저장 -> 회원정보를가지고 로그인 요청 -> user테이블에 정보가 있는 지 확인(authentication) -> ~~사용자에게 token 발급해줌 -> 서버에 요청(token)보냄 -> 해당user에 대한 응답~~ 

* 장고에서는 token 사용 X

  처리해주는 모듈이 있음

  * authenticate, login, logout 함수 

**실습 영상 다시 보기**

# Paginator

블로그 객체를 잘라서 보내주는 기능을 함

글을 쪼개서 보내는 기능을 함

```
http://127.0.0.1:8000/?page=1 
```

->1번째 페이지를 보고 싶다

**실습 영상 다시 보기**