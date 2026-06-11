# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/tools/composio_tool/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/tools/composio_tool/README.md`

## 한글 요약

ComposioTool 문서 설명 이 도구는 composio 도구 세트에 대한 래퍼이며 에이전트가 composio SDK의 다양한 도구에 액세스할 수 있도록 해줍니다. 설치 이 도구를 프로젝트에 통합하려면 아래 설치 지침을 따르십시오. 설치가 완료된 후 composio login을 실행하거나 composio API 키를 COMPOSIO API KEY로 내보내십시오. 예 다음 예는 도구를 초기화하고 github 작업을 실행하는 방법을 보여줍니다. 1. 도구 세트 초기화 사용하려는 작업을 모르는 경우 앱 및 태그 필터에서 관련 작업을 가져오거나 사용 사례를 사용하여 관련 작업을 검색합니다. 2. 에이전트 정의 3. 작업 실행 더 자세한 도구 목록은 여기에서 확인할 수 있습니다.

## 핵심 발췌

ComposioTool Documentation ## 설명 이 도구는 composio 도구 세트의 래퍼이며 에이전트가 composio SDK의 다양한 도구에 액세스할 수 있도록 해줍니다. ## 설치 이 도구를 통합하려면 i

## 원문 내용

# ComposioTool Documentation

## Description

This tools is a wrapper around the composio toolset and gives your agent access to a wide variety of tools from the composio SDK.

## Installation

To incorporate this tool into your project, follow the installation instructions below:

```shell
pip install composio-core 
pip install 'crewai[tools]'
```

after the installation is complete, either run `composio login` or export your composio API key as `COMPOSIO_API_KEY`.

## Example

The following example demonstrates how to initialize the tool and execute a github action:

1. Initialize toolset

```python
from composio import App
from crewai_tools import ComposioTool
from crewai import Agent, Task


tools = [ComposioTool.from_action(action=Action.GITHUB_ACTIVITY_STAR_REPO_FOR_AUTHENTICATED_USER)]
```

If you don't know what action you want to use, use `from_app` and `tags` filter to get relevant actions

```python
tools = ComposioTool.from_app(App.GITHUB, tags=["important"])
```

or use `use_case` to search relevant actions

```python
tools = ComposioTool.from_app(App.GITHUB, use_case="Star a github repository")
```

2. Define agent

```python
crewai_agent = Agent(
    role="Github Agent",
    goal="You take action on Github using Github APIs",
    backstory=(
        "You are AI agent that is responsible for taking actions on Github "
        "on users behalf. You need to take action on Github using Github APIs"
    ),
    verbose=True,
    tools=tools,
)
```

3. Execute task

```python
task = Task(
    description="Star a repo ComposioHQ/composio on GitHub",
    agent=crewai_agent,
    expected_output="if the star happened",
)

task.execute()
```

* More detailed list of tools can be found [here](https://app.composio.dev)