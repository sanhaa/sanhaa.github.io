---
layout: post
title: Basic | 특정 데이터 가져오기 (operator.itemgetter)
description: >
  itemgetter()는 특정 인덱스, key 값을 가진 데이터를 반환
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

~~~python
from operator import itemgetter
~~~



python의 operator 모듈의 함수 중 하나, [operator.itemgetter()](https://docs.python.org/3/library/operator.html#operator.itemgetter)


> Return a callable object that fetches item from its operand using the operand’s __getitem__() method.

말이 어렵게 써있지만,

- list, tuple, dictionary 등의 데이터에서 특정 항목을 가져온다.
- `sorted()`, `map()`에서 활용 가능하도록 호출 가능한 형태를 반환


## 예시: sorted

학생들의 시험점수를 나타낸 리스트가 있고,  

~~~python
exam = [
    ("Alice", 80),
    ("Jane", 95),
    ("Peter", 72)
]
~~~

시험 점수가 높은 학생 순으로 정렬하고 싶다면, [sorted()](https://docs.python.org/ko/3/library/functions.html#sorted)에 들어갈 key 함수에 점수 기준으로 정렬하도록 설정해야 한다.

~~~python
# 1. 리스트의 각 원소(학생)의 시험점수를 반환하는 함수를 만들고
def get_score(student):
    # (이름, 점수) 형식의 튜플
    return student[1]

# 2. def_score 함수를 key로 넘겨주어 exam 데이터 속의 점수를 기준으로 정렬할 수 있도록 한다.
sorted_students = sorted(exam, key=get_score, reverse=True)
~~~

이때 `itemgetter()`를 사용한다면 `get_socre` 함수를 만들지 않고, 특정 원소를 바로 반환받을 수 있다.

~~~python
# itemgetter(1): 1번째 원소를 반환
sorted_students = sorted(exam, key=itemgetter(1), reverse=True)
~~~

## 작동 원리

~~~python
itemgetter(1)("ABCDEFG")
### >>> 'B'

itemgetter(0, 2)("ABCDEFG") # 여러 개의 값이 선택되면 tuple 형태로 반환
### >>> ('A', 'C')
~~~

`f = itemgetter(2)` 라면 `f(r)` 호출 후 `r[2]` 반환하는 형태와 같다.


itemgetter()의 구현은 다음과 같다. ~~근데 알 필요가 없죠~~
~~~python
def itemgetter(*items):
    if len(items) == 1:
        item = items[0]
        def g(obj):
            return obj[item]
    else:
        def g(obj):
            return tuple(obj[item] for item in items)
    return g
~~~

## 활용: map

[map 함수](https://docs.python.org/ko/3/library/functions.html#map)는 iterable한 모든 항목에 지정한 funciton을 적용한 후 그 결과를 반환 (~~정확히는 결과를 내는 iterator를 반환한다, 반환형도 list가 아니라 map object~~)


~~~python
inventory = [('apple', 5), ('banana', 10), ('orange', 2), ('kiwi', 1)]

# map: inventory라는 리스트에 itemgetter(0) 함수를 동일하게 적용
# itemgetter: inventory라는 리스트에서 0번째 item을 가져옴
list(map(itemgetter(0), inventory))

### >>> ['apple', 'banana', 'orange', 'kiwi']

~~~

## 활용: dictionary key

`itemgetter()`의 매개변수로 dictionary 자료형의 key 값을 넣어줄 수 있다.

~~~python
students = [
    {'name': 'Alice', 'age': 19, 'score': 80},
    {'name': 'Jane', 'age': 17, 'score': 95},
    {'name': 'Peter', 'age': 16, 'score': 72},
]

sorted(students, key=itemgetter('age'))
### >>> [{'name': 'Peter', 'age': 16, 'score': 72},
###     {'name': 'Jane', 'age': 17, 'score': 95},
###     {'name': 'Alice', 'age': 19, 'score': 80}]

~~~


---

## Reference
- https://docs.python.org/3/library/operator.html#operator.lt
- https://wikidocs.net/109327