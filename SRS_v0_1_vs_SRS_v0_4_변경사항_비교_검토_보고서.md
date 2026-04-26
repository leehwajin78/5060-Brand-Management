# SRS_v0_1.md vs SRS_v0_4.md 변경사항 비교 검토 보고서  
## 기술 스택 명확성 / MVP 목표 및 가치전달 조정 / 기타 차이점

- **비교 대상 1**: `SRS_v0_1.md`
- **비교 대상 2**: `SRS_v0_4.md`
- **검토 관점**  
  1. 기술 스택의 명확성  
  2. MVP 목표 및 가치전달 조정 내용  
  3. 기타 차이점  
- **작성 목적**: SRS_v0_1 대비 SRS_v0_4에서 변경·축소·명확화된 내용을 항목별로 비교하고, 변경의 의미와 적절성을 판단한다.
- **작성일**: 2026-04-26

---

## 1. 핵심 결론

`SRS_v0_1.md`는 **5060 프리미엄 브랜드 매니지먼트 전체 시스템**을 전제로 한 개발자 협업용 SRS에 가깝다.  
반면 `SRS_v0_4.md`는 **완전 무료 인프라와 1인 바이브코딩 구현 가능성**을 기준으로 MVP 범위를 크게 축소한 실행형 SRS에 가깝다.

가장 큰 변화는 다음 세 가지다.

| 구분 | SRS_v0_1.md | SRS_v0_4.md | 변화의 의미 |
|---|---|---|---|
| 문서 성격 | 전체 시스템 명세 | Zero-Cost Personal MVP Revision | 개인 구현 가능성 중심으로 전환 |
| 핵심 MVP | F1·F2·F3·F4·F9·F10·F11·F15 포함 | 16문항 진단 → AI 리포트 → 관리자 검수 → CTA | 제품 검증용 최소 가치 흐름으로 축소 |
| 기술 전제 | Claude API, Supabase JSONB, Typeform, Datadog, UptimeRobot | Vercel Hobby, Supabase Free, Gemini Free Tier, Server Actions, Route Handlers | 무료·단순·개인 구현형 스택으로 재정의 |
| 운영 목표 | 99.9% 가용성, 고동시접속, 자동 모니터링 | Best-effort, 동시 진단 3명, 리포트 조회 10명 | 무료 인프라와 충돌하는 SLA 제거 |
| AI 자동화 범위 | 마스터 브리프, 코치 노트, 패턴 분류, 원라이너, 교차검증 | AI 진단 리포트 1개 중심 | 고급 AI 기능은 V1.5/V2로 이동 |

---

## 2. 비교 전제

### 2.1 SRS_v0_1.md의 성격

`SRS_v0_1.md`는 Revision 1.0 문서이며, Draft 상태다. 목적은 5060 고경력 전문가의 암묵지를 42문항 인터뷰로 진단하고, 10가지 답변 패턴을 AI로 분석하며, 최종적으로 8개 섹션의 마스터 브리프와 B2B 제안서·강의안 구조로 변환하는 전체 시스템 구축에 있다.

### 2.2 SRS_v0_4.md의 성격

`SRS_v0_4.md`는 Revision 1.3 문서이며, Status가 `Draft — Zero-Cost Personal MVP Revision`으로 변경되었다. 목적은 전체 시스템 비전은 유지하되, 1차 구현 범위를 완전 무료 인프라 기반 개인 구현 가능 MVP로 축소하는 것이다.

---

# 3. 관점 1 — 기술 스택의 명확성 비교

## 3.1 종합 평가

`SRS_v0_4.md`는 `SRS_v0_1.md`보다 기술 스택이 훨씬 명확해졌다.  
특히 기존의 Claude API·Supabase JSONB·Datadog·UptimeRobot·Typeform 중심 구조에서, **Vercel Hobby + Supabase Free + Gemini API Free Tier + Next.js Server Actions/Route Handlers** 중심으로 정리되었다.

