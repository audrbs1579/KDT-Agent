# Azure 리소스 선정과 최신 공식 근거

[문서 목록](00_보고서_안내.md)

기존 조사 정보 기준: 2026-10-18~20 · 참고 기준 정리: 2026-10-21 · 과정 종료 Forms 경로 보완: 2026-10-28

## 1. 확인 수준

이 문서의 리소스는 당시 공식 제품 문서를 조사한 **구현 후보·참고안**입니다. 지원 형식·API 버전·분석기·모델·SKU·리전은 실제 테스트·운영에서 바꿀 수 있으며 최종 제품 선택이나 지원 보증이 아닙니다. 계정·구독·권한·쿼터·정책 조회의 상세 확인값은 중복 관리하지 않고 06 실환경 확인 기록을 기준으로 합니다.

- **공식 기능 확인:** 해당 제품 문서가 설명하는 기능.
- **실환경 조회 기록:** 구독·관리자 역할·모델별 쿼터·정책 할당 목록은 06의 확인 범위를 따릅니다. 조회 성공과 실제 배포·서비스 동작 성공은 다릅니다.
- **테스트·운영 확인:** 실제 연결·권한·대상·완료 조건을 확인해 운영에 적용하고, 모델 품질·속도·가성비·파싱 결과를 운영하면서 측정·개선합니다. 가격 후보의 품질을 사전에 확정했다고 주장하지 않습니다.

세 항목은 서로 대체하지 않습니다. 최신 제품이어도 구독에서 제공되지 않을 수 있고, 제공되어도 우리 사이트 자동화를 보장하지 않습니다.

## 2. 기준 리소스

### 2.1 리소스는 어디에 만들어지는가

- **새로 만드는 Azure 리소스는 모두 `@msacademy` 계정으로 접근하는 회사 엘릭서 구독**(`7ad28d1d-…`, 소속 디렉터리 `msaischool.onmicrosoft.com`)에 생성합니다. (R17 AI Search는 R07 벡터 검색으로 부족할 때만 도입합니다.)
- **리전은 고정하지 않습니다.** 아래 표의 `Korea Central`·`East US 2`는 조사·비교 당시의 배치 예시입니다. 상황에 따라 다른 리전에 생성하거나 다른 지역에서 처리하며 실제 테스트·운영에서 선택·변경합니다. 생성 위치·저장 위치·AI 처리 위치는 서로 다를 수 있고 Global 배포가 국내 처리만을 보장하지도 않습니다. 변경 시 정책·권한·데이터 이동·지연·비용을 확인합니다.
- **`@elixirr`·`@dataschool`에는 Azure 리소스를 만들지 않습니다.** 두 조직은 Azure 구독 없이 Entra **연결 앱 등록·관리자 동의**와 Teams 앱 설치만 합니다. 앱의 인증서는 엘릭서 구독의 R09 Key Vault에 보관합니다.
- **R18은 새로 만들지 않습니다.** `@elixirr`·`@dataschool`이 이미 쓰고 있는 M365(Exchange·Teams·SharePoint)를 연결해서 씁니다.
- **R18의 파일 위치는 KDT 폴더 구조를 참고합니다.** 수강생 팀 `일반`(배포 자료·녹화), 기수별 운영 채널(매뉴얼·상담·설문 결과·내부 출결), 강사팀(양식·보고서·평가문제·호명 출석부)을 구분합니다. 이 예시는 Azure 리소스나 신규 저장소를 만드는 지시가 아니며 실제 ID·권한·연동은 별도로 확인합니다.
- 아래 표의 **연결 계정** 열은 "그 리소스가 실제 업무 데이터를 주고받는 조직"입니다. 리소스 생성 위치와는 다른 개념입니다. 예를 들어 Container Apps는 엘릭서 구독에 생성되지만, 직원 대시보드는 `@elixirr` 로그인으로, 수업방 Teams 봇은 `@dataschool`로 연결됩니다.

### 2.2 기준 리소스 표

