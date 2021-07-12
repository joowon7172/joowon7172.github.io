# 배포 사전 준비

### **환경변수**란?

시스템에 저장되어있는 변수

보통 비밀키 등 유출되면 안되는 정보

또는 환경에 차이를 둘 때 사용(테스트/프로덕션 구별 등)

os.environ 에서 dict 형식으로 불러올 수 있음

os.environ.get('변수명','기본값')으로 사용

### requirements?

내 파이썬(장고) 앱을 실행하기 위해 우선 설치되어야 하는 패키지들

Django,Pillow, 등

패키지명== 버전으로 저장

보통 requirements.txt 파일에 저장

pip freeze 명령어는 해당 환경에 설치된 모든 패키지를 보여줌

>(꺽쇠)  는 프로그램의 출력을 파일에 저장한다는 뜻

pip freeze > requirements.txt 로 생성

### IAM?

Identity and Access Management의 줄인말

IAM에서 계정을 만든 후 해당 계정 로그인 정보(엑세스키 & 시크릿 키)를 이용하여 AWS의 API활용

보안을 위해 권한을 최대한 보수적으로 잡음

### S3

Simple Storage Service의 줄인말

AWS에서 제공하는 구글드라이브 정도로 생각할 수 있음

최소 용량 지정 없이 사용한 만큼만 과금되므로 용량 예측 필요 X

여러 서버에서 동시에 접속 가능(부하 분산 유리)

# heroku 배포하기

- heroku 회원가입

- heroku CLI 설치

- 환경 변수 적용

  - DEBUG = (os.environ.get('DEBUG', 'True') != 'False')

- .gitignore파일 적용

  - gitignore.io 에서 Django 선택 후 '생성'
  - 페이지에 나온 텍스트 복사 후 .gitignore 파일로 저장

- heroku 용 파일 작성

  - Procfile 이라는 파일을 만들어 아래 내용 작성
    - web : gunicorn 프로젝트명.wsgi --log-file-
  - runtime.txt 파일에 아래 내용 작성
    - python-3.9.1

- 필요한 Dependency 설치

  - pip install gunicorn whitenoise dj-database-url psycopg2-binary

- settings.py 수정

  - Whitenoise 설치
    - MIDDLEWARE 에서 제일 SecurityMiddleware 바로 아래 내용 추가
      - 'whitenoise.middleware.WhiteNoiseMiddleware',
  - ALLOWED_HOSTS 수정
    - ALLOWED_HOSTS = [] 를 ALLOWED_HOSTS = [' * ']로 수정
  - DB 관련 코드 수정
    - settings.py 제일 밑에 아래 내용 추가

  ```
  import dj_database_url
  db_from_env = dj_database_url.config(conn_max_age=500)
  DATABASES['default'].update(db_from_env)
  ```

# Ubuntu 배포

1. EC2 인스턴트 만들기

   1. https://console.aws.amazon.com/
   2. 우측 상단 지역이 Seoul인지 확인
   3. EC2 검색
   4. Instances > Launch Instatnces
   5. Ubuntu Server 20.04 LTS (64-bit x86)
   6. t2.micro (Free tier eligible)
   7. Storage 설정 (Free Tier은 30GB까지)
   8. Security Group > Add Rule
      1. HTTP
      2. HTTPS
      3. Custom -> TCP -> 8000 -> 0.0.0.0/0,::/0
   9. Review and Launch > Launch
      1. Create a new key pair
      2. 이름은 원하는 이름 설정
      3. Download Key Pair
      4. Launch Instance

2. Elastic IP 받기

   1. Network & Security > Elastic IPs
   2. Allocate Elastic IP adress
   3. Allocate
   4. Associate Elastic IP address
   5. Instance > 아까 생성된 인스턴스 선택
   6. Associate

3. SSH 연결하기

   1. ssh ubuntu@아까_받은_Elastic_IP -i 다운받은_PEM_FILE

