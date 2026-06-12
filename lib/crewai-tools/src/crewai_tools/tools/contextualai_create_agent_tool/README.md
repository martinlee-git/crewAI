# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/contextualai_create_agent_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/contextualai_create_agent_tool/README.md`

## 한글 요약

ContextualAICreateAgentTool 설명 이 도구는 Contextual AI의 엔터프라이즈급 RAG 에이전트를 CrewAI와 통합하도록 설계되었습니다. 이 도구를 사용하면 새로운 상황별 RAG 에이전트를 생성할 수 있습니다. 문서를 업로드하여 데이터 저장소를 생성하고 상황별 에이전트 ID와 데이터 저장소 ID를 반환합니다. 설치 이 도구를 프로젝트에 통합하려면 아래 설치 지침을 따르십시오. 참고: Contextual AI API 키가 필요합니다. app.contextual.ai에 가입하여 무료 API 키를 받으세요. 예제 매개변수 api 키: Contextual AI API 키 에이전트 이름: 새 에이전트 이름 에이전트 설명: 에이전트 목적 설명 데이터 저장소 이름: 문서 데이터 저장소 이름 문서 경로: 업로드할 파일 경로 목록 예제 결과: 반환된 ID와 함께 ContextualAIQueryTool을 사용하여 기술 자료를 쿼리하고 문서에서 관련 정보를 검색할 수 있습니다. 주요 기능 완벽한 파이프라인 설정 : 데이터 저장소 생성, 문서 업로드, 에이전트 구성을 한 번의 작업으로 완료

## 핵심 발췌

문서 처리: Contextual AI의 강력한 파서를 활용하여 복잡한 PDF 및 문서 수집 벡터 저장: 대규모 문서 컬렉션을 위해 Contextual AI의 데이터 저장소 사용 사용 사례 완전한 자동화를 통해 처음부터 새로운 RAG 에이전트 설정 문서 컬렉션을 구조화된 데이터 저장소에 업로드 및 구성 법률, 금융, 기술 또는 연구 워크플로우를 위한 전문 도메인 에이전트 생성 Contextual AI의 기능에 대한 자세한 내용은 공식 문서를 참조하세요.

## 원문 내용

# ContextualAICreateAgentTool

## Description
This tool is designed to integrate Contextual AI's enterprise-grade RAG agents with CrewAI. This tool enables you to create a new Contextual RAG agent. It uploads your documents to create a datastore and returns the Contextual agent ID and datastore ID.

## Installation
To incorporate this tool into your project, follow the installation instructions below:

```
pip install 'crewai[tools]' contextual-client
```

**Note**: You'll need a Contextual AI API key. Sign up at [app.contextual.ai](https://app.contextual.ai) to get your free API key.

## Example

```python
from crewai_tools import ContextualAICreateAgentTool

# Initialize the tool
tool = ContextualAICreateAgentTool(api_key="your_api_key_here")

# Create agent with documents
result = tool._run(
    agent_name="Financial Analysis Agent",
    agent_description="Agent for analyzing financial documents",
    datastore_name="Financial Reports",
    document_paths=["/path/to/report1.pdf", "/path/to/report2.pdf"],
)
print(result)
```

## Parameters
- `api_key`: Your Contextual AI API key
- `agent_name`: Name for the new agent
- `agent_description`: Description of the agent's purpose
- `datastore_name`: Name for the document datastore
- `document_paths`: List of file paths to upload

Example result: 

```
Successfully created agent 'Research Analyst' with ID: {created_agent_ID} and datastore ID: {created_datastore_ID}. Uploaded 5 documents.
```

You can use `ContextualAIQueryTool` with the returned IDs to query the knowledge base and retrieve relevant information from your documents.

## Key Features
- **Complete Pipeline Setup**: Creates datastore, uploads documents, and configures agent in one operation
- **Document Processing**: Leverages Contextual AI's powerful parser to ingest complex PDFs and documents
- **Vector Storage**: Use Contextual AI's datastore for large document collections

## Use Cases
- Set up new RAG agents from scratch with complete automation
- Upload and organize document collections into structured datastores
- Create specialized domain agents for legal, financial, technical, or research workflows

For more detailed information about Contextual AI's capabilities, visit the [official documentation](https://docs.contextual.ai).