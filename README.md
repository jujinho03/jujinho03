# 주진호 | 금융 데이터 분석 · 모델 검증

데이터사이언스 전공. 신용리스크·현금흐름·금융 시계열을 분석하며 데이터 품질·누수·모형 가정과 결과의 해석 범위를 점검했음.

[신용리스크 검증](https://github.com/jujinho03/home-credit-default-risk/blob/c753352f588a20c7f484e25eeb16c61a72364ef6/docs/findings.md) · [보험 AI 실패 사례](portfolio/bohumpen.md#failure) · [VeriMod 모델 카드](https://github.com/jujinho03/verimod/blob/3e1d97b18ec4d1e0d96d0f951e154d8b3b138c74/docs/model-card.md)

## 대표 프로젝트

### 1. [보험펜(BohumPen) · 보험 청구지원 AI 평가](portfolio/bohumpen.md)

FinPoint 4인 팀의 여행자보험 청구지원 MVP 구현·제출 프로젝트(제출 완료는 본인 확인 기준). 주진호는 서비스 기획, 청구지원 E2E 골드셋·안전 평가, 화면 문구 검수를 맡았음.

저장된 분류 예측을 재사용한 합성 개발 평가에서 40건 중 37건(92.5%)이 허용 기준을 충족. 세부 유형을 보류해야 할 수하물 사고에서 지연 담보·필수서류를 반환한 실패가 있었음. 실제 지급 정확도는 평가하지 않았음.

[내 기여](portfolio/bohumpen.md#contribution) · [평가 설계](portfolio/bohumpen.md#evaluation) · [실패 사례](portfolio/bohumpen.md#failure) · [팀 저장소](https://github.com/k0ng-min/2026_finance_ai_challenge)

### 2. [플랜브릿지(PlanBridge) · 현금흐름과 유동성 리스크](portfolio/planbridge.md)

3인 팀의 팀장 겸 재무분석 담당으로 가상 고객의 가정·대안 비교 기준·민감도 해석·조건부 권고를 정리. 60개월 조건부 할인 현금흐름 지표는 취업 전환 C에만 첫 급여 3개월 지연을 적용하면 5,968.6만 원으로, 근로 병행 B 기본값 6,062.2만 원보다 낮음. 마지막 응시기회를 보존하려는 가상 고객에게 계약·첫 입금·단기 안전자금 확인을 전제로 B를 우선 검토.

[내 기여·팀 구현](portfolio/planbridge.md#contribution) · [비교 결과](portfolio/planbridge.md#results) · [급여 지연 민감도 원본](https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/outputs/tables/sensitivity.json)

### 3. [Home Credit · 신용리스크와 심사 우선순위](https://github.com/jujinho03/home-credit-default-risk)

팀 과제에서 데이터 품질·누수 점검과 모델 검증을 맡고, 이후 개인 재구축에서 변수 중요도 해석 오류를 교정. 층화 홀드아웃의 위험점수 상위 10% 집단 실제 부도율은 26.48%로 전체 대비 3.28배였음. 심사 우선순위 검토 근거이며 자동 승인·거절, 미래 성과·손실 절감으로 해석하지 않음.

[검증 과정과 임계값 비교](https://github.com/jujinho03/home-credit-default-risk/blob/c753352f588a20c7f484e25eeb16c61a72364ef6/docs/findings.md)

### 4. [KOSPI · 금융 시계열과 허위회귀 진단](https://github.com/jujinho03/kospi-macro-spurious-regression)

팀 과제에서 데이터 검증·시계열 진단에 참여하고, 이후 분석 전 과정을 개인 프로젝트로 재구축. 수준 회귀의 학습 R²는 0.8103이었으나 정상성·잔차 진단에서 비정상성·자기상관을 확인해 해석을 제한했음. 공적분 근거도 제한적이므로 1차 차분 결과는 단기 동시점 연관성으로만 해석. 투자 예측·인과관계를 입증한 결과는 아님.

[시계열 진단과 시점 분리 검증](https://github.com/jujinho03/kospi-macro-spurious-regression/blob/ddd4f114fa9fcc9087138b0dbb3f8b20b5ab5cde/docs/findings.md)

## 추가 프로젝트

- [서울시 공공자전거 · 시계열 수요 예측](https://github.com/jujinho03/seoul-bike-demand-forecasting) — 팀 과제에서 전처리 담당. 이후 GPS 기반 3개 군집과 시간순 검증 절차를 개인 프로젝트로 재구축. 2024년 4분기 동일 테스트 구간에서 LightGBM의 Macro RMSE가 SARIMA 대비 58.6% 낮았음. [비교 결과](https://github.com/jujinho03/seoul-bike-demand-forecasting/blob/acc34adfef41548cd36f3e52ae1397494c40390c/docs/findings.md)
- [VeriMod · AI 판정 기록의 무결성 검증](https://github.com/jujinho03/verimod) — HTTP 451 팀장으로 한국어 댓글 데이터 분할·누수 점검, R01 모델 평가, 오분류·임계값 검토를 맡고 본선에서 발표했음. R01 Macro-F1 0.6525는 모델 선택에 사용한 VALIDATION 1,255건 결과이며, 내부 독립 TEST 1,255건은 봉인·미실행.

  팀은 Base Sepolia 영수증 2건으로 기록 무결성을 시연했음. 모델 정확성·정책 안전성을 입증하는 결과는 아님.

  [데이터 분할](https://github.com/jujinho03/verimod/blob/3e1d97b18ec4d1e0d96d0f951e154d8b3b138c74/docs/data-card.md) · [모델 카드](https://github.com/jujinho03/verimod/blob/3e1d97b18ec4d1e0d96d0f951e154d8b3b138c74/docs/model-card.md) · [공개 검증 기록](https://github.com/jujinho03/verimod/blob/3e1d97b18ec4d1e0d96d0f951e154d8b3b138c74/docs/handoffs/w4-anchored-epoch-public/20261020-r01/README.md)
