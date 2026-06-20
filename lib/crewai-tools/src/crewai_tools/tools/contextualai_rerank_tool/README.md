# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/contextualai_rerank_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/contextualai_rerank_tool/README.md`

## 한글 요약

ContextualAIRerankTool 설명 이 도구는 Reranker에 이어 CrewAI와 함께 Contextual AI의 엔터프라이즈급 지침을 통합하여 관련성 및 사용자 정의 기준에 따라 문서를 지능적으로 재정렬할 수 있도록 설계되었습니다. 이 도구를 사용하면 상황을 이해하고 최적의 문서 순서를 위한 특정 지침을 따르는 Contextual AI의 순위 재지정 모델을 사용하여 RAG 시스템에 대한 검색 결과 품질과 문서 검색을 향상할 수 있습니다. 설치 이 도구를 프로젝트에 통합하려면 아래 설치 지침을 따르십시오. 참고: Contextual AI API 키가 필요합니다. app.contextual.ai에 가입하여 무료 API 키를 받으세요. 예 결과에는 문서 순위가 ​​포함됩니다. 예: 매개변수 api 키: 상황별 AI API 키 쿼리: 문서 순위 재지정에 대한 검색 쿼리: 순위를 재지정할 문서 텍스트 목록 지침: 사용자 정의 기준에 대한 선택적 재순위 지침 메타데이터: 각 문서 모델에 대한 선택적 메타데이터: 재순위 모델(기본값: "ctxl rerank en v1)

## 핵심 발췌

instruct") 주요 기능 지침 재순위 지정: 도메인별 문서 순서 지정을 위한 사용자 지정 지침을 따릅니다. 메타데이터 통합: 향상된 순위 결정을 위해 문서 메타데이터를 통합합니다. 사용 사례 문서 컬렉션의 검색 결과 관련성 향상 사용자 지정 비즈니스 기준(최신성, 권한, 관련성)에 따라 문서 재정렬 연구 및 분석 워크플로를 위해 문서 필터링 및 우선 순위 지정 Contextual AI의 기능에 대한 자세한 내용은 공식 문서를 참조하세요.

## 원문 내용

# ContextualAIRerankTool

## Description
This tool is designed to integrate Contextual AI's enterprise-grade instruction-following reranker with CrewAI, enabling you to intelligently reorder documents based on relevance and custom criteria. Use this tool to enhance search result quality and document retrieval for RAG systems using Contextual AI's reranking models that understand context and follow specific instructions for optimal document ordering.

## Installation
To incorporate this tool into your project, follow the installation instructions below:

```shell
pip install 'crewai[tools]' contextual-client
```

**Note**: You'll need a Contextual AI API key. Sign up at [app.contextual.ai](https://app.contextual.ai) to get your free API key.

## Example

```python
from crewai_tools import ContextualAIRerankTool

tool = ContextualAIRerankTool(api_key="your_api_key_here")

result = tool._run(
    query="financial performance and revenue metrics",
    documents=[
        "Q1 report content with revenue data", 
        "Q2 report content with growth metrics", 
        "News article about market trends"
    ],
    instruction="Prioritize documents with specific financial metrics and quantitative data"
)
print(result)
```

The result will contain the document ranking. For example: 
```
Rerank Result:
{
  "results": [
    {
      "index": 1,
      "relevance_score": 0.88227631
    },
    {
      "index": 0,
      "relevance_score": 0.61159354
    },
    {
      "index": 2,
      "relevance_score": 0.28579462
    }
  ]
}
```

## Parameters
- `api_key`: Your Contextual AI API key
- `query`: Search query for reranking
- `documents`: List of document texts to rerank
- `instruction`: Optional reranking instruction for custom criteria
- `metadata`: Optional metadata for each document
- `model`: Reranker model (default: "ctxl-rerank-en-v1-instruct")

## Key Features
- **Instruction-Following Reranking**: Follows custom instructions for domain-specific document ordering
- **Metadata Integration**: Incorporates document metadata for enhanced ranking decisions

## Use Cases
- Improve search result relevance in document collections
- Reorder documents by custom business criteria (recency, authority, relevance)
- Filter and prioritize documents for research and analysis workflows

For more detailed information about Contextual AI's capabilities, visit the [official documentation](https://docs.contextual.ai).