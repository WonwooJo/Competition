# 빅콘테스트 챔피언리그

> - 2020년 빅콘테스트의 데이터 분석 분야 중 챔피언리그에 참가하였습니다.
>
> - 2번째 공모전 참가이기에 많이 부족할 수 있습니다.
>
> - 이번 공모전의 개인적인 목표는 프로젝트를 완벽하게 수행한다기보단, 전처리에서 예측까지 이루어지는 한 사이클을 무사히 마치고, 부족한 점을 보완하는데 있었습니다.



## 목표

- 2019년 NS SHOP+ 편성데이터와 판매 실적을 통해 2020년 6월 판매 실적 예측 및 방송 편성 최적화 방안 제시

- 2020-09-28 15:00 제출



## 진행 과정

### 1. Data Preprocessing & EDA

- NS SHOP+에서 제공한 내부데이터(판매 실적, 시청률)와 외부데이터(날씨, 소비자심리지수) 전처리
  - 데이터가 굉장히 방대했기에 몇 몇 결측값은 단순 대치 혹은 비조건부 평균 대치를 하였다.
  - 이 과정에서 **간과했던 부분**은 이상치 인식 방법을 정하지 아니한 것이었다. *~~잘 기억하자.~~*
    - 1) ESD(Extreme Studentized Deviation) 활용 (평균으로부터 3σ 떨어진 값)
    - 2) 기하평균(GM) 활용 (기하평균 -2.5 x σ < data < 기하평균 + 2.5 x σ)
    - 3) IQR 활용 (Box plot IQR outer fence 밖에 있는 값 제거)
    - 4) 윈터라이징(상위 99%초과 → 99%값으로 , 하위 1% 미만 → 1%값으로 대체)
  - 하기 사진과 같이 Pearson 상관 계수가 너무 작았기때문에 Feature Engneering을 통해 연관성이 높도록 데이터를 가공했어야했는데, 아직 많이 부족했다.
    - 1) Indicator Variables
    - 2) Interaction Features
    - 3) Feature Representation
    - 4) External Data
    - 5) Error Analysis - Post Modeling

![image-20201006233349884](C:\Users\joww0\AppData\Roaming\Typora\typora-user-images\image-20201006233349884.png)

### 2. Modeling & Evaluation

- 시계열 데이터이기에 처음에는 ARIMA와 같은 모델을 사용하고자 했으나 연관성이 너무 적고, 급격한 비선형적 변화에 취약하다는 결론에 도달하여 Random Forest 모델을 활용하여 예측을 진행하였고, gridCV로 최적의 Random Forest 계수를 찾았다.