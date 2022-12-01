---
toc: true
layout: post
description: Clustering에 대해 알아보자.
categories: [markdown]
title: 군집분석
---
# 군집분석


## 군집화 수행 시 주요 고려사항
- 어떤 거리 척도를 사용하여 유사도를 측정할 것인가?
- 어떤 군집화 알고리즘을 사용할 것인가?
- 어떻게 최적의 군집 수를 결정할 것인가?
- 어떻게 군집화 결과를 측정/평가할 것인가?

### `#1.`어떤 거리 척도를 사용하여 유사도를 측정할 것인가?

- 유클리디안 거리 (Euclidean Distance)
- 맨하탄 거리 (Manhattan Distance)
- 마할라노비스 거리 (Mahalanobis Distance)
- 상관계수 거리 (Correlation Distance)

### `#2.` 군집화: 알고리즘

**1. 계층적 군집화**
- 개체들을 가까운 집단부터 차근차근 묶어나가는 방식
- 군집화 결과 뿐만 아니라 유사한 개체들이 결합되는 dendrogram 생성

**2. 분리형 군집화**
- 전체 데이터의 영역을 특정 기준에 의해 동시에 구분
- 각 개체들은 사전에 정의된 개수의 군집 중 하나에 속하게 됨

**3. 자기조직화 지도**
- 2차원의 격자에 각 개체들이 대응하도록 인공신경망과 유사한 학습을 통해 군집 도출

**4. 분포 기반 군집화**
- 데이터의 분포를 기반으로 높은 밀도를 갖는 세부 영역들로 전체 영역을 구분

### 계층적 군집화 (Hierarchical Clustering)
- 계층적 트리모형을 이용하여 개별 개체들을 순차적/계층적으로 유사한 개체/군집과 통합
- 덴드로그램(Dendrogram)을 통해 시각화 가능
    - 덴드로그램 : 개체들이 결합되는 순서를 나타내는 트리 형태의 구조

- 사전에 군집의 수를 정하지 않아도 수행 가능
    - 덴드로그램 생성 후 적절한 수준에서 자르면 그에 해당하는 군집화 결과 생성

#### 계층적 군집화 수행 예시
- 모든 개체들 사이의 거리에 대한 유사도 행렬 계산
- 거리가 인접한 관측치끼리 군집 형성
- 유사도 행렬 업데이트
- 위의 과정 반복

#### 핵심 수행 절차 : 두 군집 사이의 유사성/거리 측정

- Min(단일연결), max(완전연결), group average(평균연결), between centroid, Ward's, ...

![]({{ site.baseurl }}/images/dist.PNG "두 군집 사이의 유사성/거리 측정") 

`-` **Ward's method** : Distance between two clusters, A and B, how much the sum of squares will increase when they are merged.

### K-평균 군집화 (K-Means Clustering)
>대표적인 분리형 군집화 알고리즘


- 각 군집은 하나의 **중심(centroid)**을 가짐
- 각 개체는 가장 가까운 중심에 할당되며, 같은 중심에 할당된 개체들이 모여 하나의 군집을 형성
- 사전에 군집의 수 K가 정해져야 알고리즘을 실행할 수 있음



$$X = C_1 \cup C_2 \dots \cup C_k, \quad  C_i \cap C_j=\emptyset, \quad i \neq j$$

$$\underset{C}{\operatorname{\arg min}} \sum_{i=1}^K \sum_{x_j \in C_i} ||x_j-c_j||^2$$

#### 무작위 초기 중심 설정의 위험을 피하고자 다양한 연구 존재
- 반복적으로 수행하여 가장 여러 번 나타나는 군집을 사용
- 전체 데이터 중 일부만 샘플링하여 계층적 군집화를 수행한 뒤 초기 군집 중심 설정
- 데이터 분포의 정보를 사용해서 초기 중심 설정
- 하지만 많은 경우 초기 중심 설정이 최종 결과에 큰 영향을 미치지는 않음.

#### K-평균 군집화의 문제점
- 문제1 : **서로 다른 크기**의 군집을 잘 찾아내지 못함
![]({{ site.baseurl }}/images/problem_1.PNG "problem1") 

- 문제2 : **서로 다른 밀도**의 군집을 잘 찾아내지 못함
![]({{ site.baseurl }}/images/problem_2.PNG "problem2") 

