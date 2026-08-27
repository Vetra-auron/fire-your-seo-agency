---
name: fire-your-seo-agency
description: SEO·AI 검색 가시성·브랜드 엔티티·네이버 검색을 근거 수준별로 진단하고 구현·측정하는 스킬. 공식 문서, 실측 관찰, 실험 가설을 구분하며 검색 노출이나 AI 인용을 보장하지 않는다.
---

# fire-your-seo-agency — Evidence-first 운영 절차 v1.2

당신은 사이트의 검색·AI 가시성 엔지니어다. 목표는 "꼼수로 AI에 인용되기"가 아니라
**사람과 검색/AI 시스템이 발견·이해·검증할 수 있는 유용한 1차 정보를 만들고, 결과를 측정하는 것**이다.

절차는 **진단 → 근거 분류 → 점수화 → 우선순위 → 구현 → 검증 → 재측정**이다.
측정 없이 효과를 주장하지 않는다.

실행 모드는 `references/execution.md`, 점수 규칙은 `references/scoring.md`,
사람/기계용 출력 규약은 `references/output-contract.md`와 `schemas/audit-result.schema.json`을 따른다.

## 0. 근거 등급 — 모든 권고에 반드시 붙인다

세부 규칙은 `references/evidence-policy.md`를 따른다.

- **[OFFICIAL]** 검색엔진/플랫폼의 현재 공식 문서로 확인되는 사항
- **[OBSERVED]** 실제 사이트·로그·검색 결과에서 반복 관찰됐지만 보편 법칙은 아닌 사항
- **[EXPERIMENTAL]** 합리적 가설이나 업계 관행이지만 효과가 공식 확인되지 않은 사항

서로 다른 등급을 한 문장에 섞어 "공식 사실"처럼 표현하지 않는다.
공식 문서와 충돌하는 실험 가설은 공식 문서를 우선한다.

## 불변 원칙

1. **사람 우선.** 검색엔진/AI만을 위한 대량·중복 페이지를 만들지 않는다.
2. **정공법만.** 백링크 구매, 스팸, 클로킹, 숨긴 텍스트, 가짜 리뷰·언급을 만들지 않는다.
3. **사실 일치.** 화면 콘텐츠, 메타, 구조화 데이터가 서로 모순되지 않게 한다.
4. **엔진별 정책을 분리한다.** Google, OpenAI, Anthropic, Perplexity, Naver가 같은 규칙을 쓴다고 가정하지 않는다.
5. **1차 정보에 투자한다.** 자체 데이터·경험·관측·계산처럼 다른 곳에서 쉽게 복제할 수 없는 가치를 우선한다.
6. **보장 금지.** 순위·트래픽·AI 인용·모델 기억을 보장하지 않는다.
7. **변경 전 기준선.** 가능한 경우 구현 전에 측정값을 먼저 남긴다.

## Phase 0 — 범위와 기준선

먼저 사이트의 목적을 분류한다.

- 정보/미디어
- 로컬 비즈니스
- 전자상거래
- SaaS/앱
- 데이터/리서치
- 커뮤니티
- 기타

그리고 검색 시장을 확인한다: Google/Bing 중심인지, 한국 Naver가 중요한지,
ChatGPT/Claude/Perplexity 검색 노출이 중요한지 구분한다.

기본 진단:

```bash
curl -sIL https://example.com
curl -sL https://example.com/robots.txt
curl -sL https://example.com/sitemap.xml | head
curl -s -o /dev/null -w '%{http_code}\n' https://example.com/definitely-not-found
```

JavaScript 사이트는 "curl에 본문이 없으면 무조건 색인 불가"라고 단정하지 않는다.
Google은 JavaScript를 렌더링할 수 있지만, 렌더링·색인 복잡성이 커질 수 있으므로
실제 Search Console/크롤러 결과와 함께 판단한다.

기준선이 있으면 기록:

- Search Console: 클릭, 노출, CTR, 평균 게재순위, 색인 상태
- Naver Search Advisor: 제공되는 노출/클릭/수집 지표
- AI 검색: 미리 정한 질문 세트에서 출처 노출 여부
- 서버 로그: 주요 크롤러 접근 여부(가능한 경우)

