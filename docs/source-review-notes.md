# 한국어 원문과 구현의 확인 사항

2026년 10월 20일 번역 대조에서 발견한 원문 내부의 차이, 원문과 스크립트의 불일치, 근거가 부족한 설명과 게임에서 확인할 경계값을 기록한다. 이 문서는 번역 오류 목록이나 원본 수정 내역이 아니다. 영어를 원문과 다르게 고쳐 원본의 문제를 숨기지 않았으며, 한국어 원본과 게임 코드는 수정하지 않았다.

기준 원본은 `C:\hoi\hearts_of_korea`, 브랜치는 `feat/korean-focus-expansion-ai`, HEAD는 `d4031aaa0c1f85bb89b0e6ca21d041beade8bd26`이다. 아래 원본 경로는 이 폴더를 기준으로 한 상대 경로이며, 행 번호도 이 시점의 파일을 가리킨다. 설치 게임에서 확인한 자료는 별도로 표시한다.

이 문서 작성자는 아래 항목을 게임에서 직접 재현하지 않았다. **항목별 게임 결과는 모두 NOT TESTED**다. 정적 불일치가 확인됐다는 사실과 게임에서 실제로 실패했다는 판정을 구별한다. 다른 실행에서 얻은 화면·로그 결과는 해당 실행 기록을 근거로 별도 판정해야 한다.

## 판정 기준

| 구분 | 뜻 | 번역 처리 |
| --- | --- | --- |
| 원본 범위의 현지화 누락 확인 | 스크립트가 참조하는 키가 현재 원본 현지화에 없음 | 원문 없는 서사를 새로 쓰지 않음 |
| 원문 내부 불일치 | 연결된 문구나 정식·축약 명칭이 서로 다른 값을 제시함 | 어느 쪽이 의도인지 추측해 통일하지 않음 |
| 원문·스크립트 불일치 | 원문의 수치·동작과 직접 읽은 구현이 대응하지 않음 | 원문을 보존하고 불일치를 보고함 |
| 구현 근거 부족·명칭 해석 보류 | 조사한 자료만으로 설명이나 의도를 확정할 수 없음 | 미구현·오탈자로 단정하지 않음 |
| 일반적인 경계값 확인 | 값 제한 등 통상적인 구현을 게임에서 비교할 필요가 있음 | 확정 오류로 분류하지 않음 |

## RagnaROK의 원본 현지화 누락

`events/HoK_ragnarok.txt`는 일곱 번째 이벤트의 다음 키를 참조한다.

| 키 | 참조 위치 |
| --- | --- |
| `hokRagnarok.7.t` | `events/HoK_ragnarok.txt:252` |
| `hokRagnarok.7.d` | `events/HoK_ragnarok.txt:253` |
| `hokRagnarok.7.a` | `events/HoK_ragnarok.txt:261` |

현재 원본의 현지화와 이 영어 번역에는 세 키의 정의가 없다. `localisation/korean/HoK_start_game_setup_l_korean.yml:66`부터 마지막 68행까지는 `.6`의 제목·설명·선택지이며, 전체 현지화 검색에서도 `.7`의 정의를 찾지 못했다.

이는 **현재 원본 범위 내 현지화 누락**으로 확인했다. 한국어와 영어의 기존 2,971개 키가 일치한다는 검사로는 두 언어에 공통으로 없는 참조를 발견할 수 없다. 실제 화면에서 키가 그대로 표시되는지, 다른 활성 콘텐츠가 값을 제공하는지는 재현하지 않았다. 원본에 없는 제목·본문·선택지를 번역자가 임의로 작성하지 않았다.

## 원문과 연결 스크립트가 다른 항목

### RagnaROK의 날짜·세력 통합·선전포고

대상 키는 `RAGNAROK_ENABLED_TEXT_DESC`, `hokRagnarok.1.d`다. 한국어 원문은 **1938년 1월 1일**, 한국을 제외한 전 세계가 하나의 세력으로 통합되고 한국에 선전포고한다고 설명한다. 근거는 `localisation/korean/HoK_start_game_setup_l_korean.yml:19`, `:47`이다.

확인한 구현은 다음과 같다.

