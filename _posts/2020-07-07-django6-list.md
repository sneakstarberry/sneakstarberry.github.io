---
layout: default
title: "[Django]장고튜토리얼(6) - 리스트"
published: 2020-07-07 00:15:00 +0200
read_time: true
comments: true
categories: development
tags: [Python, Django, Web]
github: "https://github.com/sneakstarberry/"
noimage: true
---
장고 세션에 따라 포스트 리스트를 출력 해보기로 한다.

<!--more-->

# 장고 튜토리얼(6) - 리스트
## 리스트 페이지 html을 만들기
### `templates/blog` 아래의 `index.html`을 `ctrl+c` 그리고 `ctrl+v`를 해주어서 `index copy.html`을 만들어 줍니다.
<img src="/assets/images{{page.id}}/copy.png" class="img-responsive">

### 이후 `index.html`을 더블 클릭해서 파일을 열어줍니다. 그리고 아래 사진의 내용으로 가줍니다.
<img src="/assets/images{{page.id}}/swap.png" class="img-responsive">

### 이제 빨간 네모 사이의 내용을 바꿀 겁니다. <br/>※주의※ 네모 바깥의 `<div>`요소는 바꾸지 마시오.
<img src="/assets/images{{page.id}}/swap2.png" class="img-responsive">

#### 다음 코드로 내용을 바꿉니다.
```html
{% raw %}<div>
    <!-- for문 템플릿 태그 -->
    {% for post in posts %}
    <!-- 카드 요소 시작 -->
    <div class="card mb-3" style="max-width: 540px;">
        <div class="row no-gutters">
        <div class="col-md-4">
            <img src="{{ post.img.url }}" class="card-img" alt="...">
        </div>
        <div class="col-md-8">
            <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <p class="card-text">{{post.summary}}</p>
            <p class="card-text">
                <small class="text-muted">Created at: {{ post.created_at }}</small><br/>
                <small class="text-muted">Updated at: {{ post.updated_at }}</small>
            </p>
            </div>
        </div>
        </div>
    </div>
    <!-- 템플릿 태그를 끝내는 태그 -->
    {% endfor %}
</div>{% endraw %}
```
##### 1. `{% raw %}{% %}{% endraw %}` 이 부분은 장고의 템플릿 태그 선언 부분입니다. 
##### 2. 템플릿 태그 안에는 파이썬 코드를 넣을 수 있습니다. `for post in posts`는 파이썬에서 for문 형식과 같습니다.
##### 3. html에서는 파이썬 코드가 언제 끝나는지 모르기 때문에 `endfor`를 이용하여 `for문`이 끝났다는 것을 알려줍니다.
>템플릿 태그란?
>>HTML에 여러분은 파이썬 코드를 바로 넣을 수 없습니다. 브라우져는 파이썬 코드를 이해할 수 없기 때문입니다. 브라우저는 HTML만을 알고 있습니다. 알다시피 HTML는 정적이지만, 파이썬은 동적입니다.<br/>
>>템플릿 태그는 파이썬을 HTML로 바꿔주어, 빠르고 쉽게 동적인 웹 사이트를 만들 수 있게 도와줍니다.


#### 이때 서버를 실행 시켜 보면 빈 공간만을 볼 수 있을 겁니다.
<img src="/assets/images{{page.id}}/empty.png" class="img-responsive">
##### `views.py`에서 제대로된 데이터를 안넘겨주기 때문입니다.
### `views.py`에서 제대로된 데이터 넘겨주기
#### 1.4.1. `views.py`로 가봅시다. 아마 아래와 같이 코드가 적혀있을 겁니다.
```python
from django.shortcuts import render
from .models import Post
# Create your views here.
def home(request):
    posts = Post.objects.all()
    return render(request, "posts/index.html", {"post":posts[0]})
```
#### 1.4.2. 위 코드 중 `{"post":posts[0]}`을 `{"posts":posts}`로 바꿉니다.
##### 사진에 빨간색 네모 부분을 바꾸어 주면 됩니다.
<img src="/assets/images{{page.id}}/swap3.png" class="img-responsive">
```python
{"posts":posts}
```
##### 1. `"posts"`이 부분은 html에서 어떤 변수 형태로 받는지를 알려줍니다.
##### 2. `posts`는 `views.py`에서 사용되고 있는 변수 입니다.
##### 3. `{"posts":posts}`이 형태는 뒤에 '`posts`라는 변수를 html에서 앞의 `posts`라는 변수로 이용하겠다' 라는 것 입니다.

### 리스트 보여주기
<img src="/assets/images{{page.id}}/index.png" class="img-responsive">
#### 1.5.1. 아직 하나만 있어서 감이 잘 안오는 군요. 하나 더 추가해 보겠습니다.
##### 1.5.1.1. `/admin`페이지로 들어 갑니다.
`http://127.0.0.1:8000/admin`페이지에서 관리자 아이디로 로그인 해줍니다. 저의 경우 아이디: dev, 비밀번호: 12345
##### 1.5.1.2. add버튼을 눌러서 포스트를 작성해줍니다.
<img src="/assets/images{{page.id}}/addpost.png" class="img-responsive">
##### 1.5.1.3. 저장을 눌러서 작성한 포스트를 추가해줍니다.
<img src="/assets/images{{page.id}}/save.png" class="img-responsive">
##### 1.5.1.4. 추가해 주었으면 다시 홈페이지로 돌아가 봅니다.
<img src="/assets/images{{page.id}}/index2.png" class="img-responsive">

### 요약문 나오게 하기
#### 제목만 나오면 내용을 짐작하기 힘드니 내용도 조금 나오게 만듭니다.
#### 1.6.1. `models.py`파일을 열어줍니다.
```python
from django.db import models

# Create your models here.

class Post(models.Model):
    title = models.CharField(max_length= 100)
    body = models.TextField()
    img = models.ImageField(upload_to = "posts/image", null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```
위와 같이 코드가 작성되어 있을 것 입니다. 이제 이 아래에 다음과 같이 코드를 추가해 줍니다.
```python
from django.db import models

# Create your models here.

class Post(models.Model):
    title = models.CharField(max_length= 100)
    body = models.TextField()
    img = models.ImageField(upload_to = "posts/image", null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title

    # 추가된 코드
    def summary(self): # self는 자기 자신을 가르킨다.
        return self.body[0:30] + "..." # 포스트 글의 body요소를 돌려주는데 0에서 30까지만 돌려준다.
                                       # 즉 30글자만 보여준다.
                                       # + "..." 문자열을 +연산자로 연결해준다.
```
### 완성
#### 다시 홈페이지로 가보면 요약글까지 완벽하게 되어있다.
<img src="/assets/images{{page.id}}/index3.png" class="img-responsive">














