---
layout: post
title: Spring | 스프링 이해하기
description: >
  개념 정리보다는 내가 이해한 것과 궁금한 것 정리
# sitemap: false
hide_last_modified: false
---

- Table of Contents
{:toc .large-only}

## Spring 프레임워크란?
**Java 웹 개발을 도와주는 프레임워크** 이다.  
개발을 위한 일종의 뼈대를 제공해주며, 아래와 같은 **특징**을 갖는다. 

더욱 상세한 설명은 [여기](https://www.codestates.com/blog/content/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8)에 엄청 쉽게 나와있다.

### POJO 프로그래밍을 지향
```
Plain Old Java Object
```
순수 java만을 통해 객체를 만드는 것을 지향하여, 특정 기술이나 환경에 종속되지 않고
변화와 확장에 대처할 수 있다.

### IoC / DI
```
IoC = Inversion of Control (제어의 역전)
DI = Dependency Injection (의존성 주입)
```

Java는 객체 지향 언어로, 객체와 객체들간의 관계를 잘 정의하는 것이 무엇보다 중요하다.  
특히 객체들 간의 **의존성**이 자주 논의되는데, 이는 하나의 객체가 바뀌면 그 객체와 관련된, 그 객체에 의존하는 다른 객체의 코드도 수정해야하기 때문이다. 이렇게 코드의 유지보수 측면에서 객체들 간의 의존성을 관리하는 것이 필요하다.

A 인스턴스가 B 인스턴스의 메서드를 호출하고 있다면 "A가 B에 의존하는 관계"라고 표현할 수 있다.  
이때 더이상 B 인스턴스를 사용하지 않고 C 인스턴스를 사용하게 되었다면 B에 의존하고 있던 A의 내부 코드를 변경하는 것이 필요하다.
B에 의존하고 있던, 그러니까 B의 메서드를 호출하는 인스턴스가 A 하나 뿐만이 아니라 여러개라면
그 모든 인스턴스들의 코드를 변경하는 것이 필요하다. (B대신 C의 메서드를 호출하도록)

이때 중간에 **인터페이스**라는 층을 하나 더 추가하여 해결할 수 있다.
1. A 인스턴스가 사용하는 메서드(`example()`)를 인터페이스 I의 추상 메서드로 정의 한다.
2. 객체 B 또는 C에 `example()` 메서드를 구현한다. `Class B implements I{}`
3. A 인스턴스에서 B나 C 객체를 스스로 생성하지 않고, 인터페이스를 선언한 후 `private I i;`
4. 생성자를 통해 외부로부터 인스턴스를 받아오게 한다. `public A(I i) {this.i=i;}`

**개발자가 의존/종속 관계를 관리하는 것이 아니라 스프링 프레임워크가 해준다. = IoC, 제어의 역전**  
**스프링이 A의 생성자(인터페이스 받아오는 부분)를 통해 C와 의존성이 생기도록 한다 = DI, 의존성 주입**  

### AOP (Aspect Oriented Programming, 관심지향 프로그래밍)

코드의 중복을 해결하기 위해 공통 부분(기능)을 비즈니스 로직으로부터 분리한다.

### MVC 패턴(Model2)

자바 기반 웹앱 개발에 사용되는 아키텍쳐에는 model1과 model2가 있는데, MVC하면 보통 model2를 지칭

![](/assets/img/2023-06-26-Spring-Basic/2023-07-18-11-25-11.png)

![](/assets/img/2023-06-26-Spring-Basic/2023-07-18-11-35-06.png)

- `model`: 데이터처리를 담당하며 service영역(비즈니스 로직)과 DAO영역(DB접근 객체)으로 나누어짐. `view`와 `contorller`에 대한 정보를 가지고 있지 않아야 한다.

- `view`: 사용자에게 보여지는 부분으로, `controller`에게 받은 결과를 시각화한다.
`model`의 정보를 저장해서는 안되며, `model`, `controller`의 구성요소 모르고 어떤 `contoller`를 호출하는지만 알고 있다.

- `controller`: view에서 받은 요청을 가공하여 model에 전달, model로부터 받은 결과를 view로 넘겨준다. 모든 요청 에러, 모델 에러는 여기서 처리한다.


### Java bean은 뭐고 DAO는 뭘까

---

## Spring Framework의 구조

스프링 프레임워크는 모듈화? 되어있다.
통짜가 하니라, 기본적인 spring core + 상황에 따라 조합하여 사용할 수 있도록 구성되었다고.

![](/assets/img/2023-06-26-Spring-Basic/2023-07-18-11-32-59.png)


## Reference
- [스프링 개념과 특징 설명](https://www.codestates.com/blog/content/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8)
- [java implements](https://velog.io/@hkoo9329/%EC%9E%90%EB%B0%94-extends-implements-%EC%B0%A8%EC%9D%B4)
- [Spring Framework의 구조](https://khj93.tistory.com/entry/Spring-Spring-Framework%EB%9E%80-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-%ED%95%B5%EC%8B%AC-%EC%A0%95%EB%A6%AC)
- [Spring MVC](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.boostcourse.org%2Fweb326%2Flecture%2F58979%3FisDesc%3Dfalse&psig=AOvVaw2IIvHLt8-3sup-l-ndEwzW&ust=1689732303531000&source=images&cd=vfe&opi=89978449&ved=0CBMQjhxqFwoTCIjJzL-Xl4ADFQAAAAAdAAAAABAE)