- 도입 이벤트 선택지에서 `.2`를 **730일 뒤**로 예약한다: `events/HoK_ragnarok.txt:20`.
- `.2`부터 `.6`까지 나열된 국가 집단에 `create_wargoal`을 적용한다. 전쟁 명분 생성은 선전포고와 구별해야 한다: `events/HoK_ragnarok.txt:41`, `:55`, `:83`, `:104`, `:132`, `:149`, `:177`, `:193`, `:221`, `:235`.
- 후속 이벤트를 각각 **7일 뒤**로 예약한다: `events/HoK_ragnarok.txt:62`, `:111`, `:156`, `:200`, `:242`.
- `.7`에서 한국을 제외하고 아직 영국과 같은 세력이 아닌 국가를 영국 세력에 추가하려 한다: `events/HoK_ragnarok.txt:265`, `:271`.
- 이 이벤트 연쇄에는 직접 선전포고하는 명령이 없다. 별도 AI 전략에는 한국에 대한 `antagonize`, `prepare_for_war`가 있다: `common/ai_strategy/KOR.txt:693`, `:704`, `:710`.

따라서 고정 날짜에 전 세계의 통합과 선전포고가 동시에 이뤄진다는 설명을 이 구현만으로 보장할 수 없다. 반대로 AI가 실제로 전쟁을 일으키지 않는다고 결론 낼 근거도 없다. 영어는 원문의 설명을 보존했고, 날짜나 동작을 번역 단계에서 몰래 바꾸지 않았다.

### 군함 건조 진행률 30%와 35%

`KOR_fate_of_hms_tiger_BC_tt`는 두 전함을 각각 **90%·30%** 완성 상태로 생산 대기열에 추가한다고 설명한다: `localisation/korean/korea_focus_l_korean.yml:161`.

실제 보상에는 두 DLC 분기 모두 `progress = 0.90`과 `progress = 0.35`가 있다: `common/national_focus/korea.txt:2535`, `:2545`, `:2606`, `:2615`. **두 번째 함선의 원문 수치와 스크립트 값이 다름을 확인했다.** 영어는 원문대로 30%를 유지했다. 어느 값이 의도인지 원본에서 결정해야 한다.

### 수도 배치 안내와 주 ID 835

`KOR_army_augmentation_tt`는 완편 보병사단 4개를 수도에서 얻는다고 설명한다: `localisation/korean/korea_focus_l_korean.yml:123`.

보상은 `random_owned_controlled_state`에서 부대를 생성하며 `prioritize = { 835 }`를 사용한다: `common/national_focus/korea.txt:1838`, `:1840`. 한국의 초기 수도는 **525**다: `history/countries/KOR - Korea.txt:1`. 설치 게임의 `history/states/835-Haraghe.txt:2`는 835를 Hararghe로 정의하며, 검토한 원본에서 이를 수도로 바꾼 정의는 찾지 못했다.

이 블록은 수도를 직접 지정하지 않으므로 수도 배치를 보장하는 구현으로 보기 어렵다. 다만 소유·통제 조건 안에서 선택하므로, 835가 적혀 있다는 이유만으로 부대가 반드시 Hararghe에 생성된다고 단정해서는 안 된다. 실제 배치 위치는 NOT TESTED이며, 영어의 수도 안내는 원문대로 남겼다.

관련 키 `KOR_organization_rokasf_tt`, `KOR_organization_rokmc_tt`도 수도 배치를 안내한다: `localisation/korean/korea_focus_l_korean.yml:126`, `:151`. 이 두 중점은 525를 우선한다: `common/national_focus/korea.txt:1910`, `:2356`. 통상적인 시작 수도와는 일치하지만, `capital_scope`로 현재 수도를 찾는 방식은 아니므로 수도가 바뀐 상황까지 보장한다고 확대하지 않는다. 이는 835 불일치와 구분할 조건부 확인 사항이다.

## 원문 내부에서 값이 다른 항목

### 구축함의 인천 도착과 부산 취역

`kor_events.49.d`는 구매한 구축함 5척이 약 30일 후 **인천항**에 도착한다고 설명하지만, 연결된 `kor_events.51.d`는 **부산항 건선거**에서 함선을 소개한다: `localisation/korean/korea_event_l_korean.yml:168`, `:174`.

연결 예약은 `events/korea.txt:1654`에 있고, 도착 이벤트 앞 주석은 인천이라고 적혀 있다: `events/korea.txt:1676`. 주석 자체가 실제 생성 항구를 입증하는 것은 아니다. 두 원문에 서로 다른 항구가 적힌 점은 확인했지만, 이동 경로가 생략된 것인지 지명 오탈자인지는 확정하지 않았다. 영어도 각각 Incheon과 Busan을 유지했다.

### 장비의 정식·축약 명칭과 함선 차수

다음 차이는 현재 한국어 원문에 이미 있다. 값이 다르다는 것은 확인했지만 어느 쪽이 잘못됐는지는 결정하지 않았다. 영어는 각 키의 원래 값을 보존했다.

