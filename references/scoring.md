# Readiness Scoring — 운영 준비도 점수

버전: 1.2  
확인 기준일: 2026-08-27

이 점수는 **검색 순위 확률, 트래픽 증가율, AI 인용 확률을 예측하지 않는다.**
목적은 여러 문제를 같은 형식으로 정리하고, 무엇부터 고칠지 우선순위를 정하는 것이다.

## 1. 상태와 점수를 분리한다

최종 상태:
- **BLOCKED** — 핵심 목표 페이지에 명확한 접근/색인 차단요인이 있음
- **AT_RISK** — 치명적 차단은 아니지만 중요한 결함이 있음
- **READY** — 주요 기반이 갖춰짐. 성과를 보장하지 않음
- **UNKNOWN** — 자료가 부족해 판단 불가

Readiness score: 0~100

상태가 점수보다 우선한다. 예를 들어 점수가 80이어도 핵심 페이지가 noindex라면 상태는 BLOCKED다.

## 2. 기본 차원과 가중치

각 차원은 0~5점으로 평가한다.

| 차원 | 가중치 | 핵심 질문 |
|---|---:|---|
| Discoverability & Indexability | 25 | 핵심 페이지를 발견·접근·색인할 수 있는가 |
| Technical Semantics | 15 | 상태코드·canonical·메타·구조화 데이터가 일관적인가 |
| Content Value & Provenance | 20 | 독자적 가치·출처·기준일·방법론이 있는가 |
| AI Search Access | 15 | 검색용 AI 크롤러 정책과 출처 발견성이 의도에 맞는가 |
| Measurement & Observability | 15 | 기준선·로그·질문세트·후속 측정이 가능한가 |
| Naver Readiness | 10 | 한국 시장에서 Naver 기반이 갖춰졌는가 |

Naver가 대상 시장이 아니면 Naver 차원은 `applicable=false`로 제외하고,
**적용 가능한 가중치 합계를 100으로 정규화**한다.

공식:
```text
weighted_score = Σ(weight × dimension_score / 5)
readiness_score = round(weighted_score / Σ(applicable_weights) × 100)
```

## 3. 0~5 평가 기준

- **0**: 명확한 실패/차단
- **1**: 심각한 결함
- **2**: 여러 핵심 결함
- **3**: 기본은 갖췄으나 개선 필요
- **4**: 대부분 양호, 일부 개선
- **5**: 현재 확인 범위에서 양호
- **null**: 측정하지 못함

`null`을 0으로 바꾸지 않는다. 모르는 것과 실패한 것은 다르다.

## 4. BLOCKED 게이트

다음은 대상 페이지/목표와 실제로 관련 있을 때 BLOCKED 후보:
- 핵심 공개 페이지가 인증 장벽 뒤에 있음
- 핵심 페이지에 의도치 않은 noindex
- robots 정책이 목표 검색 크롤러 접근을 차단
- 핵심 URL이 지속적 5xx/잘못된 리다이렉트 루프
- canonical이 핵심 페이지를 엉뚱한 URL로 일관되게 넘김

단, 발견 즉시 단정하지 말고 **실제 목표·페이지 범위·플랫폼 동작을 확인**한다.

## 5. Confidence

점수에는 반드시 confidence를 붙인다.

### HIGH
- 라이브 사이트 검증
- 코드/설정 확인
- Search Console/Search Advisor/로그 등 1차 데이터 일부 확보
- 핵심 결과 재현 가능

### MEDIUM
- 라이브 사이트와 코드/설정 중 일부만 확인
- 운영 지표는 제한적

### LOW
- 정적 문서나 사용자 설명 중심
- 라이브 검증/로그/플랫폼 데이터 부족

## 6. Finding 우선순위

### P0 — Blocker
목표 달성을 직접 막는 기술 문제. 우선 확인/복구.

### P1 — High-value fix
[OFFICIAL] 근거가 강하고 영향이 크며 재현 가능한 문제.

### P2 — Improvement
중요하지만 즉각적인 차단은 아닌 개선.

### P3 — Experiment
[OBSERVED]/[EXPERIMENTAL] 기반의 저비용 검증 항목.

숫자 점수만으로 priority를 자동 결정하지 않는다. **severity + evidence + impact + effort + reversibility**를 함께 본다.

## 7. 점수 해석 금지 예

금지:
- "82점이므로 상위 10% SEO"
- "GEO 90점이라 ChatGPT 인용 가능성 90%"
- "14일 뒤 트래픽 +30% 예상"

허용:
- "Readiness 82/100, MEDIUM confidence. 색인 차단은 없지만 측정 기반과 원출처 신호가 약함."
