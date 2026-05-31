# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/apify_actors_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/apify_actors_tool/README.md`

## 한글 요약

ApifyActorsTool Apify Actor를 CrewAI 워크플로에 통합합니다. 설명 ApifyActorsTool은 웹 스크래핑 및 자동화를 위한 클라우드 기반 프로그램인 Apify Actors를 CrewAI 워크플로에 연결합니다. 소셜 미디어, 검색 엔진, 온라인 지도, 전자 상거래 사이트, 여행 포털 또는 일반 웹사이트에서 데이터를 추출하는 등의 사용 사례에 Apify Store의 4,000개 이상의 Actor를 사용하세요. 자세한 내용은 Apify 설명서의 Apify CrewAI 통합을 참조하세요. 설치 ApifyActorsTool을 사용하려면 필요한 패키지를 설치하고 Apify API 토큰을 설정하세요. 토큰을 얻는 단계는 Apify API 문서를 따르세요. 단계 1. 종속성 설치 Crewai[tools] 및 langchain apify 설치: 2. API 토큰 설정 토큰을 환경 변수로 내보내기: 사용 예 ApifyActorsTool을 사용하여 RAG 웹 브라우저 Actor를 수동으로 실행하여 웹 검색을 수행합니다. 예상 출력 다음은 위 코드 실행의 출력입니다. ApifyActorsTool은 자동으로 Actor 정의를 가져오고

## 핵심 발췌

제공된 행위자 이름을 사용하여 Apify의 입력 스키마를 사용한 다음 도구 설명 및 인수 스키마를 구성합니다. 즉, 유효한 행위자 이름만 지정하면 되며 에이전트와 함께 사용할 때 도구가 나머지를 처리하므로 실행 입력을 지정할 필요가 없습니다. 작동 방식은 다음과 같습니다. 간단히 액터 이름을 변경하고 수동으로 사용할 경우 액터 입력 스키마에 따라 실행 입력을 조정하여 Apify Store에서 다른 액터를 실행할 수 있습니다. 에이전트 사용 예시는 CrewAI Actor 템플릿을 참조하세요. 구성 ApifyActorsTool이 작동하려면 다음 입력이 필요합니다. 행위자 이름 실행할 Apify 행위자의 ID입니다(예: "apify/rag 웹 브라우저"). Apify Store에서 모든 Actor를 찾아보세요. 실행 입력 도구를 수동으로 실행할 때 액터에 대한 입력 매개변수 사전입니다. 예를 들어 apify의 경우/

## 원문 내용

# ApifyActorsTool

Integrate [Apify Actors](https://apify.com/actors) into your CrewAI workflows.

## Description

The `ApifyActorsTool` connects [Apify Actors](https://apify.com/actors), cloud-based programs for web scraping and automation, to your CrewAI workflows.
Use any of the 4,000+ Actors on [Apify Store](https://apify.com/store) for use cases such as extracting data from social media, search engines, online maps, e-commerce sites, travel portals, or general websites.

For details, see the [Apify CrewAI integration](https://docs.apify.com/platform/integrations/crewai) in Apify documentation.

## Installation

To use `ApifyActorsTool`, install the necessary packages and set up your Apify API token. Follow the [Apify API documentation](https://docs.apify.com/platform/integrations/api) for steps to obtain the token.

### Steps

1. **Install dependencies**
   Install `crewai[tools]` and `langchain-apify`:
   ```bash
   pip install 'crewai[tools]' langchain-apify
   ```

2. **Set your API token**
   Export the token as an environment variable:
   ```bash
   export APIFY_API_TOKEN='your-api-token-here'
   ```

## Usage example

Use the `ApifyActorsTool` manually to run the [RAG Web Browser Actor](https://apify.com/apify/rag-web-browser) to perform a web search:

```python
from crewai_tools import ApifyActorsTool

# Initialize the tool with an Apify Actor
tool = ApifyActorsTool(actor_name="apify/rag-web-browser")

# Run the tool with input parameters
results = tool.run(run_input={"query": "What is CrewAI?", "maxResults": 5})

# Process the results
for result in results:
    print(f"URL: {result['metadata']['url']}")
    print(f"Content: {result.get('markdown', 'N/A')[:100]}...")
```

### Expected output

Here is the output from running the code above:

```text
URL: https://www.example.com/crewai-intro
Content: CrewAI is a framework for building AI-powered workflows...
URL: https://docs.crewai.com/
Content: Official documentation for CrewAI...
```

The `ApifyActorsTool` automatically fetches the Actor definition and input schema from Apify using the provided `actor_name` and then constructs the tool description and argument schema. This means you need to specify only a valid `actor_name`, and the tool handles the rest when used with agents—no need to specify the `run_input`. Here's how it works:

```python
from crewai import Agent
from crewai_tools import ApifyActorsTool

rag_browser = ApifyActorsTool(actor_name="apify/rag-web-browser")

agent = Agent(
    role="Research Analyst",
    goal="Find and summarize information about specific topics",
    backstory="You are an experienced researcher with attention to detail",
    tools=[rag_browser],
)
```

You can run other Actors from [Apify Store](https://apify.com/store) simply by changing the `actor_name` and, when using it manually, adjusting the `run_input` based on the Actor input schema.

For an example of usage with agents, see the [CrewAI Actor template](https://apify.com/templates/python-crewai).

## Configuration

The `ApifyActorsTool` requires these inputs to work:

- **`actor_name`**
  The ID of the Apify Actor to run, e.g., `"apify/rag-web-browser"`. Browse all Actors on [Apify Store](https://apify.com/store).
- **`run_input`**
  A dictionary of input parameters for the Actor when running the tool manually.
  - For example, for the `apify/rag-web-browser` Actor: `{"query": "search term", "maxResults": 5}`
  - See the Actor's [input schema](https://apify.com/apify/rag-web-browser/input-schema) for the list of input parameters.

## Resources

- **[Apify](https://apify.com/)**: Explore the Apify platform.
- **[How to build an AI agent on Apify](https://blog.apify.com/how-to-build-an-ai-agent/)** - A complete step-by-step guide to creating, publishing, and monetizing AI agents on the Apify platform.
- **[RAG Web Browser Actor](https://apify.com/apify/rag-web-browser)**: A popular Actor for web search for LLMs.
- **[CrewAI Integration Guide](https://docs.apify.com/platform/integrations/crewai)**: Follow the official guide for integrating Apify and CrewAI.