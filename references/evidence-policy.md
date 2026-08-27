# 근거 정책 — Evidence Policy

이 프로젝트의 핵심은 "좋아 보이는 SEO 팁"과 "확인된 사실"을 섞지 않는 것이다.

## 등급

### [OFFICIAL]
플랫폼이 현재 공식 문서에서 직접 설명하는 동작·요건·정책.

사용 규칙:
- 가능하면 출처 URL과 확인일을 함께 남긴다.
- 문서가 바뀔 수 있는 항목은 재검증한다.
- "권장"과 "필수"를 구분한다.

### [OBSERVED]
특정 사이트, 검색 결과, 로그, 실험에서 실제 관찰된 패턴.

사용 규칙:
- 표본, 기간, 조건을 명시한다.
- 인과관계라고 단정하지 않는다.
- 다른 업종/엔진에 그대로 일반화하지 않는다.

### [EXPERIMENTAL]
공식 확인이 없거나 효과가 불명확하지만 테스트할 가치가 있는 가설.

사용 규칙:
- 구현 비용과 기대효과를 작게 잡는다.
- 반드시 검증 지표와 롤백 조건을 함께 둔다.
- 공식 문서와 충돌하면 폐기한다.

## 현재 기준의 핵심 공식 출처

확인 기준일: 2026-08-27

- Google 생성형 AI 검색 가이드  
  https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
- Google 검색 스니펫/메타 설명  
  https://developers.google.com/search/docs/appearance/snippet
- Google 구조화 데이터 일반 가이드  
  https://developers.google.com/search/docs/appearance/structured-data/sd-policies
- OpenAI crawlers  
  https://developers.openai.com/api/docs/bots
- Anthropic web crawlers  
  https://support.anthropic.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler
- Perplexity crawlers  
  https://docs.perplexity.ai/docs/resources/perplexity-crawlers
- Naver Search Advisor  
  https://searchadvisor.naver.com/guide
- IndexNow  
  https://www.indexnow.org/

## 충돌 해결 순서

1. 최신 공식 문서
2. 실제 사이트/로그에서 재현 가능한 관찰
3. 업계 관행
4. 개인 경험/추정

## 보고 예시

- [OFFICIAL] Google은 meta description 길이에 고정 문자 제한을 두지 않는다.
- [OFFICIAL] OAI-SearchBot과 GPTBot은 목적이 다르며 robots.txt 정책을 독립적으로 설정할 수 있다.
- [OBSERVED] 특정 데이터 페이지에서 기준일·출처·수치를 명시한 뒤 AI 검색 출처 노출이 증가했다.
- [EXPERIMENTAL] llms.txt를 다른 에이전트/도구용 사이트 안내서로 제공하고 로그 변화 여부를 관찰한다.
