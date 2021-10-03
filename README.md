# 4주차 지도학습 TIL:boom:

:pencil2: :pencil2:

### 2.3.5 결정 트리

결정트리는 분류와 회귀 문제에 널리 사용하는 모델. 예/아니오 질문을 이어나가며 학습한다

<br>

- **노드** : 질문이나 정답을 담은 네모 상자. 맨 위 노드는 **루트 노드**라 불리고, 마지막 노드는 **리프**라고도 한다. 
- **에지**는 질문의 답과 다음 질문을 연결한다.

<br>

#### 결정트리 만들기

- 데이터셋 : two_moons 사용

<br>

- 결정 트리를 학습한다는 것 -> 정답에 가장 빨리 도달하는 예/아니오 질문 목록을 학습한다는 것  
- 머신러닝에서 이런 질문들을 **테스트**라고 한다.  

---
가장 좋은 테스트를 찾는 과정을 반복해서 모델을 더 정확하게 만들 수 있다.

- 반복된 프로세스는 각 노드가 테스트 하나씩을 가진 **이진 결정 트리**를 만든다 (True/False)  
- 즉 각 테스트는 하나의 축을 따라 데이터를 둘로 나눈다  
- 계층적으로 영역을 분할해가는 알고리즘이며 각 테스트는 하나의 특성에 대해서만 이루어지므로 나누어진 영역은 항상 축에 평행  

<br>

- 데이터를 분할하는 것은 각 분할된 영역이 (결정 트리의 리프) 한 개의 타깃값(하나의 클래스나 회귀 분석 결과)을 가질 때까지 반복!

<br>

- 타깃 하나로만 이루어진 리프 노드를 **순수 노드**라고 한다.

---
- 새로운 데이터 포인트에 대한 예측은 주어진 데이터 포인트가 특성을 분할한 영역들 중 어디에 놓이는지를 확인,  
그 영역의 타깃 값 중 다수인 것을 예측 결과로 한다. _순수 노드라면 하나!_

<br>

- **회귀** 문제에도 트리 사용 가능  
같은 방법으로 새로운 데이터 포인트에 해당되는 리프 노드를 찾고, 찾은 리프 노드의 훈련 데이터 평균값이 이 데이터 포인트의 출력

<br>

> #### 결정 트리의 복잡도 제어하기


> #### 결정 트리 분석


> #### 트리의 특성 중요도


> #### 장단점과 매개변수

*여기까지 쓴 거 다 날라갔네잉 쯧ㅜㅜ 다시 써야할까? 쓰자..*

<br>

### 2.3.6 결정 트리의 앙상블

**앙상블** : 여러 머신러닝 모델을 연결하여 더 강력한 모델을 만드는 기법  
<br>
분류와 회귀 모델의 다양한 데이터셋에서 효과적인 모델 --> **랜덤 포레스트**와 **그레이디언트 부스팅**~!!  
<br>

> #### 랜덤 포레스트

- 랜덤 포레스트는 기본적으로 조금씩 다른 여러 결정 트리의 묶음  
- 잘 작동하되 서로 다른 방향으로 과대적합된 트리를 많이 만들고, 그 결과를 평균냄으로써 과대적합된 양을 줄일 수 있다.  
--> 예측 성능 유지, 과대적합 줄임

- 트리 생성 시 트리들이 달라지도록 무작위성을 주입.  
1. 트리를 만들 떄 사용하는 **데이터 포인트**를 무작위로 선택
2. 분할 테스트에서 **특성**을 무작위로 선택  
<br>

#### 랜덤 포레스트 구축

생성할 트리의 개수를 정한다. - n_estimators 매개변수  

각 트리를 완전히 독립적으로 만들기 위해 먼저 데이터의 **부트스트랩 샘플**을 생성.  
(n_samples개의 데이터 포인트 중에서 무작위로 데이터를 n_samples 횟수만큼 반복 추출한다)  
<br>
특성의 개수는 max_feature 매개변수로 조정 가능  

이렇게 만든 데이터셋으로 결정트리를 만듦
- 부트스트랩 샘플링을 통해 랜덤 포레스트의 트리가 조금씩 다른 데이터셋으로 만들어지게 됨
- 각 노드에서 특성의 일부만 사용하기 때문에 트리의 각 분기는 각기 다른 특성의 부분 집합을 사용  
--> 랜덤 포레스트의 모든 트리가 서로 달라짐

**매개변수 max_features**  
max_features의 값을 크게 하면 트리들은 매우 비슷해지고 가장 두드러진 특성을 이용해 데이터에 잘 맞춰짐  
값을 낮추면 트리들은 많이 달라지고 각 트리는 데이터에 맞추기 위해 깊이가 깊어짐  
<br>

#### 랜덤 포레스트 분석
- two_moon 데이터셋을 가지고 트리 5개로 구성된 랜덤 포레스트 모델 생성
```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import make_moons

X,y = make_moons(n_samples=100, noise=0.25, random_state=3)
X_train, X_test, y_train, y_test = train_test_split(X, y, stratify=y, random_state=42)

forest = RandomForestClassifier(n_estimate=5, random_state=2)
forest.fit(X_train, y_train)
```
랜덤 포레스트 안에 만들어진 트리는 **estimators_** 속성에 저장됨  
<br>
결정 경계 시각화  
```python
fig, axes = plt.subplots

<br>

#### 장단점과 매개변수
- 성능이 매우 뛰어나고 매개변수 튜닝을 많이 하지 않아도 잘 작동하며 데이터의 스케일을 맞출 필요가 없다
- 텍스트 데이터처럼 차원이 높고 희소한 데이터에는 잘 작동하지 않음
- 선형 모델보다 많은 메모리를 사용하며 훈련과 예측이 느림  
<br>
- 중요 매개변수는 n_estimators, max_features, max_depth같은 사전 가지치기 옵션
- n_estimators는 클수록 졸다. --> 더 많은 트리를 평균하면 과대적합 줄여 더 안정적인 모델 생성 but 긴 훈련 시간 ㅜㅜ
<br>

> #### 그래디언트 부스팅 회귀 트리
여러 개의 결정 트리를 묶어 강력한 모델을 만드는 또 다른 앙상블 방법  
(회귀와 분류 모두에 사용 가능)
<br>
- 이전 트리의 오차를 보완하는 방식으로 순차적으로 트리를 만듦
- 무작위성이 없는 대신 사전 가지치기가 사용됨
- 메모리를 적게 사용하고 예측이 빠른 것이 특징
<br>
- 얕은 트리 같은 간단한 모델(**약한 학습기**)을 많이 연결하는 것이 근본적인 아이디어

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
