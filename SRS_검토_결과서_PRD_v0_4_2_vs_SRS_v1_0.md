# SRS 검토 결과서  
## PRD v0.4.2 대비 SRS v1.0 요구사항 충족성 검토

| 항목 | 내용 |
| :--- | :--- |
| 검토 대상 PRD | `PRD_v0_4_2.md` — 5060 프리미엄 브랜드 매니지먼트 PRD v0.4.2 |
| 검토 대상 SRS | `SRS_v0_1.md` — Software Requirements Specification, Revision 1.0 |
| 검토일 | 2026-04-26 |
| 검토 기준 | Story·AC 반영성, KPI/NFR 반영성, API/Interface 반영성, Entity/Schema 완성도, Traceability Matrix, 핵심 Mermaid Diagram, Sequence Diagram, ISO/IEC/IEEE 29148 구조 적합성 |
| 판정 체계 | ✅ 충족 / 🟡 부분 충족 / ❌ 미충족 / ⚠️ 검증 불가 |

---

## 1. 종합 결론

**최종 판정: 🟡 부분 충족**

현재 SRS는 PRD의 핵심 기능 흐름, 주요 사용자 스토리, KPI, 비기능 요구사항, API 목록, Traceability Matrix의 기본 구조를 상당 부분 반영하고 있다.  
다만 다음 3가지 영역은 릴리즈 전 보완이 필요하다.

1. **PRD의 일부 AC가 REQ-FUNC로 누락 또는 불완전 반영됨**
   - `AC-Suf-3`
   - `AC-Pat-5~8`
   - `AC-One-4`
   - `AC-Out-2`
   - `AC-Out-5`
   - `AC-Logic-2`의 EXTRACT 문항 수 불일치: PRD 17문항 vs SRS 15문항

2. **핵심 다이어그램 요건 미충족**
   - Sequence Diagram은 6개 포함되어 충분하나, 요청 기준인 3~5개를 초과한다.
   - UseCase Diagram, ERD, Class Diagram, Component Diagram이 SRS에 Mermaid 형태로 작성되어 있지 않다.

3. **Appendix의 엔터티·스키마가 MVP 중심으로는 정리되어 있으나 완성본으로 보기에는 부족함**
   - `ANSWER_OUTPUT.answer_id`가 `ANSWER`를 FK로 참조하지만 `ANSWER` 엔터티가 SRS Appendix에 정의되어 있지 않다.
   - PRD의 V2 정규화 후보 엔터티인 `QUESTION`, `QUESTION_PART`, `BRANDING_ELEMENT`, `ANSWER`, `ANSWER_PATTERN`, `COACHING_FEEDBACK`, `OUTPUT_MAPPING`, `REPORT_SECTION`이 SRS Appendix에 정의되어 있지 않다.
   - ERD Mermaid가 SRS Appendix에 포함되어 있지 않다.

---

## 2. 요건별 충족 여부 요약

| # | 검토 요건 | 판정 | 핵심 판단 |
| :---: | :--- | :---: | :--- |
| 1 | PRD의 모든 Story·AC가 SRS의 REQ-FUNC에 반영됨 | 🟡 부분 충족 | US-1~US-7은 Traceability Matrix에 반영됨. 그러나 일부 AC가 REQ-FUNC에 누락 또는 부분 반영됨. |
| 2 | 모든 KPI·성능 목표가 REQ-NF에 반영됨 | ✅ 충족 | 북극성 KPI, 보조 KPI, 성능·가용성·에러율·동시성 목표가 REQ-NF로 구조화됨. |
| 3 | API 목록이 인터페이스 섹션에 모두 반영됨 | 🟡 부분 충족 | SRS 3.3과 Appendix 6.1에 API 목록이 정리됨. 단, PRD의 §10-4 API 표가 실제로는 비어 있어 PRD 원천 대비 완전성 검증은 제한됨. |
| 4 | 엔터티·스키마가 Appendix에 완성됨 | 🟡 부분 충족 | 핵심 MVP 엔터티와 42개 OUTPUT 변수는 정리됨. 그러나 일부 참조 엔터티와 V2 후보 엔터티가 누락됨. |
| 5 | Traceability Matrix가 누락 없이 생성됨 | 🟡 부분 충족 | Story/Feature 중심의 Matrix는 있음. 그러나 AC 단위 전체 추적성은 부족하고 누락 AC가 있음. |
| 6 | UseCase, ERD, Class Diagram, Component Diagram 등 핵심 다이어그램이 모두 작성됨 | ❌ 미충족 | SRS에는 Sequence Diagram만 있고, 나머지 핵심 다이어그램이 없음. |
| 7 | Sequence Diagram 3~5개가 포함됨 | 🟡 부분 충족 | Sequence Diagram은 6개 포함됨. 수량은 충분하나 요구 범위인 3~5개를 초과함. |
| 8 | SRS 전체가 ISO 29148 구조를 준수함 | ✅ 충족에 가까운 부분 충족 | Introduction, Scope, Interfaces, Requirements, NFR, Traceability, Appendix 구조는 갖춤. 다만 검증 방법·상태 모델·요구사항 품질 기준 보강 여지 있음. |

