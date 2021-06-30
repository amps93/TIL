# ARIMA



## ARIMA란?

* ARIMA는 Autoregressive Integrated Moving Average의 약자로, Autoregressive(AR)는 자기회귀모형을 의미하고, Moving Average(MA)는 이동평균모형을 의미한다.

  * **AR**: 자기회귀(Autoregression). 이전 관측값의 오차항이 이후 관측값에 영향을 주는 모형이다. 아래 식은 제일 기본적인 AR(1) 식으로, theta는 자기상관계수, epsilon은 white noise이다. Time lag은 1이 될수도 있고 그 이상이 될 수도 있다.
    ![eq_ar1](https://latex.codecogs.com/gif.latex?AR%281%29%3A%20X_%7Bt%7D%3D%5Cphi%20X_%7Bt-1%7D+%5Cepsilon_%7Bt%7D)
  * **I**: Intgrated. 누적을 의미하는 것으로, 차분을 이용하는 시계열모형들에 붙이는 표현이라고 생각하면 편하다.
  * **MA**: 이동평균(Moving Average). 관측값이 이전의 연속적인 오차항의 영향을 받는다는 모형이다. 아래 식은 가장 기본적인 MA(1) 모형을 나타낸 식으로, beta는 이동평균계수, epsilon은 t시점의 오차항이다.
    ![eq_ma1](https://latex.codecogs.com/gif.latex?MA%281%29%3A%20X_%7Bt%7D%3D%5Cepsilon_%7Bt%7D-%5Cbeta_%7B1%7D%20%5Cepsilon_%7Bt-1%7D)

* 현실에 존재하는 시계열자료는 불안정(Non-stationary)한 경우가 많다. 그런데 AR(p), MA(q) 모형이나, 이 둘을 합한 ARMA(p, q)모형으로는 이러한 불안정성을 설명할 수가 없다.
  따라서 모형 그 자체에 이러한 비정상성을 제거하는 과정을 포함한것이 ARIMA모형이며 **ARIMA(p, d, q)**로 표현한다.
  ![eq_arima](https://latex.codecogs.com/gif.latex?%5Chat%7By%7D_%7Bt%7D%3D%5Cmu%20+%5Cphi_%7B1%7Dy_%7Bt-1%7D+...+%5Cphi_%7Bp%7Dy_%7Bt-p%7D-%5Cbeta_%7B1%7D%5Cepsilon_%7Bt-1%7D-...-%5Cbeta_%7Bq%7D%5Cepsilon_%7Bt-q%7D)

  ![eq_arima_mu](https://latex.codecogs.com/gif.latex?%5Cmu%3D%20constant)
  ![eq_arima_ar](https://latex.codecogs.com/gif.latex?%5Cphi_%7B1%7Dy_%7Bt-1%7D+...+%5Cphi_%7Bp%7Dy_%7Bt-p%7D%20%3A%20AR%20terms%20%28lagged%20values%20of%20y%29)
  ![eq_arima_ma](https://latex.codecogs.com/gif.latex?-%5Cbeta_%7B1%7D%5Cepsilon_%7Bt-1%7D-...-%5Cbeta_%7Bq%7D%5Cepsilon_%7Bt-q%7D%20%3A%20MA%20terms%20%28lagged%20values%20of%20y%29)
  ![eq_arima_d0](https://latex.codecogs.com/gif.latex?%5Chat%7By%7D_%7Bt%7D%3DY_%7Bt%7D%2C%5C%20if%5C%20d%3D0)
  ![eq_arima_d1](https://latex.codecogs.com/gif.latex?%5Chat%7By%7D_%7Bt%7D%3DY_%7Bt%7D-Y_%7Bt-1%7D%2C%5C%20if%5C%20d%3D1)
  ![eq_arima_d2](https://latex.codecogs.com/gif.latex?%5Chat%7By%7D_%7Bt%7D%3D%5Cleft%20%28Y_%7Bt%7D-Y_%7Bt-1%7D%20%5Cright%20%29-%5Cleft%20%28Y_%7Bt-1%7D-Y_%7Bt-2%7D%20%5Cright%20%29%2C%5C%20if%5C%20d%3D2)

  위와 같은 특징에 따라 ARMIA(p, d, q)는 AR, MA, ARMA를 모두 표현할 수 있다.

  - AR(p) = ARIMA(p, 0, 0)
  - MA(q) = ARIMA(0, 0, q)
  - ARMA(p, q) = ARIMA(p, 0, q)



## ARIMA 모수 설정

* ARIMA의 모수는 크게 3가지가 있다. **AR모형의 Lag을 의미하는 p, MA모형의 Lag을 의미하는 q, 차분(Diffrence)횟수를 의미하는 d** 가 그것이다. 보통은 p, d, q의 순서로 쓴다.

* p와 d, q는 어떻게 정해야 할까? 

  * ACF plot와 PACF plot을 통해 AR 및 MA의 모수를 추정할 수 있다.
    * ACF(Autocorrelation function) : Lag에 따른 관측치들 사이의 관련성을 측정하는 함수
      ![eq_acf](https://latex.codecogs.com/gif.latex?%5Crho_%7Bk%7D%3D%5Cfrac%7BCov%28y_%7Bt%7D%2C%20y_%7Bt+k%7D%29%7D%7BVar%28y_%7Bt%7D%29%7D)
    * PACF(Partial autocorrelation function) : k 이외의 모든 다른 시점 관측치의 영향력을 배제하고![eq_yt](https://latex.codecogs.com/gif.latex?y_%7Bt%7D)와 ![eq_ytk](https://latex.codecogs.com/gif.latex?y_%7Bt-k%7D) 두 관측치의 관련성을 측정하는 함수
      ![eq_pacf](https://latex.codecogs.com/gif.latex?%5Cphi_%7Bkk%7D%3Dcorr%28y_%7Bt%7D%2C%20y_%7Bt-k%7D%5Cmid%20y_%7Bt-1%7D%2C%20y_%7Bt-2%7D%2C%20...%2C%20y_%7Bt-k+1%7D%29)

  * 시계열 데이터가 AR의 특성을 띄는 경우, ACF는 천천히 감소하고 PACF는 처음 시차를 제외하고 급격히 감소한다.
  * 반대로, MA의 특성을 띄는 경우 ACF는 급격히 감소하고 PACF는 천천히 감소한다.
  * 급격히 감소하는 시차를 각 AR과 MA 모형의 모수(p, q)로 사용할 수 있다. 또한 데이터를 차분하여 ACF 및 PACF 계산함으로써 적절한 차분횟수까지 구할 수 있다.
