# GEO — 생성형 검색·브라우징 가시성

확인 기준일: 2026-08-27

대상: ChatGPT Search, Perplexity, Claude 검색/브라우징 등 **외부 웹을 탐색해 출처를 제시할 수 있는 생성형 시스템**.

GEO는 하나의 표준화된 랭킹 규칙이 아니다. 플랫폼마다 크롤러, 검색 공급자, 인용 방식이 다르다.

## 1. 크롤러 정책

반드시 `references/crawlers.md`를 먼저 확인한다.

- [OFFICIAL] OpenAI의 `OAI-SearchBot`과 `GPTBot`은 목적이 다르다.
- [OFFICIAL] Anthropic도 검색/모델 개발/사용자 요청용 크롤러를 구분한다.
- [OFFICIAL] Perplexity의 검색 크롤러 정책은 별도로 확인한다.
- [OFFICIAL] 검색 노출을 허용할지와 모델 개발용 수집을 허용할지는 독립적으로 결정할 수 있는 경우가 있다.

## 2. llms.txt

- [OFFICIAL] Google Search는 생성형 AI 검색을 위해 llms.txt 같은 별도 AI 전용 파일이 필요하지 않다고 설명한다.
- [EXPERIMENTAL] llms.txt는 일부 에이전트·도구·사람에게 사이트 구조를 설명하는 보조 인터페이스로 테스트할 수 있다.
- [EXPERIMENTAL] llms.txt 존재 자체를 ChatGPT/Perplexity/Claude 인용의 직접 랭킹 신호로 주장하지 않는다.

선택적으로 제공한다면:
```markdown
# 서비스명
> 무엇을 제공하는 사이트인지

## 핵심 페이지
- [데이터 페이지](https://example.com/data): 설명

## 데이터 정책
- 원출처
- 갱신 주기
- 기준일
```

## 3. 1차 정보 전략

- [OFFICIAL] Google은 생성형 AI 검색에서도 고유하고 유용한 사람 중심 콘텐츠를 강조한다.
- [OBSERVED] 자체 조사·계산·데이터·도구·실험처럼 다른 사이트가 쉽게 복제할 수 없는 정보는 출처로서 차별화하기 쉽다.
- [OBSERVED] 숫자/사실에 기준일, 단위, 산식, 원출처를 붙이면 검증 가능한 정보가 된다.
- [EXPERIMENTAL] "AI는 정확한 데이터만 인용한다" 같은 절대 문장은 사용하지 않는다. 글의 품질·권위·관련성·시의성 등 다양한 요소가 함께 작동할 수 있다.

## 4. 검증

사전에 고정한 질문 세트로 각 플랫폼을 반복 측정한다.

확인 항목:
- 우리 도메인이 출처 목록에 등장하는가
- 어떤 URL이 선택됐는가
- 실제 내용이 정확히 반영됐는가
- 날짜/위치/계정에 따라 결과가 달라지는가
- 경쟁 출처는 무엇인가

## 5. 우선순위

1. 검색 크롤러 접근 정책
2. 기술 SEO와 색인 가능성
3. 독자적 가치/1차 정보
4. 명확한 출처·갱신 정보
5. 실제 질문 세트 측정
6. llms.txt 등 저비용 실험

출처:
- https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
- https://developers.openai.com/api/docs/bots
- https://docs.perplexity.ai/docs/resources/perplexity-crawlers
