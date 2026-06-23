# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/code_docs_search_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/code_docs_search_tool/README.md`

## 한글 요약

CodeDocsSearchTool 설명 CodeDocsSearchTool은 코드 문서 내의 의미 검색을 위해 설계된 강력한 RAG(Retrieval Augmented Generation) 도구입니다. 이를 통해 사용자는 코드 문서 내에서 특정 정보나 주제를 효율적으로 찾을 수 있습니다. 도구는 초기화 중에 문서 URL을 제공함으로써 검색 범위를 해당 특정 문서 사이트로 좁힙니다. 또는 특정 문서 URL 없이 실행 전반에 걸쳐 알려졌거나 발견된 광범위한 코드 문서를 검색하여 다양한 문서 검색 요구에 맞게 다용도로 사용할 수 있습니다. 설치 CodeDocsSearchTool 사용을 시작하려면 먼저 pip를 통해 크루아이 도구 패키지를 설치하십시오. 예 다음과 같이 CodeDocsSearchTool을 활용하여 코드 문서 내에서 검색을 수행하십시오. 참고: 'https://docs.example.com/reference'를 대상 문서 URL로 대체하고 '검색 도구 사용 방법'을 필요에 맞는 검색 쿼리로 대체하십시오. 인수 문서 URL: 선택사항. t의 URL을 지정합니다

## 핵심 발췌

그는 검색할 문서를 코딩합니다. 도구 초기화 중에 이를 제공하면 지정된 문서 콘텐츠에 대한 검색이 집중됩니다. 사용자 정의 모델 및 임베딩 기본적으로 이 도구는 임베딩 및 요약 모두에 OpenAI를 사용합니다. 모델을 사용자 정의하려면 다음과 같이 구성 사전을 사용할 수 있습니다.

## 원문 내용

# CodeDocsSearchTool

## Description
The CodeDocsSearchTool is a powerful RAG (Retrieval-Augmented Generation) tool designed for semantic searches within code documentation. It enables users to efficiently find specific information or topics within code documentation. By providing a `docs_url` during initialization, the tool narrows down the search to that particular documentation site. Alternatively, without a specific `docs_url`, it searches across a wide array of code documentation known or discovered throughout its execution, making it versatile for various documentation search needs.

## Installation
To start using the CodeDocsSearchTool, first, install the crewai_tools package via pip:
```shell
pip install 'crewai[tools]'
```

## Example
Utilize the CodeDocsSearchTool as follows to conduct searches within code documentation:
```python
from crewai_tools import CodeDocsSearchTool

# To search any code documentation content if the URL is known or discovered during its execution:
tool = CodeDocsSearchTool()

# OR

# To specifically focus your search on a given documentation site by providing its URL:
tool = CodeDocsSearchTool(docs_url='https://docs.example.com/reference')
```
Note: Substitute 'https://docs.example.com/reference' with your target documentation URL and 'How to use search tool' with the search query relevant to your needs.

## Arguments
- `docs_url`: Optional. Specifies the URL of the code documentation to be searched. Providing this during the tool's initialization focuses the search on the specified documentation content.

## Custom model and embeddings

By default, the tool uses OpenAI for both embeddings and summarization. To customize the model, you can use a config dictionary as follows:

```python
tool = CodeDocsSearchTool(
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