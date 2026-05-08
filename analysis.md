# AI 광고 마켓플레이스 플랫폼 개발 — 제안 분석 로그

> 생성일: 2026-05-08
> 공고 URL: https://www.wishket.com/project/155185/

## 1. 공고 파싱 결과

```yaml
job:
  title: "AI 광고 마켓플레이스 플랫폼 개발"
  category: "개발 / 웹 중개·매칭 플랫폼 / SaaS·솔루션 / Gen AI 서비스"
  budget_range: "1,200~1,800만 원 (예상 1,500만 원, 업체와 협의)"
  duration: "6주 / 42일 (2026.06.08 ~ 2026.07.17 가정)"
  applicants: 7
  deadline: "2026-05-22"
  priorities:
    - 1순위: 산출물 완성도
    - 2순위: 일정 준수
    - 3순위: 금액
  tech_stack_required:
    - Supabase (BE/DB/Auth/Storage)
    - Vercel (배포)
    - oye.ai.kr 서브도메인
  tech_stack_recommended:
    - Next.js 14 (App Router) + TypeScript + Tailwind CSS
    - shadcn/ui
    - Resend (이메일)
    - Sentry (에러 모니터링)
  scope:
    - 인증/회원 (이메일+카카오+구글 SSO, 광고주/크리에이터 역할)
    - 광고주 기능 (미션 CRUD, 시안 선정, 결제 요청)
    - 크리에이터 기능 (미션 검색/필터, 시안 제출 영상 200MB)
    - 관리자 페이지 (회원/미션/시안/IP/통계, 결제 입금 확인, 신고/차단)
    - IP Showcase (카탈로그, 미션 연결, 시안 IP 뱃지)
    - 결제 링크 (토스페이먼츠 또는 무통장입금, 관리자 수동 승인)
    - 오픈베타 필수 (RLS, rate limiting, 다중계정 차단, SEO/OG, Sentry)
    - 알림/이메일 (Resend, Slack)
    - 반응형 디자인 (Figma 시안 기반 퍼블리싱)
  out_of_scope_phase2:
    - IP 라이선싱 정산 시스템
    - IP 홀더 자체 가입/대시보드
    - 결제 풀 PG 연동/자동 정산/환불 자동화
    - 실시간 채팅/메시지
    - Meta/Google/TikTok 광고 자동 집행 API
    - AI 영상 생성 기능
    - 크리에이터 등급/평가 시스템
  client_questions:
    - "구현 범위 보시고: (1) 가장 우려되는 부분 / 대응 방안, (2) 일정 압박 시 우선순위 조정"
    - "Next.js + Supabase로 SaaS/마켓플레이스 구축 경험 1~2개 (역할/기술적 난이도)"
  client_provides:
    - 약관/개인정보처리방침/환불정책 텍스트
    - UI/UX Figma 시안
    - 서비스 흐름도/와이어프레임/DB 스키마 초안
    - 시드 데이터
    - 도메인, Supabase/Vercel 계정
  job_post_url: "https://www.wishket.com/project/155185/"
```

## 2. URL/이미지 분석

- 공고 본문에 첨부된 별도 참고 사이트, Figma 링크, 이미지 파일 없음
- 도메인 oye.ai.kr는 비공개 상태(착수 후 발주처 제공)
- 비교 사례로 본문에 "크몽과 유사하나 1:1 매칭이 아닌 챌린지 방식 + IP 라이선싱 레이어"라는 텍스트 단서만 존재
- **결론**: 외부 URL/이미지 분석 단계 건너뜀 — 본문 텍스트만으로 분석 진행

## 3. 실현 가능성 분석 (내부용)

### 프로젝트 유형 판정
- 풀스택 웹앱(Next.js + Supabase) + 영상 처리(200MB) + 외부 API 연동(SSO, 토스페이먼츠) → **조건부 가능**, 버퍼 +15%

### 기본 공수 산정 (AI 보조 없는 베이스)
| 영역 | M/D |
|------|-----|
| 기획/PRD/설계 | 5 |
| FE 개발 (광고주/크리에이터/관리자/IP Showcase) | 32 |
| BE/Supabase (DB/RLS/Edge Function/Storage/SSO/결제) | 22 |
| QA / 배포 / 문서 | 8 |
| **합계** | **67 M/D** |

