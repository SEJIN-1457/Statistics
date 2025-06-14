# 통계학 7주차 정규과제

📌통계학 정규과제는 매주 정해진 분량의 『*데이터 분석가가 반드시 알아야 할 모든 것*』 을 읽고 학습하는 것입니다. 이번 주는 아래의 **Statistics_7th_TIL**에 나열된 분량을 읽고 `학습 목표`에 맞게 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 추가자료와 교재를 다시 참고하여 보완하는 것이 좋습니다.

7주차는 `3부. 데이터 분석하기`를 읽고 새롭게 배운 내용을 정리해주시면 됩니다.


## Statistics_7th_TIL

### 3부. 데이터 분석하기
### 13.머신러닝 분석 방법론
### 14.모델 평가



## Study Schedule

|주차 | 공부 범위     | 완료 여부 |
|----|----------------|----------|
|1주차| 1부 p.2~56     | ✅      |
|2주차| 1부 p.57~79    | ✅      | 
|3주차| 2부 p.82~120   | ✅      | 
|4주차| 2부 p.121~202  | ✅      | 
|5주차| 2부 p.203~254  | ✅      | 
|6주차| 3부 p.300~356  | ✅      | 
|7주차| 3부 p.357~615  | ✅      | 

<!-- 여기까진 그대로 둬 주세요-->

# 13.머신러닝 분석 방법론

```
✅ 학습 목표 :
* 선형 회귀와 다항 회귀를 비교하고, 데이터를 활용하여 적절한 회귀 모델을 구축할 수 있다. 
* 로지스틱 회귀 분석의 개념과 오즈(Odds)의 의미를 설명하고, 분류 문제에 적용할 수 있다.
* k-means 알고리즘의 원리를 설명하고, 적절한 군집 개수를 결정하여 데이터를 군집화할 수 있다.
```

## 13.1. 선형 회귀분석과 Elastic Net(예측모델)
- 회귀 분석 : 하나 이상의 독립변수를 통해 종속변수의 변화를 예측하는 통계적 방법론
  - 부모와 자녀 키 연구에서 시작 -> 평균으로 회귀하는 현상에서 유래됨
  - For. 독립변수가 종속변수에 미치는 영향력 파악 및 예측
  - 회귀식: y = β₀ + β₁X₁ + ... + βₚXₚ + ε 형태로 표현
    - ŷ : 예측하고자 하는 값
    - β₀ : 절편, 독립변수가 모두 0일 때 종속변수의 예측값
    - βᵢ : 각 독립변수(Xᵢ)에 해당하는 계수 (Coefficient), 독립변수가 한 단위 변화할 때 종속변수에 미치는 영향
    - ε (epsilon) : 잔차(Error term), 모델로 설명되지 않는 부분
  - 최적 회귀선 : 잔차 제곱합(RSS)을 최소화하는 선
  - 회귀 분석 종류
    - 단순 선형 회귀 분석 : 독립변수가 1개
    - 다중 선형 회귀 분석 : 독립변수가 2개 이상
    - 다항 회귀 분석 : 독립변수와 종속변수 관계가 직선이 아닌 곡선일 때 사용. 독립변수에 차수를 높여 선형 회귀 모델로 변환하여 사용
- 규제 회귀 모델 : 과적합 방지를 위해 각 변수의 계수 크기에 제약을 주는 방법
  - Ridge : L2 norm을 사용하여 계수 제곱합을 규제 (계수를 0에 가깝게 만듦)
  - Lasso : L1 norm을 사용하여 계수 절대값 합을 규제 (영향력 없는 변수의 계수를 0으로 만듦)
  - Elastic Net : Ridge와 Lasso 규제를 결합한 모델
- 기본 가설
 - 잔차의 정규성 : 잔차가 정규 분포를 따름
 - 잔차의 등분산성 : 잔차의 분산이 일정
 - 독립변수들 간 상관관계 없음 (다중 선형 회귀) : 독립변수 간의 강한 상관관계(다중공선성) 문제 확인이 필요
 - 선형성 : 독립변수 변화에 따라 종속변수가 일정하게 변화
- 다중공선성 : 독립변수 간 상관관계 문제 -> VIF(Variance Inflation Factor) 등으로 확인. VIF가 높으면 해당 변수 제거 또는 차원 축소 고려

## 13.2. 로지스틱 회귀분석 (분류모델)
- 로지스틱 회귀분석은 선형 회귀분석이랑 비슷하게 생겼는데, 특정 수치를 예측하는 게 아니라 데이터가 어떤 카테고리에 속할지 분류하는 모델
- 주로 이항 분류에 많이 쓰임. 즉, 결과가 0 아니면 1처럼 딱 두 가지로 나뉘는 경우에 유용
  - 만약 종속변수 카테고리가 3개 이상이면 다항 로지스틱 회귀분석을 쓰면 분류를 예측할 수 있음
