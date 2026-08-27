# AI·검색 크롤러 정책

확인 기준일: 2026-08-27

크롤러를 "AI 봇" 하나로 묶지 않는다. **검색 노출용, 모델 개발/학습용, 사용자 요청용** 목적이 다르다.

## OpenAI

[OFFICIAL]

- `OAI-SearchBot`: ChatGPT 검색 결과에 사이트를 노출하기 위한 검색용 크롤러.
- `GPTBot`: 생성형 AI 기반 모델 개발에 사용할 수 있는 콘텐츠를 수집하는 크롤러.
- `ChatGPT-User`: 사용자 요청에 따라 페이지를 방문할 수 있는 사용자 액션용 에이전트. 자동 검색 색인용 봇이 아니다.

검색 노출은 허용하고 모델 학습은 원하지 않는 예:

```txt
User-agent: OAI-SearchBot
Allow: /

User-agent: GPTBot
Disallow: /
```

출처: https://developers.openai.com/api/docs/bots

## Anthropic

[OFFICIAL]

- `Claude-SearchBot`: Claude 검색 결과 품질/가시성 관련 검색용.
- `ClaudeBot`: 모델 개발용 웹 수집.
- `Claude-User`: 사용자 요청에 따른 웹 접근.

정책은 각각 독립적으로 판단한다.

출처: https://support.anthropic.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler

## Perplexity

[OFFICIAL]

- `PerplexityBot`: Perplexity 검색 결과에서 웹사이트를 발견하고 링크하기 위한 크롤러.
- 세부 사용자 에이전트와 정책은 공식 문서를 최신 확인한다.

출처: https://docs.perplexity.ai/docs/resources/perplexity-crawlers

## Naver

[OFFICIAL]

- `Yeti`: 네이버 검색 로봇.
- robots.txt 루트 배치와 접근 허용 정책을 확인한다.
- sitemap 위치를 robots.txt에 표시할 수 있다.

출처: https://searchadvisor.naver.com/guide/seo-basic-robots

## 운영 원칙

1. 기본 허용/차단을 무심코 복사하지 않는다. 사이트의 콘텐츠 전략과 법적/상업적 요구에 맞춘다.
2. 검색 노출과 모델 학습 옵트아웃을 별도 결정한다.
3. robots.txt 변경 후 즉시 효과를 가정하지 않는다.
4. 봇 이름과 정책은 바뀔 수 있으므로 자동화 템플릿에 "마지막 검증일"을 기록한다.
