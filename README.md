# Soundscape 데이터 파트 구조

**환경 규칙 기반 음악 추천 엔진**의 데이터 설계·검증·EDA를 관리

##  폴더 구조
| 폴더 | 설명 |
|------|------|
| `docs/` | 데이터/규칙의 정의, 스키마, 버전 관리 문서 |
| `datasets/` | CSV·JSON 산출물 (샘플, 규칙, 분석결과) |
| `notebooks/` | 데이터 생성 및 분석용 주피터 노트북 |
| `src/` | JSON 변환, search_query 생성 등 파이썬 스크립트 |
| `.gitignore` | 캐시/임시파일 제외 설정 |

##  진행상황
sampledata_research.md
->
sample_input_v2.csv/json
->
EDA_sampledata.ipynb
->
rule_mapping__v2.5.csv
->
build_search_query_v2.5.py → search query 생성

##  버전 관리
- 규칙 매핑표 버전 기록 → `docs/규칙매핑표_버전.md`
- 각 버전별 스키마 정의 → `docs/규칙매핑표vX_schema.md`

##  규칙
- CSV/JSON은 `datasets/` 폴더 안에서만 관리
- 코드(`src/`, `notebooks/`)와 문서(`docs/`)는 항상 같이 업데이트
- 버전명 통일: `v1`, `v2`, `v2.5`, `v3` (하이픈X)
