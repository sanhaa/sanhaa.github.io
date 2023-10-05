---
layout: post
title: Spring Boot(2) | 정적/동적 컨텐츠와 MVC패턴 vs. API
description: >
  정적/동적 컨텐츠 이해하는 것도 꽤 오랜 시간이 걸렸는데 정말 산넘어산이구나.
  정적 컨텐츠는 사실 간단하기도 하고 요즘은 특정 목적아니면 필요없고,
  동적 컨텐츠를 제공하는 방식에 1) MVC 패턴 2) API 방식이 있다고 보면 된다.
# sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}


## 1. 정적 컨텐츠
- 클라이언트가 서버에 웹페이지를 요청할 때
- 파일 그대로를 열어서 보여주는 것

### 1-1. Spring boot의 정적컨텐츠 기능
1. 클라이언트: 페이지 요청 
2. 스프링 컨테이너: 해당 페이지와 관련된 컨트롤러 찾기 (정적 페이지니까 컨트롤러 없음)
3. tomcat: 바로 resources 폴더에서 해당 페이지 찾아서 반환

![](/assets/img/2023-09-16-Spring-Boot-2/2023-09-16-17-58-49.png)
출처: 김영한 스프링 입문 강의
{:. figcaption}


## 2. 동적 컨텐츠
- 사용자와의 상호작용, 데이터 내용 등에 따라 웹페이지의 내용이 동적으로 바뀜
 
# 동적 컨텐츠를 제공하는 방법
## 1. MVC
- Model / View / Controller로 쪼개서
- 렌더링이 된 html을 전달해준다.

## 2. API
- HTTP reponse Body에 내용을 반환

![](/assets/img/2023-09-16-Spring-Boot-2/2023-09-16-18-24-30.png)


## Reference
[Youtube | 스프링 입문 강의(김영한)](https://www.youtube.com/playlist?list=PLumVmq_uRGHgBrimIp2-7MCnoPUskVMnd)