# AEO — 답변형 검색 가시성

확인 기준일: 2026-08-27

이 문서는 Google AI Overviews/AI Mode, Bing 계열 답변 경험처럼 **검색 결과 안에서 생성형 답변이 제공되는 상황**을 다룬다.

핵심 원칙: **AEO를 별도의 비밀 알고리즘으로 취급하지 않는다.**
Google은 생성형 AI 검색에도 기존 Search 기본 원칙과 사람에게 유용하고 고유한 콘텐츠를 강조한다.

## 1. 콘텐츠 구조

- [OFFICIAL] 페이지의 주제와 목적을 명확하게 하고 사람에게 실질적 가치를 제공한다.
- [OFFICIAL] 검색엔진만을 위해 유사 질문 페이지를 대량 생성하지 않는다.
- [OBSERVED] 사용자가 찾는 핵심 답을 페이지 초반에 명확히 제시하면 사람과 시스템 모두 이해하기 쉬운 경우가 많다.
- [EXPERIMENTAL] "첫 답변 40자", "질문 하나 = 페이지 하나" 같은 고정 규칙은 테스트 가설일 뿐 보편 요건이 아니다.

전용 페이지는 다음 조건을 모두 만족할 때 만든다:
1. 의도가 독립적이고,
2. 별도 페이지가 실제 가치를 제공하며,
3. 기존 페이지와 실질적으로 중복되지 않는다.

## 2. 인용·요약에 유리한 정보 품질

- [OFFICIAL] 정확성, 원출처, 작성/갱신 정보, 명확한 근거를 우선한다.
- [OBSERVED] 수치에는 기준일·단위·산출 방식·원출처를 함께 제공하면 검증과 재사용이 쉬워진다.
- [OBSERVED] 표·목록·짧은 정의처럼 구조화된 표현은 복잡한 산문보다 정보를 빠르게 파악하기 쉬울 수 있다.
- [EXPERIMENTAL] 특정 문단 길이나 문장 형식이 AI 인용을 직접 올린다고 단정하지 않는다.

## 3. FAQ와 구조화 데이터

- [OFFICIAL] FAQ 섹션은 사용자에게 실제 도움이 될 때 사용한다.
- [OFFICIAL] FAQPage structured data의 Google rich result 자격은 제한적이며 모든 사이트가 FAQ rich result를 받는 것이 아니다.
- [OFFICIAL] structured data는 가시 콘텐츠와 일치해야 한다.
- [EXPERIMENTAL] FAQ JSON-LD 자체를 AI 인용 상승 요인으로 간주하지 않는다.

## 4. 실험 설계

질문 세트를 미리 고정한다.

예:
- 브랜드/서비스 설명 질문
- 비교 질문
- 날짜/수치 질문
- 추천/선택 질문

각 질문에 대해 기록:
```text
질문:
엔진:
날짜:
우리 도메인 노출: Y/N
직접 인용: Y/N
경쟁 출처:
메모:
```

한두 번의 결과를 인과관계로 일반화하지 않는다.

## 5. 하지 말 것

- 검색 의도만 바꿔 수백 개의 얇은 변형 페이지 생성
- AI가 좋아할 것이라는 이유로 문장을 기계적으로 잘게 쪼개기
- 허위 FAQ/평점/전문성 신호 만들기
- "AI 인용 보장" 표현

출처:
- https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
- https://developers.google.com/search/docs/appearance/structured-data/faqpage
