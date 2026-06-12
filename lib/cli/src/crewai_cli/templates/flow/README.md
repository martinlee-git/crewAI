# 읽어보기

- 원문 저장소: `crewAIInc/crewAI`
- 미러 저장소: `martinlee-git/crewAI`
- 원문 문서: https://github.com/crewAIInc/crewAI/blob/main/lib/cli/src/crewai_cli/templates/flow/README.md
- 미러 경로: `lib/cli/src/crewai_cli/templates/flow/README.md`

## 한글 요약

{{crew name}} 크루 CrewAI가 제공하는 {{crew name}} 크루 프로젝트에 오신 것을 환영합니다. 이 템플릿은 CrewAI가 제공하는 강력하고 유연한 프레임워크를 활용하여 다중 에이전트 AI 시스템을 쉽게 설정할 수 있도록 설계되었습니다. 우리의 목표는 귀하의 상담원이 복잡한 작업에 효과적으로 협업하여 집단 지성과 능력을 극대화할 수 있도록 하는 것입니다. 설치 시스템에 Python =3.10 <3.14가 설치되어 있는지 확인하십시오. 이 프로젝트는 종속성 관리 및 패키지 처리에 UV를 사용하여 원활한 설정 및 실행 환경을 제공합니다. 먼저 uv를 설치하지 않은 경우 다음으로 프로젝트 디렉터리로 이동하여 종속성을 설치합니다. (선택 사항) CLI 명령을 사용하여 종속성을 잠그고 설치합니다. 사용자 정의 OPENAI API 키를 .env 파일에 추가 src/{{folder name}}/config/agents.yaml을 수정하여 에이전트 정의 src/{{folder name}}/config/tasks.yaml을 수정하여 작업 정의 src/{{folder 수정 name}}/crew.py를 사용하여 자신만의 논리를 추가하세요.

## 핵심 발췌

ols 및 특정 인수 src/{{folder name}}/main.py를 수정하여 에이전트 및 작업에 대한 사용자 지정 입력을 추가합니다. 프로젝트 실행 흐름을 시작하고 실행을 시작하려면 프로젝트의 루트 폴더에서 다음을 실행합니다. 이 명령은 구성에 정의된 대로 {{name}} 흐름을 초기화합니다. 수정되지 않은 이 예제는 AI 에이전트에서 콘텐츠 생성 흐름을 실행하고 출력을 output/post.md에 저장합니다. 조직 이해하기 {{name}} 조직은 각각 고유한 역할, 목표 및 도구를 가진 여러 AI 에이전트로 구성됩니다. 이러한 에이전트는 config/tasks.yaml에 정의된 일련의 작업에서 공동 작업을 수행하며 집단적 기술을 활용하여 복잡한 목표를 달성합니다. config/agents.yaml 파일은 팀의 각 에이전트의 기능과 구성을 간략하게 설명합니다. 지원 지원, 질문 또는

## 원문 내용

# {{crew_name}} Crew

Welcome to the {{crew_name}} Crew project, powered by [crewAI](https://crewai.com). This template is designed to help you set up a multi-agent AI system with ease, leveraging the powerful and flexible framework provided by crewAI. Our goal is to enable your agents to collaborate effectively on complex tasks, maximizing their collective intelligence and capabilities.

## Installation

Ensure you have Python >=3.10 <3.14 installed on your system. This project uses [UV](https://docs.astral.sh/uv/) for dependency management and package handling, offering a seamless setup and execution experience.

First, if you haven't already, install uv:

```bash
pip install uv
```

Next, navigate to your project directory and install the dependencies:

(Optional) Lock the dependencies and install them by using the CLI command:
```bash
crewai install
```

### Customizing

**Add your `OPENAI_API_KEY` into the `.env` file**

- Modify `src/{{folder_name}}/config/agents.yaml` to define your agents
- Modify `src/{{folder_name}}/config/tasks.yaml` to define your tasks
- Modify `src/{{folder_name}}/crew.py` to add your own logic, tools and specific args
- Modify `src/{{folder_name}}/main.py` to add custom inputs for your agents and tasks

## Running the Project

To kickstart your flow and begin execution, run this from the root folder of your project:

```bash
crewai run
```

This command initializes the {{name}} Flow as defined in your configuration.

This example, unmodified, will run a content creation flow on AI Agents and save the output to `output/post.md`.

## Understanding Your Crew

The {{name}} Crew is composed of multiple AI agents, each with unique roles, goals, and tools. These agents collaborate on a series of tasks, defined in `config/tasks.yaml`, leveraging their collective skills to achieve complex objectives. The `config/agents.yaml` file outlines the capabilities and configurations of each agent in your crew.

## Support

For support, questions, or feedback regarding the {{crew_name}} Crew or crewAI.

- Visit our [documentation](https://docs.crewai.com)
- Reach out to us through our [GitHub repository](https://github.com/joaomdmoura/crewai)
- [Join our Discord](https://discord.com/invite/X4JWnZnxPb)
- [Chat with our docs](https://chatg.pt/DWjSBZn)

Let's create wonders together with the power and simplicity of crewAI.