---

## 3. 상세 검토 결과

## 3.1 PRD Story·AC → SRS REQ-FUNC 반영성

### 3.1.1 사용자 스토리 반영 여부

| PRD Story | SRS 반영 REQ | 판정 | 비고 |
| :--- | :--- | :---: | :--- |
| US-1. 질문별 브랜드 자산 매핑 안내 | `REQ-FUNC-011` | ✅ | 진단 폼 질문 하단 안내 문구 요구사항으로 반영됨. |
| US-2. Stage 1 답변 기반 코치 분석 노트 자동 생성 | `REQ-FUNC-070`, `REQ-FUNC-020` | ✅ | 코치 분석 노트 생성 및 관리자 콘솔 표시 요구사항으로 반영됨. |
| US-3. 5060 특화 신호 감지 및 스크립트 사용 | `REQ-FUNC-051~054`, `REQ-FUNC-072` | 🟡 | 핵심 4개 패턴은 반영됨. 단, PRD의 신규 AC-Pat-5~8은 누락됨. |
| US-4. Stage 1→3 변화점 시각화 | `REQ-FUNC-090` | ✅ | Q1↔Q41 변화 리포트로 반영됨. |
| US-5. 원라이너 초안 3종 자동 생성 | `REQ-FUNC-073`, `REQ-FUNC-074`, `REQ-FUNC-075` | 🟡 | 3종 생성·인용·압축 옵션은 반영됨. 원라이너 일관성 실패 처리인 `AC-One-4`는 누락됨. |
| US-6. 마스터 브리프 원천 추적 | `REQ-FUNC-003` | ✅ | 섹션별 원천 답변 추적 정보 요구사항으로 반영됨. |
| US-7. 답변 간 일관성 충돌 자동 감지 | `REQ-FUNC-091~093` | ✅ | 가치·정체성·WHY 일관성 검증 요구사항으로 반영됨. |

### 3.1.2 AC 반영 현황

| 구분 | PRD AC | SRS 반영 상태 | 판정 |
| :--- | :--- | :--- | :---: |
| 답변 충분성 | `AC-Suf-1` | `REQ-FUNC-080` | ✅ |
| 답변 충분성 | `AC-Suf-2` | `REQ-FUNC-081` | ✅ |
| 답변 충분성 | `AC-Suf-3` | 직접 대응 REQ 없음 | ❌ |
| 패턴 분석 | `AC-Pat-1` | `REQ-FUNC-051` | ✅ |
| 패턴 분석 | `AC-Pat-2` | `REQ-FUNC-052` | ✅ |
| 패턴 분석 | `AC-Pat-3` | `REQ-FUNC-053` | ✅ |
| 패턴 분석 | `AC-Pat-4` | `REQ-FUNC-054` | ✅ |
| 패턴 분석 | `AC-Pat-5` | 직접 대응 REQ 없음 | ❌ |
| 패턴 분석 | `AC-Pat-6` | 직접 대응 REQ 없음 | ❌ |
| 패턴 분석 | `AC-Pat-7` | 직접 대응 REQ 없음 | ❌ |
| 패턴 분석 | `AC-Pat-8` | 직접 대응 REQ 없음 | ❌ |
| 브랜드 자산 매핑 | `AC-Map-1` | `REQ-FUNC-060` | ✅ |
| 브랜드 자산 매핑 | `AC-Map-2` | `REQ-FUNC-061` | ✅ |
| 브랜드 자산 매핑 | `AC-Map-3` | `REQ-FUNC-090`에 의미상 반영 | 🟡 |
| 브랜드 자산 매핑 | `AC-Map-4` | `REQ-FUNC-062` | ✅ |
| 코치 세션 준비 | `AC-Sess-1` | `REQ-FUNC-070` | ✅ |
| 코치 세션 준비 | `AC-Sess-2` | `REQ-FUNC-020` | ✅ |
| 코치 세션 준비 | `AC-Sess-3` | `REQ-FUNC-071` | ✅ |
| 코치 세션 준비 | `AC-Sess-4` | `REQ-FUNC-072` | ✅ |
| 원라이너 | `AC-One-1` | `REQ-FUNC-073` | ✅ |
| 원라이너 | `AC-One-2` | `REQ-FUNC-074` | ✅ |
| 원라이너 | `AC-One-3` | `REQ-FUNC-075` | ✅ |
| 원라이너 | `AC-One-4` | 직접 대응 REQ 없음 | ❌ |
| 교차 분석 | `AC-Cross-1` | `REQ-FUNC-090` | ✅ |
| 교차 분석 | `AC-Cross-2` | `REQ-FUNC-091` | ✅ |
| 교차 분석 | `AC-Cross-3` | `REQ-FUNC-092` | ✅ |
| 교차 분석 | `AC-Cross-4` | `REQ-FUNC-093` | ✅ |
| 최종 출력 | `AC-Out-1` | `REQ-FUNC-002` | ✅ |
| 최종 출력 | `AC-Out-2` | 직접 대응 REQ 없음 | ❌ |
| 최종 출력 | `AC-Out-3` | `REQ-FUNC-004`, `REQ-NF-033` | ✅ |
| 최종 출력 | `AC-Out-4` | `REQ-FUNC-003` | ✅ |
| 최종 출력 | `AC-Out-5` | `REQ-FUNC-005`에 일부 반영 | 🟡 |
| 최종 출력 | `AC-Out-6` | `REQ-FUNC-031` | ✅ |
| Negative AC | `AC-Neg-1` | `REQ-FUNC-110` | ✅ |
| Negative AC | `AC-Neg-2` | `REQ-FUNC-021`, `REQ-NF-036` | ✅ |
| Negative AC | `AC-Neg-3` | `REQ-FUNC-013` | ✅ |
| Negative AC | `AC-Neg-4` | `REQ-FUNC-076` | ✅ |
| Negative AC | `AC-Neg-5` | `REQ-FUNC-111` | ✅ |
| Negative AC | `AC-Neg-6` | `REQ-FUNC-005` | ✅ |
| Negative AC | `AC-Neg-7` | `REQ-FUNC-082` | ✅ |
| AI Logic | `AC-Logic-1` | `REQ-FUNC-100` | ✅ |
| AI Logic | `AC-Logic-2` | `REQ-FUNC-101` | 🟡 |
| AI Logic | `AC-Logic-3` | `REQ-FUNC-055` | ✅ |
| AI Logic | `AC-Logic-4` | `REQ-FUNC-102` | ✅ |
| AI Logic | `AC-Logic-5` | `REQ-FUNC-001`, `REQ-NF-005` | ✅ |
| AI Logic | `AC-Logic-6` | `REQ-FUNC-056` | ✅ |
| AI Logic | `AC-Logic-7` | `REQ-FUNC-077` | ✅ |