다만 v0_4에서도 한 가지 주의점은 있다.  
`Prisma` 설명에서 “SQLite(로컬) ↔ PostgreSQL(운영)” 표현이 남아 있으나, 완전 무료 개인 MVP 기준에서는 처음부터 Supabase Free PostgreSQL로 통일하는 편이 더 단순할 수 있다.

---

## 3.2 기술 스택 명확성 변경표

| 항목 | SRS_v0_1.md | SRS_v0_4.md | 변경 내용 | 평가 |
|---|---|---|---|---|
| LLM Provider | Claude 3.5 API 채택, 대체 불가 | Gemini API Free Tier 또는 저비용 모델 우선 | 특정 고비용 LLM 고정에서 무료/저비용 모델 중심으로 변경 | 적절 |
| AI 연동 방식 | Claude API 직접 호출 | Vercel AI SDK + Gemini API | Next.js 내부 구현과 맞는 방식으로 정리 | 개선 |
| 데이터베이스 | Supabase PostgreSQL + JSONB, Supabase Client SDK | Supabase Free PostgreSQL + Prisma | DB 접근 방식이 ORM 기반으로 명확화 | 개선 |
| 배포 환경 | 명시적으로 무료 인프라 전제 없음 | Vercel Hobby 또는 무료 배포 환경 | 무료 배포 전제가 명시됨 | 개선 |
| 백엔드 구조 | Backend API / API Gateway 중심 | Single Next.js App, Server Actions, Route Handlers | 별도 백엔드 개념 제거, 단일 앱 구조화 | 매우 개선 |
| 관리자 콘솔 | Next.js 또는 Retool | Next.js Admin Console 중심 | Retool 의존성 제거 | 개선 |
| 모니터링 | Datadog / Sentry / UptimeRobot / Slack 알림 | Sentry Free / Vercel Logs 선택, Datadog/UptimeRobot/Slack 제외 | 무료 MVP 기준에 맞게 단순화 | 매우 개선 |
| 설문/피드백 | Typeform Webhook + REST API | Google Forms 선택, Typeform V2 이동 | 자동 연동 제거, 수동/무료 대체 | 적절 |
| API 구조 | REST Endpoint 중심 | Server Actions / Route Handlers / Deferred APIs 구분 | 구현 단위가 더 명확해짐 | 매우 개선 |
| 데이터 보호 | Claude API 약관 준수 중심 | AI payload에서 실명·연락처 제외, 익명화/동의 선행 | 실제 고객 데이터 보호 기준 강화 | 개선 |
| 무료 인프라 제약 | 명시 부족 | 월 0원, 무료 플랜, Best-effort 운영 명시 | 제약 조건이 명확해짐 | 매우 개선 |
| 상업 운영 전환 | 별도 기준 부족 | 유료 고객·월 50명 이상·장기 저장 시 유료 전환 검토 | 무료/상업 운영 경계가 명확해짐 | 개선 |

---

## 3.3 기술 스택 측면의 핵심 변화

| 변화 유형 | 구체적 변화 | 의미 |
|---|---|---|
| 고정 LLM 제거 | Claude 대체 불가 → Gemini Free/저비용 모델 | 비용 절감 및 무료 MVP 적합성 강화 |
| 백엔드 단순화 | API Gateway → Server Actions/Route Handlers | 바이브코딩 구현 난이도 감소 |
| 운영 자동화 축소 | Datadog/UptimeRobot/Slack → 제외/V2 | 무료 인프라 목표와 정합성 확보 |
| DB 접근 명확화 | Supabase JSONB 직접 저장 → Supabase Free PostgreSQL + Prisma | 데이터 모델 구현 기준 명확화 |
| 외부 연동 최소화 | Typeform 자동 연동 → Google Forms/이메일/카카오 CTA | 개발 속도 개선 |
| 보안 실무화 | 약관 준수 문구 → payload 개인정보 제외 | AI API 사용 리스크 완화 |

---

## 3.4 기술 스택 측면 잔여 검토 포인트

