# 2026-10-20 번역 검수와 게임 확인 기록

일반판의 한국어·영어 현지화 **37개 파일·2,971개 키 전체를 대조**하고, 확인된 의미 누락·용어 불일치·영어 표현 문제 **14개 키를 10개 파일에서 수정**했다. 실제 게임 A 구성에서는 국가·정당·국가 정신·중점·만주 결정의 영어 표시를 표본으로 확인했다.

다만 도입 이벤트의 화면 넘침과 Korean Language를 추가한 구성의 한영 혼용을 확인했다. RT56는 정적 충돌이 남아 있으며 별도 빌드 설계만 작성했다. 정적 검사와 일부 화면 확인을 전체 분기·모든 문구의 표시 검증으로 확대하지 않는다.

이후 국가 선택 소개문 스크롤 수정과 720p 후속 실행, 이벤트 후보 미채택 및 설정 복원·정리 결과는 [UI 검증 기록](2026-10-20-ui-verification.md)에 있다. 이 문서의 A1·A2 결과는 수정 전 실행 기록으로 보존한다.

## 기준과 범위

| 항목 | 이번 작업의 기준 |
| --- | --- |
| 영어 번역 | `C:\hoi\Hearts of Korea English Translation Anime Modder's Edition` |
| 권위 있는 한국어 원본 | `C:\hoi\hearts_of_korea` |
| 원본 브랜치·HEAD | `feat/korean-focus-expansion-ai` · `d4031aaa0c1f85bb89b0e6ca21d041beade8bd26` |
| 번역 방향 | 한국어 → 자연스러운 영국 영어, 한국 배경을 모르는 영국인 독자 기준 |
| 정적 검수 | 4개 검토 범위로 나눠 37개 파일·2,971개 값 전체 대조; 관련 조건과 모호한 항목의 연결 스크립트 확인 |
| 실제 게임 버전 | `Operation Postern v1.19.3.0.c01a (b244)` |
| 진단·백업·실행 자료 | `C:\hoi\test\hok-english-translation-anime\20261020-implementation-01\` |

한국어 원본과 게임 코드는 수정하지 않았다. 기존 사용자 변경을 보존했고, 커밋·푸시·Workshop 업로드는 수행하지 않았다. 현지화 수정은 영어 표시 문자열에 한정했으며, 키·파일 배치·버전·BOM·줄바꿈 형식을 유지했다.

위의 14개는 이번 구현 시작 시점과 비교한 수정 수다. 이전 감사의 RagnaROK 안내 괄호, 선거 이벤트 시제, README의 Workshop ID 정정은 이미 기준 상태에 들어 있었으며 이 수에 다시 합산하지 않는다. 이전 결과는 [배포 전 검증 기록](2026-10-20-release-audit.md)에 있다.

## 수정한 이유와 대표 사례

`KOR_usfk_tt`의 `as volunteers`를 `as reinforcements`로 바꿨다. 한국어는 지원군을 안내하지만 실제 중점은 `owner = KOR`인 사단 3개를 직접 생성한다. 기존 영어는 HOI4의 별도 의용군 파병 체계로 읽힐 수 있어, 실제 동작에 맞는 증원 표현으로 명확히 했다. 사단 수와 주한미군이라는 맥락은 그대로다.

`newsk.2.desc`의 `opposition to Rhee and communism`은 반대의 대상에 공산주의도 포함되는 것으로 읽힐 수 있었다. 이를 `communism and opposition to Rhee`로 바꿔 대구 코뮌의 공산주의 이념과 반이승만 입장을 구분했다. 다른 사건 정보와 문단은 유지했다.

`KOR_confucian_democracy_desc`는 한국어 서술자가 주장하는 ‘동아시아에서 최초로 탄생한’이라는 의미가 빠져 있어 `the first humanistic philosophy to emerge in East Asia`로 복구했다. 이는 원문의 주장을 정확히 전달하는 수정이며, 번역자가 그 주장의 역사적 진위를 새로 판정한 결과가 아니다.

## 적용한 14개 키

파일명은 모두 `localisation/english/` 아래를 가리킨다. 긴 설명의 전후는 바뀐 부분만 적었다. 전체 문자열·원문·근거는 외부 자료의 `applied_changes.json`에 있다.

| 파일 | 키 | 이전 → 수정 후 | 근거 |
| --- | --- | --- | --- |
| `korea_focus_l_english.yml` | `KOR_usfk_tt` | `as volunteers` → `as reinforcements` | 지원군 안내와 KOR 소유 사단 3개 직접 생성 효과 |
| `korea_focus_l_english.yml` | `KOR_confucian_democracy_desc` | `a humanistic philosophy originating in East Asia` → `the first humanistic philosophy to emerge in East Asia` | 원문의 최초성 주장 복구 |
| `korea_focus_l_english.yml` | `KOR_park_heon_young_as_the_leader_desc` | `Workers' Party of Korea` → `Workers' Party of Joseon` | 도입 이벤트·정치적 혼란 설명에 나오는 동일한 해산 정당과 명칭 일치 |
| `korea_equipment_l_english.yml` | `KOR_railway_gun_equipment_1` | `520mm KHRG-1 Railway Gun` → `520mm KHRG-1 Heavy Railway Gun` | 원문의 ‘중열차포’ 수식어 복구 |
| `korea_equipment_l_english.yml` | `KOR_railway_gun_equipment_1_short` | `520mm KHRG-1 Railway Gun` → `520mm KHRG-1 Heavy Railway Gun` | 축약 명칭도 같은 구분 보존 |
| `korea_event_l_english.yml` | `newsk.2.desc` | `opposition to Rhee and communism` → `communism and opposition to Rhee` | 반대 대상의 범위를 명확히 함 |
| `HOK_KOR_communist_governance_l_english.yml` | `HOK_KOR_yeo_labor_compact_project_desc` | `check compliance with agreements and coordinate disputes with work schedules` → `check compliance with agreements, mediate disputes and coordinate work schedules` | 협약 이행 확인·분쟁 조정·작업 일정 조정을 각각 전달 |
| `HOK_KOR_communist_governance_l_english.yml` | `HOK_KOR_pak_production_retooling_project_desc` | `We have raised the plan.` → `We have raised the production targets.` | 뒤 문장의 더 높은 생산 실적 요구와 연결 |
| `HOK_KOR_common_followup_l_english.yml` | `HOK_KOR_cmn_smoke_withdrawal_desc` | `every ship cannot turn away` → `not every ship can turn away` | 함정별 차례와 간격을 설명하는 부분 부정 보존 |
| `HOK_KOR_constitutional_followup_l_english.yml` | `HOK_KOR_cm_allied_observers_desc` | `the navy signals, and the air force requests for support` → `the navy records signals, and the air force records requests for support` | 육·해·공군 모두의 공통 동작인 ‘기록’을 명시 |
| `HOK_KOR_fascist_staff_l_english.yml` | `HOK_KOR_nrsc_field_report_system_desc` | `Current position in the report?` → `Where is the report now?` | 보고서 위치와 부대 위치를 혼동하는 원문의 대화와 책상이라는 답변 연결 |
| `HOK_KOR_fascist_followup_l_english.yml` | `HOK_KOR_nrsc_reconstruction_secretariat_desc` | `the post-Eulhae Mutiny regime` → `the regime established after the Eulhae Military Uprising` | 기존 중점 제목과 을해군란 명칭 일치, 자연스러운 문장 연결 |
| `HOK_KOR_fascist_procurement_l_english.yml` | `HOK_KOR_fascist_procurement_programs_desc` | `the Eulhae Mutiny` → `the Eulhae Military Uprising` | 실제 선행 중점 제목과 일치; 문장 속 관사 `the`는 소문자 유지 |
| `HOK_KOR_industry_expansion_l_english.yml` | `HOK_KOR_university_industry_labs_desc` | `test problems encountered in production and try new processes` → `investigate problems encountered in production and test new processes` | 생산 문제 조사와 새 공정 시험을 자연스럽게 구분 |

정책 설명의 비용·기간·동시 진행 제한·취소·미환급 조건은 이 수정으로 바뀌지 않았다. 문장을 자연스럽게 만들기 위한 전면 재작성이나 설명 축약은 하지 않았다.

## 정적 검사와 독립 재검토

| 항목 | 결과 | 확인 범위 |
| --- | --- | --- |
| 원본·영어 파일 및 키 대응 | PASS | 각각 37개 파일·2,971개 키, 누락·추가 0 |
| 중복 키 | PASS | 검사한 현지화 범위에서 0 |
| BOM·UTF-8·영어 헤더·파일명·경로 | PASS | 37개 영어 파일 |
| 기본 문자열 형식·이스케이프·키 버전 | PASS | 기존 버전 생략 18개도 보존 |
| 보호 구문·동적 표현·개행 | PASS | 원본 대조와 수정 전후 검사; 영어 어순에 따른 기존 색상 이동은 별도 검토 |
| 전체 텍스트 대조 | 수행 | 37개 파일·2,971개 값; 연결 스크립트 확인은 조건과 모호한 항목을 중심으로 진행 |
| 수정한 14개 값 독립 재검토 | PASS | 실제 값·한국어 원문·승인안 일치, 의미·영국 영어·최소 변경 범위 확인 |
| 수정 파일의 전체 바이트 비교 | PASS | 10개 파일이 실행 전 백업에 승인된 문자열 수정만 반영한 결과와 일치 |

전체 텍스트를 읽었다는 사실은 모든 인명·실제 역사·모든 게임 효과를 독립적으로 입증했다는 뜻이 아니다. 정적 검사 통과도 엔진의 모든 치환이나 화면 표시를 보장하지 않는다. 원문과 영어에 공통으로 없는 키는 단순한 양언어 키 비교만으로 찾을 수 없다.

## 실제 게임 A 확인

일반판 Hearts of Korea와 이 영어 번역만 활성화하고 English로 1936년 한국 새 게임을 확인했다. 두 A 실행 모두 로그의 활성 모드는 2개였고, 게임 버전은 `1.19.3.0.c01a (b244)`였다. 실행 구성에서 DLC 36개를 사용했다. Korean Language·구번역·RT56는 A 구성에 넣지 않았다.

| 확인 항목 | 결과 | 실제 범위와 한계 |
| --- | --- | --- |
| 국가 선택·국호·정당 | 표본 PASS | 확인한 한국 화면에서 영어 출력 |
| 국가 정신·중점·만주 결정 | 표본 PASS | 화면에서 본 제목·설명·툴팁의 영어 출력; 모든 분기·결정 전수 확인 아님 |
| 엔진의 영어 문자열 선택 | 표본 PASS | 원본 값과 구분되는 영어가 실제 화면에서 선택됨; 37개 파일 전체의 우선순위 증명 아님 |
| 도입 이벤트 `kor_events.0.d` | FAIL | A1의 1280×720, A2의 1920×1080, UI 배율 1.0에서 초기 표시가 화면 아래로 넘침 |
| 후반 분기·수정 14개 문구 전체의 실제 표시 | NOT TESTED | 정적 재검토와 구별함 |

A1에서는 첫 중점 완료 뒤 도입 이벤트를 확인했다. 두 번째 실행 A2에서도 같은 이벤트의 초기 넘침을 확인했으며, 해당 확인은 일시정지 상태에서 진행했다. 해상도를 1920×1080으로 바꾼 것만으로 초기 넘침이 해결됐다고 판정하지 않았다.

이벤트 본문을 잘 보이게 하려고 원문의 정보를 삭제하거나 임의로 요약하지 않았다. 위 FAIL은 이 두 실행에서 관찰한 초기 표시를 가리킨다. 다른 이벤트 전체가 같은 문제를 갖는다고 확대하지 않는다.

## Korean Language 비교 B

B는 A에 Korean Language를 추가한 별도 실행이다. `dlc_load.json`의 저장 순서는 **Korean Language → 일반판 원본 → 영어 번역**이었고, 게임 로그에서 활성 모드 3개를 확인했다. 1920×1080 환경에서 기본 메뉴는 한국어, 한국 국호·정당·중점과 일부 한국 승점 이름은 영어로 표시됐다.

**영어만으로 플레이하는 구성을 목표로 한 이번 B 결과는 한영 혼용 FAIL**이다. 다만 한국어 메뉴가 나온다는 사실과 한국 모드의 일부 영어가 유지된다는 사실을 함께 기록한다. Korean Language가 모든 영어를 덮어쓴다고 결론 내리지 않는다.

앞서 확인한 중복 키 79개를 이번 화면에서 각각 검사한 것은 아니다. 다른 유효 순서를 비교하는 B2는 실행하지 않았으며, Korean Language와 관련된 모든 글꼴·UI 조합의 호환성을 판정하지 않았다. 원본의 의존성을 수정해 결과를 맞추지 않았다.

## RT56와 원문 확인 사항

RT56 구성 C는 실행하지 않았다. 서로 다른 지역을 뜻하는 주 ID 8개의 **정적 호환성 FAIL**을 유지한다. 공통 값이 같은 2,691개, 공통 값이 다른 25개, RT56 전용 27개를 합쳐 대상 키는 2,743개이며, 일반판 전용 255개는 RT56 빌드에 넣지 않는 설계다. 별도 번역 빌드의 생성·배포·게임 검증은 완료하지 않았다. [RT56 지원 설계](rt56-compatibility-design.md)에 구조와 확인 조건이 있다.

다음은 번역으로 숨기지 않고 남긴 원본 범위의 확인 사항이다. 상세 근거와 확정 수준은 [한국어 원문과 구현의 확인 사항](source-review-notes.md)을 따른다.

- RagnaROK `.7`의 제목·본문·선택지 세 키는 원본과 영어 모두에 없다. 2,971개 기존 키의 대응 PASS와 구별한다.
- 전함 설명의 두 번째 함선은 원문 30%, 실제 보상은 35%다. 영어는 원문 수치를 유지했다.
- 보병 4개 사단의 수도 배치 안내와 `random_owned_controlled_state`·우선 주 ID 835의 구현이 다르다. 835가 적혀 있다고 부대가 반드시 Hararghe에서 생성된다고 단정하지 않는다.
- RagnaROK의 고정 날짜·전 세계 통합·선전포고 안내는 지연 이벤트와 전쟁 명분 생성만으로 모두 보장되지 않는다. 실제 전쟁을 절대로 일으키지 않는다는 뜻도 아니다.
- 장비 정식·축약 명칭, 인두 정복 설명의 방향, 곡명, `SOU` 참조와 군정 연락인계의 범위는 확인 수준을 나눠 기록했다. 추측으로 통일하지 않았다.
- 시민 영향력 0~100 제한은 일반적인 경계 처리일 수 있다. 확정 원문 오류로 분류하지 않았다.

이 항목들의 게임상 결과는 별도로 확인해야 한다. A의 영문 표본 출력이 정상이라는 이유로 원문 문제까지 해결됐다고 보고하지 않는다.

## 증거 위치와 이전 기록의 구분

외부 전용 폴더에는 다음 자료가 있다. 이 자료들이 저장소에 포함돼 있다고 가정하지 않는다.

```text
C:\hoi\test\hok-english-translation-anime\20261020-implementation-01\
```

| 자료 | 내용 |
| --- | --- |
| `baseline.json`, `translation_before/`, `git_diff_before.diff` | 시작 상태·백업·기존 변경 구분 |
| `review_core.json`, `review_events.json`, `review_policies.json`, `review_root.json` | 전체 텍스트 대조, 제안과 근거 |
| `review_coverage.json` | 중복 없는 검토 범위 37개 파일·2,971개 키 |
| `applied_changes.json` | 실제 적용 14개 값·10개 파일과 파일 해시 |
| `localisation_before.json`, `localisation_after.json` | 정적 검사 전후 결과 |
| `post_patch_review.json` | 실제 적용값 및 바이트 단위 독립 재검토 |
| `runtime_a/screenshots/`, `runtime_a/logs/` | A1의 영어 표본 화면과 게임 로그 |
| `runtime_a_1080/screenshots/`, `runtime_a_1080/logs/` | A2의 1080p 도입 이벤트 초기 표시와 로그 |
| `runtime_b/screenshots/`, `runtime_b/logs/`, `runtime_b/dlc_load_test.json` | B의 한영 혼용 화면·로그·저장된 모드 구성 |

이전 [배포 전 검증 기록](2026-10-20-release-audit.md)의 게임 NOT TESTED와 화면 제어 연결 실패는 **그 감사 시점의 기록**이다. 이번 실행에서는 연결이 복구돼 위 A1·A2·B를 직접 확인했다. 초기 실패를 담은 `runtime_attempt.json`도 이번 후속 실행의 최종 판정으로 사용하지 않는다.

다음 게임 확인은 [게임 내 검증 절차](in-game-verification.md)를 바탕으로 실행 조건·확인 화면·미검증 범위를 나눠 기록한다.