### 3.1.3 누락 또는 불완전 반영 AC

| 우선순위 | PRD AC | 문제 | 보완 필요 REQ |
| :---: | :--- | :--- | :--- |
| Must | `AC-Suf-3` | 핵심 키워드 0개 추출 시 보완 질문 1~2개 자동 생성 요구가 SRS에 없음 | `REQ-FUNC-083` 신설 |
| Must | `AC-Pat-5` | Q4 전문성 마스터리 과소평가 패턴 누락 | `REQ-FUNC-057` 신설 |
| Must | `AC-Pat-6` | Q35 차별점 인식 부족 패턴 누락 | `REQ-FUNC-058` 신설 |
| Should/Must | `AC-Pat-7` | Q24 제2챕터 미설계 패턴 누락 | `REQ-FUNC-059` 신설 |
| Must | `AC-Pat-8` | Q38 방법론형 메시지 패턴 누락 | `REQ-FUNC-063` 신설 |
| Should | `AC-One-4` | 원라이너 3종 모두 일관성 점수 < 0.5일 때 경고·보완 질문 생성 누락 | `REQ-FUNC-078` 신설 |
| Must | `AC-Out-2` | 고객 동의율 “내 핵심을 정확히 짚었다” ≥ 85% 요구 누락 | `REQ-FUNC-006` 또는 `REQ-NF-046` 신설 |
| Must | `AC-Out-5` | 가치 일관성 점수 < 0.5 또는 사람 코치 권장 플래그 ≥ 3건일 때 핸드오프 안내 + 추가 코칭 CTA 조건이 일부만 반영됨 | `REQ-FUNC-006` 또는 `REQ-FUNC-112` 신설 |
| Must | `AC-Logic-2` | PRD는 EXTRACT 대상 17문항, SRS는 15문항으로 기재 | `REQ-FUNC-101` 수정 |

---

## 3.2 KPI·성능 목표 → REQ-NF 반영성

### 판정: ✅ 충족

SRS는 PRD의 KPI와 성능 목표를 REQ-NF로 잘 구조화하고 있다.

