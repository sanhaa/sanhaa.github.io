---
layout: post
title: Github Pages 블로그 (1) - hydejack 테마 적용하고 실행하기
description: >
  github pages와 jekyll 이용해서 블로그 만들기, hydejack 테마 사용하기
sitemap: false
hide_last_modified: true
---

예전에 만들다가 말았던 기술 블로그를 다시 만들어 보기로 했다.  
일단 ruby, bundler 다 세팅된 상태 ~~(여튼 로컬에서도 띄워봐야 하므로,, 대충 ruby 깔았음)~~

[jekyll 환경설정(ruby, jekyll 설치)](https://github.com/sanhaa/Study/blob/main/Jekyll.md)

`github pages`: 깃헙이 제공하는 기능, 정적 웹사이트 호스팅  
`jekyll`: 정적 사이트 생성기

> 그니까 네이버 블로그나 티스토리 말고 진짜 자신의 블로그 사이트를 만들어서 운영하고 싶을 때,  
*jekyll*을 이용하면 페이지 구조를 짜거나 DB 구축할 필요 없이 기본 blog 형태의 사이트를 편하게 만들 수 있고  
*github pages*를 이용하면 무료 웹 호스팅 가능



## Jekyll 테마 고르기

아래 사이트에서 다양한 테마 중에 마음에 드는 것을 골라보자.  

- [지킬 테마 모음](http://jekyllthemes.org/)
- 데모 페이지도 볼 수 있다.
- 마음에 드는 걸 골랐으면 해당 테마의 git 레포지토리를 들어가서
- fork 하거나 download 해서 테마 사용


### 내가 고른 테마

[hydejack 테마(v9)](https://hydejack.com/)

![](https://hydejack.com/assets/img/blog/hydejack-9.jpg)

예쁘죠
{:.figcaption}


**선정 기준**
- 반응형
- 왼쪽 사이드 바에 메뉴, 오른쪽에 글이 나오는 구성을 원해서
- documentation이 잘 되어 있어서 custom 하기 편함

## 내 레포지토리에 테마 가져오기 + 레포 이름 설정

1. fork 해서 가져온 경우 (편하다)
  - repository 이름만 잘 바꿔주자: `<username>.github.io`
2. 테마를 다운로드 한 경우
  - 압축을 풀고, git init하고 remote 저장소 설정해주기
  - 마찬가지로 repository 이름 설정: `<username>.github.io`

![](/assets/img/220927/git-repo.png "git repo")
레포 이름 잘 확인하기
{:.figcaption}


## Github Pages 호스팅을 위해 설정할 것들 

hydejack 테마 예전 버전에서는 상관 없었는데, 최신 버전(현재 버전 9)부터는 뭔가 기능이 많아져서 그런지 이대로 레포를 생성하면 github pages가 제대로 호스팅을 못한다. 

![](/assets/img/220927/gp-error.PNG)

build jekyll 명령어에서 계속 에러남
{:.figcaption}

[이 테마의 설명서](https://hydejack.com/docs/install/#github-pages)을 보니까 설정해야 할 게 좀 있었다.

~~~yml
# file: "_config.yml"
remote_theme: hydecorp/hydejack@v9.1.6

# ...

plugins:
  - jekyll-include-cache
~~~


이렇게 설명서에 나오는 대로 설정을 해주면 제대로 된다.

![](/assets/img/220927/gp-success.png)


## Github Pages와 로컬에서 모두 실행하려면

일단 위에처럼 설정을 추가해주면 github pages로 호스팅이 제대로 될텐데, 파일을 수정할 때마다 github에 push 하고 반영될 때까지 기다리는 건 비효율적이니까 로컬에서 실행할 수 있게 설정해보자.

Gemfile을 다음과 같이 수정하고

~~~ruby
# file: "Gemfile"
gem "github-pages", group: :jekyll_plugins
gem "jekyll-include-cache", group: :jekyll_plugins
~~~

프로젝트의 루트 디렉토리에서 아래 명령어 실행
~~~ruby
bundler install
bundler exec jekyll serve
~~~

![](/assets/img/220927/bundler-exec.jpg)

server running 나오는지 확인
{:.figcaption}

+ http://127.0.0.1:4000 에서 확인
+ 텍스트, 사진은 변경될 때마다 새로고침하면 바로 반영됨
+ 카테고리 추가 등은 껐다 켜야 반영

## bundler install 중 에러 해결

![](/assets/img/220927/bundler-error.jpg)  

bundler install 실행시 에러
{:.figcaption}

나는 위와 같은 에러가 났는데, github-pages에서 사용하는 jekyll과 테마 혹은 로컬에서 사용하려는 jekyll 버전이 안 맞는 것 같았다.
dependency 에러 해결법을 검색해봤더니, 그냥 downgrade 하라고 해서

github-pages가 지원하는 최신 jekyll 버전을 검색해봤다. [github-pages dependency 문서](
https://pages.github.com/versions/)

![](/assets/img/220927/gp-dep.jpg)

3.9.2까지 지원
{:.figcaption}

~~~ruby
#file: "Gemfile"
gem "jekyll", "~> 3.9"
~~~
Gemfile에서 지킬 버전을 3.9로 수정하니 해결
{:.figcaption}


## 커스터마이징

기본적인 커스터마이징을 위해 파일 `_config.yml`을 열어보자.

원래는 가장 상단의 url을 변경해줘야 하는 걸로 아는데, 주석을 보니까 Github pages를 사용할 경우 필요 없다고 되어 있다.

일단 아래 부분만 변경하고 확인해보자.
- 타이틀
- 태그라인
- 로고 이미지
- 배경 이미지

~~~yml
# file: "_config.yml"
# Uncomment and set the URL of your site (with protocol, e.g. `https://`)
# NOTE: You don't need to provide this property when hosting on GitHub Pages or Netlify.
url:                   'https://sanhaa.github.io' # 주석 읽어보면 안해도 되는데 그냥 함

# The title of your blog. Used in the sidebar and the browser tab.
title:                 devlog by mming

# ...

# A shorter description for the sidebar.
tagline:               2022~

# A (square) logo for your site.
# If provided, it will be shown at the top of the sidebar.
# It also used by the `jekyll-seo-tag` plugin.
logo:                  /assets/img/my-logo0.jpg

# ...
# Sidebar image and theme color of the site.
accent_image:          /assets/img/sidebar-bg1.jpg
accent_color:          rgb(79,177,186)
~~~


![](/assets/img/2022-09-27-jekyll-blog/2024-01-23-22-50-58.png)

잘 반영된 모습, 사진은 직접 찍은 건데 잘 어울려서 기분 좋다. mming은 그냥 단어가 귀여워서 ㅎ
{:.figcaption}

> 카테고리 추가 방법은 다음 포스트로... (내가 부지런 하다면요.. )

----
## Reference
- [깃허브 블로그 만들기](https://velog.io/@shg4821/%EA%B9%83%ED%97%88%EB%B8%8C-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-1)