| 키 | 원문 값 | 원본 근거 |
| --- | --- | --- |
| `KOR_light_tank_artillery_equipment_3` / `KOR_light_tank_artillery_equipment_3_short` | 정식 `155mm`, 축약 `105mm` | `localisation/korean/korea_equipment_l_korean.yml:21`, `:24` |
| `KOR_armored_car_at_equipment` / `KOR_armored_car_at_equipment_short` | 정식 `KM-930AT`, 축약 `KM-900AT` | 같은 파일 `:145`, `:146` |
| `KOR_cv_nav_bomber_equipment_2` / `KOR_cv_nav_bomber_equipment_2_short` | 정식 `KTBC-41`, 축약 `KCBC-41` | 같은 파일 `:219`, `:220` |
| `KOR_EQUIPMENT_VERSION_4_SHIP` / `KOR_EQUIPMENT_VERSION_6_SHIP` | 두 키 모두 `Batch-VI` | 같은 파일 `:308`, `:310` |

`Batch-VI` 중 하나를 `Batch-IV`로 바꾸거나 구경·모델 번호를 일괄 통일하지 않았다. 식별자에 들어 있는 차수만으로 표시 값을 정정할 수는 없다.

### 인두 정복 설명의 서쪽·동쪽 해석

`KOR_conquest_indu_desc`의 압축문은 `서환건국인두`이고, 괄호 안 풀이는 **동쪽으로 간 환인들**이 인두국을 세웠다고 설명한다: `localisation/korean/korea_focus_l_korean.yml:512`.

현재 영어는 앞을 `The western Hwan`, 뒤를 `The Hwan who went east`로 옮겨 두 방향의 차이를 드러낸다. `서환`을 서쪽의 환인으로 읽는 것이 의도인지, 압축문의 오탈자인지 확인이 필요하다. 방향의 차이를 없애려고 한쪽을 바꾸지 않았으며, 원문의 의도를 확정한 항목으로 보지 않는다.

## 구현 근거가 부족하거나 의도가 불명확한 항목

### 음악의 한국어 제목과 병기된 영어

다음 세 키는 한국어 제목과 괄호 안 영어가 완전히 대응하지 않는다.

| 키 | 한국어 제목 / 병기 영어 | 원본 근거 |
| --- | --- | --- |
| `Lyrical_folk_song_of_korea` | `동방의 서정가` / `Lyrical folk song of korea` | `localisation/korean/HoK_music_l_korean.yml:9` |
| `Songs_of_minjoong` | `민중의 노래` / `Songs of minjoong` | 같은 파일 `:10` |
| `Daegu_commune` | `대구 코뮌 찬가` / `Daegu commune` | 같은 파일 `:11` |

현재 영어는 병기된 영어 제목을 따랐다. `music/hok_music.asset:26`, `:32`, `:38`과 `music/hok_songs.txt:73`, `:89`, `:111`은 같은 기계 식별자를 사용하지만, 그것이 공식 영어 곡명인지 작업용 명칭인지는 설명하지 않는다. 음원을 듣고 곡의 정체를 확인한 작업도 아니다. 일반적인 번역 후보를 검증된 공식 제목처럼 사용하지 않았고, 제목을 임의로 교체하지 않았다.

### Super-China 옵션 참조

`RAGNAROK_ENABLED_TEXT_DESC`는 난이도를 높이기 위해 `중뽕옵션` 사용을 권하며 현재 영어는 이를 Super-China로 옮긴다: `localisation/korean/HoK_start_game_setup_l_korean.yml:19`.

현재 활성 규칙은 한국·RagnaROK·핀란드·몽골·동시베리아 보급 관련 항목이다: `common/game_rules/hok_game_rules.txt:1`, `:31`, `:46`, `:65`, `:79`, `:93`. 원본의 `.txt`·`.yml`에서 중국 강화 옵션에 대응하는 정의를 찾지 못했다. 외부 모드의 옵션인지, 삭제된 기능인지, 다른 이름의 기능인지 확정할 수 없다. 옵션이 실제로 존재하지 않는다는 전역 판정은 내리지 않았고, 영어 안내를 삭제하거나 게임 규칙을 새로 만들지 않았다.

### 몽골의 고유 기마포병대대

`MONGPPONG_ENABLED_TEXT_DESC`는 시작 시 몽골 전용 고유 병종 `기마포병대대`가 해금돼 있다고 설명한다: `localisation/korean/HoK_start_game_setup_l_korean.yml:37`.

확인한 시작 편제는 일반 `cavalry`와 `artillery`를 사용한다: `common/on_actions/mongppong_on_actions.txt:265`, `:281`, `:294`, `:334`. 원본과 조사한 설치 게임의 병종·기술 정의에서 별도 `horse_artillery` 또는 `mounted_artillery` 해금 근거를 찾지 못했다. 이는 **구현 근거 부족**이며, 실제 게임의 모든 동작을 확인해 미구현으로 판정한 결과가 아니다. 영어는 원문의 약속을 보존했고, 고유 병종을 만들어 넣지 않았다.

