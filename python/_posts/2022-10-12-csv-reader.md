---
layout: post
title: Basic | CSV 파일 읽기
description: >
  파이썬에서 csv 파일 읽는 법
sitemap: false
hide_last_modified: true
---

~~~python
import csv

csvreader = csv.reader(open("test.txt"))

for line in csvreader:
    print(line)
~~~
