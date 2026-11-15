# 보험펜(BohumPen) — 청구지원 AI 평가

[프로필로 돌아가기](../README.md) · [팀 저장소](https://github.com/k0ng-min/2026_finance_ai_challenge) · [내 기여](#contribution) · [평가](#evaluation) · [실패 사례](#failure)

## 문제와 서비스 범위

여행자보험 사고가 발생하면 어떤 담보와 서류를 검토해야 하는지, 그 근거가 약관 어디에 있는지 찾기 어렵다. 보험펜은 사고 설명에서 검토할 담보·서류와 약관 조항을 연결해 청구 준비와 약관 검토를 지원한다. 보험금 지급 여부를 판정하거나 지급액을 산정하지 않는다. 실제 화면의 ‘보험형광펜’은 같은 서비스이다.

FinPoint가 2026 금융 AI Challenge에 제출을 완료한 팀 프로젝트이며, 팀장은 주진호다. 팀명·팀장·제출 완료는 본인 확인 사항이다. 아래 공개 기록은 구현과 평가의 근거이며 수상·순위·심사 결과를 주장하지 않는다.

<a id="contribution"></a>

## 내 기여와 팀 구현

팀장으로 서비스 기획에 참여했고, 공개 이력으로 확인되는 개인 기여는 청구지원 E2E 골드셋·안전 평가와 화면 문구 정합화이다. 평가 결과가 보여주는 범위와 화면의 표현을 맞췄다.

머지 커밋 [a56dd76](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281)은 이 작업을 “jinho”의 기여로 명시한다. 평가 추가 커밋 [1134e8c](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516)의 골드셋·평가기·결과·안전 처리 변경과 교차 확인했다. 작성자 계정만으로 전체 구현을 개인 성과로 귀속하지 않았다.

| 주장 | 수행 주체 | 공개 근거 |
|---|---|---|
| 청구지원 E2E 골드셋·안전 평가 추가 | 주진호 | [기여를 명시한 머지](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281), [평가 변경](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516) |
| 화면 문구를 실제 기능과 정합화 | 주진호 | [머지 설명과 변경 파일](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281) |
| 보험사 7개·약관 조항 558건 구축 | 팀 | [데이터 현황](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/data_status.md) |
| 사고·담보 분리와 불확실성 처리 | 팀 | [청구지원 구현](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/claim_review.py), [후속 질문 변경](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc) |
| 결정적 순위 계산과 AI 설명 분리 | 팀 | [순위 방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md), [계산 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/ranking_score.py) |

팀 구현은 사고 유형과 담보를 분리하고 약관 조항·필요 서류를 연결한다. 분류가 불확실하면 추가 질문 또는 확인불가로 넘긴다. [6862ccc](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc)에서는 답변 보존·중복 질문 방지·질문 종료 처리를 확인했다. 이 후속 질문 전체 구현은 팀 성과로 표기한다.

보험사 순위는 결정적 로직으로 계산하고 Gemini는 이유를 설명한다. 데이터가 없는 평가 축은 제외하고 남은 가중치를 재정규화하므로, 순위를 절대적 상품 품질이나 지급 가능성으로 읽을 수 없다. [방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md) · [설명 생성 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/app/services/insurer_ranking_explain_gemini.py)

<a id="evaluation"></a>

## 평가 설계와 결과

합성 청구지원 시나리오 40건 중 37건(92.5%)이 허용 기준을 충족했다. 수치는 [저장된 평가 JSON](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)의 시나리오별 `evaluation.acceptable`과 집계 지표를 기준으로 한다.

- 표본 — 기존 분류기 검수 문장에서 구성한 합성 시나리오이다. 실제 고객 데이터가 아니다. 사고 분류와 담보·서류 연결, 인용 근거 및 미지원 사고의 처리까지 함께 평가한다.
- 실행 경로 — `routing_mode=cached-classifier-predictions`이다. 저장된 분류 모델 예측을 재사용하고 현재의 결정적 안전 처리를 적용한 개발 평가이다. 이번 포트폴리오 편집에서 외부 API를 새로 호출해 측정한 결과가 아니다.
- 허용 기준 — 분류·판단 보류 조건을 만족하고, 필수 담보·서류를 포함하며 금지 담보를 제외하는지 등을 함께 검사한다. 모든 출력 집합의 완전 일치를 요구하는 기준과 구분된다. 세부 조건은 [평가기](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)에서 확인할 수 있다.
- 인용 근거 일치 — 인용 97건 중 97건이 해당 조항 원문 안의 문자열과 일치했다. 이는 원문 문자열 포함 여부 검사이며, 사고에 맞는 조항을 골랐다는 의미의 정확도가 아니다. [검사 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py) · [결과 원본](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)

이 수치는 실제 운영 성능·지급 정확도·독립된 미관측 고객군에 대한 일반화 성능으로 해석하지 않는다. 기존 검수 문장과 현재 지식베이스를 이용한 개발 평가이므로 표본의 다양성과 정답 구성에도 한계가 있다. [평가 문서](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md)

<details>
<summary>평가 경로 확인과 재실행 명령 — 이번 편집에서는 실행하지 않음</summary>

아래는 팀 저장소의 해당 커밋을 준비하고, 의존성·DB·환경 설정을 갖춘 뒤 `backend` 디렉터리에서 사용하는 경로이다. 이 프로필 저장소에는 팀 코드·DB를 복제하지 않았다. 출력은 원본 결과 파일을 덮어쓰지 않는 별도 경로이다.

저장된 분류 예측을 재사용하는 경로:

```bash
python -m eval.evaluate_claim_pipeline --classifier-predictions eval/results/incident_eval.json --output /tmp/claim_pipeline_eval.recomputed.json
```

분류 모델의 외부 API를 새로 호출하는 경로(인증·호출 비용·응답 변동 가능):

```bash
python -m eval.evaluate_claim_pipeline --live-classifier --request-interval 4.2 --retry-wait 65 --checkpoint /tmp/claim-pipeline-predictions.json --output /tmp/claim_pipeline_eval.live.json
```

두 경로의 결과는 같은 측정으로 간주하지 않는다. `--gold-routing`은 정답 분류를 넣어 후속 연결만 격리하는 진단이며 모델 E2E 성능이 아니다. 준비 절차와 옵션은 [팀 평가 문서](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md)와 [실행 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)를 기준으로 확인해야 한다.

</details>

<a id="failure"></a>

## 실패 사례와 한계

저장 결과의 TRV-018은 “수하물이 아직 없지만 늦는 것인지 영구 분실인지 모릅니다.”라는 합성 입력이다. 정답은 세부 유형을 보류하도록 정의됐지만, 실제 출력은 수하물 지연(`TRV_BAGGAGE_DELAY`)으로 과확정해 지연 관련 담보(`FLIGHT_DELAY`)와 서류를 추가했다. 이 사례는 허용 기준을 충족하지 못했다. [시나리오·기대값·실제값](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json)

이때 반환한 인용은 원문 문자열 검사에 통과했다. 따라서 원문을 정확하게 인용하는 것과 사고에 맞는 조항을 고르는 것은 별개의 검증이다. 인용 일치율만 보고 서비스를 안전하다고 결론 내리지 않고, 모호한 사고의 판단 보류와 담보·서류의 과잉 연결을 별도로 확인해야 한다.

남은 과제는 지연·분실처럼 경계가 겹치는 입력에서 추가 질문이 필요한 조건을 검증하고, 개발에 쓰지 않은 시나리오와 실제 사용 환경에서 평가 범위를 넓히는 것이다. 현재 자료만으로 이 과제가 해결됐다고 주장하지 않는다.

<a id="evidence"></a>

## 공개 증거

아래 링크는 확인한 커밋에 고정했다. 수치는 저장된 결과를 읽어 검수했으며, 팀의 테스트·평가를 이번 편집에서 직접 실행했다고 주장하지 않는다.

- [기여를 명시한 머지 a56dd76](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/a56dd76bee0af1b717f09f643a05ef0cede46281) · [평가 추가 1134e8c](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/1134e8c5e9e9aec3cb5bc52a614288bc87ce5516) · [후속 질문 6862ccc](https://github.com/k0ng-min/2026_finance_ai_challenge/commit/6862ccc5b68bef6020448ee6fb1cd64e1e34c1cc)
- [평가 설계](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/evaluation.md) · [골드셋](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/data/eval/claim_pipeline_gold.jsonl) · [저장된 결과](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/results/claim_pipeline_eval.json) · [평가 코드](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/backend/eval/evaluate_claim_pipeline.py)
- [데이터 현황](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/data_status.md) · [순위 방법론](https://github.com/k0ng-min/2026_finance_ai_challenge/blob/984b23ba887103b9f9d8b31f7e821eb0037e4024/docs/ranking_methodology.md)

팀 원본 코드·DB·약관 PDF·제출 문서는 이 저장소에 복제하지 않았다. 공개 근거 링크와 새로 작성한 설명만으로 개인 기여와 평가 범위를 제시한다. 배포 주소는 비로그인 접속 시 서비스 중단(Service Suspended) 안내를 표시해 라이브 데모 링크를 싣지 않았다.
