# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/contextualai_query_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/contextualai_query_tool/README.md`

## 한글 요약

ContextualAIQueryTool 설명 이 도구는 Contextual AI의 엔터프라이즈급 RAG 에이전트를 CrewAI와 통합하도록 설계되었습니다. 이 도구를 실행하면 문서 및 지식 기반으로 사전 구성된 기존 Contextual AI RAG 에이전트를 쿼리할 수 있습니다. 설치 이 도구를 프로젝트에 통합하려면 아래 설치 지침을 따르십시오. 참고: Contextual AI API 키가 필요합니다. app.contextual.ai에 가입하여 무료 API 키를 받으세요. 예 이 도구를 사용하기 전에 이미 컨텍스트 에이전트를 생성하고 문서를 데이터 저장소에 수집했는지 확인하십시오. 결과에는 사용자 쿼리에 대해 생성된 답변이 포함됩니다. 매개변수 초기화: api key: 자신의 Contextual AI API 키 Query( run 메소드): query: 에이전트에 보낼 질문 또는 쿼리 Agent id: 쿼리할 기존 Contextual AI 에이전트의 ID(필수) datastore id: 문서 준비 확인을 위한 선택적 데이터 저장소 ID(제공하지 않을 경우 문서 상태 확인이 경고와 함께 비활성화됨) 주요 기능

## 핵심 발췌

문서 준비 확인: 쿼리하기 전에 문서가 처리될 때까지 자동으로 대기합니다. 근거 있는 응답: 기본 기반으로 사실 기반의 소스 기반 답변 보장 사용 사례 문서 컬렉션이 포함된 사전 구성된 RAG 에이전트 쿼리 사용자 쿼리를 통해 기업 지식 기반에 액세스 선별된 문서에 액세스할 수 있는 전문 도메인 전문가 구축 Contextual AI 기능에 대한 자세한 내용은 공식 문서를 참조하세요.

## 원문 내용

# ContextualAIQueryTool

## Description
This tool is designed to integrate Contextual AI's enterprise-grade RAG agents with CrewAI. Run this tool to query existing Contextual AI RAG agents that have been pre-configured with documents and knowledge bases.

## Installation
To incorporate this tool into your project, follow the installation instructions below:

```shell
pip install 'crewai[tools]' contextual-client
```

**Note**: You'll need a Contextual AI API key. Sign up at [app.contextual.ai](https://app.contextual.ai) to get your free API key.

## Example

Make sure you have already created a Contextual agent and ingested documents into the datastore before using this tool. 

```python
from crewai_tools import ContextualAIQueryTool

# Initialize the tool
tool = ContextualAIQueryTool(api_key="your_api_key_here")

# Query the agent with IDs
result = tool._run(
    query="What are the key findings in the financial report?",
    agent_id="your_agent_id_here",
    datastore_id="your_datastore_id_here"  # Optional: for document readiness checking
)
print(result)
```

The result will contain the generated answer to the user's query. 

## Parameters
**Initialization:**
- `api_key`: Your Contextual AI API key

**Query (_run method):**
- `query`: The question or query to send to the agent
- `agent_id`: ID of the existing Contextual AI agent to query (required)
- `datastore_id`: Optional datastore ID for document readiness verification (if not provided, document status checking is disabled with a warning)

## Key Features
- **Document Readiness Checking**: Automatically waits for documents to be processed before querying
- **Grounded Responses**: Built-in grounding ensures factual, source-attributed answers

## Use Cases
- Query pre-configured RAG agents with document collections
- Access enterprise knowledge bases through user queries
- Build specialized domain experts with access to curated documents

For more detailed information about Contextual AI's capabilities, visit the [official documentation](https://docs.contextual.ai).