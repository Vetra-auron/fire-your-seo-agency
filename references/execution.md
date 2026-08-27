# Execution Contract — v1.2 실행 모드

이 스킬은 자연어 요청을 아래 실행 모드로 해석한다.
명령 파서가 있는 것처럼 가장하지 말고 **사용자의 의도**를 기준으로 한다.

## 1. audit

예:
```text
/fire-your-seo-agency audit https://example.com
```

행동:
- 읽기 전용
- 시장/사이트 유형 파악
- 핵심 URL 샘플링
- robots/sitemap/status/canonical/메타/구조화 데이터 확인
- AI 검색 크롤러 정책 확인
- Naver 적용 여부 판단
- readiness score + findings 생성
- 기준선 데이터가 없으면 "미측정"으로 기록

금지:
- 코드 변경
- robots.txt 수정
- 대량 페이지 생성

## 2. plan

행동:
- audit 결과를 P0~P3로 재정렬
- 각 항목에 evidence level, impact, effort, verification, rollback 작성
- 묶어서 적용할 변경과 독립 실험을 분리
- 성과 지표와 기술 검증 지표를 구분

## 3. fix

사용자가 명시적으로 수정/구현을 요청했거나 앞선 plan을 승인했을 때 사용한다.

행동:
- 가능한 작은 변경 단위로 구현
- 기존 프레임워크/코딩 규칙 존중
- 변경 전 관련 파일을 읽고 영향 범위 확인
- 변경마다 verification과 rollback 정의
- 실험 항목은 가능하면 feature flag/독립 커밋 등 되돌리기 쉬운 형태 선호

금지:
- 랭킹 보장을 이유로 대량 콘텐츠 생성
- 공식 근거 없는 설정을 필수값처럼 강제
- 외부 계정 설정을 사용자 승인 없이 변경

## 4. verify

배포/변경 후 기술 상태만 확인한다.

예:
- HTTP 상태
- robots
- sitemap
- canonical
- rendered/served content
- structured data
- 주요 링크
- 목표 크롤러 정책

출력은 "기술 검증 통과/실패"이며 성과 개선을 주장하지 않는다.

## 5. measure

기준선과 후속 데이터를 비교한다.

기본 창:
- 즉시: 기술 검증
- 약 14일: 초기 체크
- 약 28일: 검색 지표 비교
- 분기: 브랜드/엔티티/장기 AI 가시성

14/28일은 고정 효과 기간이 아니다.

## 6. full

`audit → plan → fix → verify → measurement plan` 순서.

단, 사용자가 수정 권한을 명시하지 않았다면 **audit + plan까지만 수행**하고 fix는 승인 대상으로 남긴다.

## 7. 산출물 저장 규약

대상 프로젝트에 파일 쓰기가 가능하면 선택적으로 다음에 저장한다.

```text
.search-visibility/
  runs/
    YYYYMMDD-HHMMSSZ-audit.json
    YYYYMMDD-HHMMSSZ-verify.json
  measurements/
    questions-v1.csv
    baseline-YYYYMMDD.json
    followup-YYYYMMDD.json
  experiments/
    EXP-001.md
```

주의:
- 저장 경로가 기존 프로젝트 규칙과 충돌하면 사용자 프로젝트 규칙을 우선한다.
- 비밀키, 인증토큰, 개인 검색어/개인정보를 로그에 저장하지 않는다.
- 산출물 저장이 필요 없으면 채팅 보고만 한다.

## 8. 실행 중단 조건

다음이면 추정으로 밀어붙이지 않고 상태를 UNKNOWN/blocked-by-access로 보고한다.
- 인증이 필요한 데이터에 접근 불가
- production과 staging을 구분할 수 없음
- 핵심 도메인/대상 시장을 잘못 식별할 위험이 큼
- 외부 계정 변경이 필요하지만 권한/승인이 없음
