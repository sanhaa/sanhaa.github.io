---
layout: post
title: Spring Boot(3) | 의존성 주입
description: >

# sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}


## DI 방식 세 가지
1. 필드 주입
2. setter 주입
3. 생성자 주입 
```java
    @Autowired
    public MemberController(MemberService memberService){
        // Autowired 어노테이션을 통해
        // spring container 가 관리하는 controller, memberService bean을 연결해줌
        this.memberService = memberService;
    }
```

> 의존관계가 실행중에 동적으로 변하는 경우는 거의 없으므로 생성자 주입을 권장한다.

## @Autowired 에 대해 알아보자

스프링 컨테이너에 올라가는 것들(=스프링이 관리한다)만 `@Autowired`가 동작하고
스프링 빈으로 등록하지 않고 직접 생성한 객체에서는 동작하지 않음


## Reference
[Youtube | 스프링 입문 강의(김영한)](https://www.youtube.com/playlist?list=PLumVmq_uRGHgBrimIp2-7MCnoPUskVMnd)