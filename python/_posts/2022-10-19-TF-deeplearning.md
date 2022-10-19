---
layout: post
title: <텐서플로> 간단한 Deep learning 구현 (Keras)
description: >
  Tensorflow를 이용하여 모델을 생성하고 학습시키는 방법
# sitemap: false
hide_last_modified: false
---

- Table of Contents
{:toc .large-only}


## What is TensorFlow
> 머신러닝(딥러닝)을 위한 오픈소스 라이브러리

- 구글이 개발
- 데이터 처리, 딥러닝 모델 생성 및 학습을 위한 도구
- 페이스북이 개발한 딥러닝 프레임워크인 pytorch도 많이 쓰는 추세. [pytorch vs.tensorflow](https://wikidocs.net/156950)

## What is Keras
> Tensor Flow의 패키지로 제공되는 고수준 API, 딥러닝 모델을 간단하고 빠르게 구현 가능

## Tensor Flow 딥러닝 모델 구현

1. 모델 클래스 객체 생성  
    ~~~python 
    tf.keras.models.Sequential() 
    ~~~
2. 모델의 layer 구성
    ~~~python
    tf.keras.layers.Dense(units, activation)
    ~~~
    - `units`: 레이어 안의 Node 수
    - `activation`: 적용할 activiation 함수 (ex. `relu`, `sigmoid`, `softmax`)
    - 모델 구성 예시 (1) - 리스트 형태
        ~~~python
        model = tf.keras.models.Sequential([
            tf.keras.layers.Dense(20, input_dim = 2, activation='relu'),
            tf.keras.layers.Dense(20, activation='relu'),
            tf.keras.layers.Dense(1, activation='sigmoid')
        ])
        ~~~
    - 모델 구성 예시 (2) - add()를 통해 layer 추가
        ~~~python
        model = tf.keras.Sequential()
        model.add(tf.keras.layers.Dense(16, input_dim=2, activation='relu'))
        model.add(tf.keras.layers.Dense(1, activation='sigmoid'))
        ~~~
3. 모델 학습 방식 설정
    ~~~python
    model.compile(optimizer, loss)
    ~~~
    - `optimizer`: 모델 학습 최적화 방식
    - `loss`: 손실 함수 설정
    - 예시
    ~~~python
    model.compile(optimizer='adam', loss='mse')
    ~~~
4. 모델 학습
    ~~~python
    model.fit(train_x, train_y)
    ~~~
5. 모델 평가
    ~~~python
    model.evaluate(test_x, test_y)
    ~~~

6. 모델 예측
    ~~~python
    pred = model.predict(test_x) # 예측값 반환
    ~~~


## Tensor Flow + Keras를 활용하여 비선형회귀 구현
~~~python
import tensorflow as tf
import numpy as np

import matplotlib.pyplot as plt
import matplotlib as mpl
from mpl_toolkits.mplot3d import Axes3D

import os
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'

np.random.seed(100)
tf.random.set_seed(100)


# 비선형 데이터 샘플 생성
x_data = np.linspace(0, 10, 100) 
y_data = 1.5 * x_data**2 -12 * x_data + np.random.randn(*x_data.shape)*2 + 0.5

# print(x_data)
# print(x_data.shape) # (100, )

# 모델 정의
model = tf.keras.models.Sequential([
(    tf.keras.layers.Dense(20, input_dim = 1, activation='relu'),
)    tf.keras.layers.Dense(20, activation='relu'),
    tf.keras.layers.Dense(1)
])

model.compile(loss = 'mean_squared_error', optimizer = 'adam')

history = model.fit(x_data, y_data, epochs=500, verbose=1)

predictions = model.predict(x_data)

~~~

![](/assets/img/221019/keras-res.png)

{:.figcaption}

데이터(파란점)과 선형회귀(빨간선) 시각화

---

## Reference
+ https://wikidocs.net/156950