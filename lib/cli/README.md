# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/cli/README.md
- 미러 경로: `lib/cli/README.md`

## 한글 요약

CrewAI용 크루아이 cli CLI — 전체 프레임워크를 설치하지 않고도 AI 에이전트 크루를 스캐폴드, 실행, 배포 및 관리합니다. 설치 Crewai 코어(공유 유틸리티)는 가져오지만 Crewai 프레임워크 자체는 가져오지 않으므로 크루 로드가 필요하지 않은 명령(crewai 버전, Crewai 로그인, Crewai 조직 목록, Crewai 구성, Crewai Traces, Crewai Create, Crewai 템플릿)은 독립형으로 작동합니다. 사용자의 크루 또는 흐름(crewai run, Crewai train, Crewai 테스트, Crewai 채팅, Crewai 재생, Crewai 재설정 메모리, Crewai 배포 푸시, Crewai 도구 게시)을 로드하는 명령을 사용하려면 Crewai를 프로젝트 환경에 설치해야 합니다. 누락된 경우 명확한 오류를 인쇄합니다. 두 가지를 동시에 설치하려면:

## 핵심 발췌

CrewAI용 크루아이 cli CLI — 전체 프레임워크를 설치하지 않고도 AI 에이전트 크루를 스캐폴드, 실행, 배포 및 관리합니다. ## 설치 이것은 크루아이 코어(공유 유틸리티) b를 가져옵니다.

## 원문 내용

# crewai-cli

CLI for CrewAI — scaffold, run, deploy and manage AI agent crews without
installing the full framework.

## Installation

```bash
pip install crewai-cli
```

This pulls in `crewai-core` (shared utilities) but not the `crewai` framework
itself, so commands that don't need a crew loaded — `crewai version`,
`crewai login`, `crewai org list`, `crewai config *`, `crewai traces *`,
`crewai create`, `crewai template *` — work standalone.

Commands that load a user's crew or flow (`crewai run`, `crewai train`,
`crewai test`, `crewai chat`, `crewai replay`, `crewai reset-memories`,
`crewai deploy push`, `crewai tool publish`) require `crewai` to be installed
in the project's environment. They print a clear error if it is missing.

To install both at once:

```bash
pip install crewai[cli]
```