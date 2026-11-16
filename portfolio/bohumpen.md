# 보험펜(BohumPen) — 청구지원 AI 평가

[프로필로 돌아가기](https://github.com/jujinho03) · [팀 저장소](https://github.com/k0ng-min/2026_finance_ai_challenge) · [내 기여](#contribution) · [평가](#evaluation) · [실패 사례](#failure)

검사 조건은 정보가 부족한 사고의 판단 보류, 담보·필수서류 연결, 인용 문자열의 원문 포함 여부임. TRV-018에서는 세부 유형을 보류해야 할 수하물 사고에 지연 담보·필수서류를 반환했음. 반환된 인용 2건은 원문에 포함됐지만, 이 사례는 전체 허용 기준을 충족하지 못했음. 아래 결과는 저장된 분류 예측을 재사용한 합성 개발 평가이며 실제 고객·지급 성능의 근거가 아님.

## 문제와 서비스 범위

여행자보험 사고가 발생하면 어떤 담보와 서류를 검토해야 하는지, 그 근거가 약관 어디에 있는지 찾기 어려움. 보험펜은 사고 설명에서 검토할 담보·서류와 약관 조항을 연결해 청구 준비와 약관 검토를 지원함. 보험금 지급 여부를 판정하거나 지급액을 산정하지 않음. 실제 화면의 ‘보험형광펜’은 같은 서비스임.

2026 금융 AI Challenge의 FinPoint 4인 팀이 MVP를 구현·제출한 프로젝트. 팀장 주진호, 제출 완료는 본인 확인 기준. 아래 공개 기록의 범위는 서비스 구현과 개발 평가이며, 수상·순위·심사 결과는 별도 기재하지 않음.

<a id="contribution"></a>

## 내 기여와 팀 구현

팀장으로 서비스 기획에 참여. 공개 변경 이력에서 확인되는 개인 기여는 청구지원 E2E 골드셋 구성, 안전 평가, 화면 문구 검수임. 평가가 뒷받침하는 범위에 맞춰 화면 문구를 조정했음.

머지 커밋 [a56dd76](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281)은 이 작업을 “jinho”의 기여로 명시함. 평가 추가 커밋 [1134e8c](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516)의 골드셋·평가기·결과·안전 처리 변경과 교차 확인했음. 작성자 계정만으로 전체 구현을 개인 성과로 귀속하지 않았음.

| 주장 | 수행 주체 | 공개 근거 |
|---|---|---|
| 청구지원 E2E 골드셋·안전 평가 추가 | 주진호 | [기여를 명시한 머지](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281), [평가 변경](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516) |
| 화면 문구를 실제 기능과 정합화 | 주진호 | [머지 설명과 변경 파일](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281) |
| 보험사 7개·약관 조항 558건 구축 | 팀 | [데이터 현황](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/data_status.md) |
| 사고·담보 분리와 불확실성 처리 | 팀 | [청구지원 구현](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/claim_review.py), [후속 질문 변경](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc) |
| 결정적 순위 계산과 AI 설명 분리 | 팀 | [순위 방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md), [계산 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/ranking_score.py) |

팀 구현은 사고 유형과 담보를 구분해 약관 조항과 필요 서류를 연결함. 사고 유형이 불명확할 때 추가 질문하거나 판단을 보류하는 처리를 포함함. [6862ccc](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc)에서는 답변 보존·중복 질문 방지·질문 종료 처리를 확인했음. 이 후속 질문 전체 구현은 팀 성과로 표기함.

보험사 순위는 결정적 로직으로 계산하고 Gemini는 이유를 설명함. 데이터가 없는 평가 축은 제외하고 남은 가중치를 재정규화하므로, 순위를 절대적 상품 품질이나 지급 가능성으로 읽을 수 없음. [방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md) · [설명 생성 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/insurer_ranking_explain_gemini.py)

<a id="evaluation"></a>

## 평가 설계와 결과

합성 청구지원 시나리오 40건 중 37건(92.5%)이 `evaluation.acceptable`의 복합 허용 기준을 통과했음. 수치는 [저장된 평가 JSON](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)의 시나리오별 판정과 집계 지표를 기준으로 함.

- 표본 — 기존 분류기 검수 문장에서 구성한 합성 시나리오임. 실제 고객 데이터가 아님. 사고 분류와 담보·서류 연결, 인용 근거 및 미지원 사고의 처리까지 함께 평가함.
- 실행 경로 — `routing_mode=cached-classifier-predictions`임. 저장된 분류 모델 예측을 재사용하고 현재의 결정적 안전 처리를 적용한 개발 평가임. 이번 포트폴리오 편집에서 외부 API를 새로 호출해 측정한 결과가 아님.
- 허용 기준 — 분류·판단 보류 조건을 만족하고, 필수 담보·서류를 포함하며 금지 담보를 제외하는지 등을 함께 검사함. 모든 출력 집합의 완전 일치를 요구하는 기준과 구분됨. 세부 조건은 [평가기](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)에서 확인할 수 있음.
- 인용 근거 일치 — 인용 97건 중 97건이 해당 조항 원문 안의 문자열과 일치했음. 이는 원문 문자열 포함 여부 검사이며, 사고에 맞는 조항을 골랐다는 의미의 정확도가 아님. [검사 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py) · [결과 원본](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)

이 수치는 실제 운영 성능·지급 정확도·독립된 미관측 고객군에 대한 일반화 성능으로 해석하지 않음. 기존 검수 문장과 현재 지식베이스를 이용한 개발 평가이므로 표본의 다양성과 정답 구성에도 한계가 있음. [평가 문서](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md)

<details>
<summary>평가 경로 확인과 재실행 명령 — 이번 편집에서는 실행하지 않음</summary>

아래는 팀 저장소의 해당 커밋을 준비하고, 의존성·DB·환경 설정을 갖춘 뒤 `backend` 디렉터리에서 사용하는 경로임. 이 프로필 저장소에는 팀 코드·DB를 복제하지 않았음. 출력은 원본 결과 파일을 덮어쓰지 않는 별도 경로임.

저장된 분류 예측을 재사용하는 경로:

```bash
python -m eval.evaluate_claim_pipeline --classifier-predictions eval/results/incident_eval.json --output /tmp/claim_pipeline_eval.recomputed.json
```

분류 모델의 외부 API를 새로 호출하는 경로(인증·호출 비용·응답 변동 가능):

```bash
python -m eval.evaluate_claim_pipeline --live-classifier --request-interval 4.2 --retry-wait 65 --checkpoint /tmp/claim-pipeline-predictions.json --output /tmp/claim_pipeline_eval.live.json
```

두 경로의 결과는 같은 측정으로 간주하지 않음. `--gold-routing`은 정답 분류를 넣어 후속 연결만 격리하는 진단이며 모델 E2E 성능이 아님. 준비 절차와 옵션은 [팀 평가 문서](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md)와 [실행 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)를 기준으로 확인해야 함.

</details>

<a id="failure"></a>

## 실패 사례와 한계

TRV-018의 합성 입력은 “수하물이 아직 없지만 늦는 것인지 영구 분실인지 모릅니다.”임.

- 기대 — 수하물 지연·영구 분실 중 세부 유형을 보류하고 특정 담보·필수서류를 제시하지 않는 것.
- 저장된 실제 — 수하물 지연(`TRV_BAGGAGE_DELAY`)으로 분류해 `FLIGHT_DELAY` 담보와 필수서류를 반환했음.
- 판정 — 반환된 인용 2건은 원문에 포함됐지만, 이 사례는 전체 허용 기준을 충족하지 못했음.

[시나리오·기대값·실제값](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)

원문을 정확하게 인용하는 것과 사고에 맞는 조항을 고르는 것은 별개의 검증임. 인용 일치율만 보고 서비스를 안전하다고 결론 내리지 않고, 모호한 사고의 판단 보류와 담보·서류의 과잉 연결을 별도로 확인해야 함.

개선 과제는 정보가 부족할 때 추가 질문하거나 판단을 보류하는 조건을 검증하는 것임. 해당 실패의 수정·재검증 성공은 확인하지 못했으며, 개발에 사용하지 않은 시나리오와 실제 운영 환경에서의 성능도 미검증.

<a id="evidence"></a>

## 공개 증거

아래 링크는 확인한 커밋에 고정했음. 수치는 저장된 결과를 읽어 검수했으며, 팀의 테스트·평가를 이번 편집에서 직접 실행했다고 주장하지 않음.

- [기여를 명시한 머지 a56dd76](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281) · [평가 추가 1134e8c](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516) · [후속 질문 6862ccc](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc)
- [평가 설계](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md) · [골드셋](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/data/eval/claim_pipeline_gold.jsonl) · [저장된 결과](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json) · [평가 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)
- [데이터 현황](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/data_status.md) · [순위 방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md)

팀 원본 코드·DB·약관 PDF·제출 문서는 이 저장소에 복제하지 않았음. 공개 근거 링크와 새로 작성한 설명만으로 개인 기여와 평가 범위를 제시함. 배포 주소는 기존 확인 기록상 비로그인 접속 시 서비스 중단(Service Suspended) 안내를 표시했음. 이번 검토에서는 현재 배포 상태를 재확인하지 못해 라이브 데모 링크를 싣지 않았음.
