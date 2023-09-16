---
layout: post
title: Spring Boot (1) | 개발환경 세팅 (Eclipse 등)
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

[친해지자 스프링아(곧 쓸 예정)](/web/2023-06-26-Spring-Basic)

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

## 2. IDE 다운로드: (Eclipse/Intellij)

[Eclipse 다운로드](https://www.eclipse.org/downloads/)

- IntelliJ

## 3. Spring Boot로 프로젝트 생성

[https://start.spring.io/](https://start.spring.io/)

- 뚝딱뚝딱 spring project 바로 만들어준다. (원래는 Spring이 설정할 게 엄청 많다고 함..)
- Spring Boot 3.0 쓰려면 자바 버전이 최소 17이어야 한다.
- 회사는 java 8인가 쓰는데 버전에 괴리가 있긴 하지만,,

![](/assets/img/230626/springboot.PNG)
- thymeleaf(타임리프): html 템플릿 엔진
- zip으로 다운로드 하면 됨!


## 4-1. Eclipse로 프로젝트 열기
- File > Open projects from ... 선택하여
- zip 압축 푼 경로에서 프로젝트 파일 열기

## 4-2. Intellij로 프로젝트 열기
- File > Open 
![](/assets/img/2023-06-26-Spring-Setting/2023-09-16-15-33-56.png)

- gradle: 버전 설정, library 가져오는 역할
- 실행하고 `localhost:8080` 접속하면
![](/assets/img/230626/build.PNG)
- spring boot안에 tomcat (웹서버) 내장 (=tomcat 따로 설치 안해도 된다!)
- 이처럼 페이지 뜨면 완료

## 5. Build 및 실행의 이해 
- 원래 웹 프로젝트 만들고 배포하는 과정을 생각해보면
> 소스코드를 war 파일로 빌드 -> tomcat(was)이 깔려있는 서버로 war파일을 전송하고, 서버에 접속하여 (필요하다면) war 압축을 풀어줍니다. 이때, tomcat이 웹 프로젝트 파일들을 인식할 수 있도록 특정 경로에 풀어야 한다. -> tomcat (재)실행

- 그러나, **spring boot를 사용하면 내장 tomcat이 있기 때문에 jar 파일로 build하여 실행**해주기만 하면 된다.
- java 코드의 compile&run 참고)
  - [compile] `javac ` 명령어를 통해 compile 할 수 있다. (.java -> .class)
  - [run]`java` 명령어를 통해 compile(build) 된 파일을 실행할 수 있다.

- compile vs. build: 컴파일은 단순히 .java 파일을 클래스파일로 변환한 것이고, build는 다양한 리소스(라이브러리 파일 등)를 포함하여 실행가능한 형태로 만드는 과정 (ex. jar, war 등) 으로 이해하고 있다...

![](/assets/img/2023-06-26-Spring-Setting/2023-09-16-17-35-46.png)


## Reference
[Youtube | 스프링 입문 강의(김영한)](https://www.youtube.com/playlist?list=PLumVmq_uRGHgBrimIp2-7MCnoPUskVMnd)