# 주진호 | Data Science Portfolio

> 데이터를 먼저 의심하고, 검증 가능한 결과로 정리합니다.

데이터사이언스를 전공하며 금융·공공데이터의 품질 검수, 데이터 누수 방지, 모델 검증과 결과 해석을 프로젝트로 축적하고 있습니다. 아래 세 저장소는 학부 프로젝트의 문제의식을 유지하면서 실행 구조, 검증 절차와 문서를 개인 포트폴리오로 다시 구축한 결과입니다.

![Python](https://img.shields.io/badge/Python-Data%20Analysis-3776AB?style=flat-square&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-Data%20Processing-150458?style=flat-square&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Reproducible%20Analysis-F37626?style=flat-square&logo=jupyter&logoColor=white)

## 대표 프로젝트

| 순서 | 프로젝트 | 핵심 역량 | 대표 결과 |
|---:|---|---|---|
| 1 | [Home Credit 채무불이행 위험 분석](https://github.com/jujinho03/home-credit-default-risk) | 불균형 분류, 누수 방지, 해석 오류 교정 | 위험 상위 10% 부도율 26.48%, 전체 대비 Lift 3.28배 |
| 2 | [서울시 공공자전거 수요 예측](https://github.com/jujinho03/seoul-bike-demand-forecasting) | 대용량 데이터 품질, GPS 군집, 시계열 검증 | LightGBM Macro RMSE 190.724, SARIMA 대비 58.595% 개선 |
| 3 | [KOSPI 거시경제 허위회귀 검증](https://github.com/jujinho03/kospi-macro-spurious-regression) | 정상성·공적분 진단, HAC 추론, 홀드아웃 | Durbin–Watson 0.2611 → 2.0102, 수준 OLS 해석을 1차 차분으로 교정 |

각 프로젝트 README의 **프로젝트 한눈에 보기**, **나의 역할과 재구축 범위**, **핵심 주장과 검증 경로**에서 원과제와 개인 재구축의 경계, 주요 결과와 공개 증거를 바로 확인할 수 있습니다.

## 분석 원칙

- 모델보다 먼저 원본 행 수, 결측·중복·이상값과 집계 전후 보존을 확인합니다.
- 전처리와 검증을 분리하고, 시계열에서는 시간 순서를 보존합니다.
- 복잡한 모델은 단순 기준선과 같은 평가 구간에서 비교합니다.
- 핵심 수치는 CSV·그림·노트북으로 다시 확인할 수 있게 연결합니다.
- 높은 성능보다 해석 가능한 범위와 한계를 함께 기록합니다.
