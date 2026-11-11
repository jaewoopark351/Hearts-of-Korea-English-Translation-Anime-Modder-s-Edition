# 2026-11-11 원본 업데이트 대조

최신 일반판 한국어와 현재 영어 번역은 각각 **48파일·3,150키**로 대응한다. 전회 검토 이후 방위비·미군 주둔 관련 **36키**가 추가됐으며, 기존 한국어 본문·버전 변경과 삭제는 없다. 신규 영어 파일은 작업 시작부터 미커밋 상태로 존재했다. 한국어 원문·연결 스크립트·독립적인 영어 검토에서 필수 수정 사항을 발견하지 않아 **영어 현지화 전체를 바이트 그대로 보존**했다. 이번에 새로 작성·수정한 저장소 파일은 검토 기록과 문서 안내뿐이다.

## 기준과 범위

| 대상 | 확인 기준 |
| --- | --- |
| 일반판 읽기 전용 원본 | `C:\hoi\hearts_of_korea`, HEAD `e2009b635d79c80a67fed0370d5fe36a823b656f` 및 작업 시작 시의 미커밋 방위비 콘텐츠 |
| 이전 일반판 검토 | `596b221bb994d93fce552d3ee1ba70fa9b5640f1` 및 11월 10일 당시 검토한 작업 트리 변경 |
| 번역 모드 | HEAD `11ec9e2096af906a086f5c076949f2da1a1c790d` 및 기존 미커밋 `localisation/english/HOK_KOR_us_defense_l_english.yml` |
| RT56 읽기 전용 원본 | `C:\hoi\hearts_of_korea_Road_to_56`, HEAD `39e8e7e5bc3dbdcf52d8c8acc04a92c97cd0b2f5` 및 작업 시작 시의 미커밋 방위비 이식 |
| 이전 RT56 검토 | `2523bf455514c79a3538f0475dc922329afb185d` |

이전 검토의 한국어 47파일은 현재와 SHA-256까지 동일하다. 당시 키·값·버전을 재구성한 비교에서도 신규 36키, 기존 변경 0키, 삭제 0키를 확인했다. 의미 검토는 신규 36키와 연결된 조약·주둔·KATUSA·핵 연구 표시와 스크립트를 중심으로 수행했다. 후속 요청에 따라 RT56 내장 영어와의 공통 표현·업데이트 차이도 읽기 전용으로 대조했다. 기존 번역 전체를 새로 의미 검토하거나 RT56용 번역 서브모드를 구현한 작업은 아니다.

## 확인한 영어 반영 내용

대상 영어 파일은 `localisation/english/HOK_KOR_us_defense_l_english.yml`이다. 국민정신 이름·설명 8키, 조건·효과 안내 8키, 이벤트·뉴스·선택지 20키를 한국어 전체와 문장별로 대조하고 영어만 읽는 검토를 수행했다.

| 기능 | 원문·스크립트와 대조한 내용 |
| --- | --- |
| 상호방위조약 | 미국이 수락해야 양국에 방위비 국민정신을 부여하며, 소비재 공장 계수는 한국 +5%, 미국 -5% |
| 배치·방위비 협정 | 기존 단계를 교체한 국민정신의 최종 계수는 한국 +35%, 미국 -15%; 한국에 3개 사단 부여 및 승인 통보·세계 뉴스 |
| 자치령 편입 | 미국의 자치령으로 전환, 기존 방위비 국민정신 유지, 3개 사단 부여 및 통보·세계 뉴스 |
| 주둔 거부·협의 무산 | 사단·추가 경제 효과 없이 기존 조약과 보유 정신 유지; 사정 변경으로 배치가 불가능해진 경우도 설명 |
| KATUSA | 신규 주둔 요청은 미국의 승인이 있어야 승인 요건 충족; 과거 저장의 기존 접근을 보존하는 분기는 구분 |
| 국민정신 종료 | 상대국 소멸 또는 양국 간 전쟁 시 제거 |

`common/ideas/HOK_KOR_us_defense_ideas.txt`, `common/scripted_effects/HOK_KOR_us_defense_effects.txt`, `common/scripted_triggers/HOK_KOR_us_defense_triggers.txt`, `events/HOK_KOR_us_defense_events.txt`와 기존 `events/korea.txt`·`common/national_focus/korea.txt`의 호출부를 확인했다. 요청·해결·사단 지급의 일회성 플래그, 결과 처리 시 재확인 조건, 효과와 뉴스의 연결도 읽었다. 실제 동작을 실행해 확인했다는 뜻은 아니다.

### 용어와 화자의 관점