| PRD KPI / 성능 목표 | SRS 반영 REQ-NF | 판정 |
| :--- | :--- | :---: |
| 고객 1인당 B2B 수주 ≥ 2건/분기 | `REQ-NF-040` | ✅ |
| 마스터 브리프 초안 생성 ≤ 30분 | `REQ-NF-006` | ✅ |
| Option B 전환율 ≥ 10% | `REQ-NF-041` | ✅ |
| NPS ≥ 70 | `REQ-NF-042` | ✅ |
| 리테이너 전환율 ≥ 30% | `REQ-NF-043` | ✅ |
| AI 진단 리포트 완독 → CTA 클릭율 ≥ 10% | `REQ-NF-044` | ✅ |
| 월간 신규 진단 리드 수 ≥ 50명 | `REQ-NF-045` | ✅ |
| 일반 API P95 < 200ms | `REQ-NF-001` | ✅ |
| LLM 추론 API P95 < 25초 | `REQ-NF-002` | ✅ |
| 진단 폼 동시 100명 처리 | `REQ-NF-003` | ✅ |
| 결과 리포트 동시 500명 조회 P95 500ms 이하 | `REQ-NF-004` | ✅ |
| Uptime 99.9% | `REQ-NF-010` | ✅ |
| 전체 API 에러율 < 1% | `REQ-NF-011` | ✅ |
| 환각률 < 5% | `REQ-NF-036` | ✅ |
| 패턴 분류 정확도 ≥ 85% | `REQ-NF-030` | ✅ |
| 브랜드 요소 매핑 정확도 ≥ 90% | `REQ-NF-031` | ✅ |
| 코치 세션 준비 시간 60분 → 15분 | `REQ-NF-039` | ✅ |

### 보완 의견

KPI 반영 자체는 충분하다.  
다만 KPI의 성격이 비즈니스 성과 지표와 시스템 품질 지표로 혼재되어 있으므로, SRS에서는 아래처럼 구분하면 더 명확하다.

| 분류 | 예시 |
| :--- | :--- |
| Business Outcome KPI | B2B 수주 건수, Option B 전환율, 리테이너 전환율, 신규 리드 수 |
| Product Funnel KPI | 진단 완료율, CTA 클릭률, 리포트 완독률 |
| AI Quality KPI | 패턴 분류 정확도, 환각률, 매핑 정확도, 일반론 비율 |
| System Quality KPI | Latency, Availability, Error Rate, Concurrency |

---

## 3.3 API 목록 및 인터페이스 반영성

### 판정: 🟡 부분 충족

SRS에는 다음 2곳에 API가 정리되어 있다.

1. `3.3 API Overview`
2. `6.1 API Endpoint List`

### SRS에 포함된 API 목록

| Method | Endpoint | 관련 기능 |
| :---: | :--- | :--- |
| POST | `/api/leads` | 리드 생성 |
| POST | `/api/diagnosis/submit` | 진단 제출 |
| GET | `/api/reports/{diagnosis_id}` | 진단 리포트 조회 |
| POST | `/api/ai/classify-patterns` | 답변 패턴 분류 |
| POST | `/api/ai/map-branding` | 브랜딩 요소 매핑 |
| POST | `/api/ai/coach-brief` | 코치 분석 노트 생성 |
| POST | `/api/ai/master-brief` | 마스터 브리프 생성 |
| PATCH | `/api/briefs/{id}/review` | 브리프 검수 |
| GET | `/api/briefs/{id}` | 브리프 조회 |
| GET | `/api/clients/{id}/dashboard` | 고객 대시보드 |
| GET | `/api/admin/projects` | 관리자 프로젝트 목록 |

### 확인 결과

| 항목 | 판정 | 설명 |
| :--- | :---: | :--- |
| SRS 인터페이스 섹션에 API Overview 존재 | ✅ | 3.3에 API Overview가 존재함. |
| Appendix에 API Endpoint List 존재 | ✅ | 6.1에 Method, Endpoint, 설명, 주체, 관련 REQ-ID가 정리됨. |
| PRD API 목록과 1:1 대조 가능성 | ⚠️ 검증 불가 | PRD §10-4는 “기존 v0.2 API 표 전체 유지”라고 되어 있으나, 현재 첨부 PRD에는 실제 API 표가 포함되어 있지 않음. |
| API별 Request/Response Schema | ❌ | SRS에는 API 목록만 있고 요청·응답 JSON 스키마는 없음. |

### 보완 필요

SRS의 API 섹션은 “목록 수준”으로는 충분하지만, 개발자가 바로 구현 가능한 명세로 보려면 아래 항목을 추가해야 한다.

| 보완 항목 | 필요성 |
| :--- | :--- |
| Request Body Schema | 프론트엔드·백엔드 구현 기준 |
| Response Body Schema | 리포트/브리프/오류 응답 표준화 |
| Error Code 목록 | 예외 처리 일관성 |
| Auth/RBAC 요구사항 | 관리자·코치·고객 권한 분리 |
| Idempotency 정책 | Q42 자동 트리거, F1 중복 호출 방지 |
| Rate Limit / Timeout | LLM API 장애 대응 |
| API ↔ REQ ↔ Test Case Matrix | 테스트 자동화 연결 |

---

## 3.4 엔터티·스키마 Appendix 완성도

### 판정: 🟡 부분 충족

SRS Appendix 6.2에는 다음 엔터티가 정의되어 있다.

