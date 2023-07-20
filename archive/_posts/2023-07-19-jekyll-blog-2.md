---
layout: post 
title: Github Pages + Jekyll 블로그 (2) - jekyll 테마 custom, includes 파일 만들기
description: >
    여러 커스텀을 하고 싶은데, 그러기 위해서는 jekyll의 구조를 좀 알아야 할 것 같다.
    구조를 알아보면서 내가 만들고 싶은 series 컴포넌트를 만들어보자.
sitemap: false
hide_last_modified: true
---

{% include series-list.html %}

series link 컴포넌트를 만들기 위하여, 내가 사용하는 jekyll 테마를 분석할 필요가 있다.
어떻게 마크다운 파일이 html로 바뀌는지를 알아야 컴포넌트를 커스터마이징할 수 있을테니!

**목표:** 각 post의 상단에 다른 게시물로 바로 갈 수 있는 링크 목록을 넣어줄 수 있도록
series 컴포넌트 만들기
{:.message}

jekyll에 `collections`을 어떻게 잘 이용하면 되지 않을까? 싶으면서도, 일단은 직접 만들어보자...

일단, liquid라는 언어에 대해 조금은 알아야 한다.

## 템플릿 언어 Liquid

jekyll 프로젝트 파일들을 기웃거리다 보면 궁금했던 코드가 있는데 `liquid` 라네요.

jekyll 한국어 블로그[단계별 튜토리얼-liquid](https://jekyllrb-ko.github.io/docs/step-by-step/02-liquid/)에 설명이 아주 잘 나와있다.   
~~한국어 번역해놓은 레포가 있는데,, 번역 안된거 나도 기여하고 싶은데 20년도 하반기 이후로는 왜 pr을 안받으시는지?~~

*아래에도 정리했었는데, 포스트 길이만 늘리는 것 같아서 다 삭제했다. 위의 튜토리얼에 너무 잘 나와있으니 기억안나면 링크를 참고해야겠다.*


## markdown이 어떻게 html로 바뀌는 건지!
jekyll은 md파일의 내용을 어떻게 html에 적용하는 걸까. 

### layout 생성하기
먼저 레이아웃 (템플릿) 파일을 생성하자.  

~~근데 왜난 _layouts 폴더가 없는걸까...? 일단 폴더 생성해보자~~

``` html
<!-- file: "_layouts/test.html" -->
{% raw %}
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>
{% endraw %}
```

참고로 liquid 구문을 markdown에 넣을 때는
코드블럭으로 감싸도 text가 아닌 liquid로 컴파일 되기 때문에
앞뒤로 태그를 감싸주어야 한다. 아래와 같이.

![](/assets/img/2023-07-19-jekyll-blog-2/2023-07-19-12-00-55.png)


### 페이지 markdown 파일 생성

우리가 만들어둔 test 레이아웃을 사용할 markdown 파일을 만들어보자.
레이아웃에 들어가는 내용을 markdown 언어를 이용해서 적어준다고 이해했다.

아래와 같이 머릿글과 

```markdown
<!-- file: "/test.md" -->
{% raw %}---
layout: test
title: title 입니다 ?
---

<h1>{{ page.title }}</h1>

# Test page

테스트 페이지인데요.{% endraw %}
```

우리가 만들어둔 test.html 레이아웃을 사용하자는 의미로
머리말에 `layout: test` 를 적어준다.

![](/assets/img/2023-07-19-jekyll-blog-2/2023-07-19-12-12-13.png)

지금은 layout 파일에 별 게 없지만 차차...

---

## 조각파일(includes) 활용하여 공통 부분 만들기 
include 태그를 사용하면 `_includes` 폴더에 저장된 조각파일의 내용을 포함시킬 수 있다고 한다.
사이트 여러곳에 반복되는 코드를 한 곳에서 관리하기 위해.
그러니까, react나 vue의 component와 비슷한 역할이겠지!! 나에게 필요한 것이군.

자세한 사용법은 [include 튜토리얼](https://jekyllrb-ko.github.io/docs/step-by-step/05-includes/) 여기서 보도록 하자. ㅎㅎ

일단 나는 간단히 아래와 같이 `includes` 파일을 만들어 주었다.

```html
<!--/_includes/series-list.html -->
<h3>연관 포스트 보기</h3>
<ul>
    <li><a href="/archive/2022-09-27-jekyll-blog-1">Github Pages + Jekyll 블로그 (1) - hydejack 테마 적용하고 실행하기</a></li>
    <li><a href="/archive/2023-07-19-jekyll-blog-2">Github Pages + Jekyll 블로그 (2) - jekyll 테마 custom, includes 파일 만들기</a></li>
</ul>
<br>
```

필요한 post 마크다운 파일에 원하는 위치에 추가했을 때 잘 나오는지 보자.
```markdown
---
layout: post
title: Github Pages + Jekyll 블로그 (1) - hydejack 테마 적용하고 실행하기
description: >
  github pages와 jekyll 이용해서 블로그 만들기, hydejack 테마 사용하기
sitemap: false
hide_last_modified: true
---

{% raw %} {% include series-list.html %} {% endraw %}

// ...
```
머리글 바로 밑에, post 가장 상단에 나올 수 있게 첫줄에 추가했다.

![](/assets/img/2023-07-19-jekyll-blog-2/2023-07-19-14-49-26.png)
원하는대로 잘 나오고 링크도 잘 걸려있다!!!
{:.figcation}

## data 이용하여 변수로 관리하기
하지만 당연히 저건 제대로 된 컴포넌트라 할 수 없다. 링크와 post 제목이 직접 들어가있기 때문.

`_data` 폴더에 `yml` 파일을 만들어 변수를 관리할 수 있다.

```yml
# file: /_data/series-list.yml

# post series list 생성을 위한 변수 관리
- name : Github Pages + Jekyll 블로그 (1) - hydejack 테마 적용하고 실행하기
  link : /archive/2022-09-27-jekyll-blog-1/

- name : Github Pages + Jekyll 블로그 (2) - jekyll 테마 custom, includes 파일 만들기
  link : /archive/2023-07-19-jekyll-blog-2/
```
그리고 반복문을 통해 여러 post의 정보를 가져올 수 있도록 아래처럼 코드를 작성한다.
뿐만 아니라, 현재 페이지를 연한 회색으로 표시해주도록 한다.
![](/assets/img/2023-07-19-jekyll-blog-2/2023-07-19-15-08-01.png)

![](/assets/img/2023-07-19-jekyll-blog-2/2023-07-20-16-34-30.png)
실제 블로그에 나타나는 모습
{:. figcation}


근데 이제 문제는, 시리즈 추가는 어떻게 처리할 것인지...!!
나름 includes 파일을 만들어놨는데 다양한 시리즈 별로 어떻게 활용할 수 있을지..
`collections` 구조 참고해서 고쳐봐야지 (다음편에서!) 

----
## Reference
- [jekyll 디레토리 구조](https://jekyllrb-ko.github.io/docs/structure/)