- `defence`·`defence cost-sharing agreement`는 영국 영어로 유지했다. 한국이 지불하는 `American Defence Costs`와 미국이 받는 `Korean Defence Contribution`은 각 설명의 관점을 따른다.
- `Consumer Goods Factories factor`는 설치된 게임의 `localisation/english/modifiers_l_english.yml:154`에 있는 실제 표시 용어다. 추가 비율이 아니라 상위 국민정신의 **최종 값**이라는 안내를 보존했다.
- `dominion`은 스크립트의 `autonomy_dominion` 및 설치 게임 `localisation/english/autonomy_l_english.yml:2`의 `Dominion`과 대응한다. 원문의 `51st State`라는 선전적 제목·따옴표와 본문의 자치령 지위를 모두 유지했다.
- 뉴스 선택지의 청구서·국기 별 풍자와 양국 정부의 논조를 보존했다. 실제 미국 주 편입으로 게임 효과를 바꾸어 설명하지 않았다.

### 핵분열 연구 보너스

원본 커밋 `e2009b6`은 핵분열 연쇄반응 실험의 `add_tech_bonus`에 `bonus = 1.5`를 추가했다. 기존 `ahead_reduction = 2`, `uses = 1`, `category = nuclear`는 유지한다. 해당 한국어·영어 설명은 보너스 수치를 직접 쓰지 않으며, 보너스 이름 `HOK_KOR_fission_chain_reaction_experiments`는 이미 `Fission Chain Reaction Experiments`로 번역돼 있다. 수치는 원본 스크립트에 따라 자동 효과 툴팁에 표시되므로 현지화를 새로 쓰거나 게임 코드를 복사하지 않았다.

## RT56 별도 대조와 표현 일관성

RT56에도 같은 방위비 36키가 한국어·영어로 추가돼 있다. 한국어 파일은 일반판 한국어와, 영어 파일은 이 번역 모드의 영어와 **바이트까지 동일**하다. 연결 중점 7키·조약 이벤트 10키까지 총 53키의 표현도 양쪽이 일치한다. 방위비 ideas·effects·triggers·events 네 파일은 일반판과 바이트가 같고, 핵분열 150% 연구 보너스도 이미 반영돼 있다. 신규 업데이트의 용어·문체를 맞추기 위한 추가 수정은 필요하지 않았다.

| RT56 실제 현지화 | 파일 | 정의 행 | 고유 키 |
| --- | ---: | ---: | ---: |
| 한국어 전체 | 48 | 4,231 | 4,218 |
| 내장 영어 전체 | 47 | 2,927 | 2,914 |

각 언어의 장비 13키 중복은 기존 `korea_equipment`와 새 장비 `replace` 파일의 의도적인 동일 값 오버라이드다. RT56의 한국어 전용 1,304키는 호스트 장비 한국어 병합의 비한국 1,291키와 기존 공용 함장 UI 13키다. 영어는 호스트의 영어 정의를 사용하는 구조이므로 단순한 번역 누락 1,304건으로 판정하지 않았다. 새 영어 장비 파일의 17행은 기존 한국 장비 13키와 RT56 전용 1949·1953년형 이름 4키다. 일반판에 없는 후계 장비 키는 이 번역에 추가하지 않았다.

전체 공통 한국어는 2,895키이며 2,869값이 같고 26값은 다르다. 다른 값은 만주 설명 24키, RagnaROK 1키, 항공 연구망 1키다. 일반판 전용 255키와 RT56 전용 1,323키는 구분했다. 항공 연구망의 일반판 `$STATE_1029$`와 RT56 `$STATE_1144$`처럼 판별 실제 주 참조를 섞지 않았다.

**기존 공통 번역 전체가 같은 것은 아니다.** 영어 공통 2,882키 중 2,754값은 같고 128값은 다르다. 차이 중 26키는 한국어 자체가 다르며, 나머지 102키는 같은 한국어에 대한 기존 영어 표현 차이다. 이 102키 중 39키는 `Pyeongannam`/`South Pyeongan` 같은 도명 표기만 다르고, 63키는 문장 재구성·설명 정밀도·게임 용어 등이 다르다. 양쪽 모두 영국 영어를 사용하며 102키를 오류 개수로 해석하지 않는다. 신규 방위비 36키와는 별개다. 재벌 관련 `corporate oligarchs`·`Oligarchic Influence`·`conglomerates`는 양쪽에서 일치한다. 원본 맥락과 기존 검토 근거 없이 어느 한쪽으로 일괄 치환하지 않았다.

| 영어 파일 | 같은 한국어에 대한 기존 영어 차이 |
| --- | ---: |
| `HOK_KOR_state_split_l_english.yml` | 12 |
| `HOK_KOR_industry_expansion_l_english.yml` | 15 |
| `HOK_KOR_civil_nuclear_research_l_english.yml` | 5 |
| `HOK_KOR_cndp_state_development_l_english.yml` | 27 |
| `HOK_KOR_resource_prospecting_l_english.yml` | 2 |
| `HOK_KOR_research_network_l_english.yml` | 3 |
| `HOK_KOR_mio_specializations_l_english.yml` | 24 |
| `HOK_KOR_raids_l_english.yml` | 4 |
| `HOK_KOR_soyang_water_gates_l_english.yml` | 9 |
| `HOK_KOR_democratic_expansion_l_english.yml` | 1 |