| SRS 정의 엔터티 | 상태 |
| :--- | :---: |
| `LEAD` | ✅ |
| `DIAGNOSIS` | ✅ |
| `CLIENT` | ✅ |
| `PROJECT` | ✅ |
| `BRIEF` | ✅ |
| `BRAND_PROFILE` | ✅ |
| `ANSWER_OUTPUT` | ✅ |
| `RETAINER` | ✅ |
| 42개 표준 OUTPUT 변수 요약 | ✅ |

### 주요 문제

| 문제 | 설명 | 영향 |
| :--- | :--- | :--- |
| `ANSWER` 엔터티 누락 | `ANSWER_OUTPUT.answer_id`가 `ANSWER`를 FK로 참조하지만 `ANSWER` 테이블이 정의되어 있지 않음 | 스키마 무결성 오류 |
| ERD Mermaid 없음 | PRD에는 ERD가 있으나 SRS Appendix에는 ERD Mermaid가 없음 | 구조 이해와 구현 전달력 저하 |
| V2 정규화 후보 엔터티 누락 | PRD에 있는 `QUESTION`, `QUESTION_PART`, `BRANDING_ELEMENT`, `ANSWER_PATTERN`, `COACHING_FEEDBACK`, `OUTPUT_MAPPING`, `REPORT_SECTION` 등이 SRS에는 없음 | V1.5/V2 확장 시 설계 공백 |
| 관계 정의 부족 | 텍스트 테이블은 있으나 관계 다이어그램이 없어 FK 흐름이 한눈에 보이지 않음 | 개발자 구현·리뷰 효율 저하 |
| Enum 값 일부 불완전 | 일부 status/package enum은 정의되어 있으나 전체 상태 전이 규칙은 없음 | 상태 관리 오류 가능성 |

### 보완 필요 엔터티

| 엔터티 | 추가 필요 여부 | 이유 |
| :--- | :---: | :--- |
| `ANSWER` | 필수 | `ANSWER_OUTPUT`의 FK 대상 |
| `QUESTION` | 필수 | 42문항 메타데이터 관리 |
| `QUESTION_PART` | 권장 | PART 1~4 구조 관리 |
| `QUESTION_STAGE` 또는 `STAGE` | 권장 | Stage 1~4 흐름 관리 |
| `BRANDING_ELEMENT` | 필수 | 8개 브랜딩 요소 매핑 기준 |
| `ANSWER_PATTERN` | 권장 | P1~P10 패턴 분류 관리 |
| `COACHING_FEEDBACK` | 권장 | 패턴별 코칭 스크립트 관리 |
| `OUTPUT_MAPPING` | 권장 | 질문별 산출물 연결 |
| `REPORT_SECTION` | 권장 | 진단 리포트/마스터 브리프 섹션 관리 |
| `REVIEW_LOG` | 권장 | 검수자 승인·수정·거부 이력 |
| `AUDIT_LOG` | 권장 | 고객 데이터·AI 출력 접근 기록 |

---

## 3.5 Traceability Matrix 완성도

### 판정: 🟡 부분 충족

SRS에는 `5. Traceability Matrix`가 있으며, Story/Feature → REQ → Test Case 연결 구조는 존재한다.

### 충족 사항

| 항목 | 판정 |
| :--- | :---: |
| US-1~US-7 모두 Matrix에 포함 | ✅ |
| F1~F4, F9~F11, F15 기능 단위 Matrix 포함 | ✅ |
| REQ-FUNC와 Test Case ID 연결 | ✅ |
| REQ-NF와 Test Case ID 연결 | ✅ |
| KPI/PF/E11 항목 일부 연결 | ✅ |

### 부족 사항

| 부족 사항 | 설명 |
| :--- | :--- |
| AC 단위 전체 추적성 부족 | Matrix가 Story/Feature 중심이라 `AC-Suf-3`, `AC-Pat-5~8` 등의 누락을 즉시 발견하기 어려움 |
| 누락 AC가 Matrix에 없음 | SRS 본문에 없는 AC가 Matrix에도 없음 |
| REQ-FUNC별 PRD 출처가 일부 부정확 | 예: `REQ-FUNC-011`의 Source가 `US-1, AC-Suf-1, E7`로 되어 있으나, 질문별 쓰임 안내는 `AC-Map-1` 성격에 더 가까움 |
| Test Case 상세 정의 없음 | TC ID만 있고 검증 절차·입력 데이터·예상 결과가 없음 |
| 양방향 추적성 부족 | PRD → SRS는 일부 가능하나, SRS REQ → PRD 근거 역추적은 불완전 |

### 권장 Matrix 구조

현재 Matrix를 아래 형태로 확장하는 것이 좋다.

