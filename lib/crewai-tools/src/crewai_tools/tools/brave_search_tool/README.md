# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/brave_search_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/brave_search_tool/README.md`

## 한글 요약

BraveSearchTool 문서 설명 이 도구는 인터넷의 텍스트 콘텐츠에서 지정된 쿼리에 대한 웹 검색을 수행하도록 설계되었습니다. Brave Search를 쿼리하고 웹에서 검색 결과를 가져오는 REST API인 Brave Web Search API를 활용합니다. 다음 섹션에서는 Brave Web Search API에 대한 매개변수 및 헤더를 포함한 요청을 선별하고 JSON 응답을 다시 받는 방법을 설명합니다. 설치 이 도구를 프로젝트에 통합하려면 아래 설치 지침을 따르십시오. 예 다음 예는 도구를 초기화하고 주어진 쿼리로 검색을 실행하는 방법을 보여줍니다. 시작하기 단계 BraveSearchTool을 효과적으로 사용하려면 다음 단계를 따르십시오. 1. 패키지 설치 : 크루아이[tools] 패키지가 Python 환경에 설치되어 있는지 확인합니다. 2. API 키 취득 : 여기에서 API 키를 취득하세요. 3. 환경 구성 : 획득한 API 키를 BRAVE API KEY라는 환경 변수에 저장하여 사용자가 쉽게 사용할 수 있도록 합니다.

## 핵심 발췌

전자 도구. 결론 BraveSearchTool을 Python 프로젝트에 통합함으로써 사용자는 애플리케이션에서 직접 인터넷을 통해 실시간 관련 검색을 수행할 수 있는 능력을 얻게 됩니다. 제공된 설정 및 사용 지침을 준수하면 이 도구를 프로젝트에 간단하고 간단하게 통합할 수 있습니다.

## 원문 내용

# BraveSearchTool Documentation

## Description
This tool is designed to perform a web search for a specified query from a text's content across the internet. It utilizes the Brave Web Search API, which is a REST API to query Brave Search and get back search results from the web. The following sections describe how to curate requests, including parameters and headers, to Brave Web Search API and get a JSON response back.

## Installation
To incorporate this tool into your project, follow the installation instructions below:
```shell
pip install 'crewai[tools]'
```

## Example
The following example demonstrates how to initialize the tool and execute a search with a given query:

```python
from crewai_tools import BraveSearchTool

# Initialize the tool for internet searching capabilities
tool = BraveSearchTool()
```

## Steps to Get Started
To effectively use the `BraveSearchTool`, follow these steps:

1. **Package Installation**: Confirm that the `crewai[tools]` package is installed in your Python environment.
2. **API Key Acquisition**: Acquire a API key [here](https://api.search.brave.com/app/keys).
3. **Environment Configuration**: Store your obtained API key in an environment variable named `BRAVE_API_KEY` to facilitate its use by the tool.

## Conclusion
By integrating the `BraveSearchTool` into Python projects, users gain the ability to conduct real-time, relevant searches across the internet directly from their applications. By adhering to the setup and usage guidelines provided, incorporating this tool into projects is streamlined and straightforward.