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

- **지원 금액**: 16,200,000원 (VAT 별도) — 발주처 예상 상한 1,800만 원의 90%
- **지원 기간**: 42일 (6주, 클라이언트 예상 일정 그대로)
- **핵심 제안 포인트**:
  - 다중 역할 RBAC를 RLS 정책으로 매핑 (7 역할 → 본 3 역할 매트릭스)
  - 영상 업로드 추상화 레이어 우선 설계 (Supabase Storage → Mux/Cloudflare Stream 전환 가능)
  - 결제 링크 + 관리자 수동 승인 워크플로우의 명시적 상태 머신
  - 오픈베타 보안 항목(RLS/rate limiting/Sentry/SSO)을 Phase 1 내 일괄 셋업
  - IP Showcase는 베타 간소화 버전(카탈로그 + 미션 연결 + 시안 IP 뱃지)에 집중, 정산 시스템은 Phase 2 분리
  - 인수인계 가능한 산출물(README, ERD, RLS 명세, API 명세, 환경변수, 배포 가이드)

## 6. 최종 산출물

(8단계 완료 후 추가 예정)
