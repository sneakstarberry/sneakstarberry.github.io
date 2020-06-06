---
layout: default
title: "[Django]장고튜토리얼(4) - 모델 사용하기"
published: 2020-06-06 19:30:00 +0200
read_time: true
comments: true
categories: development
tags: [Python, Django, Web]
github: "https://github.com/sneakstarberry/"
noimage: true
---
장고 세션에 따라 모델을 이용하여 html안에 포스트 내용을 대체해보기로 한다.

<!--more-->
# 장고 튜토리얼(4) - 모델 사용하기
<img src="/assets/images{{page.id}}/MVT.png" class="img-responsive">
위 그림에서 MODEL부분을 어떻게 사용하는지 실습을 할 것입니다.
## 시작하기 앞서
    정적 웹페이지와 동적웹페이지를 배웠지만 아직은 html을 그대로 보여주기만하고 동적으로 내용이 바뀌게 하지는 않았습니다. 장고에서 동적웹페이지를 구현하고 싶다면 모델을 다루는 것은 필연적입니다. 왜냐하면 모델에 데이터들이 들어갈 것이기 때문입니다. 그리고 뷰에서는 모델에서 가져온 데이터들을 템플릿과 이리저리 조합해서 웹페이지를 제공해 줍니다. 이제 실습을 해보도록 하겠습니다.

> 이 포스팅 내용은 기본적으로 파이썬에 대한 이해도가 필요합니다. 제공된 파이썬 강의를 듣고 따라해주세요.

## models.py 코드추가
### models.py를 눌러줍니다.
<img src="/assets/images{{page.id}}/dir_model.png" class="img-responsive">
눌러주었다면 다음과 같은 코드들이 있을 것입니다.
```python
from django.db import models

# Create your models here.
```

### 코드추가

`Create your models here.`이라고 써져있는 부분이 있군요. 이 말에 따라 이 아래에 코드를 작성해 보도록 하겠습니다. 아래에 다음 코드를 추가해주세요.

```python
# Create your models here.

class Post(models.Model):
    title = models.CharField(max_length= 100)
    body = models.CharField(max_length=1000)
    img = models.ImageField(upload_to = "posts/image", null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```
- 저희는 위 코드로 장고에서 쓰일 데이터의 구조를 정해준 것입니다. 
- Post는 포스팅 글 하나를 말합니다.
- 저희는 포스팅 글(Post)이 제목(title), 내용(body), 사진(img), 글쓴 날짜(created_at), 수정한 날짜(updated_at)으로 이루어져 있다고 정해준 것 입니다.

## 마이그레이션 하기
### 설명
    모델에 하나의 class를 추가해 주었다면 마이그레이션이라는 것을 해주어야 합니다. 위의 그림을 보면 모델과 DB가 서로 통신을 하고 있는데 마이그레이션을 하기전에는 이 둘의 데이터가 같지 않은 상태입니다. 마이그레이션을 하면 모델에 쓰인 코드가 DB에도 적용이 되게 됩니다.


### 실습
터미널에 다음과 같이 명령어를 작성해 줍니다.
```shell
python manage.py makemigrations
```
아마 아래와 같은 에러가 발생할 것입니다. `Pillow`라는 패키지를 깔라고 하는 군요.
<img src="/assets/images{{page.id}}/pillow.png" class="img-responsive">
이러한 에러가 나오는 이유는 포스팅 글에 이미지 파일을 넣을려고 해서 입니다. python에서 이미지 파일를 다룰 땐 `Pillow`라는 패키지가 필요합니다. 그럼 패키지를 설치해 보겠습니다.
```shell
pip install Pillow
```
아래 그림과 같이 나오면서 설치가 완료되었습니다.
<img src="/assets/images{{page.id}}/pip_pillow.png" class="img-responsive">
그럼 다시 마이그레이션을 하겠습니다.
```shell
python manage.py makemigrations
```
<img src="/assets/images{{page.id}}/makemigrations.png" class="img-responsive">
사실 여러분에게 거짓말을 한 것이 있습니다. `makemigrations`라는 명령어는 사실 마이그레이션을 해주는 것이 아닌 마이그레이션할 목록을 작성하는 것이었습니다. 이제 목록을 다 작성하였으니 진짜로 마이그레이션을 해보겠습니다.
```shell
python manage.py migrate
```
위 코드를 실행하면 아래와 같은 이미지가 나오고 마이그레이션이 완료될 것입니다..
<img src="/assets/images{{page.id}}/migrate.png" class="img-responsive">

## 뷰(views.py) 코드 추가하기
이제 posts폴더 아래에 있는 `views.py`파일로 가보겠습니다.
```python
from django.shortcuts import render

# Create your views here.
def home(request):
    return render(request, "posts/index.html")
```
위와 같이 쓰여져 있을 것입니다. 위 코드를 아래코드와 동일하게 코드를 추가해 주세요.
```python
from django.shortcuts import render
from .models import Post

# Create your views here.
def home(request):
    posts = Post.objects.all()

    return render(request, "posts/index.html", {"post":posts[0]})
```


> `from .models import Post`와 `posts = Post.objects.all()` 그리고 `{"post":posts[0]}`이 추가 되었는데요. 하나 하나 보고 가겠습니다.


1. `from .models import Post`
    - 이 코드는 동일 폴더에 있는 `models`라는 곳에서 `Post`를 가져오겠다는 것입니다.
    - 저희가 방금 전만 해도 `models.py`파일에서 `Post`라는 모델을 만들었는데 위 코드는 이 내용을 가져오겠다는 것을 말합니다.
2. `posts = Post.objects.all()`
    - `Post`라는 모델의 모든 데이터를 가져오겠다는 의미의 코드입니다.
    - 그리고 모든 데이터들을 `posts`라는 변수에 담겠다는 의미입니다.
3. `{"post":posts[0]}`
    - 딕셔너리 자료형입니다. `post`에 `posts`데이터들 중 첫번째 데이터를 담습니다.
    - 이 코드를 통해서 저희는 html에 모델에 담겨있는 데이터를 이용할 수 있게 됩니다.





