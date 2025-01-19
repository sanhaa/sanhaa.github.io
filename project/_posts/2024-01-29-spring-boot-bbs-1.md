---
layout: post
title: Spring Boot | Simple BBS project(1) 스프링부트의 in-memory DB란
description: >
  spring boot는 내장되어 있는 게 너무 많아. JPA도 공부해야할 게 너무 많고.
  이렇게 모르는 거 나올 때마다 정리하면 영원히 못끝내겠는걸? ㅎ-ㅎ 
sitemap: false
hide_last_modified: true
---


## 스프링부트 in-memory DB로 H2를 쓴다? 

## 그래서 다시, JPA 가 뭔지

## JPA Entity


## JPA Entity의 equals & hashCode

### 좋은 글들  
- 일단 알아야 하는 개념: [JPA 영속성 컨텍스트](https://velog.io/@neptunes032/JPA-%EC%98%81%EC%86%8D%EC%84%B1-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8%EB%9E%80) 
-  [JPA-Entity의-equals와-hashCode](https://velog.io/@park2348190/JPA-Entity%EC%9D%98-equals%EC%99%80-hashCode)
- [equals와 hashCode 깊은 내용](https://velog.io/@nmrhtn7898/JPA-Entity%EC%97%90%EC%84%9C-equals-hashcode-%EC%82%AC%EC%9A%A9%EC%8B%9C-%EB%B0%9C%EC%83%9D%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EB%AC%B8%EC%A0%9C%EC%A0%90)


- 기본 개념으로 `영속`이란: JPA entity가 db record로 저장된 것(insert)

- 일단, 기본 java객체의 동일성과 JPA entity 동일성 (같은 객체인지를 말하는 것) 판단이 조금 다르다.

- 어쨌든 JPA entity는 DB의 레코드와 가깝기 때문에 `eqauls` , `hashCode` 메서드를 재정의하여
같은 entity(즉 같은 record) 인지 보장되도록 컨트롤하는 느낌쓰,, 


## what is factory method



---

## Reference

- 