| PRD Source Type | PRD ID | PRD 요약 | SRS REQ-ID | Test Case | 상태 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Story | US-1 | 질문별 브랜드 자산 매핑 안내 | REQ-FUNC-011 | TC-011 | Covered |
| AC | AC-Suf-3 | 핵심 키워드 0개 시 보완 질문 생성 | REQ-FUNC-083 | TC-083 | Missing → Add |
| AC | AC-Pat-5 | Q4 전문성 마스터리 과소평가 | REQ-FUNC-057 | TC-057 | Missing → Add |
| KPI | KPI-NS-1 | B2B 수주 ≥ 2건/분기 | REQ-NF-040 | TC-NF-040 | Covered |
| API | API-001 | `/api/diagnosis/submit` | REQ-FUNC-010/012 | TC-API-001 | Covered |

---

## 3.6 핵심 다이어그램 충족성

### 판정: ❌ 미충족

SRS에는 Mermaid 기반 Sequence Diagram이 6개 포함되어 있다.  
그러나 요청된 핵심 다이어그램 중 대부분이 없다.

| 요구 다이어그램 | SRS 포함 여부 | 판정 | 비고 |
| :--- | :---: | :---: | :--- |
| UseCase Diagram | 없음 | ❌ | 고객·코치·관리자·AI 엔진의 유스케이스 관계 필요 |
| ERD | 없음 | ❌ | Appendix Entity Model은 있으나 Mermaid ERD 없음 |
| Class Diagram | 없음 | ❌ | 핵심 도메인 클래스와 서비스 클래스 구조 없음 |
| Component Diagram | 없음 | ❌ | Next.js, API, Supabase, Claude, GA4, Typeform 등 컴포넌트 구조 필요 |
| Sequence Diagram | 6개 있음 | 🟡 | 3~5개 요구 대비 6개로 초과. 핵심 5개로 정리 권장 |

### 현재 SRS Sequence Diagram 목록

| # | 제목 | 위치 | 판정 |
| :---: | :--- | :--- | :---: |
| 1 | 고객 축약 진단 → 리포트 → CTA 흐름 | 3.4 | ✅ |
| 2 | F15 코치 분석 노트 자동 생성 흐름 Stage 1 | 3.4 | ✅ |
| 3 | Q42 자동 트리거 → 마스터 브리프 생성 흐름 | 3.4 | ✅ |
| 4 | Stage 3 제출 → 원라이너 3종 생성 → 2차 세션 준비 흐름 | Appendix 6.3 | ✅ |
| 5 | 교차 검증 매트릭스 처리 흐름 | Appendix 6.3 | ✅ |
| 6 | 오류 처리 — LLM API 타임아웃 흐름 | Appendix 6.3 | ✅ |

### 조정 권장

요청 기준이 “Sequence Diagram 3~5개”이므로 다음과 같이 정리하는 것이 좋다.

| 유지 권장 | 이유 |
| :--- | :--- |
| 시퀀스 1. 고객 축약 진단 → 리포트 → CTA | 리드 퍼널 핵심 |
| 시퀀스 2. F15 코치 분석 노트 자동 생성 | 코치 운영 자동화 핵심 |
| 시퀀스 3. Q42 → 마스터 브리프 생성 | 제품 핵심 산출물 |
| 시퀀스 4. Stage 3 → 원라이너 3종 생성 | 2차 세션 핵심 |
| 시퀀스 5. 교차 검증 매트릭스 처리 | 품질 게이트 핵심 |

`시퀀스 6. LLM API 타임아웃`은 Sequence Diagram에서 제외하고 “오류 처리 플로우” 또는 “운영 예외 처리” 섹션으로 이동하는 것을 권장한다.

---

## 3.7 ISO/IEC/IEEE 29148 구조 준수성

### 판정: ✅ 충족에 가까운 부분 충족

SRS는 ISO 29148 기반 SRS로서 기본 구조는 잘 갖추고 있다.

| ISO 29148 관점 | SRS 반영 | 판정 |
| :--- | :--- | :---: |
| 문서 식별 정보 | Document ID, Revision, Date, Standard 명시 | ✅ |
| 목적 | 1.1 Purpose | ✅ |
| 범위 | 1.2 Scope | ✅ |
| 정의·약어 | 1.3 Definitions | ✅ |
| 참조 문서 | 1.4 References | ✅ |
| 이해관계자 | 2. Stakeholders | ✅ |
| 시스템 컨텍스트·인터페이스 | 3. System Context and Interfaces | ✅ |
| 기능 요구사항 | 4.1 Functional Requirements | ✅ |
| 비기능 요구사항 | 4.2 Non-Functional Requirements | ✅ |
| 요구사항 식별자 | `REQ-FUNC`, `REQ-NF` 체계 | ✅ |
| 우선순위 | Must/Should 표기 | ✅ |
| 검증 가능성 | AC와 측정 기준 포함 | ✅ |
| Traceability | 5. Traceability Matrix | 🟡 |
| Appendix | API, Entity, Sequence, Validation Plan 포함 | 🟡 |
| 상태 모델 | 없음 | 🟡 |
| 상세 검증 계획 | TC ID만 있고 상세 테스트 절차 부족 | 🟡 |
| 핵심 다이어그램 | Sequence 외 다이어그램 부족 | ❌ |

