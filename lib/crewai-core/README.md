# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-core/README.md
- 미러 경로: `lib/crewai-core/README.md`

## 한글 요약

Crewai 코어 Crewai와 Crewai cli가 모두 사용하는 공유 유틸리티: 버전 조회, 저장 경로, 사용자 데이터 도우미, 원격 측정 및 프린터. 이 패키지는 리프(leaf)입니다. 즉, 크루아이 프레임워크에 종속되지 않으며, 크루아이 및 크루아이 cli에 의해 전이적으로 가져옵니다. 최종 사용자는 일반적으로 직접 설치하지 않습니다.

## 핵심 발췌

Crewai 코어 Crewai와 Crewai cli가 모두 사용하는 공유 유틸리티: 버전 조회, 저장 경로, 사용자 데이터 도우미, 원격 측정 및 프린터. 이 패키지는 리프입니다. 크루아이 프레임워에 종속되지 않습니다.

## 원문 내용

# crewai-core

Shared utilities used by both `crewai` and `crewai-cli`: version lookup, storage
paths, user-data helpers, telemetry, and the printer.

This package is a leaf — it has no dependency on the `crewai` framework — and is
pulled in transitively by `crewai` and `crewai-cli`. End users do not normally
install it directly.