- 이 모델은 선형 회귀식에서 나온 결과값을 바로 쓰는 게 아니라, Odds랑 로짓 변환을 거쳐 0부터 1 사이의 확률로 바꿔서 예측
  - 이 확률 변환할 때 시그모이드(sigmoid) 함수를 사용
  - 일반적으로 예측된 확률이 0.5보다 크면 1, 작으면 0으로 분류하는 식으로 기준을 잡음
- 로지스틱 회귀 모델 결과를 해석할 때는 선형 회귀처럼 각 변수의 계수값과 유의도를 확인
  - statsmodels 패키지를 쓰면 이런 계수값과 P-value를 볼 수 있음
  - Odds Ratio를 보면 각 독립변수가 종속변수가 특정 카테고리(보통 1)일 확률에 얼마나 영향을 주는지 알 수 있음
  - 예를 들어 Smoking_Yes의 Odds Ratio가 1.4면, 흡연하는 게 심장병 발생 확률을 비흡연자보다 1.4배 높인다고 해석가능
- 로지스틱 회귀는 분류 모델이라 모델 성능 평가는 선형 회귀랑 다른 기준을 사용
  - 혼동 행렬(Confusion Matrix)이나 ROC Curve, AUC 같은 평가 지표들이 있음
- 모델 학습 전에 데이터 전처리가 필요한데,
  - 명목형 변수는 더미 변수로 바꾸고 숫자형 변수는 스케일링(정규화/표준화)하는 과정이 포함됨
  - 학습 데이터랑 테스트 데이터로 나누는 것도 중요
  - 만약 분류하려는 데이터의 클래스 비율이 너무 차이나면(불균형 데이터), 언더샘플링이나 오버샘플링 기법을 써서 클래스 균형을 맞춰줘야 함

## 13.8. k-means 클러스터링(군집모델)
- k-means 클러스터링은 KNN(K-Nearest Neighbors)이랑 비슷해 보이는데, 레이블(정답)이 없는 데이터를 분석해서 데이터 안에 숨겨진 구조나 패턴을 찾는 비지도 학습 방법임
  - 주어진 데이터를 미리 정해둔 k개의 클러스터로 나누는 게 주된 목적
  - 목표는 각 클러스터의 중심점이랑 그 클러스터에 속한 데이터들 사이의 거리 제곱 합을 가장 작게 만드는 것
  - 작동 방식
    - 1.일단 k개의 중심점을 데이터 공간에 임의로 선정
    - 2.각 데이터들을 가장 가까운 중심점을 가진 클러스터에 배정
    - 3.각 클러스터에 새로 배정된 데이터들의 평균값을 계산해서 새로운 중심점으로 옮김
    - 4.중심점 위치가 더 이상 변하지 않을 때까지 2번과 3번 단계를 계속 반복
- k-means 클러스터링은 거리 기반으로 작동하는 모델이라 데이터의 거리 계산이 엄청 중요
  - 그래서 모델 성능에 거리가 큰 영향을 미치기 때문에 데이터의 정규화나 표준화 과정이 필수
  - 가장 적절한 클러스터 개수인 k를 정하는 게 중요한데, 대표적으로 엘보우 기법(Elbow method)이랑 실루엣 계수를 많이 사용함
  - 엘보우 기법은 k 값에 따라 클러스터 내 데이터와 중심점 간의 총 거리 제곱 합 감소율이 확 꺾이는 지점을 보고 k를 정하고,
  - 실루엣 계수는 클러스터 안에서 얼마나 뭉쳐있고 다른 클러스터랑 얼마나 떨어져 있는지 점수를 내서 가장 높은 점수가 나오는 k를 선택함
- k-means 클러스터링은 처음에 중심점을 어디에 찍는지에 따라 최종 결과가 달라질 수 있고, 지역 최솟값 문제에 빠질 가능성이 있음
  - 이런 문제를 줄이기 위해 k-means++ 같은 초기 중심점 설정 방법이 사용되기도 함
  - 이 모델은 클러스터 형태가 대체로 구형이라고 가정하고 작동하기 때문에 구형이 아닌 데이터에 잘 안 맞을 수 있고, 이상치에도 민감한 단점이 있음
  - 이런 단점은 데이터 밀도를 기반으로 군집하는 DBSCAN 같은 알고리즘으로 보완할 수 있음
- 군집 결과를 해석할 때는 각 클러스터에 속한 데이터들이 어떤 특징을 가지고 있는지 파악하고, 클러스터들 간의 차이가 통계적으로 의미 있는지 t-test나 ANOVA 같은 걸로 검증해보는 과정이 필요함


