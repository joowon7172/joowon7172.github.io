# 웹 기초

### HTML

* HTML (Hyper Text Markup Language)

* Hyper Text = Link

* 프로그래밍 언어가 아님 

* HTML 작성할 때는  대원칙 : HTML로 꾸미려 들지 말자!  

  HTML은 애초에 '꾸미는 언어' 가 아님

* Terminal : 명령을 내리는 공간

* 클라이언트와 서버는 URL로서 대화를 한다, 통신을 주고 받는다.





> !DOCTYPE html <!--<!DOCTYPE html>랑 <html>은-->

> html lang="ko" <!--'이거 HTML로 작성된 문서야' 를 알려주는 태그-->

> > head<!--head *<!--태그는 직접 문서에 들어나지는 않지만 이 문서를 설명해주는 아주 중요한 내용을 담음-->                          					       

> > > meta charset="utf=8" <!--인코딩 방식을 utf-8로 한다-->
> > >
> > > <title>나를 소개해요</title>

> > </head>

> > <body> <!--화면에 직접적으로 등장하는 태그들 입력-->

> > > (<h1>차주원 입니다</h1>) <!--중요도 순서에 따른 제목-->

> > > (<h2>안녕하세요</h2>)



> > > (<form action = "전송받을 대상">) <!--form 태그 : 사용자로부터 입력값을 받을 수 있음-->

> > > > 아이디: <input type ="text" name = "id">

> > > > 비밀번호 : <input type = "password" name = "pw">

> > > > <input type = "submit">

> > > </form>

> > >  <br> <!--줄 바꿈-->

> > >    <img src = "shit.png" height = 500> <!-- 이미지파일을 불러오려면 HTML 파일과 같은 폴더에 있어야 함-->

> > > <br>

> > > <form action = "전송받을 대상">

> > > > (<h2>나의 일기장</h2>)

> > > > 제목 : <input type = "text" name = "diarytitle"> <br>

> > > > (<select>) <!--이 안에다가 여러가지 선택할수 있는 항목들을 만드는곳 --> 

> > > > > <option value = "goodday">좋은날</option> <!--위에있는 name 과 비슷, 서버들이 알아듣는말, 좋은날 슬픈날 그저그런날은 우리가 보기위해 작성한 말-->

> > > > > <option value = "sadday">슬픈날</option>

> > > > > <option value = "sosoday">그저그런날</option>

> > > > </select> <br>

> > > > 내용 : <br>

> > > > (<textarea cols = "30" rows = "20"></textarea>)

> > > > <br><input type = "submit">

> > > </form><br>

> > >  (<h2>나의 일대기</h2>)

> > > (<ol>)<!--순서가 있는 리스트 ordered list 줄임-->

> > > > (<li><a href = "1.html">유년기</a></li>) <!-- a herf => 링크 걸게 해줌--><!-- 링크를 걸 html은 작성중인 index.html 파일과 같은 폴더에 있어야함-->

> > > > (<li><a href = "2.html">질풍노도의 시기</a></li>)

> > > > <li>방황기</li>

> > > > <li>지금</li>

> > > </ol>
> > >
> > > <!-- 위 리스트 일일이 치기 귀찮고 번거로우니까 쓰는 단축키 => ol>li*3 후 tab 누르기 => *은 곱하기를 의미, 숫자는 자식 노드 수-->



> > </body>

> </html>

 