---
layout: post
title: Java | 자바의 기본(2) 객체지향 
description: >

# sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc}

## 객체(Object)란 무엇인가?
> 실재하는 대상 (ex. 차, 책상, 컵, 컴퓨터 등등)

- object는 속성(state)와 기능(behavior)를 가진다. --> 변수(variable)와 함수(function)

![](/assets/img/2023-07-17-Java-Basic-2-OOP/2023-10-08-15-08-45.png)

출처 : codestates.com/blog
{:.figcaption}



## 객체지향의 4가지 특징

### 1. 추상화 (Abstract)

- 공통성과 본질을 모아 추출한다. --> 객체의 공통적인 속성과 기능을 추출하여 정의하는 것
- **왜?** : 핵심만 나타내어 복잡성을 줄인다. (일반화, 단순화와 비슷함), 역할(interface)과 구현의 분리가 가능하다. = 유연하고 변경이 용이함
- `java`에서는 추상클래스, 인터페이스를 통해 추상화를 구현한다.

![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-15-13-04.png) 

![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-15-13-15.png)
![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-15-13-21.png)
![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-15-13-26.png)


### 2. 다형성 (Polymorphism)

- 다양한 형태를 가질 수 있다.
- 예시) 메서드 오버라이딩(overriding) `재정의`와 오버로딩(overloading) `중복정의`
> 객체 지향 프로그래밍에서 다형성이란 한 타입의 참조변수를 통해 여러 타입의 객체를 참조할 수 있도록 만든 것을 의미합니다. 좀 더 구체적으로, 상위 클래스 타입의 참조변수로 하위 클래스의 객체를 참조할 수 있도록 하는 것입니다.

- `car`, `motorBike` class들을 호출하는 예시를 생각해봅시다. 
![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-18-13-25.png)

driver 클래스: drive() 메서드 오버로딩
{:.figcaption}

![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-18-15-45.png)

- **왜?**: 유연하고 확장이 용이하다. (ex. 탈 것에 버스, 택시 등이 추가되는 경우 등)


### 3. 캡슐화 (Capsultaion)

- 서로 연관있는 속성과 기능들을 하나의 캡슐로 만들어 데이터를 외부로부터 보호
- **왜?** : 데이터 보호, 내부 구조를 모르고 그냥 가져다 써서 결합도를 더욱 낮춰주는 역할

1. 접근제어자 활용 
![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-18-40-32.png)

2. getter() / setter() 메소드


### 4. 상속 (Inheritance)

- 기존의 클래스를 재활용하여 새로운 클래스를 작성하는 자바의 문법 요소
- 추상화의 연장선 개념으로, 클래스 들의 **공통 부분을 추출하여 상위 클래스로 추상화** 시킴
- **왜?**: 코드 재사용이 쉬워져 반복적인 코드를 최소화할 수 있다.
- `extends` 키워드 활용

![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-18-59-18.png)

![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-18-59-29.png)

![](/assets/img/2023-10-08-Java-Basic-2-OOP/2023-10-08-18-59-42.png)


### 자자, 추상화 vs. 상속은 어떻게 다른가?
- 공통점: 상위 - 하위의 관계가 존재하며, 공통적인 속성과 기능을 공유
- 차이점은, 상속의 경우 상위 클래스의 속성과 기능들을 하위 클래스에서 그대로 사용하거나, 선택적으로 overriding(재정의)하여 사용할 수 있는 반면
- 인터페이스를 통해 구현한 경우 반드시 인터페이스에 정의된 추상 메서드의 내용이 하위 클래스에서 정의되어야 한다. 

> 즉, 상속의 경우 인터페이스를 사용하는 구현에 비해 추상화의 정도가 낮다. 


## 객체지향 설계 원칙 5가지(SOLID)
1. SRP : Single Responsibility Principle (단일 책임의 원칙)
2. OCP : Open/Closed Principle (개방 폐쇄의 원칙)
3. LSP : Liskov’s Substitution Principle (리스코프 치환의 원칙)
4. ISP : Interface Segregation Principle (인터페이스 분리의 원칙)
5. DIP : Dependency Inversion Principle (의존성 역전의 원칙)


## 정리
### 높은 응집도(cohension)와 낮은 결합도(coupling)

- 결합도: 객체/class 간의 상호 의존 정도
- 응집도: 객체 또는 클래스에 얼마나 관련 있는 책임들을 할당했는지를 나타낸다.

### class와 객체의 관계
class는 공통적인 상태를 가지는 객체들을 추상화한 것
ex. `볼보 xc60`, `Genesis` 등은 객체 -> `Car` class로 추상화할 수 있다.
ex. `Car`, `Motorbike` 등은 -> `Vehicle` interface class로 

### 적절한 객체들에 적절한 책임을 할당
### 각 객체들은 능동성을 가지며 서로 상호작용


## Reference
- [codestates-객치지향 프로그래밍](https://www.codestates.com/blog/content/%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%ED%8A%B9%EC%A7%95)