# 2026-10-31 원본 업데이트 반영

일반판 한국어 원본의 신규 6파일·73키를 영국 영어로 번역하고, 원문 전체와 연결 스크립트를 대조한 뒤 독립 검토했다. 기존 현지화 38파일·2,975키는 변경하지 않았다. 현재 일반판 원본과 영어 번역은 각각 **44파일·3,048키**다. 실제 게임 화면은 이번 작업에서 확인하지 않았다.

## 원본 기준과 범위

| 구분 | 읽기 전용 원본과 기준 |
| --- | --- |
| 일반판 | `C:\hoi\hearts_of_korea`, `07de265c1e992abb6584bdfcdf140320188c07f9`, 시작 시 작업 트리 변경 없음 |
| RT56판 | `C:\hoi\hearts_of_korea_Road_to_56`, `e871bd1246152c2d32f67c43181441ff31a706e7` 및 시작 시 존재한 미커밋 기능 연동 업데이트 |
| 번역 모드 | `294304b2803757f27236a2ca555e37078be00b8b`에서 시작, 시작 시 작업 트리 변경 없음 |

일반판 직전 `860efe7`과 현재 커밋 사이의 기존 한국어 현지화 값 변경·삭제는 없다. 게임 기능과 그림은 기본 모드가 제공하므로 이 서브모드에는 영어만 추가했다. 원본 두 폴더, 게임 코드·GUI·descriptor·의존성·Workshop 정보·게임 설정은 수정하지 않았다. 커밋·푸시·업로드는 수행하지 않았다.

| 추가한 파일 (`localisation/english/`) | 키 수 | 번역 범위 |
| --- | ---: | --- |
| `HOK_KOR_civil_nuclear_research_l_english.yml` | 6 | 핵분열 실험, 민간 원자로 투자·건설 기술 |
| `HOK_KOR_mio_specializations_l_english.yml` | 31 | 군수산업조직 특성 15종과 별도 포인트 사용 안내 |
| `HOK_KOR_naval_captains_l_english.yml` | 13 | 함장·해전 이력·훈장·경험치·제독 진급 UI |
| `HOK_KOR_raids_l_english.yml` | 10 | 해군 특공 범주, 나가사키 급습과 조건·성과·손실 |
| `HOK_KOR_research_network_l_english.yml` | 4 | 시설 조건부 배치와 과학자별 한 번만 성장하는 보상 |
| `HOK_KOR_soyang_water_gates_l_english.yml` | 9 | 소양강댐 수문 개방·정상화, 비용·피해·취소·수리 |

## 용어와 의미 대조

