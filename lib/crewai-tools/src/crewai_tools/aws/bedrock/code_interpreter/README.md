# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/crewai-tools/src/crewai_tools/aws/bedrock/code_interpreter/README.md
- 미러 경로: `lib/crewai-tools/src/crewai_tools/aws/bedrock/code_interpreter/README.md`

## 한글 요약

AWS Bedrock 코드 해석기 도구 이 도구 키트는 AWS Bedrock 코드 해석기 환경과 상호 작용하기 위한 도구 세트를 제공합니다. 이를 통해 CrewAI 에이전트는 안전하고 격리된 환경에서 코드를 실행하고, 셸 명령을 실행하고, 파일을 관리하고, 계산 작업을 수행할 수 있습니다. 기능 다양한 언어로 코드 실행(주로 Python) 환경에서 셸 명령 실행 파일 읽기, 쓰기, 나열 및 삭제 장기 실행 작업을 비동기식으로 관리 스레드 기반 격리를 통한 다중 코드 해석기 세션 설치 필요한 종속성이 있는지 확인: 사용법 기본 사용법 사용 가능한 도구 도구 키트는 다음 도구를 제공합니다. 1. 코드 실행 다양한 언어(주로 Python)로 코드 실행 2. 명령 실행 환경에서 셸 명령 실행 3. 파일 읽기 환경에서 파일 내용 읽기 4. 파일 나열 디렉터리의 파일 나열 5. 파일 삭제 제거 환경의 파일 6. 파일 쓰기 파일 생성 또는 업데이트 7. 명령 실행 시작 Lo 시작

## 핵심 발췌

ng 비동기식 명령 실행 8. 작업 가져오기 비동기 작업 상태 확인 9. 작업 중지 작업 실행 중지 고급 사용 예: Python 리소스 정리를 통한 데이터 분석 리소스 누출을 방지하기 위해 완료되면 항상 코드 해석기 리소스 정리: 요구 사항 Bedrock AgentCore API에 액세스할 수 있는 AWS 계정 적절하게 구성된 AWS 자격 증명

## 원문 내용

# AWS Bedrock Code Interpreter Tools

This toolkit provides a set of tools for interacting with the AWS Bedrock Code Interpreter environment. It enables your CrewAI agents to execute code, run shell commands, manage files, and perform computational tasks in a secure, isolated environment.

## Features

- Execute code in various languages (primarily Python)
- Run shell commands in the environment
- Read, write, list, and delete files
- Manage long-running tasks asynchronously
- Multiple code interpreter sessions with thread-based isolation

## Installation

Ensure you have the necessary dependencies:

```bash
uv add crewai-tools bedrock-agentcore
```

## Usage

### Basic Usage

```python
from crewai import Agent, Task, Crew, LLM
from crewai_tools.aws import create_code_interpreter_toolkit

# Create the code interpreter toolkit
toolkit, code_tools = create_code_interpreter_toolkit(region="us-west-2")

# Create the Bedrock LLM
llm = LLM(
    model="bedrock/us.anthropic.claude-3-7-sonnet-20250219-v1:0",
    region_name="us-west-2",
)

# Create a CrewAI agent that uses the code interpreter tools
developer_agent = Agent(
    role="Python Developer",
    goal="Create and execute Python code to solve problems.",
    backstory="You're a skilled Python developer with expertise in data analysis.",
    tools=code_tools,
    llm=llm
)

# Create a task for the agent
coding_task = Task(
    description="Write a Python function that calculates the factorial of a number and test it. Do not use any imports from outside the Python standard library.",
    expected_output="The Python function created, and the test results.",
    agent=developer_agent
)

# Create and run the crew
crew = Crew(
    agents=[developer_agent],
    tasks=[coding_task]
)
result = crew.kickoff()

print(f"\n***Final result:***\n\n{result}")

# Clean up resources when done
import asyncio
asyncio.run(toolkit.cleanup())
```