### 동시베리아 요청의 SOU 스코프

`KOR_request_for_Siberia`는 동시베리아 양도 요청 중점이다: `localisation/korean/korea_focus_l_korean.yml:250`. 가용 조건과 보상이 `SOU`를 참조한다: `common/national_focus/korea.txt:4418`, `:4425`.

검토한 원본에서 `SOU` 국가 태그 정의를 찾지 못했으며, 일반적인 소련 태그인 `SOV`와 다르다. 참조 대상 확인이 필요하지만, 엔진에서 이 중점이 어떻게 평가되는지는 NOT TESTED다. 번역으로 태그를 바꾸거나 원본 스크립트를 정정하지 않았다.

### 로딩 팁의 비준 중단 표현

`LOADING_TIP_100`은 제네바 제3협약의 **비준을 중단**한다는 문구 뒤에 전장 지시를 붙인다: `localisation/korean/replace/HoK_loading_tips_l_korean.yml:11`.

원작자가 비준 절차의 중단을 의도한 것인지, 협약 준수 중단을 의도한 것인지는 문구만으로 결정할 수 없다. 영어는 명시된 `ratification`을 보존했다. 실제 역사에 맞춘다는 이유로 대체역사상의 협약·날짜·명령 내용을 새로 쓰지 않았다.

### 군정 연락인계의 범위

`HOK_KOR_hw_courier_relays`의 제목은 `군정 연락인계`다: `localisation/korean/HOK_KOR_royal_followup_l_korean.yml:46`. 설명은 왕명과 관원의 인계를 다루며, 연결 국민정신은 중앙·지방·부대의 군사 연락을 설명한다: 같은 파일 `:47`, `:83`, `:85`. 연결 중점은 `common/national_focus/korea.txt:13277`에 있다.

군정을 군사 행정으로만 한정하는 것이 의도인지, 왕명·중앙·지방의 행정까지 아우르는 표현인지 추가 확인이 필요하다. 현재 영어 제목 `Military and Civil Liaison Handovers`를 추측으로 좁히거나 넓히지 않았다.

## 일반적인 게임 경계값 확인

`HOK_KOR_civic_ui_support_civic_tt`, `HOK_KOR_civic_ui_suppress_civic_tt`는 시민사회 영향력의 **+10·-10**을 안내한다: `localisation/korean/HOK_KOR_civic_ui_l_korean.yml:30`, `:31`.

효과는 각각 10을 더하거나 빼고, 상태 동기화에서 영향력을 **0~100**으로 제한한다: `common/scripted_effects/HOK_KOR_civic_effects.txt:4`, `:133`, `:156`. 예를 들어 95에서 지원하면 제한 후 100이 되므로 실제 순증가는 5다. 이것은 스크립트에서 계산되는 예시이며, 해당 수치의 게임 화면을 재현했다는 뜻이 아니다.

이는 일반적인 경계 처리일 수 있다. **확정 원문 오류나 번역 오류로 분류하지 않았고 영어도 변경하지 않았다.** 경계에서 버튼 상태와 툴팁, 실제 변화량이 플레이어에게 어떻게 보이는지 확인할 항목으로 남긴다.

## 근거 자료와 후속 처리

이 기록은 다음 검토 자료와 위 원본의 직접 대조를 바탕으로 작성했다.

```text
C:\hoi\test\hok-english-translation-anime\20261020-implementation-01\
  review_core.json
  review_events.json
  review_policies.json
  review_root.json
```

이 JSON들은 외부 전용 테스트 폴더에 있는 **로컬 자료**이며 저장소에 포함돼 있다고 가정하지 않는다. 제안 당시의 영어 값과 검토 메모를 담으므로, 제안이 실제로 적용됐는지는 최종 변경 기록과 구별해야 한다. 이 문서는 해당 JSON들의 제안을 자동 승인하거나 번역 완료를 선언하지 않는다.

우선 확인할 대상은 원문이 없는 `.7`의 세 키, 원문과 직접 다른 군함 진행률, 수도 배치 대상과 RagnaROK의 실행 조건이다. 명칭·방향·곡명은 원작자의 의도를 확인한 뒤 처리하고, 경계값은 별도 게임 사례로 확인한다. 원본 변경이 필요하다고 판단되더라도 번역 작업으로 원본을 수정하지 않는다. 실제 확인 절차는 [게임 내 검증 절차](in-game-verification.md)를 따른다.
