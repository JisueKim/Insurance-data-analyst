

# 시계열 분석

### 시계열 데이터 

: 시간의 흐름에 따라 관찰된 데이터

1. 연속(continouse) 시계열 : 자료가 연속적으로 생성, 실제로 많은 시계열들이 연속적으로 생성 됨. 

2. 이산(discrete) 시계열 : 이산적 시점에서 자료가 생성, 일정한 시차를 두고 관측, 이산시계열의 형태를 지니느 경우가 많음. 

   -> 계열자료를 분석할 때, 관측시점들 간의 시차(time lag)가 중요한 역할을 함

* **정상성 시계열** : 시점에 상관없이 시계열 특성이 일정 (트렌드와 분산이 불변)

  - 항상 그 평균값으로 회귀하려는 경향. 평균값 주변에서의 변동은 대체로 일정한 폭을 갖음 

  - 정상시계열이 아닌 경우 특정기간의 시계열 자료로부터 얻은 정보를 다른 시기로 일반화 할 수 없음. 
  - **정상성** 만족하기 위한 특징 

  ​     1) 평균값은 시간 t 에 관계없이 일정하다. 

  ​     2) 분산값은 시간 t 에 관계없이 일정하다. 

  ​     3) 공분산은 시간 t 에 의존하지 않고 오직 시차에만 의존, 실제 어느 시점 t, s 에는 의존하지 않는다.  

* **비정상성 시계열** : 자연상태의 데이터, 정상데이터로 변화하여 분석 (트렌드 혹은 분산이 변화)

  주어진 자료가 폭발적으로 증가하는 추세이면

   i) **평균**이 일정하지 않는 경우 

   ii) 시간에 따라 **분산**이 변하는 경우

   비정상시계열로 판단

* **비정상 시계열의 정상화**

  1) 평균이 일정하지 않은 경우, 원시계열에 **차분**하면 정상시계열.

  2) 계절성을 갖는 비정상시계열은 정상시계열로 바꿀 때 **계절차분** 사용 

  2) 분산이 일정하지 않은 경우, 원시계열에 자연로그(**변환**) 를 취하면 정상 시계열. 

* **차분(Difference)** : 현시점 자료 - 전시점 자료 (관측치 사이)

  1) 일반차분 (regular difference) : 바로 전 시점의 자료를 빼는 것 

  2) 계절차분 (seasonal difference) : 여러 시점 전의 자료를 빼는 것 

### 시계열 분석 

 시계열 자료를 분석, 현상을 시간에 따라 추적하여 현상에 대한 풍부한 사실을 평가하는 것이 가능하게 하는 것이 목적 

 불규칙성을 가지는 시계열 데이터에 특정한 기법이나 모델을 적용하여 규칙적 패턴을 적용 혹은 톄측 할 수 있도록 하는 것. 

<img src="https://github.com/JisueKim/DataAnalyst/blob/master/images/arima6.png?raw=true" alt="arima6.png" style="zoom: 50%;" />

​                                                   [그림참고] https://www.analyticsvidhya.com/

1. **미래의 값을 예측** 

   - 경제학자 = 금융시장 예측
   - 도시계획자 = 미래 교통수요 예측 
   - 기업 = 미래 시장 수요 예측 
   - 다양한 분야에서 예측하는 것에 사용 

2. **시계열 자료 특성 파악**

   : 경향, 주기, 계절성, 불규칙성 등 
   
3.  불규칙성 띠는 시계열 데이터에 규칙성을 부여하는 방법 AR, MA, ARMA, ARIMA 가장 널리 알려져 있다. 

   최근에 딥러닝을 이용하여 시계열 데이터의 연속성을 기계 스스로 찾아내도록 하는 방법이 더 좋은 성능을 내고 있다. 가장 대표적인 것이 LSTM 이라는 RNN 종류의 네트워크인데, 이전 상태를 꽤나 오랫동안 기억하면서 순환적인 네트원크의 파라미터를 자동적으로 학습하는 기특한 녀석이다. 시계열 모델을 제대로 공부하기 위하여 통계적 모델링 기법이나 마르코프 기법을 이해하는 것이 더욱 도움이 된다고 생각한다. 이에 대한 내용이 학습 된 후에 딥러닝을 제대로 이해할 수 있을 것 같다. 

### 시계열분석 모델 

* **자기 회귀 모델 (AR. AutoRegression model)**

  : 과거와 현재의 자신과의 관계를 정의. 이전 관측값(과거)이 이후 관측값(현재) 영향을 주는 원리를 사용하므로 **Z** 를 활용 

   현 시점의 시계열 자료에 몇 번째 전 자료까지 영향을 주는 지 알아내는 데 있음. 
  
  <img src="https://github.com/JisueKim/DataAnalyst/blob/master/images/arima1.png?raw=true" alt="arima1.png" style="zoom:33%;" />

​       1) 파이(p) - p 시점이 현재에 어느 정도 영향을 주는지를 나타내는 모수 

