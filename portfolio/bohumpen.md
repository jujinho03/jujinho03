# 보험펜(BohumPen) — 청구지원 AI 평가

[프로필로 돌아가기](../README.md) · [팀 저장소](https://github.com/k0ng-min/2026_finance_ai_challenge) · [개인 기여](#contribution) · [평가](#evaluation) · [실패 사례](#failure)

여행자보험 청구지원 AI가 불확실한 사고에서 판단을 보류하고 필요한 담보·서류와 약관 근거를 안내하는지 점검. 저장된 분류 예측을 재사용한 합성 개발 평가 40건 중 37건이 복합 허용 기준 충족. 수하물 사고 TRV-018에서는 인용 2건이 약관 원문과 일치했으나, 지연 여부가 확인되기 전에 지연 담보와 필수서류를 안내. 실제 고객의 보험금 지급 정확도는 평가 범위 밖.

## 문제와 서비스 범위

보험펜은 여행자보험 사고 설명을 바탕으로 검토할 담보·서류를 찾고, 그 근거가 되는 약관 조항까지 연결하는 청구 준비 서비스. 보험금 지급 여부 판정과 지급액 산정은 서비스 범위 밖. 실제 화면에 표시되는 이름은 ‘보험형광펜’.

FinPoint 4인 팀이 청구 준비 MVP를 구현해 2026 금융 AI Challenge에 제출. 팀장은 주진호이며, 제출 완료는 본인 확인 기준. 공개 기록으로 확인 가능한 범위는 서비스 구현과 개발 평가. 발표 심사 진출 여부는 미확인.

<a id="contribution"></a>

## 개인 기여와 팀 구현

팀장으로 서비스 기획에 참여하고, 청구지원 전 과정(E2E)을 평가할 정답 사례를 설계. 안전 평가 결과와 실제 기능을 대조해 화면 문구 조정.

머지 커밋 [a56dd76](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281)에서 이 작업의 기여자를 “jinho”로 명시. 평가 추가 커밋 [1134e8c](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516)의 골드셋·평가기·결과·안전 처리 변경 내역과 대조해 개인 기여 범위를 확인.

| 주장 | 수행 주체 | 공개 근거 |
|---|---|---|
| 청구지원 E2E 골드셋·안전 평가 추가 | 주진호 | [기여를 명시한 머지](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281), [평가 변경](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516) |
| 화면 문구를 실제 기능과 정합화 | 주진호 | [머지 설명과 변경 파일](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281) |
| 보험사 7개·약관 조항 558건 구축 | 팀 | [데이터 현황](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/data_status.md) |
| 사고·담보 분리와 불확실성 처리 | 팀 | [청구지원 구현](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/claim_review.py), [후속 질문 변경](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc) |
| 결정적 순위 계산과 AI 설명 분리 | 팀 | [순위 방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md), [계산 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/ranking_score.py) |

팀은 사고 유형과 담보를 구분해 약관 조항과 필요 서류를 연결하고, 유형이 불명확할 때 추가 질문하거나 판단을 보류하는 절차를 구현. 팀장으로 참여한 부분은 대분류 미확정 시 후속 질문 처리 수정. [6862ccc](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc)에서 답변 보존, 중복 질문 방지, 질문 종료 처리 확인. 후속 질문 기능 전체는 팀 공동 산출물.

보험사 순위는 사전에 정한 규칙으로 계산하고 Gemini는 산출 이유를 설명. 데이터가 없는 평가 축은 제외하고 남은 가중치를 재정규화. 순위의 해석 범위는 가용한 평가 축 내 상대 비교이며, 절대적 상품 품질이나 보험금 지급 가능성은 평가 범위 밖. [방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md) · [설명 생성 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/insurer_ranking_explain_gemini.py)

<a id="evaluation"></a>

## 평가 설계와 결과

합성 청구지원 시나리오 40건 중 37건(92.5%)이 `evaluation.acceptable`의 복합 허용 기준 통과. 집계 근거는 [저장된 평가 JSON](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)의 시나리오별 판정.

- 표본 — 기존 분류기 검수 문장에서 구성한 합성 시나리오. 평가 항목은 사고 분류, 담보·서류 연결, 인용 근거, 미지원 사고의 처리. 실제 고객 데이터는 표본에서 제외.
- 실행 경로 — `routing_mode=cached-classifier-predictions`. 저장된 분류 예측에 현재의 규칙 기반 안전 처리를 적용한 개발 평가. 이번 편집에서는 외부 API 재호출 없이 저장된 평가 결과만 검토.
- 허용 기준 — 분류·판단 보류 조건 충족, 필수 담보·서류 포함, 금지 담보 제외 등을 함께 검사. 모든 출력 집합의 완전 일치 여부는 별도 기준. [평가기](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)
- 인용 근거 일치 — 인용 97건 모두 해당 조항 원문의 문자열과 일치. 이 지표의 측정 대상은 원문 문자열 포함 여부이며, 사고에 적합한 조항의 선택 여부는 별도 평가 항목. [검사 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py) · [결과 원본](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)

기존 검수 문장과 현재 지식베이스에서 구성한 표본이므로 시나리오와 정답의 다양성에 한계. 실제 운영 성능, 지급 정확도, 새로운 고객군에서의 일반화 성능은 미검증. [평가 문서](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md)

<details>
<summary>평가 재현 명령과 실행 조건</summary>

팀 저장소의 해당 커밋에서 의존성·DB·환경 설정을 준비한 뒤 `backend` 디렉터리에서 실행. 팀 코드·DB는 이 프로필 저장소에 미수록. 두 명령 모두 원본 결과와 별도 경로에 출력.

저장된 분류 예측을 재사용하는 명령

```bash
python -m eval.evaluate_claim_pipeline --classifier-predictions eval/results/incident_eval.json --output /tmp/claim_pipeline_eval.recomputed.json
```

분류 모델의 외부 API를 호출하는 명령. 인증 필요. 호출 비용과 응답 변동 가능.

```bash
python -m eval.evaluate_claim_pipeline --live-classifier --request-interval 4.2 --retry-wait 65 --checkpoint /tmp/claim-pipeline-predictions.json --output /tmp/claim_pipeline_eval.live.json
```

저장된 예측을 재사용하는 평가와 외부 API를 새로 호출하는 평가는 실행 조건에 따라 구분. `--gold-routing`은 정답 분류를 입력해 후속 연결만 검사하는 별도 진단으로, 모델 E2E 성능 평가 범위에서 제외. [팀 평가 문서](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md) · [실행 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)

</details>

<a id="failure"></a>

## 실패 사례와 한계

TRV-018은 수하물이 아직 도착하지 않아 지연과 영구 분실을 구별할 수 없는 합성 사례.

- 기대 — 세부 사고 유형 판단을 보류하고 특정 담보·필수서류 안내를 유보.
- 실제 응답 — 수하물 지연(`TRV_BAGGAGE_DELAY`)으로 분류한 뒤 `FLIGHT_DELAY` 담보와 필수서류 반환.
- 판정 — 인용 2건의 원문 일치. 판단 보류 실패로 전체 허용 기준 미충족.

[시나리오·기대값·실제값](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)

인용 정확도와 조항 선택의 적합성은 서로 다른 평가 항목. 서비스 안전성 판단에는 모호한 사고에서 판단을 보류하는지, 담보·서류를 과도하게 연결하는지도 점검할 필요.

TRV-018의 세부 사고 유형 보류 실패에 대한 수정·재검증 여부는 미확인. 새로운 시나리오에서의 추가 질문·판단 보류 조건 검증과 실제 운영 성능 확인은 차후 과제.

<a id="evidence"></a>

## 공개 증거

공개 근거 링크는 검토한 커밋에 고정. 평가 수치는 팀이 저장한 시나리오별 결과와 집계 지표를 대조해 확인.

- [기여를 명시한 머지 a56dd76](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281) · [평가 추가 1134e8c](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516) · [후속 질문 6862ccc](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc)
- [평가 설계](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md) · [골드셋](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/data/eval/claim_pipeline_gold.jsonl) · [저장된 결과](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json) · [평가 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)
- [데이터 현황](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/data_status.md) · [순위 방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md)

이 저장소에는 공개 근거 링크와 프로젝트 설명 수록. 이전 비로그인 접속 당시 배포 주소에서 서비스 중단(Service Suspended) 안내 확인. 현재 배포 상태는 미확인.
