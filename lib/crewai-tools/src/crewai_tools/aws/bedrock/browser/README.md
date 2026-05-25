# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/aws/bedrock/browser/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/aws/bedrock/browser/README.md`

## 한글 요약

AWS Bedrock 브라우저 도구 이 도구 키트는 AWS Bedrock 브라우저를 통해 웹 브라우저와 상호 작용하기 위한 도구 세트를 제공합니다. 이를 통해 CrewAI 에이전트는 웹사이트 탐색, 콘텐츠 추출, 요소 클릭 등을 수행할 수 있습니다. 기능 URL 탐색 및 웹 탐색 페이지에서 텍스트 및 하이퍼링크 추출 CSS 선택기를 사용하여 요소 클릭 브라우저 기록을 통해 뒤로 탐색 현재 웹페이지에 대한 정보 가져오기 스레드 기반 격리를 사용하는 다중 브라우저 세션 설치 필요한 종속성이 있는지 확인하십시오: 사용법 기본 사용법 사용 가능한 도구 도구 키트는 다음 도구를 제공합니다. 1. 브라우저 탐색 URL로 이동 2. 요소 클릭 CSS 선택기를 사용하여 요소 클릭 3. 텍스트 추출 현재 웹페이지에서 모든 텍스트 추출 4. 하이퍼링크 추출 현재 웹페이지에서 모든 하이퍼링크 추출 웹페이지 5. 요소 가져오기 CSS 선택기와 일치하는 요소 가져오기 6. 뒤로 탐색 이전 페이지로 이동 7. 현재 웹페이지 현재 웹페이지에 대한 정보 가져오기 고급

## 핵심 발췌

사용(비동기) 요구 사항 Bedrock AgentCore API에 액세스할 수 있는 AWS 계정 적절하게 구성된 AWS 자격 증명

## 원문 내용

# AWS Bedrock Browser Tools

This toolkit provides a set of tools for interacting with web browsers through AWS Bedrock Browser. It enables your CrewAI agents to navigate websites, extract content, click elements, and more.

## Features

- Navigate to URLs and browse the web
- Extract text and hyperlinks from pages
- Click on elements using CSS selectors
- Navigate back through browser history
- Get information about the current webpage
- Multiple browser sessions with thread-based isolation

## Installation

Ensure you have the necessary dependencies:

```bash
uv add crewai-tools bedrock-agentcore beautifulsoup4 playwright nest-asyncio
```

## Usage

### Basic Usage

```python
from crewai import Agent, Task, Crew, LLM
from crewai_tools.aws.bedrock.browser import create_browser_toolkit

# Create the browser toolkit
toolkit, browser_tools = create_browser_toolkit(region="us-west-2")

# Create the Bedrock LLM
llm = LLM(
    model="bedrock/us.anthropic.claude-3-7-sonnet-20250219-v1:0",
    region_name="us-west-2",
)

# Create a CrewAI agent that uses the browser tools
research_agent = Agent(
    role="Web Researcher",
    goal="Research and summarize web content",
    backstory="You're an expert at finding information online.",
    tools=browser_tools,
    llm=llm
)

# Create a task for the agent
research_task = Task(
    description="Navigate to https://example.com and extract all text content. Summarize the main points.",
    expected_output="A list of bullet points containing the most important information on https://example.com. Plus, a description of the tool calls used, and actions performed to get to the page.",
    agent=research_agent
)

# Create and run the crew
crew = Crew(
    agents=[research_agent],
    tasks=[research_task]
)
result = crew.kickoff()

print(f"\n***Final result:***\n\n{result}")

# Clean up browser resources when done
toolkit.sync_cleanup()
```

### Available Tools

The toolkit provides the following tools:

1. `navigate_browser` - Navigate to a URL
2. `click_element` - Click on an element using CSS selectors
3. `extract_text` - Extract all text from the current webpage
4. `extract_hyperlinks` - Extract all hyperlinks from the current webpage
5. `get_elements` - Get elements matching a CSS selector
6. `navigate_back` - Navigate to the previous page
7. `current_webpage` - Get information about the current webpage

### Advanced Usage (with async)

```python
import asyncio
from crewai import Agent, Task, Crew, LLM
from crewai_tools.aws.bedrock.browser import create_browser_toolkit

async def main():

    # Create the browser toolkit with specific AWS region
    toolkit, browser_tools = create_browser_toolkit(region="us-west-2")
    tools_by_name = toolkit.get_tools_by_name()

    # Create the Bedrock LLM
    llm = LLM(
        model="bedrock/us.anthropic.claude-3-7-sonnet-20250219-v1:0",
        region_name="us-west-2",
    )

    # Create agents with specific tools
    navigator_agent = Agent(
        role="Navigator",
        goal="Find specific information across websites",
        backstory="You navigate through websites to locate information.",
        tools=[
            tools_by_name["navigate_browser"],
            tools_by_name["click_element"],
            tools_by_name["navigate_back"]
        ],
        llm=llm
    )

    content_agent = Agent(
        role="Content Extractor",
        goal="Extract and analyze webpage content",
        backstory="You extract and analyze content from webpages.",
        tools=[
            tools_by_name["extract_text"],
            tools_by_name["extract_hyperlinks"],
            tools_by_name["get_elements"]
        ],
        llm=llm
    )

    # Create tasks for the agents
    navigation_task = Task(
        description="Navigate to https://example.com, then click on the the 'More information...' link.",
        expected_output="The status of the tool calls for this task.",
        agent=navigator_agent,
    )

    extraction_task = Task(
        description="Extract all text from the current page and summarize it.",
        expected_output="The summary of the page, and a description of the tool calls used, and actions performed to get to the page.",
        agent=content_agent,
    )

    # Create and run the crew
    crew = Crew(
        agents=[navigator_agent, content_agent],
        tasks=[navigation_task, extraction_task]
    )

    result = await crew.kickoff_async()

    # Clean up browser resources when done
    toolkit.sync_cleanup()

    return result

if __name__ == "__main__":
    result = asyncio.run(main())
    print(f"\n***Final result:***\n\n{result}")
```

## Requirements

- AWS account with access to Bedrock AgentCore API
- Properly configured AWS credentials