# 14. 모델 평가
## 14.3. 회귀성능 평가지표
- 회귀 모델이 얼마나 정확하게 예측하는지 평가하기 위해 다양한 기준을 사용
  - 분류 모델과 다른 평가지표를 씀
  - 주요 회귀성능 평가지표는 R-Square, Adjusted R-Square, RMSE, MAE, MAPE, RMSLE, AIC, BIC 등이 있음
- R-Square(결정계수)는 독립변수가 종속변수를 설명하는 설명력을 나타내며 0과 1 사이의 값으로 표현됨
  - 값이 클수록 모델의 설명력이 높다
  - Adjusted R-Square는 독립변수의 개수가 많아질수록 R-Square 값이 커지는 문제를 보정한 지표로
    - 독립변수의 개수가 다른 모델을 비교할 때 유용함
- RMSE(Root Mean Square Error)는 예측값과 실제값의 차이인 잔차 제곱의 평균에 루트를 씌운 값으로, 예측 오차의 크기를 나타낸다
  - 오차 제곱을 사용하므로 이상치(큰 오차)에 민감
- MAE(Mean Absolute Error)는 예측값과 실제값 차이의 절대값 평균으로, RMSE보다 이상치에 덜 민감함
- MAPE(Mean Absolute Percentage Error)는 절대 오차를 실제값으로 나눈 비율의 평균으로, 스케일이 다른 데이터의 모델 성능을 비교할 때 유용하다. 실제값이 0인 경우 문제가 될 수 있음
- RMSLE(Root Mean Square Logarithmic Error)는 예측값과 실제값에 로그를 취한 후 RMSE를 계산하는 방식으로,
  - 종속변수 값이 넓은 범위에 걸쳐 분포하는 경우 유용하며,
  - 예측값이 실제값보다 작을 때 더 큰 패널티를 부여함
  - 실제값이 0일 수 있다면 log(y+1) 방식을 사용해야 함
- AIC(Akaike Information Criterion)**와 **BIC (Bayesian Information Criterion)는 모델의 적합도와 복잡성을 함께 고려하는 지표로
  - 값이 작을수록 좋은 모델로 평가함
  - AIC와 BIC는 독립변수가 많아질수록 페널티를 부여함

## 14.6. 유의확률의 함정
- 유의확률(p-value)은 회귀분석 등에서 개별 변수나 모델의 유의미성을 판단하는 데 사용된다
  - 일반적으로 p-value가 0.05 미만일 때 귀무가설을 기각하고 대립가설을 채택
- 하지만 p-value 해석에는 주의가 필요함!
  - p-value가 0.05 미만이라고 해서 해당 변수가 무조건 중요하거나 종속변수에 큰 영향을 미친다는 것을 의미하지 않기 때문
  - 단지 귀무가설이 틀렸을 가능성이 높다는 것을 의미할 뿐이다
- 표본 크기가 매우 클 경우, 통계적으로 유의미하지 않은 작은 차이도 p-value가 매우 작게 나올 수 있는데,
  - 이는 통계적 유의성이 현실적인 중요성이나 효과 크기를 보장하지 않음을 보여줌
- 오직 p-value에만 의존하여 변수를 선택하면 실제로 중요하지 않은 변수가 포함되거나 중요한 변수가 제외될 수 있음을 유의
  - p-value 0.05라는 기준은 관습적이며 절대적인 기준이 아니다
  - 분석가가 원하는 p-value를 얻기 위해 데이터를 조작하는 문제는 피해야 할 것

## 14.7. 분석가의 주관적 판단과 스토리텔링
- 기계학습 분석에는 객관적인 방법론 외에도 분석가의 주관적 판단이 필수적이다
- 올바른 분석을 위해서는 데이터 분석 방법론 지식뿐만 아니라 비즈니스 도메인 지식, 데이터에 대한 깊은 이해, 통계적 지식, 창의성 등이 필요함
- 모델 선택, 데이터 전처리 방법 결정, 이상치 처리, 변수 해석 등 여러 단계에서 분석가의 주관적 판단이 중요하게 작용하며,
  - 특히 군집 분석처럼 레이블이 없는 데이터에서는 군집의 특성을 정의하고 해석하는 데 분석가의 주관이 크게 개입한다
- 분석 결과를 효과적으로 전달하기 위한 스토리텔링 능력도 중요한데, 복잡한 분석 결과도 상대방이 이해하기 쉽게 설명하고 공감할 수 있도록 논리적인 흐름으로 구성해야 함
- 좋은 분석은 비즈니스 문제 이해, 데이터 탐색 및 전처리, 모델 구축 및 평가, 그리고 발견한 인사이트를 바탕으로 한 설득력 있는 스토리텔링을 포함함을 유념
- 분석 결과의 스토리텔링은 보통 기(문제 상황)-승(문제 심화)-전(분석 과정)-결(해결 및 제언)의 구조를 따른다


<br>
<br>

