---
layout: post
title: Java | 자바의 기본 
description: >
  1학년 땐 java 참 좋아했는데,,, 객체 설계하고 상속하는 게 참 재밌었는데
  자바에 대해 자세히 모르고 앱개발 하게 되면서 이게 왜 안되지? 왜 되지? 의 답답함만 증폭됨..
# sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc}


## 0. Java란 
- 1995년 발표된 객체 지향적 프로그래밍 언어
- 현재는 웹 애플리케이션과 모바일 앱 개발에 가장 많이 사용됨
- 특히 한국에서는 [전자정부프레임워크](https://www.egovframe.go.kr/home/sub.do?menuNo=9)가 spring 기반이므로, java와 spring을 잘 아는 것은 국내 sw개발할거면 많은 도움이 되겠죠...


## 1. 프로그래밍 언어로써 Java의 특징
**1) 객체지향 언어**  

**2) 인터프리터 언어**   
  - 자바는 컴파일 언어인 동시에 인터프리터 언어이다.  
  - 텍스트 소스를 컴파일하여 클래스파일로 만든 다음 자바 런타임이 클래스 파일을 인터프리트 하면서 실행된다.

**3) 독립적인 플랫폼**
  - JVM(자바가상머신)에서 실행되므로 운영체제 상관없이 어디서든 독립적으로 사용 가능

**4) 자동 메모리 관리**
  - 개발자가 메모리에 직접 접근할 수 없으며 자바가 직접 관리
  - GC(Garbge Collector) 등등이 메모리 관리 역할을 한다. --> `jvm`이 수행
  - C/C++에서는 직접 메모리에 접근하여 동적할당하고,, stack 터트리고 그랬지만.. 자바에서는 그럴 필요 없다.

**5) 멀티 쓰레딩 지원**
  - 하나의 프로그램 단위가 동일한 쓰레드를 동시에 수행할 수 있다.

**6) 동적이다.**
  - 객체 간의 상호작용을 정의하기 때문에 필요하지 않는 객체는 생성되지 않고 필요한 객체만 생성하여 사용

**7) 안전하고 강력**
  - 4.의 특징과 관련하여 시스템 붕괴 우려가 적다.
  - 유형(type) 정의가 강해서 실행 전 검사 가능


## 3. JVM은 무엇인가?
```
Java Virtual Machine
```
- Java는 자바 가상머신(JVM) 위에서 컴파일/실행 된다. --> OS에 독립적인 특징을 가짐
- JVM은 OS에 종속받지 않고 CPU가 Java를 인식, 실행할 수 있게 하는 가상 컴퓨터

![](/assets/img/2023-07-17-16-31-17.png)


- 우리가 짠 Java 코드(.java)는 `Java Compiler`에 의해 Java bytecode(.class)로 변환된다.
- `Java Compiler`는 `jdk > bin > javac.exe`를 의미한다.
- 그 이후, `JVM`이 bytecode를 해석하여 OS가 이해할 수 있도록 한다.
- `jdk > bin > java.exe`는 jvm을 구동시키기 위한 명령 프로그램이다. (JRE)


### JVM 구성요소

![](/assets/img/2023-07-17-16-43-42.png)

## 4. jre와 jdk 차이

### JRE: 실행만 할 때
`Java Runtime Environment`로, 
JVM + 자바 클래스 라이브러리 드응로 구성되어 있다.
(이미)컴파일 된 Java 프로그램을 실행하는데 필요한 패키지

### JDK: 개발, 실행할 때
'Java Development Kit`로,
Java를 활용해 개발, 실행하기 위한 기능을 갖춘 Java용 SDK이다.
JDK는 JRE + Javac, jdb, javadoc 같은 도구도 있다.
java 프로그램을 생성, 컴파일, 실행할 수 있음

![](/assets/img/2023-07-17-16-37-54.png)

1.컴파일환경과 2.실행환경(jre)
{:.figcaption}

```bash
# 1. 컴파일
javac hello.java # hello.class 파일 생성됨

# 2. 실행
java hello # hello.class 파일을 의미
```


## 5. 그 외

### build vs. run
- `build` = compile + 그 외 작업(리소스 파일 등) 하나의 war 파일로 변환(압축)하는 과정
- `run` = build + 실행

### Build Tool (Ant, Maven, Gradle)

[Build Tool에 대해서](/web/2023-07-17-Java-BuildTool)

### war와 jar

[war와 jar 등 자바관련 파일 종류](/web/2023-07-17-war-jar)


### Package와 Class와 Java파일
내가 java를 싫어하기 시작했던 건, 패키지와 클래스들이 왜 있는지 거슬렸음에도 알아보려고 하지 않았을 때부턴 것 같다. 

뿐만 아니라, java는 또 jre니 jdk니 환경변수도 설정해줘야 했으니... 알아야할 건 많은데 일단 코드를 짜기에 급급해서 그런 기본들은 모르고 넘겼던 것 같다.

`package`는 class의 대분류이다.
객체지향 언어 java로 개발 시 다양한 class를 생성하게 되는데, 이때 관리의 용이성을 위하여
package를 통해 비슷한 class를 묶어서 계층적으로 관리한다.

`.class` 파일은 `.java`파일을 컴파일할 경우 컴파일러가 자동으로 생성해주는 파일이다.
실제 class의 정의는 `.java`에 기술됨.

자세한 건: [war와 jar 등 자바관련 파일 종류](/web/2023-07-17-war-jar)


### Java 설치할 때 왜 환경변수를 설정해줘야 하는 걸까?


## Reference
- [Java의 특징](https://s-bug.tistory.com/57)
- [JVM이란](https://doozi0316.tistory.com/entry/1%EC%A3%BC%EC%B0%A8-JVM%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B8%EA%B0%80)
- [Java 컴파일 과정](https://gyoogle.dev/blog/computer-language/Java/%EC%BB%B4%ED%8C%8C%EC%9D%BC%20%EA%B3%BC%EC%A0%95.html)
- [build와 run](https://bol-bbang.tistory.com/4)
- [java package](https://wikidocs.net/231)