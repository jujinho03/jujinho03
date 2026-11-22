# 플랜브릿지(PlanBridge) — 현금흐름·유동성 리스크 분석

[프로필로 돌아가기](../README.md) · [공개 프로젝트](https://github.com/jujinho03/afpk-cpa-financial-planning-2026) · [내 기여](#contribution) · [분석 결과](#results) · [검증과 한계](#validation)

## 문제와 분석 범위

시험 준비에서 합격·수습·채용·첫 급여로 이어지는 동안 가상 고객이 필수 지출과 안전자금 하한을 감당할 수 있는지 분석했음. CPA 합격 여부나 개인의 취업 가능성을 예측한 프로젝트가 아님.

AFPK 영 플래너 챌린지 2026을 준비한 3인 팀 프로젝트의 개인 포트폴리오. 공식 익명 참가작과는 별개이며, 고객 정보·임금·일정은 모두 가상 설정. 분석 결과는 공개 산출물로 확인 가능.

<a id="contribution"></a>

## 내 기여와 팀 구현

팀장 겸 재무분석 담당. 고객 가정 정리, 시나리오 비교, 조건부 권고를 맡았음. 역할은 본인 확인에 근거함. 공개 README의 역할표와 공동 작업 규칙도 이 담당 범위를 명시하지만, 업무 배정 기록 자체가 모든 계산을 혼자 구현했다는 증거는 아님. [역할표][readme] · [담당 범위][roles]

- 본인 확인 역할: 고객 가정과 비교 기준을 정하고, 응시기회 선호·실행 조건에 따라 권고를 정리했음. [가정 원장][assumptions]·[담당 범위][roles]에서 역할과 기준을 확인할 수 있음.
- 공개 변경 이력: 시간제 급여 미수령 스트레스를 추가한 [PR #12](https://github.com/jujinho03/afpk-cpa-financial-planning-2026/pull/12)는 주진호를 금융 해석 검토자로 명시함. [변경 커밋](https://github.com/jujinho03/afpk-cpa-financial-planning-2026/commit/fc73874f9149833ccfd6c2aad386ffae31b19bf1)의 실제 대상은 결과 내보내기·민감도 JSON·회귀 검사이며 기존 v4 수식은 유지했음.
- 팀·AI 보조 구현: 위 커밋은 Claude 공동 작성 기록을 포함함. [내보내기 코드][export]와 [PR #14](https://github.com/jujinho03/afpk-cpa-financial-planning-2026/pull/14)의 공개 AI 감사는 팀·AI 보조 작업이며, [감사 문서][audit]도 Codex의 검토 주석과 실행 계산을 구분함.

Python 참조 모형, React/Rust 데모, AI 실험 전반은 팀 작업 범위임. 개인 기여는 위에 명시한 가정·비교 기준·재무 해석 및 권고에 한정함. 참조 모형은 인수한 v4를 보존했고, 데모 원저작·AI 담당·통합 담당은 공개 협업 기록에서 구분함. 계정 소유나 PR 작성자 표기만으로 개인 수행 범위를 넓히지 않았음. [참조 모형][model] · [협업 역할][roles]

## 분석 설계

- 단기 18개월: 월말 잔액과 시점별 안전자금 하한을 비교했음. 하한 미달과 잔액이 음수가 되는 계산상 미충당은 서로 다른 사건으로 기록했음.
- 장기 60개월: 초기 현금에 월별 순현금흐름의 할인 현재가치를 더한 조건부 지표를 비교했음. 순자산·투자수익률이 아니며, 합격·수습 확보에 쓰는 가중치도 실제 개인 확률의 추정치가 아님.
- 급여 차질: C의 첫 정규 급여 지연과 B·D의 시간제 급여 미수령을 별도로 검토했음. 후자는 첫 급여 몇 회를 받지 못하는 보수적 조건이며 나중에 돌려받는 지급 이연과 다름.

가정·기간·단위와 계산 경로는 [가정 원장][assumptions], [Python 참조 모형][model], [민감도 내보내기 코드][export]에서 확인할 수 있음. 금액 단위는 만원임.

<a id="results"></a>

## 분석이 바꾼 의사결정

| 비교 조건 | 60개월 조건부 할인 현금흐름 지표 |
|---|---:|
| 취업 전환 C — 기본값 | 6,716.7만원 |
| 근로 병행 B — 기본값 | 6,062.2만원 |
| C에만 첫 급여 3개월 지연 | 5,968.6만원 |

기본값에서는 C가 가장 높지만, C의 첫 급여만 늦추면 B 기본값보다 낮아짐. 두 전략에 같은 충격을 동시에 적용한 비교가 아님. [기본 결과 JSON][summary]의 `weighted_discounted_cashflow_60`, [민감도 JSON][sensitivity]의 `c_first_salary_delay`에서 각 조건을 구분했음.

따라서 단일 지표 순위만으로 C를 권하지 않았음. 마지막 응시기회를 보존하려는 가상 고객에게는 계약·첫 입금·단기 안전자금 확인을 전제로 B를 우선 검토했음. 조건이 깨지면 고객의 응시기회 포기 수용 여부와 실제 채용·첫 급여를 확인해 C를 다시 비교함. 이후 전환은 당시 잔액·남은 기간으로 다시 계산해야 하며 초기 C의 지표를 그대로 재사용할 수 없음. [공개 권고와 조건][readme]

A/U(전업 수험·합격 후 수습 미확보)는 2027년 10월에 안전자금 하한을 위반하지만 첫 미충당은 2028년 1월임. 두 사건을 같은 ‘자금 고갈 시점’으로 묶지 않고, 하한 위반을 먼저 조정해야 할 신호로 읽었음. [경로별 결과][summary]의 `first_safety_violation_18`과 `first_unfunded_month_18`을 따로 확인할 수 있음.

<a id="validation"></a>

## 검증과 한계

공개 감사 기록은 AI 원출력 8건의 선정 주장 23건에 원문 위치·계산·근거와 한계를 연결함. 잔액 주장은 같은 입력의 계산·CSV와 대조하고, 산식·기간·집단 통계의 해석·수급 자격 등은 각각 다른 방법으로 검토했음. 예를 들어 E6/c1은 출력 자체 산식의 합계가 주장과 달랐고, E8/c2는 항목 합계가 맞아도 투자수익·임금 가정과 분석 기간의 타당성은 별개였음. 23건 전체를 같은 방식으로 검산하거나 AI 정확도를 평가한 결과가 아님. [감사 방법][audit] · [항목별 JSON][audit-json]

공식 자료의 문맥은 작성된 검토 주석이고, 프로그램을 실행한다고 최신 법령을 다시 조회하는 것은 아님. 공개 감사 JSON의 사람 승인 필드는 `NOT_RECORDED`이며 과거 AI 서비스 호출 여부는 별도로 확인하지 못했음. 팀의 최종 금융 판정은 별도 공식 참가작 부록에 기록한다는 공개 안내와 구분함. 이번 페이지는 그 비공개 원고나 최종 판정을 옮기지 않았음. [AI 기록의 인수 범위][ai-status]

월말 모형은 실제 지급일 잔액이나 취업 일정을 보장하지 않음. 임금·가중치는 가상이며, 장기 급여 지연의 달력 처리와 ICL 자발 상환 가정 등 알려진 제약도 남아 있음. [한계 원장][limits]

## 재현과 공개 근거

핵심 수치·코드 링크는 확인한 프로젝트 기본 브랜치 커밋 `c78d4f2`에 고정했음. 2026년 11월 21일 Windows의 별도 작업본에서 `python scripts/reproduce.py`를 실행해 기본 결과(`model_summary.json`), 월별 현금흐름(`monthly_cashflows.csv`), 민감도(`sensitivity.json`)를 다시 생성했음. 세 파일 모두 저장본과 바이트 단위로 일치했음. 아래 두 번째 명령은 AI 주장에 대한 별도 감사 절차임.

- [프로젝트 README][readme] · [기본 결과 JSON][summary] · [민감도 JSON][sensitivity]
- [Python 모형][model] · [재현·실행 안내][reproduce] · [AI 감사 안내][audit]

```bash
python scripts/reproduce.py
python scripts/audit_ai_claims.py --check
```

팀의 React/Rust 웹 데모는 Python 참조 결과와 가정이 다른 Rust 확장 모형이며, Python 결과의 독립 검산이 아님. 필요하면 공개 프로젝트의 실행 안내에서 두 모형의 차이를 확인할 수 있음. 이 페이지에는 배포·영상 URL이나 비공개 참가작·서명·내부 판단 기록을 추가하지 않았음.

[프로필로 돌아가기](../README.md)

[readme]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/README.md
[roles]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/AGENTS.md
[assumptions]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/docs/assumptions/BASELINE.md
[model]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/src/afpk_cpa/financial/model_v4.py
[export]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/scripts/reproduce.py
[summary]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/outputs/tables/model_summary.json
[sensitivity]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/outputs/tables/sensitivity.json
[audit]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/ai_evidence/CLAIM_AUDIT.md
[audit-json]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/ai_evidence/claim_audit.json
[ai-status]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/ai_evidence/README.md
[limits]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/docs/decisions/KNOWN_LIMITATIONS.md
[reproduce]: https://github.com/jujinho03/afpk-cpa-financial-planning-2026/blob/c78d4f2fec64c52bc9bd8012d4515e47ab8e4abb/CONTRIBUTING.md