# 확인 문제

## **문제 1. 선형 회귀**

> **🧚 칼 피어슨의 아버지와 아들의 키 연구 결과를 바탕으로, 다음 선형 회귀식을 해석하세요.**  
> 칼 피어슨(Karl Pearson)은 아버지(X)와 아들(Y)의 키를 조사한 결과를 바탕으로 아래와 같은 선형 회귀식을 도출하였습니다. 아래의 선형 회귀식을 보고 기울기의 의미를 설명하세요. 
>  
> **ŷ = 33.73 + 0.516X**  
>   
> - **X**: 아버지의 키 (cm)  
> - **ŷ**: 아들의 예상 키 (cm)  

```
다른 조건이 일정하다면, 아버지의 키(X)가 1cm 커질 때마다 아들의 예상 키(ŷ)는 평균적으로 0.516cm 커진다는 것을 의미
```
---

## **문제 2. 로지스틱 회귀**  

> **🧚 다트비에서는 학생의 학업 성취도를 예측하기 위해 다항 로지스틱 회귀 분석을 수행하였습니다. 학업 성취도(Y)는 ‘낮음’, ‘보통’, ‘높음’ 3가지 범주로 구분되며, 독립 변수는 주당 공부 시간(Study Hours)과 출석률(Attendance Rate)입니다. 단, 기준범주는 '낮음' 입니다.**   

| 변수 | Odds Ratio Estimates | 95% Wald Confidence Limits |  
|------|----------------------|--------------------------|  
| Study Hours | **2.34** | (1.89, 2.88) |  
| Attendance Rate | **3.87** | (2.92, 5.13) |  

> 🔍 Q1. Odds Ratio Estimates(오즈비, OR)의 의미를 해석하세요.

<!--변수 Study Hours의 오즈비 값이 2.34라는 것과 Attendance Rate의 오즈비 값이 3.87이라는 것이 각각 무엇을 의미하는지 구체적으로 생각해보세요.-->

```
- 공부 시간이 많을수록 학업 성취도가 높아질 가능성이 약 2.34배 커진다
- 출석률이 높을수록 학업 성취도가 높아질 가능성이 약 3.87배 커진다
```

> 🔍 Q2. 95% Wald Confidence Limits의 의미를 설명하세요.
<!--각 변수의 신뢰구간에 제시된 수치가 의미하는 바를 생각해보세요.-->

```
- 주당 공부 시간의 실제 오즈비가 해당 구간(1.89에서 2.88 사이)에 있을 것으로 95% 신뢰
- 출석률의 실제 오즈비가 해당 구간(2.92에서 5.13 사이)에 있을 것으로 95% 신뢰
```

--------------------------------------------------------------------------------

> 🔍 Q3. 이 분석을 기반으로 학업 성취도를 향상시키기 위한 전략을 제안하세요.
<!--Study Hours와 Attendance Rate 중 어느 변수가 학업 성취도에 더 큰 영향을 미치는지를 고려하여, 학업 성취도를 향상시키기 위한 효과적인 전략을 구체적으로 제시해보세요.-->

```
- 출석률 향상에 최우선 집중
  - 출석률이 학업 성취도에 가장 큰 영향을 미치는 변수이기에, 학생들의 출석률을 높이기 위한 정책이나 프로그램을 최우선적으로 추진해야 함
- 주당 공부 시간 증진 노력 병행
  - 출석률만큼은 아니지만 주당 공부 시간도 학업 성취도에 유의미한 긍정적 영향을 미치기에, 학생들이 공부 시간을 효율적으로 활용하고 늘릴 수 있도록 지원하는 프로그램도 병행하면 좋을 듯 합니다
- 두 변수의 상호작용 고려
  - 실제 전략 수립 시에는 출석과 공부 시간이 서로 영향을 미칠 수도 있다는 점을 고려하여 통합적으로 접근하기
```

---


## **문제 3. k-means 클러스터링**

> **🧚 선교는 고객을 유사한 그룹으로 분류하기 위해 k-means 클러스터링을 적용했습니다. 초기에는 3개의 군집으로 설정했지만, 결과가 만족스럽지 않았습니다. 선교가 최적의 군집 수를 찾기 위해 사용할 수 있는 방법을 한 가지 이상 제시하고 설명하세요.**

```
- 엘보우 기법
  - 엘보우 기법은 다양한 k 값에 대해 클러스터링을 수행하고, 각 k 값에 해당하는 관성 값을 계산하는 방법
    - k 값의 증가에 따른 관성 값의 변화를 그래프로 시각화 -> 일반적으로 k가 증가할수록 관성 값은 감소
    - 그래프에서 관성 값의 감소율이 급격히 줄어들어 완만해지기 시작하는 엘보우 형태의 지점을 찾는다

### 🎉 수고하셨습니다.