| 잔여 이슈 | 설명 | 권장 조치 |
|---|---|---|
| Prisma 설명의 SQLite 병행 가능성 | v0_4 Definitions에 Prisma가 SQLite↔PostgreSQL 동일 스키마로 설명됨 | 완전 무료 개인 MVP에서는 Supabase Free PostgreSQL 단일 기준으로 단순화 권장 |
| Vercel Hobby 상업 사용 문제 | v0_4에서 유료 전환 조건은 명시했으나 실제 운영 전 재확인 필요 | 상업 고객 발생 전 Pro 전환 체크리스트 추가 |
| Gemini Free 데이터 사용 조건 | v0_4에서 익명화/동의는 반영되었으나 약관 검토 절차 필요 | 운영 전 AI 데이터 처리 약관 확인 절차 명시 |
| 인증 방식 | 단일 관리자 운영으로 단순화했으나 구체 구현 방식은 부족 | 최소 관리자 비밀번호 또는 Supabase Auth 중 택일 필요 |

---

# 4. 관점 2 — MVP 목표 및 가치전달 조정 내용 비교

## 4.1 종합 평가

`SRS_v0_4.md`의 가장 큰 변화는 **MVP의 목표가 전체 제품 구현에서 가치 검증 중심으로 전환된 것**이다.

`SRS_v0_1.md`는 42문항 전체 처리, 마스터 브리프, 원라이너, 코치 노트, 교차검증까지 포함한 “프리미엄 매니지먼트 시스템”을 MVP 범위에 두고 있었다.  
`SRS_v0_4.md`는 이를 과감히 축소하여 다음 흐름을 P0로 재정의했다.

> 랜딩페이지 → 16문항 진단 → 리드/답변 저장 → AI 진단 리포트 → 관리자 검수 → 승인 리포트 웹뷰 → 상담 CTA

이 변경은 개발 난이도, 비용, 운영 리스크를 줄이면서도 핵심 가치인 “자기인식 → 브랜드 방향성 확인 → 상담 전환”은 유지한다.

---

## 4.2 MVP 목표 변경표

| 항목 | SRS_v0_1.md | SRS_v0_4.md | 변경 내용 | 평가 |
|---|---|---|---|---|
| MVP 목적 | 프리미엄 브랜드 매니지먼트 전체 시스템 구축 | 무료 인프라 기반 개인 구현 가능 브랜드 진단 파일럿 MVP | 시스템 완성 → 검증용 MVP로 전환 | 적절 |
| 구현 주체 | 개발자/운영자/코치 분리 가능 | 초급 SW 지식 보유 1인 + AI 코딩 도구 | 실제 구현자 기준 반영 | 개선 |
| 구현 기간 | 명시적으로 현실화 부족 | 3~4주 내 구축 가능한 무료 파일럿 MVP | 기간 현실성 추가 | 개선 |
| 핵심 고객 경험 | 42문항 인터뷰 → 마스터 브리프 → B2B 제안/강의안 | 16문항 진단 → AI 진단 리포트 → 상담 CTA | 가치전달 단순화 | 적절 |
| 주요 산출물 | 마스터 브리프 8섹션, 원라이너, 코치 노트 | AI 진단 리포트, 승인 리포트 웹뷰 | 산출물 축소 | 적절 |
| 고객 전환 | 리포트/브리프 기반 프리미엄 매니지먼트 전환 | 상담 CTA 중심 전환 검증 | 초기 검증 목적에 맞게 조정 | 개선 |
| AI 자동화 범위 | 패턴 분류, 매핑, 코치 노트, 원라이너, 마스터 브리프 | AI 진단 리포트 1개 중심 | 자동화 범위 대폭 축소 | 매우 적절 |
| 사람 검수 | 존재하나 복잡한 브리프 검수 중심 | AI 리포트 수정·승인 중심 | 검수 범위 단순화 | 개선 |
| 후속 로드맵 | V1 제외 항목만 일부 표시 | V1.5/V2로 기능별 이동 단계 명시 | 확장 경로 명확화 | 개선 |

