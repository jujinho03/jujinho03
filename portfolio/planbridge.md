# 플랜브릿지(PlanBridge) — 현금흐름·유동성 리스크 분석

[프로필로 돌아가기](../README.md) · [공개 프로젝트](https://github.com/jujinho03/afpk-cpa-financial-planning-2026) · [개인 기여](#contribution) · [분석 결과](#results) · [검증과 한계](#validation)

## 문제와 분석 범위

가상 고객은 CPA 2차 유예생. 시험 준비부터 합격·수습·채용을 거쳐 첫 급여를 받기까지, 월말 잔액으로 필수 지출을 충당하고 안전자금 하한을 유지할 수 있는지 분석. 개인의 시험 합격 및 취업 확률은 추정 범위 밖.

AFPK 영 플래너 챌린지 2026을 준비한 3인 팀 프로젝트. 분석에 사용한 고객 정보·임금·일정은 모두 가상 가정. 이 페이지의 수록 범위는 공개 분석 결과와 개인 기여. 공식 익명 참가작은 별도 자료이며 대회 공식 접수·수상 여부는 미확인.

<a id="contribution"></a>

## 개인 기여와 팀 구현

팀장 겸 재무분석 담당. 본인 확인과 공개 역할표 기준 개인 기여 범위는 고객 가정 설정, 시나리오 비교, 조건부 재무 권고. [역할표][readme] · [담당 범위][roles]

- **재무분석** — 고객 가정과 시나리오 비교 기준을 설정하고, 마지막 응시 기회를 유지하려는 선호와 실행 조건을 반영해 재무 권고 작성. [가정 원장][assumptions] · [담당 범위][roles]
- **금융 해석 검토** — 시간제 급여 미수령 조건을 추가한 [PR #12](https://github.com/jujinho03/afpk-cpa-financial-planning-2026/pull/12)에서 주진호를 금융 해석 검토자로 명시. [변경 커밋](https://github.com/jujinho03/afpk-cpa-financial-planning-2026/commit/fc73874f9149833ccfd6c2aad386ffae31b19bf1)의 변경 범위는 결과 내보내기, 민감도 JSON, 회귀 검사. 기존 v4 수식은 유지.
- **팀·AI 보조 구현** — 위 커밋에 Claude 공동 작성 기록 포함. [내보내기 코드][export]와 [PR #14](https://github.com/jujinho03/afpk-cpa-financial-planning-2026/pull/14)의 공개 AI 감사는 팀·AI 보조 작업. [감사 문서][audit]에서 Codex의 검토 주석과 프로그램의 실행 계산을 구분.

Python 참조 모형, React/Rust 데모, AI 실험은 팀 산출물. 참조 모형은 인수한 v4를 보존. 데모 원저작·AI 담당·통합 담당은 공개 협업 기록에 따라 구분. 계정 소유나 PR 작성자 표기만으로 개인 수행 범위를 추정하지 않고, 가정·비교 기준·재무 해석·권고로 한정. [참조 모형][model] · [협업 역할][roles]

## 분석 설계

- **18개월 유동성** — 월말 잔액과 시점별 안전자금 하한을 비교. 안전자금 하한을 밑도는 시점과 잔액이 음수가 되는 계산상 미충당 시점을 따로 기록.
- **60개월 현금흐름** — 초기 현금에 월별 순현금흐름의 할인 현재가치를 더한 조건부 지표로 전략을 비교. 순자산·투자수익률은 산출 범위 밖. 합격·수습 확보 가중치는 시나리오 가정이며, 실제 개인 확률은 추정 범위 밖.
- **급여 차질** — C의 첫 정규 급여 지연과 B·D의 시간제 급여 미수령을 별도로 검토. B·D에는 첫 몇 회분의 급여를 사후에도 받지 못하는 보수적 가정 적용.

금액 단위는 만 원. 분석 기간·가정과 계산 근거는 [가정 원장][assumptions], [Python 참조 모형][model], [민감도 내보내기 코드][export]에 수록.

<a id="results"></a>

## 첫 급여 지연에 따른 전략 비교

| 비교 조건 | 60개월 조건부 할인 현금흐름 지표 |
|---|---:|
| 취업 전환 C — 기본값 | 6,716.7만 원 |
| 근로 병행 B — 기본값 | 6,062.2만 원 |
| C에만 첫 급여 3개월 지연 | 5,968.6만 원 |

기본 가정에서 60개월 지표가 가장 높은 전략은 취업 전환(C). 근로 병행(B)의 급여 일정은 고정하고 C의 첫 급여만 3개월 늦추면 두 전략의 순위 역전. 비교에 사용한 항목은 [기본 결과 JSON][summary]의 `weighted_discounted_cashflow_60`과 [민감도 JSON][sensitivity]의 `c_first_salary_delay`.

마지막 응시 기회를 유지하려는 고객에게는 시간제 계약·첫 입금·단기 안전자금 확인을 전제로 B 우선 검토를 권고. 이 조건이 깨지면 응시 기회 포기 의사, 실제 채용 여부와 첫 급여 시점을 확인해 C와 재비교. 도중에 전략을 전환할 때는 당시 잔액·남은 기간을 기준으로 재산정. 초기 C 지표는 재사용 대상에서 제외. [공개 권고와 조건][readme]

A/U(전업 수험·합격 후 수습 미확보) 경로의 첫 안전자금 하한 위반은 2027년 10월, 첫 미충당은 2028년 1월. 하한 위반을 현금이 실제 부족해지기 전 재무 계획을 조정할 신호로 해석. [경로별 결과][summary]의 `first_safety_violation_18`과 `first_unfunded_month_18`에 각각 기록.

<a id="validation"></a>

## 검증과 한계

공개 감사 대상은 AI 원출력 8건에서 선정한 주장 23건. 주장별로 원문 위치와 계산·근거·한계를 연결. 잔액은 같은 입력의 계산 결과·CSV와 대조하고, 산식·기간·집단 통계 해석·수급 자격은 주장에 맞는 방식으로 검토. E6/c1에서는 원출력 산식의 합계와 주장 사이에 불일치. E8/c2에서는 항목 합계가 일치했으나 투자수익·임금 가정과 분석 기간의 타당성은 별도 검토 대상. AI 정확도는 평가 범위 밖. [감사 방법][audit] · [항목별 JSON][audit-json]

공식 자료의 문맥은 검토자가 작성한 주석으로 제공. 프로그램 실행 시 최신 법령을 다시 조회하는 기능은 미포함. 공개 감사 JSON의 사람 승인 필드는 `NOT_RECORDED`이며, 과거 AI 서비스 호출 여부는 미확인. 공개 프로젝트 안내상 팀의 최종 금융 판정은 공식 참가작 부록에 기록할 대상. 비공개 원고와 최종 판정은 이 페이지에 미수록. [AI 기록의 인수 범위][ai-status]

적용 범위는 가상 임금·가중치에 따른 월말 잔액. 실제 지급일 잔액과 취업 일정은 미검증. 장기 급여 지연의 달력 처리와 취업 후 상환 학자금대출(ICL)의 자발 상환 가정 검토는 차후 과제. [한계 원장][limits]

## 재현과 공개 근거

핵심 수치·코드 링크는 검토한 프로젝트 기본 브랜치 커밋 `c78d4f2`에 고정. 2026년 11월 21일 Windows의 별도 작업본에서 `python scripts/reproduce.py`로 기본 결과(`model_summary.json`), 월별 현금흐름(`monthly_cashflows.csv`), 민감도(`sensitivity.json`)를 재생성. 세 파일 모두 저장본과 바이트 단위로 일치. 아래 두 번째 명령은 AI 주장에 대한 별도 감사 절차.

- [프로젝트 README][readme] · [기본 결과 JSON][summary] · [민감도 JSON][sensitivity]
- [Python 모형][model] · [재현·실행 안내][reproduce] · [AI 감사 안내][audit]

```bash
python scripts/reproduce.py
python scripts/audit_ai_claims.py --check
```

팀의 React/Rust 웹 데모는 Python 참조 모형과 다른 가정을 적용한 확장 모형. 위 세 파일의 바이트 일치는 Python 참조 모형에 한정. 두 모형의 차이와 실행 조건은 공개 프로젝트의 재현·실행 안내에 수록.

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
