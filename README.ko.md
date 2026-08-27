# 🔥 fire-your-seo-agency — Evidence-first v1.2

**한국어** · [English](./README.md)

> SEO·AEO·GEO·LLMO·NEO를 한 번에 점검하되, **공식 사실·실측 관찰·실험 가설을 구분**하는 Claude Code 스킬입니다.

이 저장소는 `leopard627/fire-your-seo-agency`를 기반으로 한 fork이며, 현재 v1.2는 **반복 실행 가능한 Search Visibility Agent 운영 규약**까지 포함합니다.
원본의 **진단 → 구현 → 측정** 구조와 한국 시장용 Naver 레인을 유지하면서,
과도하게 단정적인 SEO/GEO 규칙을 최신 공식 문서 기준으로 보정했습니다.

## 이 fork에서 바뀐 핵심

1. 모든 권고를 **[OFFICIAL] / [OBSERVED] / [EXPERIMENTAL]**로 분리
2. `OAI-SearchBot`과 `GPTBot` 등 **검색용/모델 개발용 크롤러 구분**
3. `llms.txt`를 필수 SEO/GEO 신호가 아닌 **선택적 실험 요소**로 재분류
4. "질문 하나 = 페이지 하나", "첫 답변 40자" 같은 규칙을 절대 요건에서 휴리스틱으로 변경
5. meta title/description 글자 수를 고정 규칙이 아닌 가이드로 변경
6. FAQ JSON-LD와 AI 인용의 인과관계 주장 제거
7. Naver 공식 가이드와 AI 브리핑 실측 가설 분리
8. 14일을 성과 보장 기간이 아닌 **첫 재측정 체크포인트**로 변경
9. 기술 변경과 실제 성과를 별도 판정
10. 모든 작업에 **롤백·모르는 것·후속 측정** 포함

## 다섯 레인

| 레인 | 대상 | 핵심 질문 |
|---|---|---|
| SEO | Google/Bing/Naver의 기본 검색 | 발견·크롤링·색인·이해가 가능한가? |
| AEO | AI Overviews 등 답변형 검색 | 유용하고 검증 가능한 답을 제공하는가? |
| GEO | ChatGPT/Perplexity/Claude 검색 | 검색 크롤러가 접근하고 출처로 발견할 수 있는가? |
| LLMO | 브랜드/엔티티 일관성 | 공개 웹의 브랜드 사실이 일관되고 정확한가? |
| NEO | Naver 검색·AI 브리핑 | Naver 공식 기반과 AI 출처 실험을 분리해 관리하는가? |

## 설치

이 fork를 직접 사용할 경우:

```bash
git clone https://github.com/Vetra-auron/fire-your-seo-agency.git .claude/skills/fire-your-seo-agency
```

개발 중인 Evidence-first 브랜치를 시험하려면:

```bash
git clone -b evidence-first-v1.1 https://github.com/Vetra-auron/fire-your-seo-agency.git .claude/skills/fire-your-seo-agency
```

Claude Code에서:

```text
/fire-your-seo-agency 내 사이트 진단해줘
```

## v1.2 운영 계층

- `audit / plan / fix / verify / measure / full` 실행 모드
- 0~100 readiness score + confidence + BLOCKED/AT_RISK/READY/UNKNOWN 상태
- P0~P3 우선순위
- JSON Schema 기반 기계 가독 결과
- 기준선/후속 측정 저장 규약
- 회귀 테스트 12개

## 구조

```text
SKILL.md
references/
  evidence-policy.md   ← 근거 등급과 출처 정책
  crawlers.md          ← OpenAI·Anthropic·Perplexity·Naver 크롤러 구분
  seo.md
  aeo.md
  geo.md
  llmo.md
  neo-naver.md
  measure.md
  scoring.md
  execution.md
  output-contract.md
schemas/
  audit-result.schema.json
examples/
  audit-result.example.json
tests/
  scenarios.md
```

## 운영 철학

- 사람에게 유용한 콘텐츠가 우선
- 플랫폼별 공식 문서를 우선
- 1차 데이터와 독자적 가치를 선호
- 랭킹/트래픽/AI 인용을 보장하지 않음
- 기술 변경과 성과 개선을 분리
- 모르는 것은 모른다고 기록
- 측정 없는 성공 주장을 하지 않음

## 근거 기준일

주요 공식 정책 확인 기준일: **2026-08-27**

세부 출처는 `references/evidence-policy.md`와 각 레인 문서를 참조하세요.

## 원본 및 라이선스

Original: https://github.com/leopard627/fire-your-seo-agency

MIT License. 원저작자 고지와 라이선스 조건을 유지합니다.
