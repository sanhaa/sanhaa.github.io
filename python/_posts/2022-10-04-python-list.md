---
layout: post
title: Baisc | List 자료형
description: >
  파이썬 리스트 자료형, 리스트 순회
sitemap: false
hide_last_modified: true
---

list 자료형

---

## 리스트 순회: for
~~~python
fruits = ["키위", "포도", "멜론", "사과"]

for fruit in fruits:
    print(fruit)

for i in range(len(fruits)):
    print(f"{i}번째 과일: {fruits[i]}")

~~~