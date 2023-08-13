---
layout: post
title: JSP와 servlet
description: >
  도대체 servlet이 무엇이냐.
# sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc}

## Servlet이란

> 웹페이지를 동적으로 생성하는 서버측 프로그램 혹은 그 사양을 말한다.

### 웹페이지를 동적으로 생성하는
- 정적: 정해진 페이지를 제공하는 것
- 동적: client의 요청에 따라 뭔가가 달라짐
- `servlet`을 이용하면 클라이언트의 요청에 따라 그에 대한 결과를 전송할 수 있음

### 서버측 프로그램
- `servlet`은 HTTP 프로토콜 서비스를 지원하는 `javax.servlet.http.HttpServlet` 클래스를 상속받은 클래스
- HTTP 요청/응답을 위한 객체들을(`HttpServletRequest`, `HttpServletResponse`, `HttpServlet`) 제공

### 혹은 그 사양(=spec, 표준, 규칙)
- 자바로 웹 애플리케이션 개발을 할 수 있도록 만들어진 표준 
- 서블릿보다 이후에 나온 jsp 기술도 내부적으로는 servlet을 생성하여 동작하며 
- 요즘에는 MVC 패턴에서 servlet(controller) + JSP (view)로 역할을 구분하여 개발

> **controller(servlet)**: 브라우저 요청에 따라 흐름 제어, 필요한 데이터를 받아서 모델에 넘겨준다. 모델에서 처리된 데이터를 받아서 view로 다시 넘겨줌  
**view(jsp)**: html 코드 중심, 화면에 보여지는 것들


### 특징
- 결국 java class의 일종 (`javax.servlet.http.HttpServlet` 클래스를 상속받은)
- 기본적으로 servlet과 jsp의 역할은 동일하다. servlet 이후 jsp 기술이 등장
- `servlet`은 java 코드 안에 HTML이 포함되어 있다. 
- java thread를 이용하여 동작한다.

<details>  
<summary>servlet 코드 예시</summary>  
<div markdown="1">

```java
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.getWriter().append("Served at: ").append(request.getContextPath());

        // ...

        PrintWriter out = response.getWriter();

        String html = "<html>";
        html += "<head><title>Calculator</title></head>";
        html += "<body><h1>Calculation Result</h1><h3>" + num1 + op + num2 + "=" + result + "</h3></body>";
        html += "</html>";

        out.println(html);
        out.close();

    }
```  
</div>
</details>

## Servlet Container

> 서블릿을 관리해주는 컨테이너

![](/assets/img/2023-07-20-JSP-servlet/2023-07-21-15-32-07.png)

- 클라이언트의 request를 받고 reponse할 수 있도록 웹서버와 소켓으로 통신
- 대표적으로 `톰캣`이 있음. *아니 도대체 tomcat은 정체가 뭐임. 웹서버야 was야 서블릿 컨테이너야*

### Servlet Container 역할

1. 웹서버와의 통신 지원  
우리가 직접 소켓을 만들고 동작하도록 소켓프로그래밍 하지 않아도 됨, API 제공
2. Servlet Life Cycle 관리  
init() -> service() -> destroy() 관리
3. 멀티 쓰레드 지원 및 관리  
4. 선언적인 보안 관리


## 그럼 JSP는 뭔데

> JAVA 코드를 포함하는 HTML 코드

- 파일 형식: `.jsp` 
- html 파일 안에 자바코드는 `<% %>` 태그 안에 들어간다. 혹은 `<%= %>`으로 값 출력 가능
- 서블릿이 복잡해서 JSP가 등장하였다.
- JSP는 WAS에 의하여 서블릿 클래스로(`.java`->`.class`)로 변환하여 사용된다.
- 즉, 서블릿코드 안에서 `out`객체의 `println()`을 사용해서 구현해야하는 번거로움을 jsp를 통해 해결할 수 있다.

```jsp
<h3>결과: <%=num1%> <%=op%> <%=num2%> = <%=result%></h3>
```

## Reference

- [https://m.blog.naver.com/acornedu/221128616501](https://m.blog.naver.com/acornedu/221128616501)
- [https://mangkyu.tistory.com/14](https://mangkyu.tistory.com/14)