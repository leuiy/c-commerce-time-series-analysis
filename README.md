# Is C-Commerce Growth Temporary or a Market Restructuring?
🇺🇸 [English](#english) | 🇰🇷 [한국어](#한국어)

---

## Live Reports / 분석 결과
https://leuiy.github.io/c-commerce-time-series-analysis/c-commerce_main/c-commerce_main.html

https://leuiy.github.io/c-commerce-time-series-analysis/structural_break_analysis/2014~2021.html

https://leuiy.github.io/c-commerce-time-series-analysis/structural_break_analysis/2022~2025.html

https://leuiy.github.io/c-commerce-time-series-analysis/structural_break_analysis/2022~2026Q1.html

---
## English

## Total Cross-Border Purchases → China-Origin Purchases → China's Market Share → Structural Dominance Diagnosis
A time series analysis examining whether the rapid growth of C-Commerce platforms (AliExpress, Temu) in the Korean cross-border shopping market represents a temporary trend or a structural market reorganization. Using quarterly KOSIS data across two analytical phases — full period (2014–2026Q1) and structural break sub-periods (2014–2021 / 2022–2025 / 2022–2026Q1).

## Study Overview — SARIMA-based Forecasting & Structural Break Analysis
- **Data**: KOSIS Online Shopping Trend Survey, 2014 Q1 – 2026 Q1, quarterly
- **Variables**: `total` (total cross-border purchases), `china` (China-origin purchases), `share` (derived variable: china ÷ total — modeled independently to avoid compounded forecast error from combining two separate model predictions)
- **Stationarity**: ADF Unit Root Test + KPSS Test → 1st-order + seasonal differencing
- **Decomposition**: Additive model selected via residual CV comparison
- **Model selection**: ACF/PACF → parameter significance test → auto.arima validation
- **Final models**:
  - `total` : SARIMA(0,1,0)(0,1,1)[4]
  - `china` : SARIMA(0,1,0)(0,1,0)[4]
  - `share` : SARIMA(1,1,0)(0,1,1)[4]
- **Residual diagnostics**: ACF², QQ-Plot, Ljung-Box test
- **Structural break analysis**: Data split by increased residual volatility in the China series post-2022

## Technologies
R: astsa, forecast, tseries, ggplot2

## Key Findings
- China-series outliers confirmed at 2023 Q3 & 2025 Q3 — aligned with AliExpress/Temu's aggressive Korean market entry; share-series outlier at 2020 Q2 attributed to COVID-19 (China recovered export volume faster than the U.S. and Europe)
- Full period forecast: `total` continues moderate upward trend; `china` enters a range-bound mature phase rather than explosive growth
- `share` forecast: despite plateauing absolute volume, China's market share is projected to **exceed 70% by 2027 Q2** — structural dominance, not just growth momentum
- Asymmetric trend: stable absolute volume + continuously rising share → C-Commerce is consolidating grip, not expanding outward
- **Post-2022 structural break**: both `total` and `china` reduce to SARIMA(0,1,0)(0,1,0) — a random walk — indicating high irregular volatility; `share`, however, maintains a persistent upward trend via SARIMA(1,1,0)(0,1,0)[4] - (2022~2025)
- 2026 Q1 anomaly: notable decline observed; whether a seasonal dip or trend inflection point requires 2–3 further quarters to determine

## Conclusion
- C-Commerce has transitioned from a quantitative growth phase to a structural dominance phase
- The Korean cross-border shopping market is forecast to reorganize further around C-Commerce platforms
- Domestic e-commerce players should abandon price-war competition and instead focus on irreplaceable value: fast logistics, quality guarantees, high-touch CS, and locally curated products

## My Contributions (2-member team)
- Primary: End-to-end implementation for `total` & `china` series (preprocessing → stationarity testing → model selection → forecasting → residual diagnostics), `share` derived variable engineering (china ÷ total) with independent SARIMA modeling rationale, all visualization, sub-period structural break analysis (2022–2025, 2022–2026 Q1)
- Supporting: `share` series modeling & diagnostics, sub-period analysis (2014–2021)

---

## 한국어
## 전체 직구액 → 중국 직구액 → 중국 직구 점유율 → 구조적 지배력 진단
알리익스프레스·테무로 대표되는 C-커머스의 국내 해외직구 시장 급성장이 일시적 현상인지, 구조적 시장 재편인지를 시계열 분석을 통해 파악한 프로젝트입니다. KOSIS 분기별 데이터를 활용하여 전체 기간(2014–2026Q1) 분석과 구조적 변화 구간 분리 분석(2014–2021 / 2022–2025 / 2022–2026Q1)을 2단계로 수행하였습니다.

## 연구 개요 — SARIMA 기반 예측 및 구조적 변화 구간 분석
- **데이터**: KOSIS 온라인쇼핑동향조사, 2014년 1분기 ~ 2026년 1분기, 분기별
- **변수**: `total` (전체 직구액), `china` (중국 직구액), `share` (파생변수: china ÷ total — 두 모형의 예측 오차가 결합 시 점유율 변동성이 증폭되는 문제를 방지하기 위해 독립 시계열 모형으로 별도 구축)
- **정상성 검정**: ADF 단위근 검정 + KPSS 검정 → 1차 차분 + 계절 차분
- **시계열 분해**: 잔차 CV 비교를 통해 가법 모형 채택
- **모형 선정**: ACF/PACF 탐색 → 모수 유의성 검정 → auto.arima 검증
- **최종 모형**:
  - `total` : SARIMA(0,1,0)(0,1,1)[4]
  - `china` : SARIMA(0,1,0)(0,1,0)[4]
  - `share` : SARIMA(1,1,0)(0,1,1)[4]
- **잔차 진단**: ACF², QQ-Plot, Ljung-Box 검정
- **구조적 변화 분석**: 2022년 이후 중국 직구 잔차의 변동성 증가를 반영하여 2022년을 기점으로 데이터 분할 후 재분석

## 사용 기술
R: astsa, forecast, tseries, ggplot2

## 주요 결과
- china 시계열 이상값: 2023 Q3 & 2025 Q3 확인 — 알리익스프레스·테무의 공격적 한국 시장 진입 시기('알리 쇼크')와 일치; share 이상값: 2020 Q2 — 코로나19로 인한 외생적 충격 (미국·유럽 대비 중국의 수출 회복 속도가 빠르게 나타남)
- 전체 기간 예측: `total`은 완만한 상승세 유지; `china`는 폭발적 성장이 아닌 박스권 성숙기 진입
- `share` 예측: 거래액이 안정세임에도 **2027년 2분기 70% 돌파** 전망 — 양적 성장이 아닌 구조적 지배의 심화
- 비대칭적 추세: 거래액 안정 + 점유율 지속 상승 → C-커머스는 외연 확장이 아닌 내부 점유율 공고화 단계 진입
- **2022년 이후 구조 변화**: `total`·`china` 모두 SARIMA(0,1,0)(0,1,0) — 랜덤워크로 도출되어 높은 불규칙 변동성 확인; `share`는 SARIMA(1,1,0)(0,1,0)[4]로 상승 추세 유지 - (2022~2025)
- 2026 Q1 이상값: 뚜렷한 하락세 관찰; 계절적 이상치 혹은 추세 전환점 여부는 향후 2~3분기 추이로 판단 필요

## 결론
- C-커머스는 양적 성장 단계에서 구조적 지배 단계로 전환 중
- 국내 해외직구 시장은 향후 더욱 C-커머스 중심으로 재편될 전망
- 국내 이커머스 기업은 가격 경쟁에서 벗어나 빠른 배송·품질 보증·정교한 CS·국내 소비자 특화 상품 등 대체 불가능한 가치에 집중해야 함

## 내 역할 (2인 구성)
- 메인: `total`·`china` 전반적 코드 구현 (전처리 → 정상성 검정 → 모형 선정 → 예측 → 잔차 진단), `share` 파생변수 설계 (china ÷ total) 및 독립 SARIMA 모형 구축 근거 수립, 전체 시각화, 구간 분리 재분석 (2022–2025, 2022–2026 Q1)
- 보조: `share` 시계열 모형 구현 및 잔차 진단, 구간 분석 (2014–2021)
