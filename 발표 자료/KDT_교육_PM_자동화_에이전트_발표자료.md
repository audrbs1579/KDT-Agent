---
marp: true
theme: default
size: 16:9
paginate: true
header: "대표님·결정권자 검토"
footer: "KDT 교육 PM 자동화 에이전트 · 2026.10.28"
style: |
  section {
    font-family: 'Malgun Gothic', '맑은 고딕', 'Noto Sans KR', sans-serif;
    color: #14263d;
    background: #f8fafc;
    padding: 68px 64px 48px;
    font-size: 24px;
    line-height: 1.45;
    display: flex;
    flex-direction: column;
  }
  header { position: absolute; top: 23px; right: 64px; left: 64px; text-align: right; font-size: 15px; color: #526476; }
  footer { font-size: 14px; color: #526476; }
  h1, h2, h3, p, small, table { flex-shrink: 0; }
  h1 { color: #083b66; font-size: 52px; letter-spacing: -1.5px; margin: 0 0 24px; }
  h2 { color: #083b66; font-size: 36px; letter-spacing: -1px; margin: 0 0 18px; }
  h3 { color: #007b90; font-size: 27px; margin: 14px 0 10px; }
  p { margin: 10px 0; }
  strong { color: #005d86; }
  small, .note { color: #526476; font-size: 17px; }
  table { width: 100%; font-size: 23px; margin: 16px 0; }
  th { background: #e7f1f7; color: #083b66; }
  th, td { border-color: #cad8e3; padding: 12px 14px; }
  section.lead { justify-content: center; background: #083b66; color: #f8fbff; }
  section.lead h1, section.lead h2, section.lead strong { color: white; }
  section.lead p, section.lead small, section.lead header, section.lead footer { color: #c7e7ef; }
  .rule { border-top: 3px solid #18a0ae; margin: 16px 0 24px; }
  .message { color: #3156d9; font-size: 25px; font-weight: 700; }
  .decision { color: #007b90; font-size: 23px; font-weight: 700; border-top: 2px solid #b5d9de; padding-top: 14px; }
  .columns { display: grid; grid-template-columns: 1fr 1fr; gap: 40px; }
  .columns table { font-size: 21px; }
  .columns p { font-size: 22px; }
  .visual { display: block; width: 100%; height: 0; min-height: 0; flex: 1 1 0; max-height: 350px; margin: 12px auto; object-fit: contain; }
  section.agenda { justify-content: center; }
  section.agenda h2 { font-size: 40px; }
  section.agenda ol { list-style: none; padding: 0; margin: 14px 0; font-size: 25px; line-height: 1.7; color: #788696; }
  section.agenda li.current { color: #083b66; font-weight: 700; }
  section.agenda li.current::after { content: '  ◀ 현재 파트'; color: #007b90; font-size: 16px; }
  section::after { color: #6d8295; font-size: 14px; }
  section.lead::after { color: #c7e7ef; }
---

<!-- _class: lead -->

# KDT 교육 PM 자동화 에이전트

## 첫 검증 제안: 과정 종료 설문 운영과 결과 확인

일정·운영 규칙에 따라 반복 업무를 처리하고,<br>담당자는 결과와 예외를 확인하는 운영을 목표로 합니다.

<div class="rule"></div>

오늘 논의: **시험 대상 · 연결 책임 · 자료와 운영 기준**

<small>본편 15장(표지·목차 포함) · 업무·기술 상세는 별도 부록</small>

<!-- 발표자 노트: 오늘은 첫 검증을 시작할 조건을 정하는 자리입니다. 현 운영 배포 완료나 확정 비용을 발표하는 자리가 아닙니다. 근거: ../설계보고서/05_구현_검증_계획.md 및 정리 자료/00. 전체 발표 전략 및 장표 구성.md -->

---

<!-- _class: agenda -->
<!-- header: "01 / 06 · 운영 문제와 변화" -->

## 운영 문제와 변화

<p class="message">제안은 반복 확인·연락·집계의 수작업을 줄이는 것입니다.</p>

<ol>
  <li class="current">01. 운영 문제와 변화</li>
  <li>02. 첫 검증 범위</li>
  <li>03. 결과 확인과 사람의 역할</li>
  <li>04. 현재 준비 상태</li>
  <li>05. 실행 계획과 비용</li>
  <li>06. 이번 회의 결정</li>
</ol>

<p class="decision">먼저 확인할 질문: 담당자의 어떤 일이 줄어드는가</p>

---

## 담당자가 직접 처리하던 반복 업무를 연결합니다

<p class="message">반복 처리는 에이전트가 이어가고, 담당자는 결과와 예외를 확인합니다.</p>

| 업무 | 직접 처리하는 작업 | 자동화 후 개발 목표 |
|---|---|---|
| 대상 확인 | 종료 과정·기수·일정을 확인 | 등록 일정과 종료 조건으로 대상 선별 |
| 설문 준비·안내 | 양식과 과정 정보를 맞추고 발송 | 표준 양식 준비와 해당 과정 기본 안내 1회 |
| 응답·결과 정리 | 응답 수집, 점수 계산, 의견 정리 | 수집·집계·요약과 내부 결과 보관 |
| 진행 확인 | 자료와 메시지 이력을 다시 탐색 | 완료 근거·실패·사람 작업 대기를 한 화면에서 확인 |

<p class="note">업무 변화 예시입니다. 실제 대상의 현행 절차·소요 시간은 검증 전에 확인합니다.</p>

<!-- 근거: 정리 자료/01. 개발 이유와 목표.md; ../설계보고서/기능/F06_만족도조사.md; ../설계보고서/기능/F21_대시보드.md. 절감 실적을 뜻하지 않습니다. -->

---

<!-- _class: agenda -->
<!-- header: "02 / 06 · 첫 검증 범위" -->

## 첫 검증 범위

<p class="message">첫 검증은 일정 입력부터 종료 설문·결과 화면까지 연결합니다.</p>

<ol>
  <li>01. 운영 문제와 변화</li>
  <li class="current">02. 첫 검증 범위</li>
  <li>03. 결과 확인과 사람의 역할</li>
  <li>04. 현재 준비 상태</li>
  <li>05. 실행 계획과 비용</li>
  <li>06. 이번 회의 결정</li>
</ol>

<p class="decision">검증 범위: 표준 종료 설문 한 흐름을 끝까지 실행</p>

---

## 첫 검증 범위는 종료 설문과 결과 확인입니다

<p class="message">일정·과정 정보 입력 → 설문 준비·안내·수집 → 집계·보관·결과 확인</p>

<img class="visual" src="시각 자료/21_입력부터결과까지_첫구현검증_흐름도.svg" alt="입력, 고정 Forms 시험 수집, 과정별 종료 안내, 결과 확인의 첫 검증 흐름">

**설문 기준:** 전체 과정 종료 시 1회, 5점 선택형 2개·주관식 1개

<p class="note">Teams·Outlook 수업 일정 발행, LMS 대조, 퀴즈는 이후 연결 범위입니다. 먼저 고정 양식 응답 수집을 확인합니다.</p>

<!-- 근거: 정리 자료/05. 개발 순서와 비용.md 21장; ../설계보고서/05_구현_검증_계획.md 2절; ../설계보고서/기능/F06_만족도조사.md. 일정 입력은 첫 검증에 포함하되 실제 월별 채널 수업 발행은 후속 확장입니다. -->

---

## 종료한 과정에만 보내고 결과까지 확인합니다

<p class="message">같은 시험에서 종료한 A과정과 운영 중 B과정을 함께 확인합니다.</p>

| 시험 상황 | 기대하는 실행 결과 |
|---|---|
| A과정 전체 종료 확인 | A과정 기본 안내 1회 |
| B과정 운영 중 | 만족도 안내 대기 |
| 동일 요청 재시도·종료일 변경 | 기존 결과를 대조하고 중복 안내 차단 |
| A과정 응답 수집 | A과정 결과로 집계·저장, B과정과 분리 |
| 수집·인증 장애 | 실패·확인 대기 표시와 복구 이력 |

<p class="note">합성 시험 자료로 종료 조건을 구성합니다. 실제 운영 과정에는 검증된 조건과 권한을 적용합니다.</p>

<!-- 근거: ../설계보고서/기능/F06_만족도조사.md; 정리 자료/05. 개발 순서와 비용.md 21~22장. 표는 검증 계획이며 성공 기록이 아닙니다. -->

---

<!-- _class: agenda -->
<!-- header: "03 / 06 · 결과 확인과 사람의 역할" -->

## 결과 확인과 사람의 역할

<p class="message">담당자는 처리 결과의 근거를 보고 필요한 판단을 맡습니다.</p>

<ol>
  <li>01. 운영 문제와 변화</li>
  <li>02. 첫 검증 범위</li>
  <li class="current">03. 결과 확인과 사람의 역할</li>
  <li>04. 현재 준비 상태</li>
  <li>05. 실행 계획과 비용</li>
  <li>06. 이번 회의 결정</li>
</ol>

<p class="decision">확인 방식: 완료·실패·사람 작업 대기를 구분</p>

---

## 담당자는 결과와 예외를 확인합니다

<p class="message">양식 준비·안내·수집·집계를 자동화하고, 기준 승인과 예외 처리를 담당자에게 연결합니다.</p>

<img class="visual" src="시각 자료/13_업무예약부터완료까지_상태와대기분기.svg" alt="예약부터 응답과 자료 확인, 완료 검증 및 사람 작업 대기까지의 상태 구분">

**화면에서 확인:** 처리 대상, 원문·결과 링크, 실행 상태, 다음 담당 업무

<p class="note">확대 단계에서도 공식 출결 인정·정정은 사람이 판단합니다. 퀴즈 검수·게시 등 현재 사람 작업은 부록 A15에 정리했습니다.</p>

<!-- 근거: ../설계보고서/04_데이터_권한_복구.md; 정리 자료/03. 자동화 결과와 사람의 역할.md 13~15장. 그림은 상태 설계안입니다. -->

---

<!-- _class: agenda -->
<!-- header: "04 / 06 · 현재 준비 상태" -->

## 현재 준비 상태

<p class="message">계정과 자료 구조의 확인 기록이 있으며, 실제 업무 연결은 검증이 필요합니다.</p>

<ol>
  <li>01. 운영 문제와 변화</li>
  <li>02. 첫 검증 범위</li>
  <li>03. 결과 확인과 사람의 역할</li>
  <li class="current">04. 현재 준비 상태</li>
  <li>05. 실행 계획과 비용</li>
  <li>06. 이번 회의 결정</li>
</ol>

<p class="decision">착수 조건: 대상 채널·자료·Forms 연결·인증 복구 책임 확인</p>

---

## 계정 기반은 확인했고 실제 업무 연결을 검증해야 합니다

| 항목 | 현재 자료에서 확인한 상태 | 첫 검증에서 확인할 것 |
|---|---|---|
| 운영·직원·교육 계정 | 세 조직의 관리자 역할 조회 기록 | 자동화 대상과 필요한 접근 범위 |
| 교육 자료 | 일부 SharePoint 폴더와 제공 구조 예시 | 지정 파일·채널·실제 읽기/저장 |
| 종료 설문 | 문항·운영 기준과 구현 경로 정리 | Forms 준비·인증·응답 수집 |
| 반복 실행 | 실행·기록·복구 설계안 | 종료 조건·중복 차단·장애 복구 |

<p class="decision">첫 결과물은 우리 환경에서 한 흐름을 반복 실행한 검증 기록입니다.</p>

<p class="note">계정 확인: 2026.10.18–19 · 자료 구조 보완: 10.21 · Forms 방침 보완: 10.28. 설계보고서 기록 기준입니다.</p>

<!-- 근거: ../설계보고서/06_실환경_확인기록.md 2~4절, 9~10절; ../설계보고서/07_세계정_연결권한_체크리스트.md. 이번 발표 수정에서 새 계정 접속·배포·연동 검증을 수행하지 않았습니다. -->

---

<!-- _class: agenda -->
<!-- header: "05 / 06 · 실행 계획과 비용" -->

## 실행 계획과 비용

<p class="message">첫 흐름의 결과를 확인한 뒤 확대 여부를 정합니다.</p>

<ol>
  <li>01. 운영 문제와 변화</li>
  <li>02. 첫 검증 범위</li>
  <li>03. 결과 확인과 사람의 역할</li>
  <li>04. 현재 준비 상태</li>
  <li class="current">05. 실행 계획과 비용</li>
  <li>06. 이번 회의 결정</li>
</ol>

<p class="decision">실행 조건: 담당 가용 시간·연결 가능 여부·시범 비용 확인</p>

---

## 담당·참고 기간과 시범 비용을 확인합니다

<div class="columns">
<div>

### 개발 담당과 참고 기간

**박명균** — 설계·개발·연결·배포·테스트

| 작업 | 기존 설계 참고 기간 |
|---|---|
| 공통 연결 | 1–2주 |
| 첫 운영 흐름 | 2–3주 |

<p class="note">가용 시간과 실제 연동 결과에 따라 조정합니다. 단계는 중첩·반복할 수 있습니다.</p>

</div>
<div>

### 시범 비용 산정 조건

**시범 총비용: 산정 필요**

- 개발·유지보수 인건비
- Azure 기반과 보관 비용
- Forms 연결·실행 및 AI 사용량

<p>종료 과정 수·응답 수·보관 기간·라이선스를 정한 뒤 산정합니다.</p>

</div>
</div>

<p class="note">기존 월비용 소계는 새 Forms 실행량과 인건비 등을 제외합니다. 가정별 계산은 부록 A29, 단계별 기간은 A30에서 확인합니다.</p>

<!-- 근거: ../설계보고서/05_구현_검증_계획.md 2.3~4절; ../설계보고서/10_비용_산출_시뮬레이션.md 5~6절. 참고 기간을 단순 합산한 납기나 기존 소계를 총예산으로 제시하지 않습니다. -->

---

## 검증 결과를 보고 다음 업무로 확대합니다

| 확대 판단 기준 | 확인할 결과 |
|---|---|
| 대상·종료 조건 | 종료한 과정에만 기본 안내 1회 |
| 원본 일치 | 과정별 응답과 집계·보관 결과 일치 |
| 반복 실행 | 재시도 시 중복 처리 차단 |
| 장애 대응 | 수집·인증 실패를 표시하고 복구 기록 확보 |
| 운영 효과 | 사람 개입 횟수·시간, 오류, 실제 비용 기록 |

<p class="decision">기준 미충족 시 해당 연결을 보완하고 재검증합니다.</p>

**후속 확대:** 강사·수업 일정 연계 → LMS·출결·학습 지원

<p class="note">검증 전 현행 업무 시간을 기록하고, 검증 후 같은 업무 범위로 비교합니다. 목표 절감률은 측정 결과를 바탕으로 정합니다.</p>

<!-- 근거: ../설계보고서/05_구현_검증_계획.md 2~3절; 정리 자료/05. 개발 순서와 비용.md 22~25장. 현행 비교 기록과 확대 판단 방식은 이번 대표님용 검토를 위한 제안입니다. -->

---

<!-- _class: agenda -->
<!-- header: "06 / 06 · 이번 회의 결정" -->

## 이번 회의 결정

<p class="message">시험 대상과 실행 책임을 정하면 첫 검증을 구체화할 수 있습니다.</p>

<ol>
  <li>01. 운영 문제와 변화</li>
  <li>02. 첫 검증 범위</li>
  <li>03. 결과 확인과 사람의 역할</li>
  <li>04. 현재 준비 상태</li>
  <li>05. 실행 계획과 비용</li>
  <li class="current">06. 이번 회의 결정</li>
</ol>

<p class="decision">오늘 정할 것: 시험 대상 · 연결 담당 · 자료와 운영 기준</p>

---

## 이번 회의에서 정할 세 가지

| 결정 항목 | 구체적으로 정할 내용 |
|---|---|
| 시험 대상 | 테스트용 과정과 실제 적용 후보 기수 |
| 연결 책임 | Teams·SharePoint·Forms 설정과 인증 복구를 확인할 담당자 |
| 자료·운영 기준 | 허용 일정·명단·양식, 종료 확인, 익명·응답 기한·재안내 기준 |

<p class="decision">다음 공유 결과물: 연결 확인 결과, 시범 비용 산정, 실행·오류·사람 개입 기록</p>

**판단할 변화:** 담당자가 반복 처리에 쓰는 시간을 줄이고, 결과와 예외에 집중할 수 있는가

<p class="note">설문은 과정 종료 1회·선택형 2개·주관식 1개 기준을 적용합니다. 준비가 끝나면 착수 범위와 시범 비용 상한을 확인합니다.</p>

<!-- 근거: 정리 자료/06. 다음 단계와 마무리.md 27장; ../설계보고서/05_구현_검증_계획.md 6절; ../설계보고서/07_세계정_연결권한_체크리스트.md. 이번 회의 요청은 실행 준비를 구체화하는 제안입니다. -->
