# 2026-11-09 재벌 영어 용어 반영

일반판 영어 번역의 재벌 관련 **8파일·43개 표시값**을 수정했다. RT56에서 검토된 용어 개선을 일반판 한국어와 대조해 공통 키의 문구에 적용했다.

## 기준과 범위

- 번역 모드 시작 기준: `441b019` / 작업 트리 변경 없음.
- 일반판 읽기 전용 원본: `C:\hoi\hearts_of_korea`, `596b221` / 작업 트리 변경 없음.
- RT56 읽기 전용 대조 자료: `C:\hoi\hearts_of_korea_Road_to_56`, `95d801f` 및 기존 미커밋 용어 수정. 해당 저장소의 `docs/implementation/2026-11-09-chaebol-english-terminology.md`, `tools/hok_english_terminology_lock.json`과 실제 영어 최종 문구를 확인했다.
- 대상 43개 키의 한국어 값은 일반판과 RT56에서 동일하다. 수정 전 영어 값도 RT56의 용어 수정 전 보관본과 일치함을 확인했다.
- 일반판의 키·경로·버전·치환·수치·조건을 유지했다. RT56 전용 `HOK_KOR_chaebol_influence_change_tt`와 생성기·잠금은 가져오지 않았다. 이 번역 수정은 RT56 지원 구현이 아니다.

## 용어 선택

| 문맥 | 적용한 표현과 근거 |
| --- | --- |
| 투자·협력·통제·체포의 대상인 인물과 경제 권력집단 | `corporate oligarchs`. 원문의 경제 권력과 정경유착에 대한 비판을 전달한다. |
| 영향력 수치와 단계 | `Oligarchic Influence`, `Oligarchic` / `Oligarch-led`. 이름·설명·결정·툴팁의 같은 수치를 일관되게 가리킨다. |
| 좁은 시민사회 창의 세력 제목 | `Oligarchs`. 연결 설명에서 세력의 역할을 풀어 쓴다. |
| 기업집단·공공 소유·국유화 대상 | `conglomerates`, `Nationalised Conglomerates`, `Bring the Conglomerates into Public Ownership`. 기업과 소유주를 구분한다. |
| 소유주 재산의 국유화 | `Nationalise the Oligarchs' Assets`. 원문의 재산·축적한 부와 국유화 동사를 유지한다. |

대공황 설명의 기업집단에는 `family-controlled conglomerates`, 기업별 주문에는 `individual conglomerates`를 썼다. 원문의 착취·탐욕·군정의 강압과 투자·공급망 설명을 보존하고 별도의 독점·담합·범죄 주장을 추가하지 않았다. 내부 키·변수·함수의 `chaebol` / `jaebeol`은 식별자로 유지한다.

## 변경 파일과 연결 문맥

| `localisation/english/` 아래 파일 | 변경값 | 문맥 |
| --- | ---: | --- |
| `HOK_KOR_civic_focus_l_english.yml` | 3 | 산업협력·공공 소유 중점 |
| `HOK_KOR_civic_state_l_english.yml` | 19 | 국민정신·영향력·정책·지원과 견제·조달 설명 |
| `HOK_KOR_civic_ui_l_english.yml` | 6 | 시민사회 창·지원과 견제·기관 장악·정책 표식 |
| `HOK_KOR_fascist_procurement_l_english.yml` | 1 | 기존 기업별 주문 설명 |
| `korea_event_l_english.yml` | 2 | 도입·선거 사건 |
| `korea_focus_l_english.yml` | 8 | 노조·재산 국유화·반동분자·협력·군정 통제 중점 |
| `korea_ideas_l_english.yml` | 2 | 대공황 설명·국유화 기업집단 |
| `replace/korea_decisions_l_english.yml` | 2 | 재벌 결정 범주와 설명 |
| 합계 | **43** | 영어 8파일 |

일반판의 `common/national_focus/korea.txt`, `common/national_focus/HOK_KOR_civic_legacy_focus.txt`, `common/decisions/KOR_decision.txt`, 시민사회 결정·효과·트리거·scripted localisation 및 국민정신 정의를 확인했다. 국유화 효과, 공공 소유 정책, 삼성·현대 주문과 협력 표식의 문맥에 맞춘 표현이다. `HOK_KOR_policy_cooperation`은 RT56 후속 교정본인 `Industrial cooperation with the corporate oligarchs has been selected.`를 적용했다. 독립 검토에서도 적용 후 실제 diff의 의미·어조·문체에 추가 지적 사항이 없었다.

## 검증과 한계

기존 외부 `20261020-implementation-01/audit_localisation.py`를 수정·복사 없이 재사용했다. 출력 경로만 이번 외부 작업 폴더로 지정했다.

- 전체 **47파일·3,108키**의 한국어·영어 대응을 확인했다. 누락·추가·중복·문법·경로·키 버전·보호 토큰·동적 대괄호·개행 차이는 0이다.
- 수정 전 외부 백업과 바이트를 대조해 정확히 8파일·43개 값만 바뀌고, 해당 값 외의 바이트·키·버전·따옴표 경계·수치·토큰·UTF-8 BOM·각 파일의 기존 줄바꿈 형식이 유지됨을 확인했다.
- 영어 표시값 전체에서 독립된 단어 `chaebol` / `jaebeol`은 남아 있지 않다. 내부 식별자는 보존했다.
- 기존 검사 후보인 색상 순서 차이 3개, 자연어 대괄호 차이 1개, 수치 표면 비교 후보 118개, 양끝 공백 후보 2개는 직전 검사 기록과 같다. 이번 43개 값의 수정 전후 숫자·부호와 기술 토큰도 동일하다. 후보 개수를 오류 개수로 해석하지 않는다.
- 확인 대상으로 고정한 두 원본의 205파일과 두 원본의 HEAD·작업 상태를 보존했다. 번역 모드도 문서 기록 전에는 해당 영어 8파일 외의 추적 파일이 모두 같았다.

**실제 게임 화면은 이번에 검증하지 않았다.** 최종 표시·잘림·동적 치환은 미검증이며 기존 긴 도입 이벤트의 넘침도 해결한 작업이 아니다. 게임 실행·설정·플레이세트는 변경하지 않았다. 앞선 원본 업데이트 기록의 `Chaebol Influence` 등은 당시 용어이며 이번 기록이 현재 재벌 영어 표현을 설명한다.

검증 근거는 `C:\hoi\test\hok-english-translation-anime\2026-11-09-chaebol-terminology\`의 `baseline.json`, `changes.json`, `localisation_audit.json`, `preservation_report.json`과 수정 전 영어 8파일의 `backups/`다. 일회성 코드 파일·시험 모드·임시 계측을 만들지 않아 정리할 임시 코드는 없다. 결과와 백업은 외부에 보존했다. 커밋·푸시·업로드는 수행하지 않았다.