102키의 양쪽 영어·한국어 본문은 외부 `rt56_review.json`에, 항목별 분류·판단은 `rt56_terminology_review.json`에 모두 기록했다. 후속 일관성 검토에서 우선 볼 사항은 다음과 같다. 게임 효과 오류로 확정한 목록은 아니다.

- 연구망 툴팁 3키의 시설·전문화명은 일반판이 설치 게임의 실제 영어 표시와 일치한다. RT56의 `Experimental Facility` 표현으로 일반판을 되돌리지 않았다. 실제 시설명 키의 RT56 영어 재정의는 정적 검색에서 찾지 못했으며 최종 로드 순서는 미검증이다.
- `HOK_KOR_civilian_nuclear_technology_tt`는 RT56 자체 기술명과 툴팁의 단축 표현을 함께 확인할 후보이며, `HOK_KOR_mio_trait_jinhae_torpedo_sights`는 원문·해군항공 조직에 맞는 일반판 `Aerial Torpedo Sights`를 유지했다.
- CNDP의 도시·도시 기반, `Hamheung` 지도 표기, 공장 종류별 건설 여유와 나가사키 기습의 취소 대상 범위는 일반판의 구체적인 표현을 보존했다. 해당 RT56 표현의 선택적 정밀도 검토 근거와 키를 외부 기록에 남겼다.

신규 문구의 일치와 기존 표현 차이를 구분하며, 양쪽 번역을 전부 통일했다고 보고하지 않는다. RT56에서는 호환판 내장 영어를 사용하고 일반판 번역 서브모드는 비활성화하는 기존 방침을 유지한다. 자세한 구조는 [RT56 지원 설계](rt56-compatibility-design.md)에 기록했다.

## 원본 측 확인 사항

신규 조약 경로에서는 단계 1 정신을 부여하지만, 업데이트 전 조약을 체결한 저장에는 새 정신이 없을 수 있다. 자치령 효과는 보유 정신을 유지할 뿐 누락된 정신을 추가하지 않으므로, 이 경로에서는 `HOK_KOR_us_defense_dominion_tt`의 조약 단계 +5%/-5% 안내와 실제 보유 효과가 다를 수 있다. 동일한 효과를 쓰는 RT56에도 해당하는 정적 경로 분석이며 저장 게임에서 재현하지 않았다. 영어는 한국어의 유지 규칙과 수치를 보존했고, [원문 확인 사항](source-review-notes.md)에 별도 기준으로 기록했다.

## 검증과 한계

- 전체 48파일·3,150키의 대응, 누락·추가·중복 없음, 경로·버전·헤더·UTF-8 BOM·문자열 문법·보호 토큰·동적 표현·이스케이프 개행을 확인했다.
- 신규 36키는 색상 순서·참조 정의·수치까지 일치한다. 기존 색상 순서 후보 3개, 자연어 대괄호 후보 1개, 수치 후보 118개, 양끝 공백 후보 2개는 11월 10일 기록과 내용까지 동일하며 신규 후보는 없다. 후보를 의미 오류 개수로 해석하지 않는다.
- 기존 외부 `20261020-implementation-01/audit_localisation.py`의 읽기 함수를 수정·복사 없이 재사용했다. `§`·`£` 패턴도 확인했으며 검사기의 실행·출력 제한은 변경하지 않았다.
- RT56 전체 영어 47파일의 BOM·헤더·문자열 문법·보호 토큰·개행·버전도 검사했다. 신규 36키의 참조·수치·색상 순서는 일치하며, 장비의 의도적 13키 중복과 기존 표시 후보는 신규 방위비 오류로 집계하지 않았다. RT56의 생성기·검증 CLI는 실행하지 않았다.
- 작업 시작의 일반판 영어 48파일과 두 원본의 확인 대상 텍스트·HEAD·작업 상태를 보존했다. 게임 코드·이미지·음악·descriptor·의존성·GUI·게임 설정·플레이세트는 변경하지 않았다. 커밋·푸시·업로드는 수행하지 않았다.

**이번 실제 게임 화면·실행 검증은 수행하지 않았다.** 신규 조약·주둔 툴팁과 국민정신, 미국의 세 선택지, 한국 통보·세계 뉴스의 표시·치환·잘림, KATUSA 잠금, 저장 후 재개와 구형 저장 호환 경로는 미검증이다. 핵분열 보너스의 자동 툴팁과 실행 효과도 미검증이다. 이전 실행 결과를 이번 변경의 실행 검증으로 간주하지 않는다.

검증 근거와 기존 미커밋 영어 파일의 백업은 `C:\hoi\test\hok-english-translation-anime\2026-11-11-source-update\`에 보존했다. 주요 기록은 `before.json`, `source_delta_independent.json`, `localisation_audit.json`, `semantic_review.json`, `rt56_before_independent.json`, `rt56_review.json`, `rt56_terminology_review.json`, `rt56_static_validation.json`, `preservation_report.json`이다. 새 일회성 코드 파일·시험 모드·임시 계측은 만들지 않았으며 복원할 게임 설정 변경도 없다.
