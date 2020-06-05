---
layout: default
title: "[Django]장고튜토리얼(2) - 템플릿 실행하기"
published: 2020-06-04 11:45:00 +0200
read_time: true
comments: true
categories: development
tags: [Python, Django, Web]
github: "https://github.com/sneakstarberry/"
noimage: true
---
장고 세션에 따라 자신이 만든 html파일을 메인화면으로 바꿔보기로 하였다.

<!--more-->
# 장고 튜토리얼(2) - 템플릿 실행하기
## 작업 폴더 생성
<img src="/assets/images{{page.id}}/openfold.png" class = "img-responsive">

#### 위 그림 처럼 네비게이션 바에서 File - Open Folder를 합니다. 그럼 아래와 같은 창이 나옵니다.

<img src="/assets/images{{page.id}}/mkdir.png" class = "img-responsive">

#### `django`라는 이름으로 C드라이브에 새폴더를 생성해 줍니다. 그리고 해당 폴더를 폴더 선택을 눌러서 선택합니다. 이때 **폴더:**에 선택한 폴더이름이 나와 있어야합니다.
## 가상환경 생성
#### 그리고 이제 가상환경을 만들어 주겠습니다. "ctrl + `"키를 눌러서 터미널을 작동시켜줍니다. 그럼 다음과 같은 화면이 되었을 것 입니다.
<img src="/assets/images{{page.id}}/terminal.png" class="img-responsive">

#### 좋습니다. 여기서 이제 터미널에 아래 명령어를 입력해 주세요.
```shell
python -m venv myvenv
```
- ##### `-m`은 어떤 것을 만들어 주겠다는 것입니다.
- ##### `venv`는 virtual environment의 축약어로 가상환경을 의미합니다.
- ##### `myvenv`는 저희가 생성하는 가상환경의 이름을 의미합니다. 사실상 원하는 이름을 붙이셔도 됩니다.
이 모든 것을 합치면 `myvenv`라는 가상환경을 생성해 주겠다는 명령어가 됩니다.

#### 그럼 다음과 같이 폴더가 생깁니다.
<img src="/assets/images{{page.id}}/venv.png" class="img-responsive">

#### 그러면 가상환경을 실행시켜 보겠습니다.
```shell
source myvenv/scripts/activate
```
<img src="/assets/images{{page.id}}/venv_active.png" class="img-responsive">

#### 그럼 위와 같이 `(myvenv)`가 생겼다면 가상환경이 실행이 된 것 입니다.
## 실습 폴더 깃 클론 받기

#### 가상환경을 실행 시켰다면 다시 터미널에 다음 명령어를 입력해 봅니다.
```shell
git clone https://github.com/SYULION8TH/django_1st.git
```
#### 이 명령어를 입력하면 다음과 같이 될 것 입니다.
<img src="/assets/images{{page.id}}/clone.png" class="img-responsive">

#### 그리고 폴더 구조는 다음과 같을 것 입니다.
<img src="/assets/images{{page.id}}/clone_dir.png" class="img-responsive">

## 패키지 다운 받기
#### 이제 명령어를 통해 장고 와 부가적으로 필요한 패키지를 다운 받아야 합니다. `pip install django`를 통해 장고를 다운 받을 수도 있지만 실습 환경을 동일하게 하기 위해서 만든 requirements.txt를 통해서 `pip install`을 진행 하고자 합니다.
#### 그렇다면 requirements.txt가 있는 폴더로 이동을 해야 합니다. 먼저 터미널에 `dir` 혹은 `ls`명령어를 입력합니다.
```shell
dir
```
#### 아래와 같이 나올 것 입니다.
<img src="/assets/images{{page.id}}/dir.png" class ="img-responsive">

#### `django_1st`와 `myvenv`가 나옵니다. 현재 경로에 있는 폴더를 의미합니다.
#### 이제 `requirements.txt`가 있는 `django_1st`로 경로를 이동하도록 하겠습니다.
```shell
cd django_1st/
```
<img src="/assets/images{{page.id}}/cd.png" class="img-responsive">

#### `cd`는 `change directory`의 약자입니다. 빨간색으로 표시된 부분을 보면 `django`에서 `django_1st`로 경로가 변경이 된 것을 볼 수 있습니다.

#### `dir` or `ls`명령어를 통해서 제대로 이동이 되었는지 확인해 봅니다.
<img src="/assets/images{{page.id}}/dir2.png" class="img-responsive">

#### `requirements.txt`가 있는 것을 볼 수 있습니다.
```shell
pip install -r requirements.txt
```
#### 위 명령어를 실행하면 다음과 비슷한 화면을 볼 수 있습니다.
<img src="/assets/images{{page.id}}/pip.png" class="img-responsive">