---

## 4.3 가치전달 구조 변경표

| 가치전달 요소 | SRS_v0_1.md에서의 방식 | SRS_v0_4.md에서의 방식 | 가치 훼손 여부 | 판단 |
|---|---|---|---|---|
| 자기인식 | 42문항 또는 Stage 기반 깊은 자기탐색 | 축약 16문항 진단 | 일부 깊이는 줄어듦 | MVP 검증 단계에서는 적절 |
| 개인화 | 42 OUTPUT 변수 기반 분석 | 16문항 답변 원문 기반 AI 리포트 | 일부 약화 가능 | sourceQuestionCodes로 보완 |
| 브랜드 자산화 | 원라이너·핵심가치·USP·페르소나·스토리 등 8섹션 | 강점·약점·브랜드 방향·추천 문장 | 축소됨 | 초기 CTA 전환 검증에는 충분 |
| 코칭 개입 | F15 코치 노트, 스크립트, 사람 핸드오프 | 관리자 수동 검수/수정 | 자동 코칭은 줄어듦 | 운영자가 보완 가능 |
| 상담 전환 | 프리미엄 매니지먼트 상담 CTA | 구글폼/이메일/카카오 CTA | 유지 | 핵심 전환 가치는 유지 |
| 신뢰성 | 사람 코치 검수 + 마스터 브리프 검수 | 관리자 승인 후 리포트 공개 | 유지 | 무검수 자동 공개 방지 |
| 실행 가능성 | 높지 않음 | 크게 향상 | 개선 | v0_4의 핵심 성과 |

---

## 4.4 MVP 범위 조정표

| 기능 | SRS_v0_1.md 상태 | SRS_v0_4.md 상태 | 변경 판단 |
|---|---|---|---|
| 랜딩페이지 | In-Scope | P0 유지 | 유지 |
| 축약 12~16문항 진단 | In-Scope | 16문항 P0로 구체화 | 개선 |
| 리드 저장 | In-Scope | P0 유지 | 유지 |
| 답변 저장 | JSONB/Diagnosis 중심 | Answer 원문 저장 P0 | 구체화 |
| AI 진단 리포트 | 리포트/CTA 포함 | P0 핵심 산출물로 재정의 | 강화 |
| 관리자 콘솔 | 복잡한 검수/프로젝트 현황 | 목록·상세·수정·승인으로 축소 | 적절 |
| 승인 리포트 웹뷰 | 리포트 조회 | approved 상태 리포트만 공개 | 개선 |
| 상담 CTA | 포함 | 구글폼/이메일/카카오 중 하나 | 현실화 |
| 마스터 브리프 8섹션 | Must / MVP 핵심 | V1.5 Deferred | 적절한 후순위화 |
| 원라이너 3종 | Must | V1.5 Deferred | 적절한 후순위화 |
| F15 코치 노트 | Must | V1.5 Deferred | 적절한 후순위화 |
| 교차검증 9개 | Must | V2 Deferred | 적절한 후순위화 |
| Typeform NPS 자동화 | Should | V2 Deferred | 적절 |
| Datadog/UptimeRobot/Slack | 운영 요구 | MVP-Free 제외 | 적절 |
| 복잡한 RBAC | Must | V2 Deferred | 적절 |

---

## 4.5 MVP 조정의 핵심 의미

| 조정 방향 | 의미 |
|---|---|
| 전체 시스템 → 파일럿 MVP | 제품 완성보다 시장 반응 검증 우선 |
| 자동화 중심 → 수동 검수 중심 | AI 품질 리스크를 운영자가 통제 |
| 고급 산출물 → 진단 리포트 | 개발 범위 축소, 빠른 배포 가능 |
| 유료·상용 인프라 → 무료 인프라 | 개인 실험 비용 최소화 |
| SLA 보장 → Best-effort | 무료 인프라와 현실 정합성 확보 |
| 복잡한 API → Server Actions 중심 | 바이브코딩 구현 가능성 상승 |

---