### 보완 권장

| 보완 항목 | 이유 |
| :--- | :--- |
| Requirement Quality Checklist 추가 | 요구사항별 원자성·검증 가능성·추적성 점검 |
| Verification Method 컬럼 추가 | Test, Inspection, Analysis, Demonstration 구분 |
| State Model 추가 | 프로젝트 상태: `stage1 → session1 → stage2 → stage3 → session2 → stage4 → brief_generated → delivered` |
| Data Retention / Privacy Requirements 추가 | 자기서사 데이터 보호 강화 |
| Detailed Test Case Appendix 추가 | TC ID만으로는 QA 실행 부족 |
| Open Issues / Assumptions Log 추가 | PRD API 목록 부재, V2 엔터티 범위 등 관리 |

---

## 4. 주요 결함 목록

| ID | 심각도 | 결함 | 영향 | 조치 |
| :--- | :---: | :--- | :--- | :--- |
| GAP-001 | High | `AC-Pat-5~8` 누락 | 5060 특화 신호 감지 범위 축소 | REQ-FUNC-057~059, 063 신설 |
| GAP-002 | High | UseCase/ERD/Class/Component Diagram 없음 | SRS 다이어그램 요건 미충족 | Mermaid 다이어그램 4종 추가 |
| GAP-003 | High | `ANSWER_OUTPUT.answer_id`가 미정의 `ANSWER` 참조 | DB 스키마 무결성 오류 | `ANSWER` 엔터티 추가 |
| GAP-004 | Medium | `AC-Suf-3` 누락 | 답변 품질 보완 자동화 약화 | `REQ-FUNC-083` 신설 |
| GAP-005 | Medium | `AC-One-4` 누락 | 원라이너 품질 게이트 부족 | `REQ-FUNC-078` 신설 |
| GAP-006 | Medium | `AC-Out-2` 누락 | 고객 체감 품질 측정 누락 | `REQ-NF-046` 또는 `REQ-FUNC-006` 신설 |
| GAP-007 | Medium | `AC-Out-5` 조건 일부 누락 | 사람 코치 핸드오프 CTA 약화 | 조건·CTA 명시 요구사항 추가 |
| GAP-008 | Medium | `AC-Logic-2` 문항 수 불일치 | 테스트 기준 혼선 | SRS `REQ-FUNC-101`의 15문항을 17문항으로 수정 |
| GAP-009 | Medium | PRD API 표 부재 | PRD 대비 API 완전성 검증 불가 | PRD §10-4 API 원천 표 복원 또는 SRS에서 출처 명시 |
| GAP-010 | Low | Sequence Diagram 6개 | 요청 기준 3~5개 초과 | 5개 핵심 시퀀스로 정리, 오류 시퀀스는 예외 처리 섹션 이동 |

---

## 5. 수정 우선순위

### P0 — 반드시 수정

| 작업 | 내용 |
| :--- | :--- |
| 누락 AC의 REQ-FUNC 추가 | `AC-Suf-3`, `AC-Pat-5~8`, `AC-One-4`, `AC-Out-2`, `AC-Out-5` |
| `REQ-FUNC-101` 수정 | EXTRACT 대상 문항 수를 PRD 기준 17문항으로 정정 |
| `ANSWER` 엔터티 추가 | `ANSWER_OUTPUT.answer_id` FK 무결성 확보 |
| 핵심 다이어그램 4종 추가 | UseCase, ERD, Class Diagram, Component Diagram |

### P1 — 권장 수정

| 작업 | 내용 |
| :--- | :--- |
| Traceability Matrix AC 단위 확장 | Story/Feature 중심 → Story/AC/KPI/API/Entity 단위 추적 |
| API Request/Response Schema 추가 | 개발 구현 가능 수준으로 구체화 |
| State Model 추가 | 프로젝트 상태 전이 정의 |
| Detailed Test Case 추가 | TC ID별 입력, 절차, 예상 결과 정의 |

### P2 — 품질 향상

| 작업 | 내용 |
| :--- | :--- |
| V2 엔터티 후보 Appendix 보강 | `QUESTION`, `BRANDING_ELEMENT`, `ANSWER_PATTERN` 등 |
| 운영 로그·검수 로그 추가 | `REVIEW_LOG`, `AUDIT_LOG` |
| Sequence Diagram 수량 정리 | 핵심 5개로 정리 |

---

## 6. 추가해야 할 REQ-FUNC 제안

아래 요구사항은 SRS에 직접 추가하는 것을 권장한다.

