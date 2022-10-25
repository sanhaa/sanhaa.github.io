---
layout: post
title: 머신러닝 파이썬 코드 스니펫
description: >
  copy and paste
# sitemap: false
hide_last_modified: false
# comments: true
---


- Table of Contents
{:toc}

---

## File Open
### txt file -> 한 줄씩 읽어 list로 저장하기
~~~python
### for문 이용
lines = []
with open("sample.txt") as f:
    for row in f:
        lines.append(f.strip())

### readlines() 이용
lines2 = []
with open("sample2.txt") as f:
    lines2 = f.readlines() # 여러 줄 읽기

lines2 = [x.strip() for x in lines2] # 줄바꿈 문자 제거
~~~

## Normalize

**최대 1, 최소 0이 되도록 선형 정규화**  
각 feature 별로 (column 별) 최솟값을 빼고 최댓값으로 나누기
~~~python
for i in range(X.shape[1]):  # feature의 개수만큼 반복 = 13
    X[:, i] -= np.min(X[:, i]) # 해당 열의 minimum을 일괄적으로 빼기
    X[:, i] /= np.max(X[:, i]) # 해당 열의 max 값으로 전체 열을 나누기

return X
~~~



# Scikit-learn

~~~python
from sklearn.model_selection import train_test_split
~~~

## Regression
### Linear Regression
~~~python
from sklearn.linear_model import LinearRegression

lrmodel = LinearRegression()
lrmodel.fit(train_x, train_y)

beta_0 = lrmodel.coef_[0]   # lrmodel로 구한 직선의 기울기
beta_1 = lrmodel.intercept_ # lrmodel로 구한 직선의 y절편

print("beta_0: %f" % beta_0)
print("beta_1: %f" % beta_1)
print("Loss: %f" % loss(X, Y, beta_0, beta_1))

pred = lrmodel.predict(test_x)
socre = lr_mode.score(test_x, test_y)

~~~

### Ridge/Lasso/ElasticNet Regression
~~~python
from sklearn.linear_model import Ridge
from sklearn.linear_model import Lasso
from sklearn.linear_model import ElasticNet

ridge_reg = Ridge(alpha=10)
lasso_reg = Lasso(alpha=10)
ElasticNet_reg = ElasticNet(alpha=0.001, l1_ratio=0.01)
~~~

### Regression metrics
~~~python
from sklearn.metrics import mean_absolute_error
from sklearn.metrics import mean_squared_error
from sklearn.metrics import r2_score

loss = mean_absolute_error(y, y_pred)
~~~

## PCA

~~~python
import sklearn.decomposition

num_components = 3

pca = sklearn.decomposition.PCA(n_components=num_components)
pca.fit(X)
transform_res = pca.transform(X)
~~~

## Classification
### SVM
~~~python
from sklearn.svm import SVC
from sklearn.metrics import classification_report, confusion_matrix 

svm = SVC()
svm.fit(train_X, train_y)
pred_y = svm.predict(test_X)

# SVM 분류 결과값을 출력합니다.
print("\nConfusion matrix : \n",confusion_matrix(test_y,pred_y))  
print("\nReport : \n",classification_report(test_y,pred_y)) 
~~~

### Gaussian NB
~~~python
from sklearn.naive_bayes import GaussianNB

model = GaussianNB()
model.fit(train_X, train_y)
predicted = model.predict(test_X)
~~~

## Clustering
### K-means
~~~python
from sklearn.cluster import KMeans

kmeans = KMeans(init="random", n_clusters=3, random_state=100)
kmeans.fit(irisDF)
~~~

### Gaussian Mixture
~~~python
from sklearn.mixture import GaussianMixture

gmm = GaussianMixture(n_components=3, random_state=100)
gmm.fit(irisDF)
irisDF['cluster'] = gmm.predict(irisDF)
~~~

## 직접 구현
### Loss Function

**반복문** 
~~~python
def loss(x, y, beta_0, beta_1):
    N = len(x)

    l = 0 # loss 값
    for i in range(N):
        l += (y[i] - (beta_0*x[i] + beta_1))**2
    
    return l
~~~

**numpy 연산**
~~~python
rss = np.sum(np.square(y - y_pred)) # RSS
mse = np.mean(np.square(y - y_pred)) # MSE
~~~

### K-means Clustering

[K-means 정리 포스팅](/ml/basic/2022-10-12-kmeans.md)  
~~~python

def kmeans(X, num_clusters, initial_centroid_indices):
    import time
    N = len(X)
    centroids = X[initial_centroid_indices]
    labels = np.zeros(N)
    
    while True:
        is_changed = False # 라벨이 바뀌었는지 

        for i in range(N):
            distances = []
            for centroid in centroids:
                distances.append(distance(X[i], centroid))
                
            if labels[i] != np.argmin(distances):
                is_changed = True
            labels[i] = np.argmin(distances) # 클러스터 0, 1, 2 중 하나

        # print(labels)
        
        ### 새 중심점 계산
        for k in range(num_clusters):
            x = X[labels == k][:, 0]
            y = X[labels == k][:, 1]

            x = np.mean(x)
            y = np.mean(y)
            centroids[k] = [x, y]

        if not is_changed:
            break

    return labels

### 유클리드 거리 norm
def distance(x1, x2):
    return np.sqrt(np.sum((x1 - x2) ** 2))
~~~