​       2) Z(t) - 현재 시점 

​       3) **백색잡음(white noise)** 는 일반적인 정규분포(평균 0, 분산 1)에서 도출된  random noise 값 

​         - 불규칙 데이터 정성화시키는 가장 효율적인 방법은 시계열 변수들을 Whitening(일종의 정규화) 시키는 것. 

​         - 백색잡음으로 구성된 항들의 평균과 분산은 일정하며, 변수들간 공분산과 자기상관은 정상성 조건으로 만족하게 된다. 

​         - 시계열의 평균이 0 이고, 분산이 일정한 값이고, 자기공분산이 0 인 경우를 백색잡음 과정이라하고 시계열 분석의 **오차항**

​         - 시계열 간 확률적 독립인 경우 [**강한 백색 잡음 과정**]

​         - 정규 분포인 경우 [**가우시안 백색 잡음 과정**]         

​       4)  p 에 특정한 숫자 n 를 대입하여 n 이전의 시점부터 회귀를 하고 싶으면 AR(n) 으로 쓴다. 

​       5) **자기상관함수 (ACF)**는 빠르게 감소, **부분자기함수 (PACF)**는 어느 시점에서 절단점이 존재 

​        : 자기상관함수 (ACF) = 상관계수 k를 함수 형태로 표시함. 



**자기 회기모델은 자신의 최신 과거에 기반한 변동 루틴을 파악하기 적합한 방식. 과거를 들여다보는 윈도우 밖에서 트렌드가 위아래롤 변동하는 경우는 매우 부적합한 방식. 이 경우는 MA(Moving Average)모델이 적합**

* **이동 평균 모델(MA, Moving Average model)**

  *트렌드(평균 혹은 시계열 그래프에서 y값)가 변화하는 상황에서 적합한 회귀모델*
  
  : **이동 평균 모델(MA)** 은 과거와 현재 자신의 오차와의 관계를 정의. AR의 Z가 오차항인 알파로 바뀐 점이 차이. 
  
  시계열이 같은 시점의 백색잡음과 바로 전 시점의 백색잡음의 결합으로 이뤄진 모형 
  
  이전항의 '오차' 에서 현재 항의 상태를 추론하겠다는 의미 

<img src="https://github.com/JisueKim/DataAnalyst/blob/master/images/arima2.png?raw=true" alt="arima2.png" style="zoom:33%;" />

​        : AR 과 MR 결합하면 **ARMA** 모델인데, 이전항의 상태와 오차에서 현재의 상태를 추론한다. AR, MA 두가지 관점에서 1.      

​        윈도우 이전만큼의 과거를 참고하는 것을 ARMA(1,1) 표기, 2 윈도우 이전만큼 과거를 참고할 때도 ARMA(2,2)로 표기 



* **자기회귀 누적 이동평균 모델 (ARIMA, AutoRegreesive intergrated Moving Average model)**

  : 현재와 추세간의 관계를 정의. ARMA 모델이 불규칙 시계열 데이터를 잘 예측하지 못하는 한계를 보완위해 등장, 

  차분과 변환을 통해 AR, MA, ARMA 등으로 정상화 할 수 있다. (차분을 통해 whitening효과)

  <img src="https://github.com/JisueKim/DataAnalyst/blob/master/images/arima3.png?raw=true" alt="arima3.png" style="zoom:33%;" />

​       : ARIMA 모델은 **ARIMA(p,d,q)** 으로 표현하고, 순서대로 **AR  모형 차수, 차분, MA 모형 차수** 의미한다. 

​        이 차수의 최적 차수는 **자기 상관 함수(ACF), 편 자기 상관 함수(PACF)** 를 사용하여 찾는다. 

​        만약, ARIMA(1,2,1)이라면 AR 과 MA 를 1개만큼의 과거를 window 로 활용하고, 차분을 2 만큼 활용하는 것 

* **자기 상관 함수 (ACF, AutoCorrelation Function)**

  K 시간 단위로 구분된 시계열의 관측치 간 상관 관계 함수 즉, k가 1,2,3...일때  k단계 떨어진 데이터 점 쌍 간들의 상관 관계 

  점선으로 유의미한 상관과 유의미하지 않은 상관을 확인할 수 있는데, 선의 위쪽이 유의미한 값이다. 

  아래의 그래프에서는 절단갑 = 4 이고, ARIMA 모델에서 **MA 계수가 3개 (MA(3)) 필요할 것**  이라고 예상할 수 있다. 

   ARIMA(0,2) 모델에 해당됨 

  <img src="https://github.com/JisueKim/DataAnalyst/blob/master/images/arima4.png?raw=true" alt="arima4.png" style="zoom:50%;" />

