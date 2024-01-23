---
layout: post
title: Spring boot + Vue 셋팅
description: >
  spring boot와 vue를 깔았으면 이제 연동할 시간
sitemap: false
hide_last_modified: true
---

## spring과 vue의 연동

1) spring 프로젝트 내부 `static` 폴더로 vue의 build output 디렉토리 셋팅

> 얘는 실제 배포를 위한 설정으로, vue 빌드를 통해 생성된 파일들을 spring boot의
static 폴더에 넣어서 spring 서버 하나만 띄워서 정적파일들만 읽어오도록

- 근데 그럼 궁금한건, 그렇게 미리 build해서 프론트 파일들을 넣어준다 =정적파일 아닌가? spring boot는 동적으로 데이터 view에 넘겨줄텐데, 그게 연동이 잘되나..?


2)`vue.config.js` 파일에 proxy 설정을 통하여 vue 서버로 접속시 spring 서버와 연동됨
> 로컬에서 개발할 때는, vue 서버 띄우고 spring 서버 띄워놓은 다음
vue 서버 접속 주소로 접속하면, spring 서버에서 처리되는 데이터들을 받아올 수 있다.


---

## Reference

- [맛집 지도 만들기(1) - Spring Boot + Vue.js 설치 및 연동하기](https://doozi0316.tistory.com/entry/Vuejs-Spring-Boot-MySQL-MyBatis-%EB%A7%9B%EC%A7%91-%EC%A7%80%EB%8F%84-%EB%A7%8C%EB%93%A4%EA%B8%B01-Spring-Boot-Vuejs-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0)