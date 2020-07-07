---
layout: default
title: "[Django]장고튜토리얼(7) - 페이지네이션"
published: 2020-07-07 09:40:00 +0200
read_time: true
comments: true
categories: development
tags: [Python, Django, Web]
github: "https://github.com/sneakstarberry/"
noimage: true
---
장고 세션에 따라 포스트 리스트를 페이지네이션 해보기로 한다.

<!--more-->

# 장고 튜토리얼(7) - 페이지네이션
#### 장고 페이지 네이션을 이용해보겠습니다.
> 페이지네이션이란?
>> 페이지네이션은 리스트를 일정 갯수에 따라 페이지를 나누는 것을 의미한다.

## `views.py` 코드 변경
### 앱의 `views.py` 파일을 열어 줍니다. 그렇다면 코드는 다음과 같을 것 입니다.
```python
from django.shortcuts import render
from .models import Post
# Create your views here.
def home(request):
    posts = Post.objects.all()
    return render(request, "posts/index.html", {"posts":posts})
```

#### 코드를 바꾸어줄 것 입니다.

```python
from django.shortcuts import render
from .models import Post
from django.core.paginator import Paginator # 추가된 코드
# Create your views here.                   # 장고 내장 페이지네이션 기능을 가져온다.
def home(request):
    posts = Post.objects.all()

    paginator = Paginator(posts, 2) # 페이지네이터 함수 사용하여 2개 단위로 페이지 나누기

    page_number = request.GET.get("page") # 페이지 넘버 가져오기
    page_posts = paginator.get_page(page_number)

    return render(request, "posts/index.html", {"posts":page_posts}) # 페이지네이션 변수 page_posts를 템플릿의 posts로 받기
```

#### `views.py`에서 코드를 고쳤으니 이제 템플릿에서 페이지네이션을 이용해봅시다.

## `index.html`의 코드 고치기
### `index.html`의 for문 템플릿 태그가 끝나는 곳에 페이지네이션을 추가해줍니다.

```html
{% raw %}<div class="pagination">
    <span class="step-links">
    {% if posts.has_previous %}
    <a href="?page=1">&laquo; first</a>
    <a href="?page={{ posts.previous_page_number }}">previous</a>
    {% endif %}
    <span class="current">
        Page {{ posts.number }} of {{ posts.paginator.num_pages }}.
    </span>
    {% if posts.has_next %}
    <a href="?page={{ posts.next_page_number }}">next</a>
    <a href="?page={{ posts.paginator.num_pages }}">last &raquo;</a>
    {% endif %}
    </span>
</div>{% endraw %}
```

#### 위 코드를 추가하면 페이지네이션이 나옵니다.
<img src="/assets/images{{page.id}}/index.png" class="img-responsive">


### 아직 글이 두개 밖에 없어서 다음 페이지가 안나옵니다. 새롭게 글을 추가하고 리스트를 봅니다.
#### 첫번째 페이지
<img src="/assets/images{{page.id}}/index2.png" class="img-responsive">

#### 두번째 페이지
<img src="/assets/images{{page.id}}/index3.png" class="img-responsive">