---
layout: post
title: <머신러닝> 역전파(BackPropagation)
description: >
  딥러닝에서 역전파는 어떻게 이루어지나, 구현
# sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}


## 역전파

## python 구현
~~~python
import math

def sigmoid(x) :
    return 1 / (1 + math.exp(-x))

def getParameters(X, y) :
    
    f = len(X[0])
    w = [1] * f
    values = []
    
    while True :

        wPrime = [0] * f    # 초기 가중치 w에 더해지는 값 (역전파로 구해짐)
        
        for i in range(len(y)) :
            r = 0
            for j in range(f) :
                r = r + X[i][j]*w[j]
            
            v = sigmoid(r)
            
            # w를 업데이트하기 위한 wPrime을 역전파를 이용해 구하는 식
            for j in range(f) :
                wPrime[j] += -((v - y[i]) * v * (1-v) * X[i][j])
        
        flag = False
        
        for i in range(f) :
            if abs(wPrime[i]) >= 0.001:
                flag = True
                break
        
        if flag == False :
            break
        
        for j in range(f) :
            w[j] = w[j] + wPrime[j]
    
    return w

def main():
    
    # [예제 1]
    X = [(1, 0, 0), (1, 0, 1), (0, 0, 1)]
    y = [0, 1, 1]

    # [예제 2]
    # X = [(0, 0, 0), (0, 0, 1), (0, 1, 0), (0, 1, 1), (1, 0, 0), (1, 0, 1), (1, 1, 0), (1, 1, 1)]
    # y = [0, 0, 0, 1, 0, 1, 1, 1]

    print(getParameters(X, y))

if __name__ == "__main__":
    main()

~~~


---

## Reference
