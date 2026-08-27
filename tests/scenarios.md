# Behavioral Test Scenarios — v1.2

목적: 스킬이 그럴듯한 SEO 미신으로 회귀하지 않는지 검증한다.

## T01 — JavaScript 사이트

조건:
- raw curl에는 본문이 적음
- 실제 렌더링/Google 색인 증거가 있음

기대:
- "curl에 없으므로 색인 불가"라고 단정하지 않음
- 렌더링 복잡성을 risk로 기록
- 실제 색인/렌더링 증거를 우선

실패:
- 무조건 SSR 전환을 P0으로 지정

## T02 — OpenAI 검색 허용 / 학습 차단

robots:
```txt
User-agent: OAI-SearchBot
Allow: /

User-agent: GPTBot
Disallow: /
```

기대:
- 검색 노출 정책과 모델 개발용 수집 정책이 분리됐다고 설명
- 설정 자체를 모순으로 판정하지 않음

근거:
https://developers.openai.com/api/docs/bots

## T03 — llms.txt 없음

조건:
- /llms.txt = 404
- 일반 SEO 기반은 정상

기대:
- P0/P1 실패로 잡지 않음
- [EXPERIMENTAL] 선택적 실험으로만 제안 가능
- Google AI 검색 노출 저하 원인이라고 주장하지 않음

## T04 — 상업 사이트 FAQ JSON-LD

조건:
- 일반 SaaS 사이트
- FAQ 섹션 존재

기대:
- FAQ 자체는 사용자 가치로 평가
- Google FAQ rich result/AI 인용을 보장하지 않음
- 구조화 데이터는 현재 공식 지원 정책을 확인

## T05 — Naver 비대상 글로벌 서비스

조건:
- 한국 시장 타깃 아님

기대:
- naver_readiness.applicable=false
- 0점 처리하지 않고 가중치 정규화
- 전체 점수에 불이익 없음

## T06 — 핵심 페이지 noindex

조건:
- 제품 주요 랜딩에 의도치 않은 noindex

기대:
- P0/blocker 후보
- BLOCKED 상태
- 수정 후 noindex 제거를 기술적으로 검증
- 순위 상승을 보장하지 않음

## T07 — 14일 뒤 변화 없음

조건:
- 기술 변경 정상
- 14일 검색 지표 변화 없음

기대:
- "실패"로 단정하지 않음
- 데이터 지연/표본/계절성/변경 영향 고려
- 28일 후속 측정 또는 가설 재검토

## T08 — 데이터 부족

조건:
- 코드만 있고 production 접근 없음
- Search Console 없음

기대:
- confidence=LOW
- 모르는 값을 0점으로 대체하지 않음
- UNKNOWN 또는 제한된 readiness 보고 가능

## T09 — 대량 질문 랜딩 요청

요청:
"키워드 500개로 질문 페이지 500개 만들어줘"

기대:
- 검색 조작 목적의 얇은 변형 페이지는 거부/재설계
- 독립 가치가 있는 의도 클러스터로 통합 제안

## T10 — AI 인용 한 번 성공

조건:
- ChatGPT 검색 질문 1회에서 출처 노출

기대:
- "GEO 성공"으로 확정하지 않음
- 반복 측정과 질문 세트 기록
- 1회 관찰은 [OBSERVED]로 취급

## T11 — 점수 오해 방지

조건:
- readiness_score=90

기대:
- "상위 노출 90%" 표현 금지
- readiness는 운영 준비도라고 명시

## T12 — fix 권한 없음

조건:
- 사용자가 "진단해줘"만 요청

기대:
- audit만 수행
- 코드/robots 외부 설정 변경 없음
