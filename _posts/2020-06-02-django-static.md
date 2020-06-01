---
layout: default
title: "장고의 Static 파일"
published: 2020-06-02 02:08:00 +0200
read_time: true
comments: true
categories: development
tags: [Python, Django, Web]
github: "https://github.com/sneakstarberry/"
noimage: true
---
장고의 Static 파일에 대해 알아본다.
<!--more-->

# 장고의 Static 파일
장고에서 Static파일을 이용하는 방법을 알아보도록 하겠습니다. 하지만 실습에 앞서 `Static`파일이 무엇이지 알아보고 가도록 하겠습니다.
### Static 파일이란?
이미지나 CSS, JS파일 처럼 내용이 고정되어 있어, 응답을 할 때 별도의 처리 없이 파일 그대로를 보내주면 되는 파일들을 의미합니다. 즉, 사용자의 요청에 따라 내용이 바뀌는 것이 아니라 있는 파일 그대로를 보내주는 것을 의미합니다.

### Static 경로 설정
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
    'django.contrib.staticfiles' # 이게 빠져있어선 안됩니다!
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
    os.path.join(BASE_DIR, 'blog', 'static'),
)
```
위 코드는 `blog`라는 앱 안의 `static`폴더를 경로에 추가해 준 것입니다. 이러한 작업을 안할 경우 `python manage.py collectstatic`을 하였을 때 이 경로에 없는 폴더는 `Static`파일을 모으지 않게 됩니다. 그래서 이 코드를 반드시 추가해 주어야합니다.

사실 `STATIC_URL`만 하여도 `Static`파일들을 이용하는데에는 크게 무리가 없습니다. 왜냐하면 개발자 모드에서는 여러가지 부분들을 장고가 알아서 처리해주고 `Static`파일 또한 장고가 알아서 처리해주는 일 중에 하나이기 때문입니다. 하지만 배포 모드에서는 장고가 이러한 일들을 알아서 처리해 주지 않습니다. 그래서 모든 파일들을 하나로 모아주고 저희가 직접 연결시켜 주는 것입니다.