### 효율 반영 (AI 보조 가중 평균 50%)
- 기획: 5 × 0.65 = 3.25
- FE: 32 × 0.35 = 11.2
- BE: 22 × 0.45 = 9.9
- QA/배포: 8 × 0.45 = 3.6
- 소계: 27.95 M/D
- +15% 버퍼(조건부 가능): **32 M/D**

### 달력 일수 환산 vs 클라이언트 예상
- 32 M/D × (7/5 주말 보정) = 약 45일
- 클라이언트 예상: 42일 (6주)
- 차이: 3일 (7%, 20% 이내)

### 판정
- **클라이언트 기간(42일) 그대로 사용** + 명시적 스코프 가드레일(IP Showcase 베타 간소화, Phase 2 분리)
- 발주처가 Figma 시안 + 약관/정책 텍스트 + 시드 데이터 + 도메인/계정을 선제공하므로 외주 측 종속 작업 감소 → 42일 내 충분히 수행 가능

## 4. 포트폴리오 매칭

### 매칭 결과 (3개 추천)

| Rank | Project | Score | 매칭 근거 |
|------|---------|-------|----------|
| 1 | **EZ-Approve** | 9/10 | Next.js + 다중 역할 RBAC + 50+ 페이지 어드민 + 토큰 기반 외부 진입 — 본 프로젝트 3 역할 권한 모델 + 결제 링크 패턴과 직접 호환 |
| 2 | **Connectin** | 8/10 | 매칭 플랫폼 + 다중 역할 사용자 + 마이크로서비스 + 3개월 베타 단기 일정 준수 — 본 프로젝트의 챌린지형 매칭과 다면 사용자 권한 분리에 적용 |
| 3 | **Calendar Share** | 9/10 | Supabase Auth + Postgres + RLS + Storage 풀 스택 직접 운영 경험 — 본 프로젝트 핵심 기술 스택과 정확히 일치 (가장 핵심적 매칭) |

### 매칭 근거 점수
- 기술 스택 일치(40%): Calendar Share = Supabase 직접 매칭 / EZ-Approve = Next.js 매칭 / Connectin = Next.js + Postgres 매칭
- 도메인 유사성(30%): Connectin(매칭 플랫폼) > EZ-Approve(B2B SaaS) > Calendar Share(B2C 앱)
- 기능 유사성(20%): EZ-Approve(다중 역할 어드민) > Connectin(매칭) > Calendar Share(RLS 정책)
- 규모 적합성(10%): EZ-Approve(50+ 페이지 9주) ≈ Connectin(3개월 12 마이크로서비스) ≈ Calendar Share(45+ 스크린)

## 5. 최종 제안 요약

- **지원 금액**: 15,300,000원 (VAT 별도) — 발주처 예상 상한 1,800만 원의 85%
- **지원 기간**: 42일 (6주, 클라이언트 예상 일정 그대로)
- **핵심 제안 포인트**:
  - 다중 역할 RBAC를 RLS 정책으로 매핑 (7 역할 → 본 3 역할 매트릭스)
  - 영상 업로드 추상화 레이어 우선 설계 (Supabase Storage → Mux/Cloudflare Stream 전환 가능)
  - 결제 링크 + 관리자 수동 승인 워크플로우의 명시적 상태 머신
  - 오픈베타 보안 항목(RLS/rate limiting/Sentry/SSO)을 Phase 1 내 일괄 셋업
  - IP Showcase는 베타 간소화 버전(카탈로그 + 미션 연결 + 시안 IP 뱃지)에 집중, 정산 시스템은 Phase 2 분리
  - 인수인계 가능한 산출물(README, ERD, RLS 명세, API 명세, 환경변수, 배포 가이드)

## 6. 최종 산출물

### 제안서 사이트 URL
https://proposal-router.claude-ai-b27.workers.dev/proposal-ai-ad-marketplace-platform/

### 지원 금액 (복사용)
```
15,300,000원 (VAT 별도)
```

### 지원 기간 (복사용)
```
42일
```

### 클라이언트 질문 답변 (복사용)

**Q1. 6주 안에 오픈 베타 가능한 수준 완성 — (1) 가장 우려되는 부분 / 대응 방안, (2) 일정 압박 시 우선순위 조정 시 빼는 기능**

(1) 가장 우려되는 부분 3가지와 대응 방안

