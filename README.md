# 현대자동차 승용차(PC,RV차량) 판매량 예측

## 1. 프로젝트 개요 (Project Overview)
- **주제:** 머신러닝 기반의 하이브리드 모델(Prophet + XGBoost)을 활용한 국내 승용차 판매량 예측
- **목표:** 거시경제 지표와 과거 판매 패턴을 분석하여 향후 판매량을 정교하게 예측, 재고 관리 및 마케팅 전략 수립에 기여
- **기간:** 2025.09 ~ 2025.12
- **참여 인원:** 3명

## 2. 접근 방법 (Methodology) : Hybrid Residual Learning
단일 모델의 한계와 데이터 수집의 양이 부족함을 극복하기 위해 **시계열 모델과 트리 기반 모델을 결합**하여 예측 성능을 극대화했습니다.

1.  **Trend & Seasonality (Prophet):**
    - 데이터의 양이 절대적으로 부족하므로 LSTM을 사용해 보았으나 차원의 저주와 같은 과적합 발생으로 데이터 양이 부족할 때도 사용할 수 있도록 Prophet모델을 사용했습니다.

2.  **Residual Correction (XGBoost):**
    - Prophet이 설명하지 못한 **잔차(Residual, 오차)**를 `XGBoost`로 추가 학습하여 예측값을 보정했습니다.
    - 이를 통해 단순 시계열 모델이 놓칠 수 있는 외부 변수의 영향을 반영했습니다.

## 3. 데이터 및 주요 변수 (Data & Features)
수집한 데이터 변수 중 가장 영향력이 높을 것으로 보이는 모델의 설명력을 높일 수 있도록 랜덤 포레스트(RandomForest)의 **Feature Importance**를 통해 예측에 가장 영향력이 큰 Top 5 변수를 선정하여 모델에 적용했습니다.

- **Target:** 국내 승용차(PC차량) 판매량
- **Key Features:**
  1. **자동차 수리비:** 차량 유지비용과 구매 심리 연관성 분석
  2. **자동차 등록대수 현황:** 시장 포화도 및 교체 수요 파악
  3. **소비자 심리 지수 (CSI):** 경제 상황에 따른 구매 의사 반영
  4. **환율:** 수출입 이슈 및 경제 변동성 반영
  5. **국내 RV 차량 판매량:** 차종 간의 간섭 효과 고려

## 4. 분석 결과 (Results)
- **성능 지표:** RMSE (Root Mean Squared Error) **4,295** 달성 (검증 데이터 기준)
- **시각화:** 2025년의 판매량 피크(Peak) 구간을 포함하여 전반적으로 현대자동차 판매량과 비슷한 추세를 보여주었음.
- **성과 및 한계:** 기존 단일 Prophet 모델 대비 잔차 보정을 통해 예측 오차를 개선하였으나, 기업 내부 정보를 알 수 없었기에 하반기에 예측 성능이 매우 떨어짐을 보여줌.

## 5. 사용 기술 (Tech Stack)
- **Language:** Python
- **Data Analysis:** Pandas, NumPy
- **Machine Learning:** Facebook Prophet, XGBoost, Scikit-learn (RandomForest)
- **Visualization:** Matplotlib
- **Environment:** Google Colab

---
*이 프로젝트는 캡스톤 디자인의 일환으로 수행되었으며, 데이터 수집부터 전처리, 하이브리드 모델링 구현까지 전 과정을 주도적으로 수행했습니다.*
