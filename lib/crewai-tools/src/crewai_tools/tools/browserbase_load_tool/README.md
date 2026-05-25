# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/browserbase_load_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/browserbase_load_tool/README.md`

## 한글 요약

BrowserbaseLoadTool 설명 Browserbase는 헤드리스 브라우저를 안정적으로 실행, 관리 및 모니터링하는 개발자 플랫폼입니다. 다음을 통해 AI 데이터 검색 기능을 강화하십시오. 복잡한 UI에서 데이터를 추출하기 위해 신뢰할 수 있는 브라우저를 제공하는 서버리스 인프라 핑거프린팅 전략 및 자동 보안 문자 해결이 포함된 스텔스 모드 네트워크 타임라인 및 로그로 브라우저 세션을 검사하는 세션 디버거 자동화를 빠르게 디버그하기 위한 라이브 디버그 설치 browserbase.com에서 API 키와 프로젝트 ID를 가져와 환경 변수(BROWSERBASE API KEY, BROWSERBASE PROJECT ID)에 설정합니다. Crewai[tools] 패키지와 함께 Browserbase SDK를 설치합니다. 예 에이전트가 웹 사이트를 로드할 수 있도록 다음과 같이 BrowserbaseLoadTool을 활용합니다. 인수 api key 선택 사항입니다. 브라우저베이스 API 키. 기본값은 BROWSERBASE API KEY 환경 변수입니다. 프로젝트 ID 선택사항. 브라우저베이스 프로젝트 ID. 기본값은 BROWSERBASE PROJECT ID 환경 변수입니다. 텍스트 콘텐츠 텍스트 콘텐츠만 검색합니다. 기본값은 거짓입니다. 세션

## 핵심 발췌

이온 ID 선택사항입니다. 기존 세션 ID를 제공하세요. 프록시 선택사항. 프록시를 활성화/비활성화합니다."

## 원문 내용

# BrowserbaseLoadTool

## Description

[Browserbase](https://browserbase.com) is a developer platform to reliably run, manage, and monitor headless browsers.

 Power your AI data retrievals with:
 - [Serverless Infrastructure](https://docs.browserbase.com/under-the-hood) providing reliable browsers to extract data from complex UIs
 - [Stealth Mode](https://docs.browserbase.com/features/stealth-mode) with included fingerprinting tactics and automatic captcha solving
 - [Session Debugger](https://docs.browserbase.com/features/sessions) to inspect your Browser Session with networks timeline and logs
 - [Live Debug](https://docs.browserbase.com/guides/session-debug-connection/browser-remote-control) to quickly debug your automation

## Installation

- Get an API key and Project ID from [browserbase.com](https://browserbase.com) and set it in environment variables (`BROWSERBASE_API_KEY`, `BROWSERBASE_PROJECT_ID`).
- Install the [Browserbase SDK](http://github.com/browserbase/python-sdk) along with `crewai[tools]` package:

```
pip install browserbase 'crewai[tools]'
```

## Example

Utilize the BrowserbaseLoadTool as follows to allow your agent to load websites:

```python
from crewai_tools import BrowserbaseLoadTool

tool = BrowserbaseLoadTool()
```

## Arguments

- `api_key` Optional. Browserbase API key. Default is `BROWSERBASE_API_KEY` env variable.
- `project_id` Optional. Browserbase Project ID. Default is `BROWSERBASE_PROJECT_ID` env variable.
- `text_content` Retrieve only text content. Default is `False`.
- `session_id` Optional. Provide an existing Session ID.
- `proxy` Optional. Enable/Disable Proxies."