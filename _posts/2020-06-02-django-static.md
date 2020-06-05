---
layout: default
title: "[Django]장고튜토리얼(3) - Static"
published: 2020-06-02 02:08:00 +0200
read_time: true
comments: true
categories: development
tags: [Python, Django, Web]
github: "https://github.com/sneakstarberry/"
noimage: true
---
장고의 Static 파일에 대해 알아본다. 장고튜토리얼(2)와 이어지는 내용입니다. 이전 내용을 보시지 않았다면 보시고 와주시길 바랍니다.
<!--more-->

# 장고의 Static 파일
장고에서 Static파일을 이용하는 방법을 알아보도록 하겠습니다. 하지만 실습에 앞서 `Static`파일이 무엇이지 알아보고 가도록 하겠습니다.
## Static 파일이란?
이미지나 CSS, JS파일 처럼 내용이 고정되어 있어, 응답을 할 때 별도의 처리 없이 파일 그대로를 보내주면 되는 파일들을 의미합니다. 즉, 사용자의 요청에 따라 내용이 바뀌는 것이 아니라 있는 파일 그대로를 보내주는 것을 의미합니다.

## Static 경로 설정
`Static` 파일을 이용하기 위해서 가장 중요한 점은 `settings.py`에서`django.contrib.staticfiles`가 INSTALLED_APPS에 포함되어 있는지 확인하는 것입니다. 기본적으로 포함되어 있지만 안될 때 확인해야할 중요 사항인건 맞습니다.
```python
...
INSTALLED_APPS = [
    'garden.apps.GardenConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles', # 이게 빠져있어선 안됩니다!
    'posts',
]
...
```
이 앱이 앞으로 우리의 `Static`파일들을 관리해 줄 것입니다.
그럼 해당 파일의 가장 밑으로 내려가 보겠습니다.
아마도 이런 코드를 볼 수 있을 것입니다.
```python
...
STATIC_URL = '/static/'
```
이 코드는 `Static`파일을 불러올 때의 URL을 의미합니다. 만약 `profile.jpg`라는 이미지가 있다면
```
http://127.0.0.1:8000/static/profile.jpg
```
위와 같은 url을 통해 이미지 주소가 만들어 지게 됩니다.
이 `STATIC_URL`아래에 다음과 같은 코드를 추가해 봅니다.
```python
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```
위 코드는 `Static`파일들이 모이는 경로를 정해주는 것입니다. 이 경우 `python manage.py collectstatic`이라는 명령어를 입력할 경우 `staticfiles`라는 폴더로 `Static`파일들이 모이게 될 것입니다.

그 아래에는 다음과 같은 코드를 추가해 봅니다.
```python
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'posts', 'static'),
)
```
위 코드는 `posts`라는 앱 안의 `static`폴더를 경로에 추가해 준 것입니다. 이러한 작업을 안할 경우 `python manage.py collectstatic`을 하였을 때 이 경로에 없는 폴더는 `Static`파일을 모으지 않게 됩니다. 그래서 이 코드를 반드시 추가해 주어야합니다.

## Static 파일 사용
### `posts`앱 안에 `static`폴더를 생성해줍니다.
- `static`폴더 이름은 이미 우리가 위에서 정해주었습니다.
- `static`폴더 안에 `posts`폴더를 생성하고 `posts`폴더 안에 `css`폴더를 생성해줍니다.
<img src="/assets/images{{page.id}}/static.png" class="img-responsive">
#### 위와 같이 폴더가 생성되어 있어야 합니다.
#### 이제 `css`폴더에 `index.css`를 복사 붙여넣기를 해줍니다.
<img src="/assets/images{{page.id}}/css.png" class="img-responsive">
#### 위와 같이 파일을 추가해 줍니다.
### `index.html`코드 바꾸어 주기
- #### `index.html`가장 위 첫번째 줄에 다음 코드를 작성해 줍니다.
```html
{% load static %}
...
```
- #### 그리고 css 가져오기라고 써져있는 글 아래의 코드를 바꾸어 줍니다.
```html
...
<link rel="stylesheet" href="index.css">
...
```
#### 위 코드를 다음과 같은 코드로 바꾸어 줍니다.
```html
...
<link rel="stylesheet" href="{% static 'post/css/index.css' %}">
...
```
- `static`폴더 아래의 경로를 적어주면 되는 것 입니다.
- 위 작업을 끝냈다면 서버를 실행 했을 때 다음과 같은 화면이 나올 것 입니다.
<img src="/assets/images{{page.id}}/result.png" class="img-responsive">