### Available Tools

The toolkit provides the following tools:

1. `execute_code` - Run code in various languages (primarily Python)
2. `execute_command` - Run shell commands in the environment
3. `read_files` - Read content of files in the environment
4. `list_files` - List files in directories
5. `delete_files` - Remove files from the environment
6. `write_files` - Create or update files
7. `start_command_execution` - Start long-running commands asynchronously
8. `get_task` - Check status of async tasks
9. `stop_task` - Stop running tasks

### Advanced Usage

```python
from crewai import Agent, Task, Crew, LLM
from crewai_tools.aws import create_code_interpreter_toolkit

# Create the code interpreter toolkit
toolkit, code_tools = create_code_interpreter_toolkit(region="us-west-2")
tools_by_name = toolkit.get_tools_by_name()

# Create the Bedrock LLM
llm = LLM(
    model="bedrock/us.anthropic.claude-3-7-sonnet-20250219-v1:0",
    region_name="us-west-2",
)

# Create agents with specific tools
code_agent = Agent(
    role="Code Developer",
    goal="Write and execute code",
    backstory="You write and test code to solve complex problems.",
    tools=[
        # Use specific tools by name
        tools_by_name["execute_code"],
        tools_by_name["execute_command"],
        tools_by_name["read_files"],
        tools_by_name["write_files"]
    ],
    llm=llm
)

file_agent = Agent(
    role="File Manager",
    goal="Manage files in the environment",
    backstory="You help organize and manage files in the code environment.",
    tools=[
        # Use specific tools by name
        tools_by_name["list_files"],
        tools_by_name["read_files"],
        tools_by_name["write_files"],
        tools_by_name["delete_files"]
    ],
    llm=llm
)

# Create tasks for the agents
coding_task = Task(
    description="Write a Python script to analyze data from a CSV file. Do not use any imports from outside the Python standard library.",
    expected_output="The Python function created.",
    agent=code_agent
)

file_task = Task(
    description="Organize the created files into separate directories.",
    agent=file_agent
)

# Create and run the crew
crew = Crew(
    agents=[code_agent, file_agent],
    tasks=[coding_task, file_task]
)
result = crew.kickoff()

print(f"\n***Final result:***\n\n{result}")

# Clean up code interpreter resources when done
import asyncio
asyncio.run(toolkit.cleanup())
```

### Example: Data Analysis with Python

```python
from crewai import Agent, Task, Crew, LLM
from crewai_tools.aws import create_code_interpreter_toolkit

# Create toolkit and tools
toolkit, code_tools = create_code_interpreter_toolkit(region="us-west-2")

# Create the Bedrock LLM
llm = LLM(
    model="bedrock/us.anthropic.claude-3-7-sonnet-20250219-v1:0",
    region_name="us-west-2",
)

# Create a data analyst agent
analyst_agent = Agent(
    role="Data Analyst",
    goal="Analyze data using Python",
    backstory="You're an expert data analyst who uses Python for data processing.",
    tools=code_tools,
    llm=llm
)

# Create a task for the agent
analysis_task = Task(
    description="""
    For all of the below, do not use any imports from outside the Python standard library.
    1. Create a sample dataset with random data
    2. Perform statistical analysis on the dataset
    3. Generate visualizations of the results
    4. Save the results and visualizations to files
    """,
    agent=analyst_agent
)

# Create and run the crew
crew = Crew(
    agents=[analyst_agent],
    tasks=[analysis_task]
)
result = crew.kickoff()

print(f"\n***Final result:***\n\n{result}")

# Clean up resources
import asyncio
asyncio.run(toolkit.cleanup())
```

## Resource Cleanup

Always clean up code interpreter resources when done to prevent resource leaks:

```python
import asyncio

# Clean up all code interpreter sessions
asyncio.run(toolkit.cleanup())
```

## Requirements

- AWS account with access to Bedrock AgentCore API
- Properly configured AWS credentials