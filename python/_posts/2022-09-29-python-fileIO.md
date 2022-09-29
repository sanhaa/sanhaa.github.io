---
layout: post
title: [Python] File I/O
description: >
  파이썬 파일 input/output
sitemap: false
hide_last_modified: true
---

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

----
## Reference
- https://velog.io/@shg4821/%EA%B9%83%ED%97%88%EB%B8%8C-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-1