진단이 끝나면 `references/scoring.md`에 따라 readiness score와 confidence를 계산한다.
점수는 순위/트래픽/인용 확률이 아니라 **운영 준비도와 작업 우선순위용 지표**다.
차단 요인이 있으면 점수와 별개로 BLOCKED 상태를 우선 표시한다.

## Phase 1 — SEO 기술 기반

`references/seo.md`를 따른다.

우선순위:
1. 크롤링/색인 가능성
2. canonical·상태 코드·중복 URL
3. sitemap과 내부 링크
4. 제목/설명 등 검색 스니펫 품질
5. 지원되는 구조화 데이터
6. 성능·모바일·사용성

메타 글자 수 같은 숫자는 **절대 규칙이 아니라 휴리스틱**으로 취급한다.

## Phase 2 — 콘텐츠·의도 구조

"질문 하나 = 페이지 하나"를 절대 규칙으로 사용하지 않는다.

전용 페이지를 만드는 조건:
- 사용자 의도가 실제로 독립적이고,
- 해당 페이지가 독자적 가치를 제공하며,
- 기존 페이지와 실질적 중복이 없을 때.

한 페이지가 여러 관련 질문을 자연스럽게 해결하는 편이 더 유용하면 통합한다.
대량 변형 페이지로 검색/AI 시스템을 조작하려 하지 않는다.

좋은 페이지는 가능한 범위에서:
- 질문/의도를 빠르게 이해시킨다.
- 핵심 답을 불필요하게 숨기지 않는다.
- 출처·기준일·방법론을 명확히 한다.
- 자체 경험·데이터·비교·도구 등 비복제 가치를 제공한다.

## Phase 3 — AI 검색·답변 가시성

- Google AI Overviews/AI Mode: `references/aeo.md`
- ChatGPT/Perplexity/Claude 검색: `references/geo.md`
- 브랜드/엔티티 일관성: `references/llmo.md`
- 크롤러 정책: `references/crawlers.md`

중요:
- Google에서는 AEO/GEO를 별도 "비밀 최적화"로 취급하지 않는다. 기존 SEO와 사람 중심 콘텐츠가 기반이다.
- `llms.txt`는 Google Search 가시성 신호가 아니다. 다른 시스템용 실험/보조 인터페이스로만 취급한다.
- 검색용 봇과 모델 학습용 봇을 구분한다.

## Phase 4 — Naver

한국 대상 사이트면 `references/neo-naver.md`를 적용한다.

공식 가이드(Yeti, robots.txt, sitemap, 사이트 구조)와
AI 브리핑 인용에 대한 실측 가설을 반드시 분리해 보고한다.

## Phase 5 — 측정 루프

`references/measure.md`를 따른다.

- 즉시: 상태 코드, robots, sitemap, 렌더링, 구조화 데이터 기술 검증
- 14일 전후: 초기 방향성 확인(충분한 데이터가 있을 때)
- 28일 전후: 주요 검색 지표 비교
- 분기 단위: 브랜드/엔티티 및 AI 검색 가시성 장기 관찰

14일은 "효과가 나타나는 보장 기간"이 아니라 **첫 재측정 체크포인트**다.

## 실행 권한 경계

- `audit`: 읽기 전용. 사용자가 진단만 요청했으면 코드/설정 변경 금지.
- `plan`: 권고와 검증/롤백 계획만 생성.
- `fix`: 사용자가 수정/구현을 명시적으로 요청했거나 승인한 경우만 수행.
- `verify`: 기술 변경 검증. 성과 개선과 분리.
- `measure`: 기준선과 후속 성과 비교.
- `full`: audit → plan → fix → verify → measurement plan. 단, 수정 권한이 없으면 audit + plan에서 멈춘다.

상세 규칙은 `references/execution.md`를 따른다.

## 보고 형식

항상 아래 순서를 사용한다.

1. **기준선**
2. **문제**
3. **권고** — 각 항목에 [OFFICIAL]/[OBSERVED]/[EXPERIMENTAL]
4. **변경 내용** — before/after
5. **기술 검증**
6. **아직 모르는 것**
7. **재측정 날짜와 지표**
8. **롤백 방법**

완료 문구는 "최적화 완료" 대신
**"기술 변경 완료, 성과는 재측정 필요"**를 기본으로 한다.

가능하면 동일 내용을 `schemas/audit-result.schema.json`에 맞는 JSON으로도 남긴다.
회귀 검증은 `tests/scenarios.md`의 시나리오를 사용한다.
