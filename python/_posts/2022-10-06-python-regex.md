---
layout: post
title: Basic | 정규표현식, python re 모듈 사용하기
description: >
  정규표현식이란 무엇인가, 파이썬에서 정규표현식 사용하기 (메타문자, 수량자, 파이썬 모듈 re 사용하기)
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

모르면 완전 암호 같지만 규칙만 알면 쉬운 정규표현식!


# 정규표현식(regex)이란

> = 정규식

- 문자열에서 특정 문자 조합을 찾기 위한 패턴
- ex. 전화번호, 이메일, 웹사이트 주소를 검색하거나, 형식을 지정할 때 사용


# 메타 문자
![](/assets/img/221006/meta.jpg)


# 수량자
![](/assets/img/221006/qt.jpg) 


# 그룹
- 정규식에서 괄호 `()`로 묶음 `(abc)*de(fg)+`
- 그룹 참조하기: \1, \2 등 순서대로
- 그룹 참조하여 정규식에 나타낼 때, 이스케이프 문자 \를 한 번 더 사용해야 함 ` "abc\\1"`



# 파이썬에서 정규식 사용하기

~~~python
import re
~~~

## 1. findall 함수

> re.findall(패턴문자열, 타겟문자열)


- 반환형: `list`
- 타겟문자열에서 pattern과 일치하는 것을 모두 찾기  

*ex. 전화번호 형식 010-xxxx-xxxx 모두 찾기*
~~~python
s = "lee 010-2222-3333 kim 010-5959-5958 park 01011112222"
p = "010-\d{4}-\d{4}"

print(re.findall(p, s))
### >>> ['010-2222-3333', '010-5959-5958']
~~~


## 2. search 함수

> re.search (패턴문자열, 타겟문자열)

- 반환형: `Match object`
- 전체 문자열 중에 매치되는 오브젝트 찾기
- re.match()와 다른점: match는 선두에 매치되는 문자열이 없으면 None 반환하지만 search는 전체 문자열 탐색
- match object에 group() 함수 사용하여 매치된 결과 확인

~~~python
s = "tomato"
p = "(to)ma\\1"
m = re.search(p, s)

print(m1.group())
### >>> tomato
~~~

## 3. sub 함수

> re.sub(패턴문자열, 대체할 문자열, 타겟문자열)

- 반환형: `string`
- 타겟문자열에서 패턴문자열을 찾고 특정 형식으로 대체하기
- 대체할 문자열 파라미터에 정규식 사용 가능

*ex. 유효한 전화번호는 vaild! 문구로 대체*
~~~python
s = "lee 010-2222-3333 kim 010-5959-5958 park 01011112222"
p = "(010)\-\d{4}\-(\d{4})"
print(re.sub(p, "\g<1>-****-\g<2>", s))

'''
lee vaild! 
kim vaild! 
park 01011112222
'''
~~~

*ex. 전화번호 가운데 네 자리 블라인드(****) 하기*
~~~python
s = "lee 010-2222-3333 kim 010-5959-5958 park 01011112222"
p = "(010)\-\d{4}\-(\d{4})"
print(re.sub(p, "\g<1>-****-\g<2>", s))

'''
lee 010-****-3333 
kim 010-****-5958 
park 01011112222
'''
~~~

`g<1>` : 그룹 설정, 앞에서부터 1, 2, 3으로 이름 붙음

<br>

---

## Reference
- https://docs.python.org/3/library/re.html