- 설치된 HOI4 `1.19.3` 영어에서 시설명 `Land Warfare Facility`, `Naval Engineering Facility`, `Aerodynamics and Avionics Facility`, `Nuclear Research Facility`를 확인했다. 습격 결과는 `Limited Success / Success / Critical Success`, 함장 UI는 `Citation`·`veterancy`를 따랐다.
- 일반 문장은 `organisation`·`specialisation`·`armour`·`defence`·`harbour` 등 영국식 표기를 사용했다. 댐은 기존 번역의 `Soyanggang Dam`으로 통일했다.
- `현해탄`은 일본으로 건너가 나가사키를 공격하는 문맥상 `Korea Strait`로 옮겼다. 좁은 지리적 의미의 현해탄과 대한해협이 언제나 같다는 주장은 아니다. [국립중앙박물관 번역 사례](https://vcm.museum.go.kr/ENG/contents/E0202030000.do?exhiSpThemId=650179&listType=list&menuId=&schM=relic_view)와 [영국 지명위원회 자료](https://assets.publishing.service.gov.uk/media/679903b2d4f0d327e7707148/South_Korea_factfile.pdf)를 참고한 문맥상 선택이다.
- 습격 지휘력은 배정 의미를 보존해 `Allocates 40 Command Power`로 썼다. `10%p`는 `10 percentage points`다. 아군의 현재 조직력·전력 손실과 적 함선 피해를 구별하고, 준비 120일·해병 대대 최소 3개·수송선 40척·한 번 사용·전쟁·영토 조건을 보존했다.
- 수문의 정치력 25와 14일은 개방·정상화 양쪽에 적용했다. 서울·춘천 프로빈스와 경기·강원 주를 구별하고, 피해 재발·환불 없음·기존 피해의 별도 수리·다른 원인의 침수 유지도 옮겼다.
- 연구망은 시설 지급과 과학자 성장을 분리했다. 일반판 주 참조 `525 / 1030 / 1029 / 1028`을 보존했다. RT56 해군·항공·핵의 `920 / 1144 / 918`과 혼용하지 않았다.

RT56 신규 한국어도 73키이나 영어는 5파일·60키만 추가됐다. RT56판은 공용 함장 UI 13키에 기본 게임·RT56 영어를 사용하도록 원본의 영어 채널 한국어 파일을 이식하지 않았다. 일반판 원본에는 그 파일이 있어 이 서브모드에 영어를 추가했다. RT56 영어는 대조 자료이며 한국어가 최종 기준이었다. RT56 민간 원자로 툴팁에 빠진 `Civilian`도 이 일반판 번역에는 명시했다. RT56 원본은 수정하지 않았다.

## 검증과 남은 확인

기존 외부 현지화 검사 도구를 재사용하고 출력만 이번 전용 외부 폴더에 저장했다. 기존 도구 파일은 변경하지 않았다.

| 검사 | 결과 |
| --- | --- |
| 파일·키 대응 | PASS — 원본·영어 각각 44파일·3,048키, 누락·추가 없음 |
| 중복 키·경로·버전·문자열 문법 | PASS |
| UTF-8 BOM·영어 헤더·미번역 한국어 | PASS |
| 변수·치환·색상·아이콘 등 보호 토큰과 이스케이프 개행 | PASS |
| 신규 73키 원문·영어 의미·수치·조건 독립 검토 | PASS |
| 기존 현지화 38파일 보존 | PASS — 시작 시 SHA-256과 동일 |
| 두 원본 현지화·Git HEAD·작업 상태 보존 | PASS — 시작 시 기록과 동일 |
| 신규 영어의 실제 화면·치환·색상·잘림·로드 순서 | NOT TESTED |

전체 검사에 남은 색상 순서 차이 3개와 자연어 대괄호 차이 1개는 기존 검토 항목이며 신규 문구에는 없다. 신규 숫자 표면 비교 후보는 습격의 `10%p`/`10 percentage points` 한 건이며 의미·수치가 같다. 정적 통과는 게임 표시 통과가 아니다.

`HIRED_NEW_ADMIRAL_DESC`는 한국어와 설치 게임 영어 모두 함선 경험치가 “초기화/reset”된다고 한다. 반면 `CAPTAIN_PROMOTION_EXPERIENCE_PENALTY`는 지정 비율 감소를 설명하며, 원본의 31 October 기능 연동 기록에는 실제 25% 감소 관측이 있다. 번역으로 원본 UI 표현을 고치지 않고 `reset`을 보존했다. 이번 작업에서 진급을 직접 재현하지 않았다.

향후 일반판과 이 번역을 English로 실행해 신규 중점·MIO 특성·연구망·습격·수문·함장 UI를 확인해야 한다. 특히 긴 습격 설명의 표시와 동적 치환, 저장된 옛 함장 이력의 문자열은 정적 검사로 확인할 수 없다. 기존 도입 이벤트 넘침과 RT56 화면 미검증 상태도 유지된다.

근거는 `C:\hoi\test\hok-english-translation-anime\20261031-source-update-01\`의 `before.json`·`localisation_audit.json`·`completion_report.json`에 보관한다. 일회성 코드 파일·임시 모드·설정 변경은 생성하지 않았으며 정리·복원할 항목도 없다.
