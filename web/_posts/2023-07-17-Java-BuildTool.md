---
layout: post
title: Java | Build Tool (Ant, Maven, Gradle)  
description: >
  나중에 써야징...
# sitemap: false
hide_last_modified: false
---

- Table of Contents
{:toc}

## Build Tool
빌드 도구란 **코드를 컴파일 -> 빌드하여 실행가능한 형태로 만들어주는 것을 편리하게** 해주는 도구
- 자바 라이브러리들 (lib 폴더 하위 jar 파일 등) 추가와 버전 동기화를 편하게 해줌
- 

## 역사
1. 1세대 Make
빌드의 개념을 확립, `Makefile`을 작성하여 build 순서/과정을 기술할 수 있다.
Cmake 많이 했던 기억이 난다.
makefile의 기본 패턴은 아래와 같다.
```makefile

CC=<컴파일러>
CFLAGS=<컴파일 옵션>
LDFLAGS=<링크 옵션>
LDLIBS=<링크 라이브러리 목록>
OBJS=<Object 파일 목록>
TARGET=<빌드 대상 이름>
 
all: $(TARGET)
 
clean:
    rm -f *.o
    rm -f $(TARGET)
 
$(TARGET): $(OBJS)
$(CC) -o $@ $(OBJS)
```

2. 2세대 Ant
크로스 플랫폼에 대응하여 범용성을 높인 빌드도구이다.  
특히 **Java**는 다양한 플랫폼에서 동작할 수 있었기 때문에, Java+XML 기술을 도입한 Ant 빌드도구를 활용하여 make의 문제점이었던 **플랫폼 의존 문제를 해결**할 수 있었다. 
간단하고 사용하기 십지만, 빌드 스크립트가 길어지는 경우가 많았고, 라이브러리 의존 관계를 관리하기엔 어려웠다.
`build.xml` 파일에 빌드 스크립트를 작성한다.

3. 3세대 Maven
규칙을 기반으로 빌드 스크립트 작성이 편해졌다. <-- **빌드 생명 주기와 프로젝트 객체모델(POM) 개념**을 도입하였다.  
`pom.xml`: 라이브러리 의존관계를 자동으로 관리해준다. 메이븐 중앙 저장소를 제공하여 의존 라이브러리를 관리할 수 있다. = 네트워크 연결해서 연관 라이브러리를 같이 업데이트 해줌
`web.xml`: Java web application에 대한 내용, 설정/변경 방식을 정의한 파일

4. 4세대 Gradle
스크립트 언어로 회귀하여 유연성을 증대시켰다. = JVM위에서 동작하는 Groovy 언어로 작성 
maven의 xml형태보다 가독성이 우수하며 빠르다.
기존 maven 빌드도구와 호환이 가능하다.
Configuration Injection 방식
`build.gradle` 에 설정


## 이클립스의 Dynamic Web Project
이클립스 프로젝트 > intellij로 전환 시
eclipse / maven / gradle 중 하나를 고르게 되어있는데, 그럼 eclipse는 어떻게 빌드를 해주는 걸까? 싶어서... 
회사 프로젝트는 빌드 도구를 뭐를 쓰고 있는지 전혀 파악이 안되고,, intellij로 돌리니까 gradle이든 maven이든 ant든 아무거나로 다 빌드할 수 있는듯 하여?


## Reference
- [빌드도구 mave, gradle](https://wangmin.tistory.com/50)
- [Gradle에 대하여](https://velog.io/@hanblueblue/%EA%B8%B0%EC%B4%88-%EC%A7%80%EC%8B%9D-%EB%8B%A4%EC%A7%80%EA%B8%B0-2.-Gradle)