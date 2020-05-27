---
layout: default
title: "[Django]장고튜토리얼(1) - 시작하기"
date: 2020-05-27 4:10:00 +0200
published: 2020-05-28 4:10:00 +0200
comments: true
categories: development
tags: [Python, Django]
github: "https://github.com/sneakstarberry/"
noimage: true
---
장고 초심자들을 위한 튜토리얼 포스팅입니다. 그리고 저 또한 초심을 바로 잡기 위해 시작합니다.
**이 장고 튜토리얼은 [장고 공식 페이지](https://www.djangoproject.com/)를 참고 하였습니다.


장고 튜토리얼(1) - 시작하기
==========================

<!--more-->

시작하기
--------------------



어떤 일을 하는데 있어서 언제나 시작이 있습니다. 그리고 지금은 장고를 시작할 때입니다. 

**이 튜토리얼은 vscode를 기반으로 진행하도록 하겠습니다. 

### 바탕화면에 `tutorial`이라는 새로운 폴더를 생성해 줍니다.

### vscode를 열고 `tutorial`이라는 폴더를 열어줍니다.

### 먼저 패키지들을 관리하기 용이하도록 가상환경(`venv`)을 실행하도록 하겠습니다.  

실행하기 앞서 가상환경이 무엇을 하는지 알아보도록 하겠습니다.

- #### 가상환경의 장점

  1. 응용 프로그램 간의 서로 다른 버젼의 패키지를 이용할 수 있게한다.
  2. 서로 다른 환경에 패키지를 설치하여 서로의 환경에 영향을 미치지 않게 해준다.

 물론 지금 이런 모든 것들을 이해할 필요는 없습니다.  그냥 이런 말들이 있다는 것을 알아두고 가면 됩니다.

이제 손으로 직접 입력을 하도록 하겠습니다.

```shell
python -m venv myvenv
```

위와 같이 적어주어서  `myvenv`라는 가상환경을 생성시켜 줍니다. 그렇게 되면 `tutorial`파일 트리에 `myvenv`라는 폴더가 생겨난 것을 볼 수 있습니다.

이제 가상환경을 실행 시켜 주어야합니다. 다음 명령어를 입력해 줍니다.

```shell
source myvenv/scripts/activate
```

이 명령어를 입력했을 때 `(myvenv)`가 명령어 아래에 출력이 되면 가상환경이 실행된 것 입니다.

### 장고 설치

자, 장고는 `python`으로 만들어진 프레임 워크이고 `python`은 `pip`라는 패키지 관리 시스템을 이용합니다. 그렇기 때문에 `pip`명령어를 통해 장고를 설치하도록 하겠습니다.

```shell
pip install django
```

위 명령어를 입력하면 무언가를 다운받기 시작 할 것 입니다. 시간을 두고 모든 과정이 끝날 때 까지 기다려줍니다. 아니면 커피 한잔의 여유도 괜찮습니다.

### 프로젝트 생성

모든 설치가 끝나면 다음 명령어를 입력하여 장고 프로젝트를 생성하도록 하겠습니다.

```shell
django-admin startproject blog
```

`tutorial`폴더 아래에 `blog`폴더가 생성될 것입니다.

### 장고 서버 실행하기

이제 장고 서버를 실행시키면 이번 포스팅은 완료! 입니다.

현재 터미널의 경로는 `tutorial`폴더에 있습니다. `~/Desktop/tutorial` 이런 식으로 표현이 되어있을 겁니다. 이것을 `~/Desktop/tutorial/blog`로 바꾸어 줄 것 입니다. 이쯤되면 눈치를 채셨겠지만 마지막에 오는 폴더 이름이 현재 터미널이 위치하고 있는 폴더입니다. 그러면 이 위치를 바꿔주기 위한 명령어를 입력하겠습니다.

```shell
cd blog
```

이제 터미널의 경로도 변경하였으니 이제 장고 서버를 실행하도록 하겠습니다.

```shell
python manage.py runserver
```

이 명령어를 실행하게 되면 `Starting development server at http://127.0.0.1:8000/`라는 문구가 나올 것 입니다.문구를  `Ctrl + click`을 해줍니다.  그러면 아래와 같은 웹페이지가 보이게 될 것입니다. 안보인다구요? 그건.... 일단 내 잘못은 아닌듯 합니다.

<img src="/assets/images/{{page.id}}/top.jpg" alt = "장고 기본 페이지" style = "width:700px">

이상 포스팅을 마치겠습니다. ^^