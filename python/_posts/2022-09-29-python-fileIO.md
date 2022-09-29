---
layout: post
title: Python File I/O
description: >
  파이썬 파일 input/output
sitemap: false
hide_last_modified: true
---

file io

## file open
~~~python
f = file.open("test_file.txt")
lines = f.read()
# ...
f.close()
~~~


## with open() 구문
~~~python
with open("test_file.txt") as f:
  # 들여쓰기 내에서 파일 사용
# f.close() 필요 없음
~~~