| 신규 REQ-ID | 요구사항 설명 | Source | Priority | Acceptance Criteria |
| :--- | :--- | :--- | :---: | :--- |
| `REQ-FUNC-006` | 마스터 브리프 검토 시 고객이 “내 핵심을 정확히 짚었다”고 동의하는 비율을 측정해야 하며, 목표 동의율은 85% 이상이어야 한다. | `AC-Out-2` | Must | Given 브리프 생성 완료, When 고객 검토 설문 응답, Then 동의율 ≥ 85% |
| `REQ-FUNC-057` | Q4 답변에서 “당연한 거 아닌가요” 표현 또는 직업 나열만 감지되면 “전문성 마스터리 과소평가” 패턴으로 분류하고 재프레이밍 코칭 메시지를 생성해야 한다. | `AC-Pat-5` | Must | 감지 정밀도 ≥ 80% |
| `REQ-FUNC-058` | Q35 답변에서 “모르겠다” 또는 경력 연수만 제시되면 “차별점 인식 부족” 패턴으로 분류하고 역방향 질문을 생성해야 한다. | `AC-Pat-6` | Must | 감지 정밀도 ≥ 80% |
| `REQ-FUNC-059` | Q24 답변이 현재 직업의 단순 연장이거나 과도하게 추상적이면 “제2챕터 미설계” 패턴으로 분류하고 보완 질문을 생성해야 한다. | `AC-Pat-7` | Should | 감지 정밀도 ≥ 75% |
| `REQ-FUNC-063` | Q38 답변이 “이렇게 해라”형 방법론 메시지로 감지되면 “방법론형 메시지” 패턴으로 분류하고 관점 전환 질문을 생성해야 한다. | `AC-Pat-8` | Must | 감지 정밀도 ≥ 80% |
| `REQ-FUNC-078` | 원라이너 초안 3종이 모두 일관성 점수 0.5 미만이면 “원천 데이터 부족” 경고와 보완 질문을 자동 제안해야 한다. | `AC-One-4` | Should | 경고 적합성 ≥ 85% |
| `REQ-FUNC-083` | 특정 질문에서 핵심 키워드가 0개로 추출되면 해당 문항에 대해 보완 질문 1~2개를 자동 생성해야 한다. | `AC-Suf-3` | Must | 보완 질문 적합도 ≥ 85% |
| `REQ-FUNC-112` | 가치 일관성 점수 < 0.5 또는 사람 코치 권장 플래그 ≥ 3건이면 “사람 코치 핸드오프 권장” 안내와 추가 코칭 세션 CTA를 표시해야 한다. | `AC-Out-5` | Must | 안내 표시율 100%, 핸드오프 적합도 ≥ 85% |

---

## 7. 추가해야 할 Mermaid 다이어그램 목록

SRS의 다이어그램 요건 충족을 위해 다음 4개를 추가해야 한다.

| 다이어그램 | 권장 위치 | 목적 |
| :--- | :--- | :--- |
| UseCase Diagram | 3.5 또는 Appendix 6.5 | 고객·코치·관리자·AI 엔진이 수행하는 주요 유스케이스 정의 |
| ERD | Appendix 6.2 상단 | 엔터티 관계와 FK 구조 명확화 |
| Class Diagram | Appendix 6.6 | 도메인 객체와 서비스 클래스 구조 정의 |
| Component Diagram | 3.1 또는 Appendix 6.7 | Next.js, Backend API, Claude API, Supabase, GA4, Typeform, Monitoring 관계 정의 |

---

## 8. 최종 권고

현재 SRS는 **초안으로는 매우 양호**하다.  
특히 다음 항목은 잘 작성되어 있다.

- ISO 29148 스타일의 문서 골격
- REQ-FUNC / REQ-NF 식별자 체계
- KPI의 NFR 전환
- F1, F2, F10, F11, F15 핵심 기능 요구사항
- API Overview 및 Appendix API 목록
- 42개 OUTPUT 변수 요약
- Sequence Diagram 중심의 핵심 흐름 설명
- Traceability Matrix 기본 구조

그러나 개발 착수 전에는 다음을 반드시 보완해야 한다.

1. **누락 AC 7개와 부분 반영 AC 2개를 REQ-FUNC/REQ-NF로 보강**
2. **UseCase, ERD, Class Diagram, Component Diagram 추가**
3. **Appendix Entity Schema에서 `ANSWER` 및 질문·패턴·매핑 관련 엔터티 보강**
4. **Traceability Matrix를 AC 단위로 확장**
5. **API별 Request/Response/Error Schema 추가**
6. **Sequence Diagram은 핵심 5개로 정리하거나, 6번째 오류 시퀀스를 예외 처리 섹션으로 이동**

**따라서 현재 상태의 판정은 “부분 충족 — 보완 후 승인 권장”이다.**

---

## 9. 한 줄 결론

**SRS는 PRD의 핵심 제품 의도와 주요 기능 요구사항은 잘 반영했지만, 일부 AC 누락, 핵심 다이어그램 부재, Appendix 스키마 불완전성 때문에 최종 승인 전 구조 보강이 필요하다.**