4. 필요한 패키지 설치

   1. sudo apt update && sudo apt -y upgrade
   2. sudo apt install -y python3 python3-pip python-dev python3-venv build-essential libpq-dev vim git
   3. sudo reboot

5. 패키지 설치하는 동안 settings.py 수정

   1. 환경변수 적용
      1. Debug는 아래 값 사용
         1. DEBUG = (os.eviron.get('DEBUG', 'True') != 'False')
      2. ALLOWED_HOSTS = [] 를 ALLOWED_HOSTS = [' * '] 로 수정
   2. pip freeze > requirements.txt
   3. git add -A
   4. git commit -m "edit for deployment"

6. 매번 하던 것들

   1. python3 -m venv venv
   2. git clone 내_GitHub_레포지토리 django-app
   3. cd django-app
   4. source ../venv/bin/activate
   5. pip install -r requirments.txt
   6. python manage.py runserver 0.0.0.0:8000
   7. [http://내_Elastic_IP:8000](http://xn--_elastic_ip-v455b:8000/) 로 접속해서 Django 화면이 표시되는지 호가인
   8. deactivate

7. PostgreSQL 설치

   1. sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
   2. wget --quiet -0- https://postgresql.org.media/keys/ACCC4CF8.asc | sudo apt-key add -
   3. sudo apt update
   4. sudo apt -y install postgresql
   5. sudo systemctl enable --now postgresql@13-main
   6. sudo -u postgres createdb django
   7. sudo -u postgres psql django
   8. create user django with password 'p@ssword!';
   9. alter role django set client_dncoding to 'utf-8';
   10. alter role django set timezone to 'Asia/Seoul';
   11. grant all privileges on database django to django;

8. settings.py에 DB 설정

   1. 내 컴퓨터에서 VSCode 에서 settings.py 열기
   2. DATABASES = 부분을 아래와 같이 수정

   ```
   DATABASES = {
   'default': {
   'ENGINE': 'django.db.backends.postfresql_psycopg2',
   'NAME' : os.environ.get('DB_NAME'),
   'USER' : os.environ.get('DB_USER'),
   'PASSWORD': os.environ.get('DB_PASSWORD'),
   'HOST': os.environ.get('DB_HOST'),
   'PORT': '',
   }
   }
   ```

   1. git add -A
   2. git commit -m "edit database"
   3. git push

9. 업데이트된 설정 서버에 갖고오기 (서버에서 실행)

   1. cd/home/ubuntu/django-app
   2. git pull
   3. source ../venv/bin/activate
   4. pip install psycopg2

10. 환경 변수 설정(임시/테스트용)

    1. export DB_NAME=django
    2. export DB_USER=django
    3. export DB_PASSWORD='p@ssword!'
    4. export DB_HOST=localhost

11. 잘 작동하는지 테스트

    1. python manage.py makemigrations
    2. python manage.py migrate
    3. python manage.py runserver 0.0.0.0:8000
    4. [http://내](http://xn--220b/) Elastic IP:8000 로 접속해서 Django 화면이 표시되는지 확인

12. gunicorn 으로 Django App 실행

    1. pip isntall gunicorn
    2. deactivate
    3. ../venv/bin/gunicorn 프로젝트명.wsgi -b 0.0.0.0
    4. [http://내_Elastic_IP:8000로](http://xn--_elastic_ip-v455b:8000로/) 접속해서 Django 화면이 표시되는지 확인(사진 등 static files는 표시 안되는게 정상)
    5. systemd 에 gunicorn 등록

# DOCKER 이미지 생성

1. **준비 사항**
   1. Gitpod.io 계정 (Free or Student)
      1. GitpodFree 는 퍼블릭 레포만 작업 가능 /월 50시간 제한
      2. Gitpod Student는 프라이빗 레포도 작업 가능 /월 100시간 제한
         1. Gitpod Studnet는 학생 인증된 gitgub 계정으로 로그인 후 my subscription 페이지에서 확인 가능
   2. Gitpod 설정 수정
      1. Gitpod > Settings
         1. Feature Preview > Enable Feature Preview 체크
         2. Default IDE 선택
            1. Theia : Eclipse 팀이 만든 IDE / 강의에서 사용
            2. Code : VSCode 의 웹버전 IDE / 호환성 이슈 있음
   3. Gitpod 인스턴스 생성
      1. 본인의 GitHub 레포지토리로 이동
      2. 레포지토리 주소 앞에 gitpod.io/
      3. 예) gitpod.io/#https://github.com/username/repo
   4. DockerHub 계정생성
2. **requirements 설치**
   1. pip install -r requirements.txt
3. **Whitenoise 설치**
   1. pip install whitenoise
   2. MIDDLEWARE 에서 SecurityMiddleware 바로 아래 내용 추가
      1. 'whitenoise.middleware.WhiteNoiseMiddleware'
4. **Gunicorn 설치**
   1. pip install gunicorn
5. **Dockerfile 생성**

```
FROM python:3.8
ENV PYTHONUNBUFFERED=1
RUN mkdir /app
WORKDIR /app
COPY . /app
RUN apt-get update \
	&& apt-get install -y \
	python3 python3-pip python3-dev python3-venv build-essential libpq-dev \
	&& rm -rf/var/lib/apt/lists/*
RUN pip install -r requirements.txt
RUN chmod +x /app/run.sh
EXPOSE 8000

ENTRYPOINT ["/app/run.sh"]
```

 1.run.sh파일 생성

```
#!/bin/bash --> bash를 이용해서 실행시키겠다, 무시해도됨

python manage.py migrate

python manage.py collectstatic

gunicorn lionproject.wsgi b.0.0.0.0:8000 --> python manage.py runserver 대신에 사용하는 것
```



1. <u>pip freeze > requirements.txt</u>   #requirement 파일 생성
2. <u>sudo docker-up</u>  #이 창을 닫으시면 안됩니다
3. <u>Ctrl + Shift + `</u>  키로 새로운 터미널 열기  
4. <u>docker build -t DockerHubld/django-app .</u>  #도커 이미지 생성
5. <u>docker run -it -p 8000:8000 DockerHubld/django-app</u>  #생성된 도커 이미지 실행
6. <u>docker login</u>  #Docker Hub에 로그인(이미지 업로드용)
7. <u>docker push DockerHubld/django-app</u> #Docker Hub에 생성된 이미지 업로드
8. [https://hub.docker.com/r/DockerHubld/django-app](https://hub.docker.com/r/DockerHubld/django-app) 에서 내앱이 업로드된 것을 확인

# Docker 서버에 배포하기

### Docker로 배포하기(2. 서버 배포편)

1. **준비 사항**
   1. EC2 인스턴스 (AWS EC2 전반부 참고)
   2. Docker Hub에 등록된 이미지
2. **서버 세팅**
   1. Docker 설치
      1. curl -fsSL [https://get.docker.com|](https://get.docker.com|/) bash
   2. Docker Compose 설치
      1. sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)"
      2. sudo chmod +x /usr/local/bin/docker-compose
   3. 앱 설치 폴더 지정
      1. sudo mkdir /opt/django-app
      2. cd/opt/django-app
   4. docker-compose.yml 생성
      1. vi docker -compose.yml
      2. .env 파일 생성
3. **DB 최초 실행 (db 생성, 사용자 등록 등 진행)**
   1. sudo docker -compose up db
4. **잘 작동 되는지 테스트**
   1. sudo docker -compose up
   2. 내IP:8000 접속 되는지 확인
5. **백그라운드 모드로 전황**
   1. sudo docker -compose up -d

# Docker 이미지 자동 생성(Github Action)

### Docker로 배포하기 (3.이미지 자동 생성하기)

1. **준비사항**
   1. Docker로 배포하기가 끝난 레포
   2. GitHub 계정
2. **GitHub의 내 레포로 이동**
3. **Actions 버튼 선택**
   1. Setup a workflow yourself 선택
4. **이름을 docker-publish.yml로 설정후 아래 내용 작성**