# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/csv_search_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/csv_search_tool/README.md`

## 한글 요약

CSVSearchTool 설명 이 도구는 CSV 파일 콘텐츠 내에서 RAG(Retrieval Augmented Generation) 검색을 수행하는 데 사용됩니다. 이를 통해 사용자는 지정된 CSV 파일의 내용에서 쿼리를 의미론적으로 검색할 수 있습니다. 이 기능은 기존 검색 방법이 비효율적일 수 있는 대규모 CSV 데이터 세트에서 정보를 추출하는 데 특히 유용합니다. CSVSearchTool을 포함하여 이름에 "검색"이 포함된 모든 도구는 다양한 데이터 소스를 검색하도록 설계된 RAG 도구입니다. 설치 Crewai 도구 패키지를 설치합니다. 예제 인수 csv : 검색하려는 CSV 파일의 경로입니다. 특정 CSV 파일 없이 도구가 초기화된 경우 이는 필수 인수입니다. 그렇지 않으면 선택 사항입니다. 사용자 정의 모델 및 임베딩 기본적으로 이 도구는 임베딩 및 요약 모두에 OpenAI를 사용합니다. 모델을 사용자 정의하려면 다음과 같이 구성 사전을 사용할 수 있습니다.

## 핵심 발췌

CSVSearchTool ## 설명 이 도구는 CSV 파일 콘텐츠 내에서 RAG(Retrieval Augmented Generation) 검색을 수행하는 데 사용됩니다. 사용자가 지정된 CS의 콘텐츠에서 쿼리를 의미론적으로 검색할 수 있습니다.

## 원문 내용

# CSVSearchTool

## Description

This tool is used to perform a RAG (Retrieval-Augmented Generation) search within a CSV file's content. It allows users to semantically search for queries in the content of a specified CSV file. This feature is particularly useful for extracting information from large CSV datasets where traditional search methods might be inefficient. All tools with "Search" in their name, including CSVSearchTool, are RAG tools designed for searching different sources of data.

## Installation

Install the crewai_tools package

```shell
pip install 'crewai[tools]'
```

## Example

```python
from crewai_tools import CSVSearchTool

# Initialize the tool with a specific CSV file. This setup allows the agent to only search the given CSV file.
tool = CSVSearchTool(csv='path/to/your/csvfile.csv')

# OR

# Initialize the tool without a specific CSV file. Agent  will need to provide the CSV path at runtime.
tool = CSVSearchTool()
```

## Arguments

- `csv` : The path to the CSV file you want to search. This is a mandatory argument if the tool was initialized without a specific CSV file; otherwise, it is optional.

## Custom model and embeddings

By default, the tool uses OpenAI for both embeddings and summarization. To customize the model, you can use a config dictionary as follows:

```python
tool = CSVSearchTool(
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