선정 중심 표기: **기능** = 이 기능이 없으면 업무가 성립하지 않아 기능을 먼저 봄 / **가격** = 비슷한 기능 중 사용량 과금·저가 등급을 먼저 봄 / **속도** = 응답 지연·처리량을 먼저 봄. 근거는 [2.3](#23-선정-중심-조사-결과)에 있습니다.

| ID | 선정 리소스 | 역할 | 생성 위치(구독·리전 예시) | 연결 계정 | 선정 중심 | 선택 이유·배치 |
|---|---|---|---|---|---|---|
| R01 | Microsoft Foundry Agent Service | 명령을 이해하고 도구를 고르는 AI | `@msacademy` 엘릭서 구독 · Korea Central | `@msacademy`(관리 ID). 결과는 R02를 거쳐 `@elixirr`·`@dataschool`로 전달 | 기능 (모델은 작업별 가격/성능) | 엘릭서 구독의 Foundry 프로젝트. 관리형 prompt agent 기준, 업무 상태는 자체 DB |
| R02 | Azure Container Apps | 대시보드·업무 서버 실행 | `@msacademy` 엘릭서 구독 · Korea Central | `@elixirr`(직원 로그인·대시보드·직원 Teams 봇), `@dataschool`(수업방 Teams 봇·탭) | 가격 + 속도 | 웹/API·Teams 엔드포인트·도구 서버. 사용량 과금·자동 확장, 최소 1 인스턴스로 Teams 첫 응답 지연 방지 |
| R03 | Azure Container Registry | 배포 프로그램 보관 | `@msacademy` 엘릭서 구독 · Korea Central | `@msacademy`만(외부 연결 없음) | 가격 | Container Apps 이미지 버전 관리. 이미지 수가 적어 Basic 등급부터. 원문 ACR 지표와 혼동 금지 |
| R04 | Azure Functions + Durable Functions | 예약·승인 대기·복구 | `@msacademy` 엘릭서 구독 · Korea Central | 실행 시 `@elixirr`(Outlook 일정·직원 알림)·`@dataschool`(수업 이벤트·수업방 구성원·학생/강사 알림) 연결 앱 사용 | 기능 + 가격 | 장기 업무 흐름(1개월 단위 이벤트 생성, 전날 강사 확인 등). 신규 앱은 Flex Consumption(실행분만 과금) |
| R05 | Durable Task Scheduler | 예약 업무의 진행 상태를 기억 | `@msacademy` 엘릭서 구독 · Korea Central(R04와 같은 리전 권장) | `@msacademy`만 | 기능 → 가격 | 최신 Durable Functions 문서의 권장 저장 공급자. 운영 시작은 Consumption SKU, 운영량이 커지면 Dedicated |
| R06 | Azure Service Bus | 밀린 일을 안전하게 전달 | `@msacademy` 엘릭서 구독 · Korea Central | `@msacademy`만(작업 전달 전용) | 기능 + 가격 | 발송·문서·웹·PC 작업 분리, 실패 대기함. Standard 종량제부터. 예약 업무 자체는 R04/R05가 책임 |
| R07 | Azure Database for PostgreSQL Flexible Server | 공동 업무 장부·검색 | `@msacademy` 엘릭서 구독 · Korea Central | `@msacademy`(관리 ID·사설 접근). 세 조직의 업무 기록을 `organization_id`로 구분 저장 | 기능 + 가격 | 관계형 데이터·JSON 설정·`vector` 의미 검색을 한 DB로 통합. 처음부터 정식 운영용 General Purpose(2 vCore부터) |
| R08 | Azure Blob Storage | 원본·증거·내보내기 파일 | `@msacademy` 엘릭서 구독 · Korea Central | 원본은 `@dataschool` SharePoint 우선. Blob은 그 외 처리 사본만 | 가격 | 기존 SharePoint에 없는 파일 또는 필요한 처리 사본. 보관 등급 자동 이동·기한 삭제 |
| R09 | Azure Key Vault + Managed Identity | 비밀과 서비스 신원 | `@msacademy` 엘릭서 구독 · Korea Central | `@elixirr`·`@dataschool` 연결 앱 인증서, 외부 사이트 자격 증명 보관 | 기능(보안) | 앱 인증서·사이트 자격 증명 보호, 비밀값을 모델에 전달하지 않음. HSM이 필요 없어 Standard 등급 |
| R10 | Azure Monitor / Application Insights | 실행·장애 관제 | `@msacademy` 엘릭서 구독 · Korea Central | `@msacademy`만. 경보는 `@elixirr` 운영 채널로 발송 | 가격 | 지연·실패·비용·연결 만료 추적. 수집량 과금이라 샘플링·보존 기간 관리, 민감 원문 로그 제외 |
| R11 | Foundry Browser Automation / Playwright Workspaces | 웹사이트를 여는 손 | `@msacademy` 엘릭서 구독 · 지원 리전은 생성 전 확인 | `@dataschool` Teams 웹 일정·참석 CSV, 외부 LMS·출결 사이트 | 기능 | 채널 수업 생성·변경, 과정 종료 만족도 Forms 템플릿 복제·제목/날짜/강사·응답 설정·링크 확보, 파일 업로드·다운로드. 사이트별 검증된 절차 사용. M365 로그인·조건부 접근은 별도 확인하며 Windows 데스크톱 제어와 구분 |
| R12 | 전용 Azure Windows VM + Power Automate for desktop | 데스크톱 프로그램을 다루는 손(필요 시) | `@msacademy` 엘릭서 구독 · Korea Central | 브라우저 밖 데스크톱 작업 필요 시 사용 | 기능 → 가동 시간으로 가격 조절 | 웹 브라우저로 안 되는 데스크톱 작업이 필요할 때만 운영 시간 가동 |
| R13 | Foundry computer use tool / `computer-use-preview` | 화면을 보고 다음 클릭 제안 | `@msacademy` 엘릭서 구독 · **테스트·운영에서 선택할 지원 리전** | `@msacademy`. 조작 대상은 허용된 실행 환경 | 기능 | 당시 리전별 제공 이력은 06 참고. 지원 모델·리전·비용을 테스트·운영에서 재선택하며 정형 작업은 Playwright/PAD 우선 |
| R16 | Azure Content Understanding in Foundry Tools (+ 서버 내 한글 `.hwp`/`.hwpx` 파서·변환기) | 비정형 문서·이미지·영상에서 필요한 정보 추출 | `@msacademy` 엘릭서 구독 · Korea Central(지원 여부 확인) | 입력 자료는 `@dataschool` 교안·수강생 비정형 문서(자소서·이력서·포트폴리오·증빙)·수업 녹화 | 기능 + 가격 | PDF·Word(`.docx`/`.doc`)·PowerPoint(`.pptx`/`.ppt`)·Excel·**HTML(`.html`)/Markdown(`.md`)/TXT/RTF/ODT**·이미지·음성·영상은 R16이 기본 지원하며, **아래아한글(`.hwp`/`.hwpx`)은 서버(R02) 내 전용 파서(`.hwpx` XML/표 추출, `.hwp` OLE 파싱 또는 PDF 변환)로 전처리**해 추출. 분석량 과금이라 필요한 문서·표본 구간만 분석 |
| R17 | Azure AI Search | 검색 전용 확장 옵션 | 도입 시 `@msacademy` 엘릭서 구독 · Korea Central | `@msacademy`만 | 가격(보류 사유) | R07 검색이 요구량/기능을 충족하지 못할 때 도입. 처음부터 중복 인덱스 운영 안 함 |
| R18 | 기존 Exchange Online·Teams·SharePoint·Forms | 일정·소통·사람의 문서 공동 편집·Forms 응답 | **Azure에 생성하지 않음** — 기존 M365 테넌트 | `@elixirr`: 직원 일정·메일·Teams / `@dataschool`: 채널 수업·교육 자료·Forms. 실제 Teams·SharePoint 경로·채널 유형은 구조 확인 후 확정 | 가격(기존 라이선스 재사용) | Graph로 허용 파일을 다운로드·파싱하고 별도 결과 파일 저장. 원본 셀·Word 편집과 퀴즈 검수·정답 설정/게시 등은 해당 기능의 사람 업무. 과정 종료 만족도는 R11 화면 실행 + R19 응답 수집으로 자동화. `Sites.Selected`가 무인 Excel 셀 API를 허용하는 것은 아님 |
| R19 | Azure Logic Apps Consumption + Microsoft Forms API 연결 | 강의별 새 응답 수집·상세 조회·Service Bus 전달 | `@msacademy` 엘릭서 구독 · 커넥터 지원 리전 확인 | `@dataschool` 조직 계정으로 최초 OAuth 인증. Graph 앱 전용 인증과 별개 | 기능 + 사용량 과금 | 양식별 form_id·문항 매핑·워크플로 연결. 새 양식 자동 배치·인증 재사용·중복/장애 복구는 POC 검증. 최소 배치 권한·실행 이력 접근 제한 |

### 2.3 선정 중심 조사 결과

**기수별 하루 강의는 1개이며 같은 날 여러 기수가 동시 운영됩니다. 만족도는 각 기수의 전체 과정 종료 시 1회, 객관식 2개·주관식 1개의 Forms만 운영합니다.** R11/F19의 승인된 템플릿 준비 → 과정별 R19 연결 → 과정 종료 확인·기본 안내 1회 → 응답 수집·DB 집계·결과 저장을 개발합니다. 공식 커넥터의 응답 수집 기능은 확인했으며 생성/복제 액션을 제공한다고 가정하지 않습니다. UI·인증·양식별 연결은 실제 검증 대상입니다. 퀴즈·참가 신청 등 다른 목적 Forms의 단계는 해당 기능 기준이며 만족도 다운로드 Excel은 복구·대조용입니다. 연결 Excel과 다운로드 사본도 구분합니다([F06 상세](기능/F06_만족도조사.md)).

이 프로젝트의 업무는 대부분 **정해진 시각에 빠짐없이 실행되어야 하는 일**입니다. 1개월 단위 수업 이벤트 생성, 전날 강사 확인, 입퇴실·중간 출결, 퀴즈, 만족도 발송이 여기에 해당합니다. 1초 안에 응답해야 하는 일은 적습니다. 그래서 아래 순서로 판단했습니다.

1. **기능(신뢰성)을 먼저 봅니다.** 예약·재시도·복구·실패 대기함·보안처럼 없으면 업무가 깨지는 필수 기능은 생략하지 않습니다. 같은 기능을 충족하는 서비스·구현 방식은 비교해 바꿀 수 있습니다.
2. **기능이 충족되면 가격을 봅니다.** 사용량이 적고 들쭉날쭉하므로 고정 요금보다 사용량 과금·저가 등급부터 시작합니다.
3. **속도는 사람이 직접 기다리는 곳에만 따로 챙깁니다.** Teams 대화 응답과 대시보드가 여기에 해당합니다.

| 구분 | 해당 리소스 | 조사한 공식 근거 | 본 설계 판단 |
|---|---|---|---|
| 기능 중심 | R01, R04, R05, R09, R11, R12, R13 | Durable Task Scheduler는 Durable Functions 권장 저장소. Browser Automation은 GA, computer use는 프리뷰 모델 | 예약·복구·보안·웹/PC 조작은 대체 수단이 없어 기능 우선. 단, 같은 기능 안에서는 저렴한 등급부터 시작 |
| 기능 → 가격 단계 | R05 Durable Task Scheduler | Consumption: 처리 동작 수 과금, 최대 500 actions/초, 데이터 30일 보존, 고가용성 없음. Dedicated: CU당 월 고정, CU당 2,000 actions/초, 90일 보존, 3CU 시 고가용성 | 운영 시작은 Consumption(가격). 기수가 늘어 처리량·보존·고가용성이 필요하면 Dedicated |
| 기능 + 가격 | R04 Functions | 기존 Consumption 요금제는 레거시. 신규 서버리스 앱은 **Flex Consumption** 권장(실행분 과금, 가상 네트워크 지원) | 신규 함수 앱은 Flex Consumption으로 생성. Durable Task Scheduler와 함께 쓸 호스팅 조합은 배포 전 확인 |
| 기능 + 가격 | R06 Service Bus | Standard: 종량제, 가변 지연, 메시지 256KB. Premium: 고정 요금, 예측 가능한 성능, 100MB 메시지 | 메시지가 작고 양이 적어 Standard. 사설망 필수·대량 처리 시 Premium 검토 |
| 기능 + 가격 | R07 PostgreSQL | Burstable은 CPU 크레딧 방식. **공식 문서상 운영 워크로드 비권장**이며 크레딧 소진 시 성능이 급감할 수 있음. General Purpose는 일반 운영용 | 바로 정식 운영하므로 Burstable은 쓰지 않고 처음부터 General Purpose `2 vCore`(기능·안정성 우선, 가격은 가장 작은 GP 크기로 통제) |
| 가격 + 속도 | R02 Container Apps | Consumption: 초 단위 과금, 구독당 월 무료량(vCPU 180,000초 · 메모리 360,000GiB초 · HTTP 200만 건) | 사용량 과금(가격). 최소 1 인스턴스만 유지해 Teams 첫 응답 지연을 줄임(속도) |
| 가격 중심 | R03, R08, R10, R18 | ACR Basic은 개발·소량용 저가 등급. Blob 수명주기 정책으로 등급 이동·삭제. 로그는 수집량 과금 | 최저 등급·보관 정책·샘플링으로 비용 관리. R18은 기존 M365 라이선스 재사용 |
| 가격(보류) | R17 AI Search | Dedicated는 검색 단위 시간당 고정 과금. Serverless는 프리뷰(미리보기, SLA 없음) | R07 `vector` 검색으로 먼저 해결. 부족할 때만 도입 |
| 작업별 가격/성능 | AI 모델(R01에서 사용) | 08 모델 가격 비교 | 단가만 보면 표의 `gpt-5-nano`가 저렴한 Standard 후보. 작업별 한국어 품질·도구 지원·호출 가능 조건을 확인해 선정하며 특정 모델을 최저가나 필수 모델로 단정하지 않음. Batch·Flex는 지원·기한을 별도 확인 |
| 기능 + 가격 | R16 Content Understanding | 분석 대상·분량에 따라 과금 | 필요한 문서·영상 구간부터 분석하며 분량은 테스트·운영에서 조절(10 비용 참고 예시) |

## 3. 최신 기준으로 반영한 중요한 선택

### Durable Task Scheduler

2026-10-15 갱신된 공식 문서는 Durable Task Scheduler를 Durable Functions의 권장 저장 공급자로 안내하고, Consumption·Dedicated 과금 SKU를 설명합니다. 따라서 본 설계는 이를 우선 검토합니다.

스케줄러 자체가 업무 코드를 모두 실행하는 것은 아닙니다. Functions의 실행 프로그램과 함께 사용합니다. 해당 구독·리전에서 적합하지 않으면 공식 지원 저장 공급자와 비교해 선택 사유를 기록합니다.

### Agent Service, Browser Automation, Computer use는 서로 다름

- Agent Service: 에이전트의 실행·도구 호출 관리.
- Browser Automation: Playwright 기반 브라우저 작업. 공식 문서상 GA.
- Computer use: 스크린샷을 보고 클릭·입력을 제안하는 모델 루프. 현재 가이드가 사용하는 모델은 `computer-use-preview`.
- Windows VM/PAD: 실제 Windows 앱 실행과 정형 PC 작업. computer use를 붙여도 세션·인증·화면 검증이 별도로 필요.

### 비정형 문서 파일(한글 `.hwp`/`.hwpx` · PDF · HTML · Word · PPT · 이미지)은 이렇게 저장·검색

**지원 정보의 해석:** 아래 형식 목록과 한도는 조사 당시 문서의 지원 정보를 정리한 후보이며 우리 환경의 검증 완료 목록이 아닙니다. 예를 들어 인용한 서비스 한도 문서에는 `2026-06-01-preview` 안내가 있으므로 선택 API·분석기에서 같은 기능을 쓸 수 있는지 확인합니다. 실제 테스트·운영에서는 `형식·API/분석기·리전·파서 버전·샘플·결과·확인일`을 기록하고 파서·변환기·서비스를 변경할 수 있습니다. 판독 불가 자료는 사람 확인으로 남깁니다.

수강생에게 받는 커리어 멘토링 사전 자료([F12](기능/F12_멘토링_사전자료.md)), 지원서·포트폴리오([F02](기능/F02_모집_면접.md)), 이력서([F13](기능/F13_이력서_인재검색.md)), 병가·출결 증빙([F14](기능/F14_LMS_서류_반려안내.md))과 강사 교안([F07](기능/F07_퀴즈.md))은 **워드(`.docx`)뿐 아니라 아래아한글(`.hwp`, `.hwpx`), `.pdf`, 웹/노션 내보내기 파일(`.html`, `.md`), `.pptx`, 스캔 이미지(`.jpg`, `.png`) 등 비정형 자료**를 입력 후보로 봅니다. 별도 DB 대신 아래 **3단계 파이프라인(원본 보관 → 형식별 추출·전처리 → PostgreSQL JSONB·벡터 통합 저장)**을 공통 처리 구조로 설계합니다. 모든 파일의 추출 성공을 보장하는 것은 아니며, 지원 여부·추출 실패·판독 불확실을 구분해 사람 확인으로 남깁니다.

| 단계 | 리소스 | 저장·처리 내용 |
|---|---|---|
| **1. 원본 파일 보관** | R18 SharePoint(우선) 또는 R08 Blob | 어떤 확장자(`.hwp`, `.hwpx`, `.pdf`, `.html`, `.docx`, `.pptx`, 이미지 등)든 원본 그대로 보관. 크기 제한·보관 기간·삭제 정책 적용 |
| **2. 형식별 내용·표 추출** | **① R16 Content Understanding (공식 기본 지원 형식)**<br>**② R02 서버 내 한글(`.hwp`/`.hwpx`) 전처리 파서·변환기** | · **R16 공식 기본 지원:** `.pdf`, `.html`, `.md`, `.txt`, `.rtf`, `.docx`/`.xlsx`/`.pptx`(매크로·구버전 `.doc`/`.xls`/`.ppt` 포함), `.odt`/`.ods`/`.odp`, `.csv`/`.json`/`.xml`, `.eml`/`.msg`, `.jpg`/`.png`/`.tiff` 등 (비동기 파일당 200MB 이하, PDF 300쪽 이하)<br>· **아래아한글(`.hwp`/`.hwpx`) 대응 (중요):** Microsoft R16은 한국 고유 포맷인 `.hwp`/`.hwpx`를 직접 지원하지 않으므로, **R02 컨테이너 서버에서 ① `.hwpx`(개방형 한글, ZIP+XML 구조)는 XML 본문·표 직접 파싱, ② `.hwp`(구형 바이너리)는 한글 파서(`pyhwp`/OLE 텍스트·표 추출) 또는 LibreOffice/전용 변환기로 `.pdf` 변환 후 R16에 전달**해 추출한 뒤 표·서식 누락을 검사하고, 변환 불가·판독 불확실 자료는 사람이 확인 |
| **3. 비정형 필드·검색·권한 저장** | **R07 PostgreSQL (`JSONB` + `pgvector`)** | · `documents` / `document_versions`: 원본 URI, 확장자·MIME(`file_ext`, `mime_type`), 파서 경로(`parser_type`: `content_understanding` / `hwpx_xml` / `hwp_to_pdf` / `html_dom`), 추출 상태(`parse_status`)<br>· **`extracted_fields (JSONB)`**: 문서마다 양식이 제각각인 비정형 항목(자소서 문항, 포트폴리오 링크, 경력·기술스택, 증빙 사유 등)을 고정 컬럼 없이 유연하게 구조화 저장<br>· `chunks` + `vector`: 추출된 본문·표 텍스트 조각과 임베딩 벡터 저장 → 퀴즈([F07](기능/F07_퀴즈.md))·멘토링 요약([F12](기능/F12_멘토링_사전자료.md))·이력서 검색([F13](기능/F13_이력서_인재검색.md))에서 권한(`acl_bindings`)에 맞는 조각만 검색 |

파일 자체를 PostgreSQL에 넣지 않습니다. DB가 커지고 백업·복구가 느려지기 때문입니다. 검색 결과는 항상 원본 파일 위치로 되돌아갈 수 있게 연결합니다. 원본이 바뀌거나 삭제되면 추출 텍스트·JSONB·벡터도 함께 갱신·삭제합니다(04 데이터).


## 4. 공식 제공 상태와 본 설계의 사용 방법

**이 표는 무엇을 설명하나요?** Microsoft가 공식 문서에서 밝힌 **제품의 현재 상태**(정식 출시인지, 프리뷰(미리보기)인지, 어떤 조건·제약이 있는지)와, 그 상태 때문에 **본 설계가 그 리소스를 어떻게 제한해서 쓰는지**를 나란히 보여 줍니다. 즉 "리소스가 공식적으로 해 주는 것"과 "우리 설계가 실제로 기대하는 것" 사이의 차이(괴리)를 미리 드러내고 메우는 방법을 적은 표입니다.

읽는 법:

- **정식 출시(GA):** 운영에 써도 되는 단계. 그래도 하위 기능마다 상태가 다를 수 있습니다.
- **프리뷰(미리보기):** 서비스 수준 보장(SLA)이 없고 바뀔 수 있습니다. 본 설계는 프리뷰 기능을 **꺼도 핵심 운영이 멈추지 않게** 둡니다.
- **조건·제약:** 라이선스, 리전, 요금 등급처럼 써도 되지만 지켜야 하는 조건입니다.

| 리소스 | Microsoft 공식 상태 (쉬운 말) | 차이 때문에 본 설계가 정한 사용 방법 |
|---|---|---|
| Foundry Agent Service | 정식 출시. 단, 일부 하위 기능은 프리뷰 | 핵심 업무는 정식 기능만 사용. 하위 기능은 하나씩 상태 확인 후 추가 |
| Browser Automation | 정식 출시. 단, 사설(비공개) 사이트 접속은 공개 프리뷰 | 공개 접근 LMS 화면은 정식 기능으로 운영. 사설 사이트 접속은 프리뷰이므로 배포 전 확인 후 운영에 포함하고, 실패 시 PAD 정형 실행으로 대체 |
| Computer use | 조사 당시 프리뷰 모델(`computer-use-preview`). 모델 접근·리전 조건은 변동 가능 | 실제 테스트·운영에서 모델·지원 리전을 선택·변경. 허용된 화면 작업만 선택 사용, 정형 작업은 Playwright/PAD 우선 |
| Content Understanding | 문서·이미지·음성·영상 처리 지원. API 버전·분석기·리전 조합마다 상태가 다를 수 있음 | 실제 쓰는 조합의 상태를 확인 후 사용. 개요만 보고 모든 조합을 정식 출시로 보지 않음 |
| Power Automate 무인 실행 | Process 계열 라이선스와 Windows 머신·세션 조건 필요 | 데스크톱 자동화가 필요한 경우 Windows 버전·세션 조건을 배포 전 확인 후 운영 |
| Durable Task Scheduler | 권장 저장 방식. Consumption은 데이터 30일 보존·고가용성 없음, Dedicated는 월 고정·90일 보존·고가용성 | 운영 시작은 Consumption. 보존·고가용성이 필요해지면 Dedicated |
| Azure Functions 요금제 | 기존 Consumption 요금제는 레거시. 신규 앱은 Flex Consumption 권장 | 신규 함수 앱은 Flex Consumption으로 생성. Durable Task Scheduler와의 조합은 배포 전 확인 |
| PostgreSQL Burstable | 개발용. 운영 워크로드 비권장(CPU 크레딧 소진 시 성능 급감) | 바로 정식 운영하므로 Burstable은 쓰지 않음. 처음부터 General Purpose `2 vCore`로 생성 |
| AI Search Serverless | 프리뷰(SLA 없음) | 운영 기본 구성에 넣지 않음(R17 보류). R07 `vector` 검색 우선 |

## 5. SKU·리전·모델을 선택·갱신하는 순서

리소스 이름을 정했다고 배치·비용·품질이 확정되는 것은 아닙니다. 아래는 테스트·운영에서 갱신하는 선택 절차이며 특정 리전·모델·일정의 승인 절차가 아닙니다.

1. API·DB·스토리지·모델별 제공 여부·쿼터·정책·지연·비용에 맞게 생성 리전을 선택합니다. 모든 서비스가 같은 리전이어야 한다고 가정하지 않습니다.
2. 생성 위치·저장 위치와 실제 AI 처리 위치를 구분하고 허용 조건 안에서 다른 리전·배포 유형을 사용하거나 이전합니다. Global 방식은 생성 리전 안에서만 처리된다는 뜻이 아닙니다.
3. Foundry의 모델별 쿼터는 06 실환경 확인 기록의 CLI 조회값을 기준으로 하고, 배포 SKU 및 단가 비교는 08 모델 가격 비교를 따릅니다.
4. 서비스·모델·API/분석기 조합의 제공 상태와 실제 동작을 테스트·운영에서 확인하고 변경 사유·적용 버전을 기록합니다.
5. 필요한 처리량과 보안 요구를 넣어 SKU를 선택합니다. 모델은 운영 중 품질·속도·비용을 보며 더 좋은 모델 또는 더 가성비 있는 모델로 교체합니다.

| 항목 | 등급 선택 기준 |
|---|---|
| PostgreSQL | 처음부터 General Purpose `2 vCore`(예: `D2ds_v5`, Korea Central 시간당 $0.246). 부하·고가용성 요구가 커지면 vCore 확장 또는 영역 중복 HA 추가. 개발 환경과 운영 환경 분리 |
| Service Bus | Standard부터. 사설 엔드포인트가 필수이거나 예측 가능한 처리량이 필요하면 Premium 검토 |
| Functions·Durable Task Scheduler | Functions는 Flex Consumption. Durable Task Scheduler는 Consumption부터, 처리량·보존·고가용성 필요 시 Dedicated |
| Container Apps | Consumption 기준. CPU·메모리·최소 인스턴스(1)·최대 인스턴스·동시 요청 한도 설정 |
| Windows VM | 데스크톱 자동화 필요 시 지원 Windows 버전·라이선스 확인. 운영 시간에만 가동해 비용 절감 |
| 모델 | 계획/도구 호출, 저비용 요약, 임베딩, 이미지 해석을 역할별 선정. 정확한 모델 ID·버전은 구독 확인 후 기록 |
| 네트워크 | DB는 사설 접근 우선. 외부 API·웹훅은 TLS와 인증·검증. 모든 서비스가 같은 SKU에서 사설망을 지원한다고 가정하지 않음 |

## 6. 공식 근거 목록

표의 갱신일은 이번 조회에서 확인된 페이지 메타데이터이며 서비스 출시일이 아닙니다. 날짜 미기재 항목도 공식 문서 링크입니다.

| 근거 | 페이지 갱신일 | 확인 내용 |
|---|---|---|
| [Foundry Agent Service](https://learn.microsoft.com/en-us/azure/foundry/agents/overview) | 2026-10-15 | 관리형/hosted/Responses 경로 |
| [Foundry 지역·한도](https://learn.microsoft.com/en-us/azure/foundry/agents/concepts/limits-quotas-regions) | 2026-10-15 | GA·프리뷰 구분, 지역·모델 조건 |
| [Browser Automation](https://learn.microsoft.com/en-us/azure/foundry/agents/how-to/tools/browser-automation) | 2026-10-15 | GA, Playwright, 사람 개입 |
| [Computer use](https://learn.microsoft.com/en-us/azure/foundry/agents/how-to/tools/computer-use) | 2026-09-25 | preview 모델, 동작 루프, 실행 환경 |
| [Durable Functions](https://learn.microsoft.com/en-us/azure/durable-task/durable-functions/durable-functions-overview) | 2026-06-02 | 상태·재시도·권장 저장소 |
| [Durable Task Scheduler](https://learn.microsoft.com/en-us/azure/durable-task/scheduler/durable-task-scheduler) | 2026-10-15 | 권장 공급자·과금 SKU·지역 확인 |
| [Durable Task Scheduler 과금](https://learn.microsoft.com/en-us/azure/durable-task/scheduler/durable-task-scheduler-billing) | 2026-10-13 | Consumption/Dedicated 처리량·보존·고가용성 비교 |
| [Functions 호스팅 요금제](https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale) | 2026-09-18 | 기존 Consumption 레거시, 신규는 Flex Consumption |
| [Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/overview) | 2026-07-07 | 웹/API·작업·확장 |
| [Container Apps 과금](https://learn.microsoft.com/en-us/azure/container-apps/billing) | 2026-03-25 | 초 단위 과금, 구독당 월 무료량 |
| [Container Registry 등급](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-skus) | 2026-10-16 | Basic은 개발·소량용 저가 등급 |
| [Service Bus](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) | 2026-08-31 | 대기열·분리·부하 조절 |
| [Service Bus Premium vs Standard](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-premium-messaging) | 2026-10-13 | 종량제/고정 요금, 지연·메시지 크기 차이 |
| [PostgreSQL vector](https://learn.microsoft.com/en-us/azure/postgresql/extensions/how-to-use-pgvector) | 2026-07-13 | 확장 허용 후 `CREATE EXTENSION vector` |
| [PostgreSQL 컴퓨팅 등급](https://learn.microsoft.com/en-us/azure/postgresql/compute-storage/concepts-compute) | 2026-07-09 | Burstable 운영 비권장, General Purpose 운영용 |
| [Azure Retail Prices API](https://prices.azure.com/api/retail/prices) (PostgreSQL, `koreacentral`) | 2026-10 조회 | General Purpose Ddsv5 2 vCore 시간당 $0.246, 스토리지 GB·월 $0.131 |
| [Blob 보관 정책](https://learn.microsoft.com/en-us/azure/storage/blobs/lifecycle-management-overview) | 2026-08-25 | 등급 이동·기한 삭제 |
| [Azure Monitor 로그 비용](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/cost-logs) | 2026-09-21 | 로그 수집량 기준 과금 |
| [AI Search 요금 모델](https://learn.microsoft.com/en-us/azure/search/search-sku-tier) | 2026-09-17 | Dedicated 고정 용량, Serverless 프리뷰 |
| [Content Understanding](https://learn.microsoft.com/en-us/azure/ai-services/content-understanding/overview) | 2026-09-24 | 복합 자료→사용자 정의 필드 |
| [Content Understanding 서비스 한도](https://learn.microsoft.com/en-us/azure/ai-services/content-understanding/service-limits) | 2026-10-19 | 공식 지원 형식 `.pdf`·`.html`·`.md`·`.txt`·`.rtf`·`.docx`/`.xlsx`/`.pptx`·구버전 `.doc`/`.xls`/`.ppt`·`.odt`·이미지(비동기 200MB·PDF 300쪽 이하, HTML/TXT는 3,000자=1쪽 과금). 한국 고유 `.hwp`/`.hwpx`는 목록에 없으므로 서버 전처리(XML 파싱/PDF 변환) 후 연동 |
| [Power Automate 무인 실행](https://learn.microsoft.com/en-us/power-automate/desktop-flows/run-unattended-desktop-flows) | — | 라이선스·Windows 세션 |
| [Azure 예산](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets) | — | 예산 알림은 자동 중단이 아님 |

## 7. 실제 포털 확인 기록

**실환경 확인값·상세 스펙·확인 시점은 06 실환경 확인 기록을 기준으로 합니다.** 정책 할당 목록 조회는 완료되었지만 실제 배포 제약·연결 성공은 별도 확인입니다. 남은 연결 작업은 07 체크리스트에서 관리합니다.
