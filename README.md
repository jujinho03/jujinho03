# 주진호 | 금융 데이터 분석 · 모델 검증

데이터사이언스 전공. 신용리스크·유동성·금융 시계열을 중심으로 모형의 가정과 결과의 해석 범위를 검증. 대출 심사 우선순위와 재무 권고가 달라지는 조건을 공개 코드와 결과표로 정리.

## 대표 프로젝트

### 1. [보험펜(BohumPen) · 보험 청구지원 AI 평가](portfolio/bohumpen.md)

여행자보험 청구지원 AI가 정보가 부족한 사고를 확정하거나 불필요한 담보·서류를 제안하는지 점검. FinPoint 팀장으로 청구지원 골드셋·안전 평가와 화면 문구 검수 담당. 합성 시나리오 40건 중 37건(92.5%)이 허용 기준을 충족. 저장된 분류 예측을 재사용한 개발 평가로, 실제 보험금 지급의 정확도를 측정한 것은 아님.

[내 기여](portfolio/bohumpen.md#contribution) · [평가 설계](portfolio/bohumpen.md#evaluation) · [실패 사례](portfolio/bohumpen.md#failure) · [팀 저장소](https://github.com/k0ng-min/2026_finance_ai_challenge)

### 2. [플랜브릿지(PlanBridge) · 현금흐름과 유동성 리스크](portfolio/planbridge.md)

CPA 2차 수험생이 첫 급여를 받기까지의 소득 공백을 가상 사례로 분석. 3인 팀에서 팀장과 재무분석을 맡아 가상 고객의 현금흐름 가정, 대안 비교 기준과 조건부 권고를 정리. 취업 전환의 첫 급여만 3개월 늦추면 60개월 조건부 할인 현금흐름 지표는 5,968.6만 원으로, 근로 병행 기본값 6,062.2만 원보다 낮음. 계약과 첫 입금이 확인되는 경우 근로 병행을 우선 검토.

[분석과 내 기여](portfolio/planbridge.md) · [급여 지연 민감도 원본](https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/outputs/tables/sensitivity.json)

### 3. [Home Credit · 신용리스크와 심사 우선순위](https://github.com/jujinho03/home-credit-default-risk)

팀 과제에서 데이터 품질·누수 점검과 모델 검증 담당. 개인 재구축 과정에서 변수 중요도 해석을 재검증. 층화 홀드아웃에서 위험점수 상위 10% 집단의 부도율은 26.48%로 전체의 3.28배. 대출 심사 우선순위 검토에 해당하며, 미래 성과나 손실 절감액을 추정한 결과는 아님.

[검증 과정과 임계값 비교](https://github.com/jujinho03/home-credit-default-risk/blob/c753352f588a20c7f484e25eeb16c61a72364ef6/docs/findings.md)

### 4. [KOSPI · 금융 시계열과 허위회귀 진단](https://github.com/jujinho03/kospi-macro-spurious-regression)

팀 과제에서 데이터 검증과 시계열 진단에 참여. 이후 분석 전 과정을 개인 프로젝트로 재구축. 수준 회귀의 학습 R²는 0.8103이었으나 비정상성·자기상관이 나타났고 공적분을 뒷받침할 근거는 제한적인 것으로 보임. 1차 차분 결과는 단기 동시점 연관성으로 한정해 해석. 인과관계나 투자 예측을 입증한 것은 아님.

[시계열 진단과 시점 분리 검증](https://github.com/jujinho03/kospi-macro-spurious-regression/blob/ddd4f114fa9fcc9087138b0dbb3f8b20b5ab5cde/docs/findings.md)

## 추가 프로젝트

- [서울시 공공자전거 · 시계열 수요 예측](https://github.com/jujinho03/seoul-bike-demand-forecasting) — 팀 과제에서 전처리 담당. 이후 GPS 기반 3개 군집과 시간순 검증 절차를 개인 프로젝트로 재구축. 2024년 4분기 동일 테스트 구간에서 LightGBM의 Macro RMSE가 SARIMA 대비 58.6% 낮았음. [비교 결과](https://github.com/jujinho03/seoul-bike-demand-forecasting/blob/acc34adfef41548cd36f3e52ae1397494c40390c/docs/findings.md)
- [VeriMod · AI 판정 기록의 무결성 검증](https://github.com/jujinho03/verimod) — HTTP 451 팀장으로 AI 데이터 분할·누수 점검, 모델 평가와 오분류 분석 담당. 팀은 판정 영수증 2건을 Base Sepolia에서 대조했음. 기록 무결성 시연이며 AI 판정의 정확성을 입증하지 않음. [모델 카드](https://github.com/jujinho03/verimod/blob/3e1d97b18ec4d1e0d96d0f951e154d8b3b138c74/docs/model-card.md) · [공개 검증 기록](https://github.com/jujinho03/verimod/blob/3e1d97b18ec4d1e0d96d0f951e154d8b3b138c74/docs/handoffs/w4-anchored-epoch-public/20261020-r01/README.md)

분석 도구 · Python · pandas · scikit-learn · LightGBM · Jupyter