# 5. 관점 3 — 기타 차이점 비교

## 5.1 문서 구조 및 메타데이터 차이

| 항목 | SRS_v0_1.md | SRS_v0_4.md | 변경 내용 |
|---|---|---|---|
| Revision | 1.0 | 1.3 | Zero-Cost Personal MVP Revision으로 개정 |
| Status | Draft | Draft — Zero-Cost Personal MVP Revision | 문서 목적 명확화 |
| Authors | 브랜드 매니지먼트 사업부 (AI Ops) | 브랜드 매니지먼트 사업부 (AI Ops / Personal MVP Revision) | 개인 MVP 개정 주체 반영 |
| 개정 이력 | 없음 또는 1.0 초안 중심 | 1.1, 1.3 개정 이력 포함 | 변경 과정 추적 가능 |
| 문서 목적 | 전체 시스템 SRS | 무료 파일럿 MVP SRS | 성격 변화 |

---

## 5.2 용어 정의 차이

| 영역 | SRS_v0_1.md | SRS_v0_4.md | 변경 의미 |
|---|---|---|---|
| MVP 정의 | 일반 MVP | MVP-Free 추가 | 무료 인프라 기반 MVP 개념 추가 |
| 운영 방식 | 명확한 구분 없음 | Best-effort, Not Guaranteed 추가 | SLA 무보장 명확화 |
| 요구사항 등급 | Must/Should 중심 | Hard Requirement, Soft Target, Manual Alternative, Deferred 추가 | 무료 MVP에 맞는 현실적 등급 체계 |
| 개발 방식 | 일반 개발 전제 | 바이브코딩 정의 추가 | 실제 개발자 역량 반영 |
| 구현 기술 | LLM, JSONB 중심 | Server Action, Route Handler, Prisma, AiRun 추가 | Next.js 구현 단위 명확화 |
| 산출물 | 마스터 브리프 중심 | AI 진단 리포트, 승인 리포트 웹뷰 추가 | MVP 산출물 변경 |

---

## 5.3 이해관계자 차이

| 역할 | SRS_v0_1.md | SRS_v0_4.md | 변경 의미 |
|---|---|---|---|
| 고객 | 5060 고경력 전문가 | 파일럿 고객 | 정식 고객보다 검증 참여자 성격 강화 |
| 운영자/코치 | 세션 운영, 브리프 확정, 핸드오프 | 1인 운영자/코치 | 운영 현실성 반영 |
| 개발자 | 시스템 관리자/개발자 | 1인 개발자/바이브코딩 수행자 | 구현 주체 현실화 |
| AI | AI 분석 엔진 | AI 리포트 생성 모듈 | AI 역할 축소 |
| 비즈니스 오너 | KPI 관리, 파일럿 운영 | 유료화 판단, 상담 전환 검증 | 사업 검증 중심으로 조정 |

---

## 5.4 시스템 흐름 차이

| 항목 | SRS_v0_1.md | SRS_v0_4.md | 변경 의미 |
|---|---|---|---|
| Sequence 수 | 고객 진단, F15 노트, Q42 브리프 등 복수 흐름 | 고객 진단 제출, 관리자 검수 2개 흐름 | 핵심 흐름으로 단순화 |
| AI 호출 | Claude API에 패턴·브리프·코치 노트 요청 | Gemini API에 진단 리포트 생성 요청 | AI 작업 단순화 |
| DB 저장 | Diagnosis JSONB, AnswerOutput, Brief 중심 | Lead, Diagnosis, Answer, Report, AiRun 중심 | 최소 DB 모델로 단순화 |
| 리포트 공개 | 진단 리포트 즉시 표시 가능 | 승인된 리포트만 공개 | 검수 중심 신뢰 구조 강화 |
| 실패 처리 | 재시도·지연 안내·알림 포함 | 실패 시 AiRun 기록 + 검수 후 안내 | 운영 자동화 축소 |

---

## 5.5 API 차이

