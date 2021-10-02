# 4주차 지도학습 TIL:boom:

:pencil2: :pencil2:

### 2.3.5 결정 트리

결정트리는 분류와 회귀 문제에 널리 사용하는 모델. 예/아니오 질문을 이어나가며 학습한다

노드 : 질문이나 정답을 담은 네모 상자. 맨 위 노드는 **루트 노드**라 불리고, 마지막 노드는 **리프**라고도 한다.
에지는 질문의 답과 다음 질문을 연결한다.

> #### 결정트리 만들기

데이터셋 : two_moons 사용

결정 트리를 학습한다는 것 -> 정답에 가장 빨리 도달하는 예/아니오 질문 목록을 학습한다는 것  
머신러닝에서 이런 질문들을 **테스트**라고 한다.  

---
가장 좋은 테스트를 찾는 과정을 반복해서 모델을 더 정확하게 만들 수 있다.

반복된 프로세스는 각 노드가 테스트 하나씩을 가진 **이진 결정 트리**를 만든다 (True/False)  
즉 각 테스트는 하나의 축을 따라 데이터를 둘로 나눈다  
계층적으로 영역을 분할해가는 알고리즘이며 각 테스트는 하나의 특성에 대해서만 이루어지므로 나누어진 영역은 항상 축에 평행  

데이터를 분할하는 것은 각 분할된 영역이 (결정 트리의 리프) 한 개의 타깃값(하나의 클래스나 회귀 분석 결과)을 가질 때까지 반복!

타깃 하나로만 이루어진 리프 노드를 **순수 노드**라고 한다.

---
새로운 데이터 포인트에 대한 예측은 주어진 데이터 포인트가 특성을 분할한 영역들 중 어디에 놓이는지를 확인,  
그 영역의 타깃 값 중 다수인 것을 예측 결과로 한다. _순수 노드라면 하나!_

**회귀** 문제에도 트리 사용 가능  
같은 방법으로 새로운 데이터 포인트에 해당되는 리프 노드를 찾고, 찾은 리프 노드의 훈련 데이터 평균값이 이 데이터 포인트의 출력


> #### 결정 트리의 복잡도 제어하기


> #### 결정 트리 분석


> #### 트리의 특성 중요도


> #### 장단점과 매개변수

### 2.3.6 결정 트리의 앙상블

> #### 랜덤 포레스트

##### 랜덤 포레스트 구축
##### 랜덤 포레스트 분석
##### 장단점과 매개변수

> #### 그래디언트 부스팅 회귀 트리

### 2.3.7 배깅, 엑스트라 트리, 에이다부스트

> #### 배깅
> #### 엑스트리 트리
> #### 에이다부스트

### 2.3.8 커널 서포트 벡터 머신

> #### 선형 모델과 비선형 모델

> #### 커널 기법

> #### SVM 이해하기

> #### SVM 매개변수 튜닝

> #### SVM을 위한 데이터 전처리

> #### 장단점과 매개변수

### 2.3.9 신경망(딥러닝)

> #### 신경망 모델

> #### 신경망 튜닝

> #### 장단점과 매개변수

> #### 신경망의 복잡도 추정


## 2.4 분류 예측의 불확실성 추정

### 2.4.1 결정 함수

### 2.4.2 예측 확률
