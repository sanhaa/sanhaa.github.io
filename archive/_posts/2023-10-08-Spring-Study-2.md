---
layout: post
title: Spring 스터디 (2)
description: >
  
sitemap: false
hide_last_modified: true
---

> 23.10.08 스터디


## 학습 계획

|  |   제목        | 설명 및 방식 | 일정   |
|:--------|:---------|:----------|:----------|
| ✅ |  Java의 기본   | (개념정리) Java의 특징 |  23.08 |
| ✅ |  Spring의 기본 | (개념정리) Spring Basic | 23.08 |
|     | Spring Boot 실습 |(실습) 코드로 직접 짜보면서 배우는 스프링부트 프로젝트: [스프링부트입문-김영한](https://www.youtube.com/playlist?list=PLumVmq_uRGHgBrimIp2-7MCnoPUskVMnd) | 23.10 |
|     | Spring 개념 공부 |(개념정리) IoC의 핵심 Bean, DI 이해:  [스프링입문-백기선](https://www.inflearn.com/course/spring#curriculum) | 23.10 |
|     | Spring 개념 공부 |(개념정리) AOP 등등 나머지 스프링 특징들 | 23.10 |
|     | Spring 연관 개념 |(개념정리) servlet과 jsp 등 꼭 알아야 할 연관 개념: [스프링개념-최주호](https://inf.run/ENaN) | 23.11 |
|======|===========|===========|===========|
|      |         |         |     |



## 23.10.08 스터디 목차

## 1. 김영한 - 스프링부트 실습 진도 확인  

- 강의를 얼마나 봤고, 얼마나 이해되었는지.
- 모르는 것들 질문
    - 더 깊이 있는 걸 알고 싶다. 유료 강의 들을 듯!!

## 2. Java 객체지향 프로그래밍 실습

> 일단 Spring을 하려면 Java와 친해져야 하고, 객체지향의 특징을 잘 알아야 한다.

- 객체지향 개념 정리: https://sanhaa.github.io/web/2023-10-08-Java-Basic-2-OOP/


### 객체지향 프로그래밍 실습해보기 

- 실습파일 다운로드 및 실행 확인: https://github.com/sanhaa/oop-practice/tree/release/oop_calculator
- 절차지향으로 `Calculator.java` 안에서 구현하고 실행하기 (Main.java와 testCode)
    - 0으로 나누려고 할 때는 IllegalArgumentException 예외 발생시키기
    - 두 수가 모두 양수인지 검사하기
    

- 객체지향으로 Calculator를 만들기 (템플릿: )
    0. 절차지향/ 객체지향 calculator의 interface 만들고 인터페이스 기준으로 테스트하기 
    1. operator(사칙연산) interface 만들고 AddtionOperator, SubtractionOperator 등의 구현체 만들기
    


## 3. 토이 프로젝트 (11월 ~ )

- `슬기로운 독서생활` 프로젝트 간략 리뷰 + 의견/질문이 있다면?
- 각자가 주제를 정해보면 좋을듯?! (기본 예제: todo list, 게시판)

- 창업프로젝트 != 토이 프로젝트 (spring, vuejs, react --> 배움 | 창의적인 아이디어) --> 고도화 | 리팩토링 | 기술 전환
- 이미 있는 것 + 창의적/독창적 기능
- 시작 ~~ 수익 창출까지 (광고 등)
- 실제로 누군가가 사용할 수 있는 사이트였으면 좋겠다!!
- 주제 + 요구사항
- 공대생과 책 ㅋㅋㅋㅋ

## 프로젝트 진행 및 스터디 계획

- 10월: 김영한씨 spring 강의 + spring 이론 개념 
- 11월: 요구사항 정의서/명세서, 타겟층 --> 역할 분담
- 11월 ~ 1월: 개발
- 1월~: 런칭
- 잘되면 앱버전 출시 + 퇴사


## 웹 개발 기술 히스토리

html > servlet > jsp > spring(MVC)



## Component Scan과 bean? 의존성 주입이란??

> 일단, bean의 개념을 알아야 하고, DI(의존성 주입)과 annotation의 개념을 분리해야 한다.