| API/Action 영역 | SRS_v0_1.md | SRS_v0_4.md | 변경 판단 |
|---|---|---|---|
| 진단 제출 | `/api/diagnosis/submit` REST API | `submitDiagnosis()` Server Action | Next.js 구현 친화적 |
| 리드 생성 | `/api/leads` REST API | `createLead()` Server Action | 단순화 |
| 리포트 조회 | `/api/reports/{diagnosis_id}` | `/api/reports/[id]` Route Handler | Next.js 파일 라우팅에 맞춤 |
| 패턴 분류 | `/api/ai/classify-patterns` | V1.5 Deferred | 적절한 후순위화 |
| 브랜딩 매핑 | `/api/ai/map-branding` | V1.5 Deferred | 적절한 후순위화 |
| 코치 분석 노트 | `/api/ai/coach-brief` | V1.5 Deferred | 적절한 후순위화 |
| 마스터 브리프 | `/api/ai/master-brief` | V1.5 Deferred | 적절한 후순위화 |
| 고객 대시보드 | `/api/clients/{id}/dashboard` | V2 Deferred | 적절 |
| 관리자 검수 | `/api/briefs/{id}/review` | `reviewReport()` Server Action | 리포트 검수 중심으로 축소 |

---

## 5.6 비기능 요구사항 차이

| 항목 | SRS_v0_1.md | SRS_v0_4.md | 변경 판단 |
|---|---|---|---|
| API 성능 | P95 < 200ms | 폼 저장 5초 이내 Soft Target | 무료 인프라 기준 현실화 |
| LLM 성능 | P95 < 25초 | AI 리포트 60초 이내 Soft Target | 현실화 |
| 동시 입력 | 100명 | 3명 | 무료 파일럿 기준으로 축소 |
| 리포트 조회 | 동시 500명 / P95 500ms | 동시 10명 | 무료 파일럿 기준으로 축소 |
| Uptime | 99.9% | 공식 SLA 없음 | 기술적 모순 해소 |
| 모니터링 | UptimeRobot, Datadog, Slack | 제외 또는 선택적 Sentry/Vercel Logs | 비용 절감 |
| 보안 | TLS, RLS, RBAC, Claude 약관 | 개인정보 payload 제외, 승인 리포트만 공개 | MVP에 맞게 실무화 |
| AI 품질 KPI | 정확도 85%, 매핑 90%, 환각 5% 등 | 자동 측정 제외, 수동 검수 중심 | 현실화 |
| 비즈니스 KPI | B2B 수주, Option B, NPS, 리테이너 | 상담 CTA와 파일럿 검증 중심 | 초기 검증에 적합 |

---

## 5.7 Appendix 및 실행성 차이

| 항목 | SRS_v0_1.md | SRS_v0_4.md | 변경 의미 |
|---|---|---|---|
| DB 모델 | Supabase JSONB / AnswerOutput / Brief 중심 | MVP-Free 최소 DB 모델 추가 | 구현 가능성 향상 |
| AI Schema | 마스터 브리프 중심 | AI 진단 리포트 JSON Schema 추가 | 리포트 구현 구체화 |
| Build Plan | 없음 | Vibe Coding Build Plan 추가 | AI 작업 지시 가능 |
| Prompt Pack | 없음 | AI 코딩 도구용 Prompt Pack 추가 | 개인 구현 가능성 강화 |
| Free Infra Limits | 없음 | 무료 인프라 제약 추가 | 비용·운영 리스크 반영 |
| Manual Operation Guide | 없음 | 수동 운영 절차 추가 | 자동화 부족 보완 |
| Upgrade Trigger | 없음 | 유료 전환 기준 추가 | 상업 운영 전환 판단 가능 |

---

# 6. 변경 적절성 종합 평가

## 6.1 긍정적 변화

