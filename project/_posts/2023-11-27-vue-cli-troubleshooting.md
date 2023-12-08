---
layout: post
title: vue-cli 설치 오류는 아니고 vue create 안될 떄
description: >
  vue-cli를 설치해도 vue 명령어가 안될 때
sitemap: false
hide_last_modified: true
---

vue.js 개발 환경 설정 별 거 없다.

1. node 설치
2. npm으로 vue-cli 설치
3. vue create [프로젝트명]

끝인데

아무리 `vue-cli` 를 설치해도 설치가 안되는건지

```
vue -v 
```

하면 못알아먹는 거야!!!!!

정확한 에러(?) 내용은 따로 없고
![](/assets/img/2023-11-27-example-content/2023-12-09-00-19-52.png)

그냥 명령어를 못찾는다 = 설치가 안됐냐? 
npm 설치 패키지 조회하면 그건 또 아님.


### 흠 일단, vue.cmd 로 실행해보세요

vue-cli 의 버전에 따라 
```
vue.cmd -v
vue.cmd create project
```

이렇게 하면 된다는 사람도 있는데 
전 해결이 안됐고요

### 아 intellij terminal 문제인가?

싶어서 vscode terminal 로 해봤는데도 똑같은 에러 

### vscode terminal - power shell
![](/assets/img/2023-11-27-example-content/2023-12-09-00-22-12.png)


### vscode terminal - wsl
![](/assets/img/2023-11-27-example-content/2023-12-09-00-22-54.png)

이전에 깔아놓은 wsl
내가 뭐 하다가 좀 맛탱이가 간 거 같아서,, 쓰고 있진 않았는데
어쨌든 얘도 똑같이 별다른 에러 없이 명령어를 못찾네요


### windows terminal - powershell
내가 좋아하는 windows terminal 열어서 powershell 열었더니 얘는 또 다른 에러 메세지가 나온다.
보안 오류라네
![](/assets/img/2023-11-27-example-content/2023-12-09-00-25-03.png)

아니 그럼, 보안오류 때문에 ide 내부 terminal 에서 `vue-cli` 실행이 안됐던 건가??
맞다면 ide terminal 은 처음부터 왜 이 오류를 못뱉은걸까요 ,,,

근데 또 아래 재밌는 게 있어서 이거 먼저 해보기로 함


### windows terminal - ubuntu
마찬가지로 안되는데, 참 흥미롭다.

![](/assets/img/2023-11-27-example-content/2023-12-09-00-27-30.png)


1) wsl에서 확인한 node 버전이 내가 설치한 것과 다르다. (왜지 도대체)
2) `powershell` 과는 또다른 에러


~~아니? 사실 흥미롭지 않고 열받아~~

## wsl 에 node 재설치

> 아, 일단 장기적으로는 wsl 을 사용하고 싶으니 wsl 에 node를 재설치하자.

뭔가가 꼬일 수 있으니 windows에 설치했던 node는 삭제 해주자.

[ms가이드: wsl에 node.js설치](https://learn.microsoft.com/ko-kr/windows/dev-environment/javascript/nodejs-on-wsl)

가이드 보고 따라했다.

![](/assets/img/2023-11-27-example-content/2023-12-09-00-49-14.png)
아니 직접 windows에 설치하고 싶은데 안됐다고요 (울먹)

![](/assets/img/2023-11-27-example-content/2023-12-09-00-49-45.png)
맞다.. 이런 거 꼬이지 않도록 하는 게 중요한데 너무 대충 생각해버렸엉.


### 그래 일단 있던 node 삭제

뭔가 언젠가(?) 설치된 노드가 있었나보다(기억안남;;). 
auto-remove 옵션까지 줘서 삭제했다. 

![](/assets/img/2023-11-27-example-content/2023-12-09-00-52-33.png)
그래.. 대충 nodejs-v10이 removing 되는 게 보이는구만
{:.figcaption }


### nvm 설치

ms가이드에서 `nvm`를 통해 node.js 설치를 가이드하고 있길래,, 
똑같이 따라했다. 

v10 깔려있는거 보고 너무 옛날버전 아닌가 했는데 21년도 release더라고 ...

이렇게 버전도 워낙 빠르게 바뀌기도 하고 나처럼 설치했었는지 까먹는 경우가 있으니 `nvm`의 필요성에 더욱 공감이 갔다. 

```
sudo apt-get install curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```

가이드 그대로 설치해줬다.

터미널을 한번 껐다 키니까 `nvm -v` 로 제대로 설치된 걸 확인할 수 있었다. 


### nvm 으로 node 설치

![](/assets/img/2023-11-27-example-content/2023-12-09-01-00-51.png)

`lts` 버전만 설치해줬다. (lts니까.. 믿을맨..?)
![](/assets/img/2023-11-27-example-content/2023-12-09-01-01-22.png)

여차해서 `vue-cli` 랑 버전 안맞으면 `nvm` 으로 편하게 아래 버전을 다운로드 받을 수 있을 것.

아니다, 혹시 몰라서 일단 18.x 버전은 설치했다. 
default 버전은 그대로 `lts` 로 설정
![](/assets/img/2023-11-27-example-content/2023-12-09-01-06-14.png)

```bash
# v20(lts)로 node 버전 사용
nvm use node 
nvm use --lts

# v18 버전으로 사용
nvm use lts/hydroen
nvm use v18.19.0
```

## 이제 다시 IDE 터미널로 돌아가보자


![](/assets/img/2023-11-27-example-content/2023-12-09-01-09-45.png)
intellij
{:.figcaption}


![](/assets/img/2023-11-27-example-content/2023-12-09-01-10-16.png)
vscode
{:.figcaption}

![](/assets/img/2023-11-27-example-content/2023-12-09-01-12-31.png)
powershell에서는 인식하지 못하는 모습
{:.figcaption}

아,, 정말 이제 왔다갔다 안하고 wsl로만 착실히 개발해야겠다.

다시 vue-cli를 설치해주니,,
![](/assets/img/2023-11-27-example-content/2023-12-09-01-15-01.png)
오만 삽질만에 ,, 
{:.figcaption}


## vue-cli를 이용해 vue 프로젝트 셋팅

```bash
vue create {프로젝트명}
```
명령어 입력하면 vue-cli 창이 뜬다.

`vue2`와 `vue3`을 고를 수 있게 되어있는데, 흠 그냥 3을 골랐습니다. 
문법에서 조금 차이가 있는 것 같아요 [vue2 vs. vue3](https://moz1e.tistory.com/540)


![](/assets/img/2023-11-27-example-content/2023-12-09-01-16-31.png)


셋티이 끝나면 프로젝트 폴더 (저는 `frontend`) 기준으로 아래와 같은 디렉토리 구조를 볼 수 있습니다.
![](/assets/img/2023-11-27-example-content/2023-12-09-01-19-48.png)

## vue 페이지 띄워보기

기본적으로 vue 페이지는 `8080` 포트로 뜨는데,
springboot 플젝도 8080으로 띄우고 있어서 포트를 변경하여 지정해주었습니다.

```json
//file: package.json
    "serve": "vue-cli-service serve --port 3000",
```
![](/assets/img/2023-11-27-example-content/2023-12-09-01-25-28.png)


![](/assets/img/2023-11-27-example-content/2023-12-09-01-26-14.png)

----

### 정리
