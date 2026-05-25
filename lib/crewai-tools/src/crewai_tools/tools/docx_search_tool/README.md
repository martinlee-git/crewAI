# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/docx_search_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/docx_search_tool/README.md`

## 한글 요약

DOCXSearchTool 설명 DOCXSearchTool은 DOCX 문서 내에서 의미 검색을 위해 설계된 RAG 도구입니다. 사용자는 쿼리 기반 검색을 사용하여 DOCX 파일에서 관련 정보를 효과적으로 검색하고 추출할 수 있습니다. 이 도구는 데이터 분석, 정보 관리 및 연구 작업에 매우 중요하며 대규모 문서 컬렉션 내에서 특정 정보를 찾는 프로세스를 간소화합니다. 설치 터미널에서 다음 명령을 실행하여 크루아이 도구 패키지를 설치합니다. 예 다음 예에서는 DOCX 파일의 콘텐츠 내에서 또는 특정 DOCX 파일 경로를 사용하여 검색하도록 DOCXSearchTool을 초기화하는 방법을 보여줍니다. 인수 docx: 검색하려는 특정 DOCX 문서에 대한 선택적 파일 경로입니다. 초기화 중에 제공되지 않은 경우 도구를 사용하면 검색을 위해 DOCX 파일의 콘텐츠 경로를 나중에 지정할 수 있습니다. 사용자 정의 모델 및 임베딩 기본적으로 이 도구는 임베딩 및 요약 모두에 OpenAI를 사용합니다. 모델을 맞춤설정하려면 다음을 수행하세요.

## 핵심 발췌

n 다음과 같이 구성 사전을 사용하십시오.

## 원문 내용

# DOCXSearchTool

## Description
The DOCXSearchTool is a RAG tool designed for semantic searching within DOCX documents. It enables users to effectively search and extract relevant information from DOCX files using query-based searches. This tool is invaluable for data analysis, information management, and research tasks, streamlining the process of finding specific information within large document collections.

## Installation
Install the crewai_tools package by running the following command in your terminal:

```shell
pip install 'crewai[tools]'
```

## Example
The following example demonstrates initializing the DOCXSearchTool to search within any DOCX file's content or with a specific DOCX file path.

```python
from crewai_tools import DOCXSearchTool

# Initialize the tool to search within any DOCX file's content
tool = DOCXSearchTool()

# OR

# Initialize the tool with a specific DOCX file, so the agent can only search the content of the specified DOCX file
tool = DOCXSearchTool(docx='path/to/your/document.docx')
```

## Arguments
- `docx`: An optional file path to a specific DOCX document you wish to search. If not provided during initialization, the tool allows for later specification of any DOCX file's content path for searching.

## Custom model and embeddings

By default, the tool uses OpenAI for both embeddings and summarization. To customize the model, you can use a config dictionary as follows:

```python
tool = DOCXSearchTool(
    config=dict(
        llm=dict(
            provider="ollama", # or google, openai, anthropic, llama2, ...
            config=dict(
                model="llama2",
                # temperature=0.5,
                # top_p=1,
                # stream=true,
            ),
        ),
        embedder=dict(
            provider="google",
            config=dict(
                model="models/embedding-001",
                task_type="retrieval_document",
                # title="Embeddings",
            ),
        ),
    )
)
```