#### 만일 빨간색 문장이 나오거나 error라는 단어를 보셨다면 잘못 친 것은 없는지 확인하여야 합니다.
## 장고 실행
#### 이제 장고가 제대로 설치되었는지를 확인하기 위해 가볍게 실행해 보겠습니다. 이에 앞서 장고 프로젝트 폴더로 들어가 보겠습니다.
```shell
cd blog
```
#### 다음과 같이 경로가 바뀌어야합니다.
<img src="/assets/images{{page.id}}/cd2.png" class="img-responsive">
#### `dir`명령어를 통해 확인을 해줍니다.
<img src="/assets/images{{page.id}}/dir3.png" class="img-responsive">
#### 위와 같이 `blog`와 `manage.py`가 있다면 제대로 따라오셨습니다.
#### 이제 장고를 실행 시켜봅니다.
```shell
python manage.py runserver
```
#### 위의 명령어로 장고 서버를 실행 시킬 수 있습니다.
<img src="/assets/images{{page.id}}/runserver.png" class="img-responsive">
#### 이렇게 서버가 실행이 되고 `http://127.0.0.1:8000/`를 `ctrl+Click`을 통해서 페이지를 열어 줍니다.
#### 그럼 아래와 같은 이미지의 페이지가 생깁니다.
<img src="/assets/images{{page.id}}/defaultPage.jpg" class="img-responsive">
## 장고 앱 생성하기
#### 현재는 `blog`라는 프로젝트 폴더만 있지만 앱을 생성해 주어야합니다. 다음 명령어를 입력해 봅니다.
``` shell
python manage.py startapp posts
```
- #### `startapp`은 앱을 만든다는 명령어입니다.
- #### `posts`는 앱의 이름입니다. 굳이 `posts`가 아니어도 됩니다.
#### 위 명령어를 입력하면 다음과 같이 `posts`폴더가 생성됩니다.
<img src="/assets/images{{page.id}}/app.png" class="img-responsive">
## 앱 등록
#### 앱을 생성했으면 앱을 등록 해야합니다.
#### `blog`폴더 안에 `settings.py`를 눌러줍니다.
```python
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
...
```
#### 33번째 줄에 위와 같은 코드가 있을 겁니다. 이 코드 안에 `'posts'`를 추가 시켜 줍니다.
```python
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'posts',
]
...
```
> #### 코드를 작성한 후에는 `Ctrl+S`를 눌러서 저장을 해줍니다.

## 장고 template 쓰기
### `html`파일 추가하기
#### 정해진 경로를 생성해야합니다.`posts`폴더 안에 `templates`폴더를 생성합니다. 이는 장고에서 정해진 경로로 `templates`라는 폴더 이름을 지켜줘야 합니다. 저희는 여기에 현재 앱이름과 같은 `posts`라는 폴더를 `templates`폴더 안에 만들어줍니다. 그러면 아래 사진과 같이 될 것 입니다.
<img src="/assets/images{{page.id}}/dir_template.png" class="img-responsive">
#### 먼저 `index.html`을 만들어준 경로에 복사 붙여넣기 해주도록 한다.
<img src="/assets/images{{page.id}}/index.png" class="img-responsive">
### `views.py`파일 코드 작성하기
#### `posts`폴더 아래 `views.py`를 눌러서 열어줍니다.
<img src="/assets/images{{page.id}}/dir_views.png" class="img-responsive">
#### `views.py`내의 코드를 다음과 같이 바꾸어 준다.
<img src="/assets/images{{page.id}}/views.png" class="img-responsive">
#### 추가된 코드
```python
def home(request):
    return render(request, "posts/index.html")
```
> #### 코드를 작성한 후에는 `Ctrl+S`를 눌러서 저장을 해줍니다.

### `urls.py`를 변경하여 라우팅을 해줍니다.
> 라우팅이란? 여기서는 경로를 배정을 해주는 것입니다. 사용자가 어떤 경로를 요청하느냐에 따라서 다른 페이지를 전달 할 수 있게 해줍니다. 
>> 예시 `https://comic.naver.com/index.nhn`이와 같은 경로를 보았을 때 웹툰 페이지를 `index.nhn`로 경로 배정을 했다는 것을 알 수 있습니다.

<img src="/assets/images{{page.id}}/urls.png" class="img-responsive">
#### `blog`폴더 안에 있는 `urls.py`를 눌러주어서 코드를 봅니다.
#### `urls.py`파일의 16번째 줄에 다음과 같은 코드가 있을 것 입니다.
```python
...
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```
#### 그렇다면 이곳에 다음과 같이 코드를 추가해 줍니다.
```python
...
from django.contrib import admin
from django.urls import path
import posts.views # 추가된 코드

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', posts.views.home, name="home"), # 추가된 코드
]
```
### 장고 서버 실행하기
#### 모든 준비는 끝났습니다. 이제 서버를 실행해 줍니다.
```shell
python manage.py runserver
```
#### 위 명령어로 서버를 실행합니다.
<img src="/assets/images{{page.id}}/result.png" class="img-responsive">
#### 위 사진과 같이 나온다면 성공하셨습니다. 엉성해보이지만 .css파일을 static폴더에 추가 시켜 주면 될 일 입니다.