# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/directory_search_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/directory_search_tool/README.md`

## 한글 요약

DirectorySearchTool 설명 이 도구는 지정된 디렉터리의 내용 내에서 쿼리에 대한 의미 검색을 수행하도록 설계되었습니다. RAG(Retrieval Augmented Generation) 방법론을 활용하여 특정 디렉터리의 파일을 의미론적으로 탐색할 수 있는 강력한 수단을 제공합니다. 이 도구는 런타임에 지정된 디렉터리를 검색하도록 동적으로 설정하거나 초기화 시 특정 디렉터리 내에서 검색하도록 미리 구성할 수 있습니다. 설치 DirectorySearchTool 사용을 시작하려면 크루아이 도구 패키지를 설치해야 합니다. 터미널에서 다음 명령을 실행하십시오. 예 다음 예는 다양한 사용 사례에 대해 DirectorySearchTool을 초기화하는 방법과 검색을 수행하는 방법을 보여줍니다. 인수 디렉토리 : 이 문자열 인수는 검색할 디렉토리를 지정합니다. 도구가 디렉터리로 초기화되지 않은 경우 필수입니다. 그렇지 않으면 도구는 초기화된 디렉터리 내에서만 검색합니다. 사용자 정의 모델 및 임베드딘

## 핵심 발췌

gs 기본적으로 이 도구는 임베딩과 요약 모두에 OpenAI를 사용합니다. 모델을 사용자 정의하려면 다음과 같이 구성 사전을 사용할 수 있습니다.

## 원문 내용

# DirectorySearchTool

## Description
This tool is designed to perform a semantic search for queries within the content of a specified directory. Utilizing the RAG (Retrieval-Augmented Generation) methodology, it offers a powerful means to semantically navigate through the files of a given directory. The tool can be dynamically set to search any directory specified at runtime or can be pre-configured to search within a specific directory upon initialization.

## Installation
To start using the DirectorySearchTool, you need to install the crewai_tools package. Execute the following command in your terminal:

```shell
pip install 'crewai[tools]'
```

## Example
The following examples demonstrate how to initialize the DirectorySearchTool for different use cases and how to perform a search:

```python
from crewai_tools import DirectorySearchTool

# To enable searching within any specified directory at runtime
tool = DirectorySearchTool()

# Alternatively, to restrict searches to a specific directory
tool = DirectorySearchTool(directory='/path/to/directory')
```

## Arguments
- `directory` : This string argument specifies the directory within which to search. It is mandatory if the tool has not been initialized with a directory; otherwise, the tool will only search within the initialized directory.

## Custom model and embeddings

By default, the tool uses OpenAI for both embeddings and summarization. To customize the model, you can use a config dictionary as follows:

```python
tool = DirectorySearchTool(
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