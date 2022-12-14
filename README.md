# 2022-06-Prevention-of-a-cold-based-on-the-daily-temperature-difference-prediction
일교차 예방에 따른 감기예방을 주제로 시계열 분석

### 주제선정 배경
실제로 코로나 19 대 유행 시기를 보면 1차 대유행과 2차 대유행 발생 시기가 환절기에 나타난것을 확인하였다.
또한 환절기에는 코로나 뿐만 아니라 감기 등등 여러 호흡기 질환에 취약합니다.
때문에 환절기 시기에 늘어난 감기 환자의 추세를 파악하며,
더불어 환절기 예측을 통한 여러 질병을 예방하고자 위와같은 주제로 분석을 진행하였다.

### 데이터 설명
첫 번째, 데이터의 출처는 기상청으로 춘천의 2015년 1월 1일부터 2019년 12월 31일까지의 일별 기온, 풍속 기존의 변수들을 이용하여 창출해낸 체감온도로 칼럼이 구성되어 있으며, 12월 31일은 행의 개수가 하나이기때문에 일교차를 확인 할 수 없어 제거하였다.

두 번째, 국민건강보험공단이며 기간은 위와 같고, 춘천시 일별 감기 환자 데이터이며, 위 데이터를 통해 일교차를 구한 데이터입니다.

### 분석방법입니다. 

보통 시계열 분석을 할 때 사용하는 모형은 차분을 통한 ar값과 ma값의 모형을 합쳐 예측하는 방법인 ARIMA가 있고, ARIMA와는 달리 빈도가 높은 시계열 데이터도 설명할 수 있는 모형으로 TBATS가 있다.

본 프로젝트에서는 TBATS를 사용하였다.

왜냐하면 사용할 데이터는 일별 데이터이기 때문에 frequency를 365로 설정을 해야하지만, 
ARIMA는 frequency를 360까지 지원을 하기 때문에 일별 데이터를 분석하기에 부적합하다 생각하여 TBATS모형을 사용하였다.

### 분석 내용
그래프는, 1년 주기로 계절성이 나타나는 것을 확인할 수 있는, 일교차 데이터를 쿼리를 추출한 시각화입니다.

따라서 시계열을 계절성과 나머지 파트로 나눌 필요성이 있어 R의 decompose()함수를 이용하여  시계열 데이터를 분해하여 시각화 하였다.

그래프를 확인해보면, 결과는 약하게 계절성이 보이는 듯 하나 전과 비교하였을 때, 계절성이 크게 감소한것을 알 수 있다.

자기 상관 분석을 통해 이를 통해 ARIMA 모형의 P와 q를 결정할 수 있습니다.

한번 차분을 함으로서 ACF의 LAG가 1 이후로부터 정상성을 보인다는 것을 알 수 있으며,
차분 전에는 PACF의 LAG가 5 이후 일 때 부터 정상성을 이뤘다는 것을 볼 수 있었다.

하지만 앞서 설명한 바와 같이 주기가 1년이라는 기간이기 때문에 ARIMA 모형을 활용하여 시계열을 예측하는 것은 무리가있다.
따라서 다른 모형을 이용할 필요성이 있어, 1년 주기를 커버할 수 있는 모형인 TBATS라는 모형을 사용하게 되었고, 잘 예측할 수 있는 것을 확인 할 수 있었다.

분석 내용은 감기하고 일교차에 대한 상관분석을 진행하였다.
여러 상관 계수 중에서 대표적인 피어슨 상관 계수를 활용하여 상관계수를 구했는데 값은, P_value가 0.15라는 낮은 상관계수를 나타냅니다.

### 추후 활용 방안

추후 본 연구와 같은 예측을 통하여 기온에 따른 여행객 방문 수 예측에 따른 특정 물품 구매 등 여러 방안으로 사용 될 수 있을 것이다.
