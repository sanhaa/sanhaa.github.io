---
layout: post
title: Spring | 개발환경 세팅 (Eclipse 등)
description: >
  java 좋아하는 언어는 아니었지만 이제 java로 웹개발 해야한다...
  진짜 이제 친해져야 해 :)
# sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}


## 0. Spring이란?
겨울이 지나고 봄이 오긴 뭘 ㅠㅠ
도대체 왜쓰나요 스프링

[친해지자 스프링아(곧 쓸 예정)](/web/_posts/2023-06-26-Spring-Basic.md)

## 1. Java 다운로드
일단 Spring이든 뭐든 Java로 웹 개발 해야하므로 
Java 다운로드 해야한다.

근데 난 이미 깔려있으니 pass

~~~cmd
> java -version

java version "17.0.1" 2021-10-19 LTS
Java(TM) SE Runtime Environment (build 17.0.1+12-LTS-39)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.1+12-LTS-39, mixed mode, sharing)
~~~

## 2. Eclipse 다운로드

[Eclipse 다운로드](https://www.eclipse.org/downloads/)

- IntelliJ 쓰고 싶은데 일단 회사에서 eclipse 쓰니까... 

## 3. Spring Boot로 프로젝트 생성

[https://start.spring.io/](https://start.spring.io/)

- 뚝딱뚝딱 spring project 바로 만들어준다. (원래는 Spring이 설정할 게 엄청 많다고 함..)
- Spring Boot 3.0 쓰려면 자바 버전이 최소 17이어야 한다.
- 회사는 java 8인가 쓰는데 버전에 괴리가 있긴 하지만,,

![](/assets/img/230626/springboot.png)

- zip으로 다운로드 하면 됨!


## 4. Eclipse로 프로젝트 열기
- File > Open projects from ... 선택하여
- zip 압축 푼 경로에서 프로젝트 파일 열기


- gradle: 버전 설정, library 가져오는 역할
- 실행하고 `localhost:8080` 접속하면
![](/assets/img/220626/build.png)
- spring 안에 tomcat (웹서버) 내장 (=tomcat 따로 설치 안해도 된당~~)
- 이처럼 페이지 뜨면 완료

## Reference
[Youtube | 스프링 입문 강의(김영한)](https://www.youtube.com/playlist?list=PLumVmq_uRGHgBrimIp2-7MCnoPUskVMnd)