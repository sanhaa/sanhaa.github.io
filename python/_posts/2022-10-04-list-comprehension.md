---
layout: post
title: List Comprehension
description: >
  리스트로 리스트 만들기
sitemap: false
hide_last_modified: true
---

리스트 생성을 한 줄로 하기


- Table of Contents
{:toc .large-only}

---



## List Comprehension 이란

> 리스트를 생성할 때 짧게 한 줄로 만드는 문법


~~~python
[<원소의 최종 형태> for <변수> in <순회 가능한 값, 리스트 등>]
~~~

## 예시: list로 list 만들기

이미 존재하는 list의 값을 변형하여 새로운 list를 만드려고 할 때의 예시

~~~python
# 요일의 맨 첫 글자만 따서 새로운 리스트를 만드려고 할 때
days = ["MON", "TUE", "WED", "THU", "FRI", "SAT", "SUN"]

new_days = []
for day in days:
  new_days.append(day[0])

print(new_days)
# >>> ['M', 'T', 'W', 'T', 'F', 'S', 'S']

~~~

위와 같이 for문으로 순회하면서 만들어내야 하는 리스트를 한 줄로 짧게 만들 수 있게 하는 문법이 `리스트 컴프리헨션`이다.

~~~python
# list comprehension 
days = ["MON", "TUE", "WED", "THU", "FRI", "SAT", "SUN"]

new_days = [day[0] for day in days]
# >>> ['M', 'T', 'W', 'T', 'F', 'S', 'S']
~~~

## 예시: range() 활용

`range()` 함수는 특정 범위 값의 정수 리스트를 반환하므로 아래와 같이 활용할 수 있다.

~~~python
# 0부터 20미만 짝수 list 만들기
even_nums = [i*2 for i in range(10)]

# >>> [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
~~~


## 예시: if문 활용

~~~python
# 0부터 20미만 짝수 list 만들기
even_nums = [i for i in range(20) if i%2==0]

# >>> [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]


~~~
