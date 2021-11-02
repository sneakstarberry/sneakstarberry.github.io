---
layout: default
title: "[Dart]다트(3) - 특이한 연산자"
published: 2020-07-12 16:22:00 +0200
read_time: true
comments: true
categories: development
tags: [Dart, Flutter, Web, App, Hybrid]
github: "https://github.com/sneakstarberry/"
noimage: true
---
다트 특이 연산자

<!--more-->

# 다트(3) - 특이 연산자
#### 다트에서는 '?'를 굉장히 다양한 곳에 씁니다. 어디에 쓰이는지 알아보도록 하겠습니다.

예시)
```dart
main(){
    String name;

    print(name ?? "비어있습니다."); // 비어있습니다.
}
```
- #### '??'는 좌항의 값이 null이면 오른쪽의 값을 내보내줍니다.
- #### 이렇듯 다트에서는 '?'를 null 값을 처리하는데 많이 쓰입니다. 지금은 간단한 예시이고 다양한 상황에서의 '?'쓰임을 보겠습니다.

## 함수
### 리턴 값이 null
#### 리턴 값이 null 값이 될 수도 있을 때 이용합니다.
#### 리턴 타입 뒤에 '?'를 붙여줍니다.
```dart
int? plus(int a,int b){
    return a > 3 ? a+b : null; // 일반적인 삼항연산자
}
main(){
    print(plus(5, 5)); // 10
    print(plus(3, 5)); // null
}
```
### 매개변수의 값이 null
#### 매개변수의 값이 null이 될 수 있을 때 이용합니다.
#### 매개변수의 타입 뒤에 '?'를 붙여줍니다.
```dart
void printer(String? name){
    print(name);
}

main(){
    printer(null); // null
    printer("sneakstarberry"); // sneakstarberry
}
```

## 조건 표현식
### 삼항 연산자
#### 삼항 연산자는 우리가 익히 아는 형태입니다.
```dart
조건 ? 표현식1: 표현식2;
```
#### 이미 알고 있는 형태이므로 예시는 생략하겠습니다.
### 조건적 멤버 접근(Conditional member access)연산자
#### 이 연산자는 좌항이 null이면 null을 리턴하고 아니면 우항의 값을 리턴합니다.
```dart
좌항?.우항
```
#### 위와 같은 형태로 되어 있습니다.
예시)
```dart
class Student {
    String name;
}
main(){
    Student student = Student();
    print(student.name?.length);
}
```
#### employee가 null이면 null을 리턴하고 아니면 employee의 name에 접근합니다. 잘못된 메모리에 접근하는 것을 막기 위해 쓰입니다.

### 좌항 ?? 우항
#### 좌항 ?? 우항 형태의 연산자 입니다.
#### 좌항이 null이 아니면 좌항을 리턴하고 null이면 우항을 리턴 합니다.
#### ※null값은 오류의 원인이 되기도 합니다. 그래서 null값이 나오는 사태를 대비하여서 '??'연산자를 씁니다.
좌항 값이 null일 때의 경우 입니다.
```dart
main(){
    String name;

    print(name ?? "비어있습니다."); // 비어있습니다.
}
```
좌항 값이 들어 있을 경우 입니다.
```dart
main(){
    String name;

    name = "sneakstarberry"

    print(name ?? "비어있습니다."); // sneakstarberry
}
```
## 캐스케이드 표기법
#### 캐스케이드 표기법(..)은 한 객체로 해당 객체의 속성이나 멤버 함수를 연속으로 호출할 때 유용합니다.

```dart
class Student {
    String name;
    int age;
    showInfo(){
        print('name: $name, age: $age');
    }
}

main() {
    Student sneakstarberry = Student()
      ..name = 'sneakstarberry'
      ..age = 27
      ..showInfo();
}
```
#### '..'를 통해 연속으로 해당 객체의 속성을 지정해 주었습니다.
#### ※ ';' 표기를 마지막에 한번 해주어야 합니다.

## 타입 검사 연산자

### is: 객체가 특정 타입이면 true
```dart
좌항 is 우항(타입)
```
#### 좌항의 타입이 우항에 써놓은 타입과 같을 때 `true`를 반환 한다.
예시)
```dart
main(){
    String name;
    name = 'sneakstarberry';
    print(name is String); // true
}
```

### !is: 객체가 특정 타입이면 false

```dart
좌항 !is 우항(타입)
```
#### 좌항의 타입이 우항에 써놓은 타입과 같을 때 `false`를 반환 한다.
예시)
```dart
main(){
    String name;
    name = 'sneakstarberry';
    print(name !is String); // false
}
```





