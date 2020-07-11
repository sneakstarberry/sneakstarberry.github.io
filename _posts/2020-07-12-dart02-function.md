---
layout: default
title: "[Dart]다트(2) - 함수"
published: 2020-07-07 2:40:00 +0200
read_time: true
comments: true
categories: development
tags: [Dart, Flutter, Web, App, Hybrid]
github: "https://github.com/sneakstarberry/"
noimage: true
---
다트 함수

<!--more-->

# 다트(1) - 함수
## 다트 함수 형식
- #### 다트는 자바 문법과 유사점이 많고 자바스크립트와도 문법적인 유사점이 있습니다.
- #### 먼저 일반적인 함수 선언 방법을 보고 이후 Fat Arrow를 통한 함수 선언 방법을 살펴보도록 하겠습니다.

### 일반적인 함수식
dart의 일반적인 함수 선언 방법입니다.

```dart
타입 함수명(매개변수){
    함수...
    return 리턴 값
}
```
일반적으로 이러한 형태를 씁니다. 아래는 예제입니다.
```dart
main() {
    void printer(){
        print("Hello World");
    }

    printer(); // Hello World
}
```
dart에서는 변수를 선언할 때 처럼 함수를 만들때 타입을 붙이지 않아도 작동합니다.
```dart
main() {
    printer(){
        print("Hello World");
    }

    printer(); // Hello World
}
```
다른 언어와 문법적으로 유사합니다.

### Fat Arrow 함수식
#### 일반적으로 Fat Arrow 함수는 아래와 같은 형태를 가지고 있습니다.
``` dart
타입 함수명(매개변수...) {return 리턴 값};
```
#### 하지만 위와 같은 모양만 존재하는 것이 아닌 조금씩 다른 형태들을 가지고 있습니다. 
#### 아래 예제를 통해 알아보도록 하겠습니다.
``` dart
main() {
    void printer() => {print("Hello World")}; 
    void printer2() => print("Hello World"); // 짧은 식은 중괄호를 생략할 수 있다.
    printer3() => print("Hello World"); // 굳이 타입을 지정해 주지 않아도 된다.

    printer();
    printer2();
    printer3();
}
```

