---
layout: post
title: 시각화 | Matplotlib 기초
description: >
  matplotlib 라이브러리 기본 사용법
sitemap: false
hide_last_modified: true
---

> `matplotlib`: 파이썬에서 데이터를 그래프나 차트로 시각화할 수 있는 라이브러리

- Table of Contents
{:toc .large-only}

---

~~~python
import matplotlib.pyplot as plt
~~~

# 그래프 그리기

> 두 가지 방법이 있다.
1. [plt.plot()](#1-pltplot)
2. [plt.subplots()](#2-pltsubplots)

## 1. [plt.plot()](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)
> state machine interface 방식


*선(또는 점) 그래프*  
~~~python
# plt.plot(x, y)
x = list(map(int, range(5))) # [0, 1, 2, 3, 4]
y = list(map(int, range(4, 9))) # [4, 5, 6, 7, 8]

plt.plot(x, y)
~~~

![](/assets/img/220930/mat0.jpg)

그래프 결과
{:.figcaption}

### 해상도, 타이틀, 범주 등

~~~python
### fig: 크기 조절, dpi: 해상도 설정(default: 100)
plt.figure(figsize=(4, 4), dpi=200) 

### plot 라벨 범주 표현하기
plt.plot(x, y, label="x-y")
plt.plot(x, z, label="x-z")
plt.legend(loc="lower right") 

### 그래프 타이틀
plt.title("[Example Plot]")

### x, y 라벨
plt.xlabel("X")
plt.ylabel("Y")

# 좌표평면 범위 조절
plt.ylim([0, 10])

# 눈금 추가/삭제 (스타일마다 default가 다름)
plt.grid()
~~~

![](/assets/img/220930/mat2.jpg)

범주, 타이틀, 라벨 예시
{:.figcaption}

### Line Style

- 실선, 점선 등 선 스타일 변경 [linestyle 옵션](https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D.set_linestyle)
- 선 위에 marker 표시 
- marker 모양 변경 [marker 옵션](https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D.set_marker)

~~~python
x, y = np.array(x), np.array(y)

plt.plot(x, y,  linestyle="-", marker="o")
plt.plot(x, y+1, linestyle="--", marker="^")
plt.plot(x, y+2, linestyle="-.", marker="*")
plt.plot(x, y+3, linestyle=":")
~~~

![](/assets/img/220930/mat3.jpg)

line style, marker 예시
{:.figcaption}


## 2. [plt.subplots()](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.subplots.html)
> object oriented interface 방식



~~~python
# fig, ax = plt.subplots()
x = list(map(int, range(5))) # [0, 1, 2, 3, 4]
y = list(map(int, range(4, 9))) # [4, 5, 6, 7, 8]
z = list(map(int, range(2, 7))) # [2, 3, 4, 5, 6]

fig, ax = plt.subplots()
ax.plot(x, y)
~~~

- `fig`: 전체 figure, 도화지라고 생각
- `ax`: 그래프 객체
- 하나의 fig에 여러 개의 그래프를 그릴 수 있다.
- 하나의 ax에 여러 개의 선을 나타낼 수 있다.

### subplots(nrow, ncols) 그리드 지정 

~~~python
#### plt.subplots(nrows=1, ncols=1) # int, default:1

fig, axes = plt.subplots(2, 1) # 2행 1열 그리드 (위 아래)

# 그래프 그리기
axes[0].plot(x, y)
axes[1].plot(x, z)
~~~

![](/assets/img/220930/mat1.jpg)

그리드 지정 그래프
{:.figcaption}


### subplots() 그래프 예시
> plt.plot()으로 그리는 것과 동일하게 여러가지 옵션을 줄 수 있다.

~~~python
x = np.arange(10)
fig, ax = plt.subplots()

ax.plot(
    x, x, label='y=x',
    marker='o',
    color='blue',
    linestyle=':'
)
ax.plot(
    x, x**2, label='y=x^2',
    marker='^',
    color='red',
    linestyle='--'
)
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.legend(
    loc='upper left',
    shadow=True,
    fancybox=True,
    borderpad=2
)
~~~

![](/assets/img/220930/mat4.jpg)

subplots() 옵션 예시
{:.figcaption}




---

# 그래프 테마
> 단순히 그래프 선 색깔을 바꾸는 것 말고도 다양한 테마를 제공한다.

[matplotlib stylesheet](https://matplotlib.org/stable/gallery/style_sheets/style_sheets_reference.html)에서 다양한 스타일을 고를 수 있다.

~~~python
import matplotlib.pyplot as plt

# 'seaborn' 스타일 사용 선언
plt.style.use("ggplot")
~~~

나는 `ggplot`이나 `seaborn`이 제일 예쁘고 눈에 잘 들어오는 듯

![](/assets/img/220930/ggplot.jpg)

ggplot 스타일시트
{:.figcaption}


---

# 다른 그래프: Scatter, Bar, Histogram
## 1. [Scatter 그래프](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html)

~~~python
plt.figure(figsize=(4, 4), dpi=100) # fig 크기 조절, 해상도 설정

plt.scatter(x, y, alpha=0.8, marker="*") # alpha: 투명도
~~~

![](/assets/img/220930/scatter.jpg)

산점도 그래프 예시
{:.figcaption}

**pandas.DataFrame 산점도 그래프**
~~~python
import pandas as pd

df = pd.DataFrame(np.random.rand(100, 2)); 
print(df)

plt.scatter(df[0], df[1])
~~~

![](/assets/img/220930/scatter2.jpg)

산점도 그래프 예시2
{:.figcaption}

## 2. [Bar 그래프](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html)
~~~python
plt.bar(x=np.arange(5), height=3*x-1)
~~~

![](/assets/img/220930/bar.jpg)

막대 그래프 예시
{:.figcaption}


## 3. [Histogram 그래프](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.hist.html)

~~~python
plt.hist([1, 1, 1, 2, 3, 4, 2, 5])
# 값들에 대한 통계 (빈도수)
~~~

![](/assets/img/220930/histogram.jpg)

히스토그램 예시
{:.figcaption}



---  

# Reference
- 다양한 matplotlib 예제를 보고 싶다면: [example](
https://matplotlib.org/stable/gallery/index.html
)