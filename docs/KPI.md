# 1. 베타 없이도 측정 가능한 KPI

**추천엔진 + GPT 출력 자체만으로 산출** 가능.

즉, 사용자가 없어도, 사용자 로그가 없어도 가능.

**1) Search Hit Rate (검색 성공률)** 

- **Goal:** GPT가 생성한 "가수 - 제목"이 실제로 Spotify에 존재하는지 검증하여, **할루시네이션(거짓 정보)**을 방지한다.
- **Metric:** (Spotify API 검색 결과가 1건 이상인 추천 수 / 전체 추천 시도 수) × 100
- **Target:** **95% 이상** (오타나 없는 노래가 5% 미만이어야 함).

**2) Semantic Alignment (의미적 일치성 - Vibe Check)**

- **Goal:** 사용자의 의도(Taxonomy)와 추천된 '노래의 분위기/가사'가 일치하는가? (주관적 / 정성적)
- **Primary KPI:** LLM Judge에게 "이 상황(독서실)에 이 노래(Bang Bang)가 어울리는가?"를 묻고 **평균 4.5점** 달성.
- **Guardrail KPI:** 상황과 정반대되는 노래(예: 수면에 락, 이별 위로에 신나는 댄스) 추천 발생률 **0% 유지**.

**3) Audio Relevance Score (오디오 속성 적합도)**

- **Goal:** GPT가 추천한 노래의 **실제 오디오 속성(Actual Audio Features)**이 목표(Goal) 범위에 들어가는가? (객관적 / 정량적)
- **Method:**
    1. GPT가 추천한 노래를 Spotify API로 검색하여 `track_id` 확보.
    2. `track_id`로 **Audio Features(BPM, Energy, Valence)** 정보를 조회.
    3. 조회된 수치가 Taxonomy Goal(예: Sleep → Energy < 0.3)을 만족하는지 검사.
- **Metric:** (목표 범위를 충족한 곡 수 / 전체 검색 성공 곡 수) × 100
- **Example:** Sleep 목표인데 실제 곡의 Energy가 0.9라면 **0점(Fail)**.

**4) Consistency (일관성 - 분산 측정)**

- **Goal:** 같은 상황(`Home` + `Focus`)을 10번 물어봤을 때, 추천된 노래들의 **'결(Vibe)'**이 비슷한가?
- **Method:** 10번 추천된 곡들의 **Energy, Valence 표준편차(Standard Deviation)** 측정.
- **Target:** 표준편차가 낮을수록 좋음 (들쑥날쑥하지 않음).

**5) Diversity / Novelty (아티스트 다양성)**

- **Goal:** GPT가 특정 유명 가수(예: 아이유, BTS)만 반복해서 추천하지 않는가?
- **Metric:** (추천된 유니크 아티스트 수 / 전체 추천 곡 수)
- **Target:** 상위 3명 아티스트의 점유율이 50%를 넘지 않도록 관리.

**6) 규칙 커버리지 (Rule Coverage)**

- **Goal:** Location(7) × dB(5) × Goal(7) = 약 245개 조합 중 GPT가 **'검색 가능한 노래'**를 뱉어내지 못하는 사각지대가 있는가?
- **Metric:** (성공적으로 노래를 추천한 조합 수 / 전체 조합 수) × 100

---

# 2. 베타 없이는 절대 측정 불가능한 KPI

 **반드시 실제 사용자 이용 행태 로그가 있어야** 측정 가능.

**1) 재생 전환율 (Play Conversion Rate)** 

- **기존:** 추천 클릭률(CTR)
- **변경:** 사용자가 추천된 리스트를 보고 **실제로 재생 버튼(Deep Link)을 눌러 Spotify로 이동한 비율**.
- **의미:** 제목만 보고도 "듣고 싶다"는 마음이 들었는지 판단.

**2) 청취 유지율 (Retention / Skip Rate)** 

- **기존:** 추천 반응성
- **변경:** (Spotify 앱 제약으로 정확한 청취 시간은 알기 어려울 수 있음)
    - **앱 내 체류 시간:** 추천을 받고 나서 바로 다시 추천을 요청(Re-roll)하면 **'불만족(Skip)'**으로 간주.
    - **세션 종료:** 추천 후 앱을 끄거나 백그라운드로 가면 **'만족(Listen)'**으로 간주(간접 추론).

**3) Personalization Precision (취향 적중률)**

- **Goal:** 사용자 선호(K-Pop 선호)가 반영된 곡이 실제로 추천되었는가?
- **Metric:** (사용자 선호 장르/아티스트와 일치하는 추천 곡 수 / 전체 추천 곡 수)
- **Validation:** 실제 사용자가 해당 추천에 대해 '좋아요/저장'을 눌렀는지(Precision) 확인.

**4) Segment Response (세그먼트 반응도)**

- **Goal:** "이동 중(Moving)" 그룹과 "공부 중(Library)" 그룹 중 누가 더 추천을 많이 이용하는가?
- **Metric:** 세그먼트별 재생 전환율 비교 분석.

**5) DAU / MAU / Retention**

- **Goal:** 서비스의 성장성과 습관 형성 지표.
- **Metric:** 일간/월간 활성 사용자 수 및 재방문율(Retention Day-N).