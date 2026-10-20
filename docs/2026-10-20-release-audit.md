# 2026-10-20 배포 전 검증 기록

이 문서는 직전에 수행한 로컬 감사의 결과를 정리한다. 문서 작성 과정에서 번역이나 모드 설정을 추가 수정하지 않았으며, 새로운 게임 실행 검증도 수행하지 않았다.

정적 검사는 통과했지만 실제 게임의 최종 문자열 선택은 미검증이다. RT56에서는 지도 ID의 정적 충돌이 확인돼 별도 호환성 작업이 남아 있다.

## 검증 기준

| 항목 | 감사 당시 기준 |
| --- | --- |
| 영어 번역 저장소 | `C:\hoi\Hearts of Korea English Translation Anime Modder's Edition` |
| 번역 브랜치 | `main` |
| 번역 HEAD | `017454fe9270086fd102755ce085d92d70f831f9` |
| 기준 한국어 원본 | `C:\hoi\hearts_of_korea` |
| 원본 브랜치 | `feat/korean-focus-expansion-ai` |
| 원본 HEAD | `d4031aaa0c1f85bb89b0e6ca21d041beade8bd26` |
| 설치 게임의 런처 메타데이터 | HOI4 `1.19.3.0.c01a (5632)` |
| 검증 자료 폴더 | `C:\hoi\test\hok-english-translation-anime\20261020-release-audit-01\` |

한국어 원본은 지정된 현재 폴더를 기준으로 삼았다. 구버전은 번역 기준으로 사용하지 않았다. 감사 당시 원본 작업 트리는 깨끗했고, README에 기록된 번역 기준 커밋과 일치했다.

번역 HEAD는 감사 시작 시점의 커밋이다. 아래의 로컬 수정이 그 커밋에 포함됐다는 뜻은 아니다. 감사 시작 전부터 사용자가 `descriptor.mod`에 추가한 `remote_file_id="3823285419"` 변경이 있었으며, 이를 보존했다.

설치 버전 확인은 게임 실행 검증과 다르다. 공개 Workshop 배포물 전체가 로컬 원본 커밋과 동일한지도 확인하지 않았다.

## A. 확인된 문제와 판단

### 현재 Workshop 항목의 구분

README의 번역 Workshop ID가 기존 Musan 번역 항목인 `3370616163`을 가리켰다. 신규 항목은 `3823285419`이며, 공개 Steam 메타데이터에서 HOI4 항목임을 확인했다.

| 항목 | Workshop ID |
| --- | --- |
| 현재 Anime Modder's Edition 영어 번역 | [3823285419](https://steamcommunity.com/sharedfiles/filedetails/?id=3823285419) |
| 현재 일반판 원본 | [3793992662](https://steamcommunity.com/sharedfiles/filedetails/?id=3793992662) |
| Hearts of Korea RT56 호환판 | [3796816200](https://steamcommunity.com/sharedfiles/filedetails/?id=3796816200) |
| 기존 Musan 영어 번역 | [3370616163](https://steamcommunity.com/sharedfiles/filedetails/?id=3370616163) |
| 원작자 구버전 | [2898629778](https://steamcommunity.com/sharedfiles/filedetails/?id=2898629778) |

직전 감사에서 README를 정정했다. 프로젝트의 `descriptor.mod`와 등록된 로컬 `.mod`는 이미 신규 ID와 일치했고, 로컬 `.mod`의 경로도 올바른 작업 폴더를 가리켰으므로 수정하지 않았다. 이 확인만으로 공개 배포물의 파일 내용까지 검증된 것은 아니다.

### 영어 문자열 두 곳

| 파일·키 | 이전 | 수정 후 | 판단 |
| --- | --- | --- | --- |
| `localisation/english/HoK_start_game_setup_l_english.yml` · `RAGNAROK_ENABLED_TEXT` | `Enable RagnaROK [In Development and Testing]` | `Enable RagnaROK (In Development and Testing)` | 일반 안내문과 동적 표기의 모호성을 줄인 예방적 수정 |
| `localisation/english/korea_event_l_english.yml` · `kor_events.71.d` | `he was recently released and become the founder and leader` | `he was recently released and became the founder and leader` | 확인된 과거 시제 오류 수정 |

RagnaROK 문구는 원본 `common/game_rules/hok_game_rules.txt`의 옵션에서 참조하는 일반 상태 안내다. 기존 대괄호로 인한 엔진 오류는 재현하지 않았다. 대괄호가 있다는 이유만으로 모든 문구를 오류로 분류하지 않으며, 유효한 동적 표현은 보존했다.

### 로드 순서와 의존성

감사 당시 `dlc_load.json`과 런처 데이터베이스의 활성 플레이셋 `한국test01`에는 일반판 원본, 영어 번역 순서로 두 모드가 등록돼 있었다. `settings.txt`는 `language="l_english"`였다. Korean Language, 구번역, RT56는 이 구성에서 비활성 상태였다.

등록된 로컬 `.mod` 경로는 각각 지정된 `C:\hoi`의 원본 및 번역 폴더와 일치했다. 데이터베이스는 읽기 전용으로 확인했다.

번역의 두 dependency 이름은 일반판 및 RT56판의 실제 descriptor 이름과 정확히 일치했다. 두 이름이 적혀 있다는 사실만으로 두 기반 모드를 함께 실행해야 한다고 해석하거나 항목을 삭제하지 않았다.

이 결과는 저장된 설정의 확인이다. 기존 `system.log`에는 일반판 원본만 활성 모드로 기록돼 있어, 새 영어 번역이 실제로 로드됐다는 증거로 사용하지 않았다. 엔진이 최종적으로 어느 문자열을 선택하는지는 미검증이다.

### Korean Language

설치된 Korean Language 항목 `2743487021`은 영어 언어 채널에 한국어 문구를 제공한다. 영어 번역과 79개 키가 겹치며, 글꼴과 UI 파일도 포함한다. 동일한 상대 파일 경로의 충돌은 확인되지 않았다.

키 중복은 충돌 가능성의 근거지만, 실제 표시 언어는 유효한 로드 순서에 따라 달라진다. 항상 영어를 덮어쓴다거나 비활성화만으로 모든 문제가 해결된다고 확정하지 않았다. 원본 의존성이나 사용자 설정을 수정하지 않았다.

### Road to 56

| 비교 항목 | 정적 확인 결과 |
| --- | ---: |
| 일반판 한국어 원본 | 37개 파일·2,971개 키 |
| RT56판 한국어 원본 | 36개 파일·2,743개 키 |
| 두 원본의 공통 키 | 2,716개 |
| 일반판에만 있는 키 | 255개 |
| RT56판에만 있는 키 | 27개 |
| 공통 키 중 한국어 값이 다른 항목 | 25개 |
| RT56 영어 파일과 현재 번역의 동일 상대 경로 | 36개 |

RT56 전용 27개 키는 겹치는 파일 중 **4개 파일**에 분포한다. `HoK_achievements_l_english.yml`에 1개, `HoK_start_game_setup_l_english.yml`에 3개, `replace/HoK_countries_l_english.yml`에 3개, `replace/HoK_state_name_l_english.yml`에 20개다. 기존 임시 보고서의 “RT56 전용 키가 있는 36파일”이라는 표현은 이 두 통계를 구분하지 못한 것이므로, 이 문서에서 바로잡았다.

같은 경로의 파일 우선순위에 따라 RT56 전용 키가 선택되지 않거나 다른 모드의 문구로 대체될 가능성이 있다. 실제 결과는 엔진에서 확인해야 한다. 값이 다른 25개 중 24개는 만주 지역 관련 설명이고, 나머지 1개는 RagnaROK 관련 문구다.

특히 다음 8개 주 ID는 현재 번역과 설치된 RT56에서 서로 다른 지역을 뜻한다.

| 키 | 현재 일반판 영어 번역 | 설치된 RT56의 영어 값 |
| --- | --- | --- |
| `STATE_1028` | Hamgyeong | Dalarna |
| `STATE_1029` | Gangwon | Västerbotten |
| `STATE_1030` | Gyeongsang | Värmland |
| `STATE_1031` | Chungcheong | Opplandene |
| `STATE_1082` | Jeolla | Dominica |
| `STATE_1083` | Hwanghae | Saint Lucia |
| `STATE_1084` | Jeju Island | Saint Vincent |
| `STATE_1088` | Tsushima | Tutuila & Manu'a |

비교한 파일은 번역의 `localisation/english/replace/HoK_state_name_l_english.yml`과 RT56 Workshop 항목 `820260968`의 `localisation/english/state_names_l_english.yml`이다.

이는 확인된 정적 호환성 충돌이다. 게임에서 잘못된 지명이 표시되는 장면을 재현한 것은 아니다. 일반판의 전역 주 이름을 그대로 RT56에 적용하는 방식으로 두 지도 체계를 함께 지원할 수 있다고 판단하지 않았다. 별도 호환 번역 구성이 필요하며, 감사에서는 이를 신설하지 않았다.

## B. 직전 감사의 수정 범위

직전 감사에서 변경한 파일은 다음 3개다.

- `README.md`: 현재 Workshop 항목 구분, 로드 순서의 확인 범위, 호환성 및 미검증 사항 정리.
- `localisation/english/HoK_start_game_setup_l_english.yml`: 상태 안내 괄호 변경.
- `localisation/english/korea_event_l_english.yml`: 과거 시제 오류 수정.

영어 값 두 곳 외의 키·버전·경로·BOM·줄바꿈 형식은 보존했다. 괄호와 동사 시제에 한정된 변경이지만, 실제 UI 표시는 미검증이다. 사용자 기존 `descriptor.mod` 변경, 한국어 원본, 게임 코드·설정·플레이셋은 수정하지 않았다. 커밋·푸시·Workshop 업로드도 수행하지 않았다. `git diff --check`는 통과했다.

당시 수정의 백업은 검증 자료 폴더의 `translation_before/`에 있다. 원복이 필요하면 감사 이후의 변경 여부를 먼저 확인하고 해당 3개 파일의 필요한 변경만 복원한다. 사용자 기존 `descriptor.mod` 변경은 감사 원복 대상이 아니다.

이번 후속 요청에서는 `docs/`의 Markdown 문서만 추가했다. 앞선 감사의 수정 이력과 이번 문서화 작업을 구분한다.

## C. 검증 결과

| 항목 | 결과 | 범위와 한계 |
| --- | --- | --- |
| 한국어 원본과 영어 키 대응 | PASS | 2,971개 일치, 누락·추가 0 |
| 중복 키 | PASS | 검사한 현지화 범위에서 0 |
| BOM·UTF-8·영어 헤더·파일명·경로 | PASS | 37개 영어 파일 정적 검사 |
| 기본 문자열 형식·이스케이프·키 버전 | PASS | 버전 생략 18개를 유효한 기존 형식으로 보존 |
| 동적 표현·변수·색상·개행 | PASS | 보호 토큰 보존, 색상 순서 차이 3건은 영어 어순에 따른 정상 이동으로 검토 |
| 숫자·날짜 차이 검토 | PASS | 표면 차이 117건 대조에서 명확한 수치·날짜 오역을 발견하지 못함 |
| Workshop ID·dependency 이름·등록 경로 | PASS | 감사 당시 메타데이터와 로컬 설정의 일치 |
| 저장된 원본 → 번역 순서·English 설정 | PASS | 런처 설정 확인 |
| 엔진의 최종 문자열 선택·실제 로드 우선순위 | NOT TESTED | 새 게임 실행 증거 없음 |
| Korean Language 충돌·글꼴 차이 | NOT TESTED | 79개 중복 키 등 정적 근거만 확인 |
| RT56 정적 호환성 | FAIL | 서로 다른 지역을 뜻하는 주 ID 8개와 별도 처리할 전용 키 27개 |
| RT56 실제 게임 호환성 | NOT TESTED | 게임에서 재현하지 않음 |
| 실제 게임 실행·화면 표시 | NOT TESTED | 국가 선택, 중점, 이벤트, 결정, 정신, 이름, 장비, RagnaROK, 동적 툴팁 미확인 |

정적 검사기는 Clausewitz 엔진이 아니다. 이 결과를 전체 영어 번역의 의미·자연스러움이나 엔진의 모든 평가 동작이 완전히 검증됐다는 뜻으로 확대하지 않는다.

## D. 남은 확인과 증거 위치

게임 화면 확인에 필요한 Windows Computer Use 연결이 파일 없음 오류(`os error 2`)로 실패했고, 재시도 후에도 연결되지 않았다. 따라서 게임을 실행하거나 실제 화면을 확인했다고 보고하지 않았다. 이전 원본 기록에는 `-userdir` 격리 실패 사례가 있어 이를 검증된 격리 방식으로 가정하지 않았다.

후속 확인 순서와 결과 기록 기준은 [게임 내 검증 절차](in-game-verification.md)에 정리했다. 우선 일반판 구성의 실제 영어 출력과 최종 선택을 확인하고, Korean Language 비교를 별도로 수행해야 한다. RT56는 확인된 정적 충돌을 해결할 구성을 검토한 뒤 별도로 검증해야 한다.

감사 자료는 아래 로컬 폴더에 있으며 저장소에 포함돼 있지 않다.

```text
C:\hoi\test\hok-english-translation-anime\20261020-release-audit-01\
```

| 자료 | 용도 |
| --- | --- |
| `baseline.json`, `user_changes_before.diff`, `translation_before/` | 감사 전 상태와 사용자 변경, 백업 |
| `logs_before/` | 기존 로그 사본; 새 번역 실행 증거로 사용하지 않음 |
| `localisation_before.json`, `localisation_after.json` | 수정 전후 정적 검사 결과 |
| `numeric_review.json` | 숫자·날짜 표면 차이 대조 기록 |
| `load_order_audit.json` | 저장된 순서, 경로, 언어 모드 및 RT56 비교 근거 |
| `workshop_identity_audit.json`, `steam_metadata_snapshot.json` | Workshop 항목 식별 근거 |
| `release_audit_report.txt`, `release_audit_summary.json` | 당시 상세 보고서와 요약 |

앞선 전체 번역 업데이트 자료는 `C:\hoi\test\hok-english-translation-anime\20261020-full-update-01\`에 별도로 보존돼 있다.