- 영상 업로드(200MB) 안정성: Supabase Storage 직접 업로드 시 단일 PUT 한계 + 모바일 네트워크 끊김 리스크. 대응 — tus 또는 resumable 업로드 패턴 + 서버 측 재시도/이어받기, 업로드 인터페이스를 추상화 레이어로 캡슐화하여 트래픽 증가 시 Mux/Cloudflare Stream으로 비파괴 전환 가능하도록 설계.
- RLS 권한 매트릭스의 누락 위험: 광고주/크리에이터/관리자 + 미션·시안·IP·결제 객체의 교차 권한이 많아 RLS 정책 누락 시 보안 사고로 직결. 대응 — Phase 1 첫 주에 권한 매트릭스 표를 작성·승인받고 RLS 정책을 마이그레이션 파일로 명시화, 정책별 통합 테스트 케이스 작성.
- 카카오 OAuth + 결제 링크의 외부 의존성: 도메인 검증·콜백 URL·결제 토큰 만료 등 외부 환경에서 발생하는 비결정적 이슈가 후반 일정에 누적되면 베타 오픈 지연. 대응 — Phase 1에 SSO·결제 링크 골격을 인증 모듈과 함께 선처리, 외부 연동 실패 시 운영자 슬랙·이메일 알림으로 빠른 인지.

(2) 일정 압박 시 우선순위 조정 — 빼거나 축소할 기능

- P0 (절대 보존): 인증/회원, 광고주 미션 등록·시안 선정, 크리에이터 시안 제출(영상 업로드), 결제 링크 발행, RLS 보안 설정, Sentry 에러 모니터링
- P1 (베타 간소화로 축소): 관리자 통계 대시보드 → 핵심 4개 지표(가입자/미션/시안/활성)만 SQL view로 단순 노출, 어뷰징 차단 → rate limiting 우선·다중계정 차단은 후속, IP Showcase → 카탈로그 + 미션 연결 + 시안 IP 뱃지만 우선
- P2 (Phase 2로 이관 후보): 신고/차단 워크플로우 → 베타 단계에서는 이메일 알림만 처리, 통계 대시보드 → 스프레드시트 export로 대체, 시드 데이터 입력 도구 → 최소 SQL 스크립트로 대체

스코프 조정이 필요해질 경우 위 우선순위를 발주처와 매주 미팅에서 합의하여 베타 오픈 일정(7월 둘째 주) 자체는 절대 양보하지 않는 방향으로 운영하겠습니다.

**Q2. Next.js + Supabase로 SaaS / 마켓플레이스 구축 경험 1~2개 — 역할, 기술적 난이도**

두 축으로 답변드립니다.

(1) Next.js + 다중 역할 SaaS 구축 — B2B 전자결재 SaaS (2026.01–2026.03, 약 9주)
- 역할: 풀스택 단독 — 설계·프론트엔드·백엔드·인프라·배포 100%
- 규모: PR 504건, 50+ 페이지, 7 사용자 역할, 6계층 보안, 120-150 API 엔드포인트
- 기술 스택: Next.js 13 (App Router) + TypeScript + NestJS + MySQL + CASL(RBAC) + Lexical + Yjs(CRDT) + MUI v5
- 가장 까다로웠던 기술 난이도: (a) 7 사용자 역할 × 8 결재 액션 × 다단계 워크플로우의 권한 매트릭스를 CASL로 정합성 있게 모델링, (b) Lexical + Yjs CRDT 기반 실시간 공동편집의 충돌 해소 + 권한 분리 + 외부 셀프서비스 포탈에 토큰 기반으로 진입하는 외부 진입 패턴 설계
- 본 프로젝트와의 연결: 다중 사용자 역할 RBAC를 RLS 매트릭스로 옮기는 작업 + 외부 진입(결제 링크) 패턴이 그대로 재사용 가능

(2) Supabase 풀 스택 활용 — B2C 소셜 캘린더 앱 (2025.01–, MVP)
- 역할: 풀스택 단독 — Supabase 백엔드 설계 + Flutter 앱 + Firebase 듀얼 백엔드 동기화
- 규모: 17,628 LOC, 45+ 스크린, 7종 알림, 듀얼 백엔드 아키텍처
- 기술 스택: Supabase Auth + Postgres + RLS + Storage + Realtime + Flutter 3.27 + Firebase
- 가장 까다로웠던 기술 난이도: (a) Supabase RLS 정책을 친구 관계·이벤트·이미지 업로드 객체에 모두 적용하면서 Realtime subscribe와 RLS 일관성 확보, (b) Firebase + Supabase 듀얼 백엔드의 사용자 동기화 — 인증 토큰 매핑·Storage 미디어 이중 업로드의 트랜잭션 보장
- 본 프로젝트와의 연결: Supabase Auth + Postgres + RLS + Storage 풀 스택 활용 경험이 본 프로젝트 핵심 기술 스택(SSO 포함)과 정확히 일치

