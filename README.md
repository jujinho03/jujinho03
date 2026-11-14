# 주진호 | 금융 데이터 분석 · 모델 검증

데이터를 먼저 의심하고, 검증 가능한 결과로 정리합니다.

금융 데이터 분석을 목표로 하는 데이터사이언스 전공자로, 신용리스크·금융 시계열·청구지원 AI에서 데이터 누수와 모델 해석의 오류를 점검했습니다.

## 대표 프로젝트

### 1. [보험펜(BohumPen) — 금융 AI 평가와 청구지원](portfolio/bohumpen.md)

사고 후 검토할 담보·서류와 약관 근거를 찾는 청구지원 서비스입니다. FinPoint 팀장으로 청구지원 E2E 골드셋·안전 평가와 화면 문구 정합화를 담당했습니다.

합성 시나리오 **37/40건(92.5%)이 허용 기준을 충족**했습니다. 저장된 분류 예측을 재사용한 개발 평가이며, 실제 고객 성과나 지급 정확도가 아닙니다.

[내 기여와 팀 구현](portfolio/bohumpen.md#contribution) · [평가 근거](portfolio/bohumpen.md#evaluation) · [실패 사례](portfolio/bohumpen.md#failure) · [팀 저장소](https://github.com/k0ng-min/2026_finance_ai_challenge)

### 2. [Home Credit — 신용리스크 분석](https://github.com/jujinho03/home-credit-default-risk)

불균형 대출 데이터에서 고위험 신청자를 구분했습니다. 팀 과제에서 데이터 품질·누수 방지와 모델 검증을 맡고, 이후 개인 재구축에서 변수 중요도 해석 오류를 발견해 재검증했습니다.

층화 홀드아웃에서 위험 상위 10% 집단의 실제 부도율은 **26.48%, 전체 대비 3.28배**였습니다. 미래 시점 성과나 손실 감소를 뜻하지 않습니다. [분석 보고서와 검증 과정](https://github.com/jujinho03/home-credit-default-risk/blob/c753352f588a20c7f484e25eeb16c61a72364ef6/docs/findings.md)

### 3. [KOSPI — 금융 시계열과 허위회귀 진단](https://github.com/jujinho03/kospi-macro-spurious-regression)

수준 회귀의 학습 R²는 0.8103이었지만 공적분을 뒷받침할 근거가 없어, 장기 관계로 해석하지 않았습니다. 팀 과제의 데이터 검증과 시계열 진단을 바탕으로 분석을 개인 재구축했습니다.

1차 차분 모형은 금융 변수 변화의 **단기 동시점 연관성**으로 해석했습니다. 인과관계나 검증된 투자 예측은 아닙니다. [진단 결과와 분석 보고서](https://github.com/jujinho03/kospi-macro-spurious-regression/blob/ddd4f114fa9fcc9087138b0dbb3f8b20b5ab5cde/docs/findings.md)

### 4. [서울시 공공자전거 — 시계열 수요 예측](https://github.com/jujinho03/seoul-bike-demand-forecasting)

6인 팀 과제에서 이상치 기준 합의와 전처리를 담당했고, 이후 개인적으로 GPS 3개 군집과 시간 순서 기반 검증을 재구축했습니다.

2024년 4분기 동일 테스트 구간에서 LightGBM의 **Macro RMSE는 SARIMA보다 58.6% 낮았습니다.** 결과는 군집별 다음 1시간 수요의 예측 오차입니다. [분석 보고서와 모델 비교](https://github.com/jujinho03/seoul-bike-demand-forecasting/blob/acc34adfef41548cd36f3e52ae1397494c40390c/docs/findings.md)

## 추가 공개 프로젝트

### [VeriMod — AI 판정 기록의 무결성 검증](https://github.com/jujinho03/verimod)

BLOCK AI 2026 HTTP 451 팀 프로젝트에서 팀장으로 AI 데이터 분할·누수 점검, R01 평가와 오분류 분석을 담당했습니다.

팀은 판정 영수증 2건을 Base Sepolia 테스트넷에 등록하고, 브라우저에서 등록값과 대조했습니다. [공개 검증 기록](https://github.com/jujinho03/verimod/blob/3e1d97b18ec4d1e0d96d0f951e154d8b3b138c74/docs/handoffs/w4-anchored-epoch-public/20261020-r01/README.md). 이는 AI 판정 자체가 옳음을 증명하지 않습니다. [AI 평가·한계: Model Card](https://github.com/jujinho03/verimod/blob/3e1d97b18ec4d1e0d96d0f951e154d8b3b138c74/docs/model-card.md)

## 분석 도구

Python · pandas · scikit-learn · LightGBM · Jupyter
