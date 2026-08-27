# SEO — 기술 기반 체크리스트

확인 기준일: 2026-08-27

목표는 검색엔진이 사이트를 **발견·크롤링·렌더링·색인·이해**할 수 있게 만드는 것이다.
특정 기술(SSR, JSON-LD 등)을 목적 그 자체로 취급하지 않는다.

## 1. 크롤링·색인 가능성

- [OFFICIAL] 핵심 공개 페이지가 로그인·권한 장벽 없이 접근 가능한지 확인한다.
- [OFFICIAL] robots.txt, meta robots, HTTP 상태 코드가 의도와 일치하는지 확인한다.
- [OFFICIAL] 사이트맵에는 색인시키고 싶은 canonical URL을 넣고 실제 상태와 동기화한다.
- [OFFICIAL] Google은 JavaScript를 렌더링할 수 있으므로 "curl에 본문이 없으면 색인 불가"라고 단정하지 않는다.
- [OBSERVED] JS 의존성이 높을수록 렌더링 지연·오류·디버깅 복잡성이 커질 수 있으므로 핵심 콘텐츠의 서버/정적 렌더링을 우선 검토한다.

검증 예:
```bash
curl -sIL https://example.com
curl -sL https://example.com/robots.txt
curl -sL https://example.com/sitemap.xml | head
```

## 2. URL·상태 코드·중복

- [OFFICIAL] 없는 페이지는 적절한 404/410을 반환한다.
- [OFFICIAL] 중복/유사 URL에는 canonical을 일관되게 사용한다.
- [OFFICIAL] 영구 이동은 적절한 301/308을 사용하고 불필요한 리다이렉트 체인을 줄인다.
- [OFFICIAL] 다국어 페이지는 실제 대체 관계에 맞게 hreflang을 구성한다.
- [OBSERVED] CDN/ISR에서 일시 오류가 404로 캐시되면 장시간 잘못된 응답이 남을 수 있으므로 "없음"과 "일시 실패"를 구분한다.

## 3. 내부 링크·사이트 구조

- [OFFICIAL] 중요한 페이지가 정상적인 `<a href>` 링크를 통해 발견 가능하게 한다.
- [OFFICIAL] 핵심 페이지가 지나치게 깊게 묻히지 않도록 정보 구조를 설계한다.
- [OBSERVED] 목록/필터만 있고 상세 페이지로의 안정적 내부 링크가 없으면 발견성이 약해지기 쉽다.

## 4. 제목·메타 설명

- [OFFICIAL] 페이지마다 내용에 맞는 고유하고 설명적인 title을 사용한다.
- [OFFICIAL] meta description은 검색 결과 스니펫 후보로 사용될 수 있지만 Google이 다른 본문을 선택할 수 있다.
- [OFFICIAL] Google은 meta description에 고정 문자 수 제한을 두지 않는다.
- [EXPERIMENTAL] 50~60자 title, 150~160자 description 같은 숫자는 미리보기 품질을 위한 휴리스틱으로만 사용한다.

숫자 규칙보다 **검색 의도·명확성·중복 방지**를 우선한다.

## 5. 구조화 데이터

- [OFFICIAL] 실제 페이지 유형과 Google이 지원하는 기능에 맞는 schema만 사용한다.
- [OFFICIAL] 구조화 데이터가 가시 콘텐츠를 오해하게 만들거나 존재하지 않는 내용을 표현하지 않게 한다.
- [OFFICIAL] Rich Results Test와 schema.org validator로 문법/지원 여부를 확인한다.
- [OFFICIAL] 구조화 데이터는 노출 자격을 도울 수 있지만 rich result나 순위를 보장하지 않는다.

## 6. 사이트맵

- [OFFICIAL] sitemap.xml 또는 sitemap index를 사용하고 robots.txt에서 위치를 알릴 수 있다.
- [OFFICIAL] sitemap 한 파일의 공식 한도(50,000 URL / 압축 전 50MB)를 넘으면 분할한다.
- [OBSERVED] 신규 콘텐츠 유형이 사이트맵 생성 로직에서 빠지는 운영 사고가 흔하므로 배포 체크에 포함한다.

## 7. 성능·모바일·사용성

- [OFFICIAL] 모바일 환경에서 주요 콘텐츠와 기능이 정상 동작하게 한다.
- [OFFICIAL] Core Web Vitals와 실제 사용자 경험을 함께 본다.
- [OBSERVED] 이미지 크기, 폰트, 과도한 클라이언트 JS가 LCP/INP/CLS 악화의 주요 원인이 되는 경우가 많다.

## 8. IndexNow

- [OFFICIAL] IndexNow 지원 엔진에는 URL 변경 알림을 자동화할 수 있다.
- [OFFICIAL] Google은 IndexNow를 사용하지 않는다.
- [OFFICIAL] Naver의 지원 여부와 구체적 동작은 IndexNow 공식 참여 목록을 최신 확인한다.

## 우선순위

1. 막힌 크롤링/색인
2. 잘못된 상태 코드·canonical
3. 내부 링크·사이트맵 누락
4. 제목/스니펫 품질
5. 지원되는 구조화 데이터
6. 성능·UX
7. 실험적 최적화

출처:
- https://developers.google.com/search/docs
- https://developers.google.com/search/docs/appearance/snippet
- https://developers.google.com/search/docs/appearance/structured-data/sd-policies
- https://www.indexnow.org/