두 경험을 결합하여 본 프로젝트의 Next.js 14 App Router + Supabase Auth/DB/Storage/RLS 풀 스택을 안정적으로 구현 가능합니다.

### 지원 내용 (복사용)

```
안녕하세요, AI 광고 마켓플레이스 플랫폼 개발 프로젝트에 지원합니다.

본 프로젝트에 대한 상세 제안서(견적서, 공수계산서, PRD, 일정, 포트폴리오)를 별도 페이지로 준비하였습니다. 아래 링크에서 확인해 주시면 감사하겠습니다.
▶ 제안서 상세 페이지: https://proposal-router.claude-ai-b27.workers.dev/proposal-ai-ad-marketplace-platform/
▶ 위시켓 포트폴리오: https://www.wishket.com/partners/p/blueverse1/

---

<프로젝트 진행 제안>

■ 프로젝트 분석
- 광고주·크리에이터·관리자 3 사용자 그룹이 미션·시안·IP·결제를 중심으로 거래하는 챌린지형 3면 마켓플레이스
- 7월 둘째 주 오픈 베타 런칭 — 일반 사용자 트래픽 대응 안정성·보안 확보가 1순위 목표
- 차별점: IP Booster — 드라마/연예인/웹툰 IP를 광고 소재로 활용하는 라이선싱 레이어
- 베타 단계 스코프 잠금: IP 정산, 자동 결제 풀, 실시간 채팅, AI 영상 생성, 크리에이터 등급은 Phase 2 분리

■ 작업 일정

[Phase 1] Day 1–7 (기획·설계·인증 골격)
- 요구사항 정렬, ERD 및 RLS 권한 매트릭스 작성·승인, API 명세 v1
- Supabase Auth + 카카오/구글 SSO + 이메일 인증 골격 셋업, Figma 시안 매핑

[Phase 2] Day 8–21 (광고주·크리에이터 핵심 플로우)
- 미션 등록·관리(CRUD, 브랜드 에셋, IP 옵션), 시안 제출(영상 200MB 추상화 업로드)
- 시안 목록/상세/선정 E2E, 검색·카테고리 필터·정렬

[Phase 3] Day 22–31 (관리자·IP·결제·알림)
- 관리자 콘솔(회원/미션/시안/IP/통계, 시드 도구), IP Showcase 카탈로그·미션 연결·시안 IP 뱃지
- 토스페이먼츠 결제 링크 + 관리자 수동 입금 확인, Slack/Resend 알림

[Phase 4] Day 32–38 (QA·보안·베타 운영 준비)
- RLS 정책 검증, rate limiting, 다중계정 차단, 신고/차단 워크플로우
- Sentry 통합, SEO/OG/sitemap, 시드 데이터 입력

[Phase 5] Day 39–42 (인수인계·문서화)
- README, ERD 다이어그램, RLS 명세, API 명세, 환경변수, 배포 가이드 최종화
- oye.ai.kr 도메인 연결, 인수인계 미팅 1~2회

■ 마일스톤 및 산출물
- M1 (Day 7): 인증·DB 기반 — 가입/로그인 + RLS 매트릭스 승인
- M2 (Day 21): 핵심 플로우 알파 — 미션 등록 → 시안 영상 제출 → 선정 E2E 동작
- M3 (Day 31): 운영·결제·IP 베타 — 관리자 콘솔 + IP Showcase + 결제 링크 + 알림 정상 동작
- M4 (Day 38): 베타 오픈 준비 — 보안 리뷰 통과, Sentry/SEO/OG/신고·차단 완료
- M5 (Day 42): 인수인계 완료 — 문서·미팅 종료, oye.ai.kr 운영 환경 핸드오버

■ 미팅 시 협의 필요 사항
- RLS 권한 매트릭스 — 광고주/크리에이터/관리자 × 미션·시안·IP·결제 객체 교차 권한 표 합의
- 영상 업로드 추상화 인터페이스 — Mux/Cloudflare Stream 전환 시 트리거 기준
- 결제 링크 워크플로우 — 결제 요청·입금 확인·미션 활성화 상태 머신
- IP Showcase 베타 간소화 범위 — 카탈로그 항목·시안 뱃지 노출 정책
- 어뷰징 방지 정책 — rate limiting 임계값, 다중계정 차단 기준
- 인수인계 범위 — 문서 양식, 운영 매뉴얼, 1~2회 미팅 일정

---

<유사 프로젝트 진행 경험>

▶ 7 사용자 역할·다단계 워크플로우 SaaS (2026.01–2026.03, 약 9주)
- 프로젝트 유형: B2B 전자결재 SaaS · 다중 역할 RBAC
- 핵심 기능: 50+ 페이지 어드민, 7 사용자 역할, 다단계 결재(8종 액션), 토큰 기반 외부 셀프서비스 포탈, 실시간 공동편집
- 유사점: 다중 사용자 역할 RBAC 매트릭스 설계 → 본 3 역할 RLS 매트릭스에 직접 적용. 토큰 기반 외부 진입 패턴이 결제 링크 발행/입금 확인 흐름과 호환.
- 기술 스택: NestJS 10, Next.js 13 (App Router), TypeScript, MySQL 8, CASL (RBAC), Lexical + Yjs, MUI v5

▶ 다중 사용자 매칭·네트워킹 플랫폼 (2025.05–2025.08, 3개월)
- 프로젝트 유형: B2B 매칭 플랫폼 · 마이크로서비스
- 핵심 기능: 12 마이크로서비스, 63 API, 41 모바일 기능, 디지털 명함, BLE 근거리 탐색, E2E 암호화
- 유사점: 다면 마켓플레이스 사용자 매칭 흐름 + 역할별 권한·프로필 분리 모델 + 3개월 베타 단기 일정 준수 경험.
- 기술 스택: Next.js, React, TypeScript, Express, PostgreSQL, Flutter, 마이크로서비스

▶ Supabase Auth/DB/Storage 풀 스택 활용 앱 (2025.01–, MVP)
- 프로젝트 유형: B2C 소셜 캘린더 · Supabase 풀 스택
- 핵심 기능: Supabase Auth + Postgres + RLS + Storage + Realtime, 듀얼 백엔드(Firebase + Supabase) 동기화, 7종 알림, 45+ 스크린
- 유사점: 본 프로젝트 핵심 기술 스택과 정확히 일치 — Supabase 풀 스택 운영 경험을 그대로 적용. RLS 정책 매트릭스 노하우 + Storage 업로드 추상화 패턴이 영상 200MB 업로드와 직접 연결.
- 기술 스택: Supabase (Auth, Postgres + RLS, Storage, Realtime), Flutter 3.27, Firebase

---

<사용 기술과 툴>

▶ 개발 기술
- 프론트엔드: Next.js 14 (App Router), TypeScript, Tailwind CSS, shadcn/ui
- 백엔드/DB: Supabase (Auth, Postgres + RLS, Storage, Edge Functions)
- 외부 연동: 카카오/구글 SSO, 토스페이먼츠 결제 링크, Resend(이메일), Slack Webhook
- 모니터링: Sentry (무료 티어)
- 배포: Vercel + oye.ai.kr 서브도메인

▶ 개발 도구 및 인프라
- 버전 관리: GitHub
- CI/CD: Vercel 자동 배포 + GitHub Actions
- 환경 분리: Supabase Project (dev / prod), Vercel Preview / Production

▶ 커뮤니케이션
- 일일 진행 공유: Slack 또는 카카오톡
- 주간 미팅: Zoom / Google Meet
- 문서 공유: Notion 또는 Google Docs
- 이슈 트래킹: GitHub Issues 또는 Linear
```

### 관련 포트폴리오 추천 (위시켓 폼 선택용)

1. **7 사용자 역할·다단계 워크플로우 SaaS (전자결재)** — 다중 역할 RBAC 매트릭스 + 50+ 페이지 어드민 단기 구축 + 토큰 기반 외부 진입(결제 링크 패턴)
2. **다중 사용자 매칭·네트워킹 플랫폼** — 다면 마켓플레이스 매칭 흐름 + 역할별 권한·프로필 분리 + 3개월 베타 단기 일정 준수
3. **Supabase Auth/DB/Storage 풀 스택 활용 앱 (소셜 캘린더)** — Supabase Auth + Postgres + RLS + Storage 풀 스택 직접 운영 (본 프로젝트 핵심 기술 스택 정확히 일치)