- 문제3 : **지역적 패턴이 존재**하는 군집을 판별하기 어려움
    - (보는 위치마다 조금씩 다른 패턴이 보이는 것을 지역적 패턴이 존재한다고 한다.)
    - 지역적 패턴이 존재할 때 Geodesic distance를 이용한다.
    
![]({{ site.baseurl }}/images/problem_3.PNG "problem3") 

### `#3.` 군집화: 최적의 군집 수 결정
> 어떻게 최적의 군집 수를 결정할 것인가?

- 예시) 20개의 관측치가 존재할 때, 최적의 군집 수는?

- 다양한 군집 수에 대해 성능 평가 지표를 도시하여 최적의 군집 수 선택
- Elbow point에서 최적 군집 수가 결정되는 경우가 일반적

![]({{ site.baseurl }}/images/best_cluster.PNG "select best cluster number: k") 

### `#4.` 군집화: 결과 측정 및 평가
> 어떻게 군집화 결과를 측정/평가할 것인가?
> 분류 알고리즘처럼 모든 상황에 적용가능한 평가 지표 부재

`-` 내부 평가지표
- Dunn Index, **Silhouette**, **Sum of Squared Error**,...

`-` 외부 평가지표
- Rand Index, Jaccard Coefficient, Folks and Mallows Index,...


#### 군집화 평가지표 1: Sum of Squared Error (SSE)
$$\text{SSE} = \sum_{i=1}^k\sum_{x\in C_i}dist(x, c_i)^2$$

![]({{ site.baseurl }}/images/sse_1.PNG)

- 군집의 중심을 정의하고 군집을 중심으로부터 거리를 쭉 본것.. 차이의 제곱


- 군집의 개수가 2개가 있다면 첫번째 군집으로 부터 SSE, 두번째 군집에서의 SSE(중심과 관측치 사이의 차이제곱)의 합을 대표적으로 하겠다는 것이다.

$$ SSE = SSE_1 + SSE_2 $$


- 각 군집의 c(중심)으로부터 거리의 제곱의 합을 계산하는데 군집이 $K$개가 있는것. $K$에 따라서 값이 달라지게된다. 당연한 소리지만,,ㅎ

![]({{ site.baseurl }}/images/sse_2.PNG)


- 위의 경우 '2또는 3에서 최적의 군집이다'라고 할 수 있겠다.

#### 군집화 평가지표 2: Silhouette 통계량 (SSE의 단점보완)

- $a(i)$ 관측치 $i$로부터 같은 군집 내에 있는 모든 다른 개체들 사이의 평균 거리
- $b(i)$ 관측치 $i$로부터 다른 군집 내에 있는 개체들 사이의 평균 거리 중 최솟값
- 일반적으로 $\bar{S}$의 값 $0.5$보다 크면 군집 결과가 타당하다고 볼 수 있음
- $-1$에 가까우면 군집이 전혀 되지 않음


$$S(i) = \frac{b(i)-a(i)}{\text{max}\{a(i),b(i)\}}, \space -1 \leq(i) \leq1$$

$$\bar{S} = \frac{1}{n}\sum_{i=1}^{n}S(i)$$


![]({{ site.baseurl }}/images/sil.PNG)



$$S(i) = \frac{b(i)-a(i)}{\text{max}\{a(i),b(i)\}}, \space -1 \leq(i) \leq1$$




`-` 위의 식에서 분모의 역할

- $b(i)-a(i)$의 값은 무한대까지 갈 수 있기 때문에 스케일된 값을 만들어주기 위해서 $\text{max}\{a(i),b(i)\}$로 나눠준다.

- 따라서 실루엣 값은 $-1$과 $1$ 사이에 있다.($-1\leq S(i) \leq 1$)

- 실루엣 계수는 $1$에가까울 수록 좋고 $-1$에 가까울수록 안좋다.

![]({{ site.baseurl }}/_notebooks/my_icons/sil_pic.PNG)


> Tip: 실루엣으로 평가를 할때는 K=2일 때가 많은 경우 가장 크게 나오니 K가 2인 것을 선택하는 것보다는 2번째로 큰 실루엣값(second best)이 해당하는 K의 군집을 사용하는 것이 좋다.

### 실습예제
https://www.kaggle.com/code/kashnitsky/topic-7-unsupervised-learning-pca-and-clustering