* **부분(편) 자기 상관 함수 (Partial ACF)**

  : **부분 상관** 이란 두 확률 변수  X 와 Y 에 의해 다른 모든 변수들에 나타난 상관 관계를 설명하고 난 이후에도 여전히 남아있는 상관관계라고 할 수 있다. 

  편 자기 상관 함수(PACF) 는 자기 상관 함수와 마찬가지로 시계열 관측지 간 상관 관계 함수이고, 시차 k 에서의 k 단계만큼 떨어져 있는 모든 데이터 점들간의 상관 관계를 말한다. 

  PACF 도 역시 선 위쪽이 유의미한 값이다. 

  아래의 그래프에서  절단값은 = 2가 되며, **ARIMA 모델에서 AR 계수가 2개 (AR(2)) 필요할 것** 이라고 예상할 수 있다. ARMA(0,1)모형이다. 

<img src="https://github.com/JisueKim/DataAnalyst/blob/master/images/arima5.png?raw=true" alt="arima5.png" style="zoom:50%;" />

​        최적의 모델로 **가장 간단한 모델** 을 선택하거나 **AIC 점수가 가장 낮은 모델** 을 선택하면 된다 

​        예시 ) ARIMA(1,1,2) 일 때, 1차분 후 AR(1), MA(2), ARMA(1,2) 모델이 존재 



ACF(자기 상관 함수) : https://support.minitab.com/ko-kr/minitab/18/help-and-how-to/modeling-statistics/time-series/how-to/autocorrelation/interpret-the-results/autocorrelation-function-acf/

PACF(편 자기 상관 함수) : https://support.minitab.com/ko-kr/minitab/18/help-and-how-to/modeling-statistics/time-series/how-to/partial-autocorrelation/interpret-the-results/partial-autocorrelation-function-pacf/



* **Facebook Prophet 모델**

  Additive 모델이라는 모델링 방법에 기반하여 개량한 패키지로, 선형적이지 않은 시계열 데이터의 트렌드성을 (연간/월간/일간) 단위로 쉽게 찾아내도록 해주는 것에 초점이 맞추어져 있다. 여기서 Additive 모델(가법적 모델)이란 비선형적 회귀분석을 의미한다.

  

  잠시 Additive 모델에 대한 설명을 하겠다. Additive 모델은 선형회귀에서의 단점을 극복하기 위해 개량된 방법이라고 볼 수 있다. 일반적인 선형회귀는 다음과 같은 수식에서 부터 베타값들을 학습하는 것이었다. 

  

  ![prophet1.gif](https://github.com/JisueKim/DataAnalyst/blob/master/images/prophet1.gif?raw=true)

  

  하지만 대부분의 real world 모델은, 선형성을 띠는 경우가 드물다. 따라서 회귀 분석에 비선형적 성질을 학습시키기 위해 polynomial regression(다차항 회귀 분석)방법을 도입하기도 하고, Smoothing 방법으로 과적합을 피하는 비선형 모델을 도입하기도 한다. 그외에도 다양한 회귀분석의 변형적 방법들이 존재한다. 하지만 Additive model은 각 변수마다 비선형적 적합을 가능하게 하는 함수들을 적용하는 것이다. 수식을 살펴보면 다음과 같다.

  

  ![prophet2.gif](https://github.com/JisueKim/DataAnalyst/blob/master/images/prophet2.gif?raw=true)

  

  위 식에서 각 변수 X_ij를 각각의 함수 f_j에 부여하고 있는 것을 볼 수 있고, 이것을 가법적인(Additive model) 모델이라고 한다. 단순히 이러한 가법적인 모델을 적용하는 것을 넘어서, 일반적으로는 함수 f_j 마다 1차원의 Smoother를 적용한다. 이를 통해 제한된 클래스의 비모수 회귀를 적용하는 것이다. 다른 말로 하면, 함수들이 overfit 되지 않게 리미터를 걸어주는 역할이라고 볼수 있다.

  

  가법적인 회귀모델은 기존 선형회귀 모델의 장점인 변수에 대한 높은 설명력이라는 부분을 고스란히 가져오면서도, 예측력이 매우 높은 비선형적 결합 모델이라는 장점도 포함한다. 하지만 이 모델의 단점은 변수간의 상호작용, 즉 regression에서의 cross-production 피처를 잡아내기 힘들다는 것이다. 물론 이에 대한 극복 방법이 충분히 연구되긴 했지만, 일반적으로 변수간의 상호작용이 중요한 경우에는 이 기본 모델을 적용하지는 않는 것 같다.

  

  다시 돌아와서, Facebook의 Prophet 모델은 Additive 방식의 regression을 Facebook의 데이터 사이언스들이 시계열 예측에 최적화된 형태로 개량한 모델이라고 정의내릴 수 있다. 동시에 ARIMA와 같은 Generative 모델의 장점도 활용하고 있다고 설명되어 있다. 즉, GAM(Generative Additive Model) 모델(일반적으로 GAM 모델은 Generalized Additive Model을 의미한다)의 시계열 최적화 응용 모델이라는 것이다. 자세한 내용은 https://peerj.com/preprints/3190/ 의 논문을 참고하자.

































