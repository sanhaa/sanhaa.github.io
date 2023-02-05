---
layout: post
title: Basic | Python 문자열 함수
description: >
  파이썬 문자열에 자주 사용하는 함수
sitemap: false
hide_last_modified: true
---

파이선 문자열을 다룰 때 쓰는 대표 함수들을 알아보자. (리스트 함수 포함 ㅎ)

*목차*  
1. [startswith()](#startswith)
2. [split()](#split)
3. [lower()](#lower)
4. [replace()](#replace)


- Table of Contents
{:toc .large-only}

---



## startswith()

~~~python
string.startswith("<특정문자열>")
~~~

> 문자열이 특정 문자열로 시작하는지 검사, True/False 반환

~~~python
s = "I'm banana"

print(s.startswith("I")) # True

if s.startswith("I"):
  print("문자열 s는 I로 시작함")

if s.startswith("I'm"):
  print("문자열 s는 I'm로 시작함")
~~~

## split()

~~~python
string.split("<기준 문자>")
~~~

> 문자열을 특정 기준 문자로 쪼개서 리스트로 반환

~~~python
s = "I'm banana"

# split() 함수 안에 기준 문자가 없을 때: 공백 기준으로 문자열을 split
print(s.split()) 
# >>> ["I'm", "banana"]

print(s.split("'")) 
# >>> ["I", "'m banana"]

~~~

### split() vs. split(' ')
`split()`: 공백 전부 제거  
`split(' ')`: 공백 기준으로 모두 split, 빈 문자열이 반환됨

~~~python
numbers = "  1 2 3  "
print(numbers.split())
# >>> ['1', '2', '3']

print(numbers.split(' '))
# >>> ['', '', '1', '', '2', '', '3', '', '' ]
~~~

## lower()

> 문자열의 대소문자 변환

~~~python
s = "I'm banana"

print(s.lower())
# >>> i'm banana

print(s.upper())
# >>> I'M BANANA
~~~

**주의!**  
`s.lower()`는 문자열을 직접 수정하지 않고 새로운 값 생성.  

~~~python
s = "I'm banana"
s.upper()
print(s)
# >>> I'm banana

s = s.upper() # 꼭 반환값을 새로운 문자열 변수나 기존 변수에 넣어주도록 하자
print(s)
# >>> I'M BANANA
~~~

## replace()

~~~python
문자열.replace("기존 문자열", "대체할 문자열")
~~~

> 특정 문자열로 대체

~~~python
s = "I'm banana"

print(s.replace("I'm", "I am"))
# >>> I am banana

# 대체할 문자열에 아무것도 입력하지 않으면 문자 제거로 활용할 수 있음
print(s.replace("'", ""))
# >>> Im banana
~~~

**주의**  
마찬가지로 `replace()`는 문자열을 직접 수정하지 않고 새로운 값을 생성한다.  

