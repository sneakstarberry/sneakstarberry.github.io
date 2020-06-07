---
layout: default
title: "[Django]장고튜토리얼(5) - Media 파일"
published: 2020-06-06 19:30:00 +0200
read_time: true
comments: true
categories: development
tags: [Python, Django, Web]
github: "https://github.com/sneakstarberry/"
noimage: true
---
장고 세션에 따라 Media 파일을 이용해보기로 한다.

<!--more-->
# 장고 튜토리얼(5) - Media 파일
    개발과정에서 미리 준비되는 `static`과는 달리, 업로드 기능을 통해 프로젝트에 업로드 되는 파일

<img src="/assets/images{{page.id}}/media.png" class="img-responsive">

## Static & Media
- #### 파일을 알아내기 위해서
    - Static: 프로젝트 외부와 통신 하지 않음
    - Media: 프로젝트 외부와 통신을 통해 파일을 얻음

- #### 장고 프로젝트는 외부와 URL을 통해서 통신한다.
- #### 따라서 외부 업로드 기능 (Media 파일)을 사용하기 위해서는 `settings.py`에 다음과 같은 설정을 해야한다.
    - 내부 디렉토리 경로: 업로드될 파일을 저장할 장소
    - URL: 외부와의 통신 수단

## Media의 설정 과정
1. `settings.py`에 `media` 파일 설정 (디렉토리, `url`설정)
2. `urls.py`에서 `path` 설정
3. admin 페이지에서 사진 업로드
4. html에서 media사진 쓰기

## Media 설정 하기(실습)

### `settings.py`에 `media`파일의 저장폴더와 `url` 경로 설계
`settings.py`맨 아래에 다음과 같은 코드를 추가해 줍니다.
```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
# media파일들이 내부에 어디로 모일 것 인지 알려줌

MEDIA_URL = '/media/'
# 홈페이지/media/filename 과 같이 url이 설계됩니다.
```

### URL설정(`urls.py 에서 path 추가)
blog 폴더 아래에 있는 `urls.py`에 들어가 줍니다.
```python
from django.contrib import admin
from django.urls import path
import posts.views
```
아래에 다음 코드를 추가해 줍니다.
```python
from django.conf import settings
from django.conf.urls.static import static
```
그리고 
```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', posts.views.home, name="home"),
]
```
위 코드 아래에 다음 코드를 추가해 줍니다.
```python
urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
# 각각의 media 파일마다 url경로를 생성시켜준다.
```

### admin 페이지에서 사진 업로드
이전에 접속 했었던 admin 페이지로 이동합니다. `http://127.0.0.1:8000/admin`으로 이동을 하고 로그인을 요구하면 username: dev, password: 12345를 입력하고 로그인을 합니다.
<img src="/assets/images{{page.id}}/update.png" class="img-responsive">
`Posts`를 눌러줍니다. 아래와 같은 사진이 나올 것입니다. 하나있는 글을 눌러줍니다.
<img src="/assets/images{{page.id}}/select.png" class="img-responsive">
그럼 이전에 썻던 글이 나올 것입니다. 여기서 이미지를 다시 바꿔 봅니다.
<img src="/assets/images{{page.id}}/change.png" class="img-responsive">
이미지를 바꾼 후 `SAVE`를 눌러서 저장을 해줍니다. 왜냐하면 그것이 `SAVE`니깐...
<img src="/assets/images{{page.id}}/media_dir.png" class="img-responsive">
폴더 트리를 확인해보면 media 폴더가 추가 되어있고 안에 저희가 올리 사진이 있다는 것을 알 수 있습니다.

### html에서 media사진 쓰기
    이제 html에서 업로드 된 media사진을 어떻게 사용하는지 알아볼 것 입니다.

#### 본문 내용 위에 사진을 추가하겠습니다.
<img src="/assets/images{{page.id}}/media_tag.png" class="img-responsive">
```html
<img style="width:60%;margin: auto; margin-top: 5%;"src="{{post.img.url}}" />
```
위 코드를 사진 자리 처럼 추가 해 주었습니다.
<img src="/assets/images{{page.id}}/result.png" class="img-responsive">

# 완성!!
