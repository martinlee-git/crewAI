# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/exa_tools/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/exa_tools/README.md`

## 한글 요약

ExaSearchTool 문서 설명 이 도구를 사용하면 CrewAI 에이전트가 가장 빠르고 정확한 웹 검색 API인 Exa를 사용하여 웹을 검색할 수 있습니다. 기본적으로 이 도구는 모든 쿼리에 대해 가장 관련성이 높은 결과의 토큰 효율적 하이라이트를 반환합니다. 전체 페이지 콘텐츠를 선택할 수도 있습니다. 설치 이 도구를 프로젝트에 통합하려면 아래 설치 지침을 따르십시오. 예 다음 예는 도구를 초기화하고 검색을 실행하는 방법을 보여줍니다. 시작하기 ExaSearchTool을 효과적으로 사용하려면 다음 단계를 따르십시오. 1. 패키지 설치 : 크루아이[tools] 패키지가 Python 환경에 설치되어 있는지 확인합니다. 2. API 키 획득 : Exa 대시보드에서 Exa API 키를 가져옵니다. 3. 환경 구성: 도구가 자동으로 선택할 수 있도록 EXA API KEY라는 환경 변수에 API 키를 저장합니다. 하이라이트와 전체 콘텐츠 중에서 선택하는 방법에 대한 자세한 내용은 Exa 검색 모범 사례를 참조하세요. 참고 EXASearchTool은 더 이상 사용되지 않는 별칭입니다.

## 핵심 발췌

r ExaSearchTool. 기존 가져오기는 계속 작동하지만 지원 중단 경고를 표시합니다. ExaSearchTool로 마이그레이션하세요.

## 원문 내용

# ExaSearchTool Documentation

## Description
This tool lets CrewAI agents search the web using [Exa](https://exa.ai/), the fastest and most accurate web search API. By default the tool returns token-efficient highlights of the most relevant results for any query; you can also opt in to full page content.

## Installation
To incorporate this tool into your project, follow the installation instructions below:
```shell
uv add crewai[tools] exa_py
```

## Example
The following example demonstrates how to initialize the tool and run a search:

```python
from crewai_tools import ExaSearchTool

# Default: results with token-efficient highlights
tool = ExaSearchTool(api_key="your_api_key", highlights=True)
```

## Steps to Get Started
To effectively use the `ExaSearchTool`, follow these steps:

1. **Package Installation**: Confirm that the `crewai[tools]` package is installed in your Python environment.
2. **API Key Acquisition**: Get an Exa API key from the [Exa dashboard](https://dashboard.exa.ai/api-keys).
3. **Environment Configuration**: Store your API key in an environment variable named `EXA_API_KEY` so the tool can pick it up automatically.

For details on choosing between highlights and full content, see the [Exa search best practices](https://exa.ai/docs/reference/search-best-practices).

## Note
`EXASearchTool` is a deprecated alias for `ExaSearchTool`. Existing imports continue to work but emit a deprecation warning; please migrate to `ExaSearchTool`.