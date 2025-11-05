### rule_mapping_v2.5의 내장 규칙 구조 (search_query를 자동 생성하기 위한 로직)

| 구분                            | 필드                                  | 규칙 요약                                                                                                                      | 검색어에서의 역할                                               |
| ----------------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
|  **Goal (심리적 목표)**          | `goal`                              | focus / relax / active / sleep / meditate                                                                                  | `"for focus"`, `"to relax"`, `"for workout"` 등으로 자연어 변환 |
|  **Mood (정서적 분위기)**         | `mood`                              | calm / chill / upbeat / bright / neutral                                                                                   | 감정적 톤 표현 (검색어 내 1:1 반영)                                 |
|  **Genre (음악 장르)**          | `genre_primary`, `genre_secondary`  | <ul><li>primary는 항상 포함</li><li>secondary는 존재 시 병기</li><li>같으면 하나로만 표기</li></ul>                                            | `"lo-fi"`, `"pop edm"`, `"jazz acoustic"` 등             |
|  **Vocal (보컬 여부)**          | `vocal`                             | <ul><li>`instrumental`, `vocal-heavy`, `female-vocal`, `male-vocal`만 포함</li><li>`light-vocal`, `balanced`는 생략</li></ul>    | `"instrumental"`, `"female-vocal"`                      |
|  **Energy Hint (리듬 강도)**     | `energy_min`, `energy_max` → 평균값 기반 | <ul><li>0.0~0.3 → `soft`</li><li>0.31~0.5 → `mellow`</li><li>0.51~0.7 → `energetic`</li><li>0.71~1.0 → `intense`</li></ul> | `"mellow"`, `"energetic"`, `"intense"`                  |
|  **BPM Range (박자 범위)**      | `bpm_min`, `bpm_max`                | 정수 두 개를 `"80-90 bpm"` 형태로 연결                                                                                               | `"80-90 bpm"`                                           |
|  **Negative Filter (품질제외)** | (고정값)                               | `" -live -remix"`                                                                                                          | 라이브/리믹스 버전 제외 (검색 품질 향상용)                               |