| 항목 | 평가 |
|---|---|
| 기술 스택 명확성 | 크게 개선됨. 무료 인프라와 Next.js 단일 앱 구조가 명확해짐 |
| MVP 목표 | 전체 시스템 구축에서 파일럿 검증으로 잘 축소됨 |
| 가치전달 | 핵심 흐름인 진단→리포트→검수→CTA는 유지됨 |
| 개발 가능성 | 개인 바이브코딩 기준으로 현실화됨 |
| 비용 효율성 | 월 0원 목표와 충돌하는 요소를 대부분 제거함 |
| 리스크 관리 | SLA, 동시접속, 상업 운영, AI 데이터 전송 리스크를 명시함 |
| 문서 실행성 | Build Plan과 Prompt Pack이 추가되어 AI 작업 지시용으로 개선됨 |

---

## 6.2 주의할 변화

| 항목 | 주의점 |
|---|---|
| 브랜드 자산화 깊이 | 마스터 브리프와 원라이너가 후순위화되어 초기 산출물의 깊이는 줄어듦 |
| 코칭 개입성 | F15 코치 노트가 빠지면서 코칭 보조 기능은 약해짐 |
| AI 품질 관리 | 자동 품질 측정 대신 수동 검수로 전환되므로 운영자 역량 중요 |
| 상업 운영 | Vercel Hobby/무료 인프라 전제에서는 상업 운영 전 유료 전환 필요 |
| 데이터 보호 | 무료 AI API 사용 시 실제 고객 데이터는 익명화/동의 절차 필수 |
| DB 설계 | Prisma/SQLite↔PostgreSQL 표현은 더 단순화할 여지가 있음 |

---

## 6.3 최종 판단

| 관점 | 평가 |
|---|---|
| 기술 스택의 명확성 | **매우 개선됨** |
| MVP 목표 및 가치전달 조정 | **적절하게 축소됨** |
| 기타 문서 구조 및 실행성 | **실행형 문서로 발전함** |
| 남은 보완 필요성 | **소규모 존재** |
| 전체 변경 적절성 | **높음** |

---

# 7. 최종 결론

`SRS_v0_1.md`에서 `SRS_v0_4.md`로의 변화는 단순한 문서 보완이 아니라, **제품 개발 전략의 전환**이다.

기존 문서는 다음 성격이었다.

> 5060 프리미엄 브랜드 매니지먼트 전체 시스템을 개발하기 위한 포괄적 SRS

변경된 문서는 다음 성격이다.

> 완전 무료 인프라에서 1인이 바이브코딩으로 구현 가능한 브랜드 진단 파일럿 MVP SRS

가장 의미 있는 변화는 다음이다.

1. 기술 스택이 Claude·Supabase JSONB·Datadog 중심에서 Vercel Hobby·Supabase Free·Gemini Free·Next.js Server Actions 중심으로 명확해졌다.
2. MVP 목표가 마스터 브리프 자동 생성이 아니라 진단 리포트와 상담 CTA 검증으로 축소되었다.
3. 99.9% SLA, 동시 100/500명, 자동 모니터링 같은 무료 인프라와 충돌하는 요구가 제거되었다.
4. 고급 기능은 삭제가 아니라 V1.5/V2로 이동되어 확장 가능성은 유지되었다.
5. Build Plan과 Prompt Pack이 추가되어 AI 코딩 도구에 작업을 지시하기 쉬운 문서로 바뀌었다.

따라서 `SRS_v0_4.md`는 `SRS_v0_1.md`보다 **개인 구현 가능성, 비용 효율성, MVP 검증 속도, 기술 스택 명확성 측면에서 훨씬 적절한 문서**로 개선되었다.

다만 실제 개발 착수 전에는 다음 3가지만 추가 확정하면 더 안정적이다.

| 추가 확정 항목 | 이유 |
|---|---|
| 관리자 인증 방식 | 단일 비밀번호, Supabase Auth, Basic Auth 중 선택 필요 |
| DB 전략 | Supabase Free PostgreSQL 단일 기준인지, SQLite 로컬 개발 병행인지 확정 필요 |
| AI 데이터 처리 정책 | 무료 Gemini API 사용 시 고객 데이터 익명화/동의 절차 명확화 필요 |
