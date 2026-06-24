# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/aws/bedrock/knowledge_base/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/aws/bedrock/knowledge_base/README.md`

## 한글 요약

BedrockKBRetrieverTool BedrockKBRetrieverTool을 사용하면 CrewAI 에이전트가 자연어 쿼리를 사용하여 Amazon Bedrock 기술 자료에서 정보를 검색할 수 있습니다. 설치 요구 사항 구성된 AWS 자격 증명(환경 변수 또는 AWS CLI를 통해) boto3 및 python dotenv 패키지 Amazon Bedrock 기술 자료 사용에 대한 액세스 CrewAI 에이전트와 함께 도구를 사용하는 방법은 다음과 같습니다. 도구 인수 | 인수 | 유형 | 필수 | 기본값 | 설명 | | | | | | | | 지식 베이스 ID | str | 예 | 없음 | 지식 베이스의 고유 식별자(0 10 영숫자) | | 결과 수 | 정수 | 아니요 | 5 | 반환할 최대 결과 수 | | 검색 구성 | 사전 | 아니요 | 없음 | 기술 자료 쿼리에 대한 사용자 정의 구성 | | 가드레일 구성 | 사전 | 아니요 | 없음 | 콘텐츠 필터링 설정 | | 다음 토큰 | str | 아니요 | 없음 | 페이지 매김을 위한 토큰 | 환경 변수 응답 형식 도구는 JSON 형식으로 결과를 반환합니다. 고급 사용법 Custo

## 핵심 발췌

m 검색 구성 지원되는 데이터 소스 Amazon S3 Confluence Salesforce SharePoint 웹 페이지 사용자 정의 문서 위치 Amazon Kendra SQL 데이터베이스 사용 사례 엔터프라이즈 지식 통합 CrewAI 에이전트가 민감한 데이터를 노출하지 않고 조직의 독점 지식에 액세스할 수 있도록 에이전트가 회사의 특정 정책, 절차 및 문서에 따라 결정을 내릴 수 있도록 허용 데이터 보안을 유지하면서 내부 문서를 기반으로 질문에 답할 수 있는 에이전트 생성 전문 도메인 지식 모델 재교육 없이 도메인별 지식 기반(법률, 의료, 기술)에 CrewAI 에이전트 연결 기존 활용 귀하의 AWS 환경에서 이미 유지관리되고 있는 지식 저장소 CrewAI의 추론과 도메인별 추론을 결합합니다.

## 원문 내용

# BedrockKBRetrieverTool

The `BedrockKBRetrieverTool` enables CrewAI agents to retrieve information from Amazon Bedrock Knowledge Bases using natural language queries.

## Installation

```bash
pip install 'crewai[tools]'
```

## Requirements

- AWS credentials configured (either through environment variables or AWS CLI)
- `boto3` and `python-dotenv` packages
- Access to Amazon Bedrock Knowledge Base

## Usage

Here's how to use the tool with a CrewAI agent:

```python
from crewai import Agent, Task, Crew
from crewai_tools.aws.bedrock.knowledge_base.retriever_tool import BedrockKBRetrieverTool

# Initialize the tool
kb_tool = BedrockKBRetrieverTool(
    knowledge_base_id="your-kb-id",
    number_of_results=5
)

# Create a CrewAI agent that uses the tool
researcher = Agent(
    role='Knowledge Base Researcher',
    goal='Find information about company policies',
    backstory='I am a researcher specialized in retrieving and analyzing company documentation.',
    tools=[kb_tool],
    verbose=True
)

# Create a task for the agent
research_task = Task(
    description="Find our company's remote work policy and summarize the key points.",
    agent=researcher
)

# Create a crew with the agent
crew = Crew(
    agents=[researcher],
    tasks=[research_task],
    verbose=2
)

# Run the crew
result = crew.kickoff()
print(result)
```

## Tool Arguments

| Argument | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| knowledge_base_id | str | Yes | None | The unique identifier of the knowledge base (0-10 alphanumeric characters) |
| number_of_results | int | No | 5 | Maximum number of results to return |
| retrieval_configuration | dict | No | None | Custom configurations for the knowledge base query |
| guardrail_configuration | dict | No | None | Content filtering settings |
| next_token | str | No | None | Token for pagination |

## Environment Variables

```bash
BEDROCK_KB_ID=your-knowledge-base-id  # Alternative to passing knowledge_base_id
AWS_REGION=your-aws-region            # Defaults to us-east-1
AWS_ACCESS_KEY_ID=your-access-key     # Required for AWS authentication
AWS_SECRET_ACCESS_KEY=your-secret-key # Required for AWS authentication
```

## Response Format

The tool returns results in JSON format:

```json
{
  "results": [
    {
      "content": "Retrieved text content",
      "content_type": "text",
      "source_type": "S3",
      "source_uri": "s3://bucket/document.pdf",
      "score": 0.95,
      "metadata": {
        "additional": "metadata"
      }
    }
  ],
  "nextToken": "pagination-token",
  "guardrailAction": "NONE"
}
```

## Advanced Usage

### Custom Retrieval Configuration

```python
kb_tool = BedrockKBRetrieverTool(
    knowledge_base_id="your-kb-id",
    retrieval_configuration={
        "vectorSearchConfiguration": {
            "numberOfResults": 10,
            "overrideSearchType": "HYBRID"
        }
    }
)

policy_expert = Agent(
    role='Policy Expert',
    goal='Analyze company policies in detail',
    backstory='I am an expert in corporate policy analysis with deep knowledge of regulatory requirements.',
    tools=[kb_tool]
)
```

## Supported Data Sources

- Amazon S3
- Confluence
- Salesforce
- SharePoint
- Web pages
- Custom document locations
- Amazon Kendra
- SQL databases    

## Use Cases

### Enterprise Knowledge Integration
- Enable CrewAI agents to access your organization's proprietary knowledge without exposing sensitive data
- Allow agents to make decisions based on your company's specific policies, procedures, and documentation
- Create agents that can answer questions based on your internal documentation while maintaining data security

### Specialized Domain Knowledge
- Connect CrewAI agents to domain-specific knowledge bases (legal, medical, technical) without retraining models
- Leverage existing knowledge repositories that are already maintained in your AWS environment
- Combine CrewAI's reasoning with domain-specific information from your knowledge bases

### Data-Driven Decision Making
- Ground CrewAI agent responses in your actual company data rather than general knowledge
- Ensure agents provide recommendations based on your specific business context and documentation
- Reduce hallucinations by retrieving factual information from your knowledge bases

### Scalable Information Access
- Access terabytes of organizational knowledge without embedding it all into your models
- Dynamically query only the relevant information needed for specific tasks
- Leverage AWS's scalable infrastructure to handle large knowledge bases efficiently

### Compliance and Governance
- Ensure CrewAI agents provide responses that align with your company's approved documentation
- Create auditable trails of information sources used by your agents
- Maintain control over what information sources your agents can access