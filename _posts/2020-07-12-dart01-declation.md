---
layout: default
title: "[Dart]다트(1) - 변수 선언"
published: 2020-07-07 2:40:00 +0200
read_time: true
comments: true
categories: development
tags: [Dart, Flutter, Web, App, Hybrid]
github: "https://github.com/sneakstarberry/"
noimage: true
---
다트 변수 선언하기

<!--more-->

# 다트(1) - 변수 선언
## 다트는 기본적으로 타입 추정이 되는 언어입니다.
> 타입추정 이란?
>
> > 타입을 명시하지 않아도 컴파일이 되는 동안 타입을 추정해서 변수의 타입을 정하는 것.


#### 변수 선언
타입 추정을 이용한 변수 선언이 있고 타입을 명시해서 변수를 선언해 주는 방법이 있습니다.
### 타입 추정을 이용한 변수 선언
```dart
main() {
    var name = 'sneakstarberry';
    // or
    dynamic name2 = 'sneakstarberry2';
    
    print(name); // sneakstarberry
    print(name2); // sneakstarberry2
    // name의 타입은 자동으로 String이 된다.
    print(name.runtimeType); // String
    print(name2.runtimeType); // String
}
```

`var`과 `dynamic`의 차이는 `var`은 타입 세이프가 되고 `dynamic`은 타입 세이프가 되지 않는다.

> 타입 세이프란?
>
> > 타입 추정으로 정해진 타입을 중간에 바꿀 수 없도록 하는 것

```dart
main() {
    var name = 'sneakstarberry';
    name = 1; // 오류 코드
    
    dynamic name2 = 'sneakstarberry';
    name2 = 1; // 오류가 나지 않는다.
}
```



### 타입을 명시한 변수 선언

```dart
main() {
    String name = 'sneakstarberry';
    
    print(name); // sneakstarberry
    print(name.runtimeType); // String
}
```
<br/>

#### 기본 타입들(자주 쓰이는 타입)

| 타입   | 설명                                            |
| ------ | ----------------------------------------------- |
| num    | int 가 될 수 있고 double이 될 수 있는 숫자 타입 |
| int    | 정수 타입                                       |
| double | 실수 타입                                       |
| String | 문자열                                          |
| bool   | 참/거짓이 나오는 boolean 타입                   |





