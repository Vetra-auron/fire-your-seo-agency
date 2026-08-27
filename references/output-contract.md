# Output Contract — 사람이 읽는 보고 + 기계가 읽는 JSON

버전: 1.2

## 1. 사람용 보고 순서

1. 결론/상태
2. Readiness score + confidence
3. P0/P1 핵심 문제
4. 레인별 요약
5. 권고와 근거 등급
6. 구현/검증 결과
7. 모르는 것
8. 측정 계획
9. 롤백

## 2. JSON 산출물

정식 스키마:
`schemas/audit-result.schema.json`

최상위 필드:
- `schema_version`
- `run_id`
- `run_type`
- `generated_at`
- `target`
- `evidence_baseline_date`
- `summary`
- `scores`
- `findings`
- `baseline`
- `changes`
- `verification`
- `measurement_plan`
- `uncertainties`
- `sources`

## 3. Finding 최소 요건

모든 finding은 최소한 다음을 가진다.

```json
{
  "id": "SEO-001",
  "lane": "seo",
  "priority": "P1",
  "severity": "high",
  "evidence_level": "OFFICIAL",
  "title": "핵심 페이지 noindex",
  "observation": "무엇을 실제로 확인했는지",
  "recommendation": "무엇을 바꿀지",
  "verification": "바뀌었는지 어떻게 검증할지",
  "rollback": "문제가 생기면 어떻게 되돌릴지",
  "source_urls": []
}
```

## 4. 사실과 추론 분리

`observation`에는 관찰한 사실을 쓴다.

나쁜 예:
> llms.txt가 없어서 ChatGPT 인용이 안 된다.

좋은 예:
> /llms.txt가 404다. [EXPERIMENTAL] 이 파일은 일부 에이전트용 보조 인터페이스로 시험할 수 있지만 ChatGPT 인용 실패의 원인으로 단정할 수 없다.

## 5. 변경 기록

fix를 수행하지 않았다면 `changes: []`.

수행했다면:
- path/url
- before
- after
- reason
- evidence_level
- verification_status
- rollback

을 기록한다.

## 6. Sources

정책/플랫폼 동작을 근거로 권고할 때 공식 URL을 우선 기록한다.
사용자 사이트 자체의 URL은 `affected_urls` 또는 observation에 기록한다.

## 7. 버전 호환

스키마를 깨는 변경이면 `schema_version` major를 올린다.
필드 추가처럼 하위 호환이